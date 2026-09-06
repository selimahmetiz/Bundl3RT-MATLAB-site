# Real-Time Bundle Adjustment for Ultra-High-Resolution UAV Imagery

## Adaptive Patch-Based Feature Tracking

<p align="center">
  <img src="docs/figures/Figure_8.png" alt="Real-time bundle adjustment across multiple flight strips" width="90%">
</p>

<p align="center">
  <b>Fast, full-resolution bundle adjustment for real-time UAV mapping.</b>
</p>

---

## Overview

Real-time aerial mapping requires accurate camera orientations to be estimated while the UAV is still in flight.

This becomes particularly challenging for **ultra-high-resolution UAV imagery**, where feature extraction, feature matching, and bundle adjustment can become computationally expensive.

Conventional approaches often address this problem by:

- downsampling the imagery,
- limiting the number of features,
- processing images offline, or
- relying heavily on GNSS/IMU navigation without image-based correction.

These strategies can reduce computational cost, but they may also sacrifice image information or fail to correct accumulated navigation errors.

This project presents a lightweight **real-time Bundle Adjustment (BA) framework** that operates directly on full-resolution UAV imagery without downsampling.

The method combines:

- adaptive patch-based feature tracking,
- UAV GNSS/IMU navigation,
- image-footprint projection,
- a coarse Digital Surface Model (DSM),
- patch-constrained feature matching, and
- localized bundle adjustment over overlapping image clusters.

The framework is designed for integration into the **DLR Modular Aerial Camera System (MACS)** and targets time-critical applications such as disaster response, infrastructure monitoring, and coastal protection.

---

## Key Idea

The central idea is simple:

> **Use navigation and coarse terrain information to predict where image features should appear, then perform bundle adjustment only where it is needed.**

Instead of searching for correspondences across entire 50 MP images, each image is divided into smaller patches.

The patches are spatially propagated between images using available GNSS/IMU information and terrain-aware footprint projection.

Only corresponding patch regions are searched for features.

The resulting correspondences are then used by a localized bundle adjustment operating on a sliding cluster of overlapping images.

```text
                  UAV Image Stream
                         │
                         ▼
              Full-Resolution Image
                         │
                         ▼
                  Patch Division
                         │
                         ▼
             GNSS / IMU + Coarse DSM
                         │
                         ▼
              Patch Spatial Prediction
                         │
                         ▼
            Patch-Constrained Matching
                         │
                         ▼
              Local Feature Tracks
                         │
                         ▼
            Sliding-Window Bundle
                 Adjustment
                         │
                         ▼
              Refined Camera Poses
                         │
                         ▼
            Real-Time Aerial Mapping
```

--rname.github.io`), remove the
   `BASE_PATH` line from the workflow so the site builds for `/`.
