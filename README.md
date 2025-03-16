# Extremity Soft Tissue SArcoma ReConstruction Nomograms (SARCON)

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


## License

This project is licensed under the terms of the [MIT License](LICENSE)
**Disclaimer**: This repository is intended for educational and research purposes. The authors are not liable for any clinical decisions made based on these models. Always consult a licensed healthcare provider for clinical decision-making.
