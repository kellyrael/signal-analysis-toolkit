# Signal Analysis Toolkit

A small Python toolkit for acquiring, analyzing, and characterizing periodic signals. It provides utilities to simulate/acquire a signal on a given pin, compute its frequency spectrum via FFT, and measure its average frequency using rising-edge detection.

## Features

- **Signal acquisition** (`acquire_pin.py`) — Generates/plots a time-domain signal for a given pin number and sampling period.
- **FFT computation** (`compute_fft.py`) — Computes the single-sided amplitude spectrum of a real-valued signal.
- **Average frequency detection** (`find_average_frequency.py`) — Detects rising-edge crossings of a threshold (with optional hysteresis and sub-sample interpolation) and computes the average frequency, period, jitter, and cycle count.

## Requirements

- Python 3.8+
- [NumPy](https://numpy.org/)
- [Matplotlib](https://matplotlib.org/)

Install dependencies with:

```bash
pip install numpy matplotlib
```

## Usage

```python
from acquire_pin import acquire_pin
from compute_fft import compute_fft
from find_average_frequency import average_frequency

sampling_period = 1 / 1000  # seconds
sig = acquire_pin(pin_number=1, sampling_period=sampling_period)

freqs, spectrum = compute_fft(sig, sampling_period)

result = average_frequency(sig, sampling_period, threshold=0.0)
print(result["frequency"])
```

## API Overview

### `acquire_pin(pin_number, sampling_period)`
Returns a 1-D `np.ndarray` signal sampled over a 1-second window for the given pin number.

### `compute_fft(samples, sampling_period)`
Returns `(freqs, spectrum)` — the frequency bins (Hz, 0..Nyquist) and the scaled complex FFT coefficients.

### `average_frequency(samples, sampling_period, threshold, hysteresis=0.0, interpolate=True)`
Returns a `dict` containing `frequency`, `period`, `edge_times`, `edge_indices`, `cycles`, `periods`, `jitter`, and `span`.

## Project Structure

```
.
├── acquire_pin.py            # Signal acquisition / generation
├── compute_fft.py            # FFT computation utilities
├── find_average_frequency.py # Rising-edge based frequency measurement
└── test_plan.xlsx            # Test plan documentation
```

## License

This project currently has no explicit license. Contact the repository owner for usage terms.
