# BNP Paribas Fraud Detection Challenge


## Project Overview

This project implements a machine learning model for **fraud detection** in customer transactions, developed as part of the **BNP Paribas Fraud Detection Challenge**. The goal is to predict fraudulent transactions using customer purchase data and optimize the **Precision-Recall Area Under Curve (PR-AUC)** metric to accurately identify fraudulent transactions while minimizing false positives.

Our team achieved **1st place** on both the **public and private leaderboards** in 2024 with a final **test PR-AUC score of 0.3507**, significantly outperforming the benchmarks.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Context](#context)
3. [Dataset](#dataset)
4. [Objective](#objective)
5. [Approach](#approach)
6. [Evaluation Metrics](#evaluation-metrics)
7. [Results](#results)
8. [Team](#team)
9. [Acknowledgments](#acknowledgments)
10. [Contributing](#contributing)

---

## Context

**BNP Paribas Personal Finance**, a leader in consumer financing in Europe, is increasingly focused on combating fraud. Detecting fraud is a complex problem, especially when the fraudulent transactions are rare and can be disguised by fraudsters who adapt their behavior to avoid detection.

The **BNP Paribas Fraud Detection Challenge** aimed to build models that predict the likelihood of fraud in transaction data, where the challenge is to detect fraudulent activity despite its low occurrence (~1.4% of transactions).

---

## Dataset

The dataset provided consists of 147 features describing transaction details for 115,988 customer purchases. It includes both transaction-level and item-level details across **115,988 observations**.

### Key Features:
- **ID**: Unique transaction identifier.
- **Nb_of_items**: Number of unique items in the basket.
- **item1–item24**: Product categories.
- **cash_price1–cash_price24**: Price of each item.
- **make1–make24**: Manufacturer of each item.
- **model1–model24**: Product model.
- **goods_code1–goods_code24**: Item codes.
- **Nbr_of_prod_purchas1–Nbr_of_prod_purchas24**: Quantity of products per item.

### Target Variable:
- **fraud_flag**: Binary variable indicating if a transaction was fraudulent (1) or legitimate (0).

### Class Distribution:
- Fraud (Y=1): ~1.4% (1,681 observations)
- Non-Fraud (Y=0): ~98.6% (114,307 observations)

---

## Objective

The project’s objective was to develop a machine learning model capable of identifying fraudulent transactions from transaction data, using **Precision-Recall AUC (PR-AUC)** as the primary evaluation metric. The challenge focuses on dealing with **imbalanced datasets**, where fraud cases constitute only a small fraction of the total observations.

---

## Approach

### Data Preprocessing
1. **Data Cleaning & Feature Engineering**:
   - Handled missing values and irrelevant columns (e.g., `goods_code`).
   - Merged duplicate categorical variables and aggregated basket-level data.
   - One-hot encoded categorical variables to avoid introducing artificial ordinal relationships.

2. **Encoding & Imputation**:
   - Applied one-hot encoding for categorical variables (e.g., product categories, manufacturer).
   - Filled missing values in numerical features (`cash_price`, `Nbr_of_prod_purchas`) using `.fillna()`.

3. **Train-Test Split**:
   - The dataset was split into an **80% training** set and **20% test** set, ensuring the fraud distribution was consistent across both sets.

### Model Selection
Several classification models were evaluated, including:
- **Decision Tree**
- **Logistic Regression**
- **Random Forest**
- **Gradient Boosting (Best Model)**

The **Gradient Boosting Classifier** performed the best after hyperparameter tuning.

---

## Evaluation Metrics

Given the **imbalanced nature** of the dataset, accuracy was not an appropriate metric. Instead, the **Precision-Recall AUC (PR-AUC)** was used to evaluate model performance, as it emphasizes the detection of the minority fraud class.

### PR-AUC Formula:

The **Precision-Recall Area Under the Curve (PR-AUC)** is calculated as follows:

$\text{PR-AUC} = \sum_{n} (\text{Recall}_n - \text{Recall}_{n-1}) \times \text{Precision}_n$

Where:
- **Precision** is the ratio of true positives (TP) to the total predicted positives:
  $$
  \text{Precision} = \frac{TP}{TP + FP}
  $$
- **Recall** is the ratio of true positives (TP) to the total actual positives:
  $$
  \text{Recall} = \frac{TP}{TP + FN}
  $$

The **average_precision_score** function from **scikit-learn** was used to compute the PR-AUC score.


---

## Results

### Final PR-AUC Score: 0.3507
- **1st place** on both the public and private leaderboards.

### Benchmarks:
- **Benchmark 1** (Random Guessing): 0.017
- **Benchmark 2** (Optimized ML Model): 0.14
- Our model significantly outperformed these benchmarks.

---

## Team

This project was conducted as part of our **Machine Learning project** in the second year of our **Double Bachelor’s Degree in Artificial Intelligence and Organizational Sciences** at **Paris Dauphine University**.

### Team Members:
- **BERNARDI Julien**
- **JIN Clémence**
- **MOUANGUE Cameron**
- **CHEN Franck**

---

## Acknowledgments

I would like to thank **Tony Bonnaire** for his guidance and support throughout this project. His insights were invaluable in shaping the direction of our work.

---

## Contributing
Contributions are welcome! If you'd like to contribute, please follow these steps:

1. **Fork the repository.**
2. **Create a new branch** for your feature or bugfix:
    ```bash
    git checkout -b feature/your-feature-name
    ```
3. **Commit your changes**:
    ```bash
    git commit -m "Add your commit message here"
    ```
4. **Push to the branch**:
    ```bash
    git push origin feature/your-feature-name
    ```
5. **Open a pull request** and describe your changes.
