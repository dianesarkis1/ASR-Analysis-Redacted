# ASR Analysis

This repository contains a comprehensive analysis of how phonological features relate to Word Error Rate in Whisper v3, comparing original vs Cartesia-transformed audio across French and Spanish languages. For full python notebook, see https://github.com/dianesarkis1/ASR-Analysis-Redacted/blob/main/inference_analysis.ipynb

Note that this analysis is part of a larger research project on ASR models. 

## Overview

**Goal:** Explain model behavior by relating phonological features to Word Error Rate, and compare **original** vs **Cartesia-transformed** audio.

**Dataset:** French & Spanish utterances with acoustic features (RMS amplitude, DC offset, articulation rate, mean pitch, pitch std. dev., HNR) and WER labels for original and transformed audio.

## Key Findings

### General OLS Models
- **Low explained variance:** R² values are generally small (<10%), indicating these features explain only a small share of variation in WER
- **Key drivers:** articulation rate (+), mean pitch (-), and RMS amplitude (French only)
- **Language differences:** French performance is driven by more features than Spanish

### Delta Regressions
- **Very low model fit:** R² ≤2%, reflecting high noise in ΔWER relative to small systematic feature shifts
- **French:** Only ΔHNR is significant (positive correlation with increased transformed WER)
- **Spanish:** No Δfeatures were significant

### WER Mapping
- **Original WER is the strongest predictor** of transformed WER in both languages
- **French:** Δarticulation_rate (negative) and ΔHNR (positive) are significant after controlling for original WER
- **Spanish:** Only original WER matters; Δfeatures remain insignificant

### Statistical Tests
- **Feature-WER associations:** All features show significant but weak associations with WER category in French; no significant associations in Spanish
- **Transformation effects:** French shows significant increase in high-WER cases after transformation; Spanish shows no significant difference
- **Improvement rates:** Both languages show significantly more worsening than improvement after Cartesia transformation, but the effect is stronger in French

## Requirements

The notebook requires the following Python packages:
- pandas >= 1.3.0
- numpy == 1.22.3
- matplotlib == 3.5.3
- seaborn == 0.11.2
- statsmodels
- scikit-learn
- scipy
