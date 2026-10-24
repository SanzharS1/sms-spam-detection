# Literature Review

## 1. Introduction

This review examines the evidence supporting the proposed **Development of a Web-Based SMS Spam Detection Application Using Machine Learning**. The [Project Proposal](project_proposal.md), particularly Sections 9–18, specifies manually submitted English, Russian and Kazakh messages, classification explanations, batch checking, private history and reviewed feedback. The central question is which published findings justify those engineering choices, and which assumptions still require project-specific evaluation.

Spam detection is not a single interchangeable task. Unsolicited promotion, credential theft, fraudulent payment requests and ordinary legitimate messages have different labeling boundaries. Here, `spam` follows the [Annotation Guidelines](annotation_guidelines.md): unsolicited promotional or deceptive solicitation; unresolved cases are withheld. Studies of phishing alone therefore supply relevant threat evidence without establishing performance for the complete project label policy.

The review combines classifier research, multilingual resources and methodological evidence about data, explanations and evaluation. Published measurements are reported as results of the cited studies. No project corpus, trained model, user study or implementation result is established by this review.

## 2. Literature Selection Methodology

### 2.1. Search and selection procedure

Targeted web searches and citation-following were conducted on 24 October 2026. Searches covered SMS spam/smishing, TF-IDF and linear classifiers, Kazakh–Russian code-switching, annotation disagreement, leakage, calibration and explanation evaluation. Representative queries included `SMS spam detection 2023 2024 TF-IDF logistic regression dataset scientific publication`, `Kazakh Russian code switching dataset 2025 KRCS`, `Learning from Disagreement 2021 JAIR` and `Deduplicating Training Data Makes Language Models Better ACL 2022`.

Search results supplied leads; inclusion depended on checking publication records and relevant methods/results/limitations in primary texts. Sources were accessed through ACL Anthology, PMLR, JAIR, PubMed Central, arXiv, author-hosted papers and official dataset/software/standards pages. This is a focused critical narrative review, not an exhaustive database search, a PRISMA review or a quantitative meta-analysis. No unrecorded screening totals are claimed.

The search covered publication years 2021–2026, with recency assessed separately over the rolling five-year interval **24 October 2021–24 October 2026**. Earlier work was retained for controlled NB/SVM baselines [1], code-switching definitions [6], probability calibration [12] and local-explanation diagnostics [13]. Inclusion required a clear connection to a project decision, identifiable authors and publication status, a stable record and inspectable evidence. Duplicate versions of one work count once. Unverifiable citations, unrelated application domains without a defensible methodological connection, and inaccessible candidate papers whose findings could not be checked were excluded from the analytical set.

### 2.2. Evidence types and access boundaries

| Type | Meaning | References | Count |
|---|---|---|---|
| R | Published journal, conference or workshop research | [1]–[4], [6]–[13] | 12 |
| P | Scientific preprint; peer-reviewed publication not verified | [5] | 1 |
| D | Dataset documentation, not a scientific paper | [14] | 1 |
| T | Technical documentation, not a scientific paper | [15]–[16] | 2 |
| S | Accessibility standard, not a scientific paper | [17] | 1 |

The analytical set contains **17 unique sources**, including **12 published research papers** without relying on the preprint to meet the scientific-publication minimum. The calendar-year coverage 2021–2026 includes 10/12 published papers, 11/13 scientific works including the preprint, and 12/17 sources overall. That six-calendar-year coverage is not the five-year recency test. Within **24 October 2021–24 October 2026**, the counts are **8/12 published papers (66.7%)** [2]–[4], [7]–[11], **9/13 scientific works including the preprint (69.2%)**, and **10/17 sources overall (58.8%)**. The August 2021 survey [6] and April 2021 explanation study [13] fall outside this interval; the December 2021 survey [9] falls inside it. The two software documentation entries have no assigned publication year; their access date is not counted as a publication date.

Publication records and relevant primary-text sections were inspected for the research entries. The published journal texts of Kapoor and Narayanan [10] and Amparore et al. [13] were checked through the official Europe PMC full-text XML API after the publisher/PMC HTML routes were unavailable. Their article titles, authors, journal records and DOIs matched the bibliography; the published methods and findings support the claims used here. Earlier author manuscripts remain alternative copies of the same works, not additional counted publications. Section 8 distinguishes source inspection from experiment reproduction and team review.

## 3. Background and Existing Research

### 3.1. SMS spam, smishing and collection context

The UCI record supplies a documented English SMS baseline, not contemporary multilingual coverage [14]. Nahapetyan et al. analyze phishing messages and related campaigns from public SMS gateways [3]; their collection vantage point and URL-derived evidence differ from a browser service processing deliberately submitted text. Ali et al. provide a Portuguese mobile-money smishing resource with locally specific messages [4]. Together, these sources show why source domain and label policy must accompany a dataset name.

The project's binary policy includes unsolicited advertising as well as deception. A study separating fraudulent from legitimate payment requests cannot be assumed to measure that broader task. Nor do publicly observable messages establish the distribution, permissions or privacy conditions of voluntarily contributed SMS in Kazakhstan. These are collection and validation questions for the project.

### 3.2. Models and text representations

Wang and Manning show that NB/SVM performance depends on feature and task choices, including word bigrams and text length [1]. This supports controlled baselines rather than a universal algorithm ranking. Their MNB decision combines class-conditional log-feature evidence and class priors; their linear SVM learns a margin-based decision function. Logistic Regression instead fits a probabilistic linear classifier [2]. A linear SVM decision margin is not itself a spam probability; adding it to the service would require a separately validated probability interface.

TF-IDF weights term frequency by corpus-level document frequency, with implementation-specific smoothing and normalization [15]. Sparse word/character n-grams are not contextual semantic embeddings. Vocabulary, IDF and any learned feature selection must be fitted within training partitions/folds, as part of the leakage controls [10]. Filali et al.'s contextual/augmented configurations [2] supply a comparison to inspect, subject to the reporting and statistical limitations discussed in Section 5.1.

For this project, TF-IDF with Multinomial Naive Bayes and Logistic Regression remains a proposed reproducible comparison; Linear SVM is a reasonable additional development baseline if included under the same protocol. Word and character n-gram extraction is supported by the implementation documentation [15]. Character features may help investigate spelling and morphological variation, but improvement on native RU/KZ SMS is a hypothesis, not an established outcome of the cited studies.

### 3.3. Multilingual and low-resource transfer

Doğruöz et al. distinguish linguistic and social forms of code-switching, cautioning against treating every borrowed word as equivalent multilingual behavior [6]. Borisov et al. study Kazakh–Russian mixed text through machine translation, using a small social-text evaluation resource and synthetic training augmentation [7]. Maxutov et al. evaluate Kazakh LLM capabilities across several tasks [8]. Neither of the latter studies evaluates binary SMS spam detection.

Their relevance is methodological: mixed-language inputs need explicit treatment, and evaluation must match the intended language and task. Filali et al.'s multilingual extension consists of machine-translated French, German and Hindi messages [2]. Such derivatives can support controlled transfer experiments but cannot substitute for naturally occurring Russian or Kazakh SMS. The [Dataset Strategy](dataset_strategy.md) appropriately separates native, translated, synthetic and mixed-language evidence.

### 3.4. Dataset quality and independent evaluation

Uma et al. show that annotation disagreement and evaluation choices can change conclusions about learning methods [9]. Disagreement should therefore be recorded before adjudication rather than hidden by a single final label. Lee et al. demonstrate the importance of deduplication and train–test overlap in language-model corpora [11]. Kapoor and Narayanan identify leakage across data-processing and evaluation stages [10]. Their studied domains differ from SMS classification, so their numerical effects should not be transferred to this corpus.

The engineering implication is to preserve initial judgments, review ambiguous labels, identify related campaigns and derivatives, and fit learned transformations only inside the training partition or fold. Stratification alone does not ensure independence between near-duplicate messages or translations. Actual class balance, agreement and overlap remain properties to measure after permitted collection, not facts supplied by these publications.

### 3.5. Metrics, errors and probability interpretation

The project needs spam-class precision, recall and F1, support counts and confusion matrices for each evaluated language, rather than aggregate accuracy alone. With spam as the positive class:

```text
precision = TP / (TP + FP)
recall    = TP / (TP + FN)
F1        = 2 * TP / (2 * TP + FP + FN)
```

The scoring documentation explains class-specific and averaged metrics [16]. Accuracy, `(TP + TN) / (TP + TN + FP + FN)`, measures overall correctness; precision measures correctness among predicted spam. False positives are legitimate messages labeled spam; false negatives are missed spam. Undefined denominators and missing classes must be disclosed. Mixed-language results should be separately identified without double-counting the same messages in primary language totals.

Class imbalance is source-specific: the English benchmark in [2] is ham-majority, whereas SpamDam's default ground truth is spam-majority [5]. Neither distribution establishes deployment prevalence. For the project, class weighting, resampling or synthetic augmentation, if compared, must be confined to training folds; protected evaluation must disclose its natural class support and any sampling changes. No balancing method is assumed to improve every language or error type.

Guo et al. distinguish predictive correctness from calibrated probabilities in neural models [12]. That distinction supports checking reliability before assigning confidence labels, but their findings do not prove that this project's NB or LR probabilities are miscalibrated or that one calibration method will be best. Model, threshold and any calibration choices must use development data; final evaluation must remain separate.

### 3.6. Explanation, privacy and usable presentation

Amparore et al. assess local explanation fidelity, consistency and related properties, showing why an attractive explanation is not sufficient evidence of faithfulness [13]. Their experiments use tabular data, so they do not validate SMS word highlighting. The project must derive contributions from its actual classifier and map word/character features to displayed text; faithful model attribution and user comprehension require different checks. Feature contributions describe model behavior, not a causal account of malicious intent or a guarantee of message safety.

Li et al.'s SpamDam preprint investigates central/federated detection and adversarial resistance using socially reported SMS [5]. Its privacy motivation does not imply that federated learning, public collection or redaction guarantees anonymity. The proposal's transient processing and separately consented feedback are distinct design choices to verify. WCAG supplies relevant requirements for presenting information beyond color and making status messages available to assistive technology [17]; it supplies no evidence that the planned interface has already met them.

## 4. Structured Critical Literature Comparison

Types R/P/D/T/S follow Section 2. A result is attributed to its study and evaluation setting. Different metrics and datasets are not treated as a shared leaderboard. For documentary sources, an experimental classifier result is not applicable.

| Ref | Study / Year / Type | Method | Dataset / Languages | Evaluation / Findings | Limitations | Project Relevance |
|---|---|---|---|---|---|---|
| [[1]](#ref-1) | Wang and Manning, 2012; R | NB, SVM and NB-weighted SVM; unigram/bigram variants | English sentiment/topic datasets, including short snippets | Accuracy/error comparisons show dependence on features and task | Not SMS or RU/KZ evaluation; NB-SVM is a distinct configuration | Justifies controlled simple baselines and explicit feature settings |
| [[2]](#ref-2) | Filali et al., 2026; R | LR/SVM, recurrent models, contextual/frequency representations and augmentation | UCI English; machine-translated French/German/Hindi | Declares 80/20 stratification; Table 11 reports monolingual F1 97.61% for BERT+Bi-LSTM+GAN versus 97.59% for BERT+LR; Table 15 reports multilingual F1 94.44% | Corpus totals conflict; five-seed t-test/Wilcoxon conclusions differ; derivative-group isolation and native RU/KZ coverage are unestablished | Does not isolate a reliable augmentation gain or validate native target-language quality |
| [[3]](#ref-3) | Nahapetyan et al., 2024; R | Gateway collection, phishing identification, near-duplicate campaign and infrastructure analysis | Messages from 11 public gateways; phishing-focused observational sample | Identifies 67,991 phishing messages and 35,128 campaigns; these are collection findings, not project classifier metrics | Gateway selection and external detection thresholds affect coverage; not a representative EN/RU/KZ spam/ham test | Supports campaign grouping and distinguishing URL/infrastructure evidence from text-only checking |
| [[4]](#ref-4) | Ali et al., 2025; R | Crowdsourced collection/annotation; zero/few-shot LLM classification | Mozambican Portuguese mobile-money messages; Portuguese/English prompts | Reports per-class and macro F1; Qwen2.5-14B reaches macro F1 0.79 with 16-shot Portuguese prompting | Narrow domain; smishing/legitimate labels differ from unsolicited-advertising policy; prompt language is not message language | Shows the need for local-language/domain evidence and class-specific reporting |
| [[5]](#ref-5) | Li et al., 2024; P | OSN-based collection, BERT detection, central/federated training and adversarial tests | Multilingual Twitter/Weibo SMS reports, including English/Chinese; more than 76K collected spam messages | Reports binary precision/recall/accuracy and separate multiclass/multilabel experiments | Preprint; some balancing uses ordinary tweets as negatives; selection and non-SMS examples limit transfer | Motivates source/label review and model-update safeguards; no automatic privacy guarantee |
| [[6]](#ref-6) | Doğruöz et al., 2021; R | Linguistic/social critical survey of code-switching research | Multilingual speech/text literature, particularly European/Indian contexts | Synthesizes patterns and mismatches in computational treatment; no common classifier benchmark | Not an SMS corpus or proof of Kazakh spam-detection performance | Informs mixed-language definitions and language-competent review |
| [[7]](#ref-7) | Borisov et al., 2025; R | Synthetic code-switch augmentation and sequence-to-sequence translation | Kazakh–Russian; KRCS contains 618 social-text evaluation sentences | Uses automatic translation metrics and human evaluation; rankings depend on evaluation method | Small translation resource; synthetic training differs from natural SMS; translation quality is not spam F1 | Supports explicit mixed-language validation and limits on translated augmentation claims |
| [[8]](#ref-8) | Maxutov et al., 2024; R | Pilot evaluation of seven LLMs on six task datasets | Kazakh; selected parallel English comparisons | Uses task-specific classification/generation measures; finds capability variation by task/language | Small/task-specific benchmarks and changing model versions; no SMS spam labels | General Kazakh capability cannot replace target-task evaluation |
| [[9]](#ref-9) | Uma et al., 2021; R | Survey plus empirical comparison of approaches to multiple annotator judgments | NLP and computer-vision datasets with disagreement | Hard/soft evaluation and dataset characteristics affect method comparisons | No universal gold-label strategy or SMS-specific agreement threshold follows | Preserve independent labels, uncertainty and adjudication evidence |
| [[10]](#ref-10) | Kapoor and Narayanan, 2023; R | Leakage taxonomy, model information sheets and reproduction case study | Cross-disciplinary ML science; civil-war prediction case | Shows how leakage can invalidate apparent advantages of complex models | Not an SMS benchmark; reporting sheets do not replace access to data/code or independent methodological checks | Justifies training-only fitting, protected evaluation and reproducibility records |
| [[11]](#ref-11) | Lee et al., 2022; R | Exact/near-duplicate removal and language-model experiments | Large English web-text/language-model corpora | Studies memorization, language-model quality and train–validation overlap after deduplication | Generation/perplexity outcomes do not quantify SMS classifier gains | Preserve parent/campaign groups and audit cross-partition overlap |
| [[12]](#ref-12) | Guo et al., 2017; R | Reliability analysis and post-processing calibration, including temperature scaling | Neural image/document classification benchmarks | Evaluates calibration errors and shows accuracy need not imply reliable probabilities | Not this project's NB/LR models, language slices or class priors | Validate probability interpretation before assigning confidence categories |
| [[13]](#ref-13) | Amparore et al., 2021; R | LEAF diagnostics for LIME/SHAP local linear explanations | Four tabular datasets and multiple classifier families | Evaluates fidelity, local concordance, reiteration similarity and prescriptivity | No SMS or reader-comprehension experiment; post-hoc surrogates differ from direct feature contributions | Check explanation fidelity separately from visual clarity |
| [[14]](#ref-14) | UCI SMS Spam Collection, 2011 citation / 2012 donation; D | Documented collection/provenance and binary-label resource | English SMS from several contributing collections | Repository reports 5,574 instances and CC BY 4.0; actual admitted count requires inspection | Citation year differs from donation date; metadata is not a project inventory or RU/KZ evaluation | Candidate English baseline after permission, privacy, label and duplicate audit |
| [[15]](#ref-15) | Scikit-learn feature extraction; T, undated | Bag-of-words, TF-IDF and word/character n-gram implementation guidance | Explanatory examples; no new target-language corpus | Documents representations and their limitations; no project quality measurement | Technical capability is not empirical evidence of benefit on Kazakh SMS | Makes planned feature experiments reproducible and explicit |
| [[16]](#ref-16) | Scikit-learn scoring documentation; T, undated | Definitions of classification scores and averaging conventions | General classification API/examples | Defines precision/recall/F1 and confusion-matrix interpretation | No experimental performance for this project; label/averaging choices remain necessary | Specify positive class, support, denominators and per-language reports |
| [[17]](#ref-17) | W3C WCAG 2.2, 2024; S | Normative accessibility criteria | Web interfaces; no SMS classification dataset | Criteria 1.4.1 and 4.1.3 address color-independent meaning and status messages | Conformance requires scoped verification; standards are not usability-study findings | Inform explanation/result presentation and planned accessibility checks |

## 5. Cross-Study Critical Analysis

### 5.1. Model complexity is conditional on the comparison

Simple text models [1] and richer SMS configurations [2] provide different evidence. Their results do not establish an unconditional winner: preprocessing, representation, labels, selection procedures and held-out data all affect the comparison. The proposal's NB/LR experiment is justified as a controlled engineering baseline, not as a claimed state of the art. If a more complex model is added, it should use the same permitted data partitions and declared selection criteria, including error behavior and deployment constraints.

Filali et al.'s Table 11 difference is **0.02 percentage points**, with classifier and augmentation changing together. Table 14 reports significant t-tests but Wilcoxon `p = 0.0625` over five seeds, so significance is test-dependent. The collection narrative states 5,572 messages, whereas Table 2 lists 747 spam plus 4,852 ham (5,599); this discrepancy is unresolved. These limitations weaken a superiority claim [2].

Their reported F1 cannot be ranked against Ali et al.'s macro F1 [4]: translated SMS and native Portuguese payment-fraud messages differ in labels, averaging, support and provenance. A headline score cannot isolate an architectural advantage.

SpamDam also adds ordinary tweets as negative examples in some balancing experiments [5]. This changes the negative-class domain and does not establish behavior on representative legitimate SMS. Such balancing should not be copied into the project's primary SMS evaluation.

### 5.2. Language coverage and independent examples matter together

The multilingual studies cover different units: translated SMS [2], linguistic switching patterns [6], mixed-text translation [7] and general Kazakh tasks [8]. None supplies the missing natural RU/KZ binary SMS evaluation. Translation-derived observations may share parents or templates, so counting language versions as independent examples can inflate apparent sample diversity. The project should assess provenance groups before model selection rather than attempting to repair a leaked score after evaluation.

The annotation literature [9] also warns against interpreting consensus as automatic truth. Recipient context can matter for wanted versus unsolicited marketing. Preserving initial decisions and withheld cases exposes this limitation; forcing a binary answer merely to enlarge a dataset would conceal it. These are reasons to use the existing annotation protocol, not evidence that annotation has already succeeded.

### 5.3. Reproducibility, explanations and privacy are separate tests

Leakage controls [10], [11] are necessary for credible comparisons but do not establish population representativeness. Calibration evidence [12] concerns score reliability; explanation diagnostics [13] concern correspondence to model behavior. Neither establishes that a person understands a highlighted fragment or makes a safer decision. User comprehension therefore remains an empirical UX question alongside accessibility checks [17].

There is also a concrete feature/privacy trade-off. Infrastructure research uses URL-related signals [3], whereas the proposed preprocessing masks full URLs and sensitive spans. Its findings cannot be imported unchanged into the text-only classifier. The team must test the utility lost through masking while preserving the agreed privacy boundary. SpamDam's alternative training setting [5] does not resolve the proposed application's consent, storage or verified-feedback requirements.

## 6. Research Gaps

The following gaps are bounded conclusions from this review and the project's present evidence, not claims that no relevant research exists anywhere.

- **Native target-task evidence:** the selected sources do not establish a permitted, independently annotated natural Russian/Kazakh SMS spam/ham benchmark under the project's policy. SpamDam's multilingual search includes Russian [5], so it warrants a source-suitability audit rather than dismissal; eligible native Russian subsets, both-class coverage and reuse conditions were not verified here. Available Kazakh/mixed-language studies concern other tasks [7], [8].
- **Fair multilingual model comparison:** a comparison of NB/LR and candidate character features on identical natural-language, group-aware partitions has not been performed for this project. Translated results [2] cannot fill that gap.
- **Explanation after privacy transformation:** the team still needs an evaluated contract linking actual feature contributions, transformed text and displayed multilingual fragments. General explanation diagnostics [13] motivate scrutiny but do not validate that mapping.
- **Controlled feedback updates:** reviewed labels, reserved-group checks, versioned retraining and candidate promotion must be demonstrated. Adversarial concerns [5] support this caution but do not provide a completed project workflow.
- **Practical relevance and comprehension:** literature and technical standards cannot substitute for real user discussions, task observations or supervisor feedback. Local demand, useful explanations and acceptable processing choices remain to be validated.

## 7. Implications for Our Project

All decisions below are proposed or already documented design commitments, not completed experiments. They trace to [Project Proposal Sections 9–18](project_proposal.md#9-functional-scope), the [Dataset Strategy](dataset_strategy.md), [Annotation Guidelines](annotation_guidelines.md) and [Technology Comparison](technology_comparison.md). During this audit, the requirements specification became available in upstream `main` at commit `2ce69c0`; the `docs/requirements.md` version at that commit is used for traceability without assuming that its pending decisions or implementation criteria are satisfied.

Data/model evidence maps to **NFR-17 and EV-01**; probability and explanations to **FR-03–FR-05**; language coverage to **FR-08–FR-09 and NFR-12**; privacy and controlled contributions/retraining to **FR-11, FR-13–FR-17 and NFR-01–NFR-05**; accessibility and comprehension to **NFR-13 and NFR-20**. The specification's **D-03, D-05 and D-08** leave model interpretation/evaluation, permission/retention and UX acceptance decisions pending. These mappings identify future verification obligations, not passed tests.

| Literature Evidence | Engineering Decision | Justification | Future Validation |
|---|---|---|---|
| Dataset provenance [14] and limits of translated evaluation [2] | Audit the English candidate and seek permitted natural RU/KZ SMS; retain origin flags | A public resource or translated language field does not establish representative target coverage | Reconcile source/permission records, admitted counts and language/class support |
| Feature/task sensitivity [1] and implemented n-gram options [15] | Compare TF-IDF word/character configurations with NB/LR; consider Linear SVM as an additional baseline | Representation and classifier effects must be separated; character-feature benefit remains a hypothesis | Use matched training folds/configurations and development-only model selection |
| Mixed-language research [6]–[8] | Keep `en`, `ru`, `kk`, mixed/undetermined status and script distinct; preserve relevant Unicode | Script and interface language are not evidence of message language or model quality | Competent language review and separate natural/mixed/transliterated slices |
| Annotation disagreement [9] | Retain independent initial judgments and separately record adjudication/withheld cases | A final agreed label alone hides uncertainty and policy disagreements | Report pre-adjudication agreement, coverage, class marginals and reasons for withholding |
| Campaign structure [3] and leakage/deduplication findings [10], [11] | Keep campaigns, derivatives and contributor-related groups within one partition; fit TF-IDF inside training folds | A random stratified split alone does not rule out related examples across partitions | Audit exact/near duplicates, parent links, split manifests and fold-local fitting |
| Metric definitions [16] and heterogeneous benchmarks [2], [4] | Report spam precision/recall/F1, confusion matrices and support per language, plus a declared simple baseline | Aggregate accuracy and unlike F1 averages do not answer the same question | Record positive label, averaging, denominators, thresholds and held-out conditions |
| Probability calibration [12] | Validate score reliability before interpreting probability as confidence | Neural calibration findings motivate a check but do not determine NB/LR behavior | Use development-only calibration/threshold selection and later reliability/error analysis |
| Explanation diagnostics [13] and accessibility criteria [17] | Display genuine classifier contributions with safe text/offset mapping and non-color-only meaning | Model fidelity, Unicode correctness and user comprehension are distinct requirements | Contribution/offset fixtures, keyboard/status checks and real explanation-comprehension observations |
| Public-data/adversarial limitations [3], [5] | Process text transiently by default; separate error flags from consented, reviewed training contributions | Availability and prediction feedback do not establish permission, correct labels or safe model updates | Inspect storage/logging/access; verify labels, versioned retraining, evaluation and rollback before promotion |

Responsibilities remain those of the proposal: Beknur leads data preparation, annotation, UI and consolidation; Rafael leads training/evaluation, model versions and verified-feedback retraining; Sanzhar leads inference/explanations, threshold/error analysis, API and safe persistence. This review does not reassign those components.

## 8. Limitations of This Review

- **Search scope:** targeted web discovery and primary-source checking provide a defensible selected corpus, not exhaustive coverage. No systematic-review completeness or pooled effect size is claimed.
- **Access and version boundaries:** some candidate ACM/MDPI pages were blocked or unavailable and their unverified findings were not included. For [10] and [13], publisher/PMC HTML pages and alternative NSF/university copies were unavailable, but the published full-text XML was subsequently retrieved and inspected through the official Europe PMC API. The unsuccessful HTML/PDF requests are not counted as successful page checks. Published texts now substantiate the cited claims; earlier author manuscripts are not substituted for the final versions or counted again. [5] remains explicitly a preprint.
- **Evidence transfer:** translation, social media, language modeling, general Kazakh tasks, tabular explanation studies and neural calibration each have limits when applied to natural SMS and linear classifiers. Proposed transfers are hypotheses to test, not measured project gains.
- **Verification depth:** relevant primary-text sections, bibliographic records and cited claims were checked. Datasets were not imported, reported experiments were not rerun, and code, licenses, consent arrangements and redistribution rights were not independently audited. Repository metadata is not proof of corpus readiness.
- **Team dependency:** Rafael's ML literature notes were not available in the reviewed repository branches or open Pull Requests. This consolidation therefore uses independently checked publications and does not claim that his analysis or technical review has been completed. Integration of his findings and substantive peer review remain pending.
- **Requirements and user evidence:** the working branch starts at `9d64cc1`; the newly merged upstream requirements at `2ce69c0` were inspected read-only and mapped in Section 7. Local branch synchronization, the specification's open decisions and actual team/supervisor review remain separate steps. Completed user-research findings were not available; priorities and UX acceptance criteria may therefore require revision.

## 9. References

Numbers identify unique works; a publisher record and an accessible copy of the same work share one reference. Publication types R/P/D/T/S are defined in Section 2. Undated technical pages were accessed on 24 October 2026.

<a name="ref-1"></a>
[1] S. Wang and C. D. Manning, “Baselines and Bigrams: Simple, Good Sentiment and Topic Classification,” in *Proceedings of the 50th Annual Meeting of the Association for Computational Linguistics, Volume 2: Short Papers*, Association for Computational Linguistics, 2012, pp. 90–94. **R.** [Publication record](https://aclanthology.org/P12-2018/) · [Full text](https://aclanthology.org/P12-2018.pdf).

<a name="ref-2"></a>
[2] A. Filali, M. Shorfuzzaman, E. A. Abdellaoui Alaoui, M. Merras, M. Es-Sabry, A. Berrajaa, R. Alroobaea, and A. Yousef, “Cross-lingual SMS spam detection using GAN-based augmentation for imbalanced datasets,” *Scientific Reports*, vol. 16, art. 7128, 2026, doi: 10.1038/s41598-026-37769-4. **R.** [Published full text in PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12921278/).

<a name="ref-3"></a>
[3] A. Nahapetyan, S. Prasad, K. Childs, A. Oest, Y. Ladwig, A. Kapravelos, and B. Reaves, “On SMS Phishing Tactics and Infrastructure,” in *2024 IEEE Symposium on Security and Privacy*, IEEE Computer Society, 2024, pp. 1–16, doi: 10.1109/SP54263.2024.00169. **R.** [Author publication record](https://sathviknp.org/publication/2024-02-01-SMS-Phishing) · [Author-hosted full text](https://sathviknp.org/files/sms-phishing-paper.pdf).

<a name="ref-4"></a>
[4] F. D. M. A. Ali, S. M. Saide, R. Sousa-Silva, and H. Lopes Cardoso, “MOZ-Smishing: A Benchmark Dataset for Detecting Mobile Money Frauds,” in *Proceedings of the Sixth Workshop on African Natural Language Processing (AfricaNLP 2025)*, Association for Computational Linguistics, 2025, pp. 158–166, doi: 10.18653/v1/2025.africanlp-1.23. **R.** [Publication record](https://aclanthology.org/2025.africanlp-1.23/) · [Full text](https://aclanthology.org/2025.africanlp-1.23.pdf).

<a name="ref-5"></a>
[5] Y. Li, R. Zhang, W. Rong, and X. Mi, “SpamDam: Towards Privacy-Preserving and Adversary-Resistant SMS Spam Detection,” arXiv:2404.09481, 2024. **P — preprint; peer-reviewed venue not verified.** [Record](https://arxiv.org/abs/2404.09481) · [Inspected version 1](https://arxiv.org/html/2404.09481v1).

<a name="ref-6"></a>
[6] A. S. Doğruöz, S. Sitaram, B. E. Bullock, and A. J. Toribio, “A Survey of Code-switching: Linguistic and Social Perspectives for Language Technologies,” in *Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing, Volume 1: Long Papers*, Association for Computational Linguistics, 2021, pp. 1654–1666, doi: 10.18653/v1/2021.acl-long.131. **R.** [Publication record](https://aclanthology.org/2021.acl-long.131/) · [Full text](https://aclanthology.org/2021.acl-long.131.pdf).

<a name="ref-7"></a>
[7] M. Borisov, Z. Kozhirbayev, and V. Malykh, “Low-resource Machine Translation for Code-switched Kazakh-Russian Language Pair,” in *Proceedings of the 2025 Conference of the Nations of the Americas Chapter of the Association for Computational Linguistics: Human Language Technologies (Volume 4: Student Research Workshop)*, Association for Computational Linguistics, 2025, pp. 66–76, doi: 10.18653/v1/2025.naacl-srw.7. **R.** [Publication record](https://aclanthology.org/2025.naacl-srw.7/) · [Full text](https://aclanthology.org/2025.naacl-srw.7.pdf).

<a name="ref-8"></a>
[8] A. Maxutov, A. Myrzakhmet, and P. Braslavski, “Do LLMs Speak Kazakh? A Pilot Evaluation of Seven Models,” in *Proceedings of the First Workshop on Natural Language Processing for Turkic Languages (SIGTURK 2024)*, Association for Computational Linguistics, 2024, pp. 81–91. **R.** [Publication record](https://aclanthology.org/2024.sigturk-1.8/) · [Full text](https://aclanthology.org/2024.sigturk-1.8.pdf).

<a name="ref-9"></a>
[9] A. N. Uma, T. Fornaciari, D. Hovy, S. Paun, B. Plank, and M. Poesio, “Learning from Disagreement: A Survey,” *Journal of Artificial Intelligence Research*, vol. 72, pp. 1385–1470, 2021, doi: 10.1613/jair.1.12752. **R.** [Publication record](https://www.jair.org/index.php/jair/article/view/12752) · [Full text](https://www.jair.org/index.php/jair/article/download/12752/26751).

<a name="ref-10"></a>
[10] S. Kapoor and A. Narayanan, “Leakage and the reproducibility crisis in machine-learning-based science,” *Patterns*, vol. 4, no. 9, art. 100804, 2023, doi: 10.1016/j.patter.2023.100804. **R.** [Published metadata](https://collaborate.princeton.edu/en/publications/leakage-and-the-reproducibility-crisis-in-machine-learning-based-/) · [Verified published full text (Europe PMC XML)](https://www.ebi.ac.uk/europepmc/webservices/rest/PMC10499856/fullTextXML) · [Earlier author manuscript](https://arxiv.org/pdf/2207.07048).

<a name="ref-11"></a>
[11] K. Lee, D. Ippolito, A. Nystrom, C. Zhang, D. Eck, C. Callison-Burch, and N. Carlini, “Deduplicating Training Data Makes Language Models Better,” in *Proceedings of the 60th Annual Meeting of the Association for Computational Linguistics, Volume 1: Long Papers*, Association for Computational Linguistics, 2022, pp. 8424–8445, doi: 10.18653/v1/2022.acl-long.577. **R.** [Publication record](https://aclanthology.org/2022.acl-long.577/) · [Full text](https://aclanthology.org/2022.acl-long.577.pdf).

<a name="ref-12"></a>
[12] C. Guo, G. Pleiss, Y. Sun, and K. Q. Weinberger, “On Calibration of Modern Neural Networks,” in *Proceedings of the 34th International Conference on Machine Learning*, PMLR, vol. 70, pp. 1321–1330, 2017. **R.** [Publication record](https://proceedings.mlr.press/v70/guo17a.html) · [Full text](https://proceedings.mlr.press/v70/guo17a/guo17a.pdf).

<a name="ref-13"></a>
[13] E. Amparore, A. Perotti, and P. Bajardi, “To trust or not to trust an explanation: using LEAF to evaluate local linear XAI methods,” *PeerJ Computer Science*, vol. 7, art. e479, 2021, doi: 10.7717/peerj-cs.479. **R.** [Published record/text in PMC; HTML access restricted during audit](https://pmc.ncbi.nlm.nih.gov/articles/PMC8056245/) · [Verified published full text (Europe PMC XML)](https://www.ebi.ac.uk/europepmc/webservices/rest/PMC8056245/fullTextXML) · [Author manuscript and journal/DOI record](https://arxiv.org/abs/2106.00461) · [Author manuscript](https://arxiv.org/pdf/2106.00461).

<a name="ref-14"></a>
[14] T. Almeida and J. Hidalgo, “SMS Spam Collection,” *UCI Machine Learning Repository*, 2011, doi: 10.24432/C5CC84. **D.** [Dataset record](https://archive.ics.uci.edu/dataset/228/sms+spam+collection). The repository's recommended citation gives 2011; its donation date is 21 June 2012. Neither date establishes current project counts.

<a name="ref-15"></a>
[15] Scikit-learn developers, “Feature extraction: Text feature extraction,” *Scikit-learn User Guide*, undated. **T.** [Documentation](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction).

<a name="ref-16"></a>
[16] Scikit-learn developers, “Metrics and scoring: Quantifying the quality of predictions,” *Scikit-learn User Guide*, undated. **T.** [Documentation](https://scikit-learn.org/stable/modules/model_evaluation.html#classification-metrics).

<a name="ref-17"></a>
[17] World Wide Web Consortium, “Web Content Accessibility Guidelines (WCAG) 2.2,” *W3C Recommendation*, Dec. 12, 2024. **S.** [Standard](https://www.w3.org/TR/WCAG22/).
