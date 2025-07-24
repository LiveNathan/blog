Picking up from where we left off on the last blog post, I created a new project and copied in the OverlapSaveAdapter
and Convolution interface. Then I added a new interface method to handled multiple kernels and an object to carry them:

`double[] with(double[] signal, List<KernelSwitch> kernelSwitches);`

Since I often get nervous about what to do next (AM I DOING IT RIGHT???) I like to follow prescriptions like ZOMBIES.
Let's use that to TDD ourselves to glory.

We'll start with the zero case that should simply throw an exception and make that pass.

```java
@Test
void givenEmptyKernels_whenConvolving_thenThrowsException() {
    double[] signal = {1, 2, 3};
    List<double[]> emptyKernels = List.of();

    assertThatThrownBy(() -> convolution.with(signal, emptyKernels, 2))
            .isInstanceOf(IllegalArgumentException.class)
            .hasMessageContaining("kernels cannot be empty");
}
```

Then we'll do the "one" case, which are almost exactly the same as our previous tests:

```java
@Test
void givenSingleImpulseKernel_whenConvolvingWithCollection_thenReturnsIdentity() {
    double[] signal = {1};
    double[] kernel = {1};

    double[] actual = convolution.with(signal, List.of(kernel), 1);

    assertThat(actual).isEqualTo(kernel);
}
```

Now we get to the meat, the many case:

```java
@Test
void givenMultipleKernels_whenConvolving_thenAppliesCorrectKernelAtEachSampleIndex() {
    double[] signal = {1, 1, 1, 1}; // Simple signal for easy verification
    double[] kernel1 = {0.5}; // First kernel
    double[] kernel2 = {2.0}; // Second kernel

    List<double[]> kernelSwitches = List.of(kernel1, kernel2);

    double[] actual = convolution.with(signal, kernelSwitches, 2);

    // Expected: first two samples convolved with kernel1 (0.5), remaining samples with kernel2 (2.0)
    double[] expected = {0.5, 0.5, 2.0, 2.0};
    assertThat(actual).usingElementComparator(doubleComparator())
            .containsExactly(expected);
}
```

This one will be a little tricky to get to pass. My first idea is to simply segment the signal based on kernel switch
points and convolve each segment separately with the appropriate kernel, then combine the results in the end. Let's call
this the first naive solution.

```java
@Override
public double[] with(double[] signal, List<double[]> kernels, int periodSamples) {
    if (kernels.isEmpty()) {
        throw new IllegalArgumentException("kernels cannot be empty");
    }
    int kernelLength = kernels.getFirst().length;
    if (kernels.stream().anyMatch(kernel -> kernel.length != kernelLength)) {
        throw new IllegalArgumentException("all kernels must have the same length");
    }

    int resultLength = signal.length + kernelLength - 1;
    double[] result = new double[Math.max(resultLength, signal.length)];

    // Process each segment with its corresponding kernel
    for (int i = 0; i < kernels.size(); i++) {
        int startIndex = i * periodSamples;
        int endIndex = Math.min((i + 1) * periodSamples, signal.length);

        if (startIndex < signal.length && endIndex > startIndex) {
            // Extract signal segment
            double[] segment = new double[endIndex - startIndex];
            System.arraycopy(signal, startIndex, segment, 0, segment.length);

            // Convolve a segment with current kernel
            double[] segmentResult = with(segment, kernels.get(i));

            // Copy result back, handling overlap
            int copyLength = Math.min(segmentResult.length, result.length - startIndex);
            System.arraycopy(segmentResult, 0, result, startIndex, copyLength);
        }
    }

    return result;
}
```

The tests pass! But, that was a little too easy? I get the feeling that we are ignoring the effects of convolution
around the kernel transition region. Let's write a test to prove this.

Let's write a failing test to prove this.

```java

@Test
void givenKernelSwitchAtBoundary_whenConvolving_thenHandlesTransitionProperly() {
    double[] signal = {1, 1, 1, 1};
    double[] kernel1 = {1, 1}; // Active for output samples 0-1
    double[] kernel2 = {2, 2}; // Active for output samples 2+
    List<double[]> kernels = List.of(kernel1, kernel2);

    double[] actual = convolution.with(signal, kernels, 2);

    /*
     * output[0]: Use kernel1 (sample 0 → period 0)
     *   = signal[0] * kernel1[0] + signal[-1] * kernel1[1]
     *   = 1 * 1 + 0 * 1 = 1
     *
     * output[1]: Use kernel1 (sample 1 → period 0)
     *   = signal[1] * kernel1[0] + signal[0] * kernel1[1]
     *   = 1 * 1 + 1 * 1 = 2
     *
     * output[2]: Use kernel2 (sample 2 → period 1) ← TRANSITION OCCURS HERE
     *   = signal[2] * kernel2[0] + signal[1] * kernel2[1]
     *   = 1 * 2 + 1 * 2 = 4
     *
     * output[3]: Use kernel2 (sample 3 → period 1)
     *   = signal[3] * kernel2[0] + signal[2] * kernel2[1]
     *   = 1 * 2 + 1 * 2 = 4
     *
     * output[4]: Use kernel1 (cycles back)
     *   = signal[4] * 1 + signal[3] * 1
     *   = 0 * 1 + 1 * 1 = 1
     */

    double[] expected = {1, 2, 4, 4, 1};
    assertThat(actual).hasSize(5);
    assertThat(actual).usingElementComparator(doubleComparator())
            .containsExactly(expected);
}
```

Here's an idea: divide and conquer. Us the OLS method as the default. If the next processing block contains multiple
kernels, switch to time domain convolution where we have fine grained control over every sample.

```java

@Override
public double[] with(double[] signal, List<KernelSwitch> kernelSwitches) {
    if (kernelSwitches.isEmpty()) {
        throw new IllegalArgumentException("kernel switches cannot be empty");
    }

    // Validate and sort switches
    int kernelLength = kernelSwitches.getFirst().kernel().length;
    for (KernelSwitch ks : kernelSwitches) {
        if (ks.kernel().length != kernelLength) {
            throw new IllegalArgumentException("all kernels must have the same length");
        }
    }

    List<KernelSwitch> sortedSwitches = kernelSwitches.stream()
            .sorted(Comparator.comparingInt(KernelSwitch::sampleIndex))
            .toList();

    SignalTransformer.validate(signal, sortedSwitches.getFirst().kernel());

    // If there's only one kernel, use standard OLS
    if (sortedSwitches.size() == 1) {
        return with(signal, sortedSwitches.getFirst().kernel());
    }

    int resultLength = signal.length + kernelLength - 1;
    double[] result = new double[resultLength];

    // Pre-compute FFTs of all kernels
    int fftSize = calculateOptimalFftSize(signal.length, kernelLength);
    Complex[][] kernelTransforms = new Complex[sortedSwitches.size()][];
    for (int i = 0; i < sortedSwitches.size(); i++) {
        double[] paddedKernel = SignalTransformer.pad(sortedSwitches.get(i).kernel(), fftSize);
        kernelTransforms[i] = SignalTransformer.fft(paddedKernel);
    }

    // Process using modified OLS that switches kernels
    int blockSize = fftSize - kernelLength + 1;
    int blockStartIndex = kernelLength - 1;

    // Pad signal
    double[] paddedSignal = SignalTransformer.pad(
            signal,
            blockStartIndex,
            resultLength - signal.length - blockStartIndex
    );

    // Process blocks
    int totalBlocks = (signal.length + blockSize - 1) / blockSize;
    for (int blockIndex = 0; blockIndex < totalBlocks; blockIndex++) {
        int outputStart = blockIndex * blockSize;

        // Extract block
        double[] block = extractSignalBlock(paddedSignal, outputStart, fftSize);
        Complex[] blockTransform = SignalTransformer.fft(block);

        // Find which kernels are active in this block's output range
        int blockOutputEnd = Math.min(outputStart + blockSize, resultLength);
        boolean multipleKernels = false;
        int firstKernelIdx = -1;

        for (int n = outputStart; n < blockOutputEnd; n++) {
            int kernelIdx = findKernelIndex(n, sortedSwitches);
            if (firstKernelIdx == -1) {
                firstKernelIdx = kernelIdx;
            } else if (kernelIdx != firstKernelIdx) {
                multipleKernels = true;
                break;
            }
        }

        if (!multipleKernels) {
            // Single kernel for the entire block-use standard OLS
            Complex[] convolutionTransform = SignalTransformer.multiply(
                    blockTransform, kernelTransforms[firstKernelIdx]
            );
            double[] blockResult = SignalTransformer.ifft(convolutionTransform);

            int validLength = Math.min(blockSize, resultLength - outputStart);
            System.arraycopy(blockResult, blockStartIndex, result, outputStart, validLength);
        } else {
            // Multiple kernels in block - use time domain for this block only
            for (int n = outputStart; n < blockOutputEnd; n++) {
                int kernelIdx = findKernelIndex(n, sortedSwitches);
                double[] kernel = sortedSwitches.get(kernelIdx).kernel();

                double sum = 0.0;
                for (int k = 0; k < kernelLength; k++) {
                    int signalIndex = n - k;
                    if (signalIndex >= 0 && signalIndex < signal.length) {
                        sum += signal[signalIndex] * kernel[k];
                    }
                }
                result[n] = sum;
            }
        }
    }

    return result;
}
```

## 6. Crossfades Between Kernels

One of the most challenging aspects of real-time convolution is handling changes in the impulse response. For
applications like GainGuardian that need to switch kernels frequently, smoothly transitioning between impulse responses
is crucial to avoid audible artifacts.

### Why Kernel Crossfades Are Needed

When an impulse response changes suddenly, it can cause audible clicks, pops, or other artifacts in the output signal.
This is especially problematic for applications where parameters are adjusted in real-time, such as:

- Variable acoustic spaces in games
- Dynamic equalization
- Adaptive filtering systems

### Frequency Domain Crossfades

The traditional approach to kernel crossfades involves:

1. Running two parallel convolution processes with different kernels
2. Crossfading their outputs in the time domain

However, this doubles the computational cost. A more efficient approach is to perform the crossfade directly in the
frequency domain.

The frequency domain crossfade technique works as follows:

1. Calculate the FFT of both the current and target kernels
2. Perform a weighted sum of these frequency representations
3. Use the resulting combined frequency representation for convolution

Here's a basic implementation:

```matlab
function y = overlapSaveCrossfade(x, h1, h2, blockSize, crossfadeBlocks)
    % x: input signal
    % h1: initial impulse response
    % h2: target impulse response
    % blockSize: size of each processing block
    % crossfadeBlocks: number of blocks over which to crossfade
    
    M = max(length(h1), length(h2));  % Kernel length
    L = blockSize;                    % Block size
    N = L + M - 1;                    % FFT size
    
    % Zero pad kernels to length N
    h1_padded = [h1; zeros(N - length(h1), 1)];
    h2_padded = [h2; zeros(N - length(h2), 1)];
    
    % FFT of zero-padded kernels
    H1 = fft(h1_padded);
    H2 = fft(h2_padded);
    
    % Prepare for processing
    numBlocks = ceil((length(x) + M - 1) / L);
    x_padded = [zeros(M - 1, 1); x; zeros(numBlocks * L - length(x), 1)];
    y = zeros(length(x_padded) - (M - 1), 1);  % Output signal
    
    % Process each block
    for i = 1:numBlocks
        % Calculate crossfade weight
        if i <= crossfadeBlocks
            alpha = (i - 1) / crossfadeBlocks;  % Linear crossfade
        else
            alpha = 1;
        end
        
        % Create interpolated kernel in frequency domain
        H = (1 - alpha) * H1 + alpha * H2;
        
        % Extract overlapping block
        blockStart = (i - 1) * L + 1;
        xBlock = x_padded(blockStart:(blockStart + N - 1));
        
        % Process in frequency domain
        X = fft(xBlock);
        Y = X .* H;
        yBlock = real(ifft(Y));
        
        % Keep only the valid part (discard first M-1 samples)
        validPart = yBlock(M:end);
        
        % Add to output
        outStart = (i - 1) * L + 1;
        y(outStart:(outStart + L - 1)) = validPart;
    end
    
    % Trim output to match expected output length
    y = y(1:(length(x) + M - 1));
end
```

This approach offers approximately 30% better performance compared to running two separate convolutions and crossfading
in the time domain. It also provides a more elegant solution since everything remains in the frequency domain.

## Real-world Application in Gain Guardian

- Current implementation vs. proposed approach
- Performance comparisons
- Quality considerations

## Java Implementation

- Converting MATLAB prototype to Java
- Testing against MATLAB reference
- Optimizations for Java

## Conclusion

- Summary of findings
- Future explorations
- Community feedback invitation

## Appendix: MATLAB Gripes (optional lighthearted section)

- Development environment limitations
- Alternative approaches