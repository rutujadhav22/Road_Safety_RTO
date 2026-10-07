# PROJECT REPORT & TECHNICAL DOCUMENTATION

**Project Title:** Comprehensive Quality Audit, Legal Verification, and Full-Stack Implementation of the Indian RTO Driving Licence Question Bank  
**Candidate Name:** Rutuja Jadhav  
**Platform / Initiative:** Docnish Road Safety  
**GitHub Repository:** [https://github.com/rutujadhav22/Road_Safety_RTO](https://github.com/rutujadhav22/Road_Safety_RTO)  
**Target Branch:** `main`  
**Date of Submission:** October 2026  

---

## 1. Executive Summary

The official Indian Regional Transport Office (RTO) Learner’s Licence Question Bank is widely used across India to train aspiring motor vehicle drivers. However, an in-depth audit of the widely circulated dataset (originally published through state transport portals such as Kerala MVD and digitised by portals like `roadsafety.docnish.in`) revealed significant anomalies. These included:
1. **Critical factual errors** that promoted hazardous driving habits (such as illegal left-side overtaking on two-lane roads).
2. **Directionally inverted road signage answers** (such as mandatory right turns labeled as left turns).
3. **Outdated penalties and fines** based on the obsolete pre-2019 Motor Vehicles Act, which mislead applicants regarding statutory fines.
4. **Optical Character Recognition (OCR) errors** resulting in nonsensical questions (e.g., *"Alcohol bus"* instead of *"A school bus"*).

To resolve these defects, this project carried out a comprehensive data engineering and software development lifecycle:
- Audited all 410 questions systematically against the **Motor Vehicles Act 1988**, the **Motor Vehicles (Amendment) Act 2019**, the **Central Motor Vehicles Rules (CMVR) 1989**, and the **Motor Vehicles (Driving) Regulations 2017**.
- Produced a clean, production-ready dataset in JSON format (`rto_question_bank_corrected.json`).
- Designed, implemented, and deployed an interactive, mobile-responsive Web Application (`index.html`) featuring search, categorized study modules, and a real-time 15-question RTO Mock Exam.
- Version-controlled and pushed the complete codebase to GitHub on the `main` branch.

---

## 2. Problem Statement

Candidates preparing for the RTO Learner’s Licence Computer-Based Test (LL Test) depend directly on online question banks. When these platforms contain incorrect answer keys or obsolete regulations:
- **Safety Risk:** Drivers internalize illegal and dangerous road behaviors (e.g., overtaking on the left side).
- **Exam Failure:** Applicants fail questions on modern road tests because answers contradict recent gazetted laws.
- **Legal Misinformation:** Citizens remain unaware of updated penal provisions enacted under the 2019 Motor Vehicles Amendment.

---

## 3. Comprehensive Audit: Errors Identified & Corrections Applied

### 3.1. Fatal & Factually Incorrect Answer Keys

| Question ID / Ref | Original Question Text | Flawed Original Key | Verified Correct Answer | Legal & Technical Justification |
| :--- | :--- | :--- | :--- | :--- |
| **ID 171** *(PDF Q185)* | *You are driving on a two-lane street, vehicle in front of you is moving very slowly and the road ahead is clear for overtaking, you should...* | **Option 1:** Pass the vehicle from the left hand side ❌ | **Option 2:** Pass the vehicle from the right hand side ✅ | **Regulation 23 of the Motor Vehicles (Driving) Regulations 2017 & Rule 14 of the Rules of the Road Regulations 1989:** In left-hand drive traffic systems (India), overtaking must strictly be performed on the right. Passing on the left on a two-lane road is hazardous and illegal. |
| **PDF Q70** | *The following sign represents... (Blue circle with white arrow pointing ahead and right)* | **Option 2:** Compulsory ahead or turn left ❌ | **Option 1:** Compulsory ahead or turn right ✅ | Visual inspection confirms the arrow points straight and right. The original answer key suffered an inversion error. |
| **PDF Q48** | *The sign represents... (Red circle with two vertical arrows crossed out with red slash)* | **Option 2:** One-way ❌ | **Option 3:** Prohibited in both directions ✅ | Two opposing arrows crossed out signifies total traffic prohibition in both directions. A one-way sign displays a single permitted or single prohibited arrow. |
| **PDF Q46 vs Q66** | *The sign represents... (Blue circle with red border and red cross 'X')* | Marked as "No parking" in Q46 ❌ | Marked correctly as "No Stopping or standing" in Q66 ✅ | Under IRC:67-2012, a single red slash (`/`) is **No Parking**, whereas a full red cross (`X`) signifies a clearway: **No Stopping or Standing**. |
| **PDF Q385** | *While you intend to take a right or left turn, the sequence of action which you have to do...* | **Option 1:** gear - mirror - signal ❌ | Standard MSM routine: **Mirror -> Signal -> Gear / Manoeuvre** ✅ | Changing gear before checking mirrors and signaling violates fundamental driving safety drills. |
| **PDF Q315** | *The correct procedure for stopping a vehicle not equipped with anti lock brake system...* | **Option 2:** apply foot brake firmly once ❌ | **Option 1:** Cadence / pumping action on brakes ✅ | Applying firm continuous brake pressure without ABS locks the wheels, resulting in loss of steering control and severe skidding. |

---

### 3.2. Statutory Penalties Updated (Motor Vehicles Amendment Act 2019)

The legacy database contained obsolete fine amounts from the 1988 Act. All explanations and annotations have been aligned with current statutory law:

| Traffic Offence | Legacy Question Bank Fine | Amended Law (MV Amendment Act 2019) | Governing Section |
| :--- | :--- | :--- | :--- |
| **Seat Belt Non-Compliance** *(ID 416)* | ₹100/- | **₹1,000/-** | Section 194B |
| **Driving Under the Influence (DUI)** *(ID 325 / Q161, Q347)* | ₹2,000/- or 6 months imprisonment | **₹10,000/- and/or 6 months** (1st offence)<br>**₹15,000/- and/or 2 years** (2nd offence) | Section 185 |
| **Overloading Goods Vehicles** *(ID 177 / Q191)* | ₹2,000/- | **₹20,000/- + ₹2,000/- per additional tonne** | Section 194 |
| **Mobile Phone Usage While Driving** *(ID 386 / Q409)* | ₹100 - ₹500 | **₹1,000/- to ₹5,000/-** (Dangerous Driving) | Section 184(c) |
| **Driving Without Valid Licence** *(PDF Q424)* | ₹500/- | **₹5,000/-** | Section 181 |

---

### 3.3. Speed Limits & Certification Rules

1. **National Highway Speed Limits (PDF Q170, Q174):**
   - The question bank cited 70 km/h for motor cars and 50 km/h for motorcycles, which were archaic local speed ceilings.
   - **MoRTH Notification (S.O. 1522(E), 2018)** established national limits of **100 km/h** for M1 passenger cars on 4-lane divided National Highways (120 km/h on Expressways) and **80 km/h** for motorcycles.
2. **PUCC Validity (ID 62 / PDF Q67):**
   - The original key stated a blanket 6-month validity.
   - Under **CMVR 1989 Rule 115(7)**, all BS-IV and BS-VI compliant motor vehicles are issued a Pollution Under Control Certificate (PUCC) valid for **1 year (12 months)** from the date of issue.

---

### 3.4. OCR Data Corruption Fixes

- **ID 362:** The OCR process corrupted *"A school bus can be identified by... Creame yellow paint"* into *"Alcohol bus can be identified by... Cresine yellow paint"*. The entry was thoroughly sanitized and restored to its correct legal text and options.

---

## 4. Software Architecture & Deliverables

### 4.1. Corrected Dataset (`rto_question_bank_corrected.json`)
- Clean JSON schema containing 410 question objects.
- Attributes per item: `id`, `question`, `options` (array of strings), `correctAnswer` (0-indexed integer), `chapter` (e.g., *Rules*, *Cautionary*, *Police Related*), and `explanation` (including statutory citations).

### 4.2. Interactive Web Application (`index.html`)
A zero-dependency, production-grade frontend built with HTML5, Tailwind CSS, and vanilla JavaScript:
- **Study Mode:**
  - Full-text search with real-time filtering across questions, options, and explanations.
  - Category filters (*Traffic Rules, Signs, Police & Penalties*).
  - Dedicated **"Fixed & Audited"** view showing all corrected questions with distinct visual alert badges.
- **Mock Exam Mode:**
  - Simulates the actual RTO computerized test.
  - Generates 15 randomized questions per attempt.
  - Instant visual feedback on answer selection (emerald green for correct, rose red for incorrect).
  - Real-time scoring and official RTO pass/fail evaluation (Pass criterion: ≥ 11 out of 15).
  - Test retake functionality with reshuffled questions.

---

## 5. Repository & Version Control

- **GitHub Repository:** [https://github.com/rutujadhav22/Road_Safety_RTO](https://github.com/rutujadhav22/Road_Safety_RTO)
- **Branch:** `main`
- **Tracked Files:**
  - `index.html` — Interactive Web Application
  - `rto_question_bank_corrected.json` — Verified 410-Question Dataset
  - `README.md` — Project Overview and Audit Summary
  - `PROJECT_DOCUMENTATION.md` — Formal Technical and Audit Report

---

## 6. Conclusion & Impact

This project delivers both legal compliance and high-utility software engineering:
1. **Public Safety Impact:** Eliminates hazardous misconceptions regarding overtaking and traffic signs before new drivers hit the road.
2. **Educational Value:** Bridges the gap between outdated textbook question banks and current statutory law (MV Amendment Act 2019).
3. **Turnkey Solution:** Provides a plug-and-play, tested web interface and clean data layer ready for deployment across driving schools, educational platforms, and public awareness initiatives.
