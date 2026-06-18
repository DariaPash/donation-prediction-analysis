# Donation Forecast Modeling
This project implements a complete data analysis pipeline for predicting donation amounts (`TargetD`) based on donor demographic and behavioral features. The work is self‑contained and follows a structured model selection process.

## Pipeline Overview

1. **Data Preprocessing**
   - KNN imputation (k=5) with missing indicators
   - One‑hot encoding of categorical variables
   - Log‑transformation (`log1p`) for skewed non‑negative numeric features

2. **Feature Selection**
   - Backward stepwise OLS using p‑values
   - Optimal subset chosen by 5‑fold cross‑validated MSE

3. **Linear Model Assessment**
   - Bootstrap resampling (100 iterations, 25% sample size)
   - Estimation of intercept distribution and OOB (out‑of‑bag) MSE
   - Visualization of bootstrap confidence intervals

4. **Non‑linear Modeling (MLP)**
   - Single hidden layer with ReLU activation
   - Hyperparameter tuning via `HalvingGridSearchCV`
   - Grid search over number of neurons and regularization strength (`alpha`)

5. **Model Comparison**
   - Train, CV, OOB and holdout MSE reported for both models
   - MLP achieves ~15–24% lower error than the linear baseline

## Results Summary

| Model        | Train MSE | CV MSE | OOB MSE (mean) | OOB MSE 95% CI        | Holdout MSE | Train–Holdout Δ |
|--------------|-----------|--------|----------------|-----------------------|-------------|-----------------|
| Backward OLS | 84.41     | 85.31  | 88.31          | [76.27, 97.65]        | 79.80       | 4.61            |
| MLP (ReLU)   | 63.70     | 70.50  | 77.95          | [65.59, 93.18]        | 67.59       | 3.89            |

**Best performer:** MLP with 1 hidden layer (8 neurons, alpha=0.1).
## Russian version
# Прогнозирование суммы пожертвований

Проект содержит полный цикл анализа данных для прогнозирования суммы пожертвований (`TargetD`) на основе признаков доноров.

## Основные этапы

- Предобработка: KNN-импутация (k=5), one-hot-кодирование, логарифмическое преобразование.
- Отбор признаков: пошаговый Backward OLS с выбором лучшей сложности по 5-блочной CV-MSE.
- Оценка линейной модели: бутстреп (100 выборок по 25%) для оценки неопределённости константы и OOB-MSE.
- Нелинейная модель: MLP с ReLU, подбор гиперпараметров (число нейронов, alpha) через HalvingGridSearchCV.
- Сравнение моделей по train, CV, OOB и holdout ошибкам.

## Результаты

| Модель        | Train MSE | CV MSE | OOB MSE (средн.) | OOB MSE 95% ДИ      | Holdout MSE | Train–Holdout Δ |
|---------------|-----------|--------|------------------|---------------------|-------------|-----------------|
| Backward OLS  | 84.41     | 85.31  | 88.31            | [76.27, 97.65]      | 79.80       | 4.61            |
| MLP (ReLU)    | 63.70     | 70.50  | 77.95            | [65.59, 93.18]      | 67.59       | 3.89            |

**Лучшая модель:** MLP с 1 скрытым слоем (8 нейронов, alpha=0.1).

