
# 📘 Methodology and Results (Full KDD-Based Analysis) Version 2

This README outlines the full KDD-based workflow, model results, interpretations, and challenges encountered while analyzing student performance using J48 and Apriori models in WEKA.

---

## 🔧 Tools Used
- Microsoft Excel (data cleaning, encoding)
- WEKA v3.8.6 (J48 decision tree and Apriori rule mining)
- WebGraphviz (for decision tree visualization)

---

## 🔄 KDD Process Steps

### 📊 Exploratory Data Analysis (EDA)
- **Average study time**: 2.1 hrs/day  
- **Average attendance**: 87%  
- **Group distribution**: Science (48%), Commerce (32%), Arts (20%)  
- **Key finding**: Correlation between study time and performance: r = 0.52  
- **Suggested visuals**: Attendance histogram, performance by group bar chart, correlation matrix

---

### 1. Selection (Data Collection)
Dataset: `bd_students_per.csv` (Kaggle)  
- 24 attributes including demographics, education, and behavioral indicators  
- Cleaned to 22 attributes and 8296 rows

---

### 2. Preprocessing (Data Cleaning)
- Removed: `id`, `full_name`  
- Fixed: duplicates, missing values, capitalization issues (e.g., `city`, `urban` → `City`, `Urban`)  
- Summary: 316 rows removed, 2 columns dropped

---

### 3. Transformation (Feature Engineering)
- Added `overall_avg_score` (average of 5 subjects)  
- Created `performance_category` using:  
```excel
=IF(score<=69.4, "Low", IF(score<=80.2, "Medium", "High"))
```
- Used `PERCENTILE.INC` for percentile cutoffs (fair binning)

---

### 4. Data Mining (Pattern Extraction)
- J48: 96.08% accuracy  
- Apriori: strong rules (≥ 90% confidence)  
- Used Discretize filter for numeric values (3 bins)  
- Example rules:  
  - `stu_group = Arts ∧ studytime = Low` → `performance = Low`  
  - `stu_group = Science ∧ studytime = High` → `performance = High`

---

### 5. Interpretation & Evaluation
- Top predictors: `stu_group`, `studytime`, `attendance`  
- Patterns match real-world expectations  
- Useful for school intervention and advising  
- Visualized using WebGraphviz

---

### 6. Model Comparison
| Model   | Purpose        | Strength             | Limitation             |
|---------|----------------|----------------------|-------------------------|
| J48     | Classification | Interpretable, clear | May overfit w/o pruning |
| Apriori | Pattern mining | Rule co-occurrences  | Not predictive          |

---

### 7. Limitations
- One academic year only  
- Self-reported bias (study time)  
- Limited geographic coverage (Bangladesh)  
- No income data or socioeconomic index

---

### ✅ Conclusion
- Achieved strong model accuracy and rule strength  
- Clear patterns found between study behavior and group performance  
- Framework is repeatable, educationally actionable
