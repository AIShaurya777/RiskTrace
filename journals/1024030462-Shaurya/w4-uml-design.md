# Week 4 : UML Design and System Modeling

## Objective

The objective of Week 4 was to convert the finalized RiskTrace architecture and workflow into formal UML and system-design diagrams.

The team worked on representing the major system components, actors, external services, data movement, and interactions involved in dependency-risk analysis.

The UML design was created based on the architecture and workflow finalized during the previous weeks.

---

## 1. UML Design Planning

Before creating the diagrams, the team reviewed the finalized RiskTrace workflow:

```text
GitHub Repository
        ↓
Dependency Collection
        ↓
Dependency Resolution
        ↓
Vulnerability Matching
        ↓
Risk Feature Engineering
        ↓
ML Risk Prioritization
        ↓
SHAP Explainability
        ↓
FastAPI
        ↓
React + Tailwind Dashboard
```

The UML diagrams were designed to represent this workflow from different perspectives, including user interactions, system components, and data movement.

---

# 2. Use-Case Diagram

The Use-Case Diagram was designed to represent how a developer interacts with RiskTrace and how the platform communicates with external services.

### Primary Actor

**Developer**

The developer is the primary user of RiskTrace.

The major interactions identified for the developer include:

* Analyze Repository.
* Collect Repository Data.
* Resolve Direct and Transitive Dependencies.
* Match Known Vulnerabilities.
* Build Dependency Risk Features.
* Predict and Rank Dependency Risk.
* View Prioritized Risk Dashboard.
* Inspect Dependency and CVE Details.
* View SHAP Risk Explanations.
* View Upgrade and Remediation Advice.
* Re-run Repository Scan.

### External Systems

The Use-Case Diagram also represents the external systems required by RiskTrace.

**GitHub REST API**

Provides:

* Repository contents.
* Repository metadata.
* Source and manifest information.

**deps.dev / OpenSSF Scorecard**

Provides information related to:

* Dependency relationships.
* Dependency graph information.
* Project health.
* Repository/package health indicators.

**OSV.dev / GitHub Advisory Database / NVD**

Provide security information such as:

* Vulnerability records.
* CVE/GHSA information.
* Severity information.
* Affected versions.
* Fixed-version information where available.

The diagram therefore establishes the interaction between the developer, RiskTrace, and the external services used for dependency and vulnerability intelligence.

---

# 3. Risk Analysis and Processing Components

The UML design also represented the major internal processing stages of RiskTrace.

The system performs the following logical operations:

```text
Repository Analysis
       ↓
Dependency Resolution
       ↓
Vulnerability Matching
       ↓
Risk Feature Construction
       ↓
Risk Prediction
       ↓
SHAP Explanation
       ↓
Prioritized Results
```

This provides a clear connection between the user's repository scan request and the final risk information presented by the system.

---

# 4. Developer-Facing Use Cases

The user-facing functionality was divided into several important interactions.

### Analyze Repository

The developer provides a repository for analysis.

### View Prioritized Risk Dashboard

The system presents the analyzed dependencies in a risk-prioritized manner.

### Inspect Dependency and CVE Details

The developer can inspect individual dependencies and associated vulnerability information.

### View SHAP Risk Explanations

The developer can view the factors that contributed to the predicted risk score.

### View Upgrade and Remediation Advice

The system provides potential actions such as upgrading an affected dependency to a fixed version where such information is available.

### Re-run Repository Scan

The developer can run the analysis again to obtain updated dependency and vulnerability information.

---

# 5. Relationship Between External Services and RiskTrace

The UML model represents RiskTrace as the central platform while external services provide supporting information.

```text
                  GitHub REST API
                         │
                         ▼
                  Repository Data
                         │
                         ▼
Developer ───────► RiskTrace Platform ◄────── deps.dev / Scorecard
                         │
                         │
                         ▼
                Security Data Sources
             OSV / Advisory / NVD
                         │
                         ▼
                 Risk Analysis
                         │
                         ▼
              Prioritized Risk Results
```

This representation helped clarify which information is generated internally and which information is obtained from external systems.

---

# 6. UML Design Consistency

The Use-Case Diagram was checked against the finalized architecture to ensure that the user interactions corresponded to actual planned system functionality.

For example:

* Repository analysis corresponds to the repository collector.
* Dependency resolution corresponds to the dependency resolver.
* Vulnerability matching corresponds to the vulnerability matcher.
* Risk prediction corresponds to the ML pipeline.
* SHAP explanations correspond to the explanation service.
* Dashboard interactions correspond to the React + Tailwind frontend.
* Repository and analysis information is supported by the FastAPI backend and PostgreSQL database.

This helped ensure consistency between the project proposal, architecture, and UML representation.

---

# Key Outcome

By the end of Week 4, the team had translated the finalized RiskTrace architecture into formal UML/system-design representations.

The diagrams helped define:

* The primary system actor.
* External systems and APIs.
* User interactions.
* Major RiskTrace operations.
* Dependency and vulnerability analysis flow.
* Risk prediction and explainability interactions.
* Developer-facing outputs.

The UML design provided a clearer blueprint for the implementation phase.

---

## Individual Contribution

### Use-Case Diagram

**My contribution:**
Worked on the **RiskTrace Use-Case Diagram**, identifying the primary actor, external systems, and major interactions supported by the platform. I mapped the Developer's interactions with RiskTrace, including repository analysis, dependency resolution, vulnerability matching, risk prediction, viewing the prioritized dashboard, inspecting CVE details, viewing SHAP explanations, receiving remediation advice, and re-running repository scans. I also incorporated the interactions with the GitHub REST API, deps.dev/Scorecard, and OSV/Advisory/NVD as external systems.

