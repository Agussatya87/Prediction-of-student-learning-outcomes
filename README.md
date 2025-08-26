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

### Exploratory Data Analysis (EDA)
The Exploratory Data Analysis (EDA) stage aims to understand patterns within the data before proceeding to the modeling process. EDA helps identify the characteristics of the dataset, data distribution, detect anomalies or inconsistencies, and examine the relationships between variables. The data distribution was visualized using the Plotly Express library. The following shows the distribution results:

<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/874087ba-7370-46ce-8338-6a5966c8ede4" />

The data distribution based on the Predikat (grades) is presented in the form of a donut chart, illustrating the proportion of each Predikat category within the entire dataset, which consists of 278 records. From this distribution, it can be concluded that the majority of students received grades B and C, while only a few attained grade A. Next, the distribution of Predikat across selected subjects is presented. The analysis of grade distribution in these subjects can serve as one of the steps in the decision-making process. The following shows the Predikat (grades) distribution for several subjects:

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/5439a77a-0088-4b11-9dc3-74ac232cc50d" />

Based on the bar chart visualization above, it is evident that there are significant differences in the distribution of student grades across several subjects. In Mathematics, the number of students receiving grade C is the most dominant compared to other grades, indicating that many students face difficulties in this subject. Meanwhile, in Indonesian Language, the grade distribution is relatively more balanced, with the number of students receiving grades B and C being almost equal, although still far from the number of students achieving grade A. In Financial Accounting, the grade distribution is fairly even, although students with grade B are more dominant compared to grades A and C. After performing the data distribution, the next step is to examine the correlation between numerical variables to understand the relationships among features and how these features may influence the target variable. For this analysis, Spearman correlation is used, which is a rank-based correlation method. The following heatmap illustrates the correlation check using the Spearman method:

<img width="603" height="518" alt="image" src="https://github.com/user-attachments/assets/8d71b896-be56-4476-9828-d6ad73575123" />

From this correlation analysis, it can be concluded that the variables with a strong correlation to the target variable (Predikat) are Daily Scores (Nilai Harian), Midterm Scores (Nilai UTS), Final Exam Scores (Nilai UAS), Skills (Keterampilan), Knowledge (Pengetahuan), and Final Scores (Nilai Akhir). These score-related variables show a strong positive correlation with Predikat_Encoded, indicated by the increasingly red color approaching 1. Additionally, the negative correlation observed in Absensi (attendance) suggests that student attendance affects grades, although not very strongly. The features Nilai Harian, Nilai UTS, Nilai UAS, Keterampilan, and Pengetahuan also show high inter-correlations, indicating that students who score high in one variable tend to score high in the others as well. Despite the relatively low correlation value, the negative correlation between Absensi and Predikat still has an impact on the grades. Next, an analysis was conducted to examine the relationship between the Extracurricular variable and the target variable Predikat (grades) using the Chi-square test and Cramér's V. The Chi-square test is used to determine whether there is an association between two categorical variables. The general formula for the Chi-square test is as follows:

![Rumus Chi-Square](https://latex.codecogs.com/png.latex?\dpi{150}\bg{transparent}\color{white}X%5E2%3D%5Csum%20%5Cfrac%7B%28O-E%29%5E2%7D%7BE%7D)

Based on the calculation results, the following values were obtained: Chi-Square Score: 56.4151 and P-Value: 0.0000. The Chi-square test results show a p-value of 0.0000, which is far below the significance level of 0.05. This finding indicates that there is a significant relationship between extracurricular activities and students' academic grades. The Chi-square test indicates a relationship between the categorical variables Ekstrakurikuler and Predikat, but this method cannot measure the strength of the association between the variables. Therefore, to assess the strength of this relationship, Cramér's V is used, which is an association measure for categorical variables based on the Chi-square statistic. The formula for Cramér's V is as follows: 

![Rumus V](https://latex.codecogs.com/png.latex?\dpi{150}\bg{transparent}\color{white}V%3D%5Csqrt%7B%5Cfrac%7BX%5E2%7D%7Bn%20%5Ctimes%20%5Cmin%28k-1%2Cr-1%29%7D%7D)

Interpretasi umum untuk nilai Cramér’s V:
- 0,00 – 0,10: Hubungan sangat lemah atau tidak ada hubungan.
- 0,10 – 0,30: Hubungan lemah.
- 0,30 – 0,50: Hubungan sedang.
- '> 0,50': Hubungan kuat atau sempurna.

Based on the calculation results, a Cramér's V value of 0.3022 was obtained. This value indicates a moderate strength of association between Ekstrakurikuler and Predikat. From this result, it can be concluded that the type of extracurricular activities students participate in has a significant relationship with their academic grades, although the strength of this association is not very strong.

### Pre-Processing Data
The data pre-processing process in this study includes feature selection, handling missing values, feature encoding, outlier handling, data normalization, dataset splitting, and addressing class imbalance in Predikat. The following illustrates the workflow of these data pre-processing steps:

<img width="359" height="836" alt="image" src="https://github.com/user-attachments/assets/2069f690-dafb-4d9f-86b2-7a121f4bfc0c" />

The following flowchart illustrates the stages of data pre-processing before modeling. The process begins with feature selection, which involves choosing relevant features. Next, missing values are checked. If any missing data is found, handling missing values is performed using imputation methods or by removing incomplete records.

Subsequently, categorical data is transformed into numerical form through feature encoding, where the Predikat column uses ordinal encoding, and the Ekstrakurikuler column uses label encoding. After data transformation, outlier handling is carried out to address values that deviate significantly from the mean, which could affect model performance.

The data is then normalized through feature scaling to ensure uniformity across all features. Next, the dataset is split into 70% training data and 30% testing data. To address class imbalance in the training data, handling imbalance is performed using the SMOTE method, ensuring a more balanced class distribution.

### SVM Modelling & Evaluation
The SVM implementation was carried out using Support Vector Classification (SVC) from scikit-learn, configured with One-vs-Rest (OvR) to handle multiclass classification. In this stage, the modeling process is divided into two parts: modeling without hyperparameter tuning and modeling with hyperparameter tuning. The accuracy calculation results show that the model without hyperparameter tuning achieved an accuracy of 93%. The accuracy calculation for the model with hyperparameter tuning shows an accuracy of 95%, indicating a 2% improvement over the model without tuning. This high accuracy level demonstrates that the model can make predictions effectively, even after tuning.

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

## 🙋‍♂️ Author

**Agus Satya**  
📍 Denpasar, Indonesia  
📧 agussatya878@gmail.com  

---
