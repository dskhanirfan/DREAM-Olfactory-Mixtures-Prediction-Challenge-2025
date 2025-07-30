# DREAM-Olfactory-Mixtures-Prediction-Challenge-2025

[Raw Data]
    │
    │ Preprocessing: log₁₀ normalization, z-score scaling, correlation filtering, NaN replacement
    ▼
┌─────────────────────────────────────────────┐
│ Step 1: Initial Ensemble                    │
│ (Predicting Pleasantness & Intensity)       │
│ • GBM                                       │
│ • Decision Trees (rpart)                    │
│ • Elastic Net regression                    │
│ ─────────────────────────────────────────── │
│ Harmonic Mean Aggregation                   │
└─────────────────────────────────────────────┘
    │
    │ Pleasantness & Intensity Predictions
    ▼
┌─────────────────────────────────────────────┐
│ Step 2: Bayesian Ensemble Multiple Kernel   │
│ Learning (BEMKL)                            │
│ Inputs (Views):                             │
│ • Pleasantness                              │
│ • Intensity                                 │
│ • Log-transformed Dilution                  │
│ • Morgan Fingerprints                       │
│ • Mordred Fingerprints                      │
│ • OpenPOM Features                          │
│ ─────────────────────────────────────────── │
│ Kernels: Polynomial, Linear, Jaccard        │
│ ─────────────────────────────────────────── │
│ Averaged Predictions                        │
└─────────────────────────────────────────────┘
    │
    │ BEMKL Predictions
    ▼
┌─────────────────────────────────────────────┐
│ Step 3A: CatBoost                           │
│ (Standard Training)                         │
│ • Grid Search Hyperparameter Tuning         │
└─────────────────────────────────────────────┘
    │
    │
    ├─────────────┐
    │             ▼
    │    ┌────────────────────────────────────┐
    │    │ Step 3B: Intensity-weighted        │
    │    │ CatBoost                           │
    │    │ • Intensity-weighted Training      │
    │    │ • Grid Search Hyperparameter Tuning│
    │    └────────────────────────────────────┘
    │             │
    ▼             ▼
[Final Stacked Predictions: Ridge Regression]
    │
    ▼
[Final Submission]
