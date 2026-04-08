# Customer Segmentation & Prediction System

## Project Overview
This project builds a small customer analytics system that combines unsupervised and supervised machine learning for e-commerce customer retention analysis.

The system performs three main tasks:
1. It uses **K-Means clustering** to segment customers based on behavioral and demographic patterns.
2. It uses **supervised learning models** to predict whether a customer will be retained.
3. It applies a simple **rule-based recommendation logic** that assigns a business action to each discovered customer segment.

The goal of the project is to show how clustering, prediction, and business-oriented recommendations can be combined into a practical customer analytics pipeline.

---

## Project Structure
```text
project-folder/
│
├── Customer Segmentation & Prediction System.ipynb
├── README.md
├── final_test_predictions.csv
└── CUSTOMER RETENTION STRATEGIES IN E-COMMERCE/
    ├── Train_Data.csv
    └── Test_Data.csv
```

---

## Dataset
The dataset used in this project is the **Customer retention strategies in e-commerce** dataset from Kaggle.

The files used are:
- `CUSTOMER RETENTION STRATEGIES IN E-COMMERCE/Train_Data.csv`
- `CUSTOMER RETENTION STRATEGIES IN E-COMMERCE/Test_Data.csv`

### Main feature groups
The dataset includes:
- **Email engagement features** such as `esent`, `eopenrate`, and `eclickrate`
- **Transactional features** such as `avgorder` and `ordfreq`
- **Customer preference/service features** such as `paperless`, `refill`, and `doorstep`
- **Categorical features** such as `favday` and `city`
- **Date features** such as `created`, `firstorder`, and `lastorder`

### Target variable
The target variable is:
- `retained`  
  - `1` = retained customer  
  - `0` = not retained customer

---

## Data Preprocessing
The following preprocessing steps were applied before modeling:

- Missing values in key numerical columns were filled using the **median**
- Rows with missing or invalid date values were removed
- Date columns were converted to datetime format
- Three engineered features were created:
  - `tenure_days`
  - `days_to_first`
  - `days_since_last`
- Unnecessary columns such as `custid`, `created`, `firstorder`, and `lastorder` were dropped
- Categorical variables (`favday` and `city`) were one-hot encoded using `get_dummies`
- Training and validation sets were created using an **80/20 split**
- Features were standardized using `StandardScaler`

---

## K-Means Clustering
K-Means clustering was applied to the scaled training features to discover customer segments.

### Cluster selection
The **Elbow Method** was used to compare values of `k` from 1 to 10.  
Based on the elbow curve and cluster balance, the final number of clusters was chosen as:

- **K = 3**

### Cluster interpretation
The three clusters were interpreted as:

- **Cluster 0:** Veteran Low-Engagement Customers
- **Cluster 1:** Mid-Tenure Moderate Customers
- **Cluster 2:** New High-Engagement Customers

### Visualization
To visualize the clusters, **PCA** was used to reduce the feature space to 2 dimensions and produce a 2D cluster plot.

---

## Supervised Learning Models
Two supervised learning models were trained to predict customer retention:

- **Logistic Regression**
- **Random Forest**

### Evaluation metrics
Models were compared using:
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- ROC-AUC
- ROC Curve

### Best model
Among the evaluated models, **Random Forest** produced the strongest overall validation performance and was selected as the final model.

Its validation performance was:

- **Accuracy:** 96.51%
- **Precision:** 96.55%
- **Recall:** 99.14%
- **F1-score:** 97.83%
- **ROC-AUC:** 98.31%

---

## Recommendation Logic
A simple **rule-based recommendation system** was created based on the K-Means cluster insights.

The recommendations are:

- **Veteran Low-Engagement Customers**  
  → Send retention emails and discount offers

- **Mid-Tenure Moderate Customers**  
  → Offer personalized bundles and cross-sell products

- **New High-Engagement Customers**  
  → Recommend premium products and loyalty rewards

This recommendation layer was intentionally kept simple, as the objective of the project was to map each segment to a clear and explainable business action.

---

## Files Included
- `Customer Segmentation & Prediction System.ipynb` – main notebook containing data cleaning, clustering, model training, evaluation, and recommendation logic
- `CUSTOMER RETENTION STRATEGIES IN E-COMMERCE/Train_Data.csv` – training dataset
- `CUSTOMER RETENTION STRATEGIES IN E-COMMERCE/Test_Data.csv` – test dataset
- `final_test_predictions.csv` – final predicted retention labels for the test set
- `README.md` – project overview and instructions

---

## How to Run
1. Keep the project structure exactly as shown above.
2. Open the notebook:
   - `Customer Segmentation & Prediction System.ipynb`
3. Run the notebook from top to bottom.
4. The notebook will:
   - clean and preprocess the data
   - perform K-Means clustering
   - train and evaluate the supervised models
   - generate final test predictions
   - display the recommendation logic summary
5. The final prediction file will be saved as:
   - `final_test_predictions.csv`

---

## Notes
- The provided test set does not contain true labels, so model evaluation is performed on a validation split from the training data.
- The dataset is imbalanced, with retained customers making up the large majority of the samples.
- The recommendation system is rule-based and not a learned recommender model.

---

## Authors
- Maher Maher
- Ilyes Hasnaou
