# Concrete Compressive Strength Prediction using Machine Learning & Explainable AI

## 📌 Project Overview
This project focuses on predicting the **compressive strength of concrete** using various **machine learning and deep learning models**.  
The goal is to identify the **best-performing model** for this tabular regression problem and to **explain the final model’s behavior** using Explainable AI (XAI) techniques.

The dataset consists of concrete mix design parameters such as cement, water, aggregates, and curing age, and the target is concrete compressive strength.

---

## 📊 Dataset Description
- **Samples:** ~1,030
- **Features (Inputs):**
  - Cement
  - Blast Furnace Slag
  - Fly Ash
  - Water
  - Superplasticizer
  - Coarse Aggregate
  - Fine Aggregate
  - Age
- **Target:**
  - Concrete Compressive Strength

This is a **supervised regression problem** on **tabular numeric data**.

---

## 🧭 Project Workflow (Step-by-Step)

### 1️⃣ Data Understanding & Cleaning
- Loaded the dataset and checked:
  - Missing values
  - Data types
  - Duplicates
  - Outliers
- Verified that all features are numeric and suitable for regression.

---

### 2️⃣ Feature Engineering
To improve model performance, additional domain-informed features were created:
- `binder = cement + slag + fly_ash`
- `water_binder_ratio = water / binder`
- `total_aggregate = coarse + fine`
- Fraction-based features (cement fraction, slag fraction, etc.)
- Age transformations (log, sqrt)

These features significantly improved boosting-based models.

---

### 3️⃣ Train / Validation / Test Split
A **time-aware split** was used based on the `age` feature:
- **Train:** Oldest 80%
- **Validation:** Next 10%
- **Test:** Most recent 10%

This simulates a real-world scenario and avoids data leakage.

---

### 4️⃣ Models Implemented
I experimented with a wide range of models, from simple to advanced:

#### 🔹 Traditional & Ensemble Models
- Random Forest
- Gradient Boosting
- XGBoost
- CatBoost
- LightGBM
- Ensemble (XGBoost + CatBoost + LightGBM)

#### 🔹 Deep Learning Models
- MLP (PyTorch)
- FT-Transformer
- TabNet
- NODE (Neural Oblivious Decision Ensembles)

All models were trained using the same data split for fair comparison.

---

## 📈 Model Comparison (Test Set Performance)

| Model | MAE ↓ | RMSE ↓ | R² ↑ | Performance |
|-----|-----|-----|-----|-----|
| **LightGBM** | **4.03** | **4.87** | **0.764** | 🥇 Best |
| Ensemble (XGB + CAT + LGB) | 3.98 | 4.97 | 0.755 | 🥈 |
| XGBoost | ~4.03 | ~4.97 | ~0.75 | 🥉 |
| Gradient Boosting | 4.34 | 5.14 | 0.74 | Good |
| CatBoost | 4.69 | 5.61 | 0.69 | Average |
| Random Forest | 5.53 | 7.21 | 0.48 | Weak |
| Deep Learning (MLP) | 5.66 | 7.73 | 0.41 | Poor |
| FT-Transformer | 7.86 | 10.23 | -0.04 | ❌ |
| TabNet | 17.43 | 20.82 | -3.31 | ❌ |
| NODE | Very unstable | Very poor | ❌ | ❌ |

---

## 🏆 Final Model Selection
### ✅ **LightGBM is the Best Model**

**Reasons:**
- Lowest RMSE (most important regression metric)
- Highest R² (best generalization)
- Stable across train, validation, and test sets
- Handles tabular data and nonlinear relationships very effectively

Although the ensemble slightly reduced MAE, LightGBM handled **large errors better**, making it the final choice.

---

## ❌ Why Deep Learning Models Failed
Despite trying advanced tabular deep learning models (FT-Transformer, TabNet, NODE):

- Dataset size is relatively small (~1k samples)
- Data is purely numeric and tabular
- Time-based split caused distribution shift
- Deep learning models overfit and failed to generalize

This confirms a well-known ML principle:
> **For small-to-medium tabular datasets, gradient boosting models outperform deep learning.**

---

## 🔍 Explainable AI (XAI)
To understand **how the final LightGBM model works**, I applied **three different Explainable AI techniques**:

### 1️⃣ SHAP (SHapley Additive Explanations)
- Global feature importance
- Local explanations for individual predictions
- Shows how each feature increases or decreases predictions

### 2️⃣ LIME (Local Interpretable Model-agnostic Explanations)
- Local, rule-based explanations
- Explains one prediction at a time
- Human-readable feature contributions

### 3️⃣ Partial Dependence & ICE Plots
- Visualizes how predictions change with feature values
- Shows both global trends (PDP) and individual behavior (ICE)

These XAI methods provided strong confidence and transparency in the LightGBM model.

---
# Concrete Compressive Strength Prediction using LightGBM & Explainable AI

🚀 **Live Demo (Streamlit App):**  
👉 https://concrete-compressive-strength-lightgbm.streamlit.app/

---

## 📌 Project Overview
This project predicts the **compressive strength of concrete** using machine learning techniques based on concrete mix design parameters and curing age.

The objective was not only to build an accurate predictive model, but also to:
- Compare multiple ML and Deep Learning models
- Select the best-performing model based on test performance
- Apply **Explainable AI (XAI)** techniques to understand how the final model makes predictions
- Deploy the solution using **Streamlit** for easy interaction and visualization

## 🏆 Final Model Selection
### ✅ **LightGBM was selected as the final model**

**Reasons:**
- Lowest RMSE (best generalization)
- Highest R² on unseen test data
- Stable and robust on tabular numeric data
- Handles nonlinear feature interactions effectively

Although the ensemble slightly reduced MAE, LightGBM handled large errors better and was therefore chosen as the final model.

---

## 🔍 Explainable AI (XAI)
To interpret the LightGBM model, **three Explainable AI techniques** were applied:

### 1️⃣ SHAP (SHapley Additive Explanations)
- Global feature importance
- Local explanation for individual predictions
- Shows how each feature pushes predictions up or down

### 2️⃣ LIME (Local Interpretable Model-Agnostic Explanations)
- Rule-based local explanations
- Human-readable feature contribution ranges
- Explains one prediction at a time

### 3️⃣ Partial Dependence & ICE Plots
- Visualizes how predictions change with feature values
- Shows both global trends (PDP) and individual behavior (ICE)

These techniques improve trust and transparency in the final model.

---

## 🌐 Streamlit Web Application
The project is deployed using **Streamlit**, allowing users to:

- Enter concrete mix parameters interactively
- Predict compressive strength in real time
- Upload CSV files for batch prediction
- Explore Explainable AI visualizations (SHAP, LIME, PDP/ICE)

🔗 **Live App:**  
https://concrete-compressive-strength-lightgbm.streamlit.app/




## 📌 Conclusion
- Multiple ML and DL models were explored extensively.
- **LightGBM achieved the best overall performance**.
- Advanced deep learning models did not generalize well due to dataset characteristics.
- Explainable AI techniques were successfully used to interpret the final model.

This project demonstrates a **complete end-to-end machine learning workflow**, from data preprocessing and modeling to evaluation and explainability.

---

## 🚀 Future Work
- Hyperparameter optimization using Bayesian search
- Weighted ensemble based on validation scores
- Deployment as a web application
- Predictive uncertainty estimation

---

## 🧠 Key Takeaway
> **More complex models are not always better. Choosing the right model for the data matters more than model complexity.**
