# Week 1 : Idea Selection and Project PPT

## Objective

The objective of the first week was to identify a suitable problem statement for the project and develop an initial understanding of the proposed solution.

The idea needed to satisfy three requirements:

* It should address a practical problem.
* It should provide sufficient scope for software development and machine learning.
* It should have publicly available data or external sources that could support development and evaluation.

## Initial Problem Exploration

The team explored possible problem domains before finalizing the project direction.

One of the areas considered was **software supply-chain security**. Modern applications depend heavily on open-source libraries and packages. A project may directly use a relatively small number of libraries while indirectly depending on a much larger dependency tree.

This creates a security problem because vulnerabilities in a transitive dependency can affect an application even when the developer did not explicitly select that package.

## Problem Statement

The main problem identified was that developers can receive a large number of dependency vulnerability alerts without having an effective way to determine which dependencies should be addressed first.

A vulnerability list alone does not necessarily represent practical risk.

For example, two dependencies may both have known vulnerabilities, but their actual priority may differ because:

* One dependency may be directly used by the application.
* Another may occur several levels deep in the dependency tree.
* One package may be actively maintained while another has been stale for several years.
* One package may have a high-severity vulnerability.
* One package may have multiple known vulnerabilities.
* The overall health of the package or its source repository may differ.

This led to the idea of building a system that performs **risk assessment and prioritization**, rather than simply producing a vulnerability list.

## Idea Selection

The project idea was finalized as:

**RiskTrace: An Explainable ML-Based Dependency Risk Assessment and Prioritization Platform for Software Supply Chains**

The intended objective of RiskTrace is to analyze a GitHub repository, identify its direct and transitive dependencies, match those dependencies against vulnerability information, and prioritize the resulting risks.

The project was also designed to include explainability so that a developer can understand why a dependency received a particular risk score.

## Initial Solution Direction

The initial concept consisted of the following stages:

```text
GitHub Repository
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

The machine-learning component was considered as a later stage rather than the starting point.

The initial development philosophy was to first establish a reliable dependency and vulnerability pipeline and only then introduce machine learning.

## Project Presentation

A project presentation was prepared to communicate:

* The software supply-chain security problem.
* Motivation for solving the problem.
* Proposed RiskTrace solution.
* Core system workflow.
* Machine-learning component.
* Explainable AI component.
* Proposed technology stack.
* Expected project outcomes.

The PPT helped convert the initial idea into a more structured project proposal and also helped identify which parts of the system would require further investigation.

## Key Observation

A major observation during this stage was that the project should not treat machine learning as the entire solution.

The dependency collection and vulnerability matching stages are fundamental. If dependency information or vulnerability matching is incorrect, an ML model cannot produce a reliable risk assessment.

Therefore, the project was planned as a layered system in which the basic security-analysis pipeline would be established before ML-based prioritization.

## Result

The software supply-chain security problem was selected as the project problem domain and the project was named **RiskTrace**.

An initial project presentation was prepared and the broad system workflow was established.

The next task was to investigate datasets and external security information sources that could support vulnerability analysis and risk modeling.

