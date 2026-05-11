# Super Resolution on FFHQ: Total Variation vs U-Net

Computational Imaging Project — University Project 2025/26

Author: Vincenzo Lombardi

---

## Project Overview

This project investigates the Super Resolution (SR) problem in the context of Computational Imaging and inverse problems.

The goal is to reconstruct high-resolution facial images from degraded low-resolution observations and compare two different reconstruction paradigms:

- Classical variational regularization using Total Variation (TV)
- Deep learning reconstruction using a U-Net architecture

The project analyzes both quantitative and qualitative performance under different degradation conditions.

---

## Problem Formulation

The image degradation model is:

\[
y = Ax + n
\]

where:

- \(x\) = original high-resolution image
- \(A\) = degradation operator (downsampling)
- \(y\) = low-resolution observation
- \(n\) = additive white Gaussian noise (AWGN)

The Super Resolution problem is ill-posed because information is lost during downsampling and noise further destabilizes reconstruction.

---

## Dataset

The experiments use the FFHQ (Flickr-Faces-HQ) dataset:

- RGB images
- Resolution: 256×256
- ~4000 samples used

Dataset split:

- Training set: 3200 images
- Validation set: 400 images
- Test set: 400 images

---

## Degradation Pipeline

Each image undergoes the following degradation process:

1. Downsampling (\(\times 2\) or \(\times 4\))
2. Addition of Gaussian noise:
   - \(\sigma = 0.005\)
   - \(\sigma = 0.01\)
3. Bicubic upsampling back to 256×256

---

## Methods

### 1. Bicubic Interpolation (Baseline)

Simple interpolation-based reconstruction without learning or regularization.

### 2. Total Variation Regularization

Variational reconstruction based on:

\[
\hat{x} =
\arg\min_x
\left(
\|Ax-y\|^2 + \lambda TV(x)
\right)
\]

Implemented using:

- `skimage.restoration.denoise_tv_chambolle`

### 3. U-Net

Encoder-decoder convolutional neural network with skip connections.

Training setup:

- Loss: L1 Loss
- Optimizer: Adam
- Learning rate: \(10^{-3}\)
- Batch size: 8
- Epochs: 3

---

## Evaluation Metrics

The methods are evaluated using:

- PSNR (Peak Signal-to-Noise Ratio)
- SSIM (Structural Similarity Index)

Both quantitative and qualitative comparisons are presented.

---

## Main Results

The Total Variation method achieved the best overall performance in the tested configurations, particularly under higher noise conditions.

The U-Net produced competitive results but was limited by the reduced training time and computational constraints.

An important outcome of the project is that classical variational methods remain highly competitive even against deep learning approaches when data and computational resources are limited.

---

## Repository Structure

```text
notebooks/        → Jupyter notebook implementation
figures/          → plots and qualitative comparisons
results/          → quantitative evaluation tables
models/           → trained U-Net weights
report/           → LaTeX report and PDF
presentation/     → presentation slides
