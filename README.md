# Probability Distribution Analysis

## Overview

This project performs advanced mathematical analysis on air quality data (NO₂ levels) by fitting a custom probability distribution function to normalized and transformed data. The code demonstrates data manipulation, statistical analysis, and curve fitting using Python.

## Project Structure

- **Advance_Mathematics.ipynb** - Jupyter Notebook containing the complete analysis with interactive cells and visualizations
- **advance_mathematics.py** - Python script version of the analysis
- **README.md** - This documentation file

## Dependencies

The following Python packages are required:
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computing
- **matplotlib** - Plotting and visualization
- **scikit-learn** - Machine learning utilities
- **scipy** - Scientific computing (specifically `curve_fit` for optimization)

Install dependencies with:
```bash
pip install pandas numpy matplotlib scikit-learn scipy
```

## Code Workflow

### 1. Data Loading
- Loads air quality data from a CSV file containing NO₂ concentration levels
- Uses pandas with 'latin1' encoding for compatibility

### 2. Data Transformation
- Extracts NO₂ values from the dataset
- Applies a sinusoidal transformation: `z = x + ar * sin(br * x)`
  - `ar = 0.05 * (r % 7)` where r = 102303596
  - `br = 0.3 * ((r % 5) + 1)`
- This transformation adds a mathematical component to the original data

### 3. Normalization
- Calculates mean (`z_mean`) and standard deviation (`z_std`) of transformed data
- Normalizes the data: `z_norm = (z - z_mean) / z_std`
- Standard normal distribution is centered at 0 with unit variance

### 4. Histogram Computation
- Creates histogram with 30 bins from normalized data
- Uses density=True to obtain probability density function (PDF) values
- Calculates bin centers for curve fitting

### 5. PDF Model Definition
The fitted model is a Gaussian-like function:
```
pdf_model(x) = c * exp(-λ * (x - μ)²)
```

Where:
- **c** - Amplitude/scaling factor
- **λ** - Shape parameter (controls width)
- **μ** - Mean/location parameter

### 6. Curve Fitting
- Uses `scipy.optimize.curve_fit()` with initial parameters:
  - `c₀ = max(histogram values)`
  - `λ₀ = 1.0`
  - `μ₀ = 0.0`
- Optimization bounds: λ and μ constrained to realistic ranges
- Performs up to 50,000 function evaluations for convergence

### 7. Results & Visualization

#### Plot 1: Full Range PDF Fit
Displays:
- Histogram of normalized data (blue bars with 50% transparency)
- Fitted PDF curve (orange line)
- Legend and title

#### Plot 2: Zoomed PDF Fit (1st - 99th Percentile)
Zooms into the central distribution:
- Same histogram and fitted curve
- X-axis limited from 1st to 99th percentile
- Better visualization of the distribution core
- Reduces visual distortion from extreme outliers

### Visualization Output

![PDF Fit Plot](pdf_fit.png)

## Output

The program prints the fitted parameters:
```
FINAL PARAMETERS
c = [estimated value]
lambda = [estimated value]
mu = [estimated value]
```

## How to Run

### Using Jupyter Notebook
```bash
jupyter notebook Advance_Mathematics.ipynb
```
Then run each cell sequentially or use "Run All Cells" option.

### Using Python Script
```bash
python advance_mathematics.py
```

## Notes

- The original notebook was created in Google Colab (see header comment in advance_mathematics.py)
- The data file path (`/content/data.csv`) is specific to Colab and needs to be modified for local execution
- Update the CSV file path to your local data location: `df = pd.read_csv("your_local_path/data.csv")`

## Mathematical Background

The analysis demonstrates:
- **Data normalization** for standardized statistical analysis
- **Curve fitting** to model empirical distributions
- **Non-linear optimization** using least-squares method
- **Probability distributions** and their parameters

The fitted exponential-quadratic function approximates the shape of the empirical distribution, allowing you to:
- Model the distribution probabilistically
- Predict probabilities for data ranges
- Compare with theoretical distributions

## Author Notes

This project is part of an advanced mathematics/statistics course and demonstrates practical application of curve fitting techniques to real-world air quality data.

