# Week 3 : Project Report / Proposal Preparation

## Objective

The objective of Week 3 was to prepare the formal project report/proposal for **RiskTrace: An Explainable ML-Based Dependency Risk Assessment and Prioritization Platform for Software Supply Chains**.

The report consolidated the work completed during the previous weeks, including the finalized problem statement, datasets, system architecture, dependency-analysis workflow, machine-learning approach, explainability layer, technology stack, evaluation criteria, project scope, and risks.

The report was prepared as the formal technical documentation of the proposed system.

---

## 1. Consolidating Previous Work

The first step was to bring together the decisions made during the earlier stages of the project.

The report incorporated:

* The selected software supply-chain security problem.
* Motivation for dependency-risk prioritization.
* Selected datasets.
* Dependency collection approach.
* Vulnerability data sources.
* Final system architecture.
* Risk features.
* ML models.
* SHAP-based explainability.
* Web application architecture.
* Evaluation criteria.
* Project deliverables.
* Risks and mitigation strategies.

This helped convert the discussions and design decisions from the previous weeks into a single formal document.

---

## 2. Project Goal and Motivation

The report defined the primary goal of RiskTrace as helping developers identify and prioritize risks within software dependencies.

Instead of presenting vulnerabilities as a flat list, the proposed system aims to rank dependencies according to their overall risk and provide an explanation for the ranking.

The central idea was represented as:

```text
Dependency Information
        ↓
Vulnerability Information
        ↓
Risk Features
        ↓
ML-Based Risk Prediction
        ↓
Risk Prioritization
        ↓
SHAP Explanation
        ↓
Developer Action
```

---

## 3. Problem Statement

The report documented the major challenges associated with modern software supply chains.

These included:

* Large direct and transitive dependency trees.
* Increasing numbers of vulnerability alerts.
* Difficulty in prioritizing vulnerabilities.
* Dependence on raw severity scores.
* Manual effort required to analyze security reports.

The report emphasized that a dependency's risk may depend on more than its vulnerability severity.

Factors such as dependency depth, package staleness, maintenance activity, and repository health can provide additional context for prioritization.

---

## 4. Proposed RiskTrace Solution

The formal report described RiskTrace as a web-based dependency-risk assessment and prioritization platform.

The major components documented were:

### Dependency Collection

The system collects repository and dependency information using the GitHub API and deps.dev.

### Vulnerability Detection

Dependencies are matched against OSV.dev, with GitHub Advisory Database and NVD used for additional information where required.

### Risk Feature Engineering

Features are generated using vulnerability, dependency, freshness, maintenance, repository-health, and other relevant information.

### ML Risk Prediction

XGBoost is used as the primary model, with Random Forest and Logistic Regression used as comparison models.

### Explainability

SHAP is used to explain the factors contributing to individual risk predictions.

### Dashboard

A React + Tailwind CSS dashboard is planned to present risk scores, dependency rankings, vulnerability details, explanations, and recommendations.

---

## 5. Final System Workflow

The report documented the finalized end-to-end workflow:

```text
GitHub Repository
        ↓
Dependency Collection
(GitHub API + deps.dev)
        ↓
Direct + Transitive Dependency Analysis
        ↓
Vulnerability Matching
(OSV.dev + GitHub Advisory / NVD)
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

The workflow provided a clear connection between data acquisition, analysis, machine learning, explainability, and the developer-facing interface.

---

## 6. Technical Approach

The report documented the technical implementation planned for the system.

### Dependency Analysis

The system will identify direct and transitive dependencies and determine their versions and dependency-graph depth.

### Vulnerability Matching

Package versions will be checked against vulnerability sources to identify affected versions, vulnerability identifiers, severity information, and fixed versions.

### Feature Engineering

The planned risk features include:

* Vulnerability count.
* Maximum CVSS/severity.
* Dependency depth.
* Package age/staleness.
* Maintenance activity.
* Repository health.
* Complexity-related features where applicable.

### Machine Learning

The ML stack was finalized as:

* **XGBoost** — primary model.
* **Random Forest** — comparison model.
* **Logistic Regression** — comparison baseline.
* **Pandas + NumPy** — data processing.
* **Scikit-learn** — preprocessing and evaluation.
* **SHAP** — explainability.

---

## 7. Web Architecture

The report documented the planned three-layer application architecture.

### Frontend

React + Tailwind CSS will provide the developer-facing dashboard.

### Backend

FastAPI will handle repository analysis, API communication, analysis orchestration, ML inference, and database interaction.

### Database

PostgreSQL will store repository information, dependency information, vulnerability information, risk features, scan metadata, and generated risk results.

---

## 8. Evaluation Criteria

The report defined measurable targets for evaluating the completed system.

The primary proposed targets were:

* F1-score ≥ 0.80.
* ROC-AUC ≥ 0.85.

Additional targets included:

* ≥95% known-CVE matching accuracy.
* At least 80% of confirmed critical vulnerabilities appearing in the top-5 prioritized dependencies.
* 100% SHAP explanation coverage for flagged dependencies.
* Median scan time below 60 seconds for repositories with fewer than 200 dependencies.
* ≥99% successful scan completion during testing.

These were documented as **target evaluation criteria** for the future implementation and testing phase.

---

## 9. Project Scope and Deliverables

The report divided the planned work into initial and subsequent deliverables.

### Initial Deliverables

* GitHub repository analysis.
* Dependency extraction.
* Vulnerability matching.
* PostgreSQL integration.
* Basic dashboard.
* CI-based automation and testing.

### Subsequent Deliverables

* XGBoost-based risk prediction.
* Model comparison using Random Forest and Logistic Regression.
* SHAP-based explanations.
* Remediation recommendations.
* Dashboard history and filtering.
* Trend analysis.

---

## 10. Risks and Mitigations

The report also documented potential project risks.

| Risk                | Mitigation                                                    |
| ------------------- | ------------------------------------------------------------- |
| Data quality        | Cross-reference multiple security sources                     |
| Model reliability   | Compare multiple models and provide SHAP explanations         |
| Dataset limitations | Combine multiple public datasets and security sources         |
| Performance         | Cache dependency information and optimize database operations |

Documenting these risks helped establish that the project had considered practical implementation limitations before development began.

---

## 11. Report Review and Formatting

After the technical content was compiled, the complete project report was reviewed and formatted.

The review focused on:

* Logical ordering of sections.
* Consistency of technical terminology.
* Consistency between the architecture and written content.
* Correct representation of the ML pipeline.
* Dataset and security-source references.
* Section numbering.
* Heading hierarchy.
* Bullet-point formatting.
* Overall readability.
* Consistency in the presentation of the RiskTrace technology stack.

The final document was organized as a formal project proposal suitable for submission.

---

## Key Outcome

By the end of Week 3, the team had completed the formal **RiskTrace project report/proposal**.

The report brought together the project's problem definition, proposed solution, architecture, datasets, technical stack, ML methodology, explainability approach, evaluation criteria, deliverables, scalability considerations, and risks into a single document.

This provided the team with a formal technical reference before moving into detailed system design and UML modeling.

---

## Individual Contribution

This section can be customized by each team member.

**Contribution – Report Preparation:**
Contributed to preparing the formal RiskTrace project report by compiling the team's finalized technical decisions and organizing them into the required proposal structure.

**Contribution – Content and Technical Review:**
Reviewed and updated the technical content of the report, ensuring that the documented architecture, datasets, dependency-analysis workflow, ML stack, explainability approach, and evaluation criteria were consistent with the team's finalized design.

**Contribution – Formatting and Finalization:**
Worked on the formatting and final presentation of the complete report, including section organization, headings, numbering, bullet points, technical terminology, and overall document consistency.

