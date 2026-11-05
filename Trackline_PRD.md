# Product Requirements Document: Trackline

**Treatment monitoring for psychiatric clinics**

| Field | Value |
|---|---|
| Product | Trackline (working name) |
| Document type | Product Requirements Document (PRD) |
| Version | 0.2 (draft for discovery) |
| Date | November 2026 |
| Status | Draft: contains hypotheses marked **[TO VALIDATE]** |
| Source | [psychiatry_treatment_monitoring_app_PRD_brief.md](./psychiatry_treatment_monitoring_app_PRD_brief.md) |
| Launch market | Israel |
| Owner | Product (TBD) |
| Clinical lead | Psychiatrist adviser / medical director (TBD) |

> **How to read this document.** Items marked **[TO VALIDATE]** are hypotheses, not facts. They must be confirmed in discovery, legal review, or the pilot before they are treated as requirements. Requirement IDs (for example, `EP-01`) are stable references for design, engineering, and QA; IDs are never reused or renumbered. Priorities throughout the document: **M** = Must (MVP), **S** = Should (MVP if time allows), **C** = Could (later).

### Document history

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | November 2026 | Product | Initial draft from the PRD brief. |
| 0.2 | November 2026 | Product | Fixed timeline and phase-naming inconsistencies; defined baseline, episode and display statuses, "relevant appointment", and overdue/expired rules; added dashboard (DB) requirements, consent withdrawal, partial-submission safety alerts, vendor support access, AI pseudonymization, instrumentation, MVP decision log, and expanded glossary. |

### Approvals

| Role | Name | Status |
|---|---|---|
| Product owner | TBD | Pending |
| Clinical lead | TBD | Pending |
| Engineering lead | TBD | Pending |
| Privacy / legal counsel | TBD | Pending |

---

## Table of contents

1. [Executive summary](#1-executive-summary)
2. [Background and problem statement](#2-background-and-problem-statement)
3. [Customer, buyer roles, and user personas](#3-customer-buyer-roles-and-user-personas)
4. [Product vision and objectives](#4-product-vision-and-objectives)
5. [Competitive landscape and differentiation](#5-competitive-landscape-and-differentiation)
6. [Scope: in scope, out of scope, and future roadmap](#6-scope-in-scope-out-of-scope-and-future-roadmap)
7. [User stories and acceptance criteria](#7-user-stories-and-acceptance-criteria)
8. [Detailed functional requirements](#8-detailed-functional-requirements)
9. [Patient and guardian/caregiver check-in experience](#9-patient-and-guardiancaregiver-check-in-experience)
10. [Clinician dashboard specification](#10-clinician-dashboard-specification)
11. [Clinic administration and usage/value report](#11-clinic-administration-and-usagevalue-report)
12. [AI feature specification and guardrails](#12-ai-feature-specification-and-guardrails)
13. [Safety-alert workflow specification](#13-safety-alert-workflow-specification)
14. [Data model outline](#14-data-model-outline)
15. [Privacy, security, clinical safety, and compliance](#15-privacy-security-clinical-safety-and-compliance)
16. [Non-functional requirements](#16-non-functional-requirements)
17. [Pricing, sales model, onboarding, and customer success](#17-pricing-sales-model-onboarding-and-customer-success)
18. [Key metrics and success criteria](#18-key-metrics-and-success-criteria)
19. [MVP release plan and phased roadmap](#19-mvp-release-plan-and-phased-roadmap)
20. [Risks, assumptions, dependencies, and open questions](#20-risks-assumptions-dependencies-and-open-questions)
- [Appendix A: Glossary](#appendix-a-glossary)
- [Appendix B: Requirement ID prefixes](#appendix-b-requirement-id-prefixes)

---

## 1. Executive summary

**Trackline** is a B2B, clinician-facing treatment-monitoring SaaS product sold to psychiatric clinics in Israel. Patients, and where relevant their guardians or caregivers, complete short check-ins between visits (under 60 seconds) about symptoms, medication adherence, and side effects. Trackline turns this data into a clinician dashboard and a concise **pre-visit briefing**, so psychiatrists start each appointment already informed and can spot deterioration, non-adherence, and side effects earlier.

**Who pays:** the clinic (private practice, group practice, or clinic network). Patients use Trackline for free as part of their care.

**What Trackline is not:** a consumer mental-health app, an AI therapist, a diagnostic tool, a risk-prediction tool, or a medication-recommendation engine. Clinicians keep full clinical judgment and accountability.

**Initial focus:** monitoring episodes that follow a **medication change** (start, stop, or dose change) in small to mid-sized private psychiatric clinics (about 2 to 20 clinicians) in Israel.

**Key differentiators [TO VALIDATE]:**

- Hebrew-first and RTL, with Arabic, Russian, and English to follow.
- Built for Israeli privacy law and data residency from day one.
- Works for communities that generic tools miss, especially Haredi patients: staff-assisted phone check-in, filter-friendly web pages, discreet messaging, and Shabbat-aware scheduling.
- Guardian and caregiver reporting for minors and dependent adults, with strict confidentiality.
- A narrow, low-burden workflow designed to fit a short psychiatric appointment.

**MVP goal:** validate within 90 to 120 days of the first pilot going live that at least 3 (target 5) Israeli clinics use the workflow repeatedly and that at least 2 convert to paid annual contracts (see go/no-go criteria in [section 18.5](#185-go--no-go-criteria-90120-days-after-pilot-launch)).

---

## 2. Background and problem statement

### 2.1 Context

Measurement-based care (routinely collecting patient-reported outcomes and using them in treatment decisions) is associated with better outcomes in psychiatry. In practice, it is rarely implemented well because it adds administrative work, relies on long forms, and sits outside the clinical workflow and the clinic's electronic medical record (EMR).

The weeks after a psychiatric medication change are a high-risk period: side effects emerge, adherence drops, and symptoms may worsen before they improve. Today, clinicians often learn about these problems only at the next visit, through ad-hoc phone calls or WhatsApp messages, or after a crisis.

### 2.2 Clinic-level problem (why the clinic pays)

| Problem | Impact on the clinic |
|---|---|
| Clinicians re-collect information during the visit that could have been gathered beforehand. | Lost appointment time and lower clinician productivity. |
| Deterioration between visits is detected late. | Avoidable urgent contacts, crisis visits, and patient drop-out (lost revenue). |
| No structured data on outcomes, engagement, or quality of care. | Nothing to show patients, health funds, insurers, or partners. |
| Manual follow-up calls after medication changes. | Nursing and staff time consumed; follow-up is inconsistent. |

### 2.3 Clinician-level problem

- Psychiatrists have short appointments and limited time to gather a between-visit history.
- Patient recall of adherence and side effects over several weeks is unreliable.
- Information arriving through phone and WhatsApp is unstructured, scattered, and hard to document.
- For minors and dependent adults, the guardian's view is important but is collected informally, if at all.
- Some patients (for example, those with kosher phones) are unreachable by digital tools, so clinicians have no between-visit data for them.

### 2.4 Problem statement

> Psychiatric clinics lack a low-burden, workflow-integrated way to know how patients are doing between visits, especially after medication changes. As a result, deterioration, non-adherence, and side effects are detected late, clinician time is wasted, and clinics cannot demonstrate quality of care.

---

## 3. Customer, buyer roles, and user personas

### 3.1 Customer (paying account)

A **psychiatric clinic**: private practice, group practice, or clinic network.

- **Launch segment (Israel):** small to mid-sized private psychiatric clinics and group practices (about 2 to 20 clinicians), especially those managing medication initiations, discontinuations, and dose changes.
- **Rationale:** shorter sales cycles and a single decision-maker compared with health funds (Clalit, Maccabi, Meuhedet, Leumit) and hospitals **[TO VALIDATE]**.
- **Later segments:** clinics working with health funds under the mental-health reform, hospital outpatient psychiatry, community mental-health services, and health funds as enterprise customers.
- **Community segment:** clinics serving the Haredi community. Whether they are included in the first pilots is decided in discovery **[TO VALIDATE]**.

### 3.2 Buying roles

| Role | Typical person | Cares about | What Trackline must provide |
|---|---|---|---|
| Economic buyer | Clinic owner, medical director, managing partner | ROI, productivity, retention, reputation, quality, liability | ROI model, clinic usage and value report, clear contract and liability terms |
| Champion | Lead psychiatrist interested in measurement-based care | Clinical insight, less wasted visit time | Excellent pre-visit briefing, trends, low clicks |
| Operational owner | Practice manager or head nurse | Easy onboarding, low staff workload | Fast enrollment, automated reminders, overdue tracking |
| Gatekeepers | IT, information security, privacy officer, legal, clinical risk | Security, privacy compliance, data residency, liability | Standard security and privacy package, DPA, audit logs, data residency |

### 3.3 User personas

#### P1. Dr. Noa, psychiatrist (primary daily user)

- Runs 15 to 30 minute medication-management appointments, with a full schedule.
- Wants to know before the visit: is the patient better or worse, taking the medication, and having side effects?
- Will not adopt anything that adds clicks or steps. Distrusts "black-box" AI.
- **Success for Noa:** opens a one-screen briefing in under 1 minute before each visit and pastes it into the EMR.

#### P2. Yossi, psychiatric nurse / nurse practitioner

- Handles follow-up calls after medication changes and triages patient concerns.
- Wants a single list of who needs attention today (safety alerts, overdue check-ins, worsening trends).
- **Success for Yossi:** fewer routine calls; clear, documented alert acknowledgement.

#### P3. Rina, practice manager / clinic admin

- Manages staff accounts, configuration, billing, and vendor relationships.
- Must justify the subscription to the owner.
- **Success for Rina:** setup in under a day; monthly value report she can forward to the owner.

#### P4. Michal, medical secretary / front desk

- Enrolls patients, enters next-appointment dates, chases overdue check-ins, and performs staff-assisted phone check-ins.
- **Success for Michal:** enrolling a patient takes under 2 minutes; phone check-in entry takes under 3 minutes.

#### P5. Daniel, adult patient (end user)

- Recently started an antidepressant. Uses a smartphone, prefers Hebrew.
- Does not want an app, password, or long questionnaire.
- **Success for Daniel:** completes a check-in in under 60 seconds from an SMS link.

#### P6. Shira, 15-year-old adolescent patient in ADHD treatment

- Reports for herself; will only answer honestly if she knows her parents cannot see her answers.
- **Success for Shira:** a simple, age-appropriate check-in with a clear explanation of who sees her answers.

#### P7. Avi, parent / guardian of a minor

- Reports what he observes about his child (focus, sleep, appetite, side effects).
- May be one of two separated parents.
- **Success for Avi:** a clearly labelled "You are reporting about [first name]" check-in on his own link.

#### P8. Mrs. Goldstein, Haredi patient with a kosher phone

- Has no internet browser; SMS may be restricted. Shares a phone with family. Strong concern about discretion.
- **Success for Mrs. Goldstein:** a staff member calls at an agreed time, asks a few questions, and enters the answers. No revealing messages, no contact on Shabbat.

#### P9. Family caregiver of a dependent adult

- Legal guardian, decision supporter, or approved family caregiver of an adult with intellectual disability, dementia, or severe mental illness.
- **Success:** can report observed changes and side effects reliably, with authority recorded.

---

## 4. Product vision and objectives

### 4.1 Vision

A clinician-facing treatment-monitoring platform that makes measurement-based care effortless for psychiatric clinics, starting with the highest-value moment: the weeks after a medication change.

### 4.2 Product objective

> Help psychiatric clinics detect deterioration, non-adherence, and side effects earlier, while reducing the time their clinicians spend collecting and reviewing patient-reported information.

### 4.3 Positioning

- A workflow and measurement-based-care tool sold to psychiatric clinics.
- Not a consumer mental-health app, an AI therapist, or a diagnostic or prescribing tool.

### 4.4 Objectives and key results (MVP / pilot)

| Objective | Key results (within 90 to 120 days of the first pilot going live) |
|---|---|
| O1. Clinics adopt the workflow | ≥3 clinics actively use Trackline (≥1 new episode and ≥1 briefing viewed per clinic per week); time from signature to first enrolled patient ≤7 days |
| O2. Patients provide data | ≥50% of invited reporters complete ≥1 check-in; ≥60% of scheduled check-ins completed across active episodes **[TO VALIDATE]**; median check-in time <60 seconds |
| O3. Clinicians use the output | Pre-visit briefing opened before ≥50% of relevant appointments (see definition below) |
| O4. Buyers see value | ≥2 clinics sign a paid contract after the pilot; decision-makers report time saved or better care |
| O5. Safe operation | Zero unresolved product-related safety incidents; 100% of safety alerts delivered to at least one configured recipient |

**Relevant appointment:** an appointment recorded in Trackline for a patient with an active episode, or an episode closed within the previous 14 days, that has at least one completed check-in since the previous appointment.

**Product-related safety incident:** an event where Trackline behavior (for example, a failed or delayed alert, a missing crisis screen, a misattributed answer, or an accidental disclosure) contributed, or could have contributed, to patient harm. "Unresolved" means investigation or corrective action under CS-07 is not complete.

### 4.5 Value proposition

**For the clinic (buyer):** more productive appointments, earlier detection of problems, less manual follow-up, better retention and reputation, structured outcome data, and a measurable ROI shown in a usage and value report.

**For psychiatrists:** progress, adherence, and side effects visible before the visit; less time collecting data; earlier identification of patients needing follow-up; better documentation.

**For patients and guardians:** report in under 60 seconds, in their own language, raise concerns before the visit, and feel more engaged in treatment.

### 4.6 ROI model (for the sales process) [TO VALIDATE]

The ROI calculator will use clinic-provided inputs. Illustrative example only:

| Input | Example value |
|---|---|
| Clinicians | 5 |
| Monitored-patient appointments per clinician per month | 60 |
| Minutes saved per monitored appointment | 4 |
| Value of clinician hour | ₪400 |
| Nurse/staff follow-up calls avoided per month | 40 calls × 10 minutes |
| Value of staff hour | ₪100 |
| Patients retained per month (drop-out avoided) | 1 |
| Revenue per retained patient per month | ₪600 |

| Output | Calculation | Example result |
|---|---|---|
| Clinician time value | 5 × 60 × 4 min = 1,200 min = 20 h × ₪400 | ₪8,000 / month |
| Staff time value | 400 min ≈ 6.7 h × ₪100 | ≈ ₪670 / month |
| Retention value | 1 × ₪600 | ₪600 / month |
| **Total estimated value** | | **≈ ₪9,270 / month** |
| Example subscription | 5 seats × ₪400 | ₪2,000 / month |
| **Value-to-price ratio** | | **≈ 4.6×** |

All inputs are assumptions to be replaced with clinic data during discovery and measured during the pilot. Clinician time saved is only realized as money if the clinic converts it into additional appointments, shorter waiting lists, or reduced overtime; the sales conversation and the value report must present it as "time value", not guaranteed revenue.

---

## 5. Competitive landscape and differentiation

### 5.1 Competitor categories

| Category | Examples | Strengths | Weaknesses for our target |
|---|---|---|---|
| Measurement-based-care platforms (mostly US) | Greenspace Health, Mirah, Blueprint, Osmind, NeuroFlow **[TO VALIDATE current offerings and Israeli presence]** | Mature products, evidence base, broad measure libraries | US-centric (HIPAA, English, US EMRs), likely no Hebrew/RTL, no Israeli data residency, no community-specific features, often broad and complex |
| General PRO and survey tools | Generic form builders, EMR questionnaires | Cheap, flexible | No clinical workflow, no trends or briefing, no safety workflow, weak privacy posture for psychiatric data |
| Israeli EMR / clinic-management systems | Systems used by target clinics **[TO VALIDATE in discovery]** | Already installed, single system | Basic questionnaires at best; no between-visit monitoring, reminders, or briefing |
| Status quo | Phone calls, WhatsApp, paper forms, "we'll talk at the next visit" | Free, familiar | Unstructured, undocumented, inconsistent, staff-intensive, privacy risk |

### 5.2 Differentiation [TO VALIDATE]

1. **Israel-first:** Hebrew-first RTL, then Arabic, Russian, and English; Israeli privacy compliance and data residency; local crisis resources.
2. **Community-ready:** kosher-phone and filtered-internet access, discreet messaging, Shabbat- and holiday-aware scheduling.
3. **Guardian reporting with confidentiality:** built for child and adolescent psychiatry and dependent adults.
4. **Narrow focus:** medication-change monitoring rather than a broad platform.
5. **Very low burden:** under 60 seconds per check-in, minimal clinician clicks, no EMR integration needed to start.
6. **Briefing built for short appointments:** one screen, source-linked, exportable to any EMR.

### 5.3 Competitive risks

- Well-funded US platforms localizing for Israel.
- EMR vendors adding a "good enough" questionnaire module.
- Clinics deciding WhatsApp plus phone is sufficient.

Mitigations are listed in [section 20.1](#201-risks).

---

## 6. Scope: in scope, out of scope, and future roadmap

### 6.1 MVP objective

Validate whether psychiatric clinics will repeatedly use a simple medication-change monitoring workflow, and whether clinic decision-makers find the value large enough to pay for it after a pilot.

### 6.2 MVP end-to-end flow

1. Clinician or staff enrolls a patient in a **monitoring episode** after a medication initiation, discontinuation, or dose change; selects the reporting mode (patient, guardian/caregiver, or both); and records consent.
2. Staff enters or confirms the next appointment date.
3. Trackline sends each reporter a secure link by SMS (optionally WhatsApp or email **[TO VALIDATE WhatsApp Business API feasibility and compliance]**). Reporters without a smartphone or internet are checked in by staff phone call.
4. The reporter verifies identity (one-time code or date of birth) and completes a short check-in on a schedule (for example, twice weekly for 4 to 6 weeks).
5. Trends, adherence, side effects, and comments appear on the clinician dashboard.
6. Before the next appointment, Trackline generates a concise pre-visit briefing.
7. If a safety concern is reported, the reporter immediately sees crisis resources and emergency instructions, and the clinic's alert workflow is triggered.
8. The clinician marks the episode as reviewed, extended, or closed.

### 6.3 In scope for MVP

| Area | In scope |
|---|---|
| Patient check-in | Mobile web, no account, secure link + identity verification, <60 s, Hebrew RTL, symptom severity, condition-specific measures, adherence, side effects, optional free text, safety screen, configurable reminders, Shabbat/holiday suppression, neutral wording, opt-out, accessibility, adolescent version |
| Alternative channels | Staff-assisted phone check-in; in-clinic tablet or paper entered by staff |
| Guardian check-in | Required in MVP **if** the first condition includes ADHD or child and adolescent psychiatry; otherwise data model only, release in Phase 2 **[TO VALIDATE]** |
| Clinician dashboard | Patient list with status, timeline, trend indicators, side-effect summary, free text, reporter labelling, pre-visit briefing, copy/PDF export, episode review/extend/close, minimal configuration |
| Clinic administration | Multi-tenant clinics, multiple clinicians and locations, RBAC, assignment/reassignment, enrollment, consent, guardian management, reminders, alert routing, audit log, usage and value report, data export, staff 2FA |
| AI | Trend summary, draft briefing, highlight relevant changes, all source-linked and labelled as draft |
| Safety | Safety screen, crisis resources, configurable alert routing, acknowledgement and audit |
| Compliance | Israeli privacy law, data residency, encryption, audit logging, DPA |

### 6.4 Explicitly out of scope for MVP

- Diagnosis or diagnostic suggestions.
- Medication or dose-change recommendations.
- Suicide-risk prediction or automated risk scoring.
- AI-generated clinical advice sent directly to patients.
- Therapy chatbot or open-ended AI counseling.
- Two-way chat or messaging between patient and clinician.
- Full EMR integration (unless a specific paying pilot clinic requires it).
- Appointment scheduling (Trackline only stores the next appointment date).
- Insurance billing or claims processing.
- Native iOS and Android apps.
- Advanced analytics or payer reporting.
- Sharing patient data with rabbis, family members, or any third party from within the product. (Guardians and caregivers only submit their own reports; they never see patient data.)

### 6.5 Future roadmap (post-MVP, demand-driven)

Product phases below describe **what** is built. They are distinct from the delivery **stages** in [section 19](#19-mvp-release-plan-and-phased-roadmap), which describe **when**. Product Phase 2 capabilities are candidates for delivery during Stage 3 (validation).

| Phase | Candidate capabilities |
|---|---|
| Phase 2 (validation) | Guardian reporting (if not in MVP), automated voice (IVR) check-in, Arabic/Russian/English, WhatsApp channel, briefing improvements, additional conditions and measures, filter-service approval for additional providers |
| Phase 3 (scale in Israel) | EMR integrations with the most common Israeli systems, health-fund and hospital enterprise features (SSO, multi-site reporting), Yiddish **[TO VALIDATE]**, Arab-community adaptations (calendar, holidays) |
| Phase 4 (international) | GDPR/UK and/or HIPAA-ready deployments, local crisis resources, local measure translations, local pricing, regional data residency |
| Later (requires regulatory review) | Advanced analytics, payer reporting; any risk-prediction feature only after medical-device classification review |

---

## 7. User stories and acceptance criteria

Priority legend: see "How to read this document" at the top.

### 7.1 Psychiatrist

| ID | User story | Priority | Acceptance criteria |
|---|---|---|---|
| US-C1 | As a psychiatrist, I want a pre-visit briefing for each monitored patient so I start the appointment informed. | M | Briefing is available from the patient page and the patient list by 07:00 on the appointment day (clinic time zone), or within 15 minutes if the appointment date is entered later than that; with the default template and up to 12 check-ins per reporter it fits on one screen at 1366×768 without scrolling; shows period covered, symptom trend, adherence %, new/persistent side effects, safety events, free-text comments, and data completeness; if no check-ins were completed, it states "No patient-reported data for this period"; every AI statement links to its source data. |
| US-C2 | As a psychiatrist, I want to see symptom trend, adherence, and side effects over time so I can judge treatment response. | M | Timeline shows each check-in with date, reporter, and channel; symptom scores plotted; trend labelled worsening / improving / stable / insufficient data per defined rules ([section 10.4](#104-trend-indicator-rules)); patient and guardian series are shown separately. |
| US-C3 | As a psychiatrist, I want to copy or export the briefing so I can add it to my EMR without an integration. | M | "Copy" places plain-text, RTL-correct briefing on the clipboard; "PDF" downloads a branded PDF with patient identifier, period, and generation timestamp; export action is audit-logged. |
| US-C4 | As a psychiatrist, I want to mark an episode reviewed, extended, or closed so my list stays manageable. | M | Actions available on patient page; "extend" requires a new end date; "close" stops reminders within 5 minutes; all actions audit-logged with user and timestamp. |
| US-C5 | As a psychiatrist, I want to edit the AI draft briefing before saving it. | M | Draft clearly labelled "AI draft – for clinician review"; clinician can edit or discard; saved version records editor and time; original draft retained in audit trail. |
| US-C6 | As a psychiatrist, I want to see who reported each data point so I can interpret it correctly. | M | Every data point displays reporter type (patient / guardian with relationship / staff-entered) and channel (web / phone / in-clinic). |
| US-C7 | As a psychiatrist, I want the dashboard to work if the AI service is down. | M | With AI unavailable, charts, raw answers, and a non-AI structured briefing remain available; a banner indicates AI summary is unavailable. |
| US-C8 | As a psychiatrist, I want to mark new flagged data as reviewed so the "needs review" list only shows what I have not yet seen. | M | "Mark reviewed" action on the patient page clears the review flag for all data up to that moment; new flagged data re-raises it; action audit-logged. |

### 7.2 Nurse / clinical staff

| ID | User story | Priority | Acceptance criteria |
|---|---|---|---|
| US-N1 | As a nurse, I want a list of patients needing attention so I can prioritize follow-up. | M | Patient list filterable by status: safety alert, needs review, overdue, active, completed; safety alerts sorted first. |
| US-N2 | As a nurse, I want to receive and acknowledge safety alerts so they are handled and documented. | M | Notifications dispatched through configured channels within 2 minutes of the safety answer being saved (SA-01); acknowledgement records user, time, and optional note; closure records outcome; unacknowledged alerts escalate per clinic rules. |
| US-N3 | As a nurse, I want to record a check-in collected by phone. | M | Staff-entry form mirrors the check-in questions; data labelled "staff-entered by phone" with staff user ID; safety-screen answers trigger the same alert workflow. |

### 7.3 Medical secretary / front desk

| ID | User story | Priority | Acceptance criteria |
|---|---|---|---|
| US-S1 | As a secretary, I want to enroll a patient in under 2 minutes. | M | Enrollment form requires only: name, ID or internal reference, date of birth, phone, preferred language, assigned clinician, episode type, medication change (free text or list), reporting mode, schedule template, next appointment date, consent confirmation; validation prevents duplicate active episodes for the same patient. |
| US-S2 | As a secretary, I want to see overdue check-ins so I can remind patients or call them. | M | "Overdue" list shows reporter, last check-in, and preferred channel; Shabbat/holiday periods do not count toward overdue. |
| US-S3 | As a secretary, I want to update the next appointment date so the briefing is ready in time. | M | Date editable from patient list; briefing generation re-scheduled automatically. |
| US-S4 | As a secretary, I want to resend a check-in link. | S | Resend available per reporter; rate-limited (max 3 per day); logged. |

### 7.4 Clinic admin / practice manager

| ID | User story | Priority | Acceptance criteria |
|---|---|---|---|
| US-A1 | As a clinic admin, I want to create and manage staff accounts and roles. | M | Admin can invite, deactivate, and change role (admin, clinician, nurse, secretary); 2FA enforced on first login; changes audit-logged. |
| US-A2 | As a clinic admin, I want to configure safety-alert routing. | M | Configure recipients, channels (dashboard, SMS, email), working hours, Shabbat/holiday coverage, and escalation; clinic cannot activate patient enrollment until routing is configured. |
| US-A3 | As a clinic admin, I want a monthly usage and value report to justify the subscription. | M | Report shows the metrics in [section 11.4](#114-clinic-usage-and-value-report); downloadable as PDF; available for any past month. |
| US-A4 | As a clinic admin, I want to configure reminder rules and the neutral sender name. | M | Sender name, message template (from approved neutral options), Shabbat/holiday suppression, and quiet hours configurable. |
| US-A5 | As a clinic admin, I want to export all clinic data. | M | Export request produces machine-readable files (CSV/JSON) plus PDFs of briefings within 5 business days; access to export is restricted to admins and logged. |
| US-A6 | As a clinic admin, I want to reassign a patient to another clinician. | M | Reassignment updates access immediately; history preserved; logged. |

### 7.5 Patient

| ID | User story | Priority | Acceptance criteria |
|---|---|---|---|
| US-P1 | As a patient, I want to complete a check-in from a text message without creating an account. | M | Link opens check-in on any modern mobile browser; identity verified by OTP or date of birth; no password. |
| US-P2 | As a patient, I want the check-in to take under a minute. | M | Median completion time <60 s in pilot; ≤10 required questions in the default interim template (full-length measures, if used, are limited to baseline and end-of-episode check-ins, see CI-11). |
| US-P3 | As a patient, I want to use my language. | M (Hebrew) / S (others) | All patient-facing text available in Hebrew (RTL) at launch; language switcher if more than one enabled. |
| US-P4 | As a patient, I want reminders that don't reveal my treatment. | M | Messages contain no words such as "psychiatry", "mental health", or medication names; sender name set by clinic. |
| US-P5 | As a patient, I want to know what to do in an emergency. | M | Safety screen and a persistent "Need urgent help?" link show emergency numbers (MDA 101, Police 100, ERAN 1201 **[TO VALIDATE with clinical lead]**) and state that answers are not monitored in real time. |
| US-P6 | As a patient, I want to stop reminders. | M | Opt-out link in every message and on check-in page, plus SMS reply keyword (e.g., "STOP"/"הסר"); takes effect within 5 minutes; clinic notified on dashboard; opting out of messages does not by itself withdraw consent (see EN-08). |
| US-P7 | As an adolescent, I want to know who can see my answers. | M (if minors in MVP) | Age-appropriate notice on first check-in and accessible at any time, explaining that parents cannot see answers and when the clinic may involve parents for safety. |

### 7.6 Guardian / caregiver

| ID | User story | Priority | Acceptance criteria |
|---|---|---|---|
| US-G1 | As a guardian, I want my own link and check-in about my child or dependent. | M (if minors in MVP) | Separate link per guardian; header "You are reporting about [first name]"; guardian verifies own identity. |
| US-G2 | As a guardian, I want to know what to do if I think the patient is in danger. | M (if minors in MVP) | Guardian safety screen shows emergency instructions and triggers the clinic alert workflow. |
| US-G3 | As a guardian, I should not see the patient's own answers. | M (if minors in MVP) | Guardian views contain no patient answers, scores, or free text. |

---

## 8. Detailed functional requirements

### 8.1 Monitoring episodes (EP)

| ID | Requirement | Priority |
|---|---|---|
| EP-01 | A monitoring episode belongs to one patient, one clinic, and one assigned clinician. | M |
| EP-02 | Episode types: medication initiation, discontinuation, dose change, switch, other (free text). | M |
| EP-03 | Episode records medication name(s) and change description as entered by staff (free text or pick-list). Trackline does not validate or recommend medications. | M |
| EP-04 | Episode has a start date, planned end date (default 6 weeks), and schedule template (default twice weekly). | M |
| EP-05 | Only one active episode per patient at a time in MVP. | M |
| EP-06 | Episode statuses: draft, active, needs review, completed, closed, cancelled (definitions and transitions in 8.1.1). | M |
| EP-07 | Episode automatically becomes "needs review" at planned end date; clinician must review, extend, or close. | M |
| EP-08 | Closing an episode stops all reminders and scheduled calls for that episode. | M |
| EP-09 | A further medication change during an active episode is recorded as a dated change-log entry on the episode and shown as a marker on the timeline; the clinician may instead close the episode and start a new one. Trend baselines are not reset automatically. | M |
| EP-10 | Staff can end an episode for administrative reasons (patient left the clinic, transferred, deceased, enrolled in error) with a mandatory reason; all reminders stop and the reason is audit-logged. | M |

#### 8.1.1 Episode statuses and transitions

| Status | Meaning | Entered when | Next statuses |
|---|---|---|---|
| Draft | Enrollment started but not activated (e.g., consent missing). | Staff saves an incomplete enrollment. | Active, cancelled |
| Active | Check-ins are being scheduled and sent. | Enrollment completed with consent recorded. | Needs review, closed |
| Needs review | Planned end date reached; reminders paused. | Automatically at planned end date (EP-07). | Active (extended), completed, closed |
| Completed | Episode ran to its planned end and the clinician confirmed it. | Clinician closes an episode from "needs review". | — (terminal) |
| Closed | Episode ended early by a clinician or for an administrative reason (EP-10). | Clinician or staff closes an active episode. | — (terminal) |
| Cancelled | Draft never activated, or created in error before any check-in. | Staff cancels a draft. | — (terminal) |

Patient-list labels "Safety alert", "Needs review", and "Overdue" are **display statuses** derived from episode status and data flags; they are defined in [section 10.1](#101-patient-list-home).

### 8.2 Enrollment and consent (EN)

| ID | Requirement | Priority |
|---|---|---|
| EN-01 | Staff can enroll a patient with the minimum data set in US-S1. | M |
| EN-02 | Staff select reporting mode: patient only, guardian/caregiver only, or both. | M |
| EN-03 | Staff select contact channel per reporter: SMS link, WhatsApp link **[TO VALIDATE]**, email link, staff phone call, in-clinic. | M |
| EN-04 | Consent is recorded per reporter: who consented, on whose behalf, basis of authority, date, method (verbal/written/digital), and staff member who recorded it. Optional attachment of signed form. | M |
| EN-05 | For minors and dependent adults, record patient assent where appropriate. | M (if minors in MVP) |
| EN-06 | Patient chooses which phone number and which family member (if any) the clinic may contact; stored and respected by all messaging. | M |
| EN-07 | Patient-facing enrollment notice explains what is collected, who sees it, that it is not monitored in real time, and how to opt out. | M |
| EN-08 | A reporter can withdraw consent (via staff, or via a link in the check-in page). Withdrawal stops all messages and check-ins for that reporter within 5 minutes, is recorded as a new consent version, and notifies the clinic. Data already submitted is retained under the clinic's retention policy unless deletion is legally required **[TO VALIDATE with counsel]**. | M |
| EN-09 | Staff can update a reporter's phone number or channel; changing a phone number invalidates all open check-in links for that reporter and is audit-logged. | M |
| EN-10 | Duplicate detection on enrollment by ID/internal reference and date of birth; staff are warned before creating a second patient record. | M |

### 8.3 Scheduling and reminders (SR)

| ID | Requirement | Priority |
|---|---|---|
| SR-01 | Schedule templates configurable by clinic (frequency, duration, preferred time window). | M |
| SR-02 | No reminders, automated calls, or messages from Friday before sunset until after Shabbat ends, or on Jewish holidays (Yom Tov), using a Hebrew calendar and clinic-local Shabbat times. Configurable per clinic and per patient. | M |
| SR-03 | Check-ins falling on suppressed periods shift to the next allowed slot; reporters are not marked overdue because of suppression. | M |
| SR-04 | Quiet hours configurable (default no messages 21:00–08:00). | M |
| SR-05 | A check-in is **overdue** if not completed within 48 hours of its due time and **expired** when its check-in window closes (default 72 hours, see 9.2); suppressed periods (SR-02, SR-04) are excluded from both counts. Both durations configurable per clinic. | M |
| SR-06 | Each due check-in triggers one initial message and at most one follow-up reminder (default 24 hours later, within allowed hours). Both are configurable; the maximum is never exceeded. | M |
| SR-07 | Message text selected from clinic-approved neutral templates; no clinical terms or medication names. | M |
| SR-08 | Opt-out honored within 5 minutes across all channels. | M |
| SR-09 | Staff phone-call tasks are generated for reporters on the phone channel and appear in a call list. | M |
| SR-10 | Bulk/automated SMS complies with Israeli Communications Law anti-spam provisions (Amendment 40) and opt-out requirements **[TO VALIDATE whether treatment reminders are exempt]**. | M |

### 8.4 Check-in content (CI)

| ID | Requirement | Priority |
|---|---|---|
| CI-01 | Check-in templates are composed of: symptom severity, condition-specific measure, adherence, side-effect checklist, safety screen, optional free text. | M |
| CI-02 | Templates are configurable per condition and per medication class by the clinic, from a library approved by the Trackline clinical lead. | M |
| CI-03 | Validated measures are used only where licensing allows, with validated translations where they exist **[TO VALIDATE per measure]**. | M |
| CI-04 | Adherence question: "took as prescribed", "took partially", "did not take" (with optional reason). | M |
| CI-05 | Side-effect checklist configurable by medication class; includes "other" with free text. Sensitive items (e.g., sexual side effects) are optional, modestly worded, and can be disabled per patient. | M |
| CI-06 | Free-text field: "Anything you want your psychiatrist to know before your next visit?" with notice that messages are not monitored in real time. | M |
| CI-07 | Safety screen is included in every check-in; content approved by clinical lead. | M |
| CI-08 | Adolescent self-report template with simpler wording and validated youth measures where available. | M (if minors in MVP) |
| CI-09 | Guardian template uses observer-based wording and validated parent/caregiver measures where available and licensed. | M (if minors in MVP) |
| CI-10 | Template versions are tracked; each response stores the template version used. | M |
| CI-11 | Templates support a full-length measure at baseline and end of episode, and a brief subset at interim check-ins (e.g., PHQ-9 at baseline/end, PHQ-2 in between) **[TO VALIDATE with clinical lead]**. Interim check-ins must meet the <60 second target. | M |
| CI-12 | Every scale has a defined direction (higher = worse or higher = better) stored in the template, so trend rules and charts are consistent across measures. | M |
| CI-13 | **Baseline** = the first completed check-in for each reporter in an episode (ideally completed at or within 3 days of enrollment). If the first check-in occurs later, the briefing states the baseline date. | M |
| CI-14 | Free text limited to 500 characters per check-in. | S |

### 8.5 Dashboard and briefing (DB)

See [section 10](#10-clinician-dashboard-specification); requirements DB-01 to DB-08 are in [section 10.6](#106-dashboard-requirements-db).

### 8.6 Administration (AD)

See [section 11](#11-clinic-administration-and-usagevalue-report).

### 8.7 AI (AI)

See [section 12](#12-ai-feature-specification-and-guardrails).

### 8.8 Safety alerts (SA)

See [section 13](#13-safety-alert-workflow-specification).

### 8.9 Notifications to staff (NT)

| ID | Requirement | Priority |
|---|---|---|
| NT-01 | Staff notifications for safety alerts by dashboard, SMS, and email per routing configuration. | M |
| NT-02 | Staff notifications contain no patient-identifying clinical content outside the authenticated dashboard (e.g., "New safety alert in Trackline – please log in"). | M |
| NT-03 | Optional daily digest email to clinicians: number of briefings ready, patients needing review. No clinical content. | S |

---

## 9. Patient and guardian/caregiver check-in experience

### 9.1 Design principles

1. **Under 60 seconds** for a typical check-in.
2. **No account, no password, no app.**
3. **Discreet:** nothing in messages, page titles, or sender names reveals psychiatric treatment.
4. **Safe:** crisis instructions always reachable.
5. **Inclusive:** works on low-end phones, filtered internet, images blocked, and by phone through staff.
6. **Honest about limits:** answers are not monitored in real time.

### 9.2 Web check-in flow

| Step | Screen | Details |
|---|---|---|
| 1 | Message | Neutral SMS/WhatsApp/email: "[Clinic sender name]: you have a short form to complete. [link]". Opt-out text included. |
| 2 | Verify | Enter 6-digit OTP sent to the registered number (default), or date of birth (clinic configurable). Max 5 attempts, then the link is locked and staff are notified; staff can unlock or reissue a link. DOB verification is weaker on shared phones, so clinics are warned when enabling it. |
| 3 | Intro (first time only) | Purpose, who sees answers, "not monitored in real time", emergency numbers, opt-out. For adolescents and guardians, tailored confidentiality notice. |
| 4 | Symptom severity | Single overall rating (0–10 or 5-point labelled scale **[TO VALIDATE with clinical lead]**); scale direction defined per CI-12. |
| 5 | Condition-specific items | Short validated measure or subset per template. One question per screen or grouped, depending on template. |
| 6 | Adherence | Three-option question plus optional reason. |
| 7 | Side effects | Checklist with "none" option; severity for selected items (mild/moderate/severe). |
| 8 | Safety screen | Clinician-approved question(s). If positive → the answer is saved immediately, the crisis screen is shown (see 13.3), and the alert is created even if the reporter does not finish the check-in (SA-08). |
| 9 | Free text (optional) | With "not monitored in real time" notice. |
| 10 | Done | Thank-you, next check-in date, emergency link. No clinical feedback or scores shown. |

**Session rules:** links are single-reporter and expire at the end of the check-in window (default 72 hours) or upon completion; partial answers are saved and submitted automatically when the window closes (marked "partial" in the dashboard); page title is neutral (e.g., clinic name + "Form").

### 9.3 Guardian / caregiver experience

- **Header:** "You are reporting about [patient first name]" on every screen.
- **Identity:** guardian verifies with an OTP to their own phone (default) or their own date of birth recorded at enrollment; never with the patient's details.
- **Wording:** observer-based (e.g., "How has [name]'s sleep been?").
- **Safety screen:** worded for an observer, with instructions for what to do if they believe the patient is in danger; triggers the same clinic alert.
- **Confidentiality:** guardians never see patient answers, scores, or free text.
- **Multiple guardians:** each has an independent link and check-in; the clinic chooses which guardian(s) report.

#### 9.3.1 Reporting rules by group [TO VALIDATE with Israeli legal counsel]

| Group | Default reporting mode | Notes |
|---|---|---|
| Children (approx. <12–14) | Guardian only | Age thresholds configurable per country. |
| Adolescents (approx. 14–17) | Patient + guardian | Adolescent confidentiality notice mandatory. |
| Dependent adults | Patient + caregiver, or caregiver only | Relationship and basis of authority recorded (legal guardian, decision supporter, family caregiver approved by patient or clinician). |

#### 9.3.2 Lifecycle events

- At the patient's 18th birthday, or when guardianship ends, the system creates a task for staff to review consent and keep or remove guardian access. Guardian reminders pause until reviewed.
- Guardians can be added, changed, or removed by staff at any time; all changes audit-logged.

### 9.4 Alternative channels

| Channel | Phase | Specification |
|---|---|---|
| Staff-assisted phone check-in | MVP | Staff call list shows due phone check-ins with preferred call times. Staff form mirrors the check-in, read-aloud scripts provided in Hebrew. Response stored as "staff-entered by phone" with staff user ID. Safety answers trigger the alert workflow and show the staff member a protocol to follow during the call. Target entry time <3 minutes. |
| In-clinic tablet or paper | MVP | Kiosk-mode web check-in on a clinic tablet (patient verifies with OTP or DOB), or a printable paper form entered by staff ("staff-entered from paper"). |
| Automated voice (IVR) | Phase 2 | Inbound or outbound call; answers by keypad; Hebrew voice prompts; neutral caller ID; Shabbat/holiday suppression; safety answer → crisis message + alert. **[TO VALIDATE need in MVP for Haredi pilots]** |
| WhatsApp link | MVP optional / Phase 2 | Subject to WhatsApp Business API feasibility, cost, and privacy review **[TO VALIDATE]**. |
| Email link | MVP | Same neutral wording rules. |

The dashboard shows the channel used for every check-in.

### 9.5 Localization

| Requirement | Detail |
|---|---|
| Launch language | Hebrew, full RTL support. |
| Early follow-ups | Arabic (RTL), Russian, English **[TO VALIDATE which are needed in MVP]**. |
| Later | Yiddish **[TO VALIDATE]**. |
| Measures | Use validated translations only; if none exists, mark the item as non-validated in the clinician view. |
| Dates | Gregorian dates, with optional Hebrew calendar date display. |
| Mixed direction | Correct rendering of mixed Hebrew/English/number content (e.g., medication names, dosages). |
| Crisis resources | Configurable per country and language. |

### 9.6 Accessibility

- WCAG 2.1 AA for patient-facing pages (and Israeli accessibility regulations based on IS 5568 **[TO VALIDATE]**).
- Large text option, high contrast, minimum 44×44 px touch targets.
- Screen-reader support (labels, focus order, RTL announcements).
- Plain language; target reading level appropriate for the general population; adolescent version simpler.
- No time limits on answering questions within the session.

### 9.7 Community-specific needs: Haredi patients [TO VALIDATE in discovery]

All options below are configurable per clinic and per patient.

| Need | Requirement |
|---|---|
| Kosher phones (no internet, SMS may be restricted) | Staff-assisted phone check-in in MVP; IVR in Phase 2; in-clinic check-in. |
| Filtered internet (e.g., NetFree, Rimon) | Check-in domain submitted for approval by main filtering services before pilot; pages load fully with images blocked; no ads, third-party widgets, external fonts, analytics trackers, or unfiltered links. |
| Discretion and stigma | Neutral sender name and caller ID; no clinical words in messages; patient-chosen contact number and contact person; no data sharing with rabbis or third parties from the product. |
| Shabbat and holidays | Suppression per SR-02/SR-03; crisis instructions always visible; alert coverage defined by clinic (section 13). |
| Modest content | No images of people in patient screens, neutral icons only; sensitive items optional, modestly worded, approved by clinicians working with the community, and replaceable by an in-person question. |
| Culturally adapted measures | Use where available. |
| Families | Either parent may be the reporting guardian; clinic selects which parent(s) report. |
| Language | Hebrew at launch; English per section 9.5; Yiddish later if validated. |

The same configurable model (channels, language, discretion, calendar) will later be extended to Arab patients (Arabic, Muslim and Christian holidays, local stigma concerns), Russian-speaking patients, and other communities.

---

## 10. Clinician dashboard specification

### 10.1 Patient list (home)

| Element | Specification |
|---|---|
| Default view | "My patients" for clinicians; "All clinic patients" for nurses, secretaries, and admins (per role permissions). |
| Columns | Patient name, assigned clinician, episode type and start date, next appointment, status, last check-in (date + channel), trend indicator, adherence indicator, briefing ready. |
| Statuses | Display statuses (one per patient, highest precedence shown): **Safety alert** (open or acknowledged-but-not-closed alert) → **Needs review** (episode in "needs review" status, or flagged data per 10.4 not yet marked reviewed, US-C8) → **Overdue** (any reporter has an overdue check-in, SR-05) → **Active** → **Completed** (episode completed or closed in the last 30 days). |
| Sort | Safety alerts first, then needs review, then by next appointment date. |
| Filters | Status, clinician, location, appointment date (today / this week), reporting mode. |
| Quick actions | Open briefing, open patient, resend link, log phone check-in, update appointment date. |

### 10.2 Patient page

- **Header:** name, age, assigned clinician, episode details (type, medication change, start/end), reporting mode, reporters with relationship and channel, next appointment.
- **Timeline chart:** symptom scores over time; patient and guardian series in separate, clearly labelled lines/panels (never merged into one score).
- **Adherence strip:** per check-in (as prescribed / partial / missed / no data).
- **Side-effect table:** each side effect with first reported date, latest severity, and trend (new / persistent / resolved).
- **Comments:** free-text entries with reporter, date, and channel.
- **Safety events:** list with acknowledgement status.
- **Data completeness:** completed vs. expected check-ins per reporter.
- **Episode actions:** review, extend, close.

### 10.3 Pre-visit briefing

| Section | Content |
|---|---|
| Header | Patient, clinician, appointment date, period covered, data completeness (e.g., "5 of 6 check-ins completed"). |
| Summary (AI draft or structured fallback) | 3–6 bullet points on key changes. Each bullet links to source check-ins. |
| Symptoms | Baseline vs. latest score, trend indicator, per reporter. |
| Adherence | % as prescribed, partial, missed; reasons given. |
| Side effects | New since last visit, persistent, resolved; severities. |
| Safety | Any safety-screen positives and their acknowledgement. |
| Comments | Verbatim free text (up to the latest 5; link to all). |
| Footer | "Patient-reported data. AI-generated content is a draft for clinician review." Generation timestamp, template versions. |

**Timing:** generated automatically 24 hours before the next appointment and refreshed at 07:00 on the appointment day; if the appointment is entered or moved to less than 24 hours ahead, generated within 15 minutes; if no appointment date exists, generated on demand only. Can be regenerated on demand at any time.

**Export:** copy to clipboard (plain text, RTL-correct) and PDF. Both audit-logged.

### 10.4 Trend indicator rules

Rule-based, deterministic, and visible to clinicians (not AI). Initial rules, to be refined with the clinical lead **[TO VALIDATE]**:

| Indicator | Rule (per reporter, per measure; baseline per CI-13) |
|---|---|
| Insufficient data | Fewer than 2 completed check-ins in the episode. |
| Worsening | Latest score worse than baseline by ≥ the measure's clinically meaningful change threshold, **or** two consecutive deteriorations (each of the two most recent check-ins is worse than the one before it). |
| Improving | Latest score better than baseline by ≥ the threshold, and the Worsening rule is not met. |
| Stable | None of the above. |

Worsening always takes precedence over Improving. Partial check-ins without a score for the measure are ignored for that measure.

Adherence indicator: flag if any "did not take" or ≥2 "partial" in the last 7 days. Side-effect indicator: flag any new side effect or any rated severe. Any flag sets the patient's display status to "Needs review" until marked reviewed (US-C8).

### 10.5 Configuration (minimal)

Clinicians can change, per episode: check-in frequency, end date, template, and reporting mode (with consent update).

### 10.6 Dashboard requirements (DB)

| ID | Requirement | Priority |
|---|---|---|
| DB-01 | Patient list per 10.1, with display-status precedence and sorting as defined. | M |
| DB-02 | Patient page per 10.2; patient and guardian/caregiver series are never merged into one score. | M |
| DB-03 | Pre-visit briefing per 10.3, with deterministic structured fallback when AI is unavailable (AG-07). | M |
| DB-04 | Trend, adherence, and side-effect indicators computed by the deterministic rules in 10.4; rule definitions viewable from an info icon. | M |
| DB-05 | "Mark reviewed" action clears review flags up to that moment (US-C8). | M |
| DB-06 | Staff can correct a staff-entered response (phone/paper) with a mandatory reason; the correction is stored as a new version, the original is retained, and both are audit-logged. Reporter-submitted web responses cannot be edited. | M |
| DB-07 | Partial check-ins are shown and labelled "partial"; completeness counts only fully completed check-ins. | M |
| DB-08 | Copy and PDF exports carry the label "Patient-reported data" and separate patient-reported data from clinician notes (CS-06). | M |

---

## 11. Clinic administration and usage/value report

### 11.1 Tenant structure

- Each clinic is a separate, logically isolated tenant; no cross-tenant data access.
- A clinic may have multiple locations; patients and staff can be associated with locations.

### 11.2 Roles and permissions (MVP)

| Capability | Clinic admin | Clinician | Nurse | Secretary |
|---|---|---|---|---|
| Manage staff accounts and roles | ✓ | | | |
| Configure alert routing, reminders, sender name | ✓ | | | |
| View usage and value report | ✓ | Own data | | |
| Billing and data export | ✓ | | | |
| Enroll patients, manage reporters and consent | ✓ | ✓ | ✓ | ✓ |
| Update appointment date, resend links | ✓ | ✓ | ✓ | ✓ |
| Log staff-assisted check-ins | | ✓ | ✓ | ✓ (enter only; cannot view after submission) |
| View clinical data (answers, trends, comments) | Configurable **[TO VALIDATE]** | Assigned patients (or all, configurable) | ✓ | Status only (no answers) |
| View/edit briefing | | ✓ | View | |
| Receive and acknowledge safety alerts | Per routing | Per routing | Per routing | Per routing (acknowledge and escalate only; sees that an alert exists and the reporter's contact details, not the answers) |
| Record alert outcome and close alert | | ✓ | ✓ | |
| Review / extend / close episode | | ✓ | ✓ (configurable) | |

**Multiple roles:** a staff user may hold more than one role (for example, a clinic-owner psychiatrist who is both clinician and clinic admin); permissions are the union of their roles.

**Vendor access:** Trackline personnel have no standing access to clinic patient data. Support access requires a time-limited (default 24 hours) grant approved by a clinic admin, is scoped to the request, and is fully audit-logged and visible to the clinic.

### 11.3 Administration functions

| ID | Requirement | Priority |
|---|---|---|
| AD-01 | Invite, deactivate, and change role of staff; enforce 2FA (TOTP or SMS) for all staff. | M |
| AD-02 | Assign and reassign patients to clinicians. | M |
| AD-03 | Manage patients, demographics, episodes, reporters, and consent records. | M |
| AD-04 | Add, change, or remove guardians/caregivers; prompts at age 18 or guardianship change. | M |
| AD-05 | Configure reminder rules, neutral sender name, message templates, quiet hours, Shabbat/holiday suppression and location (for Shabbat times). | M |
| AD-06 | Configure safety-alert routing (section 13.2). | M |
| AD-07 | View audit log (filter by user, patient, action, date). | M |
| AD-08 | Request full data export; export on contract termination. | M |
| AD-09 | Configure check-in templates from the approved library. | M |
| AD-10 | Manage locations. | S |
| AD-11 | On contract termination: full export delivered (AD-08), then all clinic data deleted from production within 30 days and from backups within 90 days, with a deletion certificate **[TO VALIDATE against retention law]**. | M |
| AD-12 | Approve, view, and revoke vendor support access grants (section 11.2). | M |

### 11.4 Clinic usage and value report

Monthly, downloadable as PDF, available for any past month. Purpose: let the economic buyer justify renewal.

| Section | Metrics |
|---|---|
| Usage | Active clinicians; patients enrolled (new and active); episodes by type; check-ins sent and completed; completion rate; check-ins by channel. |
| Clinical workflow | Briefings generated; briefings viewed before appointment (% of relevant appointments, as defined in 4.4); median time from check-in to clinician view. |
| Safety | Safety alerts raised; % acknowledged within the clinic's target time; median acknowledgement time. |
| Patient engagement | % of reporters completing ≥1 check-in; % of episodes with ≥3 check-ins; opt-outs. |
| Estimated value | Estimated clinician minutes saved (briefings viewed × clinic-configured minutes per briefing); estimated staff follow-up calls replaced (configurable assumption). Clearly labelled as estimates. |

No patient-identifiable data appears in the value report.

---

## 12. AI feature specification and guardrails

### 12.1 Allowed AI functions

| ID | Function | Description |
|---|---|---|
| AI-01 | Trend summary | Plain-language summary of patient-reported trends over the episode. |
| AI-02 | Draft pre-visit briefing | 3–6 bullets summarizing key changes, for clinician review. |
| AI-03 | Highlight changes | Identify potentially clinically relevant changes (new side effects, worsening symptoms, adherence drops, notable free-text themes). |

### 12.2 Prohibited AI functions

- Diagnosis or diagnostic suggestions.
- Medication or dose recommendations.
- Suicide-risk prediction or risk scoring.
- Therapy, counseling, or any patient-facing AI conversation.
- Any AI-generated content sent to patients or guardians.
- Autonomous clinical decisions or automatic actions (AI never triggers or suppresses safety alerts; alerts are rule-based).

### 12.3 Guardrails

| ID | Guardrail |
|---|---|
| AG-01 | All AI output is labelled "AI draft – for clinician review". |
| AG-02 | Every AI statement links to the specific source check-ins/answers; statements without a source are rejected and not displayed. |
| AG-03 | AI input is limited to structured check-in data and free text for the episode; no external data. |
| AG-04 | Output validation blocks content containing diagnostic labels, medication/dose recommendations, or risk predictions (keyword and classifier filters plus prompt constraints). |
| AG-05 | Clinicians can edit or discard drafts; edits are stored with attribution. |
| AG-06 | Patient and guardian data are summarized separately and attributed; never merged. |
| AG-07 | If AI is unavailable or fails validation, the deterministic structured briefing (section 10.3) is shown. |
| AG-08 | AI vendors meet the same privacy and data-residency requirements as the product; contracts prohibit use of clinic data for model training; zero data retention where available. |
| AG-09 | Prompts, model versions, inputs (by reference), and outputs are logged for audit and quality review. |
| AG-10 | Clinicians can report an inaccurate summary with one click; reports are reviewed by the clinical lead. |
| AG-11 | Direct identifiers (name, national ID, phone, email, address) are removed or pseudonymized before data is sent to the AI service; free text is scanned and identifiers masked where feasible. |
| AG-12 | AI drafts are generated in the language of the clinician's interface (Hebrew at launch); verbatim free text is quoted in its original language. |

### 12.4 AI quality evaluation

- Before pilot: evaluate on a synthetic test set reviewed by the clinical lead for factual accuracy (target: 0 unsupported statements, ≥95% statements judged accurate and relevant) **[TO VALIDATE thresholds]**.
- During pilot: track inaccuracy reports, edit rate, and clinician usefulness rating.

---

## 13. Safety-alert workflow specification

> Trackline is **not an emergency service** and is **not monitored 24/7**. This is stated to patients and guardians at enrollment, on every safety screen, and in the customer contract.

### 13.1 Triggers

- A positive answer on the safety screen by a patient, guardian, or in a staff-entered check-in.
- (Configurable, non-urgent) Free text containing predefined crisis keywords creates a "review" flag, **not** an urgent alert, and does not replace the safety screen **[TO VALIDATE with clinical lead]**.

Triggers are rule-based only; no AI prediction.

### 13.2 Clinic configuration (required before enrolling patients)

| Setting | Description |
|---|---|
| Primary recipients | Named staff users who receive alerts during working hours. |
| Channels | Dashboard (always), SMS, email. |
| Working hours | Days and hours when the clinic responds. |
| Target acknowledgement time | E.g., within 2 working hours **[TO VALIDATE per clinic]**. |
| Escalation | If unacknowledged after X minutes, notify secondary recipient(s). |
| Out-of-hours handling | Option A: alert queued for next working period, with patient told so. Option B: on-call clinician receives alerts. |
| Shabbat/holiday coverage | Named non-observant or on-call staff, or queue until after Shabbat/holiday. Patient-facing crisis instructions remain visible at all times. |
| Patient-facing response-time message | Text shown on safety screens, derived from the above. |

The clinic admin must confirm the configuration and accept the responsibility statement before enrollment is enabled.

### 13.3 Patient/guardian experience on a positive safety screen

1. Immediately show the crisis screen: "If you are in danger now, call MDA 101 or Police 100. For emotional support, call ERAN 1201." **[TO VALIDATE with clinical lead]** One-tap call links.
2. State clearly: "Your clinic will see this answer during [clinic response-time message]. This form is not monitored in real time."
3. Allow the reporter to continue or exit the check-in; answers already given are saved.
4. For guardians: instructions for what to do if they believe the patient is in danger.

### 13.4 Staff workflow

```text
Safety answer submitted
  → Alert created (status: open) and logged
  → Notifications sent per routing (≤2 minutes)
  → Patient flagged "Safety alert" at top of patient list
  → Staff opens alert → sees reporter, channel, and time; users permitted to view clinical data (section 11.2) also see the triggering answers
  → Staff acknowledges (status: acknowledged) + optional note
  → Staff records outcome (contacted patient / referred to emergency / no action needed / other) and closes (status: closed)
  → If not acknowledged within target → escalation per configuration
```

### 13.5 Requirements

| ID | Requirement | Priority |
|---|---|---|
| SA-01 | Alerts are created within 30 seconds of the safety answer being saved and notifications dispatched within 2 minutes. | M |
| SA-02 | Alert lifecycle: open → acknowledged → closed; each transition logged with user and time. | M |
| SA-03 | Escalation to secondary recipients when unacknowledged after the configured time. | M |
| SA-04 | Notification delivery failures are retried and surfaced to the clinic admin. | M |
| SA-05 | Staff notifications contain no clinical content (NT-02). | M |
| SA-06 | Alert acknowledgement times feed the value report and pilot metrics. | M |
| SA-07 | Contract defines clinic vs. vendor responsibility: clinic owns clinical response; vendor owns system availability, alert delivery, and incident reporting. | M |
| SA-08 | A positive safety answer is persisted and triggers an alert at the moment it is answered, independent of whether the reporter completes or submits the rest of the check-in. | M |
| SA-09 | If an alert remains unacknowledged after the final escalation level, it stays pinned at the top of the patient list, recipients are re-notified at the start of each working period, and the clinic admin is notified. | M |
| SA-10 | Multiple positive safety answers for the same patient while an alert is open are attached to the existing alert (with a new notification) rather than creating duplicate alerts. | S |
| SA-11 | End-to-end alert delivery is tested automatically at least daily in production using a synthetic test tenant (NF-06). | M |

---

## 14. Data model outline

### 14.1 Entities

| Entity | Key attributes | Notes |
|---|---|---|
| **Clinic** (tenant) | id, name, country, language defaults, time zone, Shabbat location, subscription plan, data region | Root of isolation; every record carries clinic_id. |
| **Location** | id, clinic_id, name, address | Optional in MVP. |
| **StaffUser** | id, clinic_id, name, email, phone, role, 2FA settings, status | Roles: admin, clinician, nurse, secretary. |
| **Patient** | id, clinic_id, name, date of birth, national ID or internal ref (encrypted), preferred language, contact preferences, assigned_clinician_id, location_id | Contact preferences include allowed number and allowed contact person. |
| **Reporter** | id, clinic_id, patient_id, type (patient / guardian / caregiver), relationship, basis of authority, name, contact details, verification method (OTP / DOB), date of birth (if DOB verification), channel, language, status | Patient themselves is also a Reporter record. |
| **ConsentRecord** | id, reporter_id, patient_id, consenter, on_behalf_of, authority basis, assent flag, method, date, recorded_by, attachment_ref, version | Versioned; reviewed at age 18/guardianship change. |
| **MonitoringEpisode** | id, clinic_id, patient_id, clinician_id, type, medication change description, change log (EP-09), start/end dates, schedule template, status, end reason, reporting mode | One active per patient in MVP. |
| **Appointment** | id, episode_id, date/time | Next appointment date only; not a scheduler. |
| **CheckInTemplate** | id, version, condition, audience (adult / adolescent / guardian), items, languages, licence info | Approved library managed by vendor clinical lead. |
| **ScheduledCheckIn** | id, episode_id, reporter_id, due_at, window, status (scheduled / sent / completed / partial / overdue / expired / skipped / suppressed) | Adjusted for Shabbat/holidays. |
| **CheckInResponse** | id, scheduled_checkin_id, reporter_id, template_version, channel (web / phone-staff / in-clinic / paper / IVR), entered_by (null or staff_id), submitted_at, completeness (complete / partial), answers, computed scores, version, correction_reason | Immutable after submission; staff corrections create a new version (DB-06). |
| **Message** | id, reporter_id, channel, template, sent_at, delivery status | No clinical content stored in message text. |
| **SafetyAlert** | id, response_id, status, created_at, acknowledged_by/at, outcome, closed_by/at, escalations | |
| **Briefing** | id, episode_id, appointment_id, structured content, AI draft, clinician edited version, generated_at, model version, source links | Draft and final versions retained. |
| **AuditLogEntry** | id, clinic_id, actor (user / system / reporter), action, entity, entity_id, timestamp, IP/device | Append-only. |
| **AlertRoutingConfig** | clinic_id, recipients, channels, hours, escalation, Shabbat/holiday coverage, patient message | Required before enrollment. |
| **UsageMetricSnapshot** | clinic_id, month, metrics | Feeds the value report. |
| **StaffTask** | id, clinic_id, patient_id, reporter_id, type (phone check-in / consent review at 18 / locked link / opt-out follow-up), due_at, assignee, status | Drives the call list and work queues. |
| **ReviewFlag** | id, episode_id, reporter_id, type (trend / adherence / side effect / keyword), source_response_id, raised_at, reviewed_by/at | Drives "Needs review" display status. |
| **SupportAccessGrant** | id, clinic_id, vendor_user, scope, approved_by, starts_at, expires_at, revoked_at | Vendor access control (section 11.2). |
| **AIFeedback** | id, briefing_id, staff_user_id, type (inaccurate / not useful / other), note, created_at, reviewed_by | Feeds AI quality review (AG-10). |

### 14.2 Key relationships

```text
Clinic 1─* Location
Clinic 1─* StaffUser
Clinic 1─* Patient
Patient 1─* Reporter            (patient self + 0..n guardians/caregivers)
Reporter 1─* ConsentRecord
Patient 1─* MonitoringEpisode   (max 1 active in MVP)
MonitoringEpisode 1─* ScheduledCheckIn *─1 Reporter
ScheduledCheckIn 1─0..1 CheckInResponse
CheckInResponse 1─0..1 SafetyAlert
MonitoringEpisode 1─* Appointment 1─0..1 Briefing
StaffUser 1─* Patient           (assigned clinician)
Patient 1─* StaffTask
MonitoringEpisode 1─* ReviewFlag
Briefing 1─* AIFeedback
Clinic 1─* SupportAccessGrant
```

### 14.3 Data model principles

- **Tenant isolation:** clinic_id on every row, enforced at the data-access layer and verified by automated tests.
- **Reporter attribution:** every response linked to exactly one reporter, never merged.
- **Immutability:** responses, consent versions, and audit logs are append-only.
- **Guardian access ≠ data access:** guardians have no access to any patient data.
- **Configurable per country:** age thresholds, consent rules, crisis resources, calendars.

---

## 15. Privacy, security, clinical safety, and compliance

### 15.1 Clinical safety

| ID | Requirement |
|---|---|
| CS-01 | Named clinical lead (psychiatrist adviser or medical director) responsible for clinical content and safety review. |
| CS-02 | All patient-facing safety language and check-in templates approved by the clinical lead before release; changes version-controlled. |
| CS-03 | Emergency instructions and local crisis resources (Israel: MDA 101, Police 100, ERAN 1201 **[TO VALIDATE]**) on every safety screen and via a persistent link. |
| CS-04 | The product must not delay urgent care; "not monitored in real time" messaging everywhere relevant. |
| CS-05 | Clinicians can review and override AI summaries. |
| CS-06 | Clear separation of patient-reported data and clinician assessment in UI and exports. |
| CS-07 | Clinical safety incident process: reporting, investigation, corrective action, and notification to affected clinics. |
| CS-08 | Hazard log maintained from discovery onward **[TO VALIDATE whether a formal clinical-risk standard is required by customers]**. |

### 15.2 Privacy (Israel first) [TO VALIDATE with Israeli privacy counsel]

- Comply with the Protection of Privacy Law and amendments (including Amendment 13), the Privacy Protection (Data Security) Regulations, the Patient Rights Law, the confidentiality provisions of the Treatment of Mentally Ill Persons Law, the Legal Capacity and Guardianship Law (guardians and decision supporters), and Ministry of Health guidance on information security and cloud use for health data.
- Database registration/notification obligations as applicable.
- Clinic is the data controller (database owner); vendor is the processor. DPA signed with each clinic.
- Data residency: Israeli cloud region for Israeli clinics **[TO VALIDATE requirement]**.
- Consent and authorization recorded in the system, including on-behalf consent and assent.
- Data minimization: collect only what the workflow requires.
- Retention: clinic-configurable within legal limits; default retention per Israeli medical-record rules **[TO VALIDATE]**; deletion and export on termination.
- No use of patient data for training third-party AI models without explicit legal and contractual safeguards.
- No data sharing with third parties (including family members or rabbis) from within the product.
- Data-subject requests (access, correction, deletion) are handled by the clinic as controller; Trackline provides the tools to export or correct a single patient's data within 10 business days of a clinic request.
- Free text may contain third-party information (for example, about family members); it is treated with the same protections as clinical data.

### 15.3 Security

| ID | Requirement |
|---|---|
| SE-01 | Encryption in transit (TLS 1.2+) and at rest (AES-256 or equivalent); field-level encryption for national ID numbers. |
| SE-02 | RBAC (section 11.2) and mandatory 2FA for staff. |
| SE-03 | Tenant isolation enforced and tested. |
| SE-04 | Audit logs for all access to patient data, exports, configuration changes, and alert actions; retained per policy; tamper-evident. |
| SE-05 | Secure check-in links: high-entropy, single-reporter, time-limited, rate-limited identity verification. |
| SE-06 | Session timeouts for staff (e.g., 15 minutes idle) **[TO VALIDATE with clinics]**. |
| SE-07 | Vulnerability management, annual penetration test, dependency scanning. |
| SE-08 | Backups encrypted, tested restores, within the same data region. |
| SE-09 | Incident response and breach-notification process aligned with Israeli regulations. |
| SE-10 | Subprocessor list (cloud, SMS, WhatsApp, email, AI) published to clinics; each assessed for residency and security. |
| SE-11 | No third-party analytics or trackers on patient-facing pages. |
| SE-12 | Vendor personnel access to production data only via approved, time-limited support grants (AD-12); all vendor access audit-logged. |

### 15.4 Procurement package

Standard package for gatekeepers: security overview, architecture and data-flow diagram, subprocessor list, DPA template, data-retention policy, incident-response summary, answers to common security questionnaires, and clinical-safety overview.

### 15.5 Clinical content and licensing

- Use validated questionnaires only where licensing allows (e.g., PHQ-9 and GAD-7 are generally free to use; others require a licence) **[TO VALIDATE per measure]**.
- Use validated Hebrew, Arabic, and Russian translations where they exist.
- Maintain a measure register: measure, licence status, translations, audience, approval date.

### 15.6 Regulatory positioning

- Position as a clinical workflow and patient-reported outcome collection tool.
- No claims that Trackline diagnoses, treats, predicts, or prevents disease.
- Obtain regulatory advice on software-as-a-medical-device classification in Israel (Ministry of Health Medical Devices Division, AMAR) and future markets (EU MDR, US FDA, UK MHRA), with particular attention to trend indicators and AI highlights.
- Obtain advice before any clinical claims or expansion into risk prediction.
- Marketing and sales materials reviewed for claim compliance.

### 15.7 Future markets

Architecture must allow adaptation to GDPR (EU/UK), HIPAA (US), and other health-data laws without a rebuild: per-region deployments, configurable retention, consent models, crisis resources, and age thresholds.

---

## 16. Non-functional requirements

| Category | ID | Requirement |
|---|---|---|
| Performance | NF-01 | Patient check-in page first load <2 s on 4G for a mid-range phone; <4 s on 3G. Page weight <300 KB excluding fonts. |
| | NF-02 | Each check-in screen transition <500 ms. |
| | NF-03 | Dashboard patient list loads <2 s for up to 1,000 active patients per clinic. |
| | NF-04 | Briefing view loads <2 s (AI drafts pre-generated). |
| Reliability | NF-05 | Availability ≥99.5% monthly for patient check-in and dashboard (MVP); target 99.9% after MVP. |
| | NF-06 | Safety-alert pipeline monitored with automated alerting to the vendor on-call; failed deliveries retried. |
| | NF-07 | RPO ≤1 hour; RTO ≤4 hours. |
| | NF-08 | Product fully usable when the AI service is unavailable. |
| Mobile web usability | NF-09 | Supports the last 2 major versions of mobile Safari, Chrome, Samsung Internet; works on screens ≥320 px wide. |
| | NF-10 | Works with images blocked and on filtered-internet services; no external CDNs required for core function. |
| | NF-11 | Partial progress saved; resumable within the check-in window. |
| Accessibility | NF-12 | WCAG 2.1 AA on patient-facing pages and staff dashboard; Israeli accessibility requirements **[TO VALIDATE]**. |
| Localization | NF-13 | Full RTL layout for Hebrew and Arabic, including charts, tables, PDFs, and clipboard export. |
| | NF-14 | All strings externalized; adding a language requires no code change. |
| | NF-15 | Locale-aware dates, numbers, and Hebrew calendar support. |
| Scalability | NF-16 | Support 100 clinics, 2,000 staff users, and 50,000 active reporters on the initial architecture without redesign. |
| Security | NF-17 | See section 15.3. |
| Observability | NF-18 | Logs and metrics contain no clinical content; PII masked. |
| Cost | NF-19 | Variable cost per active patient (SMS/WhatsApp, cloud, AI) tracked per clinic to support gross-margin monitoring. |
| Staff dashboard | NF-20 | Supports the last 2 major versions of desktop Chrome, Edge, Safari, and Firefox at ≥1366×768; usable on tablets for in-clinic use. |
| Messaging | NF-21 | SMS/email delivery status tracked per message; delivery rate <95% for a clinic over 24 hours raises a vendor operations alert. |
| Time | NF-22 | All scheduling, overdue, and briefing timing computed in the clinic time zone, correctly handling Israeli daylight-saving transitions. |
| AI performance | NF-23 | AI draft generation completes within 60 seconds; on timeout, the structured briefing is shown (AG-07). |

---

## 17. Pricing, sales model, onboarding, and customer success

### 17.1 Pricing [TO VALIDATE in discovery]

| Element | Proposal |
|---|---|
| Payer | The clinic; never patients. |
| Primary model | Subscription per clinician seat per month, with a clinic minimum. |
| Alternative to test | Per active monitored patient per month. |
| Israeli price range to test | ₪250–₪600 per clinician per month, or clinic packages of ₪1,000–₪3,500 per month by size. |
| Pilot | 90-day **paid** pilot (extendable to 120 days) with success criteria agreed in writing in advance; pilot fee credited toward the first annual contract **[TO VALIDATE]**. |
| Contracts | Annual, billed monthly or annually after the pilot. |
| Unit economics | Price must cover variable costs per patient (messaging, cloud, AI) with target gross margin ≥70% **[TO VALIDATE]**. |

Illustrative packages:

| Package | Clinicians | Monthly price (to test) | Includes |
|---|---|---|---|
| Starter | Up to 3 | ₪1,000–₪1,500 | Core monitoring, SMS, Hebrew, standard support |
| Practice | 4–10 | ₪1,800–₪2,800 | + multiple locations, value report, phone check-in tools |
| Group | 11–20 | ₪2,800–₪3,500+ | + priority support, custom templates |

### 17.2 Sales motion

- Founder-led direct sales to clinic owners and medical directors.
- Champion psychiatrist brings Trackline into the clinic; economic buyer involved from the first meeting.
- Paid pilot with written success criteria; value report used to support conversion and renewal.
- Partnerships later: Israeli EMR/clinic-management vendors, psychiatric associations; pharmaceutical-independent channels only **[TO VALIDATE]**.
- Avoid pharmaceutical sponsorship or conflicted partnerships without legal and ethical review.

### 17.3 Onboarding

| Step | Target |
|---|---|
| Contract and DPA signed | Day 0 |
| Clinic account created, admin invited, 2FA set | Day 1 |
| Alert routing, reminders, sender name, templates configured (with vendor support) | Day 1–3 |
| Clinician training (<30 min) and staff training (<30 min) | Day 2–5 |
| Filtering-service and SMS test with a staff phone | Day 3–5 |
| First patient enrolled | **≤ Day 7** |

### 17.4 Customer success

- Named contact for each pilot clinic.
- Hebrew support during Israeli business hours; defined channel for urgent system issues.
- Support severity levels: **Sev 1** (alert delivery or check-in unavailable) – response ≤1 hour, 24/7 vendor on-call; **Sev 2** (major feature degraded) – response ≤4 business hours; **Sev 3** (minor issue or question) – response ≤2 business days **[TO VALIDATE]**.
- Pilot check-ins at weeks 2, 4, 8, and a final review against success criteria.
- Monthly value report sent to the clinic admin and economic buyer.
- Feature requests logged; build only those requested by multiple paying clinics.

---

## 18. Key metrics and success criteria

### 18.1 Adoption

- Clinics onboarded.
- Active clinicians per clinic.
- Patients enrolled in monitoring episodes.
- % of invited reporters completing ≥1 check-in.
- Median check-in completion time.
- Check-in completion rate at weeks 2, 4, and 6.
- Time from contract signature to first enrolled patient.

### 18.2 Engagement

- % of episodes with ≥3 completed check-ins.
- % of clinicians opening the pre-visit briefing before appointments.
- Briefings viewed per active clinician per week.
- Weekly active clinician rate.
- % of safety alerts acknowledged within the clinic's defined time.

### 18.3 Business

- Paying clinics; MRR; average revenue per clinic.
- Pilot-to-paid conversion rate.
- Sales cycle length.
- CAC and payback period.
- Net revenue retention (including seat expansion).
- Logo churn.
- Gross margin including messaging, cloud, and AI costs per patient.

### 18.4 Outcome proxies

- % of appointments with a completed pre-visit briefing.
- % of medication-change episodes with documented adherence and side-effect data.
- Clinician usefulness rating.
- Clinic-reported time saved.
- Clinic manager satisfaction and likelihood to renew.

### 18.5 Go / no-go criteria (90–120 days after pilot launch)

| Criterion | Threshold |
|---|---|
| Active clinics | ≥3 |
| Reporter activation | ≥50% of invited reporters complete ≥1 check-in |
| Briefing usage | Opened before ≥50% of relevant appointments (definition in 4.4) |
| Conversion | ≥2 clinics sign a paid contract |
| Perceived value | Decision-makers report time saved or improved care without added burden |
| Safety | No unresolved product-related safety incidents (definition in 4.4) |

If criteria are not met: stop feature development, interview users and buyers, and pivot before building more.

### 18.6 Instrumentation

- Product events (link sent, link opened, verification passed/failed, check-in started/completed/partial, briefing generated/viewed/copied/exported, alert created/notified/acknowledged/closed, opt-out) are captured server-side with clinic, role, and timestamp, but **no clinical content**.
- No third-party analytics on patient-facing pages (SE-11); staff-dashboard analytics are self-hosted or within the same data region.
- Every metric in sections 4.4, 11.4, and 18.1–18.5 must be computable from these events before the pilot starts (M3).

---

## 19. MVP release plan and phased roadmap

Delivery is organized in **stages** (when). Product **phases** in [section 6.5](#65-future-roadmap-post-mvp-demand-driven) describe capability sets (what).

### 19.1 Stage 1: Discovery (weeks 1–4)

- Interview 15–25 psychiatrists, nurses, clinic owners/medical directors, practice managers, and secretaries in Israel, including ≥5 economic buyers.
- Include 2–3 clinics serving the Haredi community, plus Haredi patients or family members where allowed.
- Identify the single most painful medication-monitoring workflow and the first target condition(s).
- Decide: minors in MVP (guardian reporting), Haredi clinics in first pilots, IVR in MVP, WhatsApp, MVP languages.
- Map current tools (WhatsApp, phone, EMRs), willingness to pay, approval process, and adoption blockers.
- Recruit 3–5 design-partner clinics for paid pilots.
- Start privacy, regulatory, and measure-licensing legal review; appoint clinical lead.
- Clickable prototype of check-in and briefing tested with users.

**Exit criteria:** target condition chosen, MVP scope decisions recorded in the decision log ([section 20.5](#205-mvp-scope-decision-log)), ≥3 signed pilot letters of intent, clinical lead appointed, legal review underway.

### 19.2 Stage 2: MVP build (weeks 5–12)

| Weeks | Deliverables |
|---|---|
| 5–6 | Tenant, auth/2FA, RBAC, data model, audit log, Israeli cloud region setup; check-in template engine; clinical lead approves templates and safety content. |
| 7–8 | Patient web check-in (Hebrew RTL), SMS/email messaging, Shabbat/holiday scheduling, enrollment and consent, staff phone check-in. |
| 9–10 | Dashboard, patient page, trend rules, structured briefing, copy/PDF export, safety-alert workflow and routing. |
| 11 | AI draft briefing with guardrails and fallback; guardian reporting if in MVP scope; value report. |
| 12 | Security testing, filtering-service approval, accessibility check, pilot onboarding of 3–5 clinics. |

Throughout: agree safety-alert workflow and success criteria with each pilot clinic; manual onboarding support.

**MVP cut line (if the schedule slips):** protect, in order, safety workflow → web and staff-phone check-in → patient page and structured briefing → enrollment/consent → value report. Defer first: AI draft briefing (the structured briefing remains), in-clinic tablet mode, then guardian reporting (only if minors are out of scope).

### 19.3 Stage 3: Validation (weeks 13–29)

- Run pilots for 90 days (extendable to 120); measure completion, clinician usage, alert handling, and satisfaction.
- Improve briefing and workflow based on evidence.
- Add only features requested repeatedly by multiple paying clinics (candidates: IVR, guardian reporting if not in MVP, Arabic/Russian/English, WhatsApp).
- Convert successful pilots to paid annual subscriptions.
- Build repeatable sales, onboarding, and support process.
- Go/no-go review against section 18.5.

### 19.4 Stage 4: Expansion (after validation)

- Scale to more Israeli private clinics; explore health-fund-contracted clinics, hospital outpatient departments, and health funds as enterprise customers (SSO, multi-site reporting, EMR integration).
- Extend community adaptations (Arab, Russian-speaking, Yiddish-speaking patients).
- Select first international market (candidates: UK, EU, US) based on regulatory effort, language, sales access, and willingness to pay **[TO VALIDATE]**.
- Per new country: privacy and medical-device review, local crisis resources, measure translations, local pricing, data residency.

### 19.5 Release milestones

| Milestone | Target | Definition of done |
|---|---|---|
| M1: Prototype validated | End of week 4 | Prototype tested with ≥8 users; scope decisions recorded |
| M2: Internal alpha | Week 10 | End-to-end flow works with test data; safety workflow tested |
| M3: Pilot release | Week 12 | Security, accessibility, and clinical sign-off; instrumentation live (18.6); first pilot clinic live |
| M4: Pilot review | Weeks 25–29 (90–120 days after M3) | Go/no-go decision against section 18.5 |

---

## 20. Risks, assumptions, dependencies, and open questions

### 20.1 Risks

| Risk | Why it matters | Mitigation | Likelihood / impact |
|---|---|---|---|
| Workflow burden | Clinicians and staff abandon tools that add steps. | <60 s check-ins, minimal clinician clicks, one-screen briefing. | High / High |
| Low patient completion | No data, no value. | Short check-ins, sensible reminders, native language, simple mobile web, phone fallback. | Medium / High |
| Wrong person reporting or seeing data | Guardians may lack authority or breach confidentiality. | Recorded authority, separate links and identity checks, no guardian access to patient answers, review at 18. | Medium / High |
| Excluding communities without smartphones | Haredi patients with kosher phones generate no data. | Staff phone check-in (MVP), IVR (next), filter-approved site. | High / Medium |
| Stigma and accidental disclosure | Revealing message on a shared phone could cause harm. | Neutral wording and sender, patient-chosen contact, no third-party sharing. | Medium / High |
| Culturally inappropriate content | Rejection by patients or clinics. | No images of people, modest optional sensitive items, community clinician review. | Medium / Medium |
| Safety incidents | Serious harm and liability. | Clinician-approved protocols, crisis resources, defined alert ownership, human review. | Low / Very high |
| Unclear liability for alerts | Patients may expect 24/7 monitoring. | Clear messaging, clinic-configured routing, contract terms. | Medium / High |
| Privacy and compliance | Highly sensitive, regulated data. | Privacy by design, access control, audit, consent, residency, legal review. | Medium / Very high |
| Clinician distrust of AI | Blocks adoption. | Assistive, source-linked, editable, narrow AI; non-AI fallback. | Medium / Medium |
| Users like it, buyers don't pay | No business. | Economic buyers in discovery, paid pilots, value report. | Medium / High |
| Long sales cycles | Slow growth. | Private clinics first; standard security package. | Medium / Medium |
| EMR integration expectations | Reduced adoption. | Copy/PDF export; integrate only for committed customers. | Medium / Medium |
| Medical-device classification | Could require registration and delay. | Narrow positioning, deterministic rules, early regulatory advice. | Low–Medium / High |
| Small home market | Limits growth. | Localization-ready architecture; international plan after validation. | Medium / Medium |
| Better-funded competitors | Market entry by US platforms. | Local focus, language, compliance, community fit, simplicity. | Medium / Medium |
| MVP scope vs. 8-week build | Scope (multi-channel, guardians, AI, safety, compliance) is large for weeks 5–12; slippage delays pilots. | Early scope decisions (20.5), explicit cut line (19.2), structured briefing before AI. | High / Medium |
| Alert fatigue | Too many flags or alerts cause staff to ignore them. | Deterministic, clinician-tuned thresholds; alert de-duplication (SA-10); monitor alert volume per clinic in pilot. | Medium / High |
| Shared-phone disclosure via verification | Family members on a shared phone could open a link and pass DOB verification. | OTP by default, DOB warning, neutral pages, short link lifetime. | Medium / High |

### 20.2 Assumptions

- Private psychiatric clinics in Israel will pay for a monitoring tool if it saves clinician time and improves care.
- Patients will complete short check-ins from an SMS or WhatsApp link without a dedicated app.
- A standalone tool with copy/PDF export is acceptable to early clinics without EMR integration.
- A clinical lead will be available to approve safety content and measures.
- Hebrew-first is sufficient for the first pilots.
- Clinics can define and staff a safety-alert workflow, including Shabbat/holiday coverage.
- Messaging costs (SMS/WhatsApp) per patient are low enough for target margins.

### 20.3 Dependencies

| Dependency | Needed for | Owner |
|---|---|---|
| Clinical lead appointed | Templates, safety content, trend thresholds, AI evaluation | Founders |
| Israeli privacy and regulatory counsel | Compliance, DPA, SaMD classification, guardian/minor rules | Founders / Legal |
| Measure licences and validated translations | Check-in content | Clinical lead / Legal |
| Israeli cloud region provider | Data residency | Engineering |
| SMS provider (and WhatsApp Business API if used) | Messaging | Engineering |
| Filtering services (NetFree, Rimon, others) approval | Haredi access | Product / Ops |
| AI vendor meeting residency and no-training terms | AI features | Engineering / Legal |
| Hebrew calendar and Shabbat times data source | Scheduling | Engineering |
| 3–5 design-partner clinics | Pilot | Founders |

### 20.4 Open questions

**Clinical scope**

1. Which conditions and medication changes should the first version support (depression, anxiety, ADHD, bipolar disorder, other)?
2. Which validated or pragmatic measures should be used, and are validated translations available?
3. What is the optimal check-in frequency per condition and medication type?
4. What are the clinically meaningful change thresholds for trend indicators?

**Minors, guardians, and consent**

5. Are minors in scope for MVP (depends on ADHD / child and adolescent psychiatry)?
6. At what ages may a minor report alone, consent, or keep answers confidential from parents, in Israel and later markets?
7. How should separated parents, disputed custody, or unclear authority be handled?
8. What proof of guardianship or decision-supporter appointment must clinics keep?

**Access and community**

9. How should patients without smartphones or reliable internet be supported beyond staff phone check-in?
10. Should Haredi-focused clinics be among the first pilots, and is IVR needed in MVP for them?
11. Which kosher phone plans allow SMS, and will NetFree, Rimon, and other filters approve the check-in site?
12. Which items are culturally sensitive for Haredi patients, and do adapted versions exist?
13. Is Yiddish needed, and for what share of patients?
14. Is WhatsApp an acceptable and compliant channel for check-in links in Israel?

**Safety and workflow**

15. What exact safety-alert workflow will each clinic use, including after hours and on Shabbat/holidays?
16. Should free-text crisis keywords generate a review flag?

**Commercial**

17. Which EMR or clinic-management systems do target clinics use, and is integration required to buy?
18. Who signs the contract in each segment, and what is the approval process?
19. What price and pricing model will clinic owners accept without lengthy procurement?
20. What evidence or documentation will clinics need before trusting the product?

**Regulatory and expansion**

21. Does any planned feature require medical-device registration in Israel or future markets?
22. Which country should be the first international market, and when?

### 20.5 MVP scope decision log

Decisions that block MVP build must be closed by the end of Stage 1 (week 4).

| # | Decision | Options | Owner | Decide by | Status |
|---|---|---|---|---|---|
| D1 | First target condition(s) | Depression/anxiety, ADHD, bipolar, other | Product + clinical lead | Week 4 | Open |
| D2 | Minors and guardian reporting in MVP | In MVP / Product Phase 2 | Product + legal | Week 4 | Open |
| D3 | Haredi-focused clinics in first pilots | Yes / later | Product | Week 4 | Open |
| D4 | IVR in MVP | MVP / Product Phase 2 | Product | Week 4 | Open |
| D5 | WhatsApp channel in MVP | MVP / Product Phase 2 | Product + legal | Week 4 | Open |
| D6 | MVP languages beyond Hebrew | None / English / Arabic / Russian | Product | Week 4 | Open |
| D7 | Symptom scale and measures per condition | Per CI-11/CI-12 | Clinical lead | Week 5 | Open |
| D8 | Default safety-screen wording and frequency | Every check-in / reduced | Clinical lead | Week 5 | Open |
| D9 | Israeli cloud region and AI vendor | Shortlist TBD | Engineering + legal | Week 5 | Open |

---

## Appendix A: Glossary

| Term | Definition |
|---|---|
| Monitoring episode | A defined period (e.g., 6 weeks) of between-visit check-ins following a medication change. |
| Reporter | A person who completes check-ins: the patient, a guardian, or a caregiver. |
| Check-in | A short questionnaire on symptoms, adherence, side effects, safety, and optional comments. |
| Pre-visit briefing | A one-screen summary of check-in data prepared before an appointment. |
| Baseline | The first completed check-in for each reporter in an episode (CI-13). |
| Overdue / expired | A check-in not completed 48 hours / 72 hours after its due time, excluding suppressed periods (SR-05). |
| Safety screen | Clinician-approved question(s) in every check-in that identify immediate safety concerns. |
| Safety alert | A rule-based alert created by a positive safety-screen answer and routed to clinic staff (section 13). |
| Relevant appointment | Appointment of a patient with an active or recently closed episode and ≥1 check-in since the previous appointment (section 4.4). |
| Guardian | A parent or legal guardian reporting about a minor or a dependent adult. |
| Caregiver / decision supporter | An approved family caregiver, or a person appointed under the Legal Capacity and Guardianship Law to support an adult's decisions. |
| OTP | One-time password (verification code) sent by SMS. |
| EMR | Electronic medical record. |
| Haredi | Ultra-Orthodox Jewish community. |
| Shabbat / Yom Tov suppression | No automated messages or calls from before sunset Friday (or holiday eve) until the end of Shabbat or the holiday (SR-02). |
| MDA / ERAN | Magen David Adom (emergency medical service, 101) / ERAN emotional first-aid hotline (1201). |
| RPO / RTO | Recovery point objective / recovery time objective. |
| Measurement-based care (MBC) | Routine use of patient-reported outcome measures to guide treatment. |
| PRO | Patient-reported outcome. |
| Kosher phone | A mobile phone without internet/browser access, used in parts of the Haredi community. |
| Filtered internet | Internet access through content-filtering services such as NetFree or Rimon. |
| IVR | Interactive voice response: automated phone calls answered by keypad. |
| SaMD | Software as a medical device. |
| AMAR | Israeli Ministry of Health Medical Devices Division. |
| DPA | Data processing agreement. |
| RBAC | Role-based access control. |
| 2FA | Two-factor authentication. |

## Appendix B: Requirement ID prefixes

| Prefix | Area |
|---|---|
| US-C / US-N / US-S / US-A / US-P / US-G | User stories: clinician, nurse, secretary, admin, patient, guardian |
| EP | Monitoring episodes |
| EN | Enrollment and consent |
| SR | Scheduling and reminders |
| CI | Check-in content |
| DB | Dashboard and briefing |
| NT | Staff notifications |
| AD | Administration |
| AI / AG | AI functions / AI guardrails |
| SA | Safety alerts |
| CS | Clinical safety |
| SE | Security |
| NF | Non-functional requirements |
| D | MVP scope decisions (section 20.5) |
