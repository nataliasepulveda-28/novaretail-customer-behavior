# NovaRetail+ Customer Behavior and Annual Revenue

An exploratory correlation analysis of 15,000 e-commerce customers, to identify which behavioral factors are most strongly associated with the **annual revenue** each customer generates.

**Tech stack:** Python · pandas · NumPy · SciPy · seaborn · Matplotlib · Jupyter Notebook

---

## Overview

NovaRetail+ is an e-commerce platform in Latin America with millions of users. For the close of 2024, its **Growth and Retention** team wants to know where to focus: which customer behaviors move revenue, and which ones do not.

This project analyzes customer-level data (activity, purchases, advertising exposure, satisfaction, subscription status, device and region) and measures how each variable relates to annual revenue, using the right coefficient for each type of variable.

> **Correlation is not causation.** This is an exploratory analysis: it identifies associations between variables, not cause-and-effect relationships.

## Objectives

1. Validate and prepare the dataset, documenting the assumptions behind the analysis.
2. Visualize how the numeric variables relate to each other and to annual revenue.
3. Quantify those relationships with appropriate coefficients (Pearson, Spearman, point-biserial and Cramér's V).
4. Translate the evidence into findings and business implications for the Growth and Retention team.

## Data

The dataset has **15,000 customers** and **12 variables**, with no missing values.

| Group | Variables |
|---|---|
| Customer profile | `edad` (age), `nivel_ingreso` (estimated annual income), `region`, `tipo_dispositivo` (device type) |
| Behavior | `visitas_mes` (monthly visits), `compras_mes` (monthly purchases), `gasto_publicidad_dirigida` (targeted ad spend), `satisfaccion` (1–5 rating) |
| Status | `miembro_premium` (premium subscription), `abandono` (churn) |
| Target metric | `ingreso_anual` (annual revenue generated for the company) |

Variable names are kept in Spanish, as in the source dataset.

## Methodology

The notebook is organized in six sections:

1. **Load and explore** the dataset: structure, data types and ranges.
2. **Prepare the data and document assumptions:** convert the binary columns to boolean, review numeric, binary and categorical variables, and state the assumptions.
3. **Visualize relationships:** correlation heatmap and scatterplots for the key pairs.
4. **Quantify with coefficients:** the method is chosen according to the type of variables.
5. **Findings** and their business implications.
6. **Limitations and next steps.**

| Relationship | Coefficient | Why |
|---|---|---|
| Numeric vs. numeric | Pearson and Spearman | Pearson captures linear relationships; Spearman captures monotonic ones and does not require normality |
| Numeric vs. binary | Point-biserial | Designed for one numeric and one binary variable |
| Categorical vs. categorical | Cramér's V | Measures association between categorical variables |

## Key findings

| Relationship | Result | Reading |
|---|---|---|
| `compras_mes` and `ingreso_anual` | Pearson 0.967 · Spearman 0.967 | By far the strongest association, almost perfectly linear |
| `visitas_mes` and `ingreso_anual` | Pearson 0.337 · Spearman 0.321 | Positive but weak and highly dispersed |
| `abandono` and `ingreso_anual` | Point-biserial -0.003 | No detectable linear relationship |
| `miembro_premium` and `ingreso_anual` | Point-biserial 0.093 | Premium customers generate very slightly more revenue |
| `region` and `tipo_dispositivo` | Cramér's V 0.012 | Practically independent |
| `region` and `miembro_premium` | Cramér's V 0.013 | Practically independent |

- **Purchases are the factor most closely tied to revenue.** The relationship is confirmed visually and numerically. Because both variables are likely to measure closely related quantities (frequency vs. monetary value), the analysis treats this as a strong but redundant relationship rather than two independent facts, and flags the need to check whether one variable is derived from the other.
- **Visits alone do not generate revenue.** A considerable group of customers visits the platform frequently and generates zero revenue.
- **There is a commercial activity cluster.** `visitas_mes`, `compras_mes`, `gasto_publicidad_dirigida` and `ingreso_anual` move together to a greater or lesser extent, while `edad`, `nivel_ingreso` and `satisfaccion` show practically no linear relationship with the rest.

## Business implications

- To increase revenue per customer, the most direct lever is **purchase frequency**.
- Rather than investing only in more traffic, the Growth and Retention team should focus on improving the **visit-to-purchase conversion rate**, and investigate why some customers visit without buying, since that could reveal friction in the purchase process.
- For predictive modeling, `compras_mes` and `ingreso_anual` should not be used together, so that the strength of the model is not artificially inflated.

## Repository contents

| File | Description |
|---|---|
| `novaretail_behavior_analysis_EN.ipynb` | Full analysis notebook, with code, documentation and saved outputs (tables and charts) |
| `README.md` | Project description |

## Viewing and reproducing the analysis

The notebook is saved with its outputs, so tables and charts can be read directly on GitHub without running any code.

In the notebook, the data is read from `/datasets/novaretail_comportamiento_clientes_2024.csv`. To re-run the analysis, place the file in a folder of your choice and update that path in the data loading cell. Required libraries: `pandas`, `numpy`, `scipy`, `seaborn` and `matplotlib`.

## Author

**Natalia Sepúlveda** — Data Analyst | Business Intelligence

[LinkedIn](https://www.linkedin.com/in/natalia-sepulveda-escobar) · [GitHub](https://github.com/nataliasepulveda-28)
