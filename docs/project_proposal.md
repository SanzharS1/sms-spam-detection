# Project Proposal

## 1. Project Identification and Status

| Field | Value |
|---|---|
| Project title | Development of a Web-Based SMS Spam Detection Application Using Machine Learning |
| Programme and group | Software Engineering, SE-2425 |
| Supervisor | Хармысов Чингис Аблайханович |
| Task | [DIP-3 — Define project proposal, problem statement and scope](https://sms-spam-se2425.youtrack.cloud/issue/DIP-3) |
| Assigned student | Sanzhar Sabyrov — Сабыров Санжар Әділбекұлы |
| Team | Сабыров Санжар Әділбекұлы; Серікқали Бекнұр Асланұлы; Шаехов Рафаэль Рустамович |
| Repository | [SanzharS1/sms-spam-detection](https://github.com/SanzharS1/sms-spam-detection) |
| Document date | 24 October 2026 |
| Status | Proposal draft; team and supervisor review pending |

This proposal defines the scope, objectives and evaluation approach for the system described in the [repository README](../README.md).

The published DIP-1 baseline contains the shared repository scaffold. Application development and evaluation are planned.

No runnable application, measured model results, completed user research or supervisor review is claimed.

User research under [DIP-2](https://sms-spam-se2425.youtrack.cloud/issue/DIP-2) remains incomplete. Target-user assumptions and evaluation targets are provisional pending research findings and review.

## 2. Executive Summary

The proposed system is a browser-based service for manually checking English, Russian and Kazakh SMS. A user will submit one message or a batch file and receive a spam/ham prediction, model-estimated spam probability, a documented confidence indication and highlights derived from influential model features. Planned history, statistics and an incorrect-result workflow will support review without retaining raw personal messages by default.

The initial technical approach combines a reproducible TF-IDF classification pipeline, Naive Bayes and Logistic Regression comparison, a FastAPI service and a React/TypeScript interface. Model quality will be evaluated on held-out data separately by language. Confirmed feedback may support controlled offline retraining and evaluated model promotion; it will not directly update a live model.

The intended contribution is a coherent, testable Software Engineering system integrating data preparation, evaluation, explanation, privacy and deployment. Analysis and design evidence will be assessed at the first pre-defense; implementation follows the phased delivery plan in Section 11.

## 3. Problem Statement

The project investigates a specific interaction: a person has an SMS they consider suspicious and wants to inspect its text through a browser without granting an application access to the phone inbox. The engineering problem is to provide a consistent classification-and-explanation workflow while managing input errors, uncertainty, language coverage and personal information.

There are two distinct classification errors: a legitimate message can be marked as spam, and spam can be missed. Their practical costs and acceptable trade-off must be investigated rather than assumed. A prediction must therefore be accompanied by understandable limitations, not presented as a guarantee that a message or link is safe.

The following are hypotheses to be tested through DIP-2 and the later review of literature and existing systems:

- Target users would find a manual web checker useful alongside their current practices.
- Reasons for a prediction would improve interpretation of the result.
- Separate evaluation for EN/RU/KZ is relevant to the intended Kazakhstan context.
- Users would accept the proposed processing and retention policy.

DIP-2 findings and the comparison of existing systems will determine whether these hypotheses are supported and where scope or acceptance criteria need revision.

## 4. Motivation and Relevance

The practical motivation is to investigate transparent manual checking in a multilingual setting. The academic motivation is to demonstrate an end-to-end engineering process: trace a user problem to requirements, compare technical alternatives, prepare data responsibly, evaluate a model, integrate it into a service and verify the resulting system.

DIP-2 is intended to establish local empirical relevance through 3–5 actual discussions with user representatives or a substantive agreement with an actual client, following the university criterion. Anonymized findings should identify useful scenarios, language needs, explanation expectations, error concerns and privacy preferences.

A separate critical literature review and comparison of existing systems will support the design rationale. Section 21 lists technical documentation supporting specific engineering choices.

## 5. Target Users and Stakeholders

| Group | Proposed interaction or interest | Evidence and boundary |
|---|---|---|
| Adult SMS users in Kazakhstan | Paste an EN/RU/KZ message, interpret the label and explanation, optionally report an incorrect result | Primary user hypothesis; validate through DIP-2; no inbox access required |
| Research or evaluation users | Submit permitted test batches and inspect errors, metrics and model versions | Secondary user hypothesis; scenarios to be validated |
| Team member acting as model/feedback reviewer | Validate feedback, run offline experiments and approve or reject a candidate model | Planned restricted operational role, distinct from the public checker |
| Supervisor | Review scope, methods, responsibilities and substantive deliverables | Substantive review pending |
| Pre-defense committee | Assess problem clarity, scope, engineering complexity and traceable evidence | Receives only accessible, public-safe or appropriately restricted materials |
| Dataset contributors or providers | Supply data under documented permission/licensing conditions | Availability and permitted uses must be verified before use |

The interface will present classification limitations in accessible language so users can interpret a prediction without knowledge of the ML implementation.

## 6. Overall Aim

To design, implement and evaluate a privacy-conscious web application that classifies manually submitted EN/RU/KZ SMS as spam or ham, returns model-based explanations and versioned predictions, and demonstrates reproducible per-language evaluation and tested integration across data, API, storage and UI components.

The aim will be assessed through working scenarios, reproducible artifacts and the evaluation criteria in Section 18. Model-quality targets will be established from evidence before final held-out evaluation.

## 7. Specific Objectives and Expected Evidence

Objectives O-01–O-08 connect planned results to acceptance evidence and leading responsibilities.

| Objective | Planned result | Completion evidence | Leading responsibility |
|---|---|---|---|
| O-01: Validate the problem and scope | Findings from DIP-2 linked to revised user scenarios and requirements | Real anonymized research records or client agreement; documented assumptions and revisions | Beknur coordinates research/documentation; all contribute within their parts |
| O-02: Justify the approach | Critical literature, existing-system and technology comparisons | Verified sources, consistent comparison criteria and decisions tied to requirements | Beknur assembles; each technical lead supplies their analysis |
| O-03: Prepare multilingual data | Provenance, preprocessing, annotation guide, agreement checks and reproducible splits | Dataset description, permissions, cleaning records, label review and overlap checks | Beknur; Rafael verifies splits/deduplication; Sanzhar participates in cross-labeling |
| O-04: Compare and version models | Naive Bayes and Logistic Regression classifiers using TF-IDF features, controlled tuning and selection | Experiment configuration, cross-validation results, held-out metrics and model metadata | Rafael; Beknur contributes feature experiments; Sanzhar participates in comparison/threshold analysis |
| O-05: Deliver inference and explanations | Label, probability, confidence indication, influential features and error/threshold analysis | Versioned inference contract, explanation examples and actual error-analysis report | Sanzhar; Rafael reviews clarity and Beknur implements displayed highlights |
| O-06: Integrate application workflows | API/UI, single and batch checking, private history/statistics and feedback | Agreed schemas, scenario demonstrations and component/integration checks | Sanzhar API/storage; Beknur UI; Rafael history/statistics/feedback behavior |
| O-07: Control feedback-based improvement | Verified-label retraining and candidate-model review | Label provenance, versioned training run and recorded promotion/rejection decision | Rafael; Sanzhar supports schema/feedback handling; Beknur provides UI |
| O-08: Verify and deliver the system | Tests, reproducible launch, deployment and defense materials | Actual test reports, setup verification, public demo and reviewed document pack | Rafael general testing; Sanzhar API tests/CI/Docker/deployment; Beknur UX/documentation/presentation |

## 8. Expected Deliverables and Responsibility Boundaries

The team will develop the following deliverables according to the official individual role justifications.

| Participant | Data and ML | Web application | Quality and delivery |
|---|---|---|---|
| Сабыров Санжар Әділбекұлы — Sanzhar Sabyrov, GitHub `SanzharS1` | Prediction module returning class, probability, confidence level and influential words; error analysis; participation in algorithm comparison and classification-threshold selection | Python/FastAPI REST API; database for check history; input validation and safe processing; rate limiting and personal-data masking | Docker, CI, public deployment and API integration tests |
| Серікқали Бекнұр Асланұлы — Beknur Serikkali, GitHub `serikkalibeknur` | Finding/preparing corpora; cleaning, deduplication, analysis and splits; annotation and agreement checks; character n-grams for morphologically rich languages | React/TypeScript checker, influential-word highlights, batch-file checking, multilingual interface, responsive layout and accessibility | Documentation, final unified report assembly, usability studies, presentation and demo scenario |
| Шаехов Рафаэль Рустамович — Rafael Shaekhov, GitHub `rafaeldo7` | TF-IDF training/evaluation pipeline; cross-validation; Naive Bayes/Logistic Regression training and comparison; hyperparameter tuning; held-out spam precision/recall/F1; model selection and versions | History and statistics behavior, incorrect-result feedback and a retraining script using confirmed feedback | Test plan, unit/E2E tests, load testing and invalid/malicious-input resilience |

Contributions across component boundaries are planned as follows:

- Sanzhar prepares and cross-labels some messages, connects UI to API, contributes to the data schema and feedback processing, writes his report sections and reviews others' code.
- Beknur experiments with features during model comparison, agrees API contracts and mock responses, presents history/statistics screens, writes component tests, verifies clean-machine setup and supplies his report sections.
- Rafael checks data splits and duplicates, reviews explanation clarity on examples, writes the Results chapter and his technical sections, and reviews backend, UI and deployment.

Each participant writes tests and documentation for their own components and assists with the others. Sanzhar coordinates this proposal and the common submission; Beknur leads report assembly. Task-level refinements require supervisor agreement.

The final deliverables will comprise prepared data and its documentation; a reproducible training/evaluation pipeline and model versions; inference and error analysis; API/storage/UI workflows; confirmed-feedback retraining; test reports and deployment; and the consolidated report, presentation and demonstration. Sanzhar's delivery will include Swagger documentation, a one-command launch and a public working URL.

## 9. Functional Scope

The intended application scenarios are:

1. Submit a single SMS and receive a label, model-estimated spam probability, classification threshold, confidence indication, model version and an explanation.
2. Inspect influential text fragments that correspond to actual model features; understand that the prediction may be wrong.
3. Submit a batch file and receive row-level results or specific validation errors without silently losing failed rows.
4. Select an EN/RU/KZ interface and see the model's actual supported-language limitations independently of UI language.
5. View permitted history and statistics for the current session or another explicitly authorized scope, without exposing another user's records.
6. Flag an incorrect result and, with separate consent where text is involved, propose a corrected label for review.
7. Allow an authorized reviewer to accept/reject feedback and run controlled offline retraining; evaluate a candidate before making it the active version.

Batch-file checking is part of the final scope, with CSV/UTF-8 proposed as the initial format. The requirements/API contract will define columns, size/row limits, invalid-row handling and response schemas before implementation acceptance.

## 10. Non-functional Scope

| Concern | Intended quality constraint | Required later verification |
|---|---|---|
| Privacy | Process submitted text transiently by default; no raw personal messages in history, ordinary logs or public artifacts | Review storage/logging schemas, consent/redaction and deletion tests |
| Safe processing | Bound text/file sizes and request frequency; validate payloads; handle failures without exposing input or internal details | Negative API/batch tests, rate-limit checks and error-response inspection |
| Reproducibility | Record data/split provenance, seeds, dependency versions, preprocessing, features, model and threshold | Repeat the documented training/inference process in a clean environment |
| Performance | Define single/batch workloads, hardware, concurrency, timeouts and latency/error targets before load acceptance | Measure latency distributions, throughput and errors under the stated conditions |
| Accessibility and usability | Keyboard operation, labelled controls, readable states, responsive layouts and usable explanations | Component/accessibility checks and actual usability observations |
| Maintainability | Explicit component contracts and separate training/inference paths | Code review, contract tests, version metadata and change traceability |
| Operational consistency | Deploy the evaluated artifact with compatible preprocessing and API behavior | Startup checks, model-loading validation, integration tests and recorded deployment version |

Workload limits and targets for latency, request rate, classification quality and availability will be documented and agreed before acceptance testing.

## 11. In-scope Functionality and Delivery Sequence

The final project includes all workflows in Section 9, multilingual data/evaluation, faithful explanations, safe history/statistics, verified-feedback retraining, tests and reproducible deployment. The delivery sequence phases these requirements while retaining the final scope and responsibility boundaries in Section 8.

The proposed sequence is: agree evidence and contracts; prepare data and an English demonstrator; compare/evaluate models; integrate inference/API/UI and storage; implement batch/history/feedback; extend and validate RU/KZ coverage; verify retraining and deployment. Data preparation, UI design and evaluation planning can proceed in parallel. Public language-support claims are added only when the corresponding data and evaluation exist. Later-stage dates require supervisor agreement.

## 12. Out-of-scope Functionality

- Automatic access to a phone inbox or background interception of messages.
- Carrier integration, automatic carrier-level blocking or paid SMS gateways.
- Guaranteeing fraud prevention, the safety of a URL or the authenticity of a sender.
- Opening message links, fetching their content, executing attachments or performing malware analysis.
- Training a new foundation model or demonstrating a novel classification algorithm.
- General support for languages beyond EN/RU/KZ, or guaranteed classification of every transliterated/mixed-language form.
- Unreviewed online learning from public feedback, or collecting private SMS without permission.
- A production-scale multi-tenant analytics platform with enterprise availability commitments.

These boundaries keep the project focused on a manually submitted text-classification service and its evaluation. Any extension will require an explicit scope decision.

## 13. Engineering and Technical Complexity

The engineering complexity arises from maintaining consistent, verifiable contracts across data, model, API, storage and UI components. A baseline stack and phased integration plan are intended to keep the work feasible for three students.

- **Data and language boundaries:** annotation policy, class imbalance, duplicate campaigns and mixed-language records must be handled consistently across preparation, splits and evaluation. Kazakh morphology and script variation require explicit feature and evaluation decisions.
- **Model assessment:** fair NB/LR comparison requires controlled splits and training-only fitting/tuning. Aggregate accuracy cannot serve as the project's sole success measure; errors and spam-class metrics are examined separately by language.
- **Explanation fidelity:** character features must be mapped back to visible text without inventing reasons or changing their meaning. The displayed explanation and confidence indication need a defined relationship to the actual model and validation evidence.
- **System integration:** request validation, batch errors, inference, versioned responses, persistence, UI state and failure handling must remain compatible when the model changes.
- **Feedback and privacy:** history must avoid raw personal text, whereas text-based retraining requires usable, permitted examples. Explicit consent, reviewed redaction, label confirmation and restricted access are therefore design dependencies.
- **Verification and operation:** tests, CI, artifact compatibility and repeatable deployment must establish that the evaluated system is the one demonstrated.

The work belongs to Software Engineering because it requires requirements traceability, architecture and data design, component contracts, implementation, automated and user-facing verification, configuration/version management and delivery. Experiments are one component of that engineered system.

## 14. Main Technical Approach and Intended Architecture

The intended flow is browser UI -> FastAPI REST service -> compatible preprocessing and versioned inference -> structured result. PostgreSQL is the planned store for permitted history metadata, review status and feedback; deployment is intended to use Docker and GitHub Actions. The technology comparison will justify these choices against the project requirements.

**Data and training:** Beknur leads data preparation and character-feature experiments; Rafael integrates TF-IDF and the NB/LR classifiers into the training/evaluation pipeline. Word and character configurations will be compared using the same validation protocol. Character n-grams are a supported text representation; their suitability for the proposed data will be assessed experimentally. See [scikit-learn text feature extraction](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction).

**Leakage control:** keep learned preprocessing and feature extraction inside each training/CV pipeline. Validation/test records must not participate in vocabulary/IDF fitting, hyperparameter selection, threshold selection or calibration fitting. This design follows the [scikit-learn guidance on data leakage and pipelines](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage).

**Inference and explanation:** Sanzhar leads a stable response contract covering label, probability, threshold, confidence, influential features and version. For the selected classifier, the explanation method should use genuine feature contributions and document any aggregation into displayed fragments. Explanations should reflect actual model contributions rather than a fixed suspicious-word list. The interpretation of probabilities as confidence will require validation/calibration and consistent UI wording. See [scikit-learn probability calibration](https://scikit-learn.org/stable/modules/calibration.html).

**Web integration:** Sanzhar leads API/persistence and safeguards; Rafael leads history/statistics/feedback behavior; Beknur leads their UI. REST contracts will specify input/output, failure cases, batch handling and model metadata. Offline training must be separate from public prediction requests. An operator's ability to verify feedback or promote models must not be available to ordinary public users.

**Version lifecycle:** record data/split, feature/preprocessing, estimator, threshold and explanation compatibility with each model. A candidate is evaluated against the agreed baseline and reviewed before promotion. Preserve the previous working version and a documented rollback procedure.

## 15. Multilingual EN/RU/KZ Considerations

The proposed data plan starts with verification of an English corpus such as UCI SMS Spam Collection; source, license, actual records and encoding must be checked before use. RU/KZ collection, permissions, annotation and agreement remain dependencies. An English-only demonstrator does not establish RU/KZ quality.

Preparation should preserve Unicode and language-relevant characters, document normalization, identify duplicate/near-duplicate groups and record uncertain or mixed-language labels. Character n-grams will be investigated for spelling and morphological variation, with their performance evaluated separately by language. Annotators need clear spam/ham definitions, independent cross-labeling on an agreed subset and recorded resolution of disagreements.

A pooled multilingual model versus language-specific models is an unresolved experimental decision. Model routing and the treatment of uncertain/mixed-language input must be specified before claiming multilingual support. The UI should disclose unsupported or unevaluated cases. Choosing a UI language must not silently assert that the classifier has been evaluated for that language.

Use duplicate-group-aware, approximately class/language-balanced splits where data permits; preserve an untouched held-out set. Report EN/RU/KZ sample counts, spam precision/recall/F1 and confusion matrices separately. Define how mixed-language records are reported without double-counting. Insufficient examples or missing classes must be disclosed; missing measurements must not be replaced by assumed or translated-English scores.

## 16. Privacy and Security Approach

- **Transient checking:** do not persist submitted text in normal history or application logs by default. Process text as untrusted data; do not follow links or execute content. Escape/render output as text in the UI.
- **History:** prefer prediction identifiers, time, label, score and model version within an explicitly authorized scope. Session identifiers do not by themselves make a record anonymous; access, retention and deletion require design and tests.
- **Feedback for training:** distinguish a metadata-only error report from a contribution of text. Retaining a text example requires separate informed consent and review/redaction before a confirmed label can enter a training dataset. A hash of a message alone cannot replace its text features for this pipeline.
- **Masking and feature consistency:** define which transformation happens before inference and which happens before storage. Apply compatible training/inference preprocessing and assess the effect of masking. Redaction alone is not a guarantee of anonymity.
- **Restricted operations:** authorize feedback review, data export and model promotion; ordinary users must not see others' history or approve their own unverified labels for training.
- **Service safeguards:** validate text and file structure, bound request/file sizes, apply rate limits/timeouts and define safe error responses. Specify privacy-conscious client identification and retention for rate limiting. Use HTTPS for deployment and keep credentials in deployment configuration rather than source control.
- **Public artifacts:** exclude original personal documents, identifiable interviews, raw private SMS, secrets and unintended training text embedded in artifacts. Demonstrations should use synthetic examples. Human privacy review is still required before treating contributed/redacted text as suitable for training or publication.

Consent wording, retention periods, session/access design, masking policy and workload limits require agreement by the relevant owners and review.

## 17. Risks, Assumptions, Dependencies and Limitations

Risk levels below are qualitative planning judgments.

| Risk or assumption | Consequence | Mitigation / dependency | Responsible lead |
|---|---|---|---|
| DIP-2 has not established demand or usable scenarios | Scope may solve an unverified problem | Use real findings to confirm or revise users, explanations and privacy needs | Beknur coordinates research; Sanzhar coordinates scope |
| RU/KZ data or permitted uses are insufficient | Three-language quality cannot be demonstrated | Verify sources/permissions, annotation and counts; disclose missing coverage and agree the recovery plan | Beknur; Rafael evaluates feasibility |
| Duplicate leakage, weak labels or class imbalance | Misleading results and error trade-offs | Group/label review, protected test splits, training-only tuning, per-class/per-language reports | Beknur preparation; Rafael evaluation |
| Confidence/explanations are misleading | Users over-trust the result | Validate score interpretation, feature mapping and explanation clarity; document uncertainty | Sanzhar; Rafael reviews; Beknur tests UI comprehension |
| History and feedback retain personal information | Privacy exposure or unusable training data | Agree consent/redaction/retention/access and test them; no default raw-text retention | Sanzhar storage/privacy; Rafael feedback; Beknur consent UI |
| Unverified feedback changes model behavior | Poisoned labels or quality regression | Human confirmation, versioned offline training, evaluation and promotion gate | Rafael; Sanzhar supports operational controls |
| API/model/UI contracts diverge | Broken integration despite isolated component checks | Agree schemas/mock responses early, retain version metadata, run integration/E2E tests | Sanzhar API; Beknur UI; Rafael behavior/tests |
| Scope or time exceeds team capacity | Missing required evidence or incomplete final features | Prioritize first-stage evidence; phase implementation without dropping official roles; escalate unresolved scope decisions to supervisor | Sanzhar coordinates; all own deliverables |
| Claims or review links lack evidence | Pre-defense criteria remain unfulfilled | Link claims to source evidence and document substantive review and revisions | All; Beknur assembles documents |

The main dependencies are: DIP-2 findings -> requirements and UX; data permissions/annotation -> valid splits and experiments; model selection/version -> inference/explanations; API/schema -> UI/history/feedback; confirmed permitted examples -> retraining; actual verification -> deployment/results; team/supervisor review -> approved scope.

## 18. Project Success and Evaluation Criteria

The following proposed acceptance criteria will be refined in the requirements and verification plans. Numerical quality thresholds remain subject to agreement with the supervisor before final held-out evaluation.

| Area | Proposed acceptance evidence | Decision still required |
|---|---|---|
| Problem relevance | Real DIP-2 records distinguish findings from assumptions and identify changes to requirements | Confirm target users, priority scenarios and limits of the sample |
| Data readiness | Provenance/license and annotation policy documented; agreement measured; duplicate groups kept out of conflicting splits | Sampling/annotation size, agreement method/acceptance and exact split policy |
| Classification | Reproducible NB/LR comparison on common splits, a declared simple baseline, held-out spam precision/recall/F1, support counts and confusion matrices for each supported language | Model/threshold selection rule and required improvement/error trade-off, fixed before inspecting final test results |
| Explanation and confidence | Response corresponds to the evaluated model; highlighted fragments trace to features; score/confidence mapping documented and reviewed on examples | Explanation method, aggregation policy, calibration/confidence criteria and UX acceptance |
| Functional integration | Single SMS, batch errors/results, languages, permitted history/statistics and feedback pass agreed scenarios | Detailed API/UI test cases, input/file limits and authorization model |
| Privacy and security | Tests show no default raw-text persistence in history/logs, no cross-user access, bounded invalid input and restricted feedback/model operations | Consent, masking, retention/deletion, rate policy and threat-focused test cases |
| Performance and usability | Report p50/p95 latency, throughput/errors and user task observations under declared conditions | Hardware/workloads/concurrency and performance/UX targets before acceptance testing |
| Reproducibility and delivery | Clean-machine setup, one-command container launch, actual CI/API/E2E reports, versioned model and public demonstration | Supported environment, hosting/access and operational review |

The proposed evaluation sequence is:

1. Record data provenance, labels, duplicates, language/support counts and permissions; reserve a held-out test set before feature/model decisions.
2. Compare a declared simple baseline and the NB/LR pipelines using training-only cross-validation/validation. Fit learned preprocessing only on the relevant training fold; choose hyperparameters, calibration and decision thresholds without test-set access.
3. Freeze the selected pipeline and evaluate on the held-out set under the recorded conditions. Report limitations and uncertainty appropriate to sample size; do not claim reliable language coverage when data is insufficient.
4. Analyze false positives and false negatives using at least five redacted examples where available; report the actual number examined while protecting message privacy.
5. Run component/unit, API integration, E2E, invalid/adversarial-input, privacy/access, load and UX checks under their respective owners. Record actual outcomes, failures and limitations.
6. For future confirmed-feedback updates, version the new data/model and use a separate validation/promotion protocol. Do not repeatedly tune against the original final test set while presenting it as untouched evidence.

Rafael leads model/general-test evaluation; Sanzhar leads error/threshold analysis, inference and API integration checks; Beknur leads data/annotation, component and usability evidence. Their collaborations follow Section 8.

## 19. First Pre-defense Deliverables versus Future Implementation

The first pre-defense deadline is 24 October 2026, 18:00. Later implementation and defense dates will be agreed with the supervisor.

| Stage | Intended evidence | Current status |
|---|---|---|
| DIP-1 baseline | Shared scaffold in the repository | Published; does not contain application/research deliverables |
| DIP-3 / official section 1 | Clear proposal, users, aim/objectives, outputs, realistic scope and engineering complexity | Draft awaiting team and supervisor review |
| Remaining first-stage sections | Relevance evidence; critical literature; system/technology comparisons; verifiable requirements; three diagrams with sources/exports; key-scenario prototype; evaluation plan; actual project/risk traceability; substantive supervisor comments and revisions | Separate tasks requiring evidence and review; DIP-2 is incomplete |
| Final diploma implementation | Evaluated EN/RU/KZ system, inference/explanations, batch/history/statistics/feedback, confirmed-feedback retraining, tests, Docker/CI/public launch and final report/presentation | Planned for subsequent implementation and evaluation |

For the remaining first-stage work, retain the official quantitative criteria: 12 meaningfully used sources including at least 8 scientific publications; 3–5 relevant systems against 6–10 consistent criteria; and at least 3 technical decisions with 2–3 reasonable alternatives each. The required diagrams are System Context, Use Case and Component (draft). A complete application is not required for the first pre-defense.

Submission arrangements, including the unified report PDF and separate tracker-screenshot PDF, must be verified against the official form. Beknur leads report assembly; Sanzhar is the planned team representative for submission.

Requirements, architecture, UX and verification deliverables should maintain the following traceability: map final-scope items to FR/NFR and acceptance tests; keep diagram components and API/storage responsibilities consistent with Section 8; cover all public workflows in UX; align model/threshold/version information with the evaluation protocol; and keep privacy constraints compatible with history and confirmed-feedback training.

## 20. Conclusion and Review Gate

The proposed multilingual text-checking system connects data preparation, fair evaluation, explainable inference, safe web workflows and reproducible delivery. Its scope and phased implementation reflect the official leading and secondary responsibilities of the three team members.

Team and supervisor review will assess problem clarity, scope realism, engineering complexity and the proposed acceptance criteria, and resolve outstanding API, data, privacy and evaluation choices. DIP-2 findings may lead to revisions of the problem definition. The proposal and subsequent requirements will be updated in response to research findings and substantive review; approval remains pending.

## 21. References and Supporting Documentation

The project scope and responsibilities are based on the university's first pre-defense requirements and the individual role justifications of the three team members.

The following technical documentation supports the proposed machine learning approach:

- [Scikit-learn: Text Feature Extraction](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction) — text representation and character n-gram features.
- [Scikit-learn: Common Pitfalls](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage) — prevention of data leakage during training and evaluation.
- [Scikit-learn: Probability Calibration](https://scikit-learn.org/stable/modules/calibration.html) — evaluation and calibration of predicted probabilities.

A separate literature review will provide a critical analysis of relevant scientific publications and existing research approaches.
