---
layout: post
title: "Overlap Save Method for Frequency Domain Convolution: A Developer's Guide"
date: 2025-07-15 06:00:00 -0000
categories: [ java, signal-processing, audio, convolution, fft, frequency-domain, performance, real-time ]
---

# Overlap Save Method for Frequency Domain Convolution: A Developer's Guide

As a sound engineer turned a software developer, I know a little about audio and a little about signal processing, but
not enough to, say, write a convolution function from scratch. When I reached the point in my work
on [GainGuardian](https://www.gainguardian.com/) where I needed to switch from time domain convolution to frequency
domain convolution, I started looking around for frameworks and examples in Java. Finding nothing that felt readable and
approachable, I decided to write my own.

There are many examples for MATLAB and a few for C and Python, but most materials were either too mathematical or too
abstract.

> C is great for machines, not for people. — Josh Long

Yes, shots fired indeed.

The overlap save method attracted me for two main reasons:

1. Efficiency (compared to overlap-add)
2. Opportunity for crossfading without leaving the frequency domain

This post is my attempt to explain overlap save (and better understand it myself) the way I wish someone had explained
it to me: through working code, step-by-step implementation, and practical examples. We'll build up from time domain
convolution, refactor it into frequency domain approaches, and finally implement overlap save—all while maintaining test
coverage to verify our results.

All the code in this post is available in
the [overlap-save-demo repository](https://github.com/LiveNathan/overlap-save-demo) with complete implementations and
tests.

## Starting Simple: Time Domain Convolution

Whenever I'm trying to learn something complex, I start with the smallest possible step. For convolution, that means
working with impulses—if you convolve any signal with an impulse, you just get the signal back.

I heard that an em dash is an immediate clue that the writing was done by a genie (ChatGPT, claude, etc.). I'm writing
this in Intellij, and it keeps recommending the em dash, so LAY OFF!
(but also, yes, I did rely heavily on the genie to get me through this)

Let's begin with a simple interface and Apache Commons' implementation as our reference:

```java
public interface Convolution {
    double[] with(double[] signal, double[] kernel);
}

public class ApacheAdapter implements Convolution {
    @Override
    public double[] with(double[] signal, double[] kernel) {
        return MathArrays.convolve(signal, kernel);
    }
}
```

Here's how I characterize the behavior with simple tests:

```java

@ParameterizedTest
@MethodSource("allImplementations")
void impulseConvolution_returnsIdentity(Convolution convolution) {
    double[] signal = {1};
    double[] kernel = {1};

    double[] actual = convolution.with(signal, kernel);

    assertThat(actual).isEqualTo(kernel);
}

@ParameterizedTest
@MethodSource("allImplementations")
void twoElementConvolution_computesExpectedValues(Convolution convolution) {
    double[] signal = {1, 0.5};
    double[] kernel = {0.2, 0.1};

    double[] result = convolution.with(signal, kernel);

    assertThat(result.length).isEqualTo(signal.length + kernel.length - 1); // 3
    assertThat(result[0]).isEqualTo(0.2);   // 1 * 0.2
    assertThat(result[1]).isEqualTo(0.2);   // 1 * 0.1 + 0.5 * 0.2  
    assertThat(result[2]).isEqualTo(0.05);  // 0.5 * 0.1
}
```

See the complete test
suite: [ConvolutionTest.java](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/test/java/dev/nathanlively/overlap_save_demo/ConvolutionTest.java)

### Building Our Own Implementation

Rather than writing from scratch, I copied Apache's implementation and refactored it to understand how it works. The
original code is elegant but uses academic variable names and defensive boundary checking that makes it hard to follow:

```java
// Original Apache implementation (simplified)
public static double[] convolve(double[] x, double[] h) {
    for (int n = 0; n < totalLength; n++) {
        double yn = 0;
        int k = Math.max(0, n + 1 - xLen);
        int j = n - k;
        while (k < hLen && j >= 0) {
            yn += x[j--] * h[k++];
        }
        y[n] = yn;
    }
}
```

After refactoring with explicit padding and kernel flipping, the core algorithm becomes much clearer:

```java
public double[] with(double[] signal, double[] kernel) {
    SignalTransformer.validate(signal, kernel);

    final double[] paddedSignal = SignalTransformer.padSymmetric(signal, kernel.length - 1);
    final double[] reversedKernel = reverseKernel(kernel);

    return computeConvolution(paddedSignal, reversedKernel, signal.length);
}

// Core convolution loop - slide kernel over padded signal
private double[] computeConvolution(double[] paddedSignal, double[] reversedKernel, int signalLength) {
    // ... implementation details ...
    for (int outputPos = 0; outputPos < resultLength; outputPos++) {
        result[outputPos] = computeWindowConvolution(paddedSignal, reversedKernel, outputPos, padding, kernelLength);
    }
    return result;
}
```

See the complete
implementation: [TimeDomainAdapter.java](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/main/java/dev/nathanlively/overlap_save_demo/TimeDomainAdapter.java)

This reveals the core concept: convolution is sliding a flipped kernel over a padded signal, computing dot products at
each position. The padding ensures we handle edge cases correctly, and kernel flipping converts correlation into
convolution.

**Performance Check:** Time domain convolution has O(N²) complexity—for every signal sample, we process every
kernel sample. With my 8192-sample kernels and typical audio files, this translates to millions of multiply-accumulate
operations per second of audio.

## Frequency Domain

The convolution theorem states that convolution in time equals multiplication in frequency. This transforms our O(N²)
problem into O(N log N):

```java
public double[] with(double[] signal, double[] kernel) {
    SignalTransformer.validate(signal, kernel);

    int resultLength = signal.length + kernel.length - 1;
    int paddedLength = CommonUtil.nextPowerOfTwo(resultLength);

    // Transform both to frequency domain
    final Complex[] signalTransform = SignalTransformer.fft(SignalTransformer.pad(signal, paddedLength));
    final Complex[] kernelTransform = SignalTransformer.fft(SignalTransformer.pad(kernel, paddedLength));

    // Multiply in frequency domain (equivalent to convolution in time)
    final Complex[] productTransform = SignalTransformer.multiply(signalTransform, kernelTransform);
    final double[] convolutionResult = SignalTransformer.ifft(productTransform);

    return extractValidPortion(convolutionResult, resultLength);
}
```

See the complete
implementation: [FrequencyDomainAdapter.java](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/main/java/dev/nathanlively/overlap_save_demo/FrequencyDomainAdapter.java)

The steps are straightforward:

1. **Pad both inputs** to the next power of two (FFT requirement)
2. **Transform to frequency domain** using FFT
3. **Multiply** the frequency representations
4. **Transform back** using inverse FFT
5. **Extract the valid portion** (removing padding artifacts)

This approach works beautifully for offline processing but has a critical limitation for real-time applications: you
need the entire signal before you can start processing. For a 3-minute song, that means 3 minutes of latency.

## Block Processing and the Circular Convolution Problem

To achieve real-time processing, we need to work with small blocks of incoming audio. But naive block processing creates
a problem: FFT assumes the input is periodic (repeating), giving us circular convolution instead of the linear
convolution we want.

Here's what goes wrong:

```
Signal block: [1, 2, 3, 0, 0, 0, 0, 0]  (zero-padded)
Kernel:       [0.5, 0.25, 0, 0, 0, 0, 0, 0]  (zero-padded)

FFT treats this as if the signal repeats:
...1, 2, 3, 1, 2, 3, 1, 2, 3...
```

The wraparound effect corrupts the first `kernelLength - 1` samples of each block result. The solution? Overlap methods
that account for this corruption.

![circular-vs-linear-convolution.svg](https://livenathan.github.io/blog/assets/images/circular-vs-linear-convolution.svg)

## Overlap Save

The overlap save method works by:

1. **Processing overlapping input blocks** (not overlapping outputs like overlap-add)
2. **Discarding the corrupted samples** from each result
3. **Keeping only the valid portion** from each block

Here are the key concepts from the implementation:

```java
public double[] with(double[] signal, double[] kernel) {
    // Calculate block processing parameters
    int fftSize = calculateOptimalFftSize(signal.length, kernel.length);
    int blockSize = fftSize - kernel.length + 1;  // Valid samples per block
    int blockStartIndex = kernel.length - 1;      // Where valid data starts

    // Pre-compute kernel FFT (done once, reused for all blocks)
    Complex[] kernelTransform = SignalTransformer.fft(SignalTransformer.pad(kernel, fftSize));

    // Process each overlapping block
    int totalBlocks = (signal.length + blockSize - 1) / blockSize;
    for (int blockIndex = 0; blockIndex < totalBlocks; blockIndex++) {
        // Extract overlapping block, transform, multiply, inverse transform
        double[] block = extractSignalBlock(paddedSignal, blockIndex * blockSize, fftSize);
        Complex[] blockTransform = SignalTransformer.fft(block);
        Complex[] convolutionTransform = SignalTransformer.multiply(blockTransform, kernelTransform);
        double[] blockResult = SignalTransformer.ifft(convolutionTransform);

        // Save only the valid portion (discard aliased samples)
        int validLength = Math.min(blockSize, resultLength - blockIndex * blockSize);
        System.arraycopy(blockResult, blockStartIndex, result, blockIndex * blockSize, validLength);
    }

    return result;
}
```

![overlap-save-block-processing.svg](https://livenathan.github.io/blog/assets/images/overlap-save-block-processing.svg)

See the complete
implementation: [OverlapSaveAdapter.java](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/main/java/dev/nathanlively/overlap_save_demo/OverlapSaveAdapter.java)

### The Key Insight: Block Sizing

The magic numbers in overlap save:

- **FFT Size**: Must be power of two, determines computational cost per block
- **Block Size**: `fftSize - kernelLength + 1` valid samples per block
- **Overlap**: Each block overlaps by `kernelLength - 1` samples with the previous

Larger FFT sizes mean fewer blocks (less overhead) but higher latency. Smaller FFT sizes mean more blocks (more
overhead) but lower latency.

### FFT Size Optimization

My implementation includes adaptive FFT sizing based on signal and kernel characteristics:

```java
int calculateOptimalFftSize(int signalLength, int kernelLength) {
    int minSize = Math.max(2 * kernelLength - 1, 64);
    int optimalSize = CommonUtil.nextPowerOfTwo(minSize);

    // For large signals, try larger FFT sizes and pick the most efficient
    if (signalLength > 10 * kernelLength) {
        // Evaluate efficiency trade-offs for different sizes...
    }

    return optimalSize;
}
```

See the complete optimization
logic: [OverlapSaveAdapter.java#calculateOptimalFftSize](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/main/java/dev/nathanlively/overlap_save_demo/OverlapSaveAdapter.java)

## Performance Comparison

Here's what I measured across different signal and kernel combinations:

### Large Signal, Small Kernel (1024-sample signal, 3-sample kernel)

| Method           | Time (ms) | Memory Usage | Relative Performance |
|------------------|-----------|--------------|----------------------|
| Apache Commons   | 39.52     | Low          | 26.5x slower         |
| Time Domain      | 6.75      | Low          | 4.5x slower          |
| Frequency Domain | 11.98     | Medium       | 8.0x slower          |
| Overlap Save     | 1.49      | Medium       | **Baseline**         |

### Medium Signal, Medium Kernel (performance comparison test)

| Method           | Time (ms) | Memory Usage | Relative Performance |
|------------------|-----------|--------------|----------------------|
| Frequency Domain | 24.39     | Medium       | 6.2x slower          |
| Overlap Save     | 3.95      | Medium       | **Baseline**         |

### Key Observations

The overlap save advantage becomes more pronounced with different kernel/signal ratios:

- For small kernels (3 samples): Overlap save is 4.5x faster than time domain
- For medium kernels: Overlap save is 6.2x faster than frequency domain

#### Performance trends by use case:**

**Time Domain Convolution:**

- Kernels < 64 samples
- Offline processing where simplicity matters or fine-grained control on a sample-by-sample basis
- Educational purposes (easiest to understand)
- Memory-constrained environments

**Basic Frequency Domain:**

- Medium kernels (64-1024 samples)
- Offline processing with known signal length
- One-shot convolutions
- When overlap save overhead isn't justified

**Overlap Save:**

- Real-time processing (any kernel size)
- Long kernels (> 64 samples based on these results)
- Streaming applications
- When you need consistent low-latency performance
- Best overall performance across different signal/kernel combinations

## Practical Implementation Tips

### Testing Strategy

I parameterize all tests to run against every implementation:

```java
static Stream<Convolution> allImplementations() {
    return Stream.of(
            new ApacheAdapter(),
            new TimeDomainAdapter(),
            new FrequencyDomainAdapter(),
            new OverlapSaveAdapter()
    );
}
```

This ensures behavioral consistency.

### Common Pitfalls

**Incorrect Padding:** Both overlap-add and overlap-save require careful padding. Get the math wrong and you'll have
subtle artifacts.

**FFT Size Selection:** Too small and you waste cycles on overhead. Too large and you increase latency unnecessarily.

**Kernel Normalization:** Audio applications often need normalized kernels to prevent amplitude changes.

See the complete test suite with performance
benchmarks: [ConvolutionTest.java](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/test/java/dev/nathanlively/overlap_save_demo/ConvolutionTest.java)

### Signal Processing Infrastructure

I factored common operations into a utility class:

```java
public class SignalTransformer {
    public static Complex[] fft(double[] signal) { /* ... */ }

    public static double[] ifft(Complex[] transform) { /* ... */ }

    public static Complex[] multiply(Complex[] a, Complex[] b) { /* ... */ }

    public static double[] pad(double[] array, int startPad, int endPad) { /* ... */ }

    public static void validate(double[] signal, double[] kernel) { /* ... */ }
}
```

See the complete utility
implementation: [SignalTransformer.java](https://github.com/LiveNathan/overlap-save-demo/blob/main/src/main/java/dev/nathanlively/overlap_save_demo/SignalTransformer.java)

## Next Steps: Advanced Topics

This foundation enables more sophisticated techniques:

- Frequency Domain Crossfading: Save yourself an extra domain transformation.
- Partitioned Convolution: Split very long kernels into multiple blocks for even better efficiency.
- Non-Uniform Partitioning: Use different block sizes for different frequency ranges to optimize CPU vs. latency
trade-offs.
- SIMD processing: Use the Java Vector API to leverage native vector instructions.

## Conclusion

The overlap save method transforms convolution from a time consuming academic curiosity into a practical real-time
processing
technique. By understanding the progression from time domain through frequency domain to block processing, we can make
informed decisions about which approach fits our performance requirements.

For my audio processing project, overlap save delivered the real-time performance I needed while maintaining the
flexibility to change impulse responses dynamically. The key was building understanding through working code rather than
getting lost in mathematical abstractions.