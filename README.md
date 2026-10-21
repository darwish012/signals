# Sound Generation, Noise Addition and Filtering (Python)

A Python script that builds a short melody from sine tones, adds two random-frequency tones as noise, locates the noise tones in the frequency spectrum, removes them, and plays the cleaned signal. The time-domain and frequency-domain signals are plotted at each stage.

## What is implemented

1. Signal generation: the function `sigma` sums, for each of 10 notes, two sine waves (a lower tone from the list `F1` and a higher tone from `f1`) multiplied by a rectangular gate of length `Ti1 = 0.2 s`. The note start times are spread evenly over 3 seconds. The time axis `t1` has `12*1024` points over 0 to 3 seconds.
2. Spectrum: an FFT of the signal, scaled as `2/N * abs(FFT)` with `N = 3*1024`, plotted against a 0 to 512 Hz axis.
3. Noise: two sine waves with random integer frequencies between 0 and 511 Hz (`np.random.randint`) are added to the signal.
4. Noise detection: the spectrum of the noisy signal is compared with the threshold `ceil(max of the clean spectrum)`; the first two bins above the threshold are taken as the noise frequencies.
5. Filtering: sine waves at the two detected frequencies are subtracted from the noisy signal in the time domain.
6. Output: a 6-panel figure (time domain on the left, frequency domain on the right, for the clean, noisy and filtered signals), then playback of the filtered signal with `sounddevice`.

## Files

| File | Description |
| --- | --- |
| `code` | The Python script (no file extension). |

## How to run

- Python 3 with `numpy`, `scipy`, `matplotlib` and `sounddevice`.
- The script uses `np.int`, which was removed in NumPy 1.24, so use NumPy older than 1.24 or replace `np.int` with `int`.
- Copy the contents of `code` into a file such as `signals.py` and run `python signals.py`. A figure window is shown and the filtered signal is played through the default audio device.
- The noise frequencies are random, so each run uses different noise tones.

## Author

Abdelrahman Darwish (GitHub: [@darwish012](https://github.com/darwish012))
