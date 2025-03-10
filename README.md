# SARCON: Extremity Soft Tissue SArcoma ReConstruction Nomograms

A Clinicoradiomic, Machine Learning-Powered Predictor of Postoperative Outcomes

## Overview

This repository contains five LASSO regression classifiers designed to predict the likelihood of specific postoperative complications in patients undergoing reconstructive surgery for extremity soft tissue sarcoma. The five complications of interest are:

1. **Minor Complications**  
2. **Major Complications**  
3. **Incisional Dehiscence**  
4. **Seroma**  
5. **Infection**

Each model has been trained and saved in a pickle (`.pkcls`) format for easy loading and application.

## Repository Contents

- **`minorcomp_logreg.pkcls`**  
  Lasso regression model for predicting minor complications.

- **`majorcomp_logreg.pkcls`**  
  Lasso regression model for predicting major complications.

- **`id_logreg.pkcls`**  
  Lasso regression model for predicting incisional dehiscence (abbreviated “ID”).

- **`seroma_logreg.pkcls`**  
  Lasso regression model for predicting seroma formation.

- **`ssi_logreg.pkcls`**  
  Lasso regression model for predicting surgical site infection (abbreviated “SSI”).

## Installation & Requirements

1. **Python** (3.7+ recommended)  
2. **Scikit-learn** (ensure compatibility with the pickle files; version 0.24+ typically works)  
3. **Pandas**, **NumPy** (for data manipulation and array structures)  
4. **Joblib** or **Pickle** (for model loading; though standard `pickle` is already in Python’s standard library)

You can install any missing packages via:
```
pip install -U scikit-learn pandas numpy
```

## Usage

### 1. Cloning the Repository

```
git clone https://github.com/YourUsername/SARCON.git
cd SARCON
```

### 2. Loading a Model

Below is an example of how to load and use the **Minor Complications** model in Python. The same procedure applies to the other `.pkcls` files—simply replace the filename with the desired complication’s model.

```python
import pickle
import pandas as pd

# 1. Load the model
with open('minorcomp_logreg.pkcls', 'rb') as f:
    minorcomp_model = pickle.load(f)

# 2. Load or prepare your dataset (example)
# Replace 'features.xlsx' with your actual data file
data = pd.read_excel('features.xlsx')
X = data.drop(columns=['target'])  # your feature columns
# y = data['target']  # only if you have labels for evaluation

# 3. Generate predictions or probabilities
y_pred = minorcomp_model.predict(X)
y_proba = minorcomp_model.predict_proba(X)[:, 1]  # Probability of the positive class

print("Predictions:", y_pred)
print("Probabilities:", y_proba)
```

### 3. Evaluating the Model

If you have ground truth labels (e.g., whether a complication actually occurred), you can calculate metrics like AUC, Accuracy, F1, etc.:

```python
from sklearn.metrics import accuracy_score, roc_auc_score, f1_score

y_true = data['target']  # ground truth
acc = accuracy_score(y_true, y_pred)
auc = roc_auc_score(y_true, y_proba)
f1 = f1_score(y_true, y_pred)

print(f"Accuracy: {acc:.4f}")
print(f"AUC: {auc:.4f}")
print(f"F1 Score: {f1:.4f}")
```

### 4. Applying Other Models

To use the models for **major complications**, **incisional dehiscence**, **seroma**, or **infection**, just load the corresponding `.pkcls` file (e.g., `majorcomp_logreg.pkcls`, `id_logreg.pkcls`, `seroma_logreg.pkcls`, or `ssi_logreg.pkcls`) and repeat the steps above.

## Notes & Limitations

- **Data Compatibility**: Ensure that the input features (column order, preprocessing steps) match those expected by the model. Mismatched features may produce erroneous predictions.
- **Model Interpretability**: Lasso regression can help identify important predictors by shrinking coefficients. For interpretability, examine the model coefficients to see which features have the greatest impact on each complication risk.
- **Clinical Use**: These models are provided for research and informational purposes. Any clinical application should be validated with proper regulatory and institutional approvals.
- **Performance**: The reported accuracy, AUC, and other metrics will depend on the quality and representativeness of your input data. Always evaluate the models on your local dataset before drawing conclusions.

## Contributing

If you wish to contribute (e.g., add new features or improve the models):

1. Fork this repository.
2. Create a new branch: `git checkout -b feature-branch`.
3. Make your changes and commit them: `git commit -m "Add new feature"`.
4. Push to the branch: `git push origin feature-branch`.
5. Create a Pull Request.

## License

This project is licensed under the terms of the [MIT License](LICENSE) (or whichever license you choose). See the [LICENSE](LICENSE) file for details.

**Disclaimer**: This repository is intended for educational and research purposes. The authors are not liable for any clinical decisions made based on these models. Always consult a licensed healthcare provider for clinical decision-making.
