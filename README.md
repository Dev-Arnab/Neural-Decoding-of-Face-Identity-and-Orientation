# Neural Decoding of Face Identity and Orientation in Primate Anterior Medial Cortex

## 🧠 Project Overview

This project implements machine learning decoding techniques to analyze electrophysiological data from the **Anterior Medial (AM) face patch** of two macaque monkeys, Bert and Lupo. The goal is to determine how linearly separable face-specific information-namely **face identity** and **head orientation**-is encoded in the collective firing rates of the neuronal population.

The core analysis involves comparing the performance of linear classifiers (Logistic Regression) on discrete face features against the performance of a linear regressor (Ridge Regression) on a continuous angular feature.

### Research Questions

- What are the basic statistical properties of the spike count features across the two subjects?
- Can the AM population collectively **classify** the discrete face identity and head orientation features?
- Can the collective firing rates of the AM population predict the **continuous horizontal head angle**?

## 🛠️ Methodology and Computational Pipeline

### 1\. Data Processing and Feature Engineering

The initial dataset consists of over 200,000 trial-level spike records.

- **Feature:** For each trial, the raw spike times were aggregated into a single feature: the **Total Spike Count in the first 400ms** following stimulus onset.
- **Pivoting:** This trial-level data was then averaged and pivoted using parallel processing to create a final feature matrix, \$X\$ (shape: 200 Stimuli x 154 Neurons). Each row represents the mean population response to a unique stimulus combination.

### 2\. Decoding Models

| **Task** | **Model** | **Features (X)** | **Target (Y)** | **Primary Metric** |
| --- | --- | --- | --- | --- |
| **Classification (Discrete)** | Logistic Regression (L2) | Mean Spike Counts (154 features) | 25 Face Identities (or 8 Orientations) | Accuracy, Confusion Matrix |
| --- | --- | --- | --- | --- |
| **Regression (Continuous)** | Ridge Regression (L2) | Mean Spike Counts (154 features) | Continuous Head Angle (\$0^\\circ\$ to \$315^\\circ\$) | RMSE, \$R^2\$ Score |
| --- | --- | --- | --- | --- |

## 📈 Key Quantitative Results

### A. Classification Success (Discrete Features)

The AM population strongly and linearly encodes discrete face features.

- **Face Identity (25 Classes):** Achieved **80.0% accuracy**, demonstrating a 20-fold increase over the 4% chance level. This confirms the strong, linearly separable encoding of identity.
- **Head Orientation (8 Classes):** Achieved **72.0% accuracy**, confirming a robust linear code for discrete view categories.

### B. Regression Failure (Continuous Angle)

The linear model failed to decode the continuous head angle, suggesting the continuous feature relies on a non-linear code or that the model was incorrectly specified for circular data.

- **Root Mean Squared Error (RMSE):** **99.81 degrees**, indicating poor predictive power.
- **R-squared (**\$R^2\$**):** **0.27**, meaning only 27% of the variance in the true angle was explained by the neural activity.

## 🧭 Project Artifacts and Structure

The core analysis is contained within the Jupyter Notebook.

- report_section_2.ipynb: The main notebook containing the data loading, EDA, classification models, regression models, and full discussion/conclusion.
- Project_Plots/: Directory containing all generated figures, including spike count distributions, monkey-specific variability, confusion matrices, and the regression plots.

## 🚀 Future Work

- **Circular Regression:** Implement circular statistical methods (e.g., sine/cosine transformation) to address the \$0^\\circ/360^\\circ\$ boundary problem and properly test for a parametric code.
- **Temporal Decoding:** Re-run analysis across different time windows (\$0-100ms\$ vs. \$400-800ms\$) to investigate the temporal dynamics of face encoding.
- **Non-Linear Models:** Apply non-linear classifiers (e.g., Support Vector Machines) to see if they can significantly improve the decoding accuracy of the continuous head angle.

## 👨‍💻 Author

This project was developed by **Dev Jyoti Ghosh Arnab**.

## 📚 Data Source Citation

Freiwald, W. A., & Tsao, D. Y. (2010). The face view specificity of macaque face patch AM: Data for 25 identities and 8 orientations. Harvard Dataverse
