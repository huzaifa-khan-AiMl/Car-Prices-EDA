# Car Prices EDA
 
Exploratory Data Analysis on a dataset of 50,000 used, damaged, and new car listings, focused on understanding pricing patterns for older vehicles.
 
## Objectives
 
- Understand dataset structure
- Detect data quality issues
- Clean the data
- Analyze relationships
- Generate insights
## Dataset
 
50,000 rows, 25 columns covering car identity (brand, model, year), condition (mileage, accident history), engine specs (horsepower, torque, fuel type), and pricing (price, price per km).
 
## Setup
 
This project uses a Python virtual environment to keep dependencies isolated.
 
```bash
git clone https://github.com/huzaifa-khan-AiMl/Car-Prices-EDA.git
cd Car-Prices-EDA
 
python3 -m venv car_project_env
source car_project_env/bin/activate
 
pip install -r requirements.txt
 
jupyter lab
```

# Open notebook/car_price.ipynb and run the cells from top to bottom
 
## Cleaning Decisions
 
A few cleaning steps in this project involved judgment calls, not just routine fixes:
 
- **Column names** were lowercased and stripped of extra whitespace, and columns with embedded units (e.g. `mileage(km)`) were renamed for easier access (e.g. `mileage`).
- **Duplicate rows** were checked across the full row (not a single column) before dropping, since single-column matches can occur by coincidence in continuous numeric fields.
- **Missing `priceperkm` values** were dropped, not imputed. Verification showed 2,454 of 2,459 missing values belonged to New cars (which don't carry this field) and only 5 belonged to Used cars. Since this analysis is scoped to older/used cars, dropping these rows removes New cars (out of scope) and a small number of incomplete Used records.
- **`options`** was intentionally left untouched in this pass — it's a free-text, comma-separated column with potential for future feature engineering (e.g. does having Navigation or Bluetooth affect price), but parsing it was out of scope for initial cleaning.
- **Binary categorical columns** (`accidenthistory`, `insurance`, `registrationstatus`) were converted to proper booleans for easier filtering and analysis.

## Status

Complete: data loading, cleaning, scoping, univariate analysis, 
bivariate and multivariate analysis, correlation analysis, 
and key findings summary

## Key Findings
- Mileage and car age are the strongest negative price predictors 
  (correlation -0.58 each), both acting as price ceilings
- Horsepower acts as a price floor — low HP limits price downward, 
  but high HP alone doesn't guarantee high price
- Accident history significantly reduces price; luxury-tier cars 
  (above ~$95,000) almost never carry accident history
- Brand shows a clear two-tier market: Porsche/Mercedes-Benz/Audi/BMW 
  medians above 16,000 USD vs mainstream brands under 8,000 USD
- Insurance and transmission have negligible effect on price and 
  can be safely excluded as predictors in future ML work
- Enginesize and torque correlate at 0.97 — essentially redundant 
  features for ML modeling
 
## Tools
 
Python, Pandas, NumPy, Matplotlib, Seaborn, JupyterLab — developed in WSL2 (Ubuntu).
