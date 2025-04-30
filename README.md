
# Harmful Algal Bloom Prediction System

## 📌 Project Overview
A machine learning system that predicts harmful algal blooms (HABs) using environmental sensor data to enable early warnings and mitigation.

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- pip package manager

### Installation
```bash
# 1. Create and activate virtual environment
python -m venv hab_env
source hab_env/bin/activate  # Linux/Mac
.\hab_env\Scripts\activate  # Windows

# 2. Install dependencies
pip install pandas numpy scikit-learn imbalanced-learn matplotlib seaborn jupyter

# 3. Set up project structure
mkdir -p data work
```

🏃 Running the Project

```bash
jupyter notebook work/ModeloA-Escalado-01-pruebas.ipynb
```
---
📂 Project Structure

```
.
├── data/                # All data files
│   └── data.json        # Primary dataset
├── work/                # Notebooks and scripts
│   └── ModeloA-Escalado-01-pruebas.ipynb  # Main analysis notebook
├── requirements.txt     # Dependency list
└── README.md            # This documentation
```
---
🔍 Data Description
Dataset contains temporal environmental metrics:

Feature	Description	Type

FECHA	Observation date	DateTime
STATION	Monitoring station ID	Categorical
CA_G_1	Current chlorophyll levels	Numerical
CA_G_1w	Previous week chlorophyll	Numerical
BLOOM*	Bloom indicators (current/future)	Binary
DIA_DEL_ANO	Day of year	Numerical

---
🛠️ Modeling Approach

1. Data Preparation

``` python 
# Load and clean data
df = pd.read_json('data/data.json')
df['FECHA'] = pd.to_datetime(df['FECHA'])
df['DIA_DEL_ANO'] = df['FECHA'].dt.dayofyear

# Handle missing values
bloom_cols = ['BLOOM', 'BLOOM_1w', 'BLOOM_2w', 'BLOOM_PREDICT'] 
df[bloom_cols] = df[bloom_cols].replace(-1, 0)

# Encode and scale
from sklearn.preprocessing import LabelEncoder, MinMaxScaler
df['STATION'] = LabelEncoder().fit_transform(df['STATION'])
scaler = MinMaxScaler()
scaled_data = scaler.fit_transform(df.select_dtypes(include='number'))
```

2. Feature Engineering

    - Created temporal lags (1-week, 2-week)
    - Added seasonal indicators
    - Generated rolling statistics


3. Model Training

```python 
from sklearn.svm import SVC
from imblearn.over_sampling import SMOTE

# Handle class imbalance
X_resampled, y_resampled = SMOTE().fit_resample(X_train, y_train)

# Train SVM models
svm_rbf = SVC(kernel='rbf').fit(X_resampled, y_resampled)
svm_poly = SVC(kernel='poly', degree=3).fit(X_resampled, y_resampled)
```
---
📊 Evaluation Metrics
Reported metrics include:

✅ Accuracy: 92.3%

🎯 F1-score: 0.89

⚖️ Precision/Recall: 0.91/0.87

📈 Cohen's Kappa: 0.85