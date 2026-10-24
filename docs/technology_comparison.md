# Technology Comparison: Backend and Data Storage

## 1. Purpose and evaluation basis

This comparison examines backend frameworks and data storage technologies for the multilingual SMS application defined in the [Project Proposal](project_proposal.md), particularly Sections 8–18. It evaluates how the alternatives support API contracts, Python inference, privacy, data integrity and maintainable deployment.

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

## 4. Architectural implications

### 4.1. UI, API and model boundary

The intended flow is React/TypeScript UI -> FastAPI validation and authorization -> version-compatible inference -> structured JSON result. Beknur leads the UI and agrees the contract with Sanzhar. The frontend should receive the label, score interpretation, threshold, model version and faithful explanation fields; single-message and batch schemas should define invalid-row behavior. This describes integration with the proposed frontend, not a comparison or implementation of frontend technologies.

Rafael leads training/evaluation, TF-IDF pipeline configuration and model versions. Sanzhar leads runtime inference, explanations, error/threshold analysis and the API. Beknur leads data preparation, annotation and character-feature experiments. The service must use the same deterministic privacy transformation and fitted feature extraction as the selected training pipeline. An interface-language setting must not silently select an unsupported model or establish EN/RU/KZ quality.

The API should load a trusted, reviewed artifact with compatible dependencies and explicit label, preprocessing, threshold and explanation metadata. Serialized model files should remain in protected artifact storage or a controlled read-only deployment location; PostgreSQL should hold their identifiers, checksums and lifecycle metadata. Scikit-learn warns that pickle-based formats can execute code when loaded and that environment compatibility matters. [A1] Public clients must not upload arbitrary serialized models for loading. A vocabulary may also expose retained training fragments, so artifact publication requires privacy review.

### 4.2. History, feedback and statistics

Sanzhar leads persistence, data schema, safe processing, masking and API authorization. Rafael leads history/statistics behavior, feedback and confirmed-feedback retraining; Beknur leads their screens and consent interactions. These boundaries preserve the official roles.

Ordinary checking should process text transiently and persist only agreed metadata in an authorized scope. Access/error logs, validation-error bodies, tracing and temporary batch files need the same privacy policy as the database. Validation and response models do not automatically suppress private text in these paths. Opaque session identifiers and message hashes do not prove anonymity.

Metadata-only feedback may flag a result, but retaining text requires a distinct consent and review path. Approved text should enter restricted, versioned data storage only after privacy screening, label confirmation and checks against reserved evaluation groups. Consent evidence should be separate from ordinary prediction history. Public feedback must never directly update the live classifier. PostgreSQL can record review and version transitions; database transactions do not make file publication and model activation atomic. A later promotion procedure must verify artifact availability and compatibility and preserve rollback to the previous version.

Statistics should aggregate authorized metadata. A count of predicted spam is a service statistic, not measured precision or recall. Classifier-quality metrics require the separate labeled evaluation procedure led by Rafael. Aggregate views must not expose another user's activity or small identifiable groups.

### 4.3. Docker and deployment

Sanzhar leads Docker, CI, public deployment and API integration tests. The proposed deployment separates the API process, PostgreSQL and offline training responsibilities. API instances should not depend on private text stored in their writable container layer. PostgreSQL needs durable storage; model artifacts need controlled mounting or retrieval; credentials belong in deployment configuration rather than committed files. HTTPS, request/file bounds, rate limits, timeouts and resource limits remain required application/operation controls. [F3]

Database migrations and model-compatibility checks should complete before serving requests. Health checks, restart behavior and recovery procedures must be defined. More API workers require measured CPU/RAM capacity, bounded database connections and compatible active-model versions. [F3] No hosting provider, capacity figure, deployment price or production-readiness claim is selected through this comparison.

## 5. Conclusion and unresolved implementation decisions

FastAPI and PostgreSQL are the preferred technologies because the project requires a documented Python inference API and integrity across related history, model and feedback records. Flask offers a credible smaller core, Django/DRF a broader resource-oriented framework, SQLite a simpler embedded deployment, and MongoDB a flexible document model. Their relative value depends on the actual contracts, workload and operational requirements.

Before implementation acceptance, the component owners must agree the API schemas, session/owner authorization, consent and retention rules, database relationships, migration approach, artifact format/promotion procedure and workload targets.

## 6. References

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
