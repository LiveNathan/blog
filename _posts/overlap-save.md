# Overlap Save Method for Frequency Domain Convolution: A Practical Approach

This being a practical approach, I'm going to dive straight into the code. Skip to the second half for more context and
theory.

## Step by step convolution

Whenever I'm trying to learn something new or understand something hard I usually start by procrastanating. Maybe there
are some YT videos I can watch for a while instead of getting started. Then, a few hours later, I fianlly convince
myself to get started by taking the smallest possible step. What's the least I can do?

### Known values

I might not know much about convolution, but I think I remember that if you convolve any signal with an impulse then you
just get the signal back. I can make it even easier by just convolving two impulses together.

Let's start with the Apache Commons implementation of time domain convolution.

```java
public class ApacheAdapter implements Convolution {
   @Override
   public double[] with(double[] signal, double[] kernel) {
      return MathArrays.convolve(signal, kernel);
   }
}
```

Here are 3 characterization tests. I hope these demonstrate that I like to take very small steps.

```java

@Test
void impulseConvolution_returnsIdentity() {
   Convolution convolution = new ApacheAdapter();
   double[] signal = {1};
   double[] kernel = {1};

   double[] actual = convolution.with(signal, kernel);

   assertThat(actual).isEqualTo(kernel);
}

@Test
void twoElementConvolution_computesExpectedValues() {
   Convolution convolution = new ApacheAdapter();
   double[] signal = {1, 0.5};
   double[] kernel = {0.2, 0.1};

   double[] result = convolution.with(signal, kernel);

   assertThat(result.length).isEqualTo(signal.length + kernel.length - 1); // 2 + 2 - 1 = 3
   // result[0] = signal[0] * kernel[0] = 1 * 0.2 = 0.2
   assertThat(result[0]).isEqualTo(0.2);  // 1 * 0.2
   // result[1] = signal[0] * kernel[1] + signal[1] * kernel[0]
   // result[1] = (1 * 0.1) + (0.5 * 0.2) = 0.2
   assertThat(result[1]).isEqualTo(0.2);  // 1 * 0.1 + 0.5 * 0.2
   // result[2] = signal[1] * kernel[1]
   // result[2] = 0.5 * 0.1 = 0.05
   assertThat(result[2]).isEqualTo(0.05); // 0.5 * 0.1
}

@Test
void convolutionIsCommutative() {
   Convolution convolution = new ApacheAdapter();
   double[] signal = {1, 2, 3};
   double[] kernel = {0.5, 0.25};

   double[] result1 = convolution.with(signal, kernel);
   double[] result2 = convolution.with(kernel, signal);

   assertThat(result1).isEqualTo(result2);
}
```

## Copy and refactor

Now that we have characterized a known working implementation of time domain convolution, let's write our own custom
implementation to improve our understanding. But, write it from scratch? No way! That's way too hard. Instead let's copy
the Apache method and rafactor it.

Don't try to understand this, yet. Just appreciate how concise it is before we wreck it with our refactoring.

```java
public class CustomAdapter implements Convolution {
   @Override
   public double[] with(double[] x, double[] h) {
      MathUtils.checkNotNull(x);
      MathUtils.checkNotNull(h);

      final int xLen = x.length;
      final int hLen = h.length;

      if (xLen == 0 || hLen == 0) {
         throw new NoDataException();
      }

      // initialize the output array
      final int totalLength = xLen + hLen - 1;
      final double[] y = new double[totalLength];

      // straightforward implementation of the convolution sum
      for (int n = 0; n < totalLength; n++) {
         double yn = 0;
         int k = FastMath.max(0, n + 1 - xLen);
         int j = n - k;
         while (k < hLen && j >= 0) {
            yn += x[j--] * h[k++];
         }
         y[n] = yn;
      }

      return y;
   }
}
```

Let's parametrize our tests so that they will also run against our new custom adapter.

```java
static Stream<Convolution> convolutionImplementations() {
   return Stream.of(new ApacheAdapter(), new CustomAdapter());
}

@ParameterizedTest
@MethodSource("convolutionImplementations")
void impulseConvolution_returnsIdentity(Convolution convolution) {
   double[] signal = {1};
   double[] kernel = {1};

   double[] actual = convolution.with(signal, kernel);

   assertThat(actual).isEqualTo(kernel);
}

@ParameterizedTest
@MethodSource("convolutionImplementations")
void twoElementConvolution_computesExpectedValues(Convolution convolution) {
   double[] signal = {1, 0.5};
   double[] kernel = {0.2, 0.1};

   double[] result = convolution.with(signal, kernel);

   assertThat(result.length).isEqualTo(signal.length + kernel.length - 1);
   assertThat(result[0]).isEqualTo(0.2);
   assertThat(result[1]).isEqualTo(0.2);
   assertThat(result[2]).isEqualTo(0.05);
}

@ParameterizedTest
@MethodSource("convolutionImplementations")
void convolutionIsCommutative(Convolution convolution) {
   double[] signal = {1, 2, 3};
   double[] kernel = {0.5, 0.25};

   double[] result1 = convolution.with(signal, kernel);
   double[] result2 = convolution.with(kernel, signal);

   assertThat(result1).isEqualTo(result2);
}
```

### Refactor 1 - Rename vars

The first easiest thing to do for better code understanding is to rename the variables using expressive variable names.
The first time I did this I had an LLM do it for me.

```java
public double[] with(double[] signal, double[] kernel) {
   MathUtils.checkNotNull(signal);
   MathUtils.checkNotNull(kernel);

   final int signalLength = signal.length;
   final int kernelLength = kernel.length;

   if (signalLength == 0 || kernelLength == 0) {
      throw new NoDataException();
   }
   final int resultLength = signalLength + kernelLength - 1;
   final double[] result = new double[resultLength];

   for (int resultIndex = 0; resultIndex < resultLength; resultIndex++) {
      double sum = 0;
      int kernelIndex = FastMath.max(0, resultIndex + 1 - signalLength);
      int signalIndex = resultIndex - kernelIndex;
      while (kernelIndex < kernelLength && signalIndex >= 0) {
         sum += signal[signalIndex--] * kernel[kernelIndex++];
      }
      result[resultIndex] = sum;
   }

   return result;
}
```

### Refactor 2 - Remove defense

This implementation achieves conciseness and elegance through two key design choices:

1. **Implicit zero padding**: The `result` array is initialized with zeros by default. When the loop conditions (
   `kernelIndex < kernelLength && signalIndex >= 0`) prevent execution at the boundaries, the sum remains zero,
   effectively providing the necessary padding without explicit boundary handling.

2. **Implicit kernel flipping**: The combination of `signalIndex--` and `kernelIndex++` reads the signal backwards while
   traversing the kernel forwards. This achieves the mathematical equivalent of kernel reversal required by convolution,
   without explicitly flipping the kernel array.

Unfortunately, what makes this code elegant and concise also make it difficult to read. When I try to read through the
loop in my mind, I give up almost immediately. I hate defensive code. It makes everything harder to read. Let's see if
we can remove all of the defensive code and make the explicit zero padding and kernel flipping excplicit.

```java
public double[] with(double[] signal, double[] kernel) {
   MathUtils.checkNotNull(signal);
   MathUtils.checkNotNull(kernel);

   final int signalLength = signal.length;
   final int kernelLength = kernel.length;

   if (signalLength == 0 || kernelLength == 0) {
      throw new NoDataException();
   }

   final int resultLength = signalLength + kernelLength - 1;
   final double[] result = new double[resultLength];

   // Step 1: Pad the signal with zeros on both sides
   final int padding = kernelLength - 1;
   final int paddedLength = signalLength + 2 * padding;
   final double[] paddedSignal = new double[paddedLength];
   System.arraycopy(signal, 0, paddedSignal, padding, signalLength);

   // Step 2: Flip the kernel for convolution (vs. correlation)
   final double[] flippedKernel = ArrayUtils.clone(kernel);
   ArrayUtils.reverse(flippedKernel);

   // Step 3: Slide the flipped kernel over the padded signal
   for (int outputPos = 0; outputPos < resultLength; outputPos++) {
      double sum = 0;
      int paddedSignalStartPos = outputPos + padding - kernelLength + 1;

      for (int kernelPos = 0; kernelPos < kernelLength; kernelPos++) {
         sum += paddedSignal[paddedSignalStartPos + kernelPos] * flippedKernel[kernelPos];
      }
      result[outputPos] = sum;
   }

   return result;
}
```

### Refactor 3 - Make the sliding window visible

It would be nice to have the sliding window concept be more concrete and visible.

```java
public double[] with(double[] signal, double[] kernel) {
   // setup removed for brevity
   // Step 3: Slide the flipped kernel over the padded signal
   for (int outputPos = 0; outputPos < resultLength; outputPos++) {
      int windowStartPos = outputPos + padding - kernelLength + 1;

      // Extract the current window from the padded signal
      double[] signalWindow = Arrays.copyOfRange(paddedSignal, windowStartPos, windowStartPos + kernelLength);

      // Compute dot product of window and flipped kernel
      double sum = 0;
      for (int i = 0; i < kernelLength; i++) {
         sum += signalWindow[i] * flippedKernel[i];
      }
      result[outputPos] = sum;
   }

   return result;
}
```

### Refactor 4 - Smaller methods

Our method is only about 40 lines long, but splitting it into smaller methods will make it even easier to understand and
test.

```java
 public double[] with(double[] signal, double[] kernel) {
   validateInputs(signal, kernel);

   final double[] paddedSignal = padSignal(signal, kernel.length);
   final double[] reversedKernel = reverseKernel(kernel);

   return computeConvolution(paddedSignal, reversedKernel, signal.length);
}

private void validateInputs(double[] signal, double[] kernel) {
   MathUtils.checkNotNull(signal);
   MathUtils.checkNotNull(kernel);

   if (signal.length == 0 || kernel.length == 0) {
      throw new NoDataException();
   }
}

double[] padSignal(double[] signal, int kernelLength) {
   final int padding = kernelLength - 1;
   final int paddedLength = signal.length + 2 * padding;
   final double[] paddedSignal = new double[paddedLength];
   System.arraycopy(signal, 0, paddedSignal, padding, signal.length);
   return paddedSignal;
}

double[] reverseKernel(double[] kernel) {
   final double[] flippedKernel = ArrayUtils.clone(kernel);
   ArrayUtils.reverse(flippedKernel);
   return flippedKernel;
}

private double[] computeConvolution(double[] paddedSignal, double[] reversedKernel, int signalLength) {
   int kernelLength = reversedKernel.length;
   final int resultLength = signalLength + kernelLength - 1;
   final double[] result = new double[resultLength];
   final int padding = kernelLength - 1;

   for (int outputPos = 0; outputPos < resultLength; outputPos++) {
      result[outputPos] = computeWindowConvolution(paddedSignal, reversedKernel,
              outputPos, padding, kernelLength);
   }

   return result;
}

private double computeWindowConvolution(double[] paddedSignal, double[] preparedKernel,
                                        int outputPos, int padding, int kernelLength) {
   int windowStartPos = outputPos + padding - kernelLength + 1;
   double sum = 0;

   for (int i = 0; i < kernelLength; i++) {
      sum += paddedSignal[windowStartPos + i] * preparedKernel[i];
   }

   return sum;
}
```

Let's add two new tests tht will help us nail down the behavior of our new methods and start setting ourselves up well
to drive new behavior change later.

```java

@Test
void preparePaddedSignal_addsCorrectPadding() {
   TimeDomainAdapter adapter = new TimeDomainAdapter();
   double[] signal = {1, 2};
   int kernelLength = 3;

   double[] paddedSignal = adapter.padSignal(signal, kernelLength);

   assertThat(paddedSignal).containsExactly(0, 0, 1, 2, 0, 0);
}

@Test
void prepareKernel_flipsArray() {
   TimeDomainAdapter adapter = new TimeDomainAdapter();
   double[] kernel = {1, 2, 3};

   double[] reversedKernel = adapter.reverseKernel(kernel);

   assertThat(reversedKernel).containsExactly(3, 2, 1);
}
```

### Into the frequency domain

#### Refactor 1 - Copy

I created FrequencyDomainAdapter by copying TimeDomainAdapter. Even though much of it will change, it's so much easier
to edit existing code than to start from scratch.

#### Refactor 2 - Padding

We are still going to perform the same input validation so that method can stay. We are also still going to perform
padding, but this time instead of padding the beginning and end of the signal to facilitate the sliding window, we zero
pad the end of both signal and kernel until they are both the same length and a power of two. Making them the same
length makes the multiplication step easy and making their length a power of two satisfies the FFT transform
requirement.

```java
public class FrequencyDomainAdapter implements Convolution {
   @Override
   public double[] with(double[] signal, double[] kernel) {
      validateInputs(signal, kernel);

      int convolutionLength = signal.length + kernel.length - 1;
      int paddedLength = CommonUtil.nextPowerOfTwo(convolutionLength);

      final double[] paddedSignal = padArray(signal, paddedLength);
      final double[] paddedKernel = padArray(kernel, paddedLength);

      // fft
      // multiply
      // ifft
   }

   double[] padArray(double[] array, int targetLength) {
      double[] padded = new double[targetLength];
      System.arraycopy(array, 0, padded, 0, array.length);
      return padded;
   }
}
```

#### Refactor 3 - FFT

Performing the FFT transform is just a call to the Apache Commons method.

```java
Complex[] transform(double[] signal) {
   FastFourierTransformer fft = new FastFourierTransformer(DftNormalization.STANDARD);
   return fft.transform(signal, TransformType.FORWARD);
}
```

Let's add a test for it.

```java

@Test
void transform_computesFFTForPowerOfTwoSignal() {
   FrequencyDomainAdapter adapter = new FrequencyDomainAdapter();
   double[] signal = {1, 2};

   Complex[] transform = adapter.transform(signal);

   assertThat(transform).hasSize(2);
   // FFT of [1, 2] should be [3+0i, -1+0i]
   assertThat(transform[0].getReal()).isEqualTo(3.0);
   assertThat(transform[0].getImaginary()).isEqualTo(0.0);
   assertThat(transform[1].getReal()).isEqualTo(-1.0);
   assertThat(transform[1].getImaginary()).isEqualTo(0.0);
}
```

#### Refactor 4 - IFFT

The inverse transform is very similar, but we only need the real values.

```java
double[] inverseTransformRealOnly(Complex[] transform) {
   FastFourierTransformer fft = new FastFourierTransformer(DftNormalization.STANDARD);
   Complex[] result = fft.transform(transform, TransformType.INVERSE);

   double[] realResult = new double[result.length];
   for (int i = 0; i < result.length; i++) {
      realResult[i] = result[i].getReal();
   }
   return realResult;
}
```

```java

@Test
void transformRoundTrip_preservesOriginalSignal() {
   FrequencyDomainAdapter adapter = new FrequencyDomainAdapter();
   double[] original = {1, 2, 3, 4};

   Complex[] transformed = adapter.transform(adapter.padArray(original, 8));
   double[] roundTrip = adapter.inverseTransformRealOnly(transformed);

   assertThat(roundTrip).usingElementComparator(doubleComparator())
           .containsExactly(1, 2, 3, 4, 0, 0, 0, 0);
}
```

#### Refactor 5 - Multiply

Convolution in the frequency domain is simply multiplication. Yay!

```java
private Complex[] multiplyTransforms(Complex[] transform1, Complex[] transform2) {
   Complex[] result = new Complex[transform1.length];
   for (int i = 0; i < transform1.length; i++) {
      result[i] = transform1[i].multiply(transform2[i]);
   }
   return result;
}
```

### Refactor 6 - Tie it all together

Let's tie it all together and trim any extra zeros.

```java
public double[] with(double[] signal, double[] kernel) {
   validateInputs(signal, kernel);

   int convolutionLength = signal.length + kernel.length - 1;
   int paddedLength = CommonUtil.nextPowerOfTwo(convolutionLength);

   final double[] paddedSignal = padArray(signal, paddedLength);
   final double[] paddedKernel = padArray(kernel, paddedLength);
   final Complex[] signalTransform = transform(paddedSignal);
   final Complex[] kernelTransform = transform(paddedKernel);

   final Complex[] productTransform = multiplyTransforms(signalTransform, kernelTransform);
   final double[] convolutionResult = inverseTransformRealOnly(productTransform);

   return extractValidPortion(convolutionResult, convolutionLength);
}

private double[] extractValidPortion(double[] paddedResult, int validLength) {
   double[] result = new double[validLength];
   System.arraycopy(paddedResult, 0, result, 0, validLength);
   return result;
}
```

### Refactor 7 - Prepare for OLS

To prepare for the OverlapSaveAdapter, let's move those signal transform method into a common class so we don't have to
write them again (or worry about them again!) and simplify the method names.

Afterwards the FrequencyDomainAdapter will look like this:

```java
public double[] with(double[] signal, double[] kernel) {
   SignalTransformer.validate(signal, kernel);

   int convolutionLength = signal.length + kernel.length - 1;
   int paddedLength = CommonUtil.nextPowerOfTwo(convolutionLength);

   final double[] paddedSignal = SignalTransformer.pad(signal, paddedLength);
   final double[] paddedKernel = SignalTransformer.pad(kernel, paddedLength);
   final Complex[] signalTransform = SignalTransformer.fft(paddedSignal);
   final Complex[] kernelTransform = SignalTransformer.fft(paddedKernel);

   final Complex[] productTransform = SignalTransformer.multiply(signalTransform, kernelTransform);
   final double[] convolutionResult = SignalTransformer.ifft(productTransform);

   return extractValidPortion(convolutionResult, convolutionLength);
}
```

## Overlap Save

### Refactor 1 - Copy

Let's start by simply copying over the FrequencyDomainAdapter into a new OverlapSaveAdapter and updating our tests.

```java
static Stream<Convolution> convolutionImplementations() {
   return Stream.of(new ApacheAdapter(), new TimeDomainAdapter(),
           new FrequencyDomainAdapter(), new OverlapSaveAdapter());
}
```

### Refactor 2 - Define vars

#### FFT size

In FrequencyDomainAdapter we set the FFT size to the next best value higher than the final length of the result. In
OverlapSaveAdapter we are free to set the FFT size to whatever we want. There are some ways to optimize this, but I'm
going to skip thta explanation to stay focused on the mechanics of the OLS method itself.

```java
int fftSize = calculateOptimalFftSize(signal.length, kernelLength);
```

#### Block Size

FFT treats the input signal as periodic (repeating in a cycle), which produces circular convolution instead of the
linear convolution we want. This circular wraparound corrupts the first `kernelLength - 1` samples of each result. The
remaining `fftSize - kernelLength + 1` samples are valid - this is our `blockSize`.

```java
int blockSize = fftSize - kernelLength + 1;
```

We want to know the exact index where that block starts so we'll create `blockStartIndex`.

```java
int blockStartIndex = kernelLength - 1;
```

### Refactor 3 - Pad signal

We need to pad the signal with zeros just as we did in FrequencyDomainAdapter, but this time instead of padding the end
we need to pad the start.

```java
private double[] padSignalStart(double[] signal, int resultLength, int blockStartIndex) {
   double[] paddedSignal = new double[resultLength];
   System.arraycopy(signal, 0, paddedSignal, blockStartIndex, signal.length);
   return paddedSignal;
}
```

Later I'll refactor this into a padding method that we can use commonly across our implementations. Something like this:

```java
double[] paddedSignal = SignalTransformer.pad(
        signal,
        blockStartIndex, // startPaddingAmount
        resultLength - signal.length - blockStartIndex  // endPaddingAmount
);
```

### Refactor 4 - Process in blocks

Let's get started with the real meat of the OLS convolution. The overlap-save method works by overlapping input blocks
and saving only the valid portion of each convolution result. I considered doing with in a while loop, but in the end I
think a for loop is more conventional and testable.

First we'll calculate the total number of for loop iterations.

`int totalBlocks = (signal.length + blockSize - 1) / blockSize;`

This is equivalent to `Math.ceil(signal.length / blockSize)` but avoids floating-point arithmetic.

Now, inside of this for loop where we iterate over all of the blocks:

Each time through the loop we need to:

1. Get the next signal block.
2. FFT the signal
3. Multiply kernel and signal tranform
4. IFFT back to the time domain
5. Extract the valid result block and add it to the result.

The computational heavy lifting is done for us by Apache Commons Math4, but the part that we as programmers need to take
care of is the tricky indexing.

#### Process Blocks 1 - Get the next signal block

Each time through the loop we will extract the next block of input signal starting at `blockIndex * blockSize`. I kind
of hate using `System.arraycopy` because it's not very readable, but it get's used a lot in these operations so I'm
trying to just embrace it and get used to it.

`System.arraycopy(
     paddedSignal,  // Source object 
     nextBlockStartIndex,  // Source index 
     block,  // Destination object
     0,  // Destination index
     copyLength  // Source length
);`

Most of the time copyLength is just fftSize, but the final block might be smaller than fftSize.

`int copyLength = Math.min(fftSize, paddedSignal.length - nextBlockStartIndex);`

#### Process Block 2 - Valid portion

In most cases, the valid portion of the result of convolution will be equal to the block size, but as above, the final
block is a special case since it will likely be smaller than the block size.

`int validLength = Math.min(blockSize, resultLength - nextBlockStartIndex);`

Now that we have the length of the valid portion of the result of convolution that we want to keep we can simply copy it
over to the output array.

`System.arraycopy(
   blockResult,  // Source object
   blockStartIndex,  // Source index
   result,  // Destination object
   nextBlockStartIndex,  // Destination index
   validLength);  // Source length to copy`

All tests pass, but I did have to introduce a precision of 1e-15 into the equality assertions. This is common with
floating point arithimetic.

## Introduction

> While programming can help in understanding mathematical concepts, it's not the other way around. — Mike X. Cohen

Math is hard. And I think part of why it's so hard is the use of so many symbols. But I guess it's the same when
learning any language. At the beginning it all looks like jibberish. Eventually, with practice, you are no longer
sounding out each syllable, you just see patterns of works and sentences. I can do this with various amounts of ease
with English, Portuguese, Java, and MATLAB.

The mathematical definition of convolution looks intimidating:

$(x * h)[n] = \sum_{m=-\infty}^{\infty} x[m] \cdot h[n-m]$

Apache commons has some helpful signal processing functions built in that abstract away all of the complication,
allowing you to
simply write convolution like this: `MathArrays.convolve(signal, kernel);`

But we are going to write it out step by step so that we can refactor it into the OLS method. Then in part two we'll
look at switch switching kernels mid-signal.

Here's an example. No need to understand this, yet. Just and example to show how much easier it is to read in code than
the equation above. Of course, all of this is relative. If you're used to reading equations and not code, then maybe the
equation is easier to read, but I'm writing this for software developers. (spoiler alert: I intentially used academic
var names below to make it difficult to read.)

```java
public static double[] convolve(double[] x, double[] h) {

   final int xLen = x.length;
   final int hLen = h.length;

   final int totalLength = xLen + hLen - 1;
   final double[] y = new double[totalLength];

   for (int n = 0; n < totalLength; n++) {
      double yn = 0;
      int k = JdkMath.max(0, n + 1 - xLen);
      int j = n - k;
      while (k < hLen && j >= 0) {
         yn += x[j--] * h[k++];
      }
      y[n] = yn;
   }

   return y;
}
```

As a developer working on audio processing, I recently found myself struggling to implement the overlap save method for
frequency domain convolution. Despite searching through numerous resources, I couldn't find an explanation that clicked
with my brain. Most materials were either too abstract or too heavily focused on mathematical concepts. I did find some
code examples but they, but none of them made sense to me.

This blog post is my attempt to explain the overlap save method in a way that would have helped me understand it faster.
I'll focus on practical implementations in MATLAB and Java, showing code examples rather than complex equations whenever
possible. By writing this, I'm hoping to solidify my own understanding while providing a resource for other developers
facing similar challenges.

**Disclaimer:** I don't have a formal background in DSP. I'm a sound engineer turned software developer learning DSP
concepts as
I implement them in real projects. If you spot technical errors or have suggestions for improvement, please share them
in the comments or send me a DM!

## Background

When processing audio signals, convolution is a fundamental operation that allows us to combine two signals. This is
often how we get reverb or simulate acoustic spaces but can also be used to apply EQ filters. There are two main
approaches to convolution: time domain and frequency
domain.

signal + kernel = result

### Time Domain vs. Frequency Domain Convolution

Time domain convolution combines two time series. At each signal sample you calculate the dot product of the kernel and
the signal to get the result, which is the new sample at that position. Then you go to the next signal sample. It's just
addition and multiplication. It's straightforward to
understand and implement, produces high-quality results, and is perfectly suitable for offline processing. However, it
becomes computationally expensive for long signals or large kernels, making it impractical for real-time applications.
Not only do you have to visit every sample in the signal, but then for each signal sample, you have to visit every
sample in the kernel giving you a loop inside of a loop, which is a complexity of O(N²).

Looking back at the example above, the indexing is the most complicated part. Otherwise, you can still see that's only
addition and
multiplication.

For my project, GainGuardian, we initially implemented time domain convolution for offline processing. In my case my
kernels are usually 8192 samples long so it takes about 30 seconds to perform convolution on a normal music file. While
this approach works well and produces high-quality results, it is simply too slow for real-time processing.

### The Convolution Theorem

The convolution theorem states that convolution in the time domain equals multiplication in the frequency domain:

```java
public class FrequencyDomainAdapter implements Convolution {
   @Override
   public double[] with(double[] signal, double[] kernel) {
      SignalTransformer.validate(signal, kernel);

      int resultLength = signal.length + kernel.length - 1;
      int paddedLength = CommonUtil.nextPowerOfTwo(resultLength);

      final double[] paddedSignal = SignalTransformer.pad(signal, paddedLength);
      final double[] paddedKernel = SignalTransformer.pad(kernel, paddedLength);
      final Complex[] signalTransform = SignalTransformer.fft(paddedSignal);
      final Complex[] kernelTransform = SignalTransformer.fft(paddedKernel);

      final Complex[] productTransform = SignalTransformer.multiply(signalTransform, kernelTransform);
      final double[] convolutionResult = SignalTransformer.ifft(productTransform);

      return extractValidPortion(convolutionResult, resultLength);
   }

   private double[] extractValidPortion(double[] paddedResult, int validLength) {
      double[] result = new double[validLength];
      System.arraycopy(paddedResult, 0, result, 0, validLength);
      return result;
   }

}
```

In theory, time domain convolution and frequency domain convolution should produce identical results. However, in
practice, there are differences due to:

- Numerical precision issues
- Circular vs. linear convolution effects
- Implementation details

In my experience, the two samples above should produce matching results to a precision of 1e-15, which is high!

### Why Real-time Applications Need Frequency Domain Approaches

For real-time applications, frequency domain convolution offers significant performance advantages. By transforming the
signal and kernel to the frequency domain using Fast Fourier Transform (FFT), performing multiplication, and then
transforming back using Inverse FFT (IFFT), we can reduce the computational complexity from O(N²) to O(N log N).

The key to real-time processing is to work with blocks of the input signal rather than waiting for the entire signal.
The size of these blocks directly affects latency – smaller blocks reduce latency but increase computational overhead
due to more frequent FFT operations. Time domain convolution has the most computational overhead since it is essentailly
working in blocks of 1.

## Overlap Methods Overview

### Why We Need Overlap Methods

When processing signals in blocks using frequency domain convolution, we encounter an important issue: the FFT
inherently performs circular convolution, while we typically want linear convolution for audio processing. This
discrepancy causes artifacts at the block boundaries.

To address this problem, we use overlap methods, which ensure correct results at block boundaries. The two primary
approaches are:

1. **Overlap Add**: Process each block independently with zero-padding, then add the overlapping output portions
2. **Overlap Save**: Process overlapping input blocks and discard portions affected by circular convolution

The overlap save method attracted my attention for two key reasons:

1. It's generally more computationally efficient because it doesn't require additional storage for accumulating results
2. It allows for implementing frequency domain crossfades between kernels, which is crucial for my application where
   kernels need to change frequently

## Basic Overlap Save Implementation

### Algorithm Explanation

The overlap save method overview:

1. Divide the input signal into overlapping blocks
2. Apply FFT to each block
3. Multiply with the FFT of the zero-padded kernel
4. Apply IFFT to get the time domain result
5. Discard the first overlapping samples from each result block
6. Concatenate them

The key insight is that by processing overlapping segments and discarding the circular convolution artifacts, we can
achieve linear convolution results efficiently.