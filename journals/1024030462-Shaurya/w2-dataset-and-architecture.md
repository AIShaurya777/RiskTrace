# Week 2 : Dataset Selection, Architecture Finalization and Feature Identification

## Objective

The objective of Week 2 was to investigate suitable datasets and external information sources for RiskTrace and use the findings to finalize the system architecture, risk features, and machine-learning technology stack.

The team focused on determining what information would be required at each stage of the dependency-risk analysis pipeline.

---

## 1. Dataset Investigation

After finalizing the project idea, the team investigated publicly available datasets that could support vulnerability analysis and the future machine-learning component.

Two important datasets were considered.

### OSS Vulnerabilities Dataset

The team investigated the **OSS Vulnerabilities** dataset available on Kaggle.

The dataset provides vulnerability-related information for open-source software and contains information associated with vulnerabilities reported through sources such as the National Vulnerability Database.

Reference:

https://www.kaggle.com/datasets/japkeeratsingh/oss-vulnerabilities/data

The dataset was considered useful for understanding vulnerability records and creating structured vulnerability-related information for the project.

### DataDog Malicious Software Packages Dataset

The team also investigated the **DataDog Malicious Software Packages Dataset**.

The dataset contains manually vetted malicious software packages and is intended to support research and analysis related to software supply-chain security.

Reference:

https://github.com/DataDog/malicious-software-packages-dataset

The dataset was considered useful for broadening the security perspective beyond conventional CVE-based vulnerability records and for investigating malicious-package behavior.

## Dataset Limitation

During the dataset investigation, the team identified that a single static dataset would not provide all the information required by RiskTrace.

The proposed system requires information about:

* Package versions.
* Dependency relationships.
* Direct and transitive dependencies.
* Vulnerability records.
* Vulnerable version ranges.
* Fixed versions.
* Vulnerability severity.
* Package maintenance.
* Repository health.

Therefore, the team decided to combine static datasets with information obtained from external APIs and security databases.

---

# 2. External Data Sources

The team investigated several external sources that could provide live or structured dependency and security information.

## GitHub API

The GitHub REST API was selected for repository integration.

It can provide information such as:

* Repository metadata.
* Repository contents.
* Dependency-related files.
* Source-code information.
* Commit and activity information.

The repository provided by the user would therefore act as the starting point for the RiskTrace analysis.

## deps.dev

deps.dev was selected as an important dependency-information source.

It can provide package and project information and help resolve dependency relationships.

The team planned to use it for:

* Dependency graph information.
* Package-version information.
* Direct/transitive dependency analysis.
* Project-related information.

## OpenSSF Scorecard

OpenSSF Scorecard information was considered as an additional source of repository/project health indicators.

These indicators can provide information that may be useful when assessing the overall health and maintenance characteristics of a dependency.

## OSV.dev

OSV.dev was selected as the primary vulnerability-matching source.

The planned workflow is to query vulnerability information for identified package versions.

The system can use the returned information to identify:

* Vulnerability identifiers.
* Affected versions.
* Fixed versions.
* Severity information.
* Related security metadata.

## GitHub Advisory Database and NVD

The team also retained the GitHub Advisory Database and NVD as additional vulnerability-information sources.

These sources can be used where additional vulnerability information or enrichment is required.

This resulted in a multi-source security-information strategy instead of depending on a single vulnerability database.

---

# 3. Architecture Finalization

Based on the dataset and API investigation, the initial architecture was expanded and finalized.

The final system flow became:

```text
GitHub Repository
        ↓
Dependency Collection
(GitHub API + deps.dev)
        ↓
Direct + Transitive Dependency Analysis
        ↓
Vulnerability Matching
(OSV.dev + GitHub Advisory / NVD where required)
        ↓
Risk Feature Engineering
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
```

The architecture was divided into separate logical stages so that each stage could be developed and tested independently.

---

# 4. Dependency Collection and Resolution

The first stage of the finalized architecture is repository ingestion.

The user provides a GitHub repository to RiskTrace.

The system is planned to collect:

* Repository metadata.
* Dependency manifests.
* Package names.
* Package versions.
* Ecosystem information.

The Dependency Resolver then identifies both:

**Direct dependencies**

and

**Transitive dependencies**

The dependency graph is also used to calculate dependency depth.

This information becomes important later during risk feature engineering.

---

# 5. Vulnerability Matching

After dependencies are resolved, the dependency information is passed to the vulnerability-matching stage.

The team decided to primarily use OSV.dev for package-version vulnerability lookups.

Additional information may be obtained from:

* GitHub Advisory Database.
* NVD.

The matching stage is intended to normalize vulnerability information so that different vulnerability identifiers and records can be associated with the correct dependency.

The expected information includes:

* CVE.
* GHSA.
* CWE where available.
* CVSS/severity.
* Affected versions.
* Fixed versions.

---

# 6. Risk Feature Identification

The team decided that the ML model should not rely only on vulnerability severity.

A broader set of risk features was therefore identified.

The planned features include:

### Vulnerability Features

* Number of known vulnerabilities.
* Maximum vulnerability severity/CVSS.
* Vulnerability-related indicators.

### Dependency Features

* Direct/transitive status.
* Dependency depth.
* Package ecosystem.
* Version information.

### Package Freshness

* Package age.
* Staleness indicators.

### Maintenance

* Maintenance/activity indicators.
* Recent repository activity where available.

### Repository Health

* OpenSSF Scorecard/project-health indicators.
* Repository-level health information.

### Code Complexity

Source-code complexity was considered as an additional feature.

Lizard was considered for obtaining complexity-related information where applicable.

These features were selected to provide a broader representation of dependency risk.

---

# 7. ML Stack Finalization

The machine-learning stack was also finalized during this stage.

## Primary Model

**XGBoost**

XGBoost was selected as the primary risk-prioritization model.

## Comparison Models

Two additional models were selected for comparison:

* Random Forest.
* Logistic Regression.

The comparison will help determine whether XGBoost provides meaningful improvement over alternative models.

## Data Processing

The planned data-processing stack is:

* Pandas.
* NumPy.

## Preprocessing

Scikit-learn will be used for preprocessing and model evaluation.

---

# 8. Explainability

The team decided to use **SHAP** for explainability.

The purpose is to explain the contribution of individual risk features to a model prediction.

The intended workflow is:

```text
Risk Features
      ↓
XGBoost
      ↓
Risk Score
      ↓
SHAP
      ↓
Feature Contributions
      ↓
Human-Readable Reasons
```

This ensures that RiskTrace does not simply output a risk number.

Instead, the developer should be able to understand the factors that contributed to the ranking.

---

# 9. Database and Application Architecture

PostgreSQL was finalized as the database layer.

The database is planned to store:

* Repository information.
* Dependency information.
* Dependency relationships.
* Vulnerabilities.
* Risk features.
* Scan metadata.
* Risk scores.
* Model information.
* SHAP explanations.

The application layer was divided into:

### Backend

**FastAPI**

Responsible for analysis orchestration, API communication, ML inference, and database interaction.

### Frontend

**React + Tailwind CSS**

Responsible for presenting:

* Repository risk.
* Dependency rankings.
* Vulnerability information.
* Risk scores.
* SHAP explanations.
* Recommendations.

---

# 10. Additional Features Discussed

During the architecture discussions, the team also identified features that could improve the practical usefulness of RiskTrace.

These included:

* Dependency-risk ranking.
* Vulnerability details.
* Risk explanations.
* Upgrade recommendations.
* Repository scan history.
* Filtering and sorting of dependencies.
* Trend visualization for repeated scans.

The core functionality was prioritized first, while some dashboard enhancements were kept as later deliverables.

---


# Key Design Decision

A major decision made during Week 2 was to treat RiskTrace as a **multi-stage dependency intelligence and risk-prioritization pipeline** rather than a simple vulnerability scanner.

The final conceptual flow was:

```text
Repository
    ↓
Dependency Intelligence
    ↓
Security Intelligence
    ↓
Risk Features
    ↓
ML Prioritization
    ↓
Explainability
    ↓
Developer Decision Support
```

This architecture allows the project to gradually progress from basic dependency analysis to ML-based risk prioritization without making the ML model responsible for the entire security-analysis process.

---

# Result

By the end of Week 2, the team had:

* Investigated the OSS Vulnerabilities dataset.
* Investigated the DataDog malicious software packages dataset.
* Identified GitHub API and deps.dev as dependency-information sources.
* Selected OSV.dev as the primary vulnerability-matching source.
* Retained GitHub Advisory Database and NVD for additional vulnerability information.
* Identified OpenSSF Scorecard-related health indicators.
* Finalized direct and transitive dependency analysis.
* Identified the major risk features.
* Finalized XGBoost as the primary ML model.
* Selected Random Forest and Logistic Regression for comparison.
* Selected SHAP for explainability.
* Finalized PostgreSQL, FastAPI, React, and Tailwind CSS for the application architecture.
* Discussed additional features such as recommendations, history, filtering, and trend analysis.

The finalized architecture provided the technical foundation for preparing the formal project proposal in the following week.

## Individual Contribution

Each team member can add their own contribution below.

**My contribution:**
Participated in dataset investigation and comparison, contributed to discussions on dependency and vulnerability data sources, helped finalize the architecture and risk features, and participated in discussions regarding the ML, explainability, database, backend, and frontend components.

