# IPL Matches Data Exploration and Cleaning

A comprehensive analysis and data-cleaning workflow on the **IPL Matches Dataset (`matches.csv`)** using Python and Pandas.

---

## 📋 Overview
This project processes and cleans historical Indian Premier League (IPL) match data. The initial dataset contained **1,095 rows** and **20 columns**, capturing key details such as venue, participating teams, toss results, winners, margins of victory, and targets set.

---

## 🛠️ Step-by-Step Workflow

### 1. Data Loading & Initial Inspection
- **Environment Setup:** Mounted Google Drive and loaded `pandas` (`pd`).
- **Data Load:** Read `matches.csv` into a Pandas DataFrame (`df`).
- **Structure Check:**
  - `df.head()` & `df.tail(7)`: Visualized raw records.
  - `df.info()`: Identified data types (`int64`, `float64`, `object`).

### 2. Data Cleaning & Preprocessing
- **Duplicate Verification:** `df.duplicated().sum()` confirmed **0 duplicate records**.
- **Missing Value Identification:** Checked missing entries using `df.isnull().sum()` across key columns:
  - `city` (51 missing)
  - `player_of_match` (5 missing)
  - `winner` (5 missing)
  - `result_margin` (19 missing)
  - `target_runs` (3 missing)
  - `target_overs` (3 missing)
  - `method` (1,074 missing)
- **Cleaning Actions:**
  1. Dropped the `method` column due to high sparsity (>98% missing).
  2. Applied `df.dropna(inplace=True)` to strip incomplete rows, reducing dataset size to **1,028 clean rows**.
  3. Dropped the redundant `city` column using `df.drop(columns='city', inplace=True)`.

### 3. Summary Statistics (Cleaned Data)
Using `df.describe()` on numerical features (`target_runs`, `target_overs`, `result_margin`):
- **Average Target Runs:** ~165.66
- **Maximum Target Runs:** 288
- **Average Winning Margin:** ~17 runs

---

## 💻 Code Example

```python
import pandas as pd

# Load dataset
df = pd.read_csv('matches.csv')

# Data cleaning pipeline
df.drop(columns=['method'], inplace=True)
df.dropna(inplace=True)
df.drop(columns=['city'], inplace=True)

# Verification
print(f"Cleaned dataset shape: {df.shape}")
print(df.describe())
