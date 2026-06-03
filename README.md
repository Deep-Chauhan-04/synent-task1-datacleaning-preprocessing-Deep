# Titanic Data Cleaning & Preprocessing

This repository contains a Jupyter Notebook ([Task1.ipynb](Task1.ipynb)) dedicated to the initial exploration, cleaning, and preprocessing of the classic Titanic passenger dataset ([Titanic-Dataset.csv](Titanic-Dataset.csv)). The processed and cleaned dataset is saved as [titanic_cleaned.csv](titanic_cleaned.csv).

## Table of Contents
- [Overview](#overview)
- [Dataset Specifications](#dataset-specifications)
- [Preprocessing Pipeline](#preprocessing-pipeline)
- [Installation and Setup](#installation-and-setup)

---

## Overview

The primary goal of this task is to transform the raw Titanic dataset into a clean, well-structured format suitable for exploratory data analysis (EDA) and machine learning modeling. 

The pipeline handles:
- Missing value identification and imputation
- Duplicate detection and removal
- Data type normalization (casting to appropriate numeric/categorical types)
- Column renaming to improve clarity and standardize formatting (snake_case)

---

## Dataset Specifications

The input dataset ([Titanic-Dataset.csv](Titanic-Dataset.csv)) consists of **891 rows** and **12 columns**:

| Column Name | Description |
| :--- | :--- |
| **PassengerId** | Unique identifier for each passenger |
| **Survived** | Survival status (0 = No, 1 = Yes) |
| **Pclass** | Passenger class (1 = 1st, 2 = 2nd, 3 = 3rd) |
| **Name** | Full name of the passenger |
| **Sex** | Gender of the passenger |
| **Age** | Age in years |
| **SibSp** | Number of siblings/spouses aboard |
| **Parch** | Number of parents/children aboard |
| **Ticket** | Ticket number |
| **Fare** | Passenger fare |
| **Cabin** | Cabin number |
| **Embarked** | Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton) |

---

## Preprocessing Pipeline

The notebook ([Task1.ipynb](Task1.ipynb)) walks through the following sequential steps:

### 1. Data Inspection
- Loads the dataset using `pandas`.
- Checks the shape of the dataset (`891` rows, `12` columns).
- Diagnoses missing values across all features. Initial counts:
  - **Age**: 177 missing values
  - **Cabin**: 687 missing values
  - **Embarked**: 2 missing values

### 2. Missing Value Imputation
- **Age**: Filled missing values with the **median** age of the passengers (`28`).
- **Cabin**: Replaced missing cabin codes with the placeholder `'Unknown'`.
- **Embarked**: Imputed missing embarkation ports using the **mode** (most frequent port, which is `'S'` - Southampton).

### 3. Duplicate Handling
- Scans for duplicate rows across all fields.
- Deduplicates using `drop_duplicates(keep='first')` if duplicates are found (0 duplicates were present in the source dataset).

### 4. Data Type Normalization
- Converts **Age** from float to integer (`int`).
- Casts structural categorical columns (**Survived**, **Pclass**, **Sex**, **Embarked**) to `category` type to optimize memory usage and compatibility with plotting libraries.

### 5. Column Standardization (Renaming)
Renames the original columns to follow a standardized `snake_case` format and use more descriptive naming conventions:

| Original Column Name | Cleaned Column Name | Type |
| :--- | :--- | :--- |
| `PassengerId` | `passenger_id` | `int64` |
| `Survived` | `is_survived` | `category` |
| `Pclass` | `passenger_class` | `category` |
| `Name` | `passenger_name` | `object` |
| `Sex` | `gender` | `category` |
| `Age` | `age` | `int64` |
| `SibSp` | `siblings_spouses_count` | `int64` |
| `Parch` | `parents_children_count` | `int64` |
| `Ticket` | `ticket_number` | `object` |
| `Fare` | `fare_paid` | `float64` |
| `Cabin` | `cabin_code` | `object` |
| `Embarked` | `embarkation_port` | `category` |

---

## Installation and Setup

### Prerequisites
Make sure you have Python 3.8+ installed along with Jupyter Notebook or JupyterLab.

### Install Dependencies
You can install the required packages using the `requirements.txt` file or manually via pip:

```bash
pip install pandas numpy jupyter
```
