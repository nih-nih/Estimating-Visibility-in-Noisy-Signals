# Estimating Visibility in Noisy Signals

## Overview

This project investigates robust methods for estimating the **visibility** (contrast between maxima and minima) of **noisy periodic signals**, with applications in **optical experiments** and **interference-based measurements**. Accurate visibility estimation is critical for detecting phase shifts and assessing signal quality in practical experimental setups where noise is inevitable.

We compare two core techniques:
- **Fast Fourier Transform (FFT)-based reconstruction**
- **Nonlinear Least-Squares Curve Fitting**

Additionally, we apply **signal smoothing filters** to improve signal quality before visibility extraction:
- Low-pass filtering via FFT
- Gaussian convolution
- Windowed sinc filtering

---

## Signal Generation

The synthetic intensity signal is modeled as:

```math
I(t) = A \cdot \sin^2(2\pi f t + \phi) + \alpha \cdot \mathcal{N}(0, 1)
```

Where:
- `A` is the amplitude,
- `f` is the frequency (Hz),
- `φ` is the phase (radians),
- `α` controls noise level (Gaussian noise),
- `𝒩(0,1)` is standard normal noise.

The notebook includes a Python function:

```python
def adjustable_intensity(t, A, f, phi, alpha):
    pure_intensity = A * (np.sin(2 * np.pi * f * t + phi))**2
    noise = alpha * np.random.randn(len(t))
    return np.clip(pure_intensity + noise, 0, None)
```

This function simulates both noise-free and noisy intensity data. The visibility is then calculated using:

```math
V = \frac{I_{\text{max}} - I_{\text{min}}}{I_{\text{max}} + I_{\text{min}}}
```

---

## Dependencies

The notebook requires the following Python libraries:
- `numpy`
- `matplotlib`
- `scipy`
- `pandas`

Install using:
```bash
pip install numpy matplotlib scipy pandas
```

---

## Features

- Simulates optical signals with controlled noise
- Applies smoothing filters to recover clean signals
- Compares FFT and curve fitting for visibility estimation
- Visualizes raw, filtered, and reconstructed signals
- Evaluates performance based on RMSE and recovered visibility

---

## Use Case

This project is intended for:
- Researchers analyzing optical interference data
- Signal processing practitioners working with periodic signals
- Physics students learning about noise and signal recovery

---

## Output

The notebook produces:
- Time-domain plots of pure and noisy signals
- Filtered signal visualizations
- Estimated visibility values for comparison
- RMSE metrics and evaluation summary

