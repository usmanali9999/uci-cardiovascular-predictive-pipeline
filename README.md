# Multi-Center UCI Cardiovascular Data Mining Pipeline


An advanced data mining and predictive analytics framework engineered on the multi-center 920-row UCI Heart Disease dataset. This project systematically extracts structural insights from combined clinical cohorts, optimizing multi-class prediction mechanics while addressing the data missingness, anomalies, and imbalances inherent in cross-institutional medical registries.

---

## 📊 Project Core & Mining Objectives
Clinical data collections across distinct geographical institutions often suffer from high structural variance, severe missingness, and statistical noise. This project processes multi-center observations to uncover deep physiological patterns and accurately classify the severity of coronary artery disease. 

The primary mining objective centers on engineering a reliable pathway from raw, highly incomplete clinical inputs to an optimized, mathematically sound model workspace.

---

## 📋 Biometric Feature Dictionary & Parameter Schema

The dataset consists of 14 core clinical attributes alongside metadata tracking, categorized below by their biological and diagnostic properties:

### Metadata & Demographics
* **`id` (Patient Identifier):** A unique, sequential integer assigned to index individual patient records within the consolidated database.
* **`age` (Chronological Age):** The patient's age quantified in years, serving as a primary non-modifiable risk baseline for cardiovascular degeneration.
* **`sex` (Biological Sex):** Binary categorization of the patient's biological sex (Male or Female), critical for assessing demographic risk variances.
* **`dataset` (Clinical Center Origin):** Identifies the specific institutional origin of the clinical record (e.g., Cleveland, Hungary, Switzerland, or VA Long Beach).

### Symptomatic & Baseline Biometrics
* **`cp` (Chest Pain Type):** Categorized clinical manifestation of angina, classified into four tiers: typical angina, atypical angina, non-anginal pain, or asymptomatic.
* **`trestbps` (Resting Blood Pressure):** The patient's resting systolic blood pressure measured in mm Hg upon initial hospital admission.
* **`chol` (Serum Cholesterol):** Total serum cholesterol concentration quantified in mg/dl, representing a critical metabolic lipid marker.
* **`fbs` (Fasting Blood Sugar):** A logical boolean flag indicating whether the patient's fasting blood sugar exceeds a diabetic threshold of 120 mg/dl.

### Cardiovascular Metrics & Stress Responses
* **`restecg` (Resting Electrocardiographic Results):** Captures baseline electrical cardiac activity, noting normal patterns, ST-T wave abnormalities, or left ventricular hypertrophy.
* **`thalch` (Maximum Heart Rate Achieved):** The peak heart rate achieved by the patient during a standardized stress-testing regimen.
* **`exang` (Exercise-Induced Angina):** A boolean metric logging whether physical exertion directly triggers localized ischemic chest pain.
* **`oldpeak` (ST Depression):** Quantifiable ST-segment depression induced by exercise relative to rest, measuring myocardial oxygen supply stress.
* **`slope` (Peak Exercise ST Segment Slope):** The geometric slope of the peak exercise ST segment, coded as upsloping, flat, or downsloping.

### Specialized Advanced Diagnostics
* **`ca` (Number of Major Vessels):** The total count (0–3) of major coronary arteries visualized and colored via fluoroscopy imaging.
* **`thal` (Thalassemia Scintigraphy):** A nuclear medicine imaging marker reflecting myocardial blood flow, categorized as normal, fixed defect, or reversible defect.

### Predictive Mining Target
* **`num` (Angiographic Disease Status):** The target variable tracking coronary artery narrowing, where `0` indicates no disease (<50% narrowing) and `1, 2, 3, 4` indicate progressive stages of disease configuration (>50% narrowing).

---

## 🛠️ Critical Data Anomalies & Analytical Hurdles

### 1. High-Density Structural Missingness
A primary characteristic of this dataset is the significant data dropouts observed in specialized clinical procedures. While foundational demographic attributes like patient age and biological sex are complete, deep diagnostic variables show extreme missingness thresholds:
* **Fluoroscopy Markers (`ca`):** Exhibits over 66% missing values (~611 unrecorded patient profiles), demanding robust handling beyond trivial statistical drops.
* **Scintigraphy Results (`thal`):** Lacks records for over 52% of the cohort (~486 missing entries).
* **Exercise Metrics (`slope`):** Missing structural slope data for more than 33% of observations (~309 empty profiles).

### 2. Physiological Invalidation & Outliers
Statistical data profiling exposes clear data-entry artifacts and biological anomalies that require precise truncation or transform frameworks:
* **Zero-Value Anomalies:** Essential continuous metrics like resting blood pressure (`trestbps`) and serum cholesterol (`chol`) exhibit absolute values of `0.0`, which are physiologically impossible for living subjects.
* **Extreme Tail Skewness:** Serum cholesterol measurements contain massive right-tail outliers reaching as high as `603.0 mg/dl`, introducing substantial distribution skewness.

### 3. Multi-Tiered Target Imbalance
The diagnostic target vector (`num`) is structured across a 5-tier classification hierarchy reflecting the progression of coronary narrowing:
* **Class `0`:** No diagnostic evidence of cardiovascular disease (Baseline control group).
* **Classes `1, 2, 3, 4`:** Escalating stages of localized vessel narrowing.

The distribution drops sharply across the advanced severity tiers. This requires robust stratification strategies to maintain representative subsets across training and evaluation phases.

---

## 🔍 Data Mining Discoveries & Graphical Insights

Analyzing the distributions, spreads, and interactions across your exploratory plots and notebooks reveals distinct clinical patterns directly extracted from your graphics:

### 1. Structural Insight from Histograms
* **Bimodal Cholesterol Drops:** The `chol` histogram shows a massive spike exactly at `0.0`. This visually confirms that missing data was masked as zero entries, contrasting with the true biological patient distribution which peaks normally around `220-250 mg/dl`.
* **The Aging Bell Curve:** The `age` histogram displays a smooth, near-Gaussian distribution centered heavily between 50 and 65 years old, indicating the dataset primarily captures a mature demographic group.
* **Truncated Heart Rate Thresholds:** The `thalch` (Maximum Heart Rate) histogram shows a clean left-skewed distribution. The curve drops sharply after 160 bpm, illustrating lower heart rate tolerances across high-risk cohorts.

### 2. Variance & Outlier Insights from Boxplots
* **Massive Cholesterol Tail:** The `chol` boxplot isolates a cluster of data points stretching far beyond the upper whisker, reaching all the way to `603.0 mg/dl`. This visually identifies extreme high-risk hypercholesterolemia profiles in specific individuals.
* **ST Depression Compression:** The `oldpeak` boxplot demonstrates that the vast majority of patients rest tightly between `0.0` and `1.5` mm of ST depression. However, severe stress-test indicators break away completely as outliers, extending upwards to a critical `6.2` mm.
* **Blood Pressure Variance:** The `trestbps` boxplot exhibits tight clustering around a median of `130 mm Hg`, but highlights several hypertensive extreme outliers flanking the upper bounds above `180 mm Hg`.

### 3. Feature Co-Dependency from Scatter Plots
* **The Ischemic Decay Trend:** Plotting `thalch` vs `age` reveals a clear downsloping linear trend. This visually maps the biological degeneration of cardiac threshold capacities as a patient's age increases.
* **Peak Stress Clusters:** Scatter combinations comparing `oldpeak` against `thalch` show distinct grouping patterns. Patients with lower maximum heart rates consistently exhibit significantly deeper, riskier ST depressions (`oldpeak` > 3.0), mapping a strong co-dependent signature of advanced coronary heart disease.

---

## 🚀 Execution & Pipeline Implementation Strategy

To guarantee statistical reliability, reproducibility, and production scalability, the project isolates workflows into independent steps.

### Environment Setup & Deployment
```bash
# Clone the repository
git clone https://github.com

# Navigate into the project workspace
cd uci-cardiovascular-predictive-pipeline

# Install system dependencies
pip install -r requirements.txt
```

### Multi-Stage Processing Order
1. **Target-Stratified Partitioning:** Isolation of a 20% holdout test environment using stratified splitting to preserve multiclass categorical ratios across data divisions.
2. **Context-Aware Imputation:** Categorical items are mapped via localized mode propagation, while continuous missingness undergoes multivariate iterative reconstruction to retain co-dependency metrics.
3. **Distribution Normalization:** Skewed quantitative features are mapped into Gaussian scales using non-linear transforms to remove outlier leverage.

### Model Evaluation Metric Baseline
Due to the medical risk profile of this application, optimizing solely for raw Accuracy is insufficient. The optimization loop evaluates models primarily on **Multiclass Recall (Sensitivity)** to prevent false negatives in higher-severity cardiovascular categories, cross-referenced with Macro-F1 scores to evaluate stability across all target classes.
