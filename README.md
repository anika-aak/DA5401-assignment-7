# DA5401 Assignment 7  
## Multi-Class Model Selection using ROC-AUC & PR-AP on Satimage Dataset

This project implements and compares multiple classification models for the Landsat Satimage dataset.  
The goal is to evaluate model performance using both traditional metrics and advanced threshold-independent metrics, then identify the best classifier.

---

## Dataset

- Source: UCI Satimage (Landsat MSS)  
- Input: 36 spectral features per pixel (3×3 neighborhood across 4 bands)  
- Output: Multi-class land-cover label  
- Split Provided:
  - `sat.trn` (training set)
  - `sat.tst` (test set)

**Note**: No cross-validation is used; training and evaluation follow the dataset's intended protocol.

---

## Models Evaluated

### Required Models
| Model | Notes |
|---|---|
K-Nearest Neighbors | Distance-based, standardized features  
Decision Tree | Non-parametric, interpretable splits  
Dummy Prior | Baseline using class priors  
Logistic Regression (OvR) | Linear decision boundaries  
Gaussian Naive Bayes | Class-conditional Gaussian assumption  
SVC (RBF Kernel) | Non-linear margin maximization  

### Bonus Models
| Model | Notes |
|---|---|
Random Forest | Bagged decision tree ensemble  
XGBoost | Gradient boosted trees  

---

## Evaluation Metrics

### Point Metrics
- Accuracy
- Weighted-F1

### Threshold-Independent Metrics
- Macro-averaged ROC-AUC (One-vs-Rest)
- Macro-averaged PR-AP (One-vs-Rest)

Macro averaging treats each class equally, which is important given class imbalance.

---

## Results Summary

### Required Models
| Rank | Metric Strength |
|---|---|
1. **KNN** | Best Accuracy, Weighted-F1, PR-AP; second in ROC-AUC  
2. **SVC** | Best ROC-AUC; close runner-up on others  
3. Decision Tree | Moderate performance  
4. Naive Bayes | Surprisingly strong on Satimage due to Gaussian structure  
5. Logistic Regression | Underfits non-linear boundaries  
6. Dummy Prior | Expected baseline performance  

### Bonus Models
| Rank | Metric Strength |
|---|---|
1. **Random Forest** | Best overall; strong across all metrics  
2. **XGBoost** | Very close second  

---

## Key Insights

- Neighborhood-based learning (KNN) and kernel methods (SVC) perform best among classical models.
- Ensemble trees outperform classical models by capturing non-linear spectral relationships.
- ROC-AUC and PR-AP provide complementary insight.  
  - SVC leads in ROC-AUC (ranking ability)  
  - KNN leads in PR-AP (precision at higher recall)

---

## Final Recommendation

- **Best Required Model:** KNN  
- **Best Overall Model:** Random Forest (XGBoost close second)

KNN delivers the strongest balance across Accuracy, Weighted-F1, ROC-AUC, and PR-AP.  
Ensemble models further improve results, confirming their effectiveness for high-dimensional remote-sensing data.

---

## How to Run

Ensure the files `sat.trn` and `sat.tst` are in the notebook directory, then run the notebook sequentially.  
All preprocessing and evaluation are contained within the notebook cells.

---

## Files Included

| File | Description |
|---|---|
Notebook `.ipynb` | Full implementation and analysis  
`sat.trn`, `sat.tst` | Dataset files (not uploaded due to licensing rules; add manually)  
ROC & PR plots | Model comparison visuals  

---

## Notes

- Standardization applied via pipelines where required  
- No cross-validation per dataset protocol  
- Macro-averaging used due to class imbalance


