# Wideband Source Localization with a Uniform Linear Microphone Array

Tracks the time-varying **direction of arrival (DOA)** of a moving sound source from a 16-channel MEMS microphone array, using a **delay-and-sum beamformer** adapted to wideband signals. MATLAB.

Homework 1 for the course *Sound Analysis, Synthesis and Processing*, MSc in Music and Acoustic Engineering, Politecnico di Milano (a.y. 2023/2024).

## Setup

- **Array:** EStick, a uniform linear array of M = 16 MEMS microphones, total length 45 cm (3 cm spacing), Audio-over-IP, sampled at 8 kHz
- **Scene:** one moving source in front of the array
- **Speed of sound:** 343 m/s
- **Recording:** `array_recordings.wav` (16 channels)

## Method

1. **Normalization** of the multichannel recording.
2. **Multichannel STFT** with a custom STFT implementation (`my_STFT.m`), window 1024, overlap 512.
3. **Narrowband beamforming:** for each frequency bin, each candidate angle (−90° to 90°, 1° steps) and each frame, the steering vector of the ULA is applied to the spatial covariance estimate of the frame, which gives the delay-and-sum output power (pseudospectrum). The maximum frequency without spatial aliasing is computed from the mic spacing.
4. **Wideband combination:** the narrowband pseudospectra are combined with a **geometric mean across frequencies**.
5. **DOA tracking:** the angle with maximum power in each frame gives the DOA over time.
6. **Visualization:** pseudospectrum map over time and angle, DOA curve, and an animated video of the estimated direction (`DOAs_estimation.avi`).

<!-- Add here: the pseudospectrum figure and a frame or GIF of the DOA video, plus one sentence on the result from SASP_HM_1_report.pdf -->

## Files

| File | Content |
|---|---|
| `Homework1.m` | Main script |
| `multichannel_stft.m`, `my_STFT.m` | Multichannel STFT |
| `compute_pseudospectrum.m` | Delay-and-sum pseudospectrum per frequency, angle and frame |
| `my_plots.m`, `my_videos.m` | Figures and DOA animation |
| `DOAs_estimation.avi` | Output video |
| `SASP_HM_1_report.pdf` | Full report |
| `assigment_HW1.pdf` | Assignment text |

## How to run

Open MATLAB in the repository folder and run `Homework1.m`.
