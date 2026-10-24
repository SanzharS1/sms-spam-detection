# Technology Comparison: Backend, Data Storage and Frontend

## 1. Purpose and evaluation basis

This comparison examines backend frameworks, data storage technologies and frontend alternatives for the multilingual SMS application defined in the [Project Proposal](project_proposal.md), particularly Sections 8–18. It evaluates how the alternatives support API contracts, Python inference, privacy, data integrity, multilingual interaction and maintainable deployment.

The intended system accepts manually submitted English, Russian and Kazakh SMS, returns versioned predictions and explanations, and supports batch checking, private history, statistics and reviewed feedback. The [existing-system comparison](existing_systems.md), especially Section 6, reinforces the need to distinguish these workflows and to assess privacy by data flow rather than by technology name.

The method is a qualitative comparison of official technical documentation consulted on 24 October 2026. Each matrix applies the same criteria to all three alternatives. Documented capabilities are cited; assessments of suitability and integration effort are project-specific engineering judgments. No numerical ranking is assigned because workload measurements and comparable development-time observations are unavailable. Backend deployment, database implementation, load-test results and infrastructure costs are not established by this study.

The principal decision criteria are:

- A clear REST/JSON contract for single-message and batch results, validation errors, explanations and model versions.
- Compatibility with Python/scikit-learn inference and a separate offline training pipeline.
- No default persistence of raw personal SMS in history or logs; authorized access to history and restricted feedback review.
- Reliable relationships between predictions, model versions, feedback and permitted training contributions.
- Manageable deployment, testing and maintenance for three students with distinct component responsibilities.

These criteria derive from the proposal rather than a completed FR/NFR specification. Request limits, latency targets, retention periods and the access model still require agreement before implementation acceptance.

## 2. Backend alternatives

### 2.1. Comparative matrix

FastAPI, Flask and Django with Django REST Framework (DRF) are reasonable alternatives because all can expose Python-based HTTP services. The comparison concerns their application-development responsibilities, not the quality of the classifier.

| Criterion | FastAPI | Flask | Django with DRF |
|---|---|---|---|
| REST API development | Typed endpoint declarations and OpenAPI support suit an API consumed by a separate UI. Persistence remains a separate integration choice. [F1] | A small routing core supports an explicit service design; an API schema and consistent error conventions need additional application code or extensions. [L1] | Serializers, views, viewsets and routers support resource-oriented APIs; Django conventions introduce a larger application structure. [D1], [D2] |
| Request and response validation | Pydantic-based input validation and declared response models support structured contracts. Domain rules and privacy filtering must still be specified. [F1], [F4] | Validation and serialization libraries must be selected and applied consistently; the core intentionally leaves such choices open. [L1] | Serializers provide field and cross-field validation and output representations. They must be invoked and configured correctly. [D2] |
| Python/scikit-learn integration | A Python inference module can be called behind the endpoint contract; asynchronous routing does not make model computation asynchronous. [F2] | A Python view can call the same inference module. The core has no requirement to move training into request handling. [L1], [L2] | A custom API view can call the same module independently of ORM-backed resources. The inference contract still requires project code. [D1] |
| Security and privacy | Security dependencies provide building blocks; history ownership, restricted review, masking and rate limits require explicit implementation. [F1] | Security and resource-limit configuration are documented; authorization, API validation and privacy controls need deliberate composition. [L3] | Permission policies are available, but object checks do not automatically filter list endpoints. History queries and feedback permissions require explicit rules. [D3] |
| Latency and concurrency | ASGI-oriented concurrency can accommodate I/O waits. CPU-intensive inference needs bounded execution and measured worker capacity; no speed advantage is demonstrated here. [F2], [F3] | Conventional WSGI execution is suitable for bounded synchronous calls. An async view still occupies a worker; adding async does not establish higher request throughput. [L2] | Inference, queries, serialization and server configuration determine observed latency. Generic API machinery is useful, but does not establish a workload-specific performance ranking. [D1], [D2] |
| API documentation and testing | OpenAPI and interactive documentation support contract review; TestClient supports API tests with pytest. [F1], [F5] | The documented test client supports request tests; API documentation/schema tooling must be agreed separately. [L1], [L4] | A browsable API and APIClient support inspection and request tests; schema-documentation tooling remains a configuration decision. [D1], [D5] |
| Ecosystem and persistence | Validation, dependency injection and database integration can remain modular; the team must select persistence and migration tools. [F1] | Extension freedom permits a small stack, but compatibility and consistent conventions become team responsibilities. [L1] | ORM-aware serializers integrate well with Django resources. This is attractive when model-backed administration dominates the application. [D1], [D2] |
| Hosting and deployment | An ASGI server, HTTPS termination, restart policy and worker/resource configuration are needed. Model memory must be considered per process. [F3] | Production requires a suitable WSGI server or hosting platform rather than the development server. [L5] | Deployment requires a configured Django environment, protected secrets, disabled debug output and HTTPS; using the framework does not replace operational review. [D4] |
| Maintainability | A distinct inference service and typed boundary suit the proposed architecture; database, authorization and model-lifecycle code still need modular design. | A minimal initial structure is flexible, but independent choices for schemas, errors and persistence increase the conventions to maintain. | Shared Django conventions can reduce variation across CRUD resources; the team must maintain the framework/DRF configuration and avoid coupling model inference to views. |
| Development complexity and team fit | Matches Sanzhar's officially assigned FastAPI responsibility. Contract design, ASGI operation and security remain practical learning and verification tasks. | A small first endpoint is straightforward; reaching the same validated, documented and protected API requires additional composition. | Stronger fit if extensive account/admin and resource-management features become central; learning the broader conventions is less directly justified by the current scope. |

### 2.2. Advantages, limitations and applicability

**FastAPI** offers a close match to the proposed separation between React/TypeScript and a Python API. Its main advantage here is a common definition of request/response structures that can support documentation and integration tests. Response models can constrain exposed fields, but they do not determine which data is appropriate to retain or disclose. [F1], [F4] The limitation is that persistence, consent handling, authorization and operational safeguards remain application responsibilities. It is suitable for the present prediction-oriented service if those responsibilities are designed explicitly.

**Flask** is a credible choice for a compact inference service with a deliberately small routing layer. Its flexibility is valuable when the team already has agreed libraries and application conventions. For this project, however, validation, API documentation and persistence would need additional integration decisions. [L1] That increases the coordination required to keep single-message, batch and feedback contracts consistent. Flask is not rejected as incapable or inherently too slow; it is less aligned with the already assigned framework and the requirement for a structured, documented API.

**Django with DRF** provides a coherent option for an application organized around persistent resources and permission policies. Serialization supports both ORM and non-ORM data, so scikit-learn integration is feasible. [D1], [D2] Its benefits would become more compelling if a substantial administrative interface or extensive account management were required. The current scope does not establish those needs. Introducing the broader stack would require justification against the smaller prediction service, while still implementing the same privacy and model-lifecycle rules.

### 2.3. Preferred backend and performance implications

**FastAPI is the preferred backend for the proposed implementation.** The decision rests on typed API contracts, direct Python integration, documented testing support and alignment with Sanzhar's official responsibility. It is a design choice rather than a measured performance conclusion.

Asynchronous execution can overlap waiting for compatible I/O operations; it does not shorten CPU computation automatically. Blocking inference must not simply be called inside an asynchronous endpoint without an execution strategy. A synchronous endpoint or bounded offloading is a candidate starting point; worker/process decisions require profiling. Multiple workers can also multiply loaded-model memory. [F2], [F3] Offline training and model promotion should remain outside public prediction requests.

Later performance evaluation should declare the model/artifact version, hardware, process count, request lengths, batch sizes, concurrency, database location and error rate. It should separate preprocessing/inference time from persistence and end-to-end latency, report p50/p95 latency and throughput, and distinguish startup from warm requests. Targets must be agreed before acceptance testing. No benchmark figures or fastest-framework claim follow from this comparison.

## 3. Data storage alternatives

### 3.1. Required information and privacy boundary

The application needs structured records, not a public archive of submitted SMS. Proposed prediction metadata includes an opaque prediction identifier, authorized session/owner scope, timestamp, label, score, threshold and model/preprocessing version. Language metadata must distinguish a reviewed or estimated message language from the selected UI language. History should omit raw message text, sender numbers, full URLs and text-bearing explanations by default.

Feedback metadata can reference a prediction, a proposed correction and a review decision. A retained text contribution is a separate, access-restricted record requiring informed consent, privacy review and label confirmation before training admission. Metadata-only feedback is useful for workflow tracking but cannot reconstruct the missing text features. These boundaries follow Proposal Sections 14–16 and preserve the distinction between ordinary history and permitted training data.

### 3.2. Comparative matrix

| Criterion | PostgreSQL | SQLite | MongoDB |
|---|---|---|---|
| Prediction history without default raw text | Typed rows suit a small, explicit metadata schema; constraints can reject invalid labels and missing version references. [P1] | A local SQL schema can represent the same metadata. Simplicity is attractive for a small, single-service demonstrator. [Q1], [Q3] | Prediction documents can store the same fields; validation rules must be configured to control types and permitted structure. [M1] |
| Statistics and query patterns | SQL aggregates support counts by label, period and model version, with authorized scope applied before aggregation. [P4] | SQL-based reporting is a reasonable fit for modest local data; concurrency and access must be handled by the service. [Q1], [Q2] | Aggregation pipelines support grouping and computed results; query and document design should follow the intended access patterns. [M5], [M6] |
| Feedback and model-version relationships | Foreign keys and transactions suit prediction-to-model and feedback-to-prediction relationships. Consent/text records can be separated from ordinary history. [P1], [P2] | Foreign keys and transactions support related records, but foreign-key enforcement must be enabled and verified for each connection. [Q2], [Q3] | Embedding may simplify related updates; separate references require application logic to preserve referential integrity. [M2], [M6], [M7] |
| Integrity and atomic changes | Primary/foreign keys, uniqueness and checks support explicit invariants; transactions can group related changes. [P1], [P2] | Transaction isolation is available; SQLite is not limited to non-transactional or disposable data. Constraint configuration still matters. [Q2], [Q3] | Single-document operations are atomic; multi-document transactions are supported on suitable replica-set/sharded deployments. Standalone deployments do not support them. [M2], [M4] |
| Access control and security | Privileges and optional row-level policies can supplement API authorization. Row security is not enabled automatically, and owner/superuser bypass must be considered. [P3] | Access protection depends on application authorization and protection of the database files; an embedded database is not a separate access-control service. [Q1] | Authentication, role-based access, network restrictions and transport protection require configuration. Ordinary users should access data through the API. [M3] |
| Concurrent operation and latency | MVCC supports concurrent transactions, but conflicting writes and query plans still need examination. A separate server introduces connection and network considerations. [P5] | One writer at a time per database file; WAL permits readers alongside a writer but does not remove that write limit. Low-concurrency use may still be sufficient. [Q1], [Q2] | Document layout and transaction scope affect contention and access cost. Distributed transactions add deployment requirements; no project-specific latency is established. [M2], [M4], [M6] |
| Deployment and scaling | A database service and durable storage require credentials, migrations, recovery procedures and monitoring. This is more operational work than an embedded file. | No separate database server is required. Sharing a file directly across multiple application hosts is unsuitable as a default deployment strategy. [Q1] | A separate database deployment is required; replica-set/sharding capabilities are available, but the current project has not demonstrated a need for distributed scale. [M2], [M4] |
| Development and testing | Adds service setup, but integration tests can exercise the intended database semantics directly. Test credentials and data must be isolated from deployment. | Convenient for local experiments; passing SQLite tests would not validate PostgreSQL-specific queries, migrations or access policies. | Flexible documents can ease changes, but tests must cover validators, indexes, reference consistency and the actual transaction topology. [M1], [M4], [M7] |
| Maintenance and data lifecycle | Explicit relationships help define deletion/retention behavior; schema migrations and restore tests remain necessary. | A small deployment is economical to administer, but file/WAL consistency, recovery and schema evolution still require care. [Q1], [Q2] | Flexibility does not remove schema evolution. Duplicated information and cross-document references require explicit consistency and deletion rules. [M1], [M7] |
| Project fit and trade-off | Preferred for related prediction, model and feedback records in the proposed shared web service; accepts the additional database-operation burden. | Credible for a restricted, low-write prototype. It is not selected as the target merely to avoid service setup, nor dismissed as universally unfit for web applications. | Credible where heterogeneous documents dominate. Current metadata relationships provide less justification for the added document/reference design than for relational storage. |

### 3.3. Preferred storage and alternatives retained

**PostgreSQL is the preferred target store**, consistent with the Project Proposal. Predictions refer to model versions; feedback refers to predictions; confirmed contributions require traceable review and permitted-use records. Relational constraints and transactional updates provide a direct way to express these relationships. SQL aggregation also fits the planned history/statistics behavior. [P1], [P2], [P4] This is a structural fit, not evidence of a completed database or superior measured speed.

The cost of this choice is operational complexity: connection management, migrations, secret handling, persistent volumes, recovery and updates. Row-level security may be considered as defense in depth after the session/owner model is defined; it cannot replace correctly scoped API queries or tests. Policies require explicit configuration, and privileged roles can bypass them. [P3] Retention and deletion must include restricted contributions and recovery copies, not just removal from a history screen.

SQLite remains reasonable for an isolated low-concurrency prototype. Its transaction and foreign-key support mean that it should not be characterized as lacking integrity. Its single-writer model and embedded-file deployment are the relevant constraints for future concurrent history and feedback writes. [Q1], [Q2], [Q3] If used experimentally, its limitations and differences from PostgreSQL must remain visible in integration testing.

MongoDB remains reasonable if future requirements center on heterogeneous event documents. Schema validation, atomic operations and supported multi-document transactions provide substantial capabilities. [M1], [M2] For the present relationships, embedding can duplicate model information, while separate references move consistency work into application logic. Transaction topology and security configuration also remain operational responsibilities. [M3], [M4], [M7] These trade-offs reduce its present justification without implying that document databases are inherently insecure or non-transactional.

## 4. Frontend alternatives

### 4.1. Purpose, candidates and evidence interpretation

The frontend comparison concerns the browser workflows in Proposal Sections 9–10: single-message checking, probability and explanation display, batch results, language selection, authorized history/statistics and incorrect-result feedback. Beknur leads their interface implementation; the inference, storage and feedback-processing responsibilities remain with the owners defined in Proposal Section 8.

The candidates are **React + TypeScript**, using typed components and explicit state composition; **Vue + TypeScript**, using single-file components, reactive bindings and TypeScript tooling; and **Angular + TypeScript**, using typed templates with framework-provided forms and HTTP packages. Each can support the proposed browser interface. They offer sufficiently different composition and tooling choices to make the comparison useful. [UI-R1], [UI-R2], [UI-V1], [UI-V2], [UI-A1], [UI-A4], [UI-A5]

The matrix evaluates equivalent application responsibilities rather than matching package counts. **Core** means a documented library/framework facility; **additional package** means a separately installed dependency, including official companion packages; **project work** means behavior the team must implement and verify. Statements about fit and learning effort are engineering judgments based on these responsibilities, not measured productivity. CSS, native browser controls and testing tools are available across the candidates. No browser performance, bundle-size or usability ranking is established.

### 4.2. Comparative matrix

| Criterion | React + TypeScript | Vue + TypeScript | Angular + TypeScript |
|---|---|---|---|
| Internationalization: EN/RU/KZ | Additional package: `react-i18next` exposes translation functions and runtime language changes. Reviewed resources, fallback policy and preservation of current work are project work. [UI-I1] | Additional package: Vue I18n provides translation resources and reactive runtime locale changes. The team supplies reviewed translations and state-preservation behavior. [UI-I2] | Official companion package: `@angular/localize` supports localized builds/deployment. For runtime switching comparable to the other candidates, an additional library such as ngx-translate exposes `TranslateService.use()`. Translations, fallback and state preservation still need project work. [UI-A2], [UI-A3], [UI-I3] |
| TypeScript and runtime API validation | TSX and installed React type declarations support typed props/state and static checking. API data still needs runtime checks before becoming a trusted result. [UI-R1], [UI-T1] | TypeScript support covers component code/templates; `vue-tsc` checks single-file components separately from transpilation. Runtime response checking remains project work. [UI-V1], [UI-T1] | Template checking complements TypeScript. `HttpClient` response generics do not validate received JSON; runtime contract checks remain necessary. [UI-A1], [UI-A5] |
| Responsive design | Components render HTML styled with CSS. Flexible layouts, breakpoints and long-text behavior require implementation and device/viewport checks. [UI-R3], [UI-B1] | Component templates use the same CSS layout mechanisms; single-file organization does not itself ensure mobile usability. [UI-V1], [UI-B1] | Templates need the same responsive CSS and viewport checks. Forms/HTTP tooling provides no automatic layout acceptance. [UI-A4], [UI-B1] |
| Accessibility | DOM props support ARIA attributes and focus/keyboard events. Semantic controls, labels, contrast and status announcements require deliberate design and testing. [UI-R3] | Official guidance covers semantic forms, labels and focus management. Following that guidance and testing the finished UI remain team responsibilities. [UI-V3] | Official guidance supports native controls and ARIA bindings; optional CDK utilities assist interaction patterns. Neither framework nor component package establishes accessibility compliance. [UI-A6] |
| SMS input and prediction presentation | Component state can represent editable text and result views. Validation messages and submission behavior are project code. [UI-R2] | `v-model` connects native text controls to reactive state. SMS validation and result composition remain project code. [UI-V2] | Reactive Forms provides control/group state and validators. The SMS-specific form and result components require configuration and application code. [UI-A4] |
| Probability and confidence display | Typed result props/state can drive distinct label, score and confidence views. The API contract must define their interpretation. [UI-R1], [UI-R2] | Typed component data and bindings can display those fields. Formatting and uncertainty wording require application rules. [UI-V1], [UI-V2] | Typed templates can present the same fields. Neither template checking nor form validation establishes calibrated model confidence. [UI-A1] |
| Explanation highlights | Render validated text segments as ordinary children; avoid untrusted `dangerouslySetInnerHTML`. Feature attribution and offset mapping are project work. [UI-R3] | Use escaped interpolation inside segment elements; avoid `v-html` for submitted SMS. Model contributions and segment boundaries remain external contracts. [UI-V4] | Use text interpolation and validated segments; do not bypass security for message markup. Attribution and Unicode mapping require application logic. [UI-A8] |
| Batch-file checking interface | A native file control and component state can present file selection and row results. Parsing, limits and batch-status handling require project code. [UI-B3], [UI-R2] | Native file selection and reactive form/result views support the same workflow. CSV decoding, invalid rows and server limits are not supplied by `v-model`. [UI-B3], [UI-V2] | Native file controls and application components support uploads/results. Reactive Forms does not provide a CSV parser or SMS batch classifier. [UI-B3], [UI-A4] |
| History and statistics UI | State composition supports filters and result lists; API queries and statistics presentation require application code and an authorized data scope. [UI-R2], [UI-B2] | Typed components can present the same lists and summaries. Fetching, filtering and retention behavior remain application decisions. [UI-V1], [UI-B2] | Components and `HttpClient` can present queried metadata. Authorization and the meaning of summary values remain API/application responsibilities. [UI-A1], [UI-A5] |
| Incorrect-result feedback | Form state can separate an error flag from optional text contribution. Consent, submission and confirmation states are project work. [UI-R2] | Form bindings support correction and consent controls. A submitted correction still needs server-side review. [UI-V2] | Reactive Forms supports correction controls and validation. It supplies neither consent policy nor verified-label/retraining behavior. [UI-A4] |
| Privacy and data ownership | Component state can hold transient input, but persistence, telemetry and error reporting depend on application integrations. History ownership and retention follow Proposal Section 16. [UI-R2] | Escaped text rendering addresses injection, not retention or consent. Browser persistence and authorized history access still require the same project policy. [UI-V4] | Template security controls likewise do not establish privacy. Consent, logging, retention and authorized access remain application/API responsibilities under Proposal Section 16. [UI-A8] |
| REST API integration | Browser Fetch can call FastAPI; a reusable API adapter must check HTTP status and validate payloads. React does not prescribe the transport layer. [UI-B2], [UI-T1] | Browser Fetch can serve the same contract; transport/error conventions must be agreed separately from component typing. [UI-B2], [UI-V1] | Official `HttpClient` provides HTTP methods and Observable responses. This reduces transport-tool selection but introduces subscription/error conventions to maintain. [UI-A5] |
| Loading states and error handling | Component state can distinguish idle, submitting, success and failure. Fetch requires explicit HTTP-status checks; stale-result handling is project work. [UI-R2], [UI-B2] | Reactive bindings can display those states. HTTP errors, canceled requests and late responses need explicit application handling. [UI-V2], [UI-B2] | Forms and Observable responses support submission/error flows. The team must still prevent duplicate submissions and stale result display. [UI-A4], [UI-A5] |
| Component testing | Additional package: React Testing Library provides user-oriented DOM queries. A compatible runner/environment and meaningful assertions must be configured separately. [UI-C1] | Official Vue Test Utils mounts components; the Vue testing guide discusses runner and browser-test options. Rendering and emitted-event checks require written tests. [UI-V5] | Angular documents an integrated CLI testing setup and component-testing guidance. Project tests must cover forms, services and rendered outcomes. [UI-A7] |
| End-to-end testing | Additional browser tooling such as Playwright can exercise the rendered application through roles, inputs and assertions. API fixtures or an integrated service are required. [UI-E1] | The same Playwright workflow can exercise a Vue application. Choosing Vue does not supply the test scenarios or API environment. [UI-E1] | The same browser-driven checks can exercise Angular. They remain separate from framework unit tests and need a declared application environment. [UI-E1], [UI-A7] |
| Maintainability and learning complexity | Explicit state composition suits separated screens, but the team must maintain consistent API, localization and testing conventions. Hooks/state design and package integration require learning. [UI-R2], [UI-I1], [UI-C1] | Template-oriented form bindings and TypeScript tooling offer a coherent alternative. Reactivity, component conventions and additional package compatibility require learning. [UI-V1], [UI-V2], [UI-I2] | Forms, HTTP and testing guidance reduce independent tool choices. The team must learn template, form and Observable conventions and maintain the selected localization packages. No comparative learning time is established. [UI-A1], [UI-A4], [UI-A5], [UI-A7], [UI-I3] |

### 4.3. Advantages, limitations and recommended frontend

**React + TypeScript is the recommended frontend**, consistent with the proposal and Beknur's assigned responsibility. Typed result components and explicit state transitions offer a suitable structure for the checker, explanation view, batch rows and consent interactions. [UI-R1], [UI-R2] A shared API adapter can keep HTTP/payload handling outside presentation components, while `react-i18next` and React Testing Library provide documented options for localization and user-oriented component checks. [UI-I1], [UI-C1] This composition fits the required workflows without requiring that API/storage follow a frontend-specific server framework.

The decision rule is to establish a documented implementation route for every required workflow, then consider integration responsibilities and consistency with the proposed architecture. All three candidates provide suitable mechanisms when combined with application code and selected packages. The comparison therefore identifies no exclusive functional advantage for React. Retaining it is a conditional project choice: its component/state approach fits the bounded workflows and preserves the proposal's assigned interface responsibility, while the team accepts explicit localization, API-validation and test-tool integration. The evidence does not establish lower cost or effort than Vue or Angular; later implementation findings may justify revisiting the choice.

Its principal cost is integration responsibility: React does not settle translation resources, request validation, asynchronous consistency or the test runner. Those conventions must be agreed and maintained rather than selected independently by each screen. The recommendation accepts this cost; it does not establish that React is faster, easier to learn or uniquely able to consume FastAPI. The official role assignment supports continuity, but is not evidence of prior React proficiency or a substitute for the technical comparison.

**Vue + TypeScript is a credible alternative.** Its native form bindings and TypeScript-ready single-file components provide a direct way to organize input/result screens; Vue I18n and official testing utilities cover relevant extension points. [UI-V1], [UI-V2], [UI-I2], [UI-V5] The trade-offs are the need to learn Vue's reactive/component conventions, run the appropriate type checks and maintain the same application contracts. The present requirements reveal no missing Vue capability that disqualifies it. Changing the proposed frontend would require an agreed implementation/tooling change; no demonstrated project benefit currently justifies that change.

**Angular + TypeScript is also technically suitable.** Framework-provided forms and HTTP packages and documented testing conventions are strengths where uniform structure across many forms/services is important. [UI-A4], [UI-A5], [UI-A7] These conventions require framework-specific knowledge while leaving SMS, privacy and explanation behavior to the application. Official locale-specific builds are one localization route; an additional package such as ngx-translate supports runtime language changes comparable to the React/Vue options. [UI-A2], [UI-A3], [UI-I3] Choosing between those routes entails deployment or dependency decisions. No measured learning disadvantage, performance deficit or inability to switch languages is established.

### 4.4. Application contracts and implementation boundaries

**Languages and state.** EN/RU/KZ interface labels correspond to locale identifiers `en`, `ru` and `kk`; `KZ` is the project's display shorthand for Kazakh, not the language code. This follows [Dataset Strategy Section 2](dataset_strategy.md#2-language-and-task-requirements). The team must supply reviewed translations for controls, validation, uncertainty and consent, define fallback behavior and preserve user work during language changes. Translated UI text does not establish classifier performance for that language. UI locale must remain separate from message-language metadata and model routing.

**Typed and verified responses.** TypeScript annotations are erased during compilation. Neither an asserted result type nor Angular's typed HTTP generic establishes that the server returned the required fields. [UI-T1], [UI-A5] The proposed API adapter should validate label values, finite probability bounds, version identifiers, row identifiers and explanation structures before updating result state. It should distinguish transport, contract and user-input errors, associate results with the submitted input and suppress late responses for superseded submissions. These are proposed safeguards, not an implemented contract.

**FastAPI integration.** All three alternatives can consume the same HTTP/JSON contract; no framework-specific FastAPI connector is required by this design. If UI and API have different origins, Sanzhar must configure permitted origins and any credential handling consistently with the selected session model. FastAPI documents explicit allowed origins and the limitations of wildcard settings for credentialed communication. [UI-H1] CORS configuration governs browser cross-origin access; it must not replace API authorization. Integration acceptance should cover the actual deployment origins, HTTP failures and invalid response bodies, not only successful mock requests.

**Probability, confidence and explanations.** Display the model-estimated spam probability separately from its documented confidence indication; neither is a guarantee of safety or an individual-prediction accuracy percentage. Sanzhar's explanation contract must identify contributions and their relation to the displayed text. Beknur must render checked text segments rather than inject HTML, using the frameworks' ordinary text-rendering paths and respecting their security guidance. [UI-R3], [UI-V4], [UI-A8] Normalization, redaction, emoji and differing string-index conventions require an agreed Unicode/offset mapping; invalid mappings should yield an explicit unavailable explanation, not invented highlights. Dataset Strategy Sections 8–9 and 20 define the relevant preparation/inference boundary.

**Accessible result interpretation.** Planned checks should verify that labels and influential fragments have textual meaning beyond color, and that loading, completion and error status messages are available to assistive technology without requiring focus changes. These concerns correspond to WCAG 2.2 criteria 1.4.1 and 4.1.3. [UI-W1] They apply equally to all candidates and complement keyboard, focus, contrast and responsive-layout checks. They are evaluation criteria to implement and verify, not a claim of WCAG conformance.

**Batch, history and feedback.** A browser file input only selects files: even its `accept` attribute is a chooser hint rather than validation. Server-side validation remains necessary. [UI-B3] The project must define encoding, columns, size/row limits and a stable result-or-error for each admitted row. History/statistics views should request authorized metadata and distinguish predicted-spam counts from evaluated classifier quality. Raw SMS should not enter browser persistence, analytics or error reporting by default. A feedback flag must remain separate from optional, consented text contribution; the UI cannot approve labels, authorize its own access or trigger unrestricted retraining. These rules follow Proposal Sections 9 and 16 and the existing storage boundary.

### 4.5. Traceability to requirements and later verification

The table traces the decision to the published [Project Proposal](project_proposal.md). A separate FR/NFR specification is not yet available in the reviewed baseline, so identifier mapping remains pending. No requirement identifiers or acceptance thresholds are assumed here.

| Proposal requirement basis | Consequence for frontend selection/design | Evidence required during implementation |
|---|---|---|
| Section 9, scenarios 1–2; Sections 13–14: single checking and faithful explanation | Typed result views, explicit request state, safe segment rendering and a common FastAPI contract | Component/contract checks for labels, scores, versions, malformed responses and Unicode highlights; integration checks under actual origin/session settings |
| Section 9, scenario 3: batch results and validation errors | File selection and stable row/result presentation; decoding and server limits need a separate contract | Permitted test files with valid/invalid rows; reconciled outputs; file/row limit and failure checks |
| Section 9, scenario 4; Section 15: multilingual interaction | Reviewed `en`/`ru`/`kk` resources and switching behavior, independent of model support | All-language scenario checks, missing-key/fallback checks and preservation of current work |
| Section 9, scenarios 5–7; Section 16: history and feedback boundaries | Authorized metadata views and separate error-report/text-consent interactions | UI/API checks for access failures, correction submission and consent boundaries; storage/log inspection by the relevant owner |
| Section 10: accessibility and usability | Semantic HTML, keyboard/focus behavior, textual alternatives to color and programmatically available status messages across candidates | Keyboard, status announcement, color-independent interpretation, contrast and narrow/wide-layout checks plus actual user observations |
| Sections 10 and 18: maintainability and integrated verification | Shared API adapter, consistent state/localization conventions, component checks and browser E2E | Repeatable component runs and browser scenarios against declared mock or integrated API environments |

React Testing Library offers DOM-focused component utilities; it is not itself a test runner. Vue documents component utilities and distinct runner/browser options, while Angular documents its CLI testing setup. [UI-C1], [UI-V5], [UI-A7] Playwright can drive the proposed public workflows at browser level across all candidates. [UI-E1] Mock API results can verify UI behavior but cannot establish trained-model quality or successful service integration. The checks in the table are planned evidence, not executed application tests or a replacement for the team's verification plan.

### 4.6. Limitations and decisions to confirm

The comparison uses official documentation rather than implemented candidate prototypes or observed team development. It establishes available mechanisms and a reasoned fit, not measured accessibility, development effort, runtime performance or commercial superiority. Versions and compatible localization/testing dependencies must be recorded when implementation begins; no exact runtime versions are selected here.

Before implementation acceptance, agree the API schemas and response validation, explanation offsets, language-switch behavior, batch limits, session/access model, consent/retention policy and component/browser test environments. Real user findings may change priorities. A different frontend remains possible if documented requirements or implementation evidence justify it. Formal identifier mapping and peer review remain pending; working UI evidence belongs to subsequent implementation and evaluation.

## 5. Architectural implications

### 5.1. UI, API and model boundary

The intended flow is React/TypeScript UI -> FastAPI validation and authorization -> version-compatible inference -> structured JSON result. Beknur leads the UI and agrees the contract with Sanzhar. The frontend should receive the label, score interpretation, threshold, model version and faithful explanation fields; single-message and batch schemas should define invalid-row behavior. This describes integration with the proposed frontend, not a comparison or implementation of frontend technologies.

Rafael leads training/evaluation, TF-IDF pipeline configuration and model versions. Sanzhar leads runtime inference, explanations, error/threshold analysis and the API. Beknur leads data preparation, annotation and character-feature experiments. The service must use the same deterministic privacy transformation and fitted feature extraction as the selected training pipeline. An interface-language setting must not silently select an unsupported model or establish EN/RU/KZ quality.

The API should load a trusted, reviewed artifact with compatible dependencies and explicit label, preprocessing, threshold and explanation metadata. Serialized model files should remain in protected artifact storage or a controlled read-only deployment location; PostgreSQL should hold their identifiers, checksums and lifecycle metadata. Scikit-learn warns that pickle-based formats can execute code when loaded and that environment compatibility matters. [A1] Public clients must not upload arbitrary serialized models for loading. A vocabulary may also expose retained training fragments, so artifact publication requires privacy review.

### 5.2. History, feedback and statistics

Sanzhar leads persistence, data schema, safe processing, masking and API authorization. Rafael leads history/statistics behavior, feedback and confirmed-feedback retraining; Beknur leads their screens and consent interactions. These boundaries preserve the official roles.

Ordinary checking should process text transiently and persist only agreed metadata in an authorized scope. Access/error logs, validation-error bodies, tracing and temporary batch files need the same privacy policy as the database. Validation and response models do not automatically suppress private text in these paths. Opaque session identifiers and message hashes do not prove anonymity.

Metadata-only feedback may flag a result, but retaining text requires a distinct consent and review path. Approved text should enter restricted, versioned data storage only after privacy screening, label confirmation and checks against reserved evaluation groups. Consent evidence should be separate from ordinary prediction history. Public feedback must never directly update the live classifier. PostgreSQL can record review and version transitions; database transactions do not make file publication and model activation atomic. A later promotion procedure must verify artifact availability and compatibility and preserve rollback to the previous version.

Statistics should aggregate authorized metadata. A count of predicted spam is a service statistic, not measured precision or recall. Classifier-quality metrics require the separate labeled evaluation procedure led by Rafael. Aggregate views must not expose another user's activity or small identifiable groups.

### 5.3. Docker and deployment

Sanzhar leads Docker, CI, public deployment and API integration tests. The proposed deployment separates the API process, PostgreSQL and offline training responsibilities. API instances should not depend on private text stored in their writable container layer. PostgreSQL needs durable storage; model artifacts need controlled mounting or retrieval; credentials belong in deployment configuration rather than committed files. HTTPS, request/file bounds, rate limits, timeouts and resource limits remain required application/operation controls. [F3]

Database migrations and model-compatibility checks should complete before serving requests. Health checks, restart behavior and recovery procedures must be defined. More API workers require measured CPU/RAM capacity, bounded database connections and compatible active-model versions. [F3] No hosting provider, capacity figure, deployment price or production-readiness claim is selected through this comparison.

## 6. Conclusion and unresolved implementation decisions

FastAPI and PostgreSQL are the preferred technologies because the project requires a documented Python inference API and integrity across related history, model and feedback records. Flask offers a credible smaller core, Django/DRF a broader resource-oriented framework, SQLite a simpler embedded deployment, and MongoDB a flexible document model. Their relative value depends on the actual contracts, workload and operational requirements.

Before implementation acceptance, the component owners must agree the API schemas, session/owner authorization, consent and retention rules, database relationships, migration approach, artifact format/promotion procedure and workload targets.

The frontend comparison recommends React + TypeScript for the required multilingual input/result workflows and explicit API/UI separation, while retaining Vue + TypeScript and Angular + TypeScript as viable alternatives. Localization, runtime contract validation, faithful highlights, accessibility and privacy remain implementation and verification responsibilities under every candidate.

## 7. References

The following official documentation was consulted on 24 October 2026. Links using `stable` or `current` can change; implementation must record the actual dependency and database versions selected. Project-specific conclusions above are distinguished from documented framework/database capabilities.

### Backend frameworks

- **F1.** FastAPI. [Features][F1]. Validation, OpenAPI, security components and dependency injection.
- **F2.** FastAPI. [Concurrency and async / await][F2]. I/O concurrency and CPU-bound execution.
- **F3.** FastAPI. [Deployment concepts][F3]. HTTPS, restarts, workers and model memory.
- **F4.** FastAPI. [Response model — return type][F4]. Response validation and field filtering.
- **F5.** FastAPI. [Testing][F5]. TestClient and pytest-based API checks.
- **L1.** Pallets. [Design decisions in Flask][L1]. Core responsibilities and extensions.
- **L2.** Pallets. [Using async and await][L2]. WSGI workers and async limitations.
- **L3.** Pallets. [Security considerations][L3]. Resource bounds and application safeguards.
- **L4.** Pallets. [Testing Flask applications][L4]. Test client and test structure.
- **L5.** Pallets. [Deploying to production][L5]. Production serving requirements.
- **D1.** Django REST framework. [Overview][D1]. API components and ORM/non-ORM integration.
- **D2.** Django REST framework. [Serializers][D2]. Representations and validation.
- **D3.** Django REST framework. [Permissions][D3]. Object permissions and list/create limitations.
- **D4.** Django Software Foundation. [Deployment checklist][D4]. Security and deployment settings.
- **D5.** Django REST framework. [Testing][D5]. APIClient and request verification.

### Storage and model artifacts

- **P1.** PostgreSQL Global Development Group. [Constraints][P1]. Types of relational constraints.
- **P2.** PostgreSQL Global Development Group. [Transactions][P2]. Atomic changes and rollback.
- **P3.** PostgreSQL Global Development Group. [Row security policies][P3]. Policy configuration and privileged-role exceptions.
- **P4.** PostgreSQL Global Development Group. [Aggregate functions][P4]. SQL aggregation.
- **P5.** PostgreSQL Global Development Group. [Concurrency control: introduction][P5]. MVCC and locking.
- **Q1.** SQLite. [Appropriate uses for SQLite][Q1]. Embedded deployment and client/server trade-offs.
- **Q2.** SQLite. [Isolation in SQLite][Q2]. Transactions, writers and WAL behavior.
- **Q3.** SQLite. [Foreign key support][Q3]. Connection-level enforcement and configuration.
- **M1.** MongoDB. [Schema validation][M1]. Explicit validation in a flexible document model.
- **M2.** MongoDB. [Transactions][M2]. Single-document atomicity and multi-document transactions.
- **M3.** MongoDB. [Security checklist for self-managed deployments][M3]. Access, network and transport controls.
- **M4.** MongoDB. [Production considerations for transactions][M4]. Deployment prerequisites and constraints.
- **M5.** MongoDB. [Aggregation operations][M5]. Grouped calculations over documents.
- **M6.** MongoDB. [Data modeling][M6]. Embedding and access-pattern-oriented design.
- **M7.** MongoDB. [Data consistency][M7]. Duplicated data and application-maintained references.
- **A1.** Scikit-learn developers. [Model persistence][A1]. Artifact loading risks and environment compatibility.

### Frontend frameworks, browser facilities and testing

The following official framework/library and browser-platform documentation was consulted for the frontend comparison on 24 October 2026. It supports the cited mechanisms; the selection rationale and proposed application contracts are project-specific judgments.

- **UI-R1.** React. [Using TypeScript][UI-R1]. Component props/state typing and TSX.
- **UI-R2.** React. [Managing State][UI-R2]. State structure and component coordination.
- **UI-R3.** React. [Common components][UI-R3]. DOM props, accessibility attributes, events and raw-HTML risks.
- **UI-V1.** Vue. [Using Vue with TypeScript][UI-V1]. Single-file components, type checking and tooling.
- **UI-V2.** Vue. [Form Input Bindings][UI-V2]. Native controls and reactive form state.
- **UI-V3.** Vue. [Accessibility][UI-V3]. Semantic forms, labels and focus guidance.
- **UI-V4.** Vue. [Security][UI-V4]. Text escaping and unsafe HTML injection.
- **UI-V5.** Vue. [Testing][UI-V5]. Component utilities, runners and browser testing.
- **UI-A1.** Angular. [Template type checking][UI-A1]. Template/type-checking configuration.
- **UI-A2.** Angular. [Add the localize package][UI-A2]. Official companion package and localization setup.
- **UI-A3.** Angular. [Deploy multiple locales][UI-A3]. Locale-specific application deployment.
- **UI-A4.** Angular. [Reactive forms][UI-A4]. Form controls, groups and validation.
- **UI-A5.** Angular. [Making HTTP requests][UI-A5]. HTTP methods, Observables and response-generic limitations.
- **UI-A6.** Angular. [Accessibility][UI-A6]. Native elements, ARIA and optional CDK support.
- **UI-A7.** Angular. [Unit testing][UI-A7]. CLI testing setup and component-testing guidance.
- **UI-A8.** Angular. [Security][UI-A8]. Template trust boundaries and unsafe bypasses.
- **UI-I1.** React-i18next. [useTranslation hook][UI-I1]. Translation functions and language changes.
- **UI-I2.** Vue I18n. [Composition API][UI-I2]. Translation resources and locale state.
- **UI-I3.** Ngx-translate. [TranslateService API: use][UI-I3]. Additional Angular localization library and runtime language changes.
- **UI-H1.** FastAPI. [CORS (Cross-Origin Resource Sharing)][UI-H1]. Allowed origins and credential-related configuration.
- **UI-W1.** W3C. [Web Content Accessibility Guidelines 2.2][UI-W1], criteria 1.4.1 and 4.1.3. Use of color and status-message accessibility.
- **UI-T1.** TypeScript. [The Basics: Erased Types][UI-T1]. Static types and runtime behavior.
- **UI-B1.** MDN Web Docs. [Responsive web design][UI-B1]. Flexible CSS layouts and media queries.
- **UI-B2.** MDN Web Docs. [Using the Fetch API][UI-B2]. HTTP calls and explicit response-status checks.
- **UI-B3.** MDN Web Docs. [File inputs][UI-B3]. File selection and validation limitations.
- **UI-C1.** Testing Library. [React Testing Library][UI-C1]. User-oriented DOM tests and runner separation.
- **UI-E1.** Playwright. [Writing tests][UI-E1]. Browser navigation, controls and assertions.

[F1]: https://fastapi.tiangolo.com/features/
[F2]: https://fastapi.tiangolo.com/async/
[F3]: https://fastapi.tiangolo.com/deployment/concepts/
[F4]: https://fastapi.tiangolo.com/tutorial/response-model/
[F5]: https://fastapi.tiangolo.com/tutorial/testing/
[L1]: https://flask.palletsprojects.com/en/stable/design/
[L2]: https://flask.palletsprojects.com/en/stable/async-await/
[L3]: https://flask.palletsprojects.com/en/stable/web-security/
[L4]: https://flask.palletsprojects.com/en/stable/testing/
[L5]: https://flask.palletsprojects.com/en/stable/deploying/
[D1]: https://www.django-rest-framework.org/
[D2]: https://www.django-rest-framework.org/api-guide/serializers/
[D3]: https://www.django-rest-framework.org/api-guide/permissions/
[D4]: https://docs.djangoproject.com/en/stable/howto/deployment/checklist/
[D5]: https://www.django-rest-framework.org/api-guide/testing/
[P1]: https://www.postgresql.org/docs/current/ddl-constraints.html
[P2]: https://www.postgresql.org/docs/current/tutorial-transactions.html
[P3]: https://www.postgresql.org/docs/current/ddl-rowsecurity.html
[P4]: https://www.postgresql.org/docs/current/tutorial-agg.html
[P5]: https://www.postgresql.org/docs/current/mvcc-intro.html
[Q1]: https://www.sqlite.org/whentouse.html
[Q2]: https://www.sqlite.org/isolation.html
[Q3]: https://www.sqlite.org/foreignkeys.html
[M1]: https://www.mongodb.com/docs/manual/core/schema-validation/
[M2]: https://www.mongodb.com/docs/manual/core/transactions/
[M3]: https://www.mongodb.com/docs/manual/administration/security-checklist/
[M4]: https://www.mongodb.com/docs/manual/core/transactions-production-consideration/
[M5]: https://www.mongodb.com/docs/manual/aggregation/
[M6]: https://www.mongodb.com/docs/manual/data-modeling/
[M7]: https://www.mongodb.com/docs/manual/data-modeling/data-consistency/
[A1]: https://scikit-learn.org/stable/model_persistence.html
[UI-R1]: https://react.dev/learn/typescript
[UI-R2]: https://react.dev/learn/managing-state
[UI-R3]: https://react.dev/reference/react-dom/components/common
[UI-V1]: https://vuejs.org/guide/typescript/overview.html
[UI-V2]: https://vuejs.org/guide/essentials/forms.html
[UI-V3]: https://vuejs.org/guide/best-practices/accessibility.html
[UI-V4]: https://vuejs.org/guide/best-practices/security.html
[UI-V5]: https://vuejs.org/guide/scaling-up/testing.html
[UI-A1]: https://angular.dev/tools/cli/template-typecheck
[UI-A2]: https://angular.dev/guide/i18n/add-package
[UI-A3]: https://angular.dev/guide/i18n/deploy
[UI-A4]: https://angular.dev/guide/forms/reactive-forms
[UI-A5]: https://angular.dev/guide/http/making-requests
[UI-A6]: https://angular.dev/best-practices/a11y
[UI-A7]: https://angular.dev/guide/testing
[UI-A8]: https://angular.dev/best-practices/security
[UI-I1]: https://react.i18next.com/latest/usetranslation-hook
[UI-I2]: https://vue-i18n.intlify.dev/guide/advanced/composition
[UI-I3]: https://ngx-translate.org/reference/translate-service-api/#use
[UI-H1]: https://fastapi.tiangolo.com/tutorial/cors/
[UI-W1]: https://www.w3.org/TR/WCAG22/
[UI-T1]: https://www.typescriptlang.org/docs/handbook/2/basic-types.html#erased-types
[UI-B1]: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design
[UI-B2]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
[UI-B3]: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/file
[UI-C1]: https://testing-library.com/docs/react-testing-library/intro/
[UI-E1]: https://playwright.dev/docs/writing-tests
