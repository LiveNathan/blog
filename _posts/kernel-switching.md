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