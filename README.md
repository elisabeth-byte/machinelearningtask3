# AUT-2607 Task 3

## Overview

This project investigates machine learning classification of industrial equipment faults using sensor measurements and frequency-domain features.

The objective is to predict the fault type of industrial equipment based on operational measurements and FFT-derived features.

Models used:

* Pearson Correlation
* Cross Correlation
* Linear Discriminant Analysis (LDA)
* Multi-Layer Perceptron (MLP)

Evaluation methods:

* Accuracy Score
* Confusion Matrix

---

## Dataset Description

Dataset: Industrial Fault Detection Dataset

The dataset contains:

* 1000 observations
* 36 input features
* 1 target variable

Target variable:

```text
Fault_Type
```

Classes:

```text
0 = Normal
1 = Fault A
2 = Fault B
3 = Fault C
```

The feature set is divided into two groups:

### Time-domain features

Direct physical measurements from the equipment:

* Temperature
* Vibration
* Pressure
* Flow_Rate
* Current
* Voltage

### Frequency-domain features

FFT (Fast Fourier Transform) coefficients derived from sensor signals:

* FFT_Temp_0 – FFT_Temp_9
* FFT_Vib_0 – FFT_Vib_9
* FFT_Pres_0 – FFT_Pres_9

These coefficients describe frequency patterns within the sensor signals and are commonly used in fault detection applications.

---

## Initial Data Analysis

The dataset was inspected before building the machine learning models.

The following checks were performed:

* Displayed the first rows of the dataset
* Inspected column names
* Verified dataset dimensions
* Checked for missing values
* Examined class distribution

Results:

* No missing values were found.
* No columns appeared to contain data leakage.
* No columns were considered irrelevant and therefore no columns were removed.
* The dataset contained all required information for model training.

The class distribution was noticeably imbalanced, with Fault Type 0 occurring significantly more frequently than the remaining classes.

---

## Preprocessing

Very little preprocessing was required.

The dataset:

* contained no missing values
* contained no obvious leakage variables
* consisted entirely of numerical features

Feature scaling was applied using StandardScaler before training the models.

This was particularly important for MLP, which is sensitive to differences in feature magnitude.

---

## Pearson Correlation Analysis

Pearson correlation was used to determine the relationship between input features and the target variable.

The strongest correlations were:

```text
FFT_Temp_6     -0.0578
FFT_Temp_4     -0.0578
FFT_Vib_0       0.0446
Flow_Rate      -0.0340
FFT_Vib_6      -0.0317
```

All correlation coefficients were very close to zero.

This indicates that none of the individual features had a strong linear relationship with Fault_Type.

---

## Cross Correlation Analysis

A correlation heatmap was generated to investigate relationships between input features.

Cross-correlation analysis revealed several highly correlated FFT features. This suggests that some frequency-domain variables contain redundant information and may describe similar signal characteristics.

---

## Results

### LDA

Accuracy:

```text
0.70
```

Confusion Matrix:

```text
[[140   0   0   0]
 [ 20   0   0   0]
 [ 22   0   0   0]
 [ 18   0   0   0]]
```

Observation:

The LDA model predicted only the majority class (Fault Type 0).

---

### MLP

Accuracy:

```text
0.555
```

Confusion Matrix:

```text
[[107  14  11   8]
 [ 15   3   1   1]
 [ 20   1   1   0]
 [ 12   2   4   0]]
```

Observation:

The MLP model attempted to classify all fault categories but still produced relatively poor performance.

---

## Discussion

Both machine learning models achieved limited performance.

LDA classified almost every observation as the majority class, resulting in an accuracy of 70%.

MLP produced more diverse predictions but achieved a lower overall accuracy of 55.5%.

The Pearson correlation analysis showed that almost all features had very weak relationships with Fault_Type.

This suggests that the available features do not provide sufficient information to clearly distinguish between the four fault categories.

---


## Conclusion

The project successfully demonstrated a complete machine learning workflow involving preprocessing, scaling, correlation analysis, LDA and MLP classification.

However, both models produced relatively poor performance.

The weak Pearson correlations suggest that the available features provide limited information about the target variable, which likely contributed to the low classification accuracy.

This dataset serves as a useful example of how machine learning performance depends heavily on feature quality and class separability.
