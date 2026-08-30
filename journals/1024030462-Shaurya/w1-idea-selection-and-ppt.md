# Week 1 : Idea Selection and Project PPT

## Objective

The objective of the first week was to identify and finalize a suitable project problem for the semester project and prepare an initial presentation describing the selected idea.

The team evaluated different problem domains and considered factors such as practical relevance, availability of data, technical feasibility, scope for machine learning, and the possibility of developing a complete working system within the project timeline.

## Problem Domain Exploration

The team explored several possible problem areas before selecting the software supply-chain security domain.

During the discussion, the team focused on the increasing dependence of modern software applications on open-source packages and libraries.

A single application may directly depend on a limited number of packages while indirectly pulling in a much larger number of transitive dependencies.

This creates a potential security problem because vulnerabilities in a transitive dependency can affect the application even when the developer did not explicitly add that dependency.

## Problem Identification

The team identified that simply detecting vulnerabilities is not always sufficient.

A repository can contain multiple vulnerable dependencies, but all vulnerabilities may not have the same practical priority.

For example, risk can depend on factors such as:

* Vulnerability severity.
* Number of vulnerabilities associated with a package.
* Dependency depth.
* Whether the dependency is direct or transitive.
* Package age and staleness.
* Maintenance activity.
* Repository/project health.

This led to the idea of developing a system that would not only detect vulnerable dependencies but also **prioritize their risk**.

## Finalized Project Idea

The team finalized the project:

**RiskTrace: An Explainable ML-Based Dependency Risk Assessment and Prioritization Platform for Software Supply Chains**

The primary objective of RiskTrace is to analyze a GitHub repository, identify its direct and transitive dependencies, detect known vulnerabilities, and generate a prioritized dependency-risk assessment.

A major focus of the project is explainability.

Instead of providing only a numerical risk score, the system is intended to explain the factors responsible for the score using SHAP-based explanations.

## Initial System Concept

The initial workflow discussed by the team was:

```text
GitHub Repository
        ↓
Dependency Collection
        ↓
Dependency Analysis
        ↓
Vulnerability Detection
        ↓
Risk Assessment
        ↓
Risk Prioritization
        ↓
Developer Dashboard
```

The team decided that dependency collection and vulnerability detection should form the foundation of the system before introducing the ML component.

This approach allows the basic analysis pipeline to be verified before adding risk prediction.

## Initial Technology Discussion

The team discussed the major technologies that could be used for the project.

The initial technology direction included:

* GitHub API for repository information.
* deps.dev for dependency information.
* OSV.dev and other vulnerability databases for security information.
* Python for data processing and analysis.
* Machine-learning models for risk prioritization.
* SHAP for explainability.
* PostgreSQL for persistent storage.
* FastAPI for backend services.
* React for the frontend dashboard.

These technologies were considered based on their suitability for the planned architecture and availability of existing APIs and libraries.

## Project Presentation

After finalizing the idea, the team prepared a project PPT.

The presentation was used to communicate:

* The software supply-chain security problem.
* Motivation behind the project.
* Existing challenges in dependency management.
* Proposed RiskTrace solution.
* Major system components.
* Initial workflow.
* Machine-learning approach.
* Explainable AI component.
* Proposed technology stack.
* Expected outcomes.

The PPT helped the team organize the project idea and identify the components that required further investigation.

## Key Design Decision

One of the important decisions made during this week was to treat **risk prioritization** as the main objective rather than limiting the project to vulnerability detection.

The intended transformation was:

```text
Vulnerability Detection
        ↓
Risk Assessment
        ↓
Prioritization
        ↓
Explanation
        ↓
Developer Action
```

This became the central idea behind RiskTrace.

## Result

By the end of Week 1, the team had:

* Selected the software supply-chain security problem.
* Finalized the RiskTrace project idea.
* Defined the initial problem statement.
* Established the initial system workflow.
* Discussed the major technical components.
* Prepared the initial project PPT.

The next step was to investigate suitable datasets and external security-information sources and use these findings to finalize the technical architecture.

## Individual Contribution

Each team member can add their own contribution below.

**My contribution:**
Participated in the problem-domain discussions, helped refine the RiskTrace idea and its objectives, contributed to the problem statement and workflow, and participated in preparing and reviewing the project PPT.

