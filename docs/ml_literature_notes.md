# Critical Scientific Review of Machine Learning for Multilingual SMS Spam Detection

**Project:** Development of a Web-Based SMS Spam Detection Application Using Machine Learning, SE-2425.

**Task:** [DIP-12 — Critically review ML scientific literature](https://sms-spam-se2425.youtrack.cloud/issue/DIP-12), plan step S05.

**Date:** 24 October 2026.

**Responsible student:** Rafael Shayekhov.

**Status:** Prepared with Codex assistance for substantive student and team review. Rafael's personal verification, scientific interpretation and actual contribution remain to be confirmed. No project experiments or peer approval are reported.

## 1. Introduction

SMS spam detection is a supervised classification problem in which the observable message text provides incomplete evidence about whether communication is unwanted. Short messages offer few lexical observations, often omit context and may contain informal spelling, abbreviations, links, numbers and mixed scripts. A model can consequently learn collection-specific templates instead of transferable evidence. Research on SMS phishing campaigns illustrates repeated content and infrastructure [3], while the English UCI collection documents heterogeneous contributing sources [14]. These characteristics make the unit of evaluation and independence of examples central scientific questions.

The binary labels follow the team's [Annotation Guidelines](annotation_guidelines.md): `spam` covers unsolicited promotional or deceptive/abusive solicitation; `ham` covers legitimate personal, requested transactional and supported subscribed communication. Phishing is a subset of the project's positive class. `uncertain` and `unusable` are annotation workflow states excluded from scored binary data until resolved. The same commercial wording may be wanted by one recipient and unwanted by another. A text-only classifier cannot recover absent consent or transaction context; withholding unresolved examples also narrows the population to which its eventual results apply.

The proposed browser application offers manual checking and model-based explanations. Its practical utility and acceptable error costs remain user-research questions under DIP-2. A false positive can mislead a user about legitimate communication; a false negative can leave an unwanted solicitation unrecognized. Neither a ham prediction nor a high score verifies sender authenticity or link safety. This review supports the ML decisions in the [Project Proposal](project_proposal.md), rather than claiming demonstrated application effectiveness.

English, Russian and Kazakh require separate evaluation because lexical coverage, morphology, source composition and class distributions can differ. Kazakh task evaluation [8] and Kazakh–Russian translation research [7] motivate language-sensitive assessment, but neither establishes SMS spam performance. The research question is therefore whether reproducible sparse-text baselines provide useful error trade-offs on permitted natural messages in each target language, including explicitly identified mixed-language cases.

## 2. Literature Search and Selection Methodology

### 2.1. Scope and actual search procedure

This focused narrative review extends [DIP-9's general literature review](literature_review.md). The existing bibliography was the starting candidate set; its reported verification was checked against primary records and relevant text rather than accepted as evidence of a new inspection. Targeted web search and direct source retrieval were performed on 24 October 2026. Actual discovery queries included `site.scikit-learn.org "Multinomial Naive Bayes" "tf-idf"`, `site.scikit-learn.org "Logistic regression" "sparse"` and `site.scikit-learn.org "Probability calibration" "Brier"`. Search results supplied leads; secondary tutorials and search snippets were not used as scientific evidence.

Publication records and selected sections concerning methods, results or limitations were inspected through ACL Anthology, the JAIR journal site, PMLR, PubMed Central, an author's publication page/PDF, arXiv and the official Europe PMC full-text XML service. UCI, scikit-learn and Unicode documentation were checked for implementation and resource claims. No subscription database search in Scopus, Web of Science or IEEE Xplore is claimed; the IEEE paper was checked through its author-hosted text and bibliographic record. This procedure is neither an exhaustive systematic review nor a meta-analysis. Screening totals, experiment reproduction and complete reading of every page are not claimed.

| References | Evidence inspected in this review | Verification boundary |
|---|---|---|
| [1], [4], [6]–[8], [11] | ACL-hosted papers; publication records where retrieved; relevant task, corpus and evaluation descriptions | Publication evidence, not independent reruns or corpus audits |
| [2] | Published PMC text, dataset description and Tables 2, 11, 13–15 | Reporting inconsistencies are retained; superiority is not assumed |
| [3] | Author-hosted paper and author publication record, including IEEE venue and DOI | Gateway observations do not establish deployment prevalence |
| [5] | arXiv version 1, including collection and classification sections | Treated as a preprint; a peer-reviewed venue was not verified |
| [9], [12] | JAIR and PMLR primary papers, including publication information and evaluation rationale | Findings concern their study settings |
| [10], [13] | Published article metadata, abstracts and relevant body sections retrieved from official Europe PMC XML | PMC HTML/publisher routes failed or were restricted; the XML retrieval succeeded |
| [14]–[21] | Official dataset record, software guides and Unicode annex | Documentation establishes definitions/capabilities, not classifier quality |

During this revision on 24 October 2026, all 31 URLs in the corrected bibliography were requested again and their content types and response content were checked. Thirty responses contained recognizable publication records, extractable PDFs, article XML or official resource/documentation pages. The direct PMC HTML request for [2] returned a CAPTCHA page despite HTTP 200; that response did not provide the article. The numerical claims in [2] were separately re-inspected in the published primary text exposed through web retrieval. Bibliographic discovery, page availability, inspected primary sections and experiment reproduction are distinct evidence levels; a successful HTTP status does not establish source reading or scientific validity.

The current numerical recheck covered [2]'s dataset description and Tables 2, 11, 13–14; [3]'s abstract; [4]'s Table 2; [7]'s introduction and dataset description/Table 2; and [8]'s abstract and introduction. These sections support the quoted counts and scores in Section 8. Direct access to [4]'s PDF initially failed through the web tool, but following the PDF link from its official ACL record exposed the primary table; a screenshot request failed, so this check used extracted text. For [21], the fixed revision 57 header was inspected directly. The earlier source inspections recorded above are retained as prior-pass evidence, without implying that every paper was read in full again.

The supplied `requirements (1).docx` was opened by extracting its document XML. Its literature-review row requires at least 12 meaningfully used sources, including at least eight scientific publications, critical comparison and an appropriate recent core with foundational exceptions. The supplied `SE2425_YouTrack_Predzashchita1_Posledovatelnyj_Plan.pdf` was text-extracted; pages 4 and 7 were rendered, and the S05 card on page 7 was visually inspected. It identifies this file as the ML-literature deliverable. The PDF is the team's operational roadmap; it is not an additional scientific publication. These local assessment materials and repository documents are contextual evidence, excluded from the literature counts below.

### 2.2. Selection, publication status and recency

Inclusion required identifiable authors, a stable primary record, inspectable evidence and a specific role in understanding SMS classification, target-language limitations, data validity or model interpretation. Earlier foundational studies were retained for simple classifiers [1], code-switching concepts [6], calibration [12] and explanation diagnostics [13]. Exclusions cover unverifiable citations, inaccessible findings without a usable primary alternative, unrelated benchmarks used merely to enlarge the bibliography and duplicate versions of the same work. Other-domain studies remain included only with an explicit transfer limitation.

The bibliography contains **21 external reference entries: 12 published scientific papers** ([1]–[4], [6]–[13]), **one scientific preprint** ([5]), **one dataset record** ([14]), **six technical guide pages** ([15]–[20]) and **one technical standard** ([21]). The six technical pages belong to one scikit-learn User Guide; counting that guide once gives **16 distinct works**, rather than 21 independent works. The 12 published research papers are distinct publications under either convention. Published conference/workshop and journal research is distinguished from preprints and documentation. Technical pages do not count toward the eight-publication minimum. References [1]–[16] preserve DIP-9's numbering for the shared works; [17]–[21] supply directly used algorithm, calibration and normalization details. DIP-9's accessibility reference is outside this ML supplement's bibliography; its number [17] is not reused as a cross-document identifier. Numbers in this document are local.

The rolling five-year window is **24 October 2021–24 October 2026**. Eight of the 12 published papers fall within it: [2]–[4], [7]–[11]. The December 2021 paper [9] qualifies; the August 2021 and April 2021 papers [6], [13] do not. Thus the recent published core is 8/12, while four earlier works have stated methodological roles. Adding the 2024 preprint gives nine recent works among 13 scientific works. Access dates on undated software pages are not publication dates. Recency and source counts describe this selected evidence set, not comprehensive coverage of the field.

## 3. Classical Machine Learning Approaches

### 3.1. Representation and short-message constraints

TF-IDF transforms a message into a sparse non-negative vector. Term frequency is weighted by inverse document frequency computed from the fitted corpus; smoothing and vector normalization are configuration choices [15]. Word unigrams capture individual terms, while bigrams add adjacent lexical context. Character n-grams describe local substrings; `char` and boundary-aware `char_wb` define different feature spaces. These representations encode surface evidence rather than contextual semantic equivalence. A fixed vocabulary also leaves unseen features unrepresented.

The team's [Dataset Strategy, Section 19](dataset_strategy.md#19-word-and-character-n-gram-representations) proposes word unigrams/bigrams and character lengths 2–5. Their benefit for native RU/KZ SMS is a **team hypothesis**. Character overlap might share evidence across inflections or spelling variants, but can also memorize campaigns, redaction placeholders and source-specific fragments. Bigrams may preserve a short warning phrase while increasing sparsity. Very short messages may yield few usable features under either representation. A zero-vector input still receives a mathematical model score, which alone cannot establish evaluated language coverage.

**Planned representation comparison:** record analyzer, token rules, n-gram range, `min_df`, `max_df`, vocabulary cap, term-frequency scaling, IDF smoothing and norm explicitly. Compare word and character features on the same frozen groups. Audit whether token rules discard single-character tokens or split typed placeholders, and whether vocabulary filtering disproportionately removes minority-language evidence. These are implementation and empirical checks, not published RU/KZ gains. The baseline retains Unicode letters and avoids stemming, lemmatization and a fixed English stopword list, as already specified by DIP-4.

### 3.2. Multinomial Naive Bayes

Multinomial Naive Bayes (MNB) estimates class priors and smoothed class-conditional feature frequencies [17]. For class `c` and vector `x`, the decision score has the form:

```text
s_c(x) = log P(c) + sum_j x_j log theta_cj
theta_cj = (N_cj + alpha) / (sum_k N_ck + alpha * V)
```

Here `N_cj` is accumulated training feature mass, `V` is vocabulary size and `alpha > 0` controls smoothing. The conditional-independence assumption gives a compact additive rule. TF-IDF is a supported practical input, although fractional, normalized weights are not literal multinomial token counts. Non-negative inputs must be preserved; centering into negative feature values would violate this configuration's requirements [17].

MNB is attractive as an inexpensive baseline when training resources are limited. Its principal scientific limitation is the independence assumption: correlated unigrams, bigrams or overlapping character features can count related evidence repeatedly. This motivates a calibration check, not an assertion that this untrained model is miscalibrated. Rare features depend strongly on smoothing, and training priors need not match future prevalence. Both classes and representative linguistic variation are needed to assess useful discrimination. An ability to produce predictions from little data is not evidence that their generalization is reliable.

### 3.3. Logistic Regression and its comparison with MNB

Binary Logistic Regression (LR) directly models conditional class probability through a linear score and logistic link [18]:

```text
z(x) = b + sum_j w_j x_j
p_model(spam | x) = 1 / (1 + exp(-z(x)))
objective = weighted training log loss + regularization penalty
```

Unlike MNB's separate class-frequency estimates, LR learns coefficients jointly against a discriminative loss. Regularization can constrain rare or correlated features, but does not make their coefficients stable causal explanations. Its linear decision surface still lacks arbitrary semantic interactions unless the representation encodes them. Useful training requires both classes, sufficient independent examples and attention to convergence. Regularization strength, solver, stopping tolerance and weighting are model-selection choices [18].

The following comparison is an analytical interpretation of the decision rules and the project's constraints, rather than a measured ranking.

| Criterion | MNB | LR | Consequence for the planned comparison |
|---|---|---|---|
| Learning target | Estimates class priors and feature distributions | Optimizes conditional discrimination | Match feature/data versions before attributing a difference to the estimator |
| Dependence between features | Assumes conditional independence | Joint coefficients can accommodate correlation, without learning unrestricted interactions | Compare identical word/bigram or character configurations |
| Small-sample behavior | Smoothing limits zero-frequency problems; source artifacts remain learnable | Regularization limits coefficient growth; rare features and separation remain concerns | Report learning curves by independent groups where feasible; no presumed winner |
| Main controls | Smoothing, prior policy and representation | Regularization, solver, convergence and class/sample weights | Use a declared, comparable search budget and retain unsuccessful configurations |
| Scores | Posterior under the model assumptions | Logistic probability under the fitted conditional model | Neither output is automatically calibrated for future SMS |
| Incremental updates | Sufficient-statistic updates are computationally possible | Standard batch LR usually requires an offline refit | Both remain inside the project's reviewed offline lifecycle |
| Explanations | Class log-evidence differences | Signed coefficient × feature contributions | Explain the actual fitted decision, including its intercept/prior |

**Planned NB/LR experiment:** use matched training folds and a predeclared validation objective, inspect spam precision/recall and error types, and measure fitting/inference resources under the same conditions. Any class weighting or resampling changes the fitted objective/distribution and may alter probability interpretation. LR's probabilistic loss does not guarantee calibration under misspecification, regularization or domain shift. No choice between MNB and LR is established by the present review.

### 3.4. Linear Support Vector Machine

A linear SVM fits a separating score with a margin-based objective and regularization. `LinearSVC` is the relevant sparse linear candidate; it should not be conflated with nonlinear kernel SVC or with Wang and Manning's distinct NB-weighted SVM configuration [1], [19]. It offers an additional discriminative comparison without requiring dense contextual embeddings. Both-class support, an appropriate regularization value and convergence checks remain necessary. Noise near the boundary can affect the fit, and linearity imposes the same representation limitations discussed above.

The raw margin is not a spam probability. **Planned SVM experiment:** compare its classification behavior under the same partitions and representation, then evaluate a separate calibration procedure if it is considered for the probability-returning API. A candidate lacking validated score interpretation cannot silently replace the NB/LR response contract. Wang and Manning's feature- and task-dependent findings justify controlled baselines; their sentiment/topic experiments do not prove SVM or MNB superiority on SMS [1].

### 3.5. Computational and data requirements

Let `Z` be the number of non-zero training-matrix entries, `V` the vocabulary size, `K = 2` the number of classes, `s` the active features in one message and `E` the number of optimization passes. The estimates below are order-of-growth reasoning for sparse implementations, not measured runtimes or solver-independent guarantees. Shared vectorization costs must be included in a service benchmark.

| Component | Approximate work and storage | Data requirement and SMS-specific limitation |
|---|---|---|
| MNB | Accumulation and smoothing roughly `O(Z + K*V)`; parameters `O(K*V)`; scoring `O(K*s)` | Smoothed non-negative feature mass; sparse evidence and redundant features affect estimates |
| LR | Sparse gradient/pass roughly `O(Z + V)`; repeated passes and solver overhead; binary coefficients `O(V)` | Both classes, regularization and convergence; coefficient estimates can be unstable with little independent data |
| Linear SVM | Iterative sparse optimization; cost depends on solver, tolerance, sparsity and passes; binary linear parameters `O(V)` | Both classes and margin tuning; calibration adds fits and additional data requirements |
| TF-IDF | Vocabulary/document-frequency fitting plus sparse weighting roughly proportional to extracted features; matrix `O(Z)` and vocabulary `O(V)` | Representative training-only frequency statistics; rare variants and vocabulary caps can remove useful evidence |
| Word n-grams | For a fixed maximum n, extraction grows approximately with token count; vocabulary/storage can expand sharply | Repeated lexical contexts are needed; inflected and misspelled forms can fragment counts |
| Character n-grams | For length `L` and a fixed set of `r` lengths, about `O(L*r)` emitted windows; feature storage depends on distinct substrings | Less dependence on token boundaries, but more overlapping features and no automatic cross-language semantics |

**Planned resource measurement:** record vocabulary/non-zero counts, artifact size, training time, peak memory and preprocessing plus inference latency, separating cold loading from warm execution. These observations will inform integration with the [Architecture](architecture.md) and [Technology Comparison](technology_comparison.md); no latency target is inferred from another paper's hardware.

## 4. Multilingual SMS Spam Detection

### 4.1. English evidence and transfer boundaries

The UCI record documents a historical English collection assembled from several sources [14]. It is a useful feasibility candidate after intake checks, not a sample of current Kazakhstan SMS. Changes in solicitation tactics, brands, collection channels and message purposes can change both feature distributions and label relationships. This is the review's inference from heterogeneous study settings, rather than a measured transfer failure for this project.

Filali et al.'s multilingual extension uses machine-translated French, German and Hindi messages [2]. Translation can preserve the original campaign and label while changing lexical realization; it does not create independent native-language observations. Consequently, a high English UCI result cannot automatically establish Russian or Kazakh quality. It leaves native wording, local legitimate messages, code-switching, consent-dependent labels and class priors untested. Ali et al.'s locally collected Portuguese resource offers contrasting task/domain evidence, not a transferable numerical target [4].

### 4.2. Russian and Kazakh processing

For Russian, the planned engineering checks cover inflected forms, informal spelling, `ё`, transliteration, abbreviations and mixed Latin/Cyrillic text. For Kazakh, they cover suffix variation, language-specific letters and transliterated forms. The concern that surface-word vocabularies fragment such variation is a **team design hypothesis** motivating feature experiments; the selected papers do not quantify that effect for the team's SMS task. Stemming or lemmatization could also merge useful distinctions or fail on informal text. Such transformations require a separate development comparison instead of an assumed improvement.

Kazakh resource constraints are task-specific. Maxutov et al. assess seven LLMs across six task datasets and observe language/task-dependent capability [8]. This does not establish that larger models solve sparse Kazakh SMS classification or that a sparse baseline will fail. Borisov et al.'s Kazakh–Russian resource concerns translation of social text [7]. These studies support seeking competent linguistic review and appropriate data, while leaving the project's binary-label evidence unresolved.

### 4.3. Code-switching, Unicode and origin

Doğruöz et al. show why computational code-switching needs linguistic and social distinctions [6]. Consistent with DIP-4, `mixed` requires substantive meaning from multiple languages; a brand, URL or isolated borrowed item is insufficient. Codes `en`, `ru` and `kk` identify message-language buckets, while script and UI language are separate attributes. Each record enters one primary reporting bucket; script slices are overlapping secondary analyses.

Unicode NFC provides canonical normalization; compatibility normalization has different equivalence rules [21]. Reference [21] fixes a bibliographic version of the annex; it does not select the project's runtime Unicode version, which must be recorded when implemented. The baseline follows [Dataset Strategy Sections 8–10](dataset_strategy.md#8-unicode-and-normalization): strict decoding, privacy transformation and documented normalization, preserving Kazakh letters and Russian `ё`. It does not silently transliterate or fold lookalike characters. Casefolding and whitespace changes require versioned offsets for explanations. Malformed decoding must not be hidden by a permissive fallback.

**Planned multilingual comparison:** compare a pooled model with language-specific alternatives only where independent both-class support permits. Use identical external partitions and record routing, unknown-language and mixed-input behavior. Pooled training can share some patterns but can also favor the largest language; separate models reduce each model's available sample. Both statements are hypotheses to assess. Character sharing across scripts is not semantic alignment.

**Planned augmentation comparison:** if permissions and language review permit translated or synthetic training data, preserve `origin_type` and parent links, and evaluate its incremental effect on natural held-out SMS. Generated fluency does not establish label correctness, realistic prevalence or natural switching patterns. Derivatives of an evaluation parent remain excluded from training. Artificial challenge sets can diagnose behavior but cannot replace primary native-language results.

## 5. Dataset Quality and Data Leakage

### 5.1. Labels and annotation consistency

Uma et al. demonstrate that disagreement and evaluation choices affect learning comparisons [9]. Their evidence supports examining uncertainty; it does not supply a universal SMS agreement cutoff. Follow [Annotation Guidelines Sections 13–15](annotation_guidelines.md#13-independent-cross-labeling-and-pilot): preserve locked initial judgments, distinguish upstream labels from fresh annotation, report agreement before adjudication and retain separate resolution records. Reviewers must be competent in the language. Unresolved context-dependent items remain withheld, with exclusion counts and reasons.

The proposed pilot groups are training-only because discussion may alter labeling policy. All newly collected natural RU/KZ items and proposed primary validation/test items require independent double labeling under the documented protocol. Agreement reporting includes coverage, class marginals, raw agreement and Cohen's kappa with undefined cases disclosed. Targeted difficult cases and representative audits must be reported separately. These are existing team commitments; no completed annotation or measured agreement is established here.

### 5.2. Related messages and partition independence

Leakage can arise from processing and evaluation choices, not only exact duplicate rows [10]. Lee et al.'s language-model study investigates overlap and memorization [11], while SMS campaign research identifies repeated-message structure [3]. Their effect sizes do not quantify the benefit of grouping for this classifier. The project-specific implication is to inspect related-message families before claiming generalization to unseen examples.

**Planned data audit:** apply DIP-4's canonical exact-text checks and reviewed near-duplicate procedure. Its character 5-gram Jaccard threshold of 0.85 for messages of at least 30 normalized characters is an initial candidate-generation heuristic, not a validated universal rule. Review short texts, false merges and transitive chains. Preserve distinct meaningful variants; do not propagate labels merely because texts are similar. The deduplication shingles are separate from learned classifier features.

Connected `leakage_group_id` components link confirmed duplicates, campaigns, known contributors and original/derivative families across languages and sources. Group integrity takes precedence over exact class proportions. Unknown contributor/campaign relations remain limitations. Privacy masking can make previously different messages identical or label-conflicting; those cases require review before splitting.

**Planned splitting and fold checks:** retain the strategy's 70/15/15 message-count targets, seed `42`, count-based assignment procedure and training-only pilot/derivative eligibility. Approximate class/language stratification operates subject to indivisible groups. Record actual deviations and feasibility. Stratification alone is insufficient. Verify pairwise-disjoint record IDs, fingerprints and leakage groups, including original/translation links. If independent groups cannot support both classes for a language, report it as not evaluable rather than breaking groups to force a ratio.

Vocabulary, IDF, learned feature selection, resampling and classifier parameters must be fitted inside training folds. A vectorizer fitted once before CV exposes fold-held-out text statistics even without labels. Redaction rules and grouping thresholds must not be adjusted in response to held-out prediction errors. Fixed documented corpus-preparation rules differ from learned transformations; this distinction does not authorize model selection on test text [10].

### 5.3. Imbalance, provenance and privacy

**Planned imbalance analysis:** report message and independent-group counts by class, language, origin and partition. Compare an always-ham reference; test weighting or resampling only inside training folds. Keep natural validation/test proportions under the documented sampling process. Volunteer contributions and benchmark mixtures do not estimate deployment prevalence. Do not import non-SMS negatives to obtain an attractive balance without declaring the resulting domain change.

The UCI page reports 5,574 instances, a 2011 recommended citation, a 2012 donation date and CC BY 4.0 [14]. None establishes admitted project counts or completes privacy review. Maintain the [Dataset Strategy](dataset_strategy.md) register of source revisions, hashes, collection method, label policy and separately permitted uses. Public availability, contribution permission and public redistribution permission are different facts. The review provides no legal determination or completed license/consent audit.

Transient prediction and ordinary metadata-only feedback remain separate from consented text intake. Mask full URLs and sensitive spans consistently at training/inference; human privacy review is still required for retained data. Do not publish private text, consent evidence, identifiable rationales or unchecked vocabulary artifacts. Whole-URL masking removes potentially informative infrastructure evidence used in [3]; that utility trade-off requires development evaluation within the existing privacy boundary.

## 6. Evaluation Metrics and Experimental Design

### 6.1. Metrics and decision costs

Use spam as the positive label and a confusion matrix with true classes in rows and predicted classes in columns, both ordered `[ham, spam]` [16].

| Actual / Predicted | ham | spam |
|---|---|---|
| ham | TN: legitimate message recognized | FP: legitimate message marked spam |
| spam | FN: spam missed | TP: spam recognized |

```text
spam precision = TP / (TP + FP)
spam recall    = TP / (TP + FN)
spam F1        = 2*TP / (2*TP + FP + FN)
accuracy       = (TP + TN) / (TP + TN + FP + FN)
```

Precision concerns the correctness of spam alerts; recall concerns coverage of actual spam. F1 summarizes their balance but omits true negatives and does not encode the relative cost of mistakes. Accuracy can be dominated by a majority class: an always-ham classifier can appear accurate while missing all spam. This is a mathematical possibility, not a measured project result. Report raw confusion counts, support and the always-ham comparator alongside spam metrics. Mark undefined denominators and absent classes explicitly; document any software zero-division convention. Macro and pooled averages may supplement, but cannot replace, language-specific reporting.

**Planned threshold analysis:** choose `spam` when the agreed score is greater than or equal to a development-selected threshold, if that equality rule is adopted under D-03. Examine false-positive/false-negative trade-offs and precision–recall behavior with actual support. The team must agree the primary selection objective and any precision/recall constraint before comparing candidates. A threshold of 0.5 is a software convention, not an empirically established optimum or an approved acceptance target. Threshold and probability must use the same score space.

### 6.2. Probability calibration

Guo et al. establish a distinction between accuracy and probability reliability in neural benchmarks [12]. The transfer here is the need to check reliability, not a conclusion about untrained NB/LR or the universal suitability of temperature scaling. Calibration concerns frequencies over comparable predictions, not a guarantee for one message.

**Planned calibration assessment:** compare reliability diagrams with bin counts, Brier score and log loss on development predictions; retain class/language support and binning choices. Proper scoring rules reflect discrimination as well as calibration, so a lower Brier score alone does not prove improved reliability [20]. Check natural-language slices and disclose insufficient support. Weighted or augmented fitting, and later prevalence changes, require renewed interpretation rather than an assumption of stable probabilities.

**Planned calibration fitting:** use a group-disjoint subset of validation for fitting a predeclared mapping and a separate validation subset for threshold/selection checks when support permits. Keep the base pipeline fitted on training only. Compare sigmoid with isotonic calibration only if data supports the comparison; the latter can overfit small calibration samples. If additional splitting is infeasible, use explicitly group-aware out-of-fold training predictions with each full pipeline refitted inside its fold, or defer calibration. Do not let a calibration wrapper introduce row-wise folds after campaign grouping. In-sample scores are unsuitable calibrator-fitting evidence [20]. No development calibration score is independent final evidence.

### 6.3. Reproducible sequence and protected testing

All steps in this experimental sequence are **Planned**. It specifies implications for Rafael's later evaluation protocol (plan step S16), without claiming that protocol or the pipeline has been implemented.

| Stage | Planned action | Required record and independence condition |
|---|---|---|
| 1 — Planned | Admit data after permission, privacy, annotation and grouping checks | Versioned inventory, exclusions, label lineage, agreement and group manifests |
| 2 — Planned | Freeze natural-message training/validation/test assignments | 70/15/15 targets, seed 42, actual support and deviations; protect test access |
| 3 — Planned | Compare representations and NB/LR; optionally Linear SVM | Training-only group-aware CV, initially five folds if feasible; reduce folds with rationale rather than overlap groups |
| 4 — Planned | Select configuration and any calibration/threshold on development data | Predeclared objective, search budget, fold results, independent calibration scores and decision rule |
| 5 — Planned | Freeze the fitted training-only pipeline and interpretation contract | Data/split hashes, dependencies, feature/classifier settings, label map, calibration, threshold and explanations |
| 6 — Planned | Evaluate the selected candidate and predeclared baselines on protected test data | One recorded confirmatory evaluation; natural EN/RU/KZ and mixed support, confusion matrices and spam metrics |
| 7 — Planned | Inspect errors and uncertainty after recording results | Permitted redacted examples, group-aware paired uncertainty analysis where feasible; disclose exposed-test reuse |
| 8 — Planned | Assess later feedback-trained candidates with versioned review | Reviewed labels, evaluation-group exclusion, refreshed evaluation evidence and promotion/rollback decision |

Training CV chooses hyperparameters without touching external validation/test. Its tuning scores are selection evidence and may be optimistic. Verify both-class support in every base-model training fold and calibration-fitting subset, including within each language-specific model; reduce folds or defer an infeasible experiment. Maintain the simple initial protocol in DIP-4: fit the final base model on the 70% training partition and use validation only for development decisions. Combining development partitions for a refit would require a separately documented calibration/threshold procedure before test access. Repeatedly inspecting final test errors and adjusting a model converts that set into an exposed benchmark.

**Planned uncertainty and subgroup reporting:** estimate paired differences on the same test groups using group-aware resampling where independent group counts permit, recording seeds, interval method and unstable/missing estimates. Report EN, RU, KZ and `mixed` separately, without counting one mixed message in two primary totals. Keep translated/synthetic and other-domain challenge results separate. Small language/class cells, unknown campaign links and volunteer selection limit inference; repeated random seeds do not create additional independent SMS.

## 7. Explainability and User Trust

### 7.1. Explaining the fitted sparse classifier

For LR or a binary linear SVM, `w_j*x_j` decomposes the linear score, with the intercept included separately. For binary MNB, subtraction of class scores gives:

```text
MNB log-odds = log(P(spam)/P(ham))
             + sum_j x_j * log(theta_spam,j/theta_ham,j)
```

These are algebraic decompositions of the rules in Section 3, not experimental explanation results. A term appearing in spam is not necessarily positive evidence: its contribution depends on the fitted contrast between classes. The displayed explanation must identify the predicted class and score space. Signed spam evidence should not be presented as a reason for ham without changing its interpretation. Feature contributions add in score/log-odds space, not as additive probability percentages.

Local surrogate approaches such as LIME and SHAP offer alternative explanation frameworks, but their configuration and approximation must be examined. Amparore et al.'s LEAF study evaluates fidelity, concordance and stability in tabular experiments [13]; it does not validate multilingual SMS highlights. Direct score decomposition is a suitable initial candidate for the planned linear models, while comprehension remains a separate user-study question.

Overlapping n-grams can assign evidence to the same characters several times. A short positive fragment can occur inside a legitimate warning or quotation. Normalization, vector normalization, redaction and out-of-vocabulary tokens further limit a word-only visualization. Deleting a highlighted word changes other features and possibly the entire vector norm; the original contribution is therefore not a causal estimate of deletion's effect. Coefficients and highlights describe model behavior, not the sender's intent.

**Planned explanation validation:** reconstruct the raw linear/log-odds score from all contributions and the intercept/prior within numerical tolerance; verify class/sign conventions; report any omitted residual when showing top features. Map normalized features to visible spans with tested Unicode offsets and a declared overlap aggregation rule. Masked content remains protected. Where calibrated probabilities are returned, explain the underlying score and disclose the calibration stage; a nonlinear mapping does not preserve an additive probability decomposition. An ensemble of calibrated classifiers requires an explanation method for that ensemble, rather than silently using one member's coefficients.

### 7.2. Four distinct interpretation concepts

| Concept | Meaning | Evidence required before a user-facing claim |
|---|---|---|
| Model-estimated probability | Output of the fitted probabilistic rule or probability mapping | Correct label ordering and score computation; it can still be unreliable |
| Calibrated probability | Probability with demonstrated empirical frequency correspondence within a stated distribution and uncertainty | Independent reliability evidence with support, language and version limitations |
| User-facing confidence | Interface wording/category derived from a documented interpretation policy | Agreed mapping and real comprehension checks; arbitrary score bands are insufficient |
| Explanation fidelity | Correspondence between the explanation and actual model behavior | Contribution reconstruction or surrogate checks, including preprocessing and displayed spans |

These properties are not interchangeable [12], [13]. A faithful explanation can accompany a wrong prediction; a calibrated model can still make errors; understandable wording does not establish either property. Under current **FR-03–FR-05**, the interface must use real pipeline evidence, disclose unavailable/limited mappings and never invent reasons from a fixed suspicious-word list. It must not describe an unvalidated score as calibrated certainty. Actual comprehension evaluation remains **Planned** under NFR-20 and D-08.

## 8. Structured Critical Literature Comparison

The table compares study scope and evidential limits rather than constructing a leaderboard. **R** denotes published research and **P** a preprint. Reported findings belong to the cited study; project implications are this review's synthesis. Documentary sources [14]–[21] support definitions and implementation decisions elsewhere and have no classifier results to compare.

| Study | Research focus | Dataset / Language | Methods | Evaluation | Key findings | Limitations | Relevance |
|---|---|---|---|---|---|---|---|
| Wang and Manning, 2012, [[1]](#ref-1), R | Strength of simple text baselines | English sentiment/topic tasks, including short snippets | NB, SVM, NB-weighted SVM; unigrams/bigrams | Classification accuracy/error across feature/task settings | Performance depends on task, text length and feature variant | Not an SMS or RU/KZ study; NB-weighted SVM differs from plain SVM | Compare explicit configurations; avoid universal rankings |
| Filali et al., 2026, [[2]](#ref-2), R | Representations and augmentation for SMS | UCI English; translated French/German/Hindi | LR/SVM and other classifiers; contextual embeddings; GAN augmentation | Declared stratified 80/20 split; F1 and other metrics; five-seed analysis | Table 11 reports F1 97.61% for BERT+Bi-LSTM+GAN and 97.59% for BERT+LR | Inconsistent corpus counts; test-dependent significance; native RU/KZ and derivative isolation unestablished | Richer methods warrant controlled comparison, not automatic adoption |
| Nahapetyan et al., 2024, [[3]](#ref-3), R | SMS phishing campaigns/infrastructure | Public SMS gateways; phishing-focused observations | Collection, identification and near-duplicate campaign analysis | Observational collection/campaign and infrastructure analysis | Reports 67,991 phishing messages linked into 35,128 campaigns | Gateway selection; phishing differs from full spam/ham policy; URL evidence differs from masked text | Motivate campaign grouping and a source-aware task definition |
| Ali et al., 2025, [[4]](#ref-4), R | Mobile-money smishing in a local domain | Crowdsourced Mozambican Portuguese SMS | Human annotation and zero/few-shot LLM prompting | Class-specific/macro F1 across prompt settings | Reports macro F1 0.79 for Qwen2.5-14B with 16-shot Portuguese prompts | Domain-specific binary policy; prompt language differs from message language; no RU/KZ validation | Require natural local data and declared metric averaging |
| Li et al., 2024, [[5]](#ref-5), P | Collection, private training settings and adversarial behavior | Socially reported SMS from Twitter/Weibo; multilingual evidence | OCR/collection pipeline, BERT, central/federated classification, adversarial tests | Binary and separate multi-label classification; attack evaluations | Demonstrates a social-report collection route and examines vulnerabilities | Reporting/OCR selection; some balancing uses non-SMS tweets; peer-reviewed venue unverified | Audit source/negative-class suitability; feedback needs controls |
| Doğruöz et al., 2021, [[6]](#ref-6), R | Linguistic/social treatment of code-switching | Multilingual speech/text literature | Critical survey of switching patterns and computational practice | Conceptual synthesis rather than one SMS benchmark | Identifies mismatches between linguistic variation and computational resources/evaluation | Contexts and tasks differ from Kazakhstan SMS | Define meaningful mixing and use competent language review |
| Borisov et al., 2025, [[7]](#ref-7), R | Low-resource Kazakh–Russian mixed-text translation | KRCS: 618 social-text parallel evaluation sentences | Sequence-to-sequence models and synthetic switching augmentation | BLEU, ChrF++, COMET and human judgments | Human/automatic assessments provide different model comparisons | Small translation resource; synthetic training; no spam labels | Reserve natural mixed-language SMS evaluation; do not transfer translation scores |
| Maxutov et al., 2024, [[8]](#ref-8), R | Kazakh LLM capability | Six Kazakh task datasets; selected parallel English tasks | Seven LLMs | Task-specific classification/generation measures | Observes capability differences by task and language | Pilot tasks and model versions; no SMS spam benchmark | General language capability cannot certify target-task performance |
| Uma et al., 2021, [[9]](#ref-9), R | Learning with annotator disagreement | NLP/computer-vision datasets with multiple judgments | Survey and empirical comparison of learning strategies | Hard/soft label evaluations | Evaluation form and dataset characteristics change method comparisons | No universal agreement cutoff or SMS-specific labeling solution | Preserve initial labels, uncertainty and adjudication lineage |
| Kapoor and Narayanan, 2023, [[10]](#ref-10), R | Leakage and scientific reproducibility | Cross-disciplinary literature; civil-war prediction case | Leakage taxonomy, information sheets and reproduction study | Methodological audit and corrected model comparisons | Leakage can invalidate apparent advantages of complex models | Not an SMS effect estimate; a reporting sheet alone cannot establish correctness | Fit transformations within folds and record model-selection exposure |
| Lee et al., 2022, [[11]](#ref-11), R | Deduplication in language modeling | Large English web-text corpora | Exact/near-duplicate detection and model training | Overlap, memorization and language-model quality | Deduplication reduces overlap/memorization in their settings | Generative outcomes differ from spam precision/recall | Audit overlap without inventing a classifier improvement |
| Guo et al., 2017, [[12]](#ref-12), R | Probability reliability | Neural image/document benchmarks | Calibration diagnostics and post-processing | Calibration error alongside predictive performance | High accuracy need not imply reliable probabilities | Neural models/distributions differ from NB/LR SMS | Assess reliability separately before interpreting confidence |
| Amparore et al., 2021, [[13]](#ref-13), R | Quality of local linear explanations | Four tabular datasets; multiple classifiers | LEAF diagnostics for LIME/SHAP | Fidelity, concordance, stability and other explanation properties | Reveals explanation defects and motivates separate evaluation | Tabular experiments do not validate SMS span mapping or comprehension | Verify genuine contributions and presentation independently |

One comparison needs particular caution. In [2], the two Table 11 F1 values differ by **0.02 percentage points**, but classifier and augmentation change together. The dataset narrative gives 5,572 messages, whereas Table 2 lists 747 spam plus 4,852 ham, totaling 5,599. Five-seed Wilcoxon tests report `p = 0.0625`, unlike the significant parametric tests. These inconsistencies and design differences weaken a superiority claim; they are not evidence that the team has reproduced or refuted the experiments.

## 9. Research Gaps

The gaps below are bounded by the selected sources and current repository evidence. They do not claim the worldwide absence of relevant datasets or research.

| Gap and evidence basis | Consequence | Planned validation or response |
|---|---|---|
| Natural RU/KZ SMS under this label policy is not established by this review or DIP-4; [7], [8] address other tasks | Target-language quality cannot yet be estimated | Audit permitted both-class sources and native contributions; investigate eligible Russian subsets of [5] without assuming availability/rights |
| English/translated evidence [2], [14] does not establish cross-language transfer | Pooled scores can hide language-specific errors | Matched NB/LR comparisons by natural language and source; report missing support |
| Code-switching resources [6], [7] do not validate binary mixed SMS classification | Mixing and transliteration may expose coverage gaps | Competent annotation and a separate natural `mixed` slice; character-feature benefit is a team hypothesis |
| Disagreement, related examples and evaluation choices [9]–[11] can undermine comparisons | Aggregate metrics may conceal uncertain labels or dependent examples | Preserve label lineage, group-disjoint partitions, denominator/support tables and fold-local fitting |
| Calibration and explanation evidence [12], [13] concerns distinct properties and other settings | Probability, highlights and trust can be conflated | Reliability checks, score reconstruction, safe span mapping and later real comprehension tasks |
| SMS source/collection evidence [3], [5], [14] does not establish safe reuse or confidential processing | Permitted training, transient inference and public artifacts need separate controls | Provenance/use register, screened intake, separate consent and artifact/privacy review under DIP-4/D-05 |
| No project NB/LR comparison or lifecycle evidence exists in the reviewed baseline | Literature cannot choose the production model | Versioned matched experiments, protected testing and reviewed offline updates under NFR-17/EV-01 |

## 10. Implications for Our Project

### 10.1. Technical decisions and current requirement traceability

The following are literature-informed recommendations or existing design commitments, with experimental verification **Planned**. They use the identifiers in the current [Requirements Specification](requirements.md), rather than earlier draft mappings. The [Architecture](architecture.md) keeps offline preparation/training and authorized promotion separate from public checking.

| Evidence and recommendation | Project decision | Current requirement connection | Planned acceptance evidence |
|---|---|---|---|
| Conditional simple-model evidence [1]; algorithm definitions [17], [18] | TF-IDF + MNB baseline; TF-IDF + LR alternative; retain always-ham reference | NFR-17, EV-01, D-03 | Matched partitions, training CV and native per-language held-out reports |
| Sparse linear comparison [19] | Linear SVM as an additional candidate, subject to time/data and probability compatibility | FR-03, FR-22, EV-01 | Classification comparison plus separately evaluated probability mapping if promoted |
| Surface representation [15] and target-task gaps [7], [8] | Compare word features with character n-grams; pooled/separate models remain unresolved | FR-09, FR-21, NFR-12, D-03 | Origin/language/script slices, analyzer configuration and support/coverage evidence |
| Annotation/leakage research [9]–[11] | Follow DIP-4's independent labels, grouping and protected evaluation | NFR-17, EV-01 | Agreement/adjudication records, group manifests and fold-local transformation audit |
| Calibration and explanation distinctions [12], [13], [20] | Validate probability interpretation and actual feature contributions | FR-03–FR-05, NFR-20, D-03/D-08 | Reliability analysis, reconstructed scores, span fixtures and comprehension observations |
| Normalization [21] and documented privacy boundary | Share deterministic privacy-aware preprocessing across training, single and batch inference | FR-11, FR-21, NFR-01/NFR-02/NFR-12, D-05 | Unicode/placeholder/offset fixtures; no default text retention in ordinary history/logs |
| Reproducibility and adversarial considerations [5], [10] | Version evaluated models and reviewed feedback releases; controlled promotion/rollback | FR-14–FR-17, FR-22, NFR-18, D-07 | Permitted label-confirmed contributions, reserved-group checks and activation records |

Rafael's reproducible experiments and substantive interpretation, with team review, will determine the final model. Literature supplies candidate methods and methodological constraints. It cannot substitute for measured local performance, compatibility or an agreed error trade-off. D-03 remains open: this document proposes evidence and comparisons without approving an estimator, routing policy, quality target, threshold or confidence bands.

### 10.2. Ownership and integration boundaries

Responsibilities follow the [README](../README.md), Proposal and Architecture. Rafael leads TF-IDF training/evaluation, comparison, model versions and verified-feedback retraining; Beknur leads source preparation, annotation, character-feature experiments and UI; Sanzhar leads inference/explanations, threshold/error analysis, API/privacy and safe persistence. These descriptions allocate future work and do not certify completed student contributions.

The planned handoff to inference must identify data/split, preprocessing, analyzer/vocabulary, estimator, label ordering, calibration, threshold/equality, explanation and dependency versions. History statistics count predictions rather than measured classifier quality. Metadata-only error flags cannot reconstruct training text or confirm labels. Any later update requires permitted text, independent review and an evaluated offline candidate; public feedback cannot directly retrain or activate a model.

### 10.3. Documentation consistency observations

The recommendations follow DIP-4's detailed partition protocol, DIP-8, DIP-9 and DIP-10. One substantive wording conflict needs clarification: Proposal Section 14 excludes validation/test records from threshold selection and calibration fitting, whereas Proposal Section 18 and Dataset Strategy Section 17 allow development validation for those decisions while protecting the final test. This review follows the more specific DIP-4 protocol: training-only CV/fitting of the base model, development-only calibration/threshold selection and an untouched final test. **Sanzhar, as proposal owner, should reconcile Section 14 in a separate follow-up PR**, with Rafael reviewing the evaluation interpretation. Cross-document consistency remains pending until that wording is agreed; this document does not amend the proposal or claim that D-03 is resolved.

Some inherited status prose is also stale: the README says research documents/diagrams are yet to be added; Technology Comparison Sections 1 and 4.5 say a completed FR/NFR specification is unavailable; DIP-9 describes a historical branch/upstream synchronization boundary and unavailable Rafael notes. The current checkout contains requirements, architecture and the general review. These document-status inconsistencies should be reconciled by their owners during consolidation. This task leaves their files unchanged and uses current requirement definitions.

## 11. Limitations and Future Validation

### 11.1. What published research supports

The selected papers support conditional comparisons of simple text models, careful interpretation of multilingual resources, and separate attention to labels, overlap, calibration and explanations. Their methods and findings were inspected to the depth recorded in Section 2. Domains, labels, languages, sampling and metrics differ. Cross-paper scores therefore cannot establish an architecture ranking or expected project accuracy. No cited dataset was ingested and no published experiment was rerun for this task.

### 11.2. What the team has documented

The repository documents binary semantics, permission/privacy gates, independent annotation, group-aware 70/15/15 target splits, seed 42, training-only transformations, per-language evaluation and a separate offline lifecycle. Current requirements provide traceability through NFR-17 and EV-01, with model interpretation, retention, operations and usability decisions still pending. Written commitments establish design intent; their implementation and acceptance require later evidence.

### 11.3. What remains unverified

Natural RU/KZ both-class coverage, contributor permissions, annotation feasibility/agreement, group completeness, real prevalence and acceptable error costs remain unresolved. The benefit of character features, pooled versus separate models, calibration, threshold selection and faithful multilingual highlight comprehension are untested team hypotheses. Source [5] remains a preprint in this review. Publication verification does not settle code quality, redistribution rights or the scientific reliability of every reported result. The bounded search may omit relevant work, including Russian-specific text-processing studies; no dedicated Russian morphology benchmark was reviewed.

The university requirements and team roadmap were accessible, but substantive supervisor acceptance, student review and review activity in Git/YouTrack have not been established by this preparation. Codex-assisted drafting is not evidence that Rafael independently read, reproduced or approved the material.

### 11.4. Future validation and review handoff

**Planned:** Rafael should inspect the primary studies and proposed NB/LR reasoning, record his actual analysis, and agree the later experiment-selection protocol with the relevant owners. Beknur should verify language/data/annotation feasibility; Sanzhar should verify score, privacy and explanation handoff. Subsequent experiments follow Section 6 and must retain actual failures and missing-language outcomes as well as successful results. Synthetic fixtures can establish contract behavior but cannot establish native SMS quality.

An authorized commit and Draft PR may make this document available for the pending personal and independent team review, using the actual contributor's identity. Draft publication does not establish Rafael's personal verification or another participant's approval. Only actual reviewer actions and evidence should be recorded in YouTrack. Supervisor confirmation and any necessary revisions remain separate acceptance steps; the issue must not be marked complete solely because this document was generated or published for review.

## 12. References

Research numbers [1]–[13] identify unique works; alternative copies do not add publications. **R:** published research; **P:** preprint; **D:** dataset documentation; **T:** technical documentation; **S:** technical standard. Official web resources were accessed on 24 October 2026. Undated software guides use that access date only; their actual runtime versions must be fixed during implementation.

<a id="ref-1"></a>
[1] S. Wang and C. D. Manning. “Baselines and Bigrams: Simple, Good Sentiment and Topic Classification.” 2012. In *Proceedings of the 50th Annual Meeting of the Association for Computational Linguistics, Volume 2: Short Papers*, pp. 90–94. **R — conference paper.** [Official record](https://aclanthology.org/P12-2018/) · [Primary text](https://aclanthology.org/P12-2018.pdf).

<a id="ref-2"></a>
[2] A. Filali, M. Shorfuzzaman, E. A. Abdellaoui Alaoui, M. Merras, M. Es-Sabry, A. Berrajaa, R. Alroobaea, and A. Yousef. “Cross-lingual SMS spam detection using GAN-based augmentation for imbalanced datasets.” 2026. *Scientific Reports* 16, 7128. DOI: **10.1038/s41598-026-37769-4**. **R — journal article.** [Published text](https://pmc.ncbi.nlm.nih.gov/articles/PMC12921278/).

<a id="ref-3"></a>
[3] A. Nahapetyan, S. Prasad, K. Childs, A. Oest, Y. Ladwig, A. Kapravelos, and B. Reaves. “On SMS Phishing Tactics and Infrastructure.” 2024. In *2024 IEEE Symposium on Security and Privacy*, pp. 1–16. DOI: **10.1109/SP54263.2024.00169**. **R — conference paper.** [Author publication record](https://sathviknp.org/publication/2024-02-01-SMS-Phishing) · [Primary text](https://sathviknp.org/files/sms-phishing-paper.pdf).

<a id="ref-4"></a>
[4] F. D. M. A. Ali, S. M. Saide, R. Sousa-Silva, and H. Lopes Cardoso. “MOZ-Smishing: A Benchmark Dataset for Detecting Mobile Money Frauds.” 2025. In *Proceedings of the Sixth Workshop on African Natural Language Processing (AfricaNLP 2025)*, pp. 158–166. DOI: **10.18653/v1/2025.africanlp-1.23**. **R — workshop paper.** [Official record](https://aclanthology.org/2025.africanlp-1.23/) · [Primary text](https://aclanthology.org/2025.africanlp-1.23.pdf).

<a id="ref-5"></a>
[5] Y. Li, R. Zhang, W. Rong, and X. Mi. “SpamDam: Towards Privacy-Preserving and Adversary-Resistant SMS Spam Detection.” 2024. arXiv:**2404.09481**. **P — preprint; peer-reviewed venue not verified.** [Record](https://arxiv.org/abs/2404.09481) · [Inspected version 1](https://arxiv.org/html/2404.09481v1).

<a id="ref-6"></a>
[6] A. S. Doğruöz, S. Sitaram, B. E. Bullock, and A. J. Toribio. “A Survey of Code-switching: Linguistic and Social Perspectives for Language Technologies.” 2021. In *Proceedings of ACL-IJCNLP 2021, Volume 1: Long Papers*, pp. 1654–1666. DOI: **10.18653/v1/2021.acl-long.131**. **R — conference paper.** [Official record](https://aclanthology.org/2021.acl-long.131/) · [Primary text](https://aclanthology.org/2021.acl-long.131.pdf).

<a id="ref-7"></a>
[7] M. Borisov, Z. Kozhirbayev, and V. Malykh. “Low-resource Machine Translation for Code-switched Kazakh-Russian Language Pair.” 2025. In *Proceedings of the 2025 Conference of the Nations of the Americas Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 4: Student Research Workshop*, pp. 66–76. DOI: **10.18653/v1/2025.naacl-srw.7**. **R — workshop paper.** [Official record](https://aclanthology.org/2025.naacl-srw.7/) · [Primary text](https://aclanthology.org/2025.naacl-srw.7.pdf).

<a id="ref-8"></a>
[8] A. Maxutov, A. Myrzakhmet, and P. Braslavski. “Do LLMs Speak Kazakh? A Pilot Evaluation of Seven Models.” 2024. In *Proceedings of the First Workshop on Natural Language Processing for Turkic Languages (SIGTURK 2024)*, pp. 81–91. **R — workshop paper.** [Official record](https://aclanthology.org/2024.sigturk-1.8/) · [Primary text](https://aclanthology.org/2024.sigturk-1.8.pdf).

<a id="ref-9"></a>
[9] A. N. Uma, T. Fornaciari, D. Hovy, S. Paun, B. Plank, and M. Poesio. “Learning from Disagreement: A Survey.” 2021. *Journal of Artificial Intelligence Research* 72, pp. 1385–1470. DOI: **10.1613/jair.1.12752**. **R — journal article.** [Official record](https://www.jair.org/index.php/jair/article/view/12752) · [Primary text](https://www.jair.org/index.php/jair/article/download/12752/26751).

<a id="ref-10"></a>
[10] S. Kapoor and A. Narayanan. “Leakage and the reproducibility crisis in machine-learning-based science.” 2023. *Patterns* 4(9), 100804. DOI: **10.1016/j.patter.2023.100804**. **R — journal article.** [Official published full-text XML](https://www.ebi.ac.uk/europepmc/webservices/rest/PMC10499856/fullTextXML).

<a id="ref-11"></a>
[11] K. Lee, D. Ippolito, A. Nystrom, C. Zhang, D. Eck, C. Callison-Burch, and N. Carlini. “Deduplicating Training Data Makes Language Models Better.” 2022. In *Proceedings of the 60th Annual Meeting of the Association for Computational Linguistics, Volume 1: Long Papers*, pp. 8424–8445. DOI: **10.18653/v1/2022.acl-long.577**. **R — conference paper.** [Official record](https://aclanthology.org/2022.acl-long.577/) · [Primary text](https://aclanthology.org/2022.acl-long.577.pdf).

<a id="ref-12"></a>
[12] C. Guo, G. Pleiss, Y. Sun, and K. Q. Weinberger. “On Calibration of Modern Neural Networks.” 2017. In *Proceedings of the 34th International Conference on Machine Learning*, PMLR 70, pp. 1321–1330. **R — conference paper.** [Official record](https://proceedings.mlr.press/v70/guo17a.html) · [Primary text](https://proceedings.mlr.press/v70/guo17a/guo17a.pdf).

<a id="ref-13"></a>
[13] E. Amparore, A. Perotti, and P. Bajardi. “To trust or not to trust an explanation: using LEAF to evaluate local linear XAI methods.” 2021. *PeerJ Computer Science* 7, e479. DOI: **10.7717/peerj-cs.479**. **R — journal article.** [Official published full-text XML](https://www.ebi.ac.uk/europepmc/webservices/rest/PMC8056245/fullTextXML).

<a id="ref-14"></a>
[14] T. Almeida and J. Hidalgo. “SMS Spam Collection.” 2011 (recommended citation; donation dated 21 June 2012). *UCI Machine Learning Repository*. DOI: **10.24432/C5CC84**. **D — dataset record.** [Official documentation](https://archive.ics.uci.edu/dataset/228/sms+spam+collection).

<a id="ref-15"></a>
[15] Scikit-learn developers. “Feature extraction,” text feature extraction sections. Undated. *Scikit-learn User Guide*. **T — technical documentation.** [Official guide](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction).

<a id="ref-16"></a>
[16] Scikit-learn developers. “Metrics and scoring: quantifying the quality of predictions.” Undated. *Scikit-learn User Guide*. **T — technical documentation.** [Official guide](https://scikit-learn.org/stable/modules/model_evaluation).

<a id="ref-17"></a>
[17] Scikit-learn developers. “Naive Bayes,” including Multinomial Naive Bayes. Undated. *Scikit-learn User Guide*. **T — technical documentation.** [Official guide](https://scikit-learn.org/stable/modules/naive_bayes).

<a id="ref-18"></a>
[18] Scikit-learn developers. “Linear Models,” Logistic regression section. Undated. *Scikit-learn User Guide*. **T — technical documentation.** [Official guide](https://scikit-learn.org/stable/modules/linear_model#logistic-regression).

<a id="ref-19"></a>
[19] Scikit-learn developers. “Support Vector Machines.” Undated. *Scikit-learn User Guide*. **T — technical documentation.** [Official guide](https://scikit-learn.org/stable/modules/svm).

<a id="ref-20"></a>
[20] Scikit-learn developers. “Probability calibration.” Undated. *Scikit-learn User Guide*. **T — technical documentation.** [Official guide](https://scikit-learn.org/stable/modules/calibration).

<a id="ref-21"></a>
[21] K. Whistler (editor), Unicode Consortium. “Unicode Normalization Forms.” 2025. *Unicode Standard Annex #15*, revision 57, Unicode 17.0.0, 30 July 2025. **S — technical standard.** [Versioned official annex](https://www.unicode.org/reports/tr15/tr15-57.html).
