# rainfall-runoff-modelling
Simple Python rainfall–runoff model using the SCS Curve Number method
# Rainfall–Runoff Modelling (SCS Curve Number Method)

This project uses Python to implement a simple rainfall–runoff model based on the SCS Curve Number method. It demonstrates basic hydrological modelling, data analysis, and visualisation.

## What the project does
- Loads a CSV file with daily rainfall values
- Applies the SCS Curve Number method to estimate runoff
- Calculates runoff depth for each day
- Plots rainfall vs runoff for easy interpretation

## Tools used
- Python
- Pandas
- NumPy
- Matplotlib

## How to run
1. Install the required libraries:
2. Run the script:

## Why I built this
My MSc research involved rainfall–runoff modelling, and I have worked with hydrological datasets throughout my engineering career. This project shows how I can apply Python to implement a simple hydrological model and analyse rainfall–runoff relationships.
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset (replace with your own CSV if needed)
df = pd.read_csv("rainfall_data.csv")

# SCS Curve Number parameters
curve_number = 75  # example value
S = (25400 / curve_number) - 254  # potential maximum retention (mm)

def scs_runoff(P):
    """Calculate runoff using the SCS Curve Number method."""
    if P <= 0.2 * S:
        return 0
    else:
        return ((P - 0.2 * S) ** 2) / (P + 0.8 * S)

# Apply model
df["runoff"] = df["rainfall"].apply(scs_runoff)

# Plot
plt.figure(figsize=(12, 6))
plt.plot(df["date"], df["rainfall"], label="Rainfall (mm)")
plt.plot(df["date"], df["runoff"], label="Runoff (mm)", linestyle="--")
plt.xlabel("Date")
plt.ylabel("Depth (mm)")
plt.title("Rainfall–Runoff Modelling (SCS Curve Number Method)")
plt.legend()
plt.grid(True)
plt.show()
date,rainfall
2024-01-01,5
2024-01-02,0
2024-01-03,12
2024-01-04,3
2024-01-05,25
2024-01-06,40
2024-01-07,2
2024-01-08,10
2024-01-09,0
2024-01-10,18
