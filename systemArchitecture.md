# Relapse Velocity Monitor (RVM) - System Architecture

The **Relapse Velocity Monitor (RVM)** detects and anticipates emotional shifts by analyzing subtle behavioral and physiological trends. It integrates **data ingestion, feature extraction, and predictive analysis** within a modular, privacy-conscious framework to provide **proactive, personalized self-care insights**.

---

## 1. High-Level System Components

The RVM utilizes a **three-tier cloud-native architecture** for scalability, personalization, and data security.

### 1.1. Mobile App Frontend
- **Purpose:** User interface for mood logging, habit tracking, and displaying Proactive Nudges and the Relapse Velocity graph.
- **Technology:** Cross-platform framework (e.g., React Native or Flutter) for iOS and Android.
- **Data Handling:** Initial encryption and local storage of non-critical configuration data.

### 1.2. Cloud Backend & API Layer
- **Purpose:** Central gateway for authentication, data transmission, and routing requests to the Analytical Engine.
- **Technology:** Cloud-hosted serverless functions (e.g., AWS Lambda, Google Cloud Functions) or containerized apps (Docker/Kubernetes). Uses **Python** for ML execution and **Node.js** or **Java** for API routing.

### 1.3. Data Layer (Persistence)
- **Purpose:** Secure storage of time-series data, personalized baselines, and aggregated analytical trends.
- **Technology:** Scalable NoSQL database (e.g., MongoDB, DynamoDB) for flexible user logs and **encrypted object storage** (e.g., AWS S3) for individual ML baselines.

### 1.4. Notification Service
- **Purpose:** Pushes context-aware Proactive Nudges to the user’s device in real-time.
- **Technology:** Push notification services (e.g., Firebase Cloud Messaging, Apple Push Notification Service).

---

## 2. RVM Layered Architecture (Processing Flow)

### 2.1. Data Ingestion Layer
- **Function:** Collects multi-source inputs such as mood logs, sleep quality, activity levels, and menstrual cycle data.
- **Input Sources:** User entries via the Mobile App and potential external API integrations (e.g., wearable devices).
- **Data Handling:** All data is anonymized and encrypted **client-side** before transmission and storage.

### 2.2. Processing Layer
- **Preprocessing:** Cleans, normalizes, and timestamps incoming data.
- **Feature Extraction:** Quantifies behavioral stability and identifies deviations over time, such as:
  - Sleep variability over 7 days  
  - Activity drop-off  

### 2.3. Analytical Layer (Scoring Engine)
- **Purpose:** Computes the **Relapse Velocity Score (RVS)**, a dynamic indicator of emotional fluctuation.
- **Personalization:** Models learn from individual baselines, not global averages.

**Relapse Velocity Scoring Engine:**

The **RVS** quantifies the rate of shift toward an emotional risk zone. It focuses on deviations from an individual’s baseline, weighted by behavioral importance and cycle proximity.  

<img width="697" height="81" alt="Screenshot 2025-11-08 143609" src="https://github.com/user-attachments/assets/21977a68-4e99-4ed0-ba8e-9f47ce00e509" />


**Where:**
- `Δ Behavior_i` = Time-series deviation in micro-relapse metrics (sleep, activity) from rolling baseline  
- `W_i` = Weight of that behavior, adjusted by ML based on historical reactivity  
- `CycleProximity` = Factor based on current day relative to sensitive premenstrual phase  
- `W_c` = Weight increased during high-risk periods

### 2.4. Insight & Feedback Layer
- **Threshold:** When RVS crosses a sustained 75% threshold (or personalized adaptive value), the Notification Service is triggered.  
- **Nudge Generation:** Provides supportive, compassionate messages tailored to current deviations and cycle phase, avoiding clinical or alarming language.

---

## 3. Guiding Principles
- **Personalization:** Emphasis on **N-of-1 models** (individual baselines).  
- **Privacy & Security:** End-to-end encryption for all user data.  
- **Interpretability:** Outputs focus on gentle nudges and self-care guidance, maintaining transparency and user control.
