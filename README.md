# Katamaran QA Technical Assignment: Tichi App

Welcome to the QA Technical Assignment submission for the **Tichi App**.

This repository contains professional Quality Assurance documentation, including a comprehensive test suite and a defect report for the Tichi mobile application.

---

## 📱 App Under Test: Tichi App
**Developer:** Albequu Solutions  
**App Type:** Commission-Free Mobile Service Marketplace  

### Core Features
- **Flexible Marketplace:** Allows users to post any requirement or opportunity without rigid category constraints.
- **Social Media Intelligence (SMI) Matching:** Uses an intelligent algorithm to analyze user requirements and match them with relevant, skilled service providers.
- **Direct Connections:** Enables clients and service providers to unlock contact details and chat in real-time.
- **Commission-Free Model:** Service providers keep 100% of their earnings. The platform charges a small fee only to unlock direct connections.
- **In-App Messaging & Reviews:** Seamless communication interface and reputation tracking through rating and feedback mechanisms.

---

## 📂 Repository Contents

### 1. [QA_Test_Cases.md](file:///C:/Users/Nijanth/.gemini/antigravity-ide/scratch/Katamaran-QA-Technical-Assignment/QA_Test_Cases.md)
A comprehensive test suite containing structural test cases mapped to the following critical modules:
- **Module 1: User Authentication & Profile Management**
- **Module 2: Requirement Posting & Marketplace Feed**
- **Module 3: SMI Match Engine & Notifications**
- **Module 4: Connection Fee Payments & Contact Unlocking**
- **Module 5: Real-time Chat & In-App Messaging**
- **Module 6: Review & Rating System**

Each test case includes a unique ID, description, pre-conditions, steps, expected results, priority, and severity level.

### 2. [Defect_Report.md](file:///C:/Users/Nijanth/.gemini/antigravity-ide/scratch/Katamaran-QA-Technical-Assignment/Defect_Report.md)
A defect report detailing simulated functional and cosmetic bugs found during application testing. Bugs are documented with:
- Unique Defect ID
- Title & Description
- Priority & Severity (Critical, Major, Medium, Minor)
- Detailed Steps to Reproduce
- Expected vs. Actual Results
- Environmental details (OS version, device model)

---

## 🧪 Testing Methodology
- **Functional Testing:** Verifying that all core user flows (posting, matching, paying, chatting) function exactly as specified.
- **Boundary Value Analysis (BVA):** Testing inputs at their edge limits (e.g., maximum character limits on descriptions, connection fees).
- **Compatibility Testing:** Validating performance and layout across Android and iOS versions.
- **Interrupt Testing:** Ensuring the app handles real-world scenarios such as incoming calls, network switches (Wi-Fi to mobile data), and background suspension.
