# 🚲 Bike Sharing Demand Prediction

## 📌 Overview
This project aims to predict the number of bike rentals (`count`) based on environmental and temporal features.  
The evaluation metric used is **Root Mean Squared Logarithmic Error (RMSLE)**.

---

## 📂 Dataset
The dataset contains the following features:
- `datetime`
- `season`
- `holiday`
- `workingday`
- `weather`
- `temp`, `atemp`
- `humidity`
- `windspeed`
- `casual`, `registered` (used only in training, removed to avoid leakage)
- `count` (target variable)

---

## ⚙️ Data Preprocessing

### 🔹 Datetime Processing
- Converted `datetime` to pandas datetime format
- Extracted:
  - `hour`
  - `day_of_week`

### 🔹 Dropped Columns
- `datetime` (after feature extraction)
- `casual`, `registered` → to prevent data leakage
- `atemp` → highly correlated with `temp`

---

## 🧠 Feature Engineering

### ⏱ Time-Based Features
- `hour`
- `day_of_week`
- `is_weekend`
- `is_rush_hour`

### 🔄 Cyclical Encoding
- `hour_sin`
- `hour_cos`

### 🔗 Interaction Features
- `working_hour = workingday × hour`
- `temp_humidity = temp × humidity`

### 🏷 Categorical Encoding
- One-hot encoding for:
  - `season`
  - `weather`

---

## 🚨 Outlier Handling
- Used IQR method to detect outliers
- Decision:
  - Kept most outliers → represent real-world demand spikes
  - Applied capping only when necessary

---

## 🤖 Models

### 1️⃣ Linear Regression
- Applied `log1p` transformation on target
- Used `StandardScaler`
- Baseline model

**Performance:**
- RMSLE ≈ **0.78**

---

### 2️⃣ Random Forest
- No scaling required
- Captures non-linear relationships
- Improved performance over linear regression

---

### 3️⃣ XGBoost
- Gradient boosting model
- Handles complex interactions
- Best performing model

**Expected RMSLE:**
- ~ **0.5 – 0.6**

---

## 📊 Model Evaluation

Metrics used:
- **RMSLE (primary metric)**
- MSE
- MAE
- R²

Validation:
- **5-Fold Cross Validation**
- Ensures model stability and reliability

---

## 🏁 Final Training
- Retrained models on **full training dataset**
- Applied same preprocessing pipeline to test data
- Ensured feature alignment between train and test sets

---

## 📤 Submission

Generated submission file:
submission_1
submission_2

for testing our work 


Steps:
1. Apply feature engineering on test data
2. Align columns with training data
3. Predict using trained model
4. Save as `.csv`
5. Upload to Kaggle

---

## 📈 Results

| Model              | RMSLE |
|------------------|------|
| Linear Regression | ~0.79 |
| Random Forest     | 0.47|


---

## 📚 Key Learnings

- Feature engineering > model choice
- Time-based features are critical
- Log transformation improves regression performance
- Cross-validation ensures reliability
- Tree-based models outperform linear models for this task

---

## 🚀 Future Improvements

- Hyperparameter tuning (GridSearch, Optuna)
- Use LightGBM / advanced boosting models
- Feature importance analysis
- Model ensembling

---

## 📌 Conclusion

This project demonstrates a complete machine learning workflow:

- Data preprocessing  
- Feature engineering  
- Model training  
- Evaluation  
- Kaggle submission  

---

## 👤 Author
Rashed Moukattash
