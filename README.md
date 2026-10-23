# Development of a Web-Based SMS Spam Detection Application Using Machine Learning

A planned web application for checking SMS messages in English, Russian and Kazakh, explaining classifications and evaluating model quality separately for each language.

**Status: Initial Scaffold.**

No runnable application, measured model results, completed user research or supervisor review is claimed.

## Problem Statement

The project addresses the manual assessment of potentially unwanted or fraudulent SMS. The proposed application will classify a submitted message and explain which text features influenced the result, helping users interpret the prediction.

Language coverage, false positives, missed spam and the handling of personal information are central design concerns. The practical need for the proposed workflow remains to be validated through real user discussions or a substantive agreement with an actual client.

## Target Users

- People in Kazakhstan who receive SMS in English, Russian or Kazakh and want to check a message manually.
- Researchers and evaluators who need to compare classification results, explanations and errors by language.

These are proposed user groups; their needs have not yet been confirmed by project research.

## Aim and Expected Outcomes

The aim is to design, implement and evaluate a privacy-conscious web application for SMS spam detection using machine learning.

Expected outcomes are:

- A reproducible data preparation and annotation process for English, Russian and Kazakh, including deduplication, dataset splits and annotation-agreement checks.
- A comparison of Naive Bayes and Logistic Regression classifiers using TF-IDF features, reporting spam-class precision, recall and F1 on held-out data for each language.
- A multilingual application providing single-message and batch-file checks, a class label, probability, confidence level and influential-word highlights.
- History, statistics and an incorrect-result feedback workflow, with confirmed feedback used for evaluated, versioned retraining.
- Documented tests, error and threshold analysis, a reproducible containerized launch and a public demonstration.

These are final-project deliverables, not completed results.

## Project Scope

**In scope:** manually submitted SMS and batch files; EN/RU/KZ interface and evaluation; explanations; history and statistics without raw personal data; verified-feedback retraining; model versions; input validation, masking and rate limiting; testing and deployment.

**Out of scope:** automatic access to a phone inbox, carrier-level blocking, paid SMS gateways, guaranteed fraud prevention and collection of private messages without permission.

For the first pre-defense, the focus is evidence, analysis, requirements, architecture, key-scenario mockups, an evaluation plan and traceable team work. A complete application is not required at that stage.

## Current Development Status

The initial project scaffold consists of this README, privacy exclusions, a configuration example, a Pull Request template and empty data/model directory markers. Application code, research documents, diagrams, tests and CI workflows will be added through separate development tasks and reviewed Pull Requests.

Preparatory documents, diagrams, application source, tests and a CI draft are stored separately and have not yet been added to the repository. The YouTrack project has been created; task tracking and team access are being configured.  User research, ML experiments and substantive supervisor feedback remain unconfirmed.

## Team Members and Supervisor

**Group:** SE-2425.

**Supervisor:** Хармысов Чингис Аблайханович.

- Сабыров Санжар Әділбекұлы — **Sanzhar**, GitHub: `SanzharS1`.
- Серікқали Бекнұр Асланұлы — **Beknur**, GitHub: `serikkalibeknur`.
- Шаехов Рафаэль Рустамович — **Rafael**, GitHub: `rafaeldo7`.

### Official Leading Responsibilities

The following planned responsibilities follow the three official project justification documents.

| Participant | Data and Machine Learning | Web Application | Quality and Delivery |
|---|---|---|---|
| Sanzhar | Inference returning class, probability, confidence level and influential words; error analysis; participation in algorithm comparison and classification-threshold selection | Python/FastAPI REST API; database for check history; input validation and safe processing; rate limiting and personal-data masking | Docker, CI, public deployment and API integration tests |
| Beknur | Corpus search and preparation; cleaning, deduplication, analysis and splits; annotation and agreement checks; character n-grams for morphologically rich languages | React/TypeScript; SMS checker, influential-word highlights, batch-file checking, multilingual interface, responsive layout and accessibility | Documentation, final report assembly, usability studies, presentation and demo scenario |
| Rafael | TF-IDF training/evaluation pipeline; cross-validation; Naive Bayes and Logistic Regression training/comparison; hyperparameter tuning; held-out spam-class precision, recall and F1; model selection and versions | History and statistics behavior; incorrect-result feedback; retraining script using confirmed feedback | Test plan, unit and end-to-end tests, load testing and resilience to invalid or malicious input |

### Participation in Other Parts

- **Sanzhar:** preparation and cross-labeling of some messages, UI/API integration, data schema and feedback processing, report sections for his components and review of others' code.
- **Beknur:** feature experiments during algorithm comparison, agreement on the API contract and mock responses, history/statistics screens, component tests, clean-machine setup checks and report sections for his components.
- **Rafael:** verification of dataset splits and duplicates, review of explanation clarity on examples, the Results chapter and his technical sections, and review of backend, UI and deployment.

Each participant writes tests and documentation for their own components and assists with the others. Sanzhar coordinates the team and is the planned representative submitting the common form. Task-level refinements require agreement with the supervisor.

## Proposed Technology Stack

| Area | Planned Technologies |
|---|---|
| Data and ML | Python, scikit-learn, TF-IDF, Naive Bayes, Logistic Regression |
| Backend and storage | FastAPI, REST/JSON, PostgreSQL |
| Frontend | React, TypeScript |
| Delivery | Docker, GitHub Actions |

These choices remain subject to documented comparison and evaluation. The scaffold includes a placeholder configuration example in `.env.example`; dependencies, workflows and runtime configuration will accompany the implementation.

## Repository and Project Management Links

| Resource | Link or Status |
|---|---|
| GitHub repository | [SanzharS1/sms-spam-detection](https://github.com/SanzharS1/sms-spam-detection) |
| YouTrack project | [SMS Spam Detection — Diploma Project](https://sms-spam-se2425.youtrack.cloud) — setup in progress |
| Project documentation | **Pending** — drafts are stored separately; links will be added when reviewed materials enter the repository |

Each participant will develop their part through real YouTrack tasks, task branches, commits and Pull Requests reviewed by another teammate.

**First pre-defense deadline:** 24 October 2026, 18:00.

## Setup, Execution and Testing

**To be added when the runnable implementation is introduced.**

The current scaffold has no runnable code, dependency file or automated test workflow. Installation, execution and testing commands will be documented alongside the implementation.

Keep original personal documents, private SMS/interviews, credentials and local databases outside public Git. Use reviewed anonymized findings and synthetic demonstration inputs; `.env.example` must contain placeholders only.
