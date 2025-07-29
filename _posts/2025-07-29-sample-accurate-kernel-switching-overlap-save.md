---
layout: post
title: "Sample-Accurate Kernel Switching with Overlap-Save Convolution"
date: 2025-07-29 08:00:00 -0000
categories: [ audio, signal-processing, convolution, kernel-switching, overlap-save, tdd, dsp ]
---

# Sample-Accurate Kernel Switching with Overlap-Save Convolution

Digital audio processing often requires changing filter characteristics in real-time - think of a synthesizer's filter
envelope sweeping from bright to dark, or a DJ transitioning between effects. But naive kernel switching can introduce
audible clicks and pops that destroy the listening experience. This post explores implementing sample-accurate kernel
switching using the overlap-save method.

## The Problem

When processing audio with convolution-based filters, we sometimes need to change the filter characteristics while the
audio is playing. Simply swapping out kernels at arbitrary sample boundaries doesn't work - convolution inherently
creates dependencies between input and output samples that span the kernel length. Ignore these dependencies, and you'll
hear unwanted artifacts.

## Why Kernel Switching Matters

Imagine you're building a synthesizer where the filter cutoff follows an envelope. If you simply swap kernels at
arbitrary points, you'll hear clicks every time the kernel changes. Sample-accurate switching ensures smooth transitions
while maintaining the precise timing that audio applications demand.

Real-world examples include:

- Envelope-controlled filters in synthesizers
- Dynamic EQ that responds to input characteristics
- Crossfading between different impulse responses
- Time-varying reverb effects

## Extending the Interface

Picking up from my previous blog post on overlap-save convolution, I created a new project and copied in the
`OverlapSaveAdapter` and `Convolution` interface. Then I needed to extend the interface to handle multiple kernels.

We started with:

```java
double[] with(double[] signal, double[] kernel);
```

And added:

```java
double[] with(double[] signal, List<double[]> kernels, int periodSamples);
```

The `periodSamples` parameter controls how long each kernel stays active before switching to the next one in the list.

## Following the ZOMBIES Path

Since I often get nervous about what to do next (AM I DOING IT RIGHT???), I like to follow prescriptions like ZOMBIES.
ZOMBIES (Zero, One, Many, Boundary, Interface, Exception, Simple) gives us a systematic way to think about test cases.
For kernel switching, the "boundary" case is particularly crucial - that's where the magic (or disasters) happen.

Let's use ZOMBIES to TDD ourselves to glory.

## Starting Simple: The Zero and One Cases

We'll start with the zero case that should simply throw an exception:

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

Then we'll do the "one" case, which should behave exactly like our previous single-kernel tests:

```java
@Test
void givenSingleImpulseKernel_whenConvolvingWithCollection_thenReturnsIdentity() {
    double[] signal = {1};
    double[] kernel = {1};

    double[] actual = convolution.with(signal, List.of(kernel), 1);

    assertThat(actual).isEqualTo(kernel);
}
```

## The Many Case: Where It Gets Interesting

Now we get to the meat - the many case:

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

## The Naive Solution (And Why It's Wrong)

This test will be tricky to get to pass. My first idea is to simply segment the signal based on kernel switch points and
convolve each segment separately with the appropriate kernel, then combine the results in the end. Let's call this the
first naive solution:

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

## Houston, We Have a Problem

The tests pass! 🎉 But wait... that was suspiciously easy.

In audio processing, "easy" solutions often hide nasty surprises. The issue is that we're ignoring the effects of
convolution around the kernel transition region. Think of it like a sliding window - as the kernel changes, we need to
ensure the window's contents are processed with the correct filter, not chopped up mid-calculation.

Let's write a failing test to prove this problem exists.

## Proving the Problem with a Failing Test

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

Let's work through what should happen at the boundary. For discrete convolution, each output sample depends on multiple
input samples according to the kernel length. The comments above show the mathematical expectation - notice how
`output[2]` depends on both `signal[2]` and `signal[1]`, but uses `kernel2` for both coefficients.

The test fails as expected, proving our naive approach completely ignores the overlap inherent in convolution.

## The Real Solution: Block-Based Processing

So how do we make it pass? The key insight is to divide the signal into blocks that match the switching periods. This
way, kernel transitions happen at block boundaries and not within blocks, preserving the mathematical correctness of
convolution.

Here's the corrected implementation:

```java
private double[] convolveWithKernelSwitching(double[] signal, List<double[]> kernels, int periodSamples) {
    int kernelLength = kernels.getFirst().length;
    int fftSize = CommonUtil.nextPowerOfTwo(periodSamples + kernelLength - 1);
    int resultLength = signal.length + kernelLength - 1;
    double[] result = new double[Math.max(resultLength, signal.length)];

    List<Complex[]> kernelTransforms = SignalTransformer.precomputeKernelTransforms(kernels, fftSize);
    double[] paddedSignal = SignalTransformer.pad(signal, kernelLength - 1, fftSize);
    int totalBlocks = (resultLength + periodSamples - 1) / periodSamples;

    for (int blockIndex = 0; blockIndex < totalBlocks; blockIndex++) {
        int outputStartIndex = blockIndex * periodSamples;
        int kernelIndex = (outputStartIndex / periodSamples) % kernels.size();
        Complex[] kernelTransform = kernelTransforms.get(kernelIndex);

        int inputStartIndex = blockIndex * periodSamples;
        double[] blockResult = SignalTransformer.processConvolutionBlock(
                paddedSignal, inputStartIndex, fftSize, kernelTransform);

        int validLength = Math.min(periodSamples, result.length - outputStartIndex);
        if (validLength > 0) {
            System.arraycopy(blockResult, kernelLength - 1, result, outputStartIndex, validLength);
        }
    }

    return result.length == resultLength ? result : Arrays.copyOf(result, resultLength);
}
```

You can see that I've refactored the convolution math into the `SignalTransformer` class, so the `OverlapSaveAdapter`
focuses on orchestrating the signal transformations and block indexing. This separation of concerns makes the code more
maintainable and testable.

## Additional Test Cases

With the core logic working, I added several more test cases to ensure robustness:

**Cycling through multiple kernels:**

```java

@Test
void givenLongerSignal_whenConvolving_thenCyclesThroughKernelsCorrectly() {
    double[] signal = new double[10];
    Arrays.fill(signal, 1.0);
    double[] kernel1 = {1.0}; // Samples 0-1
    double[] kernel2 = {2.0}; // Samples 2-3
    double[] kernel3 = {3.0}; // Samples 4-5

    List<double[]> kernels = List.of(kernel1, kernel2, kernel3);
    double[] actual = convolution.with(signal, kernels, 2);

    // Verify the pattern: 1,1,2,2,3,3,1,1,2,2
    double[] expected = {1, 1, 2, 2, 3, 3, 1, 1, 2, 2};
    assertThat(actual).usingElementComparator(doubleComparator())
            .containsExactly(expected);
}
```

**Testing with realistic audio filters:**
```java

@Test
void givenRealisticFilters_whenConvolving_thenProducesExpectedOutput() {
    double[] signal = {1, 0, 0, 0, 0, 0}; // Impulse
    double[] lowpass = {0.25, 0.5, 0.25};  // Simple lowpass
    double[] highpass = {-0.25, 0.5, -0.25}; // Simple highpass

    List<double[]> kernels = List.of(lowpass, highpass);
    double[] actual = convolution.with(signal, kernels, 3);

    // The first 3 samples get lowpass, the next 3 get highpass
    double[] expected = {0.25, 0.5, 0.25, 0, 0, 0, 0, 0};
    assertThat(actual).usingElementComparator(doubleComparator())
            .containsExactly(expected);
}
```

## Lessons Learned

This exercise reinforced a key principle in audio DSP: **mathematical correctness comes first, optimization second**.
The naive segmentation approach seemed simpler but violated the fundamental mathematics of convolution. The block-based
approach respects the mathematical constraints while still achieving our goal of sample-accurate kernel switching.

Another insight: **test-driven development shines brightest at the boundaries**. The failing boundary test immediately
exposed the flaw in our reasoning and guided us toward the correct solution.

## The Plot Thickens

We've solved the mathematical correctness problem, but introduced a new one: abrupt kernel switches will create audible
artifacts in real audio signals. The human ear is remarkably sensitive to discontinuities, and switching from a lowpass
to a highpass filter instantaneously will produce audible clicks.

Next time, we'll explore crossfading and windowing techniques to make kernel transitions smooth enough for professional
audio applications. We'll also discuss the trade-offs between mathematical precision and perceptual quality - sometimes
the "mathematically correct" solution isn't the best one for human listeners.