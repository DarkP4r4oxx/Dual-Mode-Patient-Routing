PROJECT SYNOPSIS
Project Title: Dual Mode Patient Routing System
Domain: Edge Computing, IoT, and Web Development
University: Savitribai Phule Pune University (SPPU)
Academic Year: Third Year (6th Semester)
Branch: Electronics and Computer Engineering


1. Introduction
Public healthcare infrastructure in India manages thousands of walk-in Outpatient Department (OPD) patients daily. Traditional queue management systems rely on sequential static tokens and active internet connectivity. However, these systems often fail in ground-reality scenarios: static tokens cause patient disputes when triage algorithms reorder the queue, and cloud-reliant systems fail in hospital corridors characterized by thick concrete walls and internet dead zones.
The Dual Mode Patient Routing System is a Cloud-Edge Hybrid architecture designed to physically de-crowd hospital waiting areas. It integrates a cloud-hosted online booking website (using Supabase Backend-as-a-Service) with an offline-first local network (ESP32 Captive Portal) deployed at the hospital. The system replaces static tokens with dynamic Estimated Wait Times (EWT) and utilizes a Consultation-Duration (Shortest Job First) algorithm to maintain continuous patient flow without overlapping with emergency casualty protocols.

3. Problem Statement
Existing hospital queuing systems suffer from three critical socio-technical flaws:
Queue Chaos: Assigning visible, static priority tokens (e.g., Token #12) causes patient disputes and anxiety when the line is dynamically reordered by administrative staff or triage algorithms.
Flawed Triage Logic: Attempting to sort OPD patients by "medical severity" is redundant, as life-threatening cases are handled by Emergency/Casualty wards. The actual OPD bottleneck is the mixing of high-duration "New Diagnoses" (20 mins) with low-duration "Report Checking" consultations (2 mins).
Infrastructure Dependency: Display-board systems force crowds to wait in unventilated corridors to track their numbers, and mobile-app solutions fail due to a lack of 4G/5G connectivity inside hospital buildings.


5. Literature Survey Summary
A review of recent hospital queuing systems reveals a heavy reliance on either purely local static token dispensers or heavily cloud-dependent Machine Learning predictive models. While systems using Accumulated Priority Queuing (APQ) successfully sort patients, they create on-ground friction by displacing patients' visual queue numbers. Existing IoT-based systems require users to download APKs or navigate to specific URLs using mobile data. There is a distinct gap in utilizing connectionless Edge computing (Captive Portals) combined with duration-based sorting to physically disperse walk-in crowds in resource-constrained environments.


7. Objectives
To develop a Dual Mode architecture that seamlessly syncs online home-booked appointments (Cloud) with offline walk-in registrations (Edge).
To design an Offline-First Captive Portal using an ESP32 microcontroller, allowing patients to check their queue status via a local intranet without requiring mobile data or app downloads.
To implement a Shortest Job First (SJF) algorithmic variant that segregates patients based on consultation type (New Checkup vs. Showing Reports) to optimize doctor clearance rates.
To actively de-crowd the waiting area by replacing static token numbers with Uber-style dynamic Estimated Wait Times (EWT).


9. Proposed System Architecture
The framework operates on a dual-node architecture combining Backend-as-a-Service with localized Edge routing.

The Cloud Node (Online Platform): A web application hosted on the internet, allowing patients to book appointments from home. Data and authentication are securely managed using Supabase.
The Edge Node (Hospital Intranet): * Data Sync: At the start of the OPD session, a local server (running on the doctor's workstation) fetches the online appointments from the Supabase cloud.
Captive Portal (ESP32): An ESP32 microcontroller acts as a local DNS server and Access Point (SoftAP). When walk-in patients connect, an offline HTML/CSS form automatically pops up on their smartphone, gathering registration details.

Doctor's UI Dashboard: A native web dashboard running locally features a clean Material UI and Glassmorphism design, displaying the algorithmically sorted patient list in real-time.

11. Methodology & Algorithms
The core intelligence of the system lies in its sorting and estimation algorithms, processed entirely on the local edge server to bypass internet latency:
Consultation-Type Triage (Modified SJF): Instead of First-Come-First-Serve, the algorithm interleaves tasks. For every two high-duration tasks ("New Checkup"), the system routes one low-duration task ("Showing Reports").

Dynamic EWT Calculation: The system calculates the ETA for each patient based on the doctor's real-time clearance rate. If a patient is pushed down the queue, their timer smoothly adjusts, eliminating the psychological friction of losing a static queue position.

13. Hardware and Software Requirements
Hardware Specs:
ESP32 Development Board (Wi-Fi Microcontroller for SoftAP and Captive Portal)
5V Portable Power Source / Power Bank
Local Processing Unit (Standard PC/Laptop for local server hosting)
Software & Tech Stack:
Frontend UI: React.js / Next.js (utilizing Material UI components and pure CSS Glassmorphism styling).
Cloud Backend: Supabase (PostgreSQL database and REST APIs for online booking).
Local Backend Server: Node.js (Express framework) with SQLite (for offline hospital data management).
Microcontroller Firmware: C/C++ (Arduino IDE for DNS hijacking and WebServer hosting).

15. Advantages and Applications
Advantages:
Functions seamlessly in internet dead zones.
Zero friction for users (No app installation required).
Eliminates patient disputes through blind EWT tokens.
Highly cost-effective (Requires only a single ESP32 node per waiting room).
Applications:
Government and Municipal Hospitals.
Large-scale free medical camps in rural areas.
Busy private clinics with high daily footfalls.

17. Expected Outcomes and Future Scope
The successful deployment of the Dual Mode Patient Routing System will result in an internet-independent, conflict-free patient management system. It will physically disperse crowds from infectious hospital corridors by notifying them locally when their EWT reaches a minimum threshold.
Future Scope: Integration with local pharmacy inventory to notify patients if their prescribed medicines are available at the in-house medical store before they leave the premises.

