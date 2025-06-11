
---

# 📘 **II. Methodology — Steps in the Knowledge Discovery in Databases (KDD) Process**

---

## **1️⃣ Selection (Data Collection)**

### 🔹 Identify and select relevant data sources

* Selected dataset from **Kaggle: Bangladesh Student Performance EDA**
* Data originated from academic records and student/parent surveys.

### 🔹 Define the variables of interest

* **Dependent Variables:**

  * Subject Scores: English, Math, Science, Social Science, Art & Culture.
  * Derived Target: Performance Category (Low, Average, High).

* **Independent Variables:**

  * Socioeconomic: Parental education, parental job, family size, location.
  * Educational Inputs: Studytime, school type, internet access, tutoring, attendance, extracurricular activities.
  * Demographic: Gender, Guardian.

### 🔹 Extract data from databases, surveys, or other sources

* Data extracted directly from Kaggle platform (public repository).
* CSV file format, structured tabular data.

---

## **2️⃣ Preprocessing (Data Cleaning)**

### 🔹 Handle missing values using imputation techniques

* One missing value found in `location` column.
* Imputed using **mode imputation** ("Urban") based on frequency.

### 🔹 Identify and remove duplicate or inconsistent records

* Verified no duplicates in dataset.
* Categorical inconsistencies manually corrected:

  * Unified case formatting (e.g. `urban` → `Urban`).
  * Merged redundant categories (`Hons` → `Honors`, `None` → `Non_Educated`).

### 🔹 Detect and treat outliers to improve data quality

* Applied **Interquartile Range (IQR)** method (1.5×IQR rule) to numeric fields.
* Outliers in subject scores and attendance retained (to preserve academic variability).
* Age filtered: kept students aged **13 to 20 years**.

  * 3 records outside valid age range were removed.

### 🔹 Normalize or standardize data if necessary

* No normalization applied.
* Decision Trees and Random Forests are scale-invariant models, so standardization was not required.

---

## **3️⃣ Transformation (Feature Engineering)**

### 🔹 Convert raw data into a suitable format for analysis

* Structured tabular dataset prepared after cleaning.
* Manual corrections applied to labels.
* Converted categorical variables into consistent, valid categories.

### 🔹 Apply dimensionality reduction techniques if needed

* Dimensionality reduction not applied.
* Final feature space was manageable after encoding.

### 🔹 Encode categorical variables into numerical representations

* Applied **One-Hot Encoding** to 13 categorical features:

  * Gender, Location, Parental Education & Jobs, Guardian, Parental Involvement, Internet Access, Tutoring, School Type, Extracurricular Activities, Academic Group (stu\_group).

### 🔹 Generate new derived variables that enhance analysis

* Created `Total_Score` as sum of 5 subject scores.
* Created `Performance_Category` using 20th and 80th percentile cutoffs to define Low, Average, and High categories (Siemens & Baker, 2012).

  * This balanced class sizes to improve classification stability.

---

## **4️⃣ Data Mining (Pattern Extraction)**

### 🔹 Apply statistical or machine learning techniques to extract patterns

* Applied three classification models:

  * ✅ Decision Tree (primary model, highly interpretable)
  * ✅ Random Forest (ensemble method)
  * ✅ Support Vector Machine (non-linear classifier)

### 🔹 Use clustering, classification, or regression models to analyze relationships

* Used **classification models**.
* No clustering or regression applied as the problem was categorical prediction.

### 🔹 Identify trends, correlations, or predictive insights

* Extracted important predictors:

  * Academic Group (Commerce, Science)
  * Studytime
  * Attendance
  * Extracurricular participation
  * Parental Involvement
  * Guardian type

* Model performances:

| Model                        | Accuracy  |
| ---------------------------- | --------- |
| Decision Tree                | **77.7%** |
| Random Forest                | 77.6%     |
| Support Vector Machine (SVM) | 66.3%     |

* Decision Tree chosen as primary model due to:

  * Highest interpretability.
  * Comparable or better performance.

---

## **5️⃣ Interpretation & Evaluation (Knowledge Discovery)**

### 🔹 Assess the results and validate findings

* All models validated on hold-out test set (20% split).
* Decision Tree provided best trade-off between accuracy and interpretability.
* Strong alignment with prior educational research (OECD, 2019; Romero & Ventura, 2010; Sirin, 2005).

### 🔹 Interpret meaningful patterns from the data

* Academic track and study time dominate performance outcomes.
* Studytime ≥ 6 hours/day is strongly associated with high performance.
* Commerce students are at risk under low studytime and attendance.
* Extra-curricular activities and parental involvement provide additional benefits.

### 🔹 Compare findings with existing research or domain knowledge

* Findings align well with established education literature:

  * SES effects are smaller than school-based interventions.
  * Academic engagement (studytime, attendance) remains critical.
  * Parental involvement has moderate positive effects.


---


