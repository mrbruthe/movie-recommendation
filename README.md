# 🎬 Movie Recommendation System

![Python](https://img.shields.io/badge/Python-3.12-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-purple)
![Scikit--Surprise](https://img.shields.io/badge/Scikit--Surprise-Collaborative%20Filtering-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

An end-to-end collaborative filtering recommendation system built on approximately **10 million movie ratings**.

The project progresses from simple statistical baselines to an optimized SVD recommender, followed by full-data retraining and generation of predictions for the unseen test set.

---

## 📌 Project Overview

The objective of this project is to predict how users would rate movies they have not previously rated.

The dataset is highly sparse, with more than **99.8% of possible user–movie interactions unobserved**, making collaborative filtering a natural modelling approach.

The workflow includes:

- data validation and exploratory analysis;
- user and movie behaviour analysis;
- statistical baselines;
- collaborative filtering with SVD;
- controlled hyperparameter optimisation;
- validation-based model selection;
- full-data retraining;
- final test prediction generation.

---

## 📊 Dataset

| Dataset | Rows |
|---|---:|
| Training ratings | 10,000,038 |
| Test interactions | 5,000,019 |
| Unique users | 162,541 |
| Unique movies | 48,213 |

The user–movie interaction matrix has a density of approximately **0.13%**, illustrating the extreme sparsity of the recommendation problem.

---

## 🔍 Exploratory Analysis

The exploratory analysis focused on understanding the structure of the recommendation problem before modelling.

The main observations were:

- ratings range from **0.5 to 5.0**;
- the average rating is approximately **3.53**;
- the median rating is **3.5**;
- the most common rating is **4.0**;
- user activity is highly uneven;
- movie popularity is strongly long-tailed;
- the interaction matrix is approximately **99.87% sparse**.

These characteristics suggest that simple averages alone are insufficient and that the model must learn both systematic rating behaviour and user–movie interaction patterns.

---

## 🎯 Validation Strategy

A fixed **20% holdout validation set** was used throughout model development.

This produced approximately:

- **8 million rows** for model training;
- **2 million rows** for validation.

The same split was maintained across experiments so that model comparisons remained consistent.

Performance was evaluated using **Root Mean Squared Error (RMSE)**, where lower values indicate more accurate rating predictions.

---

## 🧠 Modelling Approach

Three levels of modelling were evaluated.

### 1. Global Mean

The simplest baseline assigns every user–movie pair the average rating observed in the modelling training set.

**Validation RMSE: 1.0609**

This establishes the minimum reference point for the project.

---

### 2. User and Movie Bias Model

A regularised bias model captures systematic differences in user rating behaviour and movie reception.

Some users consistently rate more generously than others, while some movies receive systematically higher or lower ratings.

**Validation RMSE: 0.8655**

This represents a substantial improvement over the global-mean baseline and confirms that user and movie effects explain a large proportion of rating variation.

---

### 3. SVD Collaborative Filtering

SVD represents users and movies through latent factors while also accounting for user and movie biases.

This allows the recommender to capture interaction patterns that cannot be explained by additive effects alone.

The selected SVD configuration achieved:

**Validation RMSE: 0.807368**

---

## ⚙️ Final Model

The selected SVD configuration was:

| Parameter | Value |
|---|---:|
| Latent factors | 190 |
| Epochs | 250 |
| Learning rate | 0.002 |
| Regularization | 0.06 |

The final configuration was selected after controlled hyperparameter optimisation across latent dimensionality, training duration, learning rate, and regularization.

After model selection, the configuration was retrained using the complete **10,000,038-rating training dataset**.

---

## 📈 Results

| Model | RMSE |
|---|---:|
| Global Mean | 1.0609 |
| User + Movie Bias | 0.8655 |
| SVD Collaborative Filtering | **0.807368** |

The final competition submission achieved an RMSE of approximately **0.79**, placing **29th out of 454 participants**.

The progression from **1.0609 → 0.8655 → 0.807368** demonstrates the value gained by moving from simple statistical assumptions to latent-factor collaborative filtering.

---

## 🔄 Project Pipeline

```text
Raw Ratings
    ↓
Data Validation
    ↓
Exploratory Analysis
    ↓
Validation Split
    ↓
Global Mean Baseline
    ↓
User + Movie Bias Model
    ↓
SVD Collaborative Filtering
    ↓
Hyperparameter Optimisation
    ↓
Model Selection
    ↓
Full-Data Retraining
    ↓
Test Predictions
    ↓
Submission
```

---

## 🛠️ Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Scikit-Surprise
- Matplotlib
- Jupyter Notebook

---

## 📂 Repository Structure

```text
movie-recommendation/
│
├── movie-recommendation.ipynb
├── README.md
├── requirements.txt
├── .gitignore
│
└── artifacts/
    └── svd_tuning/
        └── best_svd_config.json
        └── svd_tuning_results.csv
```

---

## 💡 Key Takeaways

This project demonstrates a complete recommendation-system workflow, progressing from statistical baselines to latent-factor collaborative filtering on approximately **10 million ratings**.

Key lessons from the project include:

- establishing strong baselines before introducing more complex models;
- maintaining a fixed validation strategy for reliable model comparison;
- tuning interacting hyperparameters systematically rather than independently;
- separating model selection from final full-data training;
- preserving the selected configuration for reproducibility;
- using full-data retraining only after model selection is complete.

---

## 🚀 Future Improvements

The current system uses standard SVD collaborative filtering.

Potential extensions include:

- SVD++;
- implicit-feedback modelling;
- richer movie metadata;
- hybrid recommendation systems;
- neural collaborative filtering;
- ranking-oriented evaluation metrics;
- additional contextual and interaction features.

---

## 👤 Author

**Perseverance Ebah**

Data Scientist · Machine Learning Engineer · Data Engineer
