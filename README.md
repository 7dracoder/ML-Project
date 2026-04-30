# Scaling Laws for Language Models Trained on SVG Code

**CS-GY 6923 Optional Project — Spring 2026**  
**Tanmay Sahu** (ts5888@nyu.edu) — NYU Tandon

## What This Is

A scaling laws study training GPT-style transformers on SVG (Scalable Vector Graphics) code. We train 5 model sizes from 1.4M to 88.6M parameters on 115M tokens of SVG data and fit power-law scaling curves.

## Key Results

| Metric | Value |
|--------|-------|
| Training tokens | 112.7M |
| Power law exponent (α) | 0.81 |
| Power law R² | 0.956 |
| Best test perplexity | 1.57 |
| SVG render rate | 54% |
| 10× extrapolation | 0.495 [0.47, 0.52] |

## What We Tried

- **Standard Parameterization (SP):** Fixed LR from Tiny sweep degrades at Large/XL (expected). Sqrt-scaled LR gives a clean scaling curve.
- **µP (Maximal Update Parameterization):** Used the `mup` library with attention scaling `1/d_head`, `MuReadout`, and `MuAdam`. Did not achieve competitive performance — `set_base_shapes` couldn't properly track our custom architecture. Honest negative result.
- **SVG Generation:** XL model trained for 3 epochs generates valid SVGs 54% of the time. Post-processing auto-closes unclosed SVG tags.

## Project Structure

```
├── notebooks/
│   ├── Part1_Data_Preprocessing.ipynb   # Data collection, BPE tokenization
│   ├── Part2_Scaling_Study.ipynb        # SP scaling with 5 model sizes
│   ├── Part3_muP_Scaling.ipynb          # µP investigation
│   ├── Part4_Generation.ipynb           # Extended training + sample generation
│   └── Part5_Analysis.ipynb             # Final figures and report numbers
├── output/                              # Plots and figures for the report
├── report.tex                           # LaTeX report
└── optional-project-spring26.pdf        # Project spec
```

## How to Run

1. Upload notebooks to Google Colab (GPU runtime required)
2. Run in order: Part 1 → 2 → 3 → 4 → 5
3. Each notebook saves results to Google Drive under `svg_scaling_v2/`
4. Copy plots from Drive to `output/` folder for the report
