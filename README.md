# 🎓 Prediction of Student Learning Outcomes using SVM

This project aims to predict the **learning outcomes of vocational high school students** using **Support Vector Machine (SVM)**. The model leverages academic performance data, attendance, and extracurricular involvement to classify students into different performance categories (A, B, C).

---

## 📌 Project Overview

- **Objective**: To develop a machine learning model that can predict student performance based on historical academic records.
- **Method**: Support Vector Machine (SVM) classification.
- **Use case**: Assists educators in identifying students at risk and tailoring interventions accordingly.

---

## 📊 Dataset

The dataset is derived from student academic records from **SMK TP 45 Denpasar**, consisting of:

- **Features**:
  - Absensi (Attendance)
  - Nilai Harian, UTS, UAS, Keterampilan
  - Nilai Akhir
  - Jenis Kelamin, Kelas, Semester
  - Ekstrakurikuler (Paduan Suara, Pramuka, Tari, dll.)

- **Target Variable**: `Predikat` (A, B, C)

---

## 🔍 Workflow Summary

1. **Data Collection**  
   - Import data from Excel.
   - Combine two datasets: subject-wise scores and final student summary.

2. **Exploratory Data Analysis (EDA)**  
   - Descriptive statistics.
   - Visual distribution by subjects and semester.
   - Correlation analysis using Cramér's V.
   - Outlier detection.

3. **Preprocessing**  
   - Handling missing values (on Absensi and Keterampilan).
   - Feature selection and encoding (`Ekstrakurikuler` and `Predikat`).
   - Feature scaling using MinMaxScaler.
   - Train-test split (70:30).
   - Handling imbalanced data using **SMOTE**.

4. **Modeling**  
   - Training SVM classifier.
   - Hyperparameter tuning using GridSearchCV.
   - Evaluation using confusion matrix, classification report, and accuracy score.

5. **Result**  
  - Accuracy without tuning: 93%
  - Accuracy after tuning: 95%
  - Applying SMOTE helped balance class distribution, improving the model’s ability to generalize.
  - Hyperparameter tuning using GridSearchCV (best parameters: C=100, gamma=scale, kernel='linear') significantly improved model performance.
---

## 📈 Key Technologies Used

| Tool / Library       | Function                         |
|----------------------|----------------------------------|
| `pandas`             | Data loading & manipulation      |
| `matplotlib`, `seaborn` | Data visualization           |
| `scikit-learn`       | Modeling, preprocessing, evaluation |
| `imblearn` (SMOTE)   | Handling class imbalance         |

---

## 🧪 Evaluation Metrics

- **Accuracy**
- **Confusion Matrix**
- **Classification Report** (Precision, Recall, F1-score)

---


---

## 🚀 How to Run This Project

> This project is implemented using Google Colab.  
> Simply open the `.ipynb` file using the button below:

[🔗 Open in Google Colab](https://colab.research.google.com/drive/1f-ttiLGIwW5U5soIUx6jeVPbop-DJV6g)

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, modify, and distribute with attribution.

---

## 🙋‍♂️ Author

**Agus Satya**  
📍 Denpasar, Indonesia  
📧 agussatya878@gmail.com  
🔗 [GitHub](https://github.com/Agussatya87)

---
