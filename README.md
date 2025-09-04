# ASR Analysis - Redacted

This repository contains a comprehensive analysis of how phonological features relate to Word Error Rate (WER) in Whisper v3, comparing original vs Cartesia-transformed audio across French and Spanish languages.

## Overview

**Goal:** Explain model behavior by relating phonological features to Word Error Rate, and compare **original** vs **Cartesia-transformed** audio.

**Dataset:** French & Spanish utterances with acoustic features (RMS amplitude, DC offset, articulation rate, mean pitch, pitch std. dev., HNR) and WER labels for original and transformed audio.

## Analysis Structure

1. **Data preparation** - Load files, align original vs transformed data, split into training/holdout
2. **Descriptive statistics** - Basic summaries and exploratory data analysis
3. **Δ-regressions** - Analyze changes in features and their relationship to WER changes
4. **WER_orig → WER_trans mapping** - Predict transformed WER from original WER and feature changes
5. **Holdout validation** - Robustness checks on held-out data
6. **Statistical tests** - Chi-squared and binomial tests for independence and improvement rates

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
- **Improvement rates:** Both languages show significantly more worsening than improvement after transformation

## Files

- `inference_analysis.ipynb` - Main analysis notebook

## Requirements

The notebook requires the following Python packages:
- pandas >= 1.3.0
- numpy == 1.22.3
- matplotlib == 3.5.3
- seaborn == 0.11.2
- statsmodels
- scikit-learn
- scipy

## Usage

1. Clone this repository
2. Install dependencies: `pip install pandas numpy matplotlib seaborn statsmodels scikit-learn scipy`
3. Run the Jupyter notebook: `jupyter notebook inference_analysis.ipynb`

## Results Summary

The analysis reveals that:

1. **Whisper performance is primarily stable** across Cartesia transformations - original WER strongly predicts transformed WER
2. **French is more sensitive** to acoustic feature changes than Spanish
3. **Cartesia transformation generally worsens performance** in both languages, but the effect is stronger in French
4. **Articulation rate and harmonicity** are the most important features for understanding transformation effects in French

## Contact

For questions about this analysis, please open an issue in this repository.
