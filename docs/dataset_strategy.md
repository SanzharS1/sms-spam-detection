# Multilingual SMS Dataset Strategy

| Field | Value |
|---|---|
| Project | Development of a Web-Based SMS Spam Detection Application Using Machine Learning |
| Group | SE-2425 |
| Task | [DIP-4 — Document multilingual dataset strategy and annotation protocol](https://sms-spam-se2425.youtrack.cloud/issue/DIP-4) |
| Author and data preparation lead | Beknur Serikkali |
| Technical reviewer | Rafael Shaekhov |
| Supporting contributor | Sanzhar Sabyrov |
| Date | 24 October 2026 |

## 1. Purpose and responsibility boundaries

This strategy specifies how a reproducible English, Russian and Kazakh SMS corpus will be sourced, screened, prepared and partitioned for the [Project Proposal](project_proposal.md), particularly Sections 8 and 14–18. The accompanying [Annotation Guidelines](annotation_guidelines.md) define the same binary classification task and the human review process. Corpus collection and experiments remain planned.

Beknur leads sourcing, preparation, annotation, agreement assessment and character n-gram experiments. Rafael reviews duplicates and partitions and leads TF-IDF training, Naive Bayes/Logistic Regression comparison, cross-validation and model evaluation. Sanzhar supports preparation and independent cross-labeling and leads future inference, explanation, threshold/error analysis and API/privacy integration. Responsibilities follow the individual role justifications and the proposal.

## 2. Language and task requirements

The output labels are `spam` and `ham`. Spam includes unsolicited promotional solicitation and deceptive or abusive solicitation, including phishing. Ham includes legitimate personal communication and requested or otherwise legitimate transactional/commercial communication. Unresolved cases receive a review status, never a forced binary label; see Annotation Guidelines Sections 2–8.

The user-facing language names EN/RU/KZ correspond to record codes `en`, `ru` and `kk`. Additional values are `mixed`, `und` (undetermined) and `other`. Script is a separate attribute: Cyrillic, Latin, mixed or other. Cyrillic alone does not distinguish Russian from Kazakh. Interface language is not evidence of message language or classifier support.

Real SMS with both classes is needed for each language's evaluation. Counts, class proportions and collection dates are unknown until intake. Translated English examples cannot establish native RU/KZ performance. Mixed-language and transliterated records require explicit review rather than automatic exclusion or assumed translation equivalence.

## 3. Candidate sources and verified evidence

The following publisher pages were checked on 24 October 2026. Verification is limited to visible metadata and documentation; it does not include corpus inspection, independent label validation or a completed permission review. Corpus ingestion and independent annotation remain planned.

| ID and candidate | Verified information and reference | Permission evidence | Proposed disposition and unverified matters |
|---|---|---|---|
| S-01: UCI SMS Spam Collection, EN | UCI describes labeled SMS, reports 5,574 instances and identifies several contributing collections, including NUS [R1] | UCI lists CC BY 4.0 | Preferred English baseline candidate. Check actual bytes, encoding, row count, labels, duplicates and privacy before admission; the reported count is not a project inventory count |
| S-02: SMS Spam Multilingual Collection, including RU | The publisher card describes translations derived from English SMS and shows a Russian text field [R2] | The page displays the generic tag `gpl`; the precise license version and upstream/translation conditions have not been resolved | Defer ingestion. If cleared and language-reviewed, consider a separate training augmentation experiment. Preserve links to English parents; exclude translations from the primary native-language validation/test sets |
| S-03: TeleSpam, RU | The creator describes Russian Telegram data with some generated spam; file access requires accepting conditions [R3] | The card states CC BY-NC 4.0; gated conditions and underlying message permissions still need review | Exclude from the SMS baseline. A later separately identified domain-transfer experiment would require permission and provenance review; Telegram labels are not SMS ground truth |
| S-04: KazSpam v1, KZ | The creator describes web-crawled Kazakh-focused texts and automatic `normal`, `casino`, `porn`, `other` labels [R4] | The page lists Apache-2.0; underlying source permissions have not been independently checked | Exclude from the SMS baseline: domain and labels differ. Do not map `normal` to SMS ham or all other categories to SMS spam |
| S-05: prospective opt-in native SMS contributions, especially RU/KZ | A proposed collection route, rather than an existing corpus; intake and review are specified in Sections 4, 6–7 and Annotation Guidelines Sections 12–15 | No contributor permission or institutional approval is claimed | Preferred route to fill native RU/KZ gaps after consent, privacy and collection arrangements are approved. Volumes and availability remain unknown |

S-02–S-04 provide verifiable leads and explicit exclusion/deferment decisions. Their discovery does not close the native RU/KZ SMS gap. This review has not established a reusable native Kazakh SMS spam/ham benchmark; it does not claim that no such dataset exists.

## 4. Provenance, licensing and use permission

Maintain a source register before importing any records. Each entry must contain the publisher, original URL/DOI, access date, immutable revision or retrieval identifier, artifact SHA-256, documented collection method, language/domain, original label policy, license text/reference, attribution and permitted operations. Record training, internal evaluation, text redistribution and model/artifact publication separately as `approved`, `pending` or `not permitted` with supporting evidence.

A visible license tag does not resolve every upstream permission or personal-data concern. Public visibility and availability through a mirror do not by themselves authorize reuse. S-01's attribution must accompany permitted derived releases. S-02 remains pending until its license version, derivation chain and translation terms are understood. S-03 requires review of noncommercial and gated conditions. S-04's declared license does not establish suitability or settle each underlying source's rights. Preserve restrictions at record level when sources are combined.

For S-05, agree an intake notice before collection: purpose, voluntary participation, intended internal training/evaluation, access, retention, withdrawal procedure and separate optional publication permission. A contributor must be authorized to share a message; their agreement does not automatically authorize retaining information about other people. Store contact/permission evidence separately from pseudonymous dataset records. Do not collect inbox exports, passwords, active authentication codes, identity documents or unnecessary third-party details. Required university procedures and the concrete retention period must be resolved before collection starts.

## 5. Source suitability comparison and selection rationale

| Criterion | S-01 | S-02 | S-03 | S-04 | S-05 |
|---|---|---|---|---|---|
| SMS domain | Yes, documented | SMS-derived translations | Telegram | Web documents | SMS required at intake |
| Target language contribution | EN | RU augmentation candidate | RU transfer candidate | KZ domain research only | Native RU/KZ sought; EN also possible |
| Binary-label compatibility | Audit upstream labels | Translation and label audit needed | Domain-specific policy differs | Four categories do not match | Apply project guidelines |
| Access/use readiness | License documented; intake audit pending | Terms unresolved | Gated; terms pending | Source review pending | Consent process pending |
| Main evaluation eligibility | Candidate after audit | No | No | No | Candidate after permission and annotation |

Select S-01 for an initial English feasibility baseline after its audit. Prioritize S-05 for representative RU/KZ data. Keep synthetic, translated and other-domain material separately identifiable and outside primary validation/test evidence. This selection is based on suitability and verifiability, not assumed dataset size or reported classifier scores.

## 6. Inclusion, exclusion and collection procedure

Admit only permitted SMS text that can be decoded, reviewed for privacy, assigned a language status and given a defensible final binary label. Store the provider's label separately from the project's decision. Preserve ordinary spelling, slang, emojis, punctuation and legitimate commercial messages so cleaning does not erase difficult cases.

Quarantine missing permissions, label conflicts, unresolved consent-dependent marketing, uncertain language requiring assistance, damaged text and privacy failures. Exclude non-SMS documents from the primary corpus, empty records, inaccessible attachments and examples whose meaning cannot survive necessary redaction. Screenshots require permitted, checked transcription; do not infer text from an unreadable image. Record every exclusion reason.

For native contributions, recruit voluntarily across intended language and message types, without asserting population representativeness. Seek both wanted messages and unwanted messages, avoiding a spam-only collection. Record recruitment route, time window and selection instructions; never silently choose only easily classified examples. Contributor availability, sample targets and collection schedule require review.

## 7. Inventory, metadata and storage layers

Use UTF-8 JSONL for the prospective restricted record exchange; embedded newlines remain escaped. A later CSV export must quote text correctly. The minimal logical schema is:

| Fields | Purpose and constraints |
|---|---|
| `record_id`, `source_id`, `source_record_id`, `source_revision` | Stable pseudonymous identifier and retrieval lineage; no email/phone-derived public ID |
| `domain`, `origin_type`, `parent_record_id` | `sms` or explicitly separate other domain; `natural`, `translated` or `synthetic`; link derivatives to parents |
| `text_redacted`, `model_text`, `preprocessing_version` | Privacy-reviewed annotation text and deterministic model input |
| `language`, `language_components`, `script`, `language_review_status` | Primary reporting bucket and reviewed language/script evidence |
| `source_label`, `label_origin`, `annotation_status`, `final_label` | Preserve upstream labels; final label only `spam`/`ham` or null while unresolved |
| `annotation_batch_id`, `guideline_version`, `annotation_record_refs` | Link independent decisions and adjudication without exposing personal annotator details |
| `permission_ref`, `use_status`, `privacy_status`, `redaction_version` | Restricted evidence references and admission gates |
| `contributor_group_id`, `duplicate_group_id`, `campaign_group_id`, `leakage_group_id` | Pseudonymous related-record groups, with unavailable contributor metadata explicitly null |
| `exact_fingerprint`, `split`, `dataset_version` | Restricted equality check and frozen assignment |
| `received_at`, `collection_period`, `exclusion_reason` | Audit timing; use coarse dates unless finer timestamps are necessary and permitted |

Original received content, where temporary retention is permitted, stays in restricted intake storage. The working corpus contains reviewed redacted text. Split manifests and evaluation artifacts remain restricted where their IDs or fingerprints could expose records. Public documentation contains aggregate counts, reproducibility instructions and synthetic examples; it does not contain the private intake, consent register or raw messages. Directory names in the repository do not grant permission to store personal data there.

## 8. Unicode and normalization

Decode each source using a verified encoding; attempt strict UTF-8 first when appropriate, and explicitly record any alternative. Do not use a Latin-1 fallback merely to suppress decoding errors. Quarantine mojibake, unpaired surrogates or replacement-character corruption for review.

Normalize text to NFC following Unicode normalization terminology [R5]. Preserve Kazakh letters such as `ә`, `ғ`, `қ`, `ң`, `ө`, `ұ`, `ү`, `һ`, `і`, Russian `ё`, Latin letters and diacritics. Do not transliterate, strip accents or replace all Cyrillic with Latin lookalikes in the baseline. NFKC or homoglyph folding may be considered only as separately versioned development experiments.

Normalize line endings; trim outer whitespace and collapse internal whitespace to a single space for `model_text`. Detect control and invisible characters, retaining a restricted flag and applying a documented deterministic mapping. Remove transport artifacts such as a leading byte-order mark; do not silently erase meaningful emoji sequences or text. Casefold only the model/deduplication view; retain readable case in `text_redacted` and preserve offset mappings for explanations.

## 9. URLs, numbers, symbols and sensitive spans

The proposed baseline uses deterministic privacy transformation before feature extraction at both training and inference. Replace full URLs, email addresses and phone numbers with `__url__`, `__email__` and `__phone__`. Replace identified account identifiers, authentication codes and personal names/addresses with typed placeholders such as `__account__`, `__otp__`, `__person__` and `__address__`. Apply span detection before whitespace/case changes; specify overlapping-pattern precedence and regression fixtures when implementing the transformation.

Preserve ordinary prices, percentages, dates, currency markers, punctuation and emojis when they do not identify a person. A bare digit sequence is not automatically a phone number: use documented patterns and contextual review during intake. If an ambiguous number cannot safely be retained, mask it and record the reason. Redaction must not erase the solicitation's meaning; quarantine examples that become unusable or contradict another identical model input.

Do not follow URLs, preserve tracking identifiers or request live codes for annotation. Whole-URL masking sacrifices domain cues; that limitation must be evaluated on development data. Automatic detection will miss some personal information, so human privacy review remains necessary for training admission. No claim of anonymization follows from placeholders alone. API text can be processed transiently, while any retained feedback text requires separate consent and privacy review. The final deterministic rules and explanation-offset behavior must be agreed with Sanzhar before implementation.

## 10. Multilingual preprocessing sequence

The intended sequence is permission screening → strict decoding → Unicode/control checks → privacy review/redaction → readable annotation view → deterministic model normalization → duplicate/campaign analysis → final annotation decisions → group partitioning → training-only learned transformations.

Do not remove stopwords, apply stemming or lemmatization, discard short words or filter to an English alphabet in the baseline. These operations can remove useful negation or distort RU/KZ morphology. Any later alternative must use identical held-out boundaries and be selected with development data. Metadata, language labels, source identifiers and annotation rationales are not text features in the baseline. The same versioned deterministic transformation must serve single-message and batch inference.

## 11. Exact and near-duplicate detection

Compute exact equality on NFC/casefold/whitespace-normalized, privacy-transformed text across all sources. Store a SHA-256 fingerprint only in restricted manifests; a message hash is not proof of anonymity. Check for collisions by comparing the underlying permitted normalized strings. Keep one canonical training/evaluation record for identical content while retaining all provenance links and multiplicities. Conflicting labels must be adjudicated, never resolved by majority deletion.

For near-duplicate candidate generation, use a separate deterministic template view that also replaces variable digit runs with `__num__`. Compare sets of character 5-grams using Jaccard similarity `|A ∩ B| / |A ∪ B|`. An initial candidate threshold of 0.85 is proposed for messages at least 30 normalized characters long. Manually review shorter messages, shared templates and candidate pairs before confirming a group. This threshold is a preparation heuristic, not a classifier acceptance target; calibrate it on pilot/development material, record decisions and freeze it before test reservation.

Retain meaningful campaign variants but group them. Do not merge messages solely because they share a placeholder, language, brand or common greeting. Pair review should check template/meaning, length and false merges, including transitive chains that produce unusually large groups. Record the method/version, candidate scores and confirmed edges. If scalable candidate indexing is later used, document its recall audit rather than assuming every near-duplicate was found.

## 12. Campaign and derivative grouping

Before partitioning, create an undirected relation graph linking confirmed exact/near duplicates, known campaign variants, translated/synthetic derivatives and their originals, and records from the same pseudonymous contributor where that information is available. The connected components form `leakage_group_id`. Groups can cross sources and languages.

Use permitted collection evidence and redacted template patterns to establish campaign links; do not retain raw sender numbers or secret identifiers just for grouping. Unknown campaign/contributor links remain a stated limitation. Keep group identifiers out of model features. All records in a component belong to one partition, even when desired class/language ratios become less exact. Group membership does not prove that every member has the same label.

## 13. Class imbalance

Report message and independent-group counts by class, language, source and partition before selecting remedies. Prefer natural validation/test proportions within the documented collection process; do not oversample or artificially balance those sets. A volunteer corpus still does not estimate deployment prevalence.

Compare an always-ham baseline with the planned classifiers. Rafael can compare Logistic Regression class weighting or training-only resampling; Sanzhar contributes threshold/error analysis. Apply resampling only inside each training fold after partitioning. Do not insert copies or synthetic examples into validation/test. The initial text baseline does not require SMOTE. Select remedies and thresholds using the same development protocol and report false positives as well as missed spam.

## 14. Mixed-language and transliterated SMS

Assign one primary reporting bucket per message. Use `mixed` when at least two languages contribute substantive meaning; a URL, brand or isolated borrowed word is insufficient. Store the language components and optional dominant language separately. If a competent reviewer can identify transliterated Russian or Kazakh, use `ru` or `kk` with `script=Latin`; otherwise retain `und` pending review.

Do not automatically translate or transliterate the baseline input. Keep natural spelling and code-switching. Report mixed-language performance separately and disclose which transliterated examples occur within the RU/KZ buckets. Synthetic/transformed variants retain their origin flag and parent relation. They cannot replace natural test messages or increase the reported independent sample size.

## 15. Training, validation and test partitions

Use 70% training, 15% validation and 15% held-out test as proposed message-count targets, with seed `42`. Actual ratios depend on indivisible groups and will be reported. Split only admitted, finalized records. Place annotation-pilot groups used to refine the policy in training only; they must not enter primary validation/test.

The planned assignment procedure is:

1. Sort stable group IDs and record each group's class × primary-language counts, sources and eligibility. Establish grouping without fitting a vocabulary or examining model errors.
2. Using one pseudorandom generator initialized with seed `42`, generate 100 permutations of the sorted natural-message groups; record the generator/library version. Preassign pilot groups to training. In each permutation, place each remaining group into the eligible partition minimizing the current sum of `abs(actual_count - target_count) / max(1, target_count)` over partition totals and partition × class × language cells. Break placement ties in training, validation, test order. Among completed assignments with both classes in each claimed language's validation/test sets, choose the lowest final sum, then the earliest permutation on a tie. Selection uses counts and constraints only, never model performance. Record the implementation revision and selected assignment.
3. Require natural, permitted SMS in primary validation/test. Derivatives and other development-only records are training-only; if their parent is reserved for evaluation, omit those derivatives rather than moving the parent or splitting the family. Do not add derivatives until natural-record assignments have been frozen.
4. Complete independent annotation/review for every proposed primary validation/test record before locking the split. Label corrections that change allocation require a documented rerun before any model evaluation, not a quiet replacement after seeing results.
5. Verify pairwise-disjoint IDs, exact fingerprints and leakage groups; publish restricted manifests and aggregate count tables with deviations and missing cells.

This is a proposed algorithm specification, not an implemented splitter. Rafael must review feasibility before freezing a dataset. If a class/language lacks independent groups, or giant connected groups make a feasible split impossible, report the affected language as not evaluable and collect more data or revise the protocol through review. Do not break groups, fabricate samples or search seeds for better scores. Chronological evaluation can be a later separate design only when trustworthy time metadata exists.

## 16. Protected held-out set

After permission, annotation and grouping checks, freeze the test manifest, redacted texts, final labels and hashes under restricted access. Beknur maintains the data register; Rafael leads the evaluation procedure. Record access and designate a test custodian so model selection does not use test text, labels, errors or feature statistics. Aggregate support checks are allowed; tuning against test observations is not.

Freeze preprocessing, feature configuration, classifier, calibration and decision threshold before the final test run. Evaluate the selected pipeline and predeclared baseline under the same conditions. Inspect errors only after the result is recorded. Once test findings inform revisions, describe subsequent results as reuse of an exposed benchmark and obtain a new independently reserved set for fresh confirmatory claims. Withdrawn, corrupted or leaked test records require a versioned correction and disclosure; never replace difficult test items to improve metrics.

## 17. Group-aware cross-validation and leakage controls

Use group-aware folds within training only, initially aiming for five folds if independent class/language groups permit. Composite class/language strata may be used to approximate coverage; `StratifiedGroupKFold` is a candidate implementation with non-overlapping groups, not a guarantee of exact balance [R7]. Verify that both classes are present in the training partition and in each CV training fold; language-specific models require this check within each modeled language. Reduce the fold count with a recorded rationale if needed; if adequate class support remains unavailable, defer the affected experiment until sufficient independent data is available. Do not fall back to overlapping row-wise folds.

Place TF-IDF vocabulary/IDF, feature selection, learned normalization, resampling and estimator fitting inside the training-fold pipeline. Validation transforms use fitted training objects; test data is transformed only by the frozen pipeline [R6]. Fixed Unicode/privacy rules and duplicate grouping are corpus preparation, not corpus-wide statistical fitting. Do not learn redaction dictionaries, similarity thresholds or language routing from held-out model errors.

Use training CV for parameter comparisons, then validation for final configuration, threshold and any calibration. If development data is later combined for a final refit, document a leakage-free calibration/threshold protocol before test access; the simpler initial protocol retains the 70% training fit. Newly contributed feedback must be checked against all frozen evaluation groups and quarantined from training if related. Freeze test labels separately from subsequent feedback adjudication.

## 18. Reproducibility and dataset versioning

For each prospective dataset release, record source revisions and hashes, allowed-use register version, intake/exclusion counts, annotation/guideline versions, redaction/normalization and grouping configurations, seed, splitter implementation, dependency versions and immutable split manifests. Record the Unicode/runtime version as case handling and text processing can change between environments.

Use a version such as `sms-en-ru-kk-v0.1` only when an actual artifact is created. Any label, membership, redaction or split change creates a new version and changelog entry; do not mutate an evaluated dataset in place. Hash restricted artifacts for internal integrity and expose only public-safe summaries. Reproduction by an authorized reviewer requires access to the permitted artifacts or documented retrieval process; publishing a hash alone is insufficient.

## 19. Word and character n-gram representations

The planned baseline compares word TF-IDF unigrams/bigrams with character TF-IDF n-grams, initially lengths 2–5. `char` and `char_wb` are candidate analyzer alternatives [R8]. These are proposed configurations to test on development data, not proven choices. Avoid a fixed English stopword list and preserve non-English letters.

Beknur leads character-feature experiments; Rafael integrates the fair representation comparison and estimator tuning. Record tokenization, minimum/maximum document frequency, vocabulary limits, normalization, n-gram ranges and placeholder behavior. Fit all vocabulary statistics only on the current training fold. Character features may help handle spelling/morphology, but no RU/KZ performance benefit is claimed before evaluation. Keep the fixed character shingles used for duplicate detection distinct from learned TF-IDF features.

## 20. Classifier and inference compatibility

Provide sparse non-negative TF-IDF features compatible with Multinomial Naive Bayes and Logistic Regression. Compare identical data versions, folds and metrics. A pooled multilingual model versus separate language-specific models remains an experimental choice; do not silently introduce routing or claim support based on translated training examples.

The future training-to-service handoff must identify the dataset/split, preprocessing, representation, estimator, label mapping, threshold, calibration and explanation versions. Sanzhar's API must use the same deterministic transformation and fitted feature extraction as training. Output labels remain `spam`/`ham`; display-language translation does not change their meaning. Explanations must map actual word/character contributions to visible input without exposing private spans or inventing reasons for masked content. Probability and confidence need validation; neither is evidence that a message or URL is safe.

## 21. Per-language evaluation readiness

For EN, RU and KZ separately, report admitted natural SMS counts, spam/ham support, independent groups, sources and coverage gaps. Each record contributes to one primary language bucket only; mixed-language records have their own table. Additional script slices must be labeled as overlapping subgroup analyses. Do not pool translated and natural-message results under a native-language heading.

Rafael's evaluation will report spam precision, recall and F1, a confusion matrix with order `[ham, spam]`, and actual denominators; Sanzhar leads threshold and false-positive/false-negative interpretation. Missing classes or zero metric denominators must be explicitly marked, with any library zero-division convention stated. Accuracy alone is insufficient. Estimate uncertainty using group-aware resampling where enough independent groups exist; otherwise disclose instability rather than presenting a narrow interval. Results describe this corpus and collection procedure, not universal Kazakhstan-wide accuracy.

## 22. Dataset quality assurance and release checks

Before releasing data to model development, verify the following and retain the actual outcomes:

- Every admitted record has supported provenance, approved intended use, privacy review and a final label with traceable origin.
- Text decodes correctly; Kazakh/Russian letters survive normalization; redaction preserves task meaning; schemas and IDs are valid.
- Inventory counts reconcile intake, exclusions, canonical duplicates and retained variants by source/language/class.
- Independent judgments, agreement and adjudication meet the documented annotation procedure; no invented scores or post-adjudication agreement substitutes are used.
- Exact/near duplicates, parents, contributors and campaigns have been checked across all sources and partitions; any unknown links are disclosed.
- Split constraints hold, held-out access is controlled and training-only origins stay outside primary evaluation.
- Dataset/configuration hashes and versions are fixed; permitted-reviewer reproduction instructions and publication restrictions are available.

These checks assess dataset readiness. Failed checks block the affected records or release and produce a correction log.

## 23. Privacy and security throughout the lifecycle

Treat every message as untrusted text. Do not open links, execute content, render it as HTML, or send private examples to public translation/annotation services. Restrict access by role; protect intake and working storage; keep permission evidence separate; and set access, retention and deletion arrangements before collection. Review exported text and model artifacts for unintended retained vocabulary or personal details before publication.

Runtime prediction remains transient by default, with metadata-only history under the proposal. An error flag does not authorize storing the message or retraining on it. Text-bearing feedback needs separate informed consent, privacy screening, independent label confirmation, duplicate checks and a versioned offline release. Rafael leads controlled retraining behavior; Sanzhar leads safe API/storage handling; Beknur supplies the corresponding consent/review UI. No live model learns directly from public feedback.

Retention periods, withdrawal handling and storage implementation remain decisions for the owners and supervisor. Approved research use does not automatically permit public redistribution. Demonstrations and public documentation use synthetic messages, never private student records or unreviewed SMS.

## 24. Limitations, dependencies and review decisions

| Outstanding matter | Required next evidence or decision | Lead and support |
|---|---|---|
| Native RU/KZ SMS coverage and both-class support | Approved collection route, real inventory and independent annotation | Beknur; Sanzhar cross-labeling, Rafael feasibility review |
| Candidate source terms | Source register with exact terms, revisions and permitted operations; resolve S-02 or exclude it | Beknur; supervisor/provider clarification where needed |
| Privacy and retention | Approved intake notice, retention/withdrawal rules and working-storage access | Beknur data process; Sanzhar privacy/storage; Rafael feedback behavior |
| Redaction and feature offsets | Reviewed deterministic rules and training/inference compatibility checks | Beknur and Sanzhar; Rafael pipeline review |
| Duplicate grouping and split feasibility | Audited groups, actual support counts and reproducible assignment | Beknur; Rafael technical review |
| Annotation capacity and competence | Independent language-competent reviewers and pilot records | Beknur; Sanzhar cross-labeling, Rafael technical review |
| Model/language support | Development-only comparison and later untouched natural-message evaluation | Rafael; Beknur features, Sanzhar threshold/API analysis |

DIP-2 findings and supervisor feedback may refine collection scenarios. They are not assumed complete. No collected volumes, completed labeling, agreement scores, trained models or multilingual results are claimed.

## 25. References

Publisher metadata and technical guidance were consulted on 24 October 2026. Dataset-card assertions remain publisher assertions until corpus intake verifies them. The workflow parameters in this document are project proposals.

- **R1.** Almeida, T. and Hidalgo, J. *SMS Spam Collection*. UCI Machine Learning Repository. [Dataset record and license](https://archive.ics.uci.edu/dataset/228/sms+spam+collection), DOI: [10.24432/C5CC84](https://doi.org/10.24432/C5CC84).
- **R2.** dbarbedillo. *SMS Spam Multilingual Collection Dataset*. [Publisher dataset card](https://huggingface.co/datasets/dbarbedillo/SMS_Spam_Multilingual_Collection_Dataset). Translation lineage and displayed license tag; exact reuse terms remain pending.
- **R3.** AugustLight. *TeleSpam: Russian Telegram Spam Detection Dataset*. [Creator dataset card](https://huggingface.co/datasets/AugustLight/telegram_spam_ru). Telegram domain, generated data and stated use restrictions.
- **R4.** salyamq. *KazSpam v1*. [Creator dataset card](https://huggingface.co/datasets/salyamq/kazspam-v1). Web-text domain, automatic labels and declared license.
- **R5.** Unicode Consortium. [Unicode Standard Annex #15: Unicode Normalization Forms](https://www.unicode.org/reports/tr15/).
- **R6.** Scikit-learn developers. [Common pitfalls: data leakage](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage).
- **R7.** Scikit-learn developers. [StratifiedGroupKFold](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.StratifiedGroupKFold.html).
- **R8.** Scikit-learn developers. [Text feature extraction](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction).