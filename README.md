# RiskTrace

https://www.kaggle.com/datasets/japkeeratsingh/oss-vulnerabilities/data

https://github.com/DataDog/malicious-software-packages-dataset?utm_source=chatgpt.com

Final flow

GitHub Repository
↓
Dependency Collection — GitHub API + deps.dev
↓
Direct + Transitive Dependency Analysis
↓
Vulnerability Matching — OSV.dev (+ GitHub Advisory/NVD where needed)
↓
Risk Feature Engineering — vulnerability, severity, dependency depth, staleness, maintenance/Scorecard health, etc.
↓
PostgreSQL
↓
XGBoost Risk Prioritization
↓
SHAP Explainability
↓
FastAPI
↓
React + Tailwind Dashboard
↓
Risk Score + Reasons + Recommendations

ML stack 🔒
Primary: XGBoost
Comparison: Random Forest + Logistic Regression
Explainability: SHAP
Preprocessing: Scikit-learn
Data processing: Pandas + NumPy
Storage: PostgreSQL
