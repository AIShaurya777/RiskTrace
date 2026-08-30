# Week 2 : Dataset Selection and Architecture Finalization

## Objective

The objective of this week was to investigate suitable datasets and security information sources for RiskTrace and use the findings to finalize the system architecture and risk features.

## Dataset Investigation

After finalizing the problem statement, the next challenge was identifying data that could support the proposed vulnerability analysis and machine-learning component.

Two important publicly available datasets were investigated.

### 1. OSS Vulnerabilities Dataset

The first dataset considered was the **OSS Vulnerabilities** dataset available on Kaggle.

The dataset contains vulnerabilities identified in open-source software and reported to the National Vulnerability Database (NVD). It includes vulnerability-related information such as CVE and CWE identifiers and descriptions.

Dataset reference:

https://www.kaggle.com/datasets/japkeeratsingh/oss-vulnerabilities/data

This dataset was considered useful for obtaining structured vulnerability information and developing vulnerability-related features.

### 2. DataDog Malicious Software Packages Dataset

The second major dataset investigated was the **DataDog Malicious Software Packages Dataset**.

The repository contains more than 28,000 malicious software packages identified as part of DataDog's software supply-chain security research. The dataset currently covers ecosystems including npm and PyPI, along with IDE extensions and AI Skills. DataDog states that the included packages have been manually triaged by humans.

Reference:

https://github.com/DataDog/malicious-software-packages-dataset

The dataset was considered useful for studying malicious-package behavior and for broadening the security data used by the project.

## Dataset Limitation

An important observation was that no single dataset completely represents the dependency-risk problem.

The project needs information about:

* Known vulnerabilities.
* Affected package versions.
* Dependency relationships.
* Dependency depth.
* Package maintenance.
* Repository health.
* Malicious-package indicators.

Therefore, datasets alone would not be sufficient.

The final design would need to combine datasets with live or structured security information from external services.

## External Data Sources

The proposed architecture therefore included multiple sources.

### OSV.dev

OSV.dev was selected as a major vulnerability-matching source.

Its API supports querying vulnerabilities for a specific package and version, as well as batch vulnerability queries.

This makes it suitable for checking whether a dependency version identified from a repository has known vulnerabilities.

### deps.dev

deps.dev was selected for dependency and package metadata.

The deps.dev API provides information about package versions, dependency relationships, projects, advisories, and related package information. It also aggregates data from package registries and project sources and includes OpenSSF Scorecard information.

This makes it useful for obtaining information beyond the vulnerability itself.

## Architecture Finalization

Based on the dataset and API investigation, the system architecture was refined and finalized as a pipeline rather than a single ML application.

The final conceptual flow became:

```text
GitHub Repository
        ↓
Dependency Collection
(GitHub API + deps.dev)
        ↓
Direct + Transitive Dependency Analysis
        ↓
Vulnerability Matching
(OSV.dev + GitHub Advisory / NVD where needed)
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

## Dependency Collection

The first stage of the architecture receives a GitHub repository from the user.

The system is intended to identify both:

* Direct dependencies.
* Transitive dependencies.

The use of deps.dev was planned to help obtain dependency relationships and package metadata. The GitHub API was included for repository integration and repository-level information.

## Vulnerability Matching

After dependencies are identified, each dependency and relevant version is checked against vulnerability information.

The primary planned source is OSV.dev.

GitHub Advisory Database and NVD were retained as additional sources where required.

This multi-source approach was selected because relying on one vulnerability source could result in incomplete coverage.

## Risk Feature Engineering

The project was expanded beyond simple vulnerability severity.

The planned features include:

* Vulnerability presence.
* Vulnerability severity.
* Number of vulnerabilities.
* Dependency depth.
* Direct/transitive dependency status.
* Package staleness.
* Maintenance activity.
* Repository health.
* OpenSSF Scorecard-related health indicators.
* Other package-level security indicators where available.

The purpose of these features is to provide the ML model with more context than a raw CVSS or vulnerability severity value.

## ML Stack

The machine-learning stack was finalized as:

**Primary model:**

* XGBoost

**Comparison models:**

* Random Forest
* Logistic Regression

**Preprocessing:**

* scikit-learn

**Data processing:**

* Pandas
* NumPy

XGBoost was selected as the primary model because the proposed feature set is primarily structured/tabular data and may contain nonlinear relationships between dependency characteristics and risk.

The comparison models will provide baselines for evaluating whether the additional complexity of XGBoost provides useful improvement.

## Explainability

SHAP was selected as the explainability layer.

The objective is not only to output a numerical risk score but also to identify the features that contributed to the prediction.

For example, a high-risk dependency could potentially receive a high score because of a combination of:

* High vulnerability severity.
* Multiple known vulnerabilities.
* Large dependency depth.
* Outdated package information.
* Poor maintenance indicators.

The final explanation should allow a developer to understand the factors behind the prioritization.

## Storage

PostgreSQL was selected as the database layer.

The planned database will store information such as:

* Repository information.
* Dependency records.
* Dependency relationships.
* Vulnerability records.
* Risk features.
* Model predictions.
* SHAP explanations.
* Scan results.

## Additional Features

The architecture was also expanded to include developer-oriented output rather than only raw analysis.

The dashboard is intended to provide:

* Overall repository risk.
* Dependency-level risk scores.
* Vulnerability details.
* Risk explanations.
* Priority ranking.
* Recommended actions.
* Historical scan information in later iterations.

## Key Observation

The dataset investigation changed the architecture from a simple vulnerability scanner into a multi-stage risk-analysis system.

The project therefore became:

```text
Data Collection
      +
Dependency Analysis
      +
Vulnerability Intelligence
      +
Feature Engineering
      +
Machine Learning
      +
Explainable AI
      +
Developer Dashboard
```

## Result

The primary datasets and external information sources were identified, and the final high-level architecture and ML stack were established.

The next step was to consolidate these decisions into the formal project proposal.

