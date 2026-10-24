# SMS Spam/Ham Annotation Guidelines

| Field | Value |
|---|---|
| Project | Development of a Web-Based SMS Spam Detection Application Using Machine Learning |
| Group and task | SE-2425; [DIP-4](https://sms-spam-se2425.youtrack.cloud/issue/DIP-4) |
| Author and annotation lead | Beknur Serikkali |
| Technical reviewer | Rafael Shaekhov |
| Supporting independent annotator | Sanzhar Sabyrov |
| Date | 24 October 2026 |

## 1. Purpose and annotation unit

These guidelines operationalize the binary task in the [Dataset Strategy](dataset_strategy.md) and [Project Proposal](project_proposal.md), Sections 8 and 14–18. The unit is one complete, permitted SMS, including concatenated segments when they are known to form one message. A pasted conversation, web article, email or Telegram post is not automatically an SMS unit. Do not split one solicitation into multiple apparently independent records.

Annotate meaning and communicative purpose, not the presence of a suspicious word. The final classifier labels are `spam` and `ham`; `uncertain` and `unusable` are workflow decisions excluded from binary training/evaluation until resolved. A binary decision does not certify sender authenticity, link safety or legal status.

## 2. Spam definition

Assign `spam` when the available evidence supports unsolicited promotional solicitation or deceptive/abusive solicitation. Included cases are unsolicited mass offers, prize/advance-fee scams, credential or payment-information harvesting, deceptive impersonation and other unwanted solicitations. Record the relevant rule and a short text-based rationale.

Use the following reason codes:

| Code | Decision basis |
|---|---|
| S1 | Unsolicited promotional solicitation, supported by documented recipient/source context |
| S2 | Deceptive prize, reward, advance-payment or similar solicitation |
| S3 | Phishing, credential/payment-data harvesting or deceptive impersonation |
| S4 | Other clearly unwanted abusive solicitation; explain the pattern for reviewer approval |

Fraud-related content is included within spam for this project's binary task. Do not add a third model class called `fraud`. Optional subtype/reason codes are annotation metadata only.

## 3. Ham definition

Assign `ham` to legitimate personal communication, requested service/transactional information, and legitimate commercial communication for which the relevant requested/authorized context is supported. A message can contain money, a URL, an authentication-code placeholder or an advertisement and still be ham.

| Code | Decision basis |
|---|---|
| H1 | Ordinary personal, educational or work coordination |
| H2 | Expected transactional/service notice, including a requested authentication message |
| H3 | Legitimate requested or subscribed commercial information |

A sender's claim to be a bank, courier or familiar person is not verification. Conversely, bad grammar, a short URL, urgency or a digit sequence alone is insufficient evidence of spam. Absence of proof of fraud does not establish ham.

## 4. Decision procedure

Apply the same order to every record:

1. **Eligibility:** confirm intake permission/privacy status and that the record is a complete, readable SMS. If not, use `unusable` or return it to intake without adding a binary label.
2. **Language competence:** identify the primary language bucket and script under Section 10. Request competent review if meaning is uncertain; do not guess.
3. **Meaning:** read the complete redacted text and the same approved context available to the other annotator. Identify what action or information the sender seeks to convey.
4. **Deceptive solicitation:** apply S2/S3 when supported by the content and documented context. A credential request embedded in an otherwise routine-looking message is not canceled by its greeting or sender branding.
5. **Commercial consent/context:** use S1 for documented unsolicited promotion and H3 for legitimate requested promotion. If the same wording could be wanted or unwanted and context is absent, use `uncertain` with U1.
6. **Ordinary or transactional communication:** apply H1/H2 where supported. Do not label all unknown-sender, commercial, OTP or money-related text as spam.
7. **Record the decision:** save the label/workflow status, reason code, uncertainty and concise rationale before seeing another annotator's decision.

Use only approved collection context. Do not open message links, search a recipient's identity, contact a sender, or use classifier predictions as an answer key. Unknown recipient relationships remain unknown. If labels depend on context unavailable to the future text-only model, flag `context_required`; review indistinguishable/contradictory texts before inclusion, and disclose the irreducible limitation.

## 5. Inclusion and exclusion criteria

Include permitted, privacy-reviewed natural EN/RU/KZ SMS with an interpretable meaning and defensible label. Retain informal language, spelling errors, emoji and mixed scripts. Source labels are evidence about the original collection, not proof of independent human validation under this protocol. Keep them in a separate `source_label` field.

Exclude from the primary natural-message corpus non-SMS text, empty/corrupted records, incomplete fragments without recoverable meaning, unsupported languages pending review, prohibited private content and records without reuse permission. Translations and synthetic examples must be marked as such and handled separately under Dataset Strategy Sections 3 and 15. Other-domain category labels cannot be imported as SMS spam/ham labels.

If an original label conflicts with these definitions, record the conflict and request review. Do not silently relabel a whole provider dataset or assume every unknown commercial message is unsolicited. Any upstream labels retained without fresh annotation must remain visibly identified as upstream decisions with an audit status.

## 6. Illustrative examples

**All messages below are synthetic illustrations of the annotation rules.** The stipulated context guides each decision and must not be assumed for real messages. Placeholders follow Dataset Strategy Section 9.

| Language/script | Synthetic SMS | Stipulated context | Decision and reason |
|---|---|---|---|
| EN | Can we meet at the library at 10 tomorrow? | Ordinary coordination; no solicitation evidence | `ham`, H1 |
| EN | Your requested sign-in code is `__otp__`. Do not share it. | Recipient requested the sign-in; no request to disclose the code | `ham`, H2 |
| EN | Here is the sale reminder you subscribed to. Details: `__url__`. | Legitimate subscription is documented | `ham`, H3 |
| EN | You won a cash prize! Send your card security code here to claim it: `__url__`. | Fabricated prize and credential-harvesting solicitation | `spam`, S2/S3 |
| RU | Встретимся завтра в библиотеке в 10:00? | Ordinary coordination | `ham`, H1 |
| RU | Ваш заказ готов к выдаче. Номер заказа: `__account__`. | Recipient placed the order; legitimate notification | `ham`, H2 |
| RU | Только сегодня скидка 50%! Подробности: `__url__`. | Whether the promotion was requested is unknown | `uncertain`, U1 |
| RU | Вы выиграли приз! Пришлите код с обратной стороны карты для получения: `__url__`. | Deceptive prize and request for card security details | `spam`, S2/S3 |
| KZ/Cyrillic | Ертең сағат 10:00-де кітапханада кездесеміз. | Ordinary coordination | `ham`, H1 |
| KZ/Cyrillic | Сіз сұратқан растау коды: `__otp__`. Кодты ешкімге айтпаңыз. | Requested authentication notice | `ham`, H2 |
| KZ/Cyrillic | Сіз жүлде ұтып алдыңыз! Оны алу үшін картаңыздың құпия кодын жіберіңіз: `__url__`. | Deceptive prize and request for card security details | `spam`, S2/S3 |
| KZ/Latin | Erten sagat 10-da kezdesemiz. | A competent reviewer identifies transliterated Kazakh coordination | `ham`, H1; `language=kk`, `script=Latin` |
| Mixed | Сәлем! Meeting moved to 15:00, бүгін кеңседе кездесеміз. | Legitimate work coordination with substantive language mixing | `ham`, H1; `language=mixed` |
| RU | Инструкция по безопасности: никому не сообщайте код `__otp__`. | Legitimate safety reminder; warning against disclosure | `ham`, H2 |
| Undetermined | `__person__` `__account__` `__url__` | Necessary redaction removed the whole communicative meaning | `unusable`, X3 |

Keywords such as “prize”, “скидка” or “код” do not define the label on their own. A quoted scam discussed in an ordinary conversation is not itself an attempted scam; review the complete message's purpose.

## 7. Ambiguous and context-dependent cases

Use `uncertain` when evidence cannot support a defensible binary decision. Assign a reason:

| Code | Ambiguity | Required action |
|---|---|---|
| U1 | Requested versus unsolicited marketing is unknown | Ask for permitted collection context through the data lead; otherwise withhold |
| U2 | Language, slang, transliteration or sarcasm is unclear | Obtain a competent independent language review |
| U3 | Possible impersonation or fraud cannot be resolved from available evidence | Reviewer assesses content/context; never test the link or contact the sender |
| U4 | Missing conversation context, contradictory upstream label or indistinguishable model text with conflicting labels | Adjudicate; exclude if the necessary distinction remains unavailable |

Urgency, a brand name, an unsubscribe instruction or polished grammar is not decisive. A complaint about spam or a forwarded warning may be ham; a disguised credential solicitation may be spam. If meaningful redaction changes the decision, return the record for privacy review rather than interpreting masked names or numbers as suspicious features.

Do not set `final_label` from an annotator's guess or confidence level. Unresolved items remain outside training and all scored evaluation sets, with counts and reasons reported. They may support a separately described qualitative challenge set, never silently disappear from the intake inventory.

## 8. Commercial and transactional messages

An expected receipt, appointment reminder, delivery update, bank notification or requested sign-in code is a ham candidate under H2. It is not automatically ham merely because it resembles a known template. Assess deceptive requests and the available context first.

Legitimate subscribed offers use H3; documented unsolicited offers use S1. An advertisement's commercial subject alone does not establish the recipient's preference. Distinguish permission to contribute a message to research from permission to receive marketing; they are separate facts. Record subscription/transaction context as restricted annotation metadata, not model input.

An unexpected OTP is not automatically spam or proof of a compromised account. Without sufficient context, use U3/U4. A message requesting disclosure of a security code to claim a prize fits S2/S3. Annotators do not make security guarantees or act on message instructions.

## 9. Language-specific review

Apply identical spam/ham definitions across English, Russian and Kazakh. Reviewer language competence is required; Cyrillic script, a model's language guess or UI selection is insufficient. Preserve Kazakh-specific letters and Russian `ё`. Do not penalize spelling, grammatical variation, regional wording or nonstandard punctuation.

Annotators may record a reviewed language correction without changing the binary decision. A language correction must propagate to inventory and reporting slices. If no team member can reliably interpret a record, keep it pending competent assistance rather than producing an assumed label or undocumented machine translation.

## 10. Mixed-language and transliterated text

Use the mutually exclusive primary language values `en`, `ru`, `kk`, `mixed`, `und` and `other`. Set `mixed` only when two or more languages contribute substantive meaning; brands, URLs and isolated borrowed words do not suffice. Record components and script separately. Native language written in Latin transliteration may retain `ru`/`kk` when competently identified.

Do not transliterate or translate text before the independent decision. If a translation is later used for assistance, retain its method and flag, obtain a competent review and preserve the original's group linkage. Assistance does not turn a translated record into a natural target-language SMS. Each record contributes to only one primary language result table.

## 11. Unusable examples and privacy returns

Use `unusable` with a final label of null for:

- **X1:** empty, corrupted, unreadable or materially incomplete text;
- **X2:** non-SMS or outside the supported language/domain scope;
- **X3:** redaction removes the meaning needed for labeling;
- **X4:** missing permission, prohibited content retention or unresolved privacy risk.

Annotators should receive only screened content. If residual personal information appears, stop processing that item, flag it to Beknur and avoid copying it into rationales or discussion logs. Use the record ID in review communication. A privacy return is an intake/quality event, not evidence that the message is spam. Record whether corrected text is later resubmitted under a new version.

## 12. Annotation record format

Retain one immutable decision row per annotator, record and guideline version. Keep adjudication separately so initial judgments cannot be overwritten. The working format is UTF-8 JSONL with the following logical fields:

| Field | Values or purpose |
|---|---|
| `record_id`, `annotation_batch_id` | Link to the restricted data inventory |
| `annotator_id`, `annotated_at` | Pseudonymous reviewer and decision timestamp |
| `guideline_version`, `text_version` | Exact policy and redacted text seen |
| `language`, `language_components`, `script` | Reviewed primary bucket and script |
| `decision` | `spam`, `ham`, `uncertain` or `unusable` |
| `reason_codes`, `rationale` | One or more codes; concise explanation without personal information |
| `confidence` | Optional `high`, `medium`, `low`; never a substitute for the label |
| `context_ref`, `context_required`, `privacy_flag` | Restricted evidence reference and review flags |
| `independent` | Whether the decision was submitted without another label/model prediction |

The dataset record separately stores `source_label`, `label_origin`, `annotation_status`, `final_label`, decision references, `adjudication_ref` and group/version fields from Dataset Strategy Section 7. `label_origin` distinguishes upstream retention, independently agreed human labels and adjudicated labels. An uncertain/unusable decision never enters a model as a third class.

The synthetic decision record below uses the example guideline identifier `example-guidelines-v1`:

```json
{"record_id":"example-en-001","annotation_batch_id":"example-only","annotator_id":"annotator-a","annotated_at":"2026-10-24T10:00:00+05:00","guideline_version":"example-guidelines-v1","text_version":"synthetic-1","language":"en","language_components":["en"],"script":"Latin","decision":"ham","reason_codes":["H1"],"rationale":"Ordinary meeting coordination.","confidence":"high","context_ref":null,"context_required":false,"privacy_flag":false,"independent":true}
```

## 13. Independent cross-labeling and pilot

Beknur coordinates the batches and serves as a primary annotator; Sanzhar contributes independent cross-labeling as specified in the proposal. Rafael contributes technical review of data quality and evaluation implications within his project responsibilities. Assign only language-competent reviewers. If the primary pair cannot interpret a language reliably, obtain qualified assistance before labeling it.

Start with a proposed pilot of up to 60 natural, permitted records, seeking approximately 20 per language and both classes where available. These are planning targets rather than collected counts. Use available records if fewer exist, report gaps and keep all pilot leakage groups training-only because discussion may shape the policy.

For the pilot, both annotators read the same screened text and approved context independently, without upstream labels, model predictions or each other's decisions. Lock initial submissions, calculate agreement, then discuss failures and revise rules. New pilot rounds require newly unseen records and versioned results; do not report a relabeling after discussion as independent agreement.

Under the proposed initial protocol, independently double-label all newly collected natural RU/KZ records and all proposed primary validation/test records, including imported EN items. On imported EN training material, independently audit a seeded sample of at least 10% of canonical records or 50 records, whichever is larger, capped at the available number. Sample with seed `42`, cover both source classes where available, record inclusion probabilities and identify the sample as an audit rather than full relabeling. Inspect all conflicts and privacy flags in addition to that sample; do not mix targeted cases into the random-audit agreement estimate.

## 14. Inter-annotator agreement

Compute agreement on locked initial decisions **before** discussion or adjudication. Count canonical messages once; duplicated campaign text must not inflate the sample. For each batch and primary language, report:

1. Total records assigned; numbers with both responses; binary-pair coverage; each annotator's uncertain/unusable counts; exclusions and missing judgments.
2. A decision table over all four workflow values to expose abstentions and unusable items.
3. On pairs where both decisions are binary, a 2 × 2 table with each annotator's spam/ham marginals, raw agreement and unweighted Cohen's kappa [A1].

Let `n` be the binary-pair count, `n_hh` and `n_ss` the matching ham and spam counts, and `a_h`, `a_s`, `b_h`, `b_s` the two annotators' class totals. Calculate:

```text
observed_agreement = (n_hh + n_ss) / n
expected_agreement = (a_h*b_h + a_s*b_s) / n^2
kappa = (observed_agreement - expected_agreement) / (1 - expected_agreement)
binary_pair_coverage = n / number_of_records_with_two_initial_decisions
```

If `n=0`, report the binary statistics as not estimable. If expected agreement is 1, report kappa as undefined, with the class table; do not replace it with perfect agreement. If no records have two decisions, coverage is also undefined. Disclose missing classes, low support, class imbalance and the number of independent campaign groups. High raw agreement alone is insufficient when almost every record is ham.

Report pilot, representative audit and targeted difficult-case results separately. Where enough groups exist, group-bootstrap the paired records for uncertainty intervals and record seed/resampling settings; otherwise disclose that uncertainty could not be estimated reliably. No agreement score, universal cutoff or measured language quality is established here. Rafael and Beknur should assess disagreement patterns and feasibility during the pilot; systematic unresolved ambiguity requires revised guidance or exclusion, even if an aggregate score looks favorable.

## 15. Disagreement resolution and adjudication

After initial judgments and statistics are locked, compare decisions using record IDs. Beknur and Sanzhar explain the applicable rule and evidence without changing their original submissions. Agreements can receive a final label only if permission/privacy checks pass. Disagreements, uncertain items, source-label conflicts and material language mismatches require review under the same guidelines. Rafael contributes technical assessment of their effects on data quality and evaluation; linguistic uncertainty requires a reviewer competent in the relevant language.

Beknur coordinates the adjudication process and maintains a separate record of the resolution reached by the annotators and a qualified reviewer. The record includes the record/text version, initial decision references, reviewer, reviewed evidence, applicable rule, final label or withheld status, rationale, date and guideline version. A reviewer who supplied an initial label must not provide the sole independent review of that case; seek another qualified reviewer. If evidence or language competence is insufficient, or no defensible resolution is reached, retain the item as withheld rather than assigning a label by authority alone.

Do not resolve conflicts by model majority vote, classifier probability or a quota for class balance. If a case reveals a missing rule, record the policy change, locate earlier affected decisions and re-review them in a new version. Agreement figures remain tied to the original independent round.

## 16. Duplicates, campaigns and related examples

Use Dataset Strategy Sections 11–12 to identify exact and near duplicates across sources. Annotate a canonical exact-text record, preserving all source links and original label conflicts. Validate that any propagated decision applies to the same reviewed text and context. Do not propagate labels across merely similar campaigns: variants may change meaning or legitimacy.

Choose distinct canonical messages for agreement reporting and report the group count. Review near-duplicate variants individually when their meaning differs, but keep their leakage group intact. Translations and generated variants retain parent links and origin flags. No original, derivative, contributor or campaign group may cross train/validation/test boundaries. Do not adjust a label to make a split feasible; correct labels and then rerun the documented pre-lock split procedure if needed.

## 17. Quality assurance and reviewer handoff

Before an annotation batch is accepted, Beknur checks schema completeness, allowed decisions, rationale/code consistency, readable multilingual text, permission/privacy status, independent-decision locks and reconciliation of all assigned records. Check disagreements, all withheld cases and a separate spot-check sample of agreed labels. Log who reviewed what; spot checks do not replace independent labeling.

Inspect class/language/source distributions for unexpected patterns and template shortcuts, including “URL means spam”, “commercial means spam” and language/script bias. Do not force a preferred class ratio. Preserve a list of unresolved reasons and affected records. A batch requires correction if applicable rules were misunderstood, personal information remains or annotation evidence is missing.

Handoff to Rafael contains the finalized permitted labels, origin flags, agreement report, adjudication log, exclusion summary, group manifest and policy versions. Handoff to Sanzhar contains the agreed binary semantics and redaction/offset contract, with synthetic examples; it does not authorize copying private corpus text into API fixtures.

## 18. Version tracking and corrections

Version these guidelines independently from dataset and model versions. Record every change to definitions, reason codes, language policy, sampling or adjudication. A change log must identify the rationale, reviewer, affected batches and re-review requirement. Preserve earlier independent decisions for audit; do not rewrite them in place.

Changing a redacted text creates a new `text_version` and requires checking whether its label, group and partition remain valid. A label/membership/split correction creates a new dataset version. If held-out evaluation has already occurred, disclose the correction and test exposure; a revised test is not automatically new untouched evidence.

## 19. Evaluation and feedback boundaries

Final labels and group assignments feed the 70/15/15 target split with seed `42` in Dataset Strategy Section 15. All proposed primary validation/test items require independent annotation and completed adjudication before locking. Those sets contain natural, permitted SMS, excluding annotation-pilot groups, translations and synthetic examples. Actual sizes depend on available independent groups; missing language coverage must remain visible.

Do not show predictions to annotators during independent corpus labeling. A later user error report is a claim to review, not a verified training label. Metadata-only feedback cannot supply missing message text; text retention needs separate consent and privacy review. Accepted feedback must pass this protocol, be checked against reserved evaluation groups and enter a versioned offline training process. No feedback directly updates the live classifier.

Rafael leads evaluation and controlled retraining behavior; Sanzhar leads inference, explanations, threshold/error analysis and safe API integration; Beknur leads data/annotation and the UI. The meaning of labels stays stable across components. Neither a ham annotation nor a high predicted confidence certifies safety.

## 20. Privacy and permitted-use requirements

Annotate only within approved storage/access arrangements. View screened, redacted content and minimal necessary context; keep contributor/contact evidence separate. Do not include original names, phone numbers, account details or private URLs in rationales, screenshots, public issues, commits or presentations. Use synthetic examples for public explanation. Do not upload private text to public annotation, translation or model services.

Follow each source's permitted-use record. Research contribution permission and public redistribution permission are separate; neither is implied by an available dataset card. Apply agreed retention and withdrawal procedures and propagate removals through active dataset versions and future retraining as required by the approved process. Public repository documentation does not make a private corpus public. Collection cannot begin until these arrangements and any required university approval are resolved.

## 21. Supporting references

- **A1.** Scikit-learn developers. [Cohen's kappa: definition and computation](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.cohen_kappa_score.html). Consulted 24 October 2026. The project uses the unweighted nominal-label definition and reports undefined cases explicitly.
- **A2.** [Multilingual SMS Dataset Strategy](dataset_strategy.md), especially Sections 2–4, 7–17 and 21–24: shared definitions, source restrictions, preparation, partitioning, evaluation and unresolved dependencies.
- **A3.** [Project Proposal](project_proposal.md), Sections 8 and 14–18: responsibilities, multilingual scope, privacy and evaluation approach.

Data collection, independent annotation and agreement assessment remain planned; no measured performance or agreement results are reported.
