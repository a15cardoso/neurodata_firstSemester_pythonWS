# neurodata_firstSemester_pythonWS# Reverse-Engineering Project — Team 03

## 1. Inferred Model & Parameters
- **Drift Offset:** -0.0344 mV
- **Drift Amplitude:** 0.6306 mV
- **Drift Frequency:** 0.4990 Hz
- **Drift Phase:** 1.4818 rad
- **Spike Amplitude:** 5.0142 mV
- **Spike Decay Constant (tau):** 0.2958 ms
- **Noise Std Dev (sigma):** 0.3444 mV
- **Firing Rate:** 42.00 Hz

## 2. Assumptions
- The baseline drift is modeled as a low-frequency pure sinusoid: $A \sin(2\pi f t + \phi) + \text{offset}$.
- Spikes exhibit an immediate step voltage increase followed by a first-order exponential decay ($V_0 e^{-t/\tau}$).
- Background noise is zero-mean additive white Gaussian noise (AWGN) estimated from quiet periods.
- Reconstructed signal contains structured components only ($drift + spikes$), omitting noise realization.

## 3. Detection & Reconstruction Method
1. **Spike Detection:** Rising-edge thresholding at $\text{Mean} + 4\sigma$.
2. **Quiet Baseline Masking:** Masking a 15 ms post-onset window for each detected spike.
3. **Drift Estimation:** Ordinary Least Squares (OLS) grid search across frequencies ($0.02 - 0.5$ Hz) on quiet baseline samples.
4. **Decay Dynamics:** Log-linear fitting on average spike profile to estimate $\tau$.
