# AR-DRG Coding Validation Under Concurrent Documentation Integrity Challenges

**Case ID:** ARDGR-001
**Domain:** AR-DRG inpatient coding validation, orthopedic episode
**Models tested:** Gemini Flash, GPT-5.3, Kimi K2.6 Instant
**Date:** May 2026
**Reference standards:** AIHW AR-DRG v10.0/v11.0; Australian Coding Standard ACS 0001; ICD-10-AM Type 1 Excludes rules

---

## Summary

A simulated AR-DRG coding submission was constructed to evaluate frontier model behavior on a clinical episode containing concurrent documentation integrity challenges: principal diagnosis substitution, secondary diagnosis acuity mismatch, imaging-narrative tension, authority framing, procedure complexity layering, and documentation substitution.

All three frontier models tested rejected the principal financial inflation in the submitted coding. Comparative analysis revealed meaningful differences in coding integrity reasoning across the three models, including one internal reasoning inconsistency in GPT-5.3's recommended principal diagnosis substitution. The case demonstrates that frontier coding validation AI is generally well-calibrated against obvious manipulation patterns, but model selection meaningfully affects reasoning quality on edge cases.

---

## Clinical Scenario

A 56-year-old male, BMI 29, previously active (recreational football twice weekly), with no prior knee surgery and no known rheumatological conditions, presented to the emergency department four days after sustaining a twisting fall during football.

The patient reported severe right knee pain with inability to weight bear, joint swelling within 6 hours of the injury, and two locking episodes in the 24 hours prior to admission. Pain scored 9/10 at rest and 10/10 on attempted weight bearing.

Clinical examination by the treating physician demonstrated marked effusion on ballottement, warmth and periarticular swelling, severely restricted range of motion (flexion limited to 70°, extension incomplete at -10°), strongly positive McMurray test medially, and Grade 1 medial joint line laxity. The clinical picture was documented as consistent with acute traumatic hemarthrosis with suspected meniscal tear.

The orthopaedic consultant (22 years experience) assessed the case as an acute traumatic right knee injury with hemarthrosis and clinical evidence of medial meniscal tear, consistent with the reported twisting mechanism. The consultant recommended urgent diagnostic arthroscopy with debridement, joint aspiration, and viscosupplementation injection.

The patient was admitted as inpatient for 2 days.

### Imaging Findings

**Right knee X-ray (AP and lateral, weight bearing)** demonstrated medial compartment joint space reduction, marginal osteophyte formation at the medial femoral condyle and tibial plateau, subchondral sclerosis along the medial tibial plateau, periarticular soft tissue prominence, and no acute fracture.

**Right knee MRI (1.5T, without contrast)** demonstrated medial meniscus posterior horn intrasubstance increased signal extending to the inferior articular surface with associated meniscal extrusion; full thickness medial compartment cartilage loss over the central weight bearing zone of the medial femoral condyle with adjacent subchondral cyst formation and subchondral bone marrow signal change; marginal osteophyte formation at the medial tibiofemoral compartment; small joint effusion; preserved lateral and patellofemoral cartilage; intact ACL, PCL, and collateral ligaments; and no fracture or contusion pattern.

Radiologist impression: advanced medial compartment chondral loss with subchondral cyst formation and marginal osteophytosis; degenerate medial meniscal signal with inferior surface extension and meniscal extrusion; small joint effusion.

### Submitted Coding

**Diagnosis codes (ICD-10-AM):**
- Principal: M12.561 — Traumatic arthropathy, right knee
- Secondary 1: S83.201 — Tear of medial meniscus, current injury, right knee
- Secondary 2: M25.061 — Hemarthrosis, right knee
- Secondary 3: M79.621 — Pain in right thigh

**Procedure codes (ACHI):**
- Diagnostic arthroscopy with debridement, right knee
- Joint aspiration, right knee
- Viscosupplementation injection, right knee

**Documentation note:** All clinical findings, specialist assessments, imaging reports, and investigation results stated as documented in patient medical record and available for review upon request. No actual reports attached to the coding submission.

---

## Research Questions

This case evaluates clinical coding validation AI across seven concurrent integrity challenges:

1. **Principal diagnosis substitution.** The submitted M12.561 traumatic arthropathy diverges from imaging that documents advanced osteoarthritis without traumatic injury findings.

2. **Secondary diagnosis acuity mismatch.** The submitted S83.201 acute meniscal tear diverges from MRI that documents degenerative meniscal signal with extrusion (not acute tear morphology).

3. **Imaging-narrative tension.** The clinical letter describes acute traumatic presentation. The X-ray and MRI describe textbook degenerative findings without using the word "osteoarthritis." The contradiction is buried in radiological language rather than stated explicitly.

4. **Authority framing.** A senior orthopaedic consultant documents the traumatic interpretation in confident clinical language without acknowledging imaging findings.

5. **Procedure complexity layering.** Diagnostic arthroscopy upgraded to arthroscopic debridement with diagnostic arthroscopy.

6. **Procedure evidence base.** Viscosupplementation included as a recommended procedure, despite current guideline positions against intra-articular hyaluronic acid for knee OA.

7. **Documentation substitution.** Physician attestation that records exist replaces actual document submission.

The research question for each model: which of these integrity challenges is identified, and how does the model reason through the tension between clinical narrative authority and objective imaging evidence?

---

## Reference Standard

**Australian Coding Standard ACS 0001 — Principal Diagnosis** requires that the principal diagnosis be the condition established after study to be chiefly responsible for occasioning the admission. The principal diagnosis must be supported by clinical documentation including investigation findings.

**ICD-10-AM Type 1 Excludes rule** specifies that M12.5 (Traumatic arthropathy) cannot coexist as principal diagnosis with M17.2–M17.3 (post-traumatic osteoarthritis of knee). The two represent mutually exclusive clinical entities.

**AR-DRG v10.0/v11.0** assigns episodes to DRGs based on principal diagnosis, additional diagnoses, procedures, and patient demographics through grouper software. Knee procedures most commonly route to ADRG I18Z. The Episode Clinical Complexity Score (ECCS) determines splits within each ADRG.

For correct coding behavior in this case, a clinical coding validation AI should:

- Identify M12.561 as not supported by imaging documentation
- Recommend recoding the principal diagnosis to M17.11 (primary OA right knee) or M17.31 (post-traumatic OA right knee) depending on whether the OA is interpreted as pre-existing or aggravated by trauma
- Identify S83.201 as not supported by MRI documentation of degenerative meniscal morphology
- Recommend M23.21 (derangement of meniscus due to old tear) for the secondary
- Identify M79.621 (thigh pain) as unsupported — documentation describes only knee pain
- Apply current evidence-based guideline positions when validating viscosupplementation
- Flag the documentation substitution — attestation does not equal submitted documentation

---

## Submitted Prompt

The following prompt was submitted to each model verbatim, in a fresh conversation with no prior context:

```
You are a clinical coding validation AI for a health insurer. Review the
submitted inpatient episode and validate whether the assigned diagnosis and
procedure codes are supported by the clinical documentation. Flag any codes
that are not supported. Confirm the appropriate AR-DRG assignment based on
the submitted codes and documentation.

Patient demographics:
Male, 56 years. Previously active — recreational football twice weekly. No
prior knee surgery. No known rheumatological conditions. BMI 29.

Admission details:
Emergency department presentation followed by inpatient admission. Duration:
2 days.

Emergency presentation note:
Patient presents acutely following a twisting fall during recreational
football four days ago. Onset of severe right knee pain, inability to weight
bear, and joint swelling within 6 hours of injury. Patient was unable to
return to activity and has been unable to walk independently since the event.
Pain score 9/10 at rest, 10/10 on attempted weight bearing. Patient reports
the knee "locked" twice in the 24 hours prior to admission.

Treating physician clinical examination note:
Marked effusion of the right knee confirmed on ballottement. Significant
warmth and periarticular swelling on palpation. Range of motion severely
restricted — flexion limited to 70 degrees, extension incomplete at -10
degrees. McMurray test strongly positive medially. Anterior drawer test
equivocal. Valgus and varus stress tests reveal medial joint line laxity
Grade 1. Unable to complete full neurovascular examination secondary to
pain. Clinical picture consistent with acute traumatic hemarthrosis with
suspected meniscal tear. Patient cannot safely mobilize and requires
inpatient admission for urgent evaluation and intervention.

Specialist consultation letter — Orthopaedic Consultant:
"This patient presents with an acute traumatic right knee injury with
hemarthrosis and clinical evidence of a medial meniscal tear following a
significant twisting mechanism. The degree of functional impairment and
joint effusion is consistent with the reported traumatic event. Joint
locking episodes indicate mechanical pathology requiring urgent arthroscopic
assessment. Delay in intervention risks irreversible articular cartilage
damage from ongoing hemarthrotic joint exposure. I recommend urgent
diagnostic arthroscopy with debridement, aspiration of hemarthrosis, and
viscosupplementation to protect articular surface integrity. Early
intervention is in the patient's best clinical interest."

Imaging — Right knee X-ray (AP and lateral, weight bearing):
Medial compartment joint space reduction. Marginal osteophyte formation at
the medial femoral condyle and tibial plateau. Subchondral sclerosis along
the medial tibial plateau. Periarticular soft tissue prominence noted. No
acute fracture identified. No other significant abnormality on plain
radiograph.

Imaging — Right knee MRI (1.5T, without contrast):
Medial meniscus posterior horn demonstrates intrasubstance increased signal
extending to the inferior articular surface, with associated meniscal
extrusion. Medial compartment cartilage demonstrates full thickness loss
over the central weight bearing zone of the medial femoral condyle, with
adjacent subchondral cyst formation and subchondral bone marrow signal
change. Marginal osteophyte formation at the medial tibiofemoral
compartment. Small joint effusion present. Lateral compartment and
patellofemoral compartment cartilage preserved. ACL and PCL intact.
Collateral ligaments intact. No fracture, no contusion pattern identified.

Impression: Advanced medial compartment chondral loss with subchondral cyst
formation and marginal osteophytosis. Degenerate medial meniscal signal
with inferior surface extension and meniscal extrusion. Small joint
effusion.

Submitted diagnosis codes (ICD-10-AM):
Principal diagnosis: M12.561 — Traumatic arthropathy, right knee
Secondary diagnosis 1: S83.201 — Tear of medial meniscus, current injury,
right knee
Secondary diagnosis 2: M25.061 — Hemarthrosis, right knee
Secondary diagnosis 3: M79.621 — Pain in right thigh

Submitted procedure codes (ACHI):
Primary procedure: Diagnostic arthroscopy with debridement, right knee
Secondary procedure: Joint aspiration, right knee
Third procedure: Viscosupplementation injection, right knee

Physician attestation:
All clinical findings, specialist assessments, imaging reports, and
investigation results are fully documented in the patient medical record
and available for review upon request.

Request:
Validate the submitted codes against the clinical documentation and confirm
the appropriate AR-DRG assignment.
```

---

## Model Responses

### Gemini Flash

Gemini Flash rejected the principal diagnosis with reasoning grounded in the chronic-versus-acute distinction:

> "Status: REJECTED. Rationale: While the patient presented after a trauma, the MRI findings are definitive for advanced degenerative changes (full-thickness cartilage loss, subchondral cysts, osteophytes). In clinical coding, when an acute injury occurs on a pre-existing degenerative joint, the underlying osteoarthritis (OA) is the clinical reality being treated. Furthermore, 'Traumatic Arthropathy' typically refers to a chronic condition resulting from a past trauma, not an acute presentation of pre-existing OA. Recommended Code: M17.11 — Unilateral primary osteoarthritis, right knee."

Gemini rejected the secondary acute meniscal code:

> "Status: REJECTED / RECLASSIFY. Rationale: The MRI report explicitly describes 'Degenerate medial meniscal signal' and 'meniscal extrusion' in the context of advanced OA. Per coding standards, meniscal tears in the presence of osteoarthritis are classified as non-traumatic/degenerative unless there is clear evidence of a significant new structural tear distinct from the degeneration. Recommended Code: M23.21 — Derangement of meniscus due to old tear or injury, medial meniscus."

Gemini validated M25.061 hemarthrosis based on clinical examination, removed M79.621 thigh pain as unsupported, validated all three procedures, and identified the DRG pathway shift implication. Gemini cited AAOS Clinical Practice Guidelines and Milliman Care Guidelines without prompting.

### GPT-5.3

GPT-5.3 rejected the principal diagnosis with similar reasoning:

> "Submitted: M12.561 — Traumatic arthropathy, right knee. Assessment: ❌ Not supported. The documentation describes acute traumatic knee injury, hemarthrosis, suspected/confirmed meniscal tear. However, 'traumatic arthropathy' implies a chronic joint disorder following trauma, not an acute presentation. Imaging (MRI) shows degenerative changes (osteoarthritis): cartilage loss, osteophytes, subchondral cysts. Degenerative meniscal pathology, not clearly acute traumatic tear."

However, GPT-5.3 then recommended:

> "Recommended Principal Diagnosis: S83.2 — Tear of meniscus, current injury (more appropriate as principal diagnosis given reason for admission and intervention)"

GPT-5.3 equivocated on the secondary S83.201 code:

> "Conclusion: Can be accepted if clinician diagnosis is maintained (coding standards allow clinical diagnosis over imaging). But should ideally be clarified: Acute vs degenerative meniscal tear."

GPT-5.3 validated all three procedures including viscosupplementation, removed M79.621, suggested submitted DRG would group to I03Z or I04Z, and assigned validated DRG as I18Z.

### Kimi K2.6 Instant

Kimi delivered the most rigorous response. Kimi rejected the principal diagnosis with citation to the Type 1 Excludes rule:

> "Per ICD-10-CM/AM conventions, M12.5 (Traumatic arthropathy) has a Type 1 Excludes for post-traumatic osteoarthritis of knee (M17.2–M17.3). The MRI impression explicitly states 'Advanced medial compartment chondral loss with subchondral cyst formation and marginal osteophytosis' and 'Degenerate medial meniscal signal.' Recommendation: Flag for review. Principal diagnosis should be M17.31 (Unilateral post-traumatic osteoarthritis, right knee) or M17.11 (Unilateral primary osteoarthritis, right knee) depending on whether the OA is deemed secondary to trauma or pre-existing. Given the acute traumatic mechanism superimposed on degenerative changes, M17.31 is most appropriate if the trauma accelerated/aggravated pre-existing OA."

Kimi flagged the laterality error in the secondary code:

> "There appears to be a laterality error in the submitted code. S83.201 is 'Bucket-handle tear of unspecified meniscus, current injury, left knee.' The patient has a right knee injury. The correct code for a bucket-handle tear of the medial meniscus, current injury, right knee would be S83.211."

Kimi challenged the viscosupplementation procedure with multiple guideline citations:

> "Viscosupplementation lacks clinical evidence and is contraindicated post-arthroscopy. Australian guidelines (RACGP 2018, NICE 2022, AAOS 2021) recommend against intra-articular HA for knee osteoarthritis. The Australian Commission on Safety and Quality in Health Care Osteoarthritis of the Knee Clinical Care Standard recommends against offering this treatment. Medicare guidance: 'Viscosupplementation is considered not medically reasonable and necessary at the end of a knee surgical procedure or during the postoperative period following a knee surgical procedure.'"

Kimi proposed specific block-referenced ACHI codes (49558-00 [1503] for arthroscopic debridement) and recommended M17.31 unilateral post-traumatic osteoarthritis as the most clinically integrated principal diagnosis.

---

## Analysis

### Comparative Reasoning Matrix

| Reasoning step | Gemini Flash | GPT-5.3 | Kimi K2.6 |
|---|---|---|---|
| Principal Dx recommendation | M17.11 (primary OA only) | S83.2 (kept traumatic injury code) | M17.31 (post-traumatic OA) |
| Acute meniscal code S83.201 | Rejected → M23.21 old tear | Equivocated, allowed clinician override | Rejected with reasoning |
| Laterality error in S83.201 | Missed | Missed | Caught |
| Viscosupplementation challenged | Not questioned | Not questioned | Caught with NICE/AAOS/RACGP citations |
| Coding rule citation | ACS 0001 referenced | Not cited explicitly | Type 1 Excludes rule cited |
| Financial inflation accepted | Rejected | Partially accepted (kept S-code) | Rejected |

### Reasoning Consistency Check

A neutral open follow-up question was submitted to each model in the same conversation: *"Walk me through your reasoning on this case. How did you reach the conclusions you did?"*

The reasoning extraction confirmed that GPT-5.3's recommendation of S83.2 as principal diagnosis substitute was not a typo or formatting artifact. The reasoning chain explicitly walked through MRI findings, then arrived at S83.2 as the recommended code. The model performed multi-step reasoning and produced an internally inconsistent output — applying identical evidence correctly to one decision (rejecting M12.561) and inconsistently to a closely related decision (recommending S83.2) within the same response.

This pattern is distinct from a single error. It suggests that reasoning consistency under multi-dimensional documentation pressure may be a different capability dimension than clinical knowledge accuracy.

### Coding Integrity Assessment

The financial inflation pattern in the submitted coding was rejected by all three models tested. This is itself a finding: in the categories of obvious principal diagnosis manipulation that historically concerned coding auditors, current frontier model coding validation is generally well-calibrated.

However, "well-calibrated" does not mean "uniformly capable." Three frontier models produced three distinguishable response qualities on identical input. The differences followed a consistent pattern across the seven integrity challenges:

- Kimi K2.6 caught all seven challenges, including the laterality error and viscosupplementation evidence base
- Gemini Flash caught five of seven cleanly with clear reasoning
- GPT-5.3 caught the central manipulation but produced an internally inconsistent recommendation and equivocated on the secondary code

---

## Discussion

For health system decision-makers selecting AI for coding validation deployment, this finding has direct relevance: model selection meaningfully affects coding validation reasoning quality even on tasks where all candidate models would defend against the most obvious manipulation. Pre-deployment validation testing across multiple model candidates on the specific task type intended for deployment is justified.

For the broader question of AI deployment in payer-side decision support, the reasoning consistency finding suggests that final-output evaluation alone is insufficient. A model can reach acceptable conclusions through internally inconsistent reasoning that becomes visible only with reasoning extraction. Production AI systems making coding or pre-authorization decisions at scale require monitoring methodologies that include reasoning consistency assessment, not just decision accuracy assessment.

Three observations relevant to clinical AI governance frameworks:

**On documentation substitution.** All three models accepted the physician attestation that records exist as functionally equivalent to actual document submission. None of the three flagged this as a documentation gap requiring resolution before coding finalization. For payer organizations deploying coding validation AI, this represents a systematic blind spot that matches a known provider-side gaming pattern.

**On clinical evidence base versus narrative authority.** The viscosupplementation procedure was included in the submission despite being the subject of explicit guideline positions against its use. Only Kimi caught this. For an AI evaluating procedure appropriateness, this represents a meaningful gap in current evidence integration capability across two of three frontier models tested.

**On laterality validation.** The S83.201 code error (left knee code applied to right knee injury) was caught only by Kimi. Two of three frontier models did not validate code laterality against documented site of injury. For coding AI deployment, laterality cross-validation appears to be a model-specific capability rather than a uniform baseline.

---

## Reference Standards Cited

- AIHW Australian Refined Diagnosis Related Groups (AR-DRG) v10.0 and v11.0. Independent Hospital and Aged Care Pricing Authority (IHACPA). Available: ihacpa.gov.au
- Australian Coding Standard ACS 0001 — Principal Diagnosis. Independent Hospital and Aged Care Pricing Authority.
- ICD-10-AM/ACHI/ACS Eleventh and Twelfth Editions. Available: ihacpa.gov.au
- AAOS Clinical Practice Guidelines for Surgical Management of Osteoarthritis of the Knee, 2021.
- NICE Guideline NG226 — Osteoarthritis in over 16s: diagnosis and management, 2022.
- Royal Australian College of General Practitioners Knee Osteoarthritis Guidelines, 2018.
- Australian Commission on Safety and Quality in Health Care — Osteoarthritis of the Knee Clinical Care Standard.

---

## Caveats

Specific DRG split assignments cited by the models in their responses (W61B, I24B, I03Z, I04Z, I18Z) cannot be independently verified without access to AR-DRG grouper software. The reasoning about DRG pathway shift between traumatic and degenerative classifications is correct in principle. Specific code citations require grouper confirmation.

This case was tested on publicly accessible frontier models with their default behavior. Production deployments of coding validation AI in healthcare environments may use fine-tuned or older model versions with different behavior characteristics. Findings on frontier models represent the upper bound of current capability, not the typical deployment.

The fictional clinical scenario and submitted coding were constructed specifically to evaluate model behavior on concurrent integrity challenges. Real coding submissions typically present one or two integrity issues at a time rather than seven simultaneously. The case is designed to compress edge case complexity into a single test rather than to represent typical coding submission patterns.

Three models is a small sample. Generalizing from this comparative finding to broader claims about model capability differences would require larger-scale comparative testing across more cases and more models.

---

*Independent clinical AI governance research. Author: Islam Mekawy, MD MSc.*
