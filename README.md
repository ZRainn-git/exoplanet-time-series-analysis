# Exoplanet Time-Series Analysis and Orbital Period Estimation

Time-series analysis of NASA Kepler light curves using signal-processing techniques to identify periodic transit signatures and estimate exoplanet orbital periods.

This project investigates how different time-series methods perform on exoplanet light curves with varying levels of noise and signal structure. Rather than applying a single method to every target, I used the characteristics of each light curve to guide the choice of filtering and period-estimation techniques.

## Project Overview

Exoplanet transits produce periodic decreases in the observed brightness of a host star as a planet passes across the stellar disk. In real observational data, however, these signals can be obscured by stellar variability, noise, long-term trends, and transient features.

Using labeled light curves from NASA's **Kepler Space Telescope**, this project explores several approaches for recovering periodic structure from noisy astronomical time-series data.

The analysis focuses on four selected confirmed-exoplanet light curves exhibiting different signal characteristics:

- **Exoplanet 4:** periodic structure with substantial noise
- **Exoplanet 5:** comparatively clear repeating variability
- **Exoplanet 6:** highly noisy signal with no clearly recoverable periodicity
- **Exoplanet 7:** strong repeating transit-like dips with a harmonic-rich Fourier spectrum

The goal was not only to estimate orbital periods, but also to examine when different time-series techniques succeed or fail.

## Methods

The analysis was performed in Python using a combination of time-domain, frequency-domain, and time-frequency techniques.

Methods explored include:

- Light-curve normalization
- Fast Fourier Transform (FFT)
- Seasonal decomposition
- Hann-window smoothing
- Butterworth filtering
- Savitzky-Golay filtering
- Autocorrelation
- Peak detection
- Short-Time Fourier Transform (STFT) / spectrogram analysis
- Phase folding

Initial FFT spectra were used as diagnostics to determine the dominant frequency structure of each light curve. Different preprocessing and validation techniques were then selected according to the characteristics of each signal.

## Key Results

### Exoplanets 4 and 5 — Periodic Signals

Exoplanets 4 and 5 both exhibited repeating variability, but with different levels of noise.

For **Exoplanet 5**, seasonal decomposition was used to separate long-term trends from the repeating component. Applying an FFT to the seasonal component produced an estimated period of approximately:

**6.01 hours**

For the noisier **Exoplanet 4**, Hann-window smoothing was used before frequency-domain analysis. The dominant frequency produced an estimated period of approximately:

**5.99 hours**

These cases demonstrate how preprocessing can improve frequency-domain period estimation when long-term trends or noise interfere with the underlying periodic signal.

### Exoplanet 6 — Noisy and Transient Behaviour

Exoplanet 6 showed strong noise and no obvious stable periodic structure.

A **Savitzky-Golay filter** was used to remove broad trends while preserving sharper local features. The resulting FFT did not contain a sufficiently dominant frequency to support a reliable orbital-period estimate.

Instead, a **Short-Time Fourier Transform (STFT)** was used to investigate how the frequency content changed with time. A broadband power enhancement was observed near time step ~2850, corresponding to an isolated deviation in the light curve.

This demonstrated an important limitation of period-search techniques: not every apparent feature in an astronomical time series represents stable periodic behaviour.

### Exoplanet 7 — Validating an Orbital Period Across Multiple Methods

Exoplanet 7 provided the clearest example of repeating transit-like dips.

A straightforward FFT initially suggested a period of approximately **25.37 hours**. Visual inspection of the light curve showed that this estimate did not match the actual spacing between the major flux dips.

Several independent methods were therefore used to reassess the period:

- autocorrelation
- peak-to-peak spacing
- restricted low-frequency FFT analysis
- phase folding

Autocorrelation revealed a characteristic lag of approximately **200 time steps**, corresponding to roughly **100 hours**.

Peak detection and restricted-frequency FFT analysis produced estimates of approximately **101.77–106.57 hours**.

Finally, phase folding with a period of:

**≈ 101.77 hours**

aligned the repeating light-curve features, supporting this as a substantially more plausible period estimate than the initial FFT result.

This case highlights the importance of combining visual, statistical, and frequency-domain evidence rather than interpreting the strongest Fourier peak as an orbital period automatically.

## Example Results

Add selected figures from the `figures/` folder here once the final filenames are chosen.

Example syntax:

```markdown
![Phase-folded light curve](figures/your_filename.png)
```

## Dataset

The analysis uses the **Kepler Labelled Time Series Data** dataset, containing stellar light curves derived from observations by NASA's Kepler Space Telescope.

Each light curve contains slightly more than 3,000 sequential flux measurements sampled at **30-minute intervals**. The training dataset contains 37 objects labeled as confirmed exoplanet hosts.

Dataset source:

**Kepler Labelled Time Series Data — Kaggle**  
https://www.kaggle.com/datasets/keplersmachines/kepler-labelled-time-series-data

The files used in this analysis are:

```text
exoTrain.csv
exoTest.csv
```

## Repository Structure

```text
Exoplanet-Time-Series/
│
├── README.md
├── notebook/
│   └── exoplanet_time_series_analysis.ipynb
├── figures/
│   └── analysis figures
├── report/
│   └── final_report.pdf
└── data/
    ├── exoTrain.csv
    └── exoTest.csv
```

## Tools and Libraries

- Python
- NumPy
- Matplotlib
- SciPy
- statsmodels
- Jupyter Notebook

## Limitations and Future Work

The analysis demonstrates that dominant Fourier peaks do not necessarily correspond directly to an exoplanet's orbital period, particularly when sharp transit features generate strong harmonics.

Potential extensions include:

- Lomb-Scargle periodograms
- Gaussian-process regression for stellar variability
- Empirical mode decomposition
- automated transit detection
- machine-learning classification of Kepler light curves
- comparison with published orbital parameters

## Full Report

The original project report, including detailed methodology, interpretation, additional figures, and discussion, is available in the `report/` directory.

## Author

**Rain Zhao**

Undergraduate Physics / Astronomy  
Time-Series Analysis · Scientific Computing · Astronomical Data Analysis
