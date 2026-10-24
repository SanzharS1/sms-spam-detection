# Comparison of Existing SMS Spam Detection Solutions

| Field | Value |
|---|---|
| Project | Development of a Web-Based SMS Spam Detection Application Using Machine Learning |
| Group | SE-2425 |
| Author | Beknur Serikkali |
| Task | [DIP-5 — Compare existing SMS spam detection solutions](https://sms-spam-se2425.youtrack.cloud/issue/DIP-5) |
| Date | 24 October 2026 |

## 1. Purpose and comparison methodology

This study compares four existing solutions to inform the scope and requirements of the application defined in the [Project Proposal](project_proposal.md), particularly Sections 9–16. It addresses the first pre-defense requirement for an evidence-based comparison of 3–5 systems using 6–10 consistent criteria. The selected systems are Google Messages, Truecaller, Apple Messages and ScamShield (Singapore).

The method is a documentary comparison of official product documentation, support articles and privacy statements reviewed on 24 October 2026. Ten criteria are applied to all four systems. Relevant evidence is identified by source codes linked to the official pages in Section 8. Product descriptions and privacy assurances are attributed to their publishers; they have not been independently verified through application testing or a security audit.

The study evaluates documented workflows and their relevance to the proposed system. It does not assign accuracy scores or rank classifier quality: there is no common test corpus, controlled installation study or measured comparison in this work. The project's EN/RU/KZ classification, explanations, batch checking and privacy controls remain planned requirements.

## 2. Selection and description of four existing solutions

### 2.1. Google Messages

Google Messages is relevant as an Android messaging application with integrated spam/scam detection and a companion browser interface. Google describes standard protection using on-device processing and enhanced protection that can also use Private AI Compute. Its documentation includes spam warnings, reporting and a Spam & blocked folder. [G1], [G2]

The web interface displays the mobile application's messages through device pairing; it is not evidence of an independent paste-and-classify SMS service. The documented setup connects an Android phone, a browser and a Google Account. [G3]

### 2.2. Truecaller

Truecaller is relevant for third-party SMS organization, fraud warnings and user feedback. Its SMS inbox documentation describes automatic separation of spam/fraud and promotional messages. Android Message ID provides category notifications and fraud warnings, while iPhone SMS filtering has separate setup instructions and country-specific category availability. [T1], [T2], [T3]

Truecaller's web Scam Checker is also included within this system's scope. Its FAQ documents free, account-free checks of phone numbers, URLs and scam types. That functionality must be distinguished from classification of an arbitrary SMS text supplied by the user. [T5]

### 2.3. Apple Messages

The comparison focuses on the documented iPhone Messages workflow, including the iOS 26 guide. Apple's support article describes on-device spam detection in iOS 26 and later, with a Spam folder and recovery of incorrectly filtered messages. [A1]

Unknown-sender screening, transaction/promotion organization and installed third-party filtering extensions are related but distinct functions. Their behavior and availability depend on configuration and region; they must not all be attributed to one built-in spam classifier. [A2], [A3]

### 2.4. ScamShield (Singapore)

ScamShield is relevant as a Singapore-focused mobile service combining checking, reporting and protective filtering. Its official guide describes manual message checking by pasted text or a selected screenshot, with sender details requested in the text workflow. This directly overlaps with the project's proposed single-message checking scenario. [S1], [S2]

ScamShield also presents contextual information about check outcomes and documents a history of reported numbers subsequently added to its blocklist. Those capabilities provide useful comparison points for explanations and feedback tracking. [S1], [S5] The publisher describes the service as free and tailored to scams in Singapore. [S6]

## 3. Comparison criteria and evidence interpretation

The following operational definitions keep the comparison consistent across platforms.

| ID | Criterion | Evidence sought |
|---|---|---|
| C1 | Platform and accessibility | Supported device/application workflow, browser access and dependencies; no accessibility-conformance certification is inferred |
| C2 | Automatic incoming SMS spam filtering | Automatic identification, routing or warnings for received SMS; sender-based screening is distinguished from content classification |
| C3 | Manual SMS text checking | A dedicated workflow accepting an arbitrary pasted SMS for assessment; reviewing an inbox or looking up a number/URL alone is different |
| C4 | Batch file checking | Import of multiple SMS records from a file and corresponding record-level results; screenshot upload alone does not establish this capability |
| C5 | Documented validation for English, Russian and Kazakh SMS | Language-specific evaluation data, conditions and spam precision/recall/F1 or equivalent evidence; interface language and translated examples are insufficient |
| C6 | Explanations for individual classification decisions | Reasons or evidence accompanying an outcome; category badges, reputation signals and model-feature attribution are distinguished |
| C7 | User reporting and incorrect-classification feedback | Reporting suspected spam and correcting false positives; no particular retraining mechanism is inferred from a feedback button |
| C8 | History of classification outcomes | Reviewable outcomes and their scope; message folders and report histories are distinguished from a versioned classification event log |
| C9 | Privacy and message-processing arrangements | Documented processing location, content disclosure, report handling and third-party access, with feature-specific boundaries |
| C10 | Access requirements and permissions | Device, account, configuration, geographic and permission constraints; documented charges or free access are included where established |

**Not established in reviewed sources** means that the cited source set does not substantiate the specific capability or validation claim. It is an evidence gap, not proof that the product lacks the feature. Partial evidence is described explicitly rather than converted into a binary yes/no score. Product capabilities can vary by operating system, release, country, carrier and enabled feature.

For C5, none of the reviewed source sets establishes a reproducible, common EN/RU/KZ SMS benchmark with per-language outcomes. This finding does not establish that these products cannot process Russian or Kazakh. For C6, a useful warning or contextual reason can be valuable without establishing faithful word/character-feature attribution. No aggregate numerical score is calculated because the criteria describe different workflows and evidence levels.

## 4. Comparative matrix

The four columns represent the same systems throughout. Source codes refer to Section 8; unknown entries are bounded by the reviewed documentation.

| Criterion | Google Messages | Truecaller | Apple Messages | ScamShield (Singapore) |
|---|---|---|---|---|
| **C1 — Platform and accessibility** | Android app and paired browser client; web access depends on the mobile messaging setup. [G3] | Android/iPhone workflows differ; a web Scam Checker supports number/URL lookup. [T2], [T3], [T5] | Reviewed spam/filtering workflow is on iPhone; guide scope is iOS 26. Independent browser SMS-text checking: **Not established in reviewed sources**. [A1], [A2] | Mobile workflows are documented for iOS/Android. Public guidance is available online; browser-based SMS classification: **Not established in reviewed sources**. [S1], [S5] |
| **C2 — Automatic incoming SMS spam filtering** | Documented spam/scam protection can flag or route suspected messages to Spam & blocked. [G1] | Automatic spam/fraud routing is documented; iPhone filtering/category availability has separate conditions. [T1], [T2] | On-device Filter Spam is documented for iOS 26+; unknown-sender screening is a separate setting. [A1], [A2] | SMS filtering from unknown contacts is documented; protection requires the relevant configuration/permissions. [S4], [S5] |
| **C3 — Manual SMS text checking** | Arbitrary pasted-SMS checking: **Not established in reviewed sources**. Paired web messaging and reporting concern existing conversations. [G2], [G3] | Arbitrary pasted-SMS checking: **Not established in reviewed sources**. The web checker documents numbers, URLs and scam-type searches. [T5] | Arbitrary pasted-SMS checking: **Not established in reviewed sources**. Reading or recovering a received message is a different operation. [A1], [A2] | Documented: paste message text or upload a screenshot; the text workflow requests sender details. [S1], [S2] |
| **C4 — Batch file checking** | **Not established in reviewed sources** for multi-record SMS files and row-level results. [G1], [G3] | **Not established in reviewed sources** for multi-record SMS files and row-level results. [T1], [T5] | **Not established in reviewed sources** for multi-record SMS files and row-level results. [A1], [A2] | **Not established in reviewed sources**. The documented screenshot/text workflow does not establish batch-file processing. [S1] |
| **C5 — Documented validation for English, Russian and Kazakh SMS** | **Not established in reviewed sources** under the evaluation definition in Section 3. [G1], [G2], [G3] | **Not established in reviewed sources**; category availability is not per-language classifier validation. [T1], [T2], [T3], [T5] | **Not established in reviewed sources**; country-specific filtering does not establish EN/RU/KZ evaluation. [A1], [A2], [A3] | **Not established in reviewed sources**; Singapore-specific design is not native RU/KZ performance evidence. [S1], [S6] |
| **C6 — Explanations for individual classification decisions** | Spam/scam warnings are documented. Individual model-feature contributions: **Not established in reviewed sources**. [G1] | Category colors and fraud warnings are documented. Individual model-feature contributions: **Not established in reviewed sources**. [T3], [T4] | Spam labeling/recovery is documented. Individual model-feature contributions: **Not established in reviewed sources**. [A1] | Outcomes can include known-scam similarity, report information and sender-related context. Word/character-feature attribution: **Not established in reviewed sources**. [S1] |
| **C7 — User reporting and incorrect-classification feedback** | Report spam and report-not-spam actions are documented; blocked conversations can be reviewed. [G1], [G2] | Fraud/spam feedback and Mark as safe corrections are documented. [T4] | Report-spam and not-spam recovery actions are documented; SMS reporting depends on carrier/country. [A1], [A4] | Scam reporting is documented; some scam/spam check outcomes automatically submit a report. A specific false-positive correction workflow: **Not established in reviewed sources**. [S2], [S5] |
| **C8 — History of classification outcomes** | Spam & blocked provides reviewable filtered conversations. A versioned classification event log: **Not established in reviewed sources**. [G2] | Spam/Promotions tabs retain categorized inbox views. A versioned classification event log: **Not established in reviewed sources**. [T1] | Spam-folder review and recovery are documented. A versioned classification event log: **Not established in reviewed sources**. [A1] | Your Scam Reports shows reported numbers added to the blocklist. A full history of every message-check outcome: **Not established in reviewed sources**. [S5] |
| **C9 — Privacy and message-processing arrangements** | Standard protection is on-device; enhanced protection can use Private AI Compute. URL checks and reporting have data flows beyond local processing. [G1] | Publisher describes local processing for Android Message ID. This is feature-specific evidence, not an audit of all app/reporting data flows. [T3] | Built-in spam detection is described as on-device. Installed third-party filters can access unknown-sender content; reporting has separate disclosures. [A1], [A3], [A4] | Privacy statement covers analyzed unknown-sender content, sender details, submitted screenshots/OCR and possible third-party processing. [S3] |
| **C10 — Access requirements and permissions** | Web pairing needs the phone, Google Account and connectivity; carrier/data charges can apply. [G3] | iPhone filter selection and country-specific categories apply. Android notification permissions depend on the feature. Number/URL web checks are free without an account. [T2], [T3], [T5] | Compatible iPhone/OS and configured filters; options vary by region and provider. A separate filtering price: **Not established in reviewed sources**. [A1], [A2], [A3] | Publisher describes free, Singapore-focused access. Filtering needs relevant permissions, including contacts/SMS access in the documented setup. [S4], [S6] |

## 5. Critical discussion of findings

### 5.1. Established strengths and overlapping workflows

The reviewed products address several useful forms of protection: integrated incoming-message handling, third-party SMS organization and explicit assessment of suspicious content. Google Messages documents both mobile protection and companion web messaging; Truecaller documents SMS categories and corrective feedback; Apple documents built-in spam recovery and configurable filtering. [G1], [G3], [T1], [T4], [A1], [A2]

ScamShield already supports manual message assessment and presents contextual signals alongside check outcomes, so manual checking and understandable result information cannot be claimed as unique project contributions. [S1] Truecaller's free web checker also prevents a blanket claim that existing competitors offer no browser access: its documented input domain is numbers, URLs and scam searches. [T5] The relevant distinction is the complete workflow and its evidence, not a general mobile-versus-web dichotomy.

### 5.2. Platform, geography and cost require qualified conclusions

Truecaller's iPhone support article lists enhanced categories for iOS 16 and later in India, Nigeria, South Africa, Kenya, Bangladesh and Sri Lanka, and older category filtering for a separate country list. Kazakhstan is not listed in those category-availability lists; that does not establish that every Truecaller feature is unavailable there. [T2] Apple's guide likewise identifies regional variation, while its privacy notice describes specific transaction/promotion filtering for Brazil and India separately from third-party filters. [A2], [A3]

ScamShield explicitly targets Singapore. Its sender- and authority-related evidence must not be assumed to transfer unchanged to Kazakhstan. [S1], [S6] Store availability, minimum OS requirements and feature behavior in the intended deployment region still require a configuration-specific check; this study does not establish a global installation restriction from regional product focus alone.

For the access arrangements assessed under C10, free use is documented for Truecaller's number/URL checker and for ScamShield. Google identifies potential carrier/data charges for its messaging workflow. [T5], [S6], [G3] The review does not establish comparable total costs for all SMS configurations, devices, subscriptions and regions; it therefore makes no universal cheapest-product or free-equivalent claim.

### 5.3. Validation evidence and label semantics limit accuracy comparisons

A supported interface language or a region-specific feature does not establish measured SMS classification quality for English, Russian or Kazakh. C5 records a gap in the reviewed evidence, not an assertion of language failure. Without matched data, labels and evaluation conditions, documented features cannot justify a numerical accuracy ranking or a claim that the proposed classifier will perform better.

The task boundaries also differ. ScamShield distinguishes scam, spam, uncertain and apparently safe outcomes in its guide; the project's planned binary label `spam` includes unsolicited promotion and deceptive solicitation, while unresolved annotations are withheld from scored datasets. [S2] A comparison of classifier errors would require an explicit label mapping, permitted natural-message data, common evaluation rules and disclosure of coverage. Such an experiment has not been performed.

### 5.4. Explanations, feedback and history are not interchangeable

Category colors, sender reputation, report counts and model-feature contributions provide different kinds of information. Truecaller documents category/fraud indicators, and ScamShield documents contextual reasons; neither source set establishes the specific word/character attribution contract planned in the Project Proposal. [T3], [S1] The absence of that contract from reviewed documentation is not proof that the products have no useful explanations.

Similarly, a Spam folder supports recovery of filtered messages, while a report history tracks a different event. ScamShield's documented history concerns reported numbers that entered its blocklist. [G2], [A1], [S5] A future project history should specify prediction identifiers, time, label/score and model version, access boundaries and deletion behavior instead of implying that message storage alone creates a reproducible audit trail.

### 5.5. Privacy must be evaluated by feature and data flow

On-device classification is a meaningful strength, but it does not by itself describe URL lookups, reporting, browser synchronization or optional enhanced processing. Google's protection modes and encrypted browser cache illustrate these separate boundaries. [G1], [G3] Truecaller's local-processing description applies to Message ID; extrapolating it to all services or voluntarily submitted reports would exceed the evidence. [T3]

Apple distinguishes on-device functionality from the content access available to installed third-party filters and from report handling. [A1], [A3], [A4] ScamShield's privacy annex explicitly covers message content, sender information and screenshot/OCR submissions, with possible processing/disclosure involving service providers. Its guide warns against submitting sensitive personal details. [S3], [S7] These are documented arrangements, not evidence that any product is categorically unsafe or that a web service is inherently more private.

## 6. Implications for the proposed SMS spam detection application

The comparison supports a focused engineering direction already defined in the [Project Proposal](project_proposal.md). The following are planned requirements and evaluation questions, not implemented advantages.

| Finding from the comparison | Implication within the existing project scope | Evidence needed from the project |
|---|---|---|
| Manual checking already exists, and browser access takes several forms | Provide a coherent browser workflow for deliberately submitted SMS without requiring inbox integration | A working single-message scenario, agreed API/UI behavior and real user observations |
| Batch-file assessment is not established in the reviewed workflows | Specify permitted UTF-8/CSV inputs, row-level outputs and explicit invalid-row handling | Reviewed batch contract and functional/privacy tests |
| Matched EN/RU/KZ evaluation is not established by the reviewed sources | Prepare permitted native-language data and report actual spam precision/recall/F1 and support separately by language | Provenance, independent annotation/agreement, group-aware held-out splits and reproducible measurements |
| Warning/context information differs from model-feature attribution | Link the displayed explanation to actual TF-IDF word/character contributions and disclose interpretation limits | Documented contribution method, offset mapping and reviewed explanation examples |
| Reporting and recovery already provide feedback value | Distinguish metadata-only error flags from consented text contributions and controlled retraining | Confirmed labels, restricted review and versioned offline model evaluation before promotion |
| Message/report histories have different semantics | Define a privacy-conscious prediction history with meaningful model/version metadata | Access, retention and deletion rules plus verification of the stored fields |
| Device-local processing is already available in competitors | Assess the privacy trade-off of sending selected text to the proposed API; minimize retention and keep raw text out of normal logs/history | Reviewed processing/storage design, compatible masking and privacy tests |

The proposed niche is therefore a transparent, browser-based SMS assessment and evaluation workflow tailored to the project's English/Russian/Kazakh scope, combining batch handling, faithful explanations and reproducible per-language evidence. This is a design rationale to validate through implementation and user research. Commercial superiority, market uniqueness and confirmed local demand are not established by the comparison.

Responsibilities remain those in the Project Proposal: Beknur leads data preparation, annotation, character-feature experiments, UI and document assembly; Rafael leads the ML training/evaluation pipeline and reviews data splits and duplicates; Sanzhar leads inference, explanations, threshold/error analysis and the API/privacy integration. Automatic inbox interception and carrier-level blocking remain outside the proposed scope.

## 7. Study limitations

- **Documentation and date boundary:** findings reflect the official pages reviewed on 24 October 2026. Some pages are undated or describe older feature subsets; current in-app availability may differ. The iPhone guide references are pinned to iOS 26 where available.
- **Evidence origin:** publisher support material establishes documented behavior and product claims. It does not constitute independent performance, privacy or accessibility validation. No accuracy figures or user-study results are inferred from marketing language.
- **Configuration coverage:** no phones were provisioned and no live messages were submitted. Device, carrier, store-region and subscription-specific behavior remains untested.
- **Unknown features:** negative conclusions are limited to the reviewed source set. Undocumented batch processing, arbitrary-text checks, model explanations or history functions may exist elsewhere; the matrix does not claim exhaustive absence.
- **Language and domain:** this study does not establish EN/RU/KZ accuracy, natural-language coverage or cross-country transfer for any competitor. Scam/phishing detection, promotion classification and the project's spam/ham policy are not identical label spaces.
- **Privacy comparison:** policy descriptions are not a legal-compliance assessment or a security audit. On-device, submitted-content and reporting paths require separate interpretation.
- **Project maturity:** implementation, native RU/KZ data permissions, user relevance evidence and model results remain dependencies. A documentation comparison cannot verify that the planned system satisfies those requirements.

## 8. References

All sources below are official developer or service-operator publications, accessed on 24 October 2026. Source identifiers used in the text and matrix link to the corresponding pages.

### Google

- **G1.** Google. [How Google protects your privacy with spam and scam protection][G1]. Protection modes, spam handling and processing arrangements.
- **G2.** Google. [Block senders & report spam in Google Messages][G2]. Reporting, blocked conversations and the Spam & blocked view; computer instructions.
- **G3.** Google. [Check your messages on your computer or Android tablet][G3]. Paired web access, setup, charges and browser caching.

### Truecaller

- **T1.** Truecaller Support. [Why don't I see all my SMS in the Messages inbox?][T1]. Spam/fraud and promotion routing.
- **T2.** Truecaller Support. [How do I enable SMS Filtering on iPhone][T2]. Filter setup and country-specific category lists, including enhanced categories for iOS 16 and later.
- **T3.** Truecaller. [Message ID for SMS Senders][T3]. Android notifications, feature permissions and publisher-described local processing.
- **T4.** Truecaller Support. [Fraud Warnings][T4]. Mark-as-safe corrections and message/sender feedback.
- **T5.** Truecaller. [Scam Checker][T5]. FAQ on phone-number/URL/scam-type checks and free account-free access.

### Apple

- **A1.** Apple Support. [View and recover spam messages on your iPhone][A1]. On-device spam filtering and recovery in iOS 26 and later; published 17 September 2026.
- **A2.** Apple. [Screen and filter text messages on iPhone][A2]. iPhone User Guide, iOS 26; unknown-sender and text-filter configuration.
- **A3.** Apple. [Text Message Filtering & Privacy][A3]. Third-party content access and specific on-device filtering arrangements; dated 12 December 2025.
- **A4.** Apple. [Report spam and block senders in Messages on iPhone][A4]. iPhone User Guide, iOS 26; reporting, recovery and carrier/country qualifications.

### ScamShield

- **S1.** ScamShield. [How to check for scams on ScamShield app][S1]. Manual checking overview; updated 18 May 2026.
- **S2.** ScamShield. [How to check a scam message][S2]. Text/screenshot inputs, check outcomes, contextual evidence and reporting behavior.
- **S3.** Government Technology Agency, Singapore. [ScamShield Privacy Statement][S3]. Service data handling and mobile-application annex; statement dated 13 October 2025, page updated 8 April 2026.
- **S4.** ScamShield. [Why does ScamShield need access to my contacts, make and manage phone calls, and send and view SMS?][S4]. Unknown-contact filtering and permissions.
- **S5.** ScamShield. [Setup Notifications][S5]. iOS/Android guidance and the scope of Your Scam Reports history.
- **S6.** ScamShield. [Why us?][S6]. Free access and Singapore-specific purpose.
- **S7.** ScamShield. [Privacy Policy][S7]. Guidance on sensitive information in checking/reporting submissions and link to the complete privacy statement.

[G1]: https://support.google.com/messages/answer/9327903?hl=en
[G2]: https://support.google.com/messages/answer/7029021?hl=en
[G3]: https://support.google.com/messages/answer/7611075?hl=en
[T1]: https://support.truecaller.com/support/solutions/articles/81000392326-why-don-t-i-see-all-my-sms-in-the-messages-inbox-
[T2]: https://support.truecaller.com/support/solutions/articles/81000406341-how-do-i-enable-sms-filtering-on-iphone
[T3]: https://www.truecaller.com/message-id
[T4]: https://support.truecaller.com/support/solutions/articles/81000410682-fraud-warnings
[T5]: https://www.truecaller.com/scam-checker
[A1]: https://support.apple.com/en-gb/124159
[A2]: https://support.apple.com/guide/iphone/screen-and-filter-texts-iph203ab0be4/26/ios/26
[A3]: https://www.apple.com/legal/privacy/data/en/sms-filtering/
[A4]: https://support.apple.com/guide/iphone/report-spam-and-block-senders-iph3f94d910d/26/ios/26
[S1]: https://www.scamshield.gov.sg/check-for-scams/how-to-check-for-scams-on-scamshield-app/
[S2]: https://guide.scamshield.gov.sg/using-scamshield/check-for-scams/how-to-check-a-scam-message
[S3]: https://www.scamshield.gov.sg/privacy/
[S4]: https://guide.scamshield.gov.sg/resources/help-center/your-privacy/why-does-scamshield-need-access-to-my-contacts-make-and-manage-phone-calls-and-send-and-view-sms
[S5]: https://guide.scamshield.gov.sg/getting-started/new-setup-notifications
[S6]: https://guide.scamshield.gov.sg/introduction/why-us
[S7]: https://guide.scamshield.gov.sg/legal/privacy-policy
