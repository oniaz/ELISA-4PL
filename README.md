# ◈ 4PL Model Fitting — ELISA Standard Curve Analyzer

A clean, minimal web app for fitting **Four-Parameter Logistic (4PL)** curves to ELISA standard curve data and calculating sample concentrations from OD readings.

Built with Python + Streamlit.

---

## What it does

In ELISA, you run a series of standards with known concentrations and measure their optical density (OD). This app:

1. Takes your standard concentration and OD values
2. Fits a 4PL curve to the data
3. Lets you enter unknown sample OD values and back-calculates their concentrations
4. Flags extrapolated results (OD outside standard curve range)
5. Shows R² so you can assess fit quality
6. Exports results to CSV

---

## The 4PL Model

The Four-Parameter Logistic equation used is:

```
y = D + (A - D) / (1 + (x / C)^B)
```

| Parameter | Description |
|-----------|-------------|
| A | Bottom asymptote (minimum response) |
| B | Hill slope (steepness of the curve) |
| C | EC50 / inflection point |
| D | Top asymptote (maximum response) |

---

## Getting started

### Requirements

```bash
pip install streamlit numpy scipy matplotlib pandas
```

### Run locally

```bash
streamlit run app.py
```
---

## How to use

### Entering standard curve data

You have two input modes:

**Bulk** — paste all values comma-separated:
```
Concentration: 0, 10, 20, 40, 80, 160
OD:            0.05, 0.18, 0.35, 0.62, 0.95, 1.28
```

**One by one** — add each concentration/OD pair individually using the `+ Add another point` button. Good for entering values directly from your plate reader as you go.

### Fitting the model

Click **▶ FIT MODEL**. The app will:
- Validate your inputs (minimum 4 points, no negative concentrations)
- Warn you about duplicate concentration values
- Display the fitted curve and parameters A, B, C, D
- Show R² with a color-coded quality indicator

| R² | Quality |
|----|---------|
| ≥ 0.99 | Excellent ✓ |
| ≥ 0.95 | Acceptable |
| < 0.95 | Poor — check your data |

### Calculating sample concentrations

Enter your sample's OD value and click **⊕ CALCULATE CONCENTRATION**.

- Results within the standard curve range are shown normally
- Results outside the range are flagged with a ⚠ extrapolation warning — treat these with caution

All results are logged in the **Results History** table with the fit number they belong to, so you can tell which results came from which standard curve if you re-fit mid-session.

### Exporting

Click **⬇ Export CSV** to download all calculated results.

---

## Project structure

```
.
├── app.py            # Main Streamlit app
├── requirements.txt  # Python dependencies
└── README.md
```

---

## Built by

Omnia Abouhaikal · [@oniaz](https://github.com/oniaz)