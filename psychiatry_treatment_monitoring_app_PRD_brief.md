# PRD Brief: Trackline — Treatment Monitoring for Psychiatric Clinics

## Instructions for Claude

You are a senior product manager and healthcare product strategist. Use the brief below to create a complete, professional Product Requirements Document (PRD) for a **B2B treatment-monitoring SaaS product sold to psychiatric clinics** and used by psychiatrists and their clinical teams.

The paying customer is the **clinic** (practice, group, or institution), not the individual patient. Patients use the product for free as part of their care at the clinic.

Do not design a consumer self-help app, AI therapist, diagnosis tool, or medication-recommendation engine. The product must support psychiatrists and their clinical teams by collecting structured patient-reported information and presenting it as a concise pre-visit briefing.

Write the PRD in clear business language, with enough product detail for a designer or developer to begin discovery and prototyping. Include assumptions, open questions, risks, and a phased MVP scope. Items marked **[TO VALIDATE]** are hypotheses, not facts; treat them as such.

---

## 1. Product vision

Build a clinician-facing treatment-monitoring platform for psychiatric clinics.

The product helps psychiatrists detect symptom worsening, medication non-adherence, and side effects earlier by collecting brief patient-reported check-ins between visits and turning them into an actionable pre-visit summary.

**One-sentence product objective:**

> Help psychiatric clinics detect deterioration, non-adherence, and side effects earlier, while reducing the time their clinicians spend collecting and reviewing patient-reported information.

**Positioning:**

- Not a consumer mental-health app.
- Not an AI therapist.
- Not a diagnostic or prescribing tool.
- A workflow and measurement-based-care tool sold to psychiatric clinics.

**Working product name:** Trackline.

## 2. Problem statement

Psychiatric clinics often lack an efficient way to understand how patients are doing between appointments. Clinicians may learn about worsening symptoms, missed medication, or side effects only at the next visit, or after a crisis.

Existing measurement-based-care approaches can improve outcomes, but they are difficult to implement because they add administrative work, require patients to complete lengthy forms, and are often poorly integrated with clinical workflows and electronic medical records (EMRs).

**The clinic-level problem (why the clinic pays):**

- Clinicians lose appointment time re-collecting information that could have been gathered beforehand.
- Deterioration between visits leads to avoidable urgent contacts, crisis visits, and patient drop-out.
- Clinic managers have no structured data on treatment outcomes, patient engagement, or quality of care to show patients, payers, or partners.
- Manual follow-up calls after medication changes consume nursing and staff time and are inconsistent.

## 3. Customer, buyers, and users

The product has a **B2B buying model**. The people who pay, the people who approve, and the people who use it are different. The PRD must address each.

### 3.1 Customer (the paying account)

The customer is a **psychiatric clinic**: a private practice, group practice, or clinic network. Later segments may include clinics contracted with health funds (HMOs), hospital outpatient departments, and community mental-health services.

### 3.2 Buying roles inside the clinic

| Role | Typical person | What they care about |
|---|---|---|
| Economic buyer (signs the contract) | Clinic owner, medical director, or managing partner | ROI, clinician productivity, patient retention, reputation, quality of care, liability |
| Champion | A lead psychiatrist who wants measurement-based care | Better clinical insight, less time wasted in visits |
| Operational owner | Practice manager or head nurse | Easy onboarding, low staff workload, clear enrollment and reminder process |
| Gatekeepers / potential blockers | IT, information security, privacy officer, legal, clinical risk | Data security, privacy law compliance, data residency, liability, contracts |

### 3.3 Users

- **Psychiatrists** (primary daily users): review dashboards and pre-visit briefings. Have limited time, will not adopt a tool that adds workflow burden, and must retain full clinical judgment and accountability.
- **Psychiatric nurses, nurse practitioners, and physician assistants**: review alerts, follow up with patients, manage episodes.
- **Practice managers / administrators**: manage clinician accounts, configuration, billing, and usage reports.
- **Medical secretaries / front-desk staff**: enroll patients, manage reminders, track overdue check-ins.
- **Patients** (end users, not customers): complete brief check-ins.
- **Guardians and caregivers** (end users, not customers): report on behalf of, or in addition to, patients who cannot fully report alone. This includes parents of **minors** (for example, children and adolescents in ADHD treatment) and legal guardians, decision supporters, or family caregivers of **dependent adults** (for example, intellectual disability, dementia, or severe mental illness). See section 6.1.

### 3.4 Initial target market

- **Launch country: Israel.**
- **Initial segment:** small to mid-sized private psychiatric clinics and group practices (approximately 2 to 20 clinicians), especially those treating patients who are starting, stopping, or changing psychiatric medications.
- **Why private clinics first:** shorter sales cycles and a single decision-maker, compared with health funds (Clalit, Maccabi, Meuhedet, Leumit) and hospitals, which have long procurement processes **[TO VALIDATE]**.
- **Later segments in Israel:** clinics working with health funds under the mental-health reform, hospital outpatient psychiatry, and the health funds themselves as enterprise customers.
- **Community segment:** clinics serving the ultra-Orthodox (Haredi) community, which need low-tech channels, discretion, and Shabbat-aware scheduling (section 6.2). Decide in discovery whether to target them in the first pilots **[TO VALIDATE]**.
- **International expansion:** after product-market fit in Israel. See section 11.

## 4. Core value proposition

### For the clinic (the buyer)

- More productive appointments: clinicians start each visit already informed.
- Earlier detection of patients who are deteriorating, not taking medication, or having side effects, which can reduce crisis contacts and drop-out.
- Less manual follow-up by nurses and staff after medication changes.
- Better patient retention and experience, which helps a private clinic's reputation and revenue.
- Structured outcome data the clinic can use for quality reporting, internal review, and conversations with health funds or insurers.
- A clear, measurable ROI the clinic manager can see in a simple usage and value report.

### For psychiatrists

- See patient progress, adherence, and side effects before the appointment.
- Reduce time spent collecting and interpreting patient-reported outcomes.
- Identify patients who may need earlier follow-up.
- Improve documentation and measurement-based care with minimal extra work.

### For patients

- Report how they are doing in under 60 seconds, in their own language.
- Communicate concerns before the visit.
- Feel more prepared and engaged in treatment.

### ROI hypothesis to validate with clinics **[TO VALIDATE]**

The PRD should include a simple ROI model the sales process can use, for example:

- Minutes saved per appointment × appointments per clinician per month.
- Reduction in missed appointments and treatment drop-out.
- Reduction in unplanned phone calls and urgent visits after medication changes.
- Nursing or staff hours saved on manual follow-up calls.

## 5. Competitive landscape and differentiation

The PRD must include a short competitive analysis. Categories to cover:

- **Measurement-based-care platforms** (mostly US-focused), for example Greenspace Health, Mirah, Blueprint, Osmind, NeuroFlow. **[TO VALIDATE current offerings and presence in Israel]**
- **General patient-reported outcome and survey tools** (for example, generic form tools or EMR questionnaires).
- **Existing EMR and clinic-management systems** used by Israeli clinics, which may already have basic questionnaire features.
- **Status quo:** phone calls, WhatsApp messages, paper questionnaires, and "we'll talk at the next visit".

Expected differentiation **[TO VALIDATE]**:

- Built for the Israeli market first: Hebrew-first and RTL, with Arabic, Russian, and English; local privacy compliance; local crisis resources.
- Works for communities that generic tools miss, such as Haredi patients: kosher-phone and filtered-internet access, discreet messaging, and Shabbat-aware scheduling.
- Narrow focus on medication-change monitoring rather than a broad, complex platform.
- Very low workload for clinicians and staff.
- Pre-visit briefing designed to fit into a short psychiatric appointment.

## 6. MVP scope

### MVP objective

Validate whether psychiatric clinics will use a simple medication-change monitoring workflow repeatedly, and whether clinic decision-makers find the value large enough to pay for it after a pilot.

### MVP user flow

1. A clinician or staff member enrolls a patient in a monitoring episode after a medication initiation, discontinuation, or dose change, chooses who reports (patient, guardian/caregiver, or both; see section 6.1), and records the required consent.
2. The staff member enters or confirms the patient's next appointment date so the briefing is ready in time.
3. The system sends the patient a secure link by SMS, and optionally by WhatsApp or email **[TO VALIDATE WhatsApp Business API feasibility and compliance]**. For patients without a smartphone or internet (for example, kosher phones), staff collect the check-in by phone instead (see section 6.2).
4. The patient verifies their identity (for example, with a one-time code or date of birth) and completes a short check-in on a defined schedule, such as twice weekly for four to six weeks.
5. The system displays symptom trends, adherence, side effects, and patient comments in a clinician dashboard.
6. Before the next appointment, the system generates a concise pre-visit briefing for the clinician.
7. If the patient reports an acute safety concern, the app immediately shows crisis resources and emergency instructions, and triggers the clinic's configured alert workflow (see section 8).
8. The clinician marks the episode as reviewed, extends it, or closes it.

### MVP features

#### Patient check-in

- Secure, mobile-friendly web check-in; a native mobile app is not required for MVP.
- No patient account or password required; secure link plus lightweight identity verification.
- Check-in completion time target: under 60 seconds.
- Languages: Hebrew (RTL) at launch; Arabic, Russian, and English as early follow-ups **[TO VALIDATE which are needed in MVP]**.
- Symptom severity rating.
- Condition-specific symptom questions using validated measures where licensing allows (see section 8.4).
- Medication adherence question: took as prescribed, took partially, did not take.
- Common side-effect checklist, configurable by medication class or treatment episode.
- Optional free-text field: "Anything you want your psychiatrist to know before your next visit?" with a clear notice that messages are **not monitored in real time**.
- Safety screen with clear escalation instructions and local crisis resources.
- Reminder schedule with configurable frequency, with no reminders on Shabbat and Jewish holidays (configurable per clinic).
- Neutral, discreet reminder wording and sender name, with no mention of psychiatry or medication.
- Staff-assisted phone check-in for patients without a smartphone or internet access.
- Check-in page works on filtered internet and with images blocked.
- Patient can opt out of reminders at any time.
- Accessible design (large text, simple language, screen-reader support).
- Age-appropriate version of the check-in for adolescents who report for themselves (simpler wording, validated youth measures where available).

#### Guardian / caregiver check-in

See section 6.1 for the full rules. In short:

- Separate, clearly labelled check-in: "You are reporting about [patient first name]".
- Guardian verifies their own identity, not the patient's.
- Observer-based questions (what the guardian sees), not questions about the patient's inner feelings, using validated parent or caregiver measures where available.
- Same adherence, side-effect, free-text, and safety screens, worded for an observer.

#### Clinician dashboard

- Patient list with monitoring status: active, completed, overdue, needs review, safety alert.
- Patient timeline showing symptom trend, adherence, and side effects.
- Clear visual indicators for worsening, improving, stable, or incomplete data.
- Side-effect summary.
- Patient free-text comments.
- Every data point labelled by **who reported it** (patient, or guardian/caregiver with relationship). Patient and guardian reports shown side by side, never merged into one score.
- Pre-visit briefing view, linked to the next appointment date.
- **Export of the briefing** (copy-to-clipboard and PDF) so it can be pasted into the clinic's existing EMR without an integration.
- Ability to mark a monitoring episode as reviewed, extended, or closed.
- Minimal configuration for check-in frequency and monitoring duration.
- Hebrew-first, RTL-ready interface.

#### Clinic administration (the customer's account)

- Multi-tenant model: each clinic is a separate, isolated account.
- Support for multiple clinicians and, if needed, multiple locations within one clinic account.
- Clinician and staff accounts with role-based access control (for example: clinic admin, clinician, nurse, secretary).
- Patient assignment to a clinician, and reassignment when a patient moves to another clinician.
- Patient enrollment, basic demographics, and treatment-episode details.
- Consent capture and record, including guardian authority and minor assent where relevant.
- Add, change, or remove a guardian/caregiver linked to a patient (for example, when a minor turns 18 or guardianship changes).
- Reminder preferences.
- Safety-alert routing configuration: who receives alerts, by which channel, and during which hours.
- Basic audit log.
- **Clinic usage and value report** for the clinic manager: active clinicians, enrolled patients, check-in completion, briefings viewed, alerts raised. This is what the buyer uses to justify renewal.
- **Data export** of the clinic's data on request or on contract termination.
- Two-factor authentication for staff accounts.

#### AI features

Use AI narrowly and conservatively:

- Summarize patient-reported trends.
- Draft a short pre-visit briefing for clinician review.
- Highlight potentially clinically relevant changes, such as new side effects or worsening symptoms.
- Do not diagnose.
- Do not recommend medication or dose changes.
- Do not provide therapy.
- Do not make autonomous clinical decisions.
- Clearly label AI-generated summaries as draft support for clinician review.
- Show the source data behind every statement in the summary, so clinicians can verify it.
- The product must remain fully usable if the AI service is unavailable (charts and raw data still visible).
- AI vendors must meet the same privacy and data-residency requirements as the rest of the product, and must not use clinic data for model training.

### 6.1 Minors and dependent adults: guardian and caregiver reporting

Some patients cannot report reliably or legally on their own. Without a guardian path, the product collects no data for these patients, and clinics treating children, adolescents, or dependent adults will not buy it.

**Who this covers**

- **Children** (for example, under about 12 to 14): a parent or legal guardian reports.
- **Adolescents** (for example, about 14 to 17): the adolescent reports for themselves, a parent reports, or both. Clinicians often value both views (for example, in ADHD or depression).
- **Dependent adults**: a legal guardian, an appointed decision supporter, or a family caregiver approved by the patient or clinician reports, alone or alongside the patient.

Exact age thresholds and who may legally give consent and see data must come from Israeli legal advice (for example, the Patient Rights Law and the Legal Capacity and Guardianship Law) **[TO VALIDATE]**, and must be configurable per country.

**Reporting modes (set by the clinician at enrollment)**

1. Patient only.
2. Guardian/caregiver only.
3. Patient and guardian/caregiver, each with their own check-in.

**Requirements**

- Each guardian/caregiver has their own contact details, secure link, and identity verification; links are never shared between reporters.
- Record the relationship (parent, legal guardian, decision supporter, family caregiver, other) and the basis of authority. Optionally store proof of guardianship.
- Allow more than one guardian per patient (for example, two parents, including separated parents) **[TO VALIDATE how clinics handle custody disputes]**.
- Guardian questions are observer-based; use validated parent or caregiver versions of measures where they exist and are licensed.
- The safety screen is shown to guardians too, with instructions on what to do if they believe the patient is in danger, and it triggers the same clinic alert workflow.
- When a minor turns 18, or guardianship ends, the system prompts staff to review consent and remove or keep the guardian's access.

**Confidentiality**

- Guardians **cannot** see the patient's own answers or free-text by default. Many adolescents will not report honestly if parents can read their answers.
- Only the clinic team sees all reports. Any sharing with guardians is the clinician's decision, outside the product.
- The adolescent is told clearly, in age-appropriate language, who can see their answers and when the clinic may need to involve parents for safety reasons.

**MVP decision [TO VALIDATE in discovery]**

- If the first target condition includes ADHD or child and adolescent psychiatry, guardian reporting is **required in MVP**.
- If the first version is adult-only, build the data model to support guardians from day one, and release guardian reporting in the next phase.

### 6.2 Community-specific needs: ultra-Orthodox (Haredi) patients

The Haredi community is a large and fast-growing part of Israel's population, with high birth rates (many minors) and its own clinics, health-fund services, and referral networks. A product that ignores its needs will not work for many Israeli clinics. Supporting it well is also a strong local differentiator that foreign competitors are unlikely to match.

The needs below apply to **many, not all**, Haredi patients and vary between groups. Each clinic must be able to configure them per patient. Validate every point with Haredi patients, clinicians, and community mental-health organisations during discovery **[TO VALIDATE]**.

**Access without a smartphone or internet**

- Many Haredi patients use "kosher" phones with no internet or browser, and some kosher phone plans block or restrict SMS **[TO VALIDATE current carrier restrictions]**. A web link alone will not reach them.
- Others use filtered internet (for example, NetFree or Rimon). The check-in site must be approved by the main filtering services, load with images blocked, and contain no ads, external widgets, or unfiltered links.
- Provide alternative check-in channels:
  - **Staff-assisted phone check-in (MVP):** clinic staff call the patient or guardian and enter answers on their behalf, recorded as "staff-entered by phone".
  - **Automated voice (IVR) check-in (next phase):** the patient calls a number or receives an automated call and answers by keypad. Phone voice lines are familiar and widely used in the community.
  - **In-clinic tablet or paper check-in** before the appointment, entered by staff.
- The dashboard must show which channel was used for each check-in.

**Discretion and stigma**

- Mental illness can carry strong stigma, including concern about effects on a family's matchmaking (shidduchim) prospects. Patients may hide treatment even from family members.
- Phones are often shared within the family. Reminder messages and caller ID must be neutral: no words such as "psychiatry", "mental health", or medication names, and a neutral sender name chosen by the clinic.
- The patient chooses which phone number, and which family member if any, the clinic may contact.
- Patients may wish to involve a rabbi in treatment decisions. The product does not share data with rabbis or other third parties; any sharing is the clinician's decision, with the patient's explicit consent, outside the product.

**Shabbat and Jewish holidays**

- No reminders, automated calls, or messages from Friday before sunset until after Shabbat ends, or on Jewish holidays (Yom Tov). Use a Hebrew calendar with the clinic's local Shabbat times.
- Check-in schedules shift automatically around Shabbat and holidays so patients are not marked "overdue" because of them.
- Safety alerts must still be handled. Clinics must define who covers alerts during Shabbat and holidays (see section 8.2). Patient-facing crisis instructions must stay visible at all times.
- Optional display of Hebrew calendar dates alongside Gregorian dates.

**Language and content**

- Hebrew at launch, with English for English-speaking Haredi patients. Yiddish to be validated as a later option.
- Simple, modest wording. No images of people in patient-facing screens; use neutral icons only.
- Sensitive questions (for example, sexual side effects of medication) must be optional, phrased modestly, and approved by clinicians who work with the community. Where possible, the clinician should be able to ask these in person instead.
- Use culturally adapted versions of questionnaires where they exist.

**Families and guardians**

- Large families mean many minors, so guardian reporting (section 6.1) is likely needed for Haredi-focused clinics.
- Either parent may be the reporting guardian; the clinic must be able to choose which parent or parents report.

**Other Israeli communities**

The same approach of configurable channels, language, discretion, and calendar should later be extended to Arab patients (Arabic, Muslim and Christian holidays, and local stigma concerns), Russian-speaking patients, and other communities.

## 7. Explicit exclusions for MVP

The MVP must not include:

- Diagnosis or diagnostic suggestions.
- Medication recommendations or dose-change recommendations.
- Suicide-risk prediction or automated risk scoring.
- AI-generated clinical advice sent directly to patients.
- Therapy chatbot or open-ended AI counseling.
- Two-way chat or messaging between patient and clinician.
- Full EMR integration, unless a specific paying pilot clinic requires it.
- Appointment scheduling (the product only stores the next appointment date).
- Insurance billing or claims processing.
- Native iOS and Android apps.
- Advanced analytics or payer reporting.

## 8. Safety and compliance requirements

### 8.1 Clinical safety

- All patient-facing safety language must be reviewed and approved by a qualified clinician.
- The company must have a named clinical lead (a psychiatrist adviser or medical director) responsible for clinical content and safety review.
- The product must include clear instructions for emergencies and local crisis resources (for Israel, for example: MDA 101, Police 100, and ERAN emotional first aid 1201) **[TO VALIDATE with clinical lead]**.
- The product must not delay urgent care.
- Clinicians must be able to review and override AI-generated summaries.
- The product must maintain a clear separation between patient-reported data and clinician assessment.

### 8.2 Safety-alert ownership (must be defined before pilot)

The product is **not an emergency service and is not monitored 24/7**. The PRD must define:

- Who at the clinic receives safety alerts, by which channel (dashboard, SMS, email), and within what time frame.
- What happens outside working hours, on weekends, on Shabbat, and on Jewish and other holidays, given that some clinic staff will not use devices then.
- What the patient is told about response times, at enrollment and on every safety screen.
- How alerts are acknowledged and documented in the audit log.
- How responsibility is split between the clinic and the vendor in the customer contract.

### 8.3 Privacy and security

- **Israel (launch market):** comply with the Protection of Privacy Law and its amendments (including Amendment 13), the Privacy Protection (Data Security) Regulations, the Patient Rights Law, and Ministry of Health guidance on information security and cloud use for health data **[TO VALIDATE with Israeli privacy counsel]**.
- **Other markets (later):** design so that the product can be adapted to GDPR (EU and UK), HIPAA (US), and other local health-data laws without a rebuild.
- Data residency: store data in a region approved for the target market (for example, an Israeli cloud region for Israeli clinics) **[TO VALIDATE requirement]**.
- Encrypt data in transit and at rest.
- Role-based access control and two-factor authentication for staff.
- Audit logs for all access to patient data.
- Appropriate patient consent and authorization, recorded in the system. For minors and dependent adults, record who consented on the patient's behalf, their authority, and the patient's own assent where appropriate.
- Clear data-retention, deletion, and export policies.
- The clinic owns its patient data; the vendor processes it on the clinic's behalf. Define this in a data processing agreement (DPA) with each clinic.
- Do not use patient data to train third-party AI models without explicit legal and contractual safeguards.
- Prepare a standard security and privacy package for clinic procurement (security overview, DPA template, answers to common security questionnaires).

### 8.4 Clinical content and licensing

- Use validated questionnaires only where licensing allows (for example, some measures such as PHQ-9 and GAD-7 are free to use, while others require a licence) **[TO VALIDATE per measure]**.
- Use validated translations of each measure (Hebrew, Arabic, Russian) where they exist.

### 8.5 Regulatory positioning

- Position the product as a clinical workflow and patient-reported outcome collection tool.
- Avoid claims that it diagnoses, treats, predicts, or prevents disease.
- Obtain regulatory advice on whether any feature could be classified as software as a medical device in Israel (Ministry of Health Medical Devices Division, AMAR) and in future markets (EU MDR, US FDA, UK MHRA).
- Obtain regulatory and legal advice before making any clinical claims or expanding into risk prediction.

## 9. Key metrics

### Adoption metrics

- Number of clinics onboarded.
- Number of active clinicians per clinic.
- Number of patients enrolled in monitoring episodes.
- Percentage of invited patients who complete at least one check-in.
- Median check-in completion time.
- Check-in completion rate at 2, 4, and 6 weeks.
- Time from contract signature to first enrolled patient (time to value).

### Engagement metrics

- Percentage of monitoring episodes with at least three completed check-ins.
- Percentage of clinicians who open the pre-visit briefing before appointments.
- Number of pre-visit briefings viewed per active clinician per week.
- Weekly active clinician rate.
- Safety alerts acknowledged within the clinic's defined time frame.

### Business metrics (clinic as customer)

- Number of paying clinics.
- Monthly recurring revenue (MRR).
- Average revenue per clinic.
- Pilot-to-paid conversion rate.
- Sales cycle length (first meeting to signed contract).
- Customer acquisition cost (CAC) and payback period.
- Net revenue retention, including seat expansion within existing clinics.
- Clinic (logo) churn.
- Gross margin, including SMS, WhatsApp, cloud, and AI costs per patient.

### Outcome proxies

- Percentage of appointments with a completed pre-visit briefing.
- Percentage of medication-change episodes with documented adherence and side-effect data.
- Clinician-reported usefulness rating.
- Clinic-reported time saved.
- Clinic manager satisfaction and likelihood to renew.

## 10. Monetization and sales model

### Pricing **[TO VALIDATE in discovery]**

- Price is paid by the **clinic**, never by patients.
- Primary model: clinic subscription priced per clinician seat per month, with a minimum per clinic.
- Alternative to test: price per active monitored patient per month, which may fit clinics with variable clinician hours.
- Israeli price range to test: approximately ₪250 to ₪600 per clinician per month, or a clinic package of approximately ₪1,000 to ₪3,500 per month depending on size. Adjust for other markets.
- Offer a 60- to 90-day **paid** pilot with clear success criteria agreed in advance, rather than a long free trial.
- Annual contracts with monthly or annual billing after the pilot.
- Pricing must cover variable costs per patient (SMS/WhatsApp, cloud, AI).

### Sales motion

- Direct, founder-led sales to clinic owners and medical directors at first.
- Use the champion psychiatrist to bring the product into the clinic, and the clinic usage and value report to support renewal.
- Partnerships to explore later: Israeli EMR and clinic-management software vendors, psychiatric associations, pharmaceutical-independent channels only **[TO VALIDATE]**.
- Avoid funding or partnerships that could create conflicts of interest about medication (for example, pharmaceutical sponsorship) without careful legal and ethical review.

### Onboarding and customer success

- Onboarding target: a clinic enrolls its first patient within one week of signing.
- Short training for clinicians (under 30 minutes) and for staff.
- A named contact for each pilot clinic.
- Support in Hebrew during Israeli business hours.

## 11. Go-to-market plan

### Phase 1: Discovery, weeks 1 to 4

- Interview 15 to 25 psychiatrists, psychiatric nurses, clinic owners or medical directors, practice managers, and medical secretaries in Israel.
- Include at least 2 to 3 clinics serving the Haredi community, plus Haredi patients or family members where the clinic allows it.
- Interview at least 5 people who would actually sign the contract (economic buyers).
- Identify the single most painful medication-monitoring workflow.
- Ask what they currently use (including WhatsApp and phone calls), what they would pay, who approves the purchase, and what would prevent adoption.
- Map which EMR or clinic-management systems the target clinics use.
- Identify 3 to 5 design-partner clinics willing to run a paid pilot.
- Start privacy and regulatory legal review in parallel.

### Phase 2: MVP build, weeks 5 to 12

- Build the narrow medication-change monitoring workflow in Hebrew.
- Agree on the safety-alert workflow and pilot success criteria with each pilot clinic.
- Onboard 3 to 5 pilot clinics.
- Manually support onboarding and configuration.
- Measure completion, clinician usage, and satisfaction.

### Phase 3: Validation, weeks 13 to 24

- Convert successful pilots to paid annual subscriptions.
- Improve the pre-visit briefing and workflow.
- Add only features requested repeatedly by multiple paying clinics.
- Develop a repeatable sales, onboarding, and support process.

### Phase 4: Expansion, after validation

- Expand to more Israeli clinics and explore health funds and hospitals as enterprise customers.
- Select the first international market based on regulatory effort, language, sales access, and willingness to pay (candidates: UK, EU countries, US) **[TO VALIDATE]**.
- For each new country: local privacy and medical-device review, local crisis resources, translations of measures, local pricing, and data residency.

## 12. Success criteria

Proceed to broader investment only if, within 90 to 120 days of pilot launch:

- At least 3 clinics actively use the product.
- At least 50 percent of invited patients complete at least one check-in.
- Clinicians open the pre-visit briefing before at least 50 percent of relevant appointments.
- At least 2 clinics sign a paid contract after the pilot.
- Clinic decision-makers report that the product saves time or improves care without adding burden.
- No unresolved safety incidents related to the product.

If these criteria are not met, stop, interview users and buyers, and pivot before building more features.

## 13. Major risks

| Risk | Why it matters | Mitigation |
|---|---|---|
| Workflow burden | Clinicians and staff will abandon tools that add steps. | Design for under 60 seconds per check-in and minimal clinician clicks. |
| Low patient completion | The product has no value without patient data. | Short check-ins, sensible reminders, native-language content, simple mobile web access. |
| Wrong person reporting or seeing data | Guardians, separated parents, or caregivers may lack legal authority or may breach a patient's confidentiality. | Recorded authority per guardian, separate links and identity checks, guardians cannot see patient answers, review at age 18 or guardianship change. |
| Excluding communities without smartphones | Many Haredi patients use kosher phones or filtered internet, so a link-only product will get no data from them. | Staff-assisted phone check-in in MVP, automated voice check-in next, filter-approved site. |
| Stigma and accidental disclosure | A revealing message on a shared family phone could harm the patient socially. | Neutral message wording and sender name, patient-chosen contact number, no third-party sharing. |
| Culturally inappropriate content | Immodest images or blunt sensitive questions could cause patients or clinics to reject the product. | No images of people, optional and modestly worded sensitive items, review by community clinicians. |
| Safety incidents | Mental-health data and crisis situations create serious risk. | Clinician-approved safety protocols, local crisis resources, defined alert ownership, human review. |
| Unclear liability for alerts | Patients may expect someone is watching 24/7. | Clear patient messaging, clinic-configured alert routing, contract terms splitting responsibility. |
| Privacy and compliance | Psychiatric data is highly sensitive and regulated differently in each country. | Privacy, access control, audit logs, consent, data residency from day one; local legal review per market. |
| Clinician distrust of AI | AI errors or unclear accountability can block adoption. | Keep AI assistive, transparent, source-linked, reviewable, and narrowly scoped. |
| Users like it, buyers don't pay | Psychiatrists may like the product but the clinic owner may not see ROI. | Involve economic buyers in discovery, paid pilots, clinic value report. |
| Long sales cycles | Health funds and hospitals have slow procurement. | Start with private clinics; prepare a standard security and privacy package. |
| EMR integration expectations | Lack of integration may reduce adoption. | Start standalone with copy/PDF export; integrate only for committed customers. |
| Small home market | Israel alone may limit growth. | Design for localization from the start; plan international expansion after validation. |
| Competitors with more funding | US platforms may enter the market. | Local focus, language, compliance, and very simple workflow as differentiators. |

## 14. Assumptions

- Private psychiatric clinics in Israel will pay for a monitoring tool if it saves clinician time and improves care.
- Patients will complete short check-ins by SMS or WhatsApp link without a dedicated app.
- A standalone tool with export is acceptable to early clinics without EMR integration.
- A clinical lead will be available to approve safety content and measures.
- Hebrew-first is sufficient for the first pilots.

## 15. Open questions

- Which psychiatric conditions and medication changes should the first version support (depression, anxiety, ADHD, bipolar disorder, or another)?
- Which validated or pragmatic symptom measures should be used, and are validated translations available?
- Are minors in scope for MVP? This depends on whether the first condition includes ADHD or child and adolescent psychiatry.
- At what ages may a minor report alone, give their own consent, or keep answers confidential from parents, in Israel and in later markets?
- How should the product handle separated parents, disputed custody, or a guardian whose authority is unclear?
- What proof of guardianship or decision-supporter appointment do clinics need to keep?
- What is the optimal check-in frequency for each condition and medication type?
- How should the product handle patients who do not have smartphones or reliable internet access?
- Should Haredi-focused clinics be among the first pilot clinics, and is automated voice (IVR) check-in needed in MVP for them?
- Which kosher phone plans allow SMS, and is the check-in site approved by NetFree, Rimon, and other filtering services?
- Which questionnaire items are culturally sensitive for Haredi patients, and are culturally adapted versions available?
- Is Yiddish needed, and for which share of patients?
- Is WhatsApp an acceptable and compliant channel for check-in links in Israel?
- What exact safety-alert workflow will each clinic use, including after hours?
- Which EMR or clinic-management systems do target clinics use, and is any integration required to buy?
- Who signs the contract in each segment, and what is the typical approval process?
- What price and pricing model will clinic owners accept without lengthy procurement?
- What evidence or documentation will clinics need before trusting the product?
- Does any planned feature require medical-device registration in Israel or future markets?
- Which country should be the first international market, and when?

## 16. Requested PRD output

Create a complete PRD that includes:

1. Executive summary.
2. Background and problem statement (clinic-level and clinician-level).
3. Customer, buyer roles, and user personas.
4. Product vision and objectives.
5. Competitive landscape and differentiation.
6. Scope: in-scope, out-of-scope, and future roadmap.
7. User stories and acceptance criteria (for clinicians, staff, clinic admins, and patients).
8. Detailed functional requirements.
9. Patient and guardian/caregiver check-in experience specification, including localization, accessibility, alternative channels (staff phone, IVR, in-clinic), and community-specific needs such as Haredi patients.
10. Clinician dashboard specification.
11. Clinic administration and usage/value report specification.
12. AI feature specification and guardrails.
13. Safety-alert workflow specification.
14. Data model outline, including multi-tenant clinic structure and patient–guardian relationships.
15. Privacy, security, clinical safety, and compliance requirements (Israel first, then other markets).
16. Non-functional requirements: performance, accessibility, reliability, mobile web usability, localization (RTL).
17. Pricing, sales model, onboarding, and customer success.
18. Key metrics and success criteria.
19. MVP release plan and phased roadmap, including international expansion.
20. Risks, assumptions, dependencies, and open questions.
