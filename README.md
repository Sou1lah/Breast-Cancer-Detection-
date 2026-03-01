
#  Breast Cancer Detection

Binary classification model that predicts whether a breast tumor is malignant or benign from 30 clinical measurements derived from fine needle aspirate (FNA) images. Built with TensorFlow/Keras on the Wisconsin Breast Cancer Dataset, the model achieves 97% accuracy and — more critically for clinical relevance — 98% recall on malignant cases, meaning it misses only 1 in 42 cancer diagnoses. The project ships with a Streamlit app featuring interactive charts, presets, and feature importance analysis across two methods.

---

## Results

| Metric | Malignant | Benign | Overall |
|--------|-----------|--------|---------|
| Accuracy | — | — | **97%** |
| Precision | 95% | 99% | 97% |
| Recall | **98%** | 97% | 97% |
| F1 Score | 96% | 98% | 97% |
| AUC-ROC | — | — | ~0.99 |

> Recall on malignant (class 0) is the primary success metric. A false negative — predicting benign when the tumor is malignant — is far more dangerous than a false positive.

---

## Model Architecture

```
Input: 30 numerical features
       ↓
Dense(64, activation='relu')
BatchNormalization()
Dropout(0.3)
       ↓
Dense(32, activation='relu')
BatchNormalization()
Dropout(0.3)
       ↓
Dense(1, activation='sigmoid')

Loss:      Binary Cross Entropy
Optimizer: Adam
Metric:    Accuracy, AUC, Recall
```

---

## Key ML Techniques

**[RobustScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.RobustScaler.html)**
Scales features using the interquartile range instead of mean/std. Chosen over `StandardScaler` because several features (e.g. `area error`) contain 11%+ outliers that would skew standard normalization.

**[Batch Normalization](https://keras.io/api/layers/normalization_layers/batch_normalization/)**
Normalizes layer outputs during training, stabilizing gradients and allowing faster convergence. Applied after each Dense layer before Dropout.

**[Dropout](https://keras.io/api/layers/regularization_layers/dropout/)**
Randomly disables 30% of neurons per forward pass during training, forcing the network to learn redundant representations and reducing overfitting.

**[Early Stopping](https://keras.io/api/callbacks/early_stopping/)**
Monitors `val_loss` with a patience of 10 epochs and restores the best weights automatically. Prevents overfitting without manually tuning epoch count — training stopped at epoch ~72.

**[Binary Cross Entropy](https://keras.io/api/losses/probabilistic_losses/#binarycrossentropy-class)**
Standard loss for binary classification. Heavily penalizes confident wrong predictions — critical when the cost of missing a malignant case is high.

---

## Project Structure

```
Breast Cancer/
├── Dataset/                  # Raw CSV data
├── model/                    # Saved Keras model and scaler
├── reports/                  # Dataset analysis report
├── file.ipynb                # Training notebook
├── deploy.py                 # Streamlit web app
└── README.md
```

- [`model/`](./model) — stores `breast_cancer_model.h5` and `scaler.pkl`. Both are required by the Streamlit app at runtime.
- [`file.ipynb`](./file.ipynb) — full training pipeline: EDA, preprocessing, model training, evaluation, and export.
- [`deploy.py`](./deploy.py) — Streamlit app with prediction UI and dataset visualizations.

---

## Installation

```bash
# Clone the repo
git clone https://github.com/yourusername/breast-cancer-detection.git
cd "breast-cancer-detection/Breast Cancer"

# Install dependencies
pip install tensorflow scikit-learn streamlit plotly pandas numpy
```

**Dependencies:**

| Library | Purpose |
|---------|---------|
| [TensorFlow / Keras](https://www.tensorflow.org/api_docs/python/tf/keras) | Model building and training |
| [Scikit-learn](https://scikit-learn.org/stable/) | Preprocessing, metrics, Random Forest |
| [Streamlit](https://docs.streamlit.io/) | Web app |
| [Plotly](https://plotly.com/python/) | Interactive charts |
| [Pandas](https://pandas.pydata.org/docs/) | Data manipulation |
| [NumPy](https://numpy.org/doc/) | Numerical operations |

---

## Running the App

```bash
# From inside the Breast Cancer/ directory
streamlit run deploy.py
```

The app loads the saved model and scaler from [`model/`](./model) at startup. Both files must exist before running.

---

## App Features

- **Presets** — one-click auto-fill with average malignant or benign feature values from the dataset
- **Live prediction** — input 30 measurements and get an instant malignant/benign result with confidence score
- **Class distribution** — pie chart of benign vs malignant split across 569 samples
- **Feature comparison** — box plots comparing any feature's distribution across both classes
- **Correlation heatmap** — top 10 feature correlations visualized as an interactive matrix
- **Feature importance (correlation)** — all 30 features ranked by absolute correlation with the target label
- **Feature importance (Random Forest)** — importance scores from a 100-tree Random Forest trained on the full dataset
- **Method agreement analysis** — highlights which features both importance methods agree on, identifying the most reliable predictors
