# Hybrid Digital Twin (HDT) for Human-Centric PCB Assembly Optimization

This repository contains the complete data science and optimization pipeline for a **Hybrid Digital Twin (HDT)** framework applied to a Printed Circuit Board (PCB) assembly line. Built upon the **Industry 5.0 paradigm**, this framework moves beyond traditional automation by explicitly integrating human cognitive factors (fatigue and learning curves) directly into the manufacturing scheduling loop.

The project demonstrates a full implementation of **Predictive and Prescriptive Analytics**—transitioning from raw industrial data collection to explainable machine learning predictions, and finally to evolutionary optimization.

---

## 🎯 Framework Architecture & Pipeline

The pipeline is organized sequentially across four Jupyter Notebooks, tracking the lifecycle of the Digital Twin:

### 1. [Notebook 01: Product Twin - Preprocessing & EDA](./01_product_twin_eda.ipynb)
* **Focus:** Data Ingestion, Cleaning, and Exploratory Data Analysis.
* **Key Tasks:** Resolving data quality issues, handling missing values, and establishing initial feature correlations.
* **Outcome:** Engineering the categorical foundation for product complexity based on process cycle-time quantiles.

### 2. [Notebook 02: Human Twin - Feature Engineering](./02_human_twin_features.ipynb)
* **Focus:** Mathematical Modeling of Human Factors.
* **Key Tasks:** Implementing recursive mathematical formulations to capture **Dynamic Cognitive Fatigue ($F_t$)** and **Cumulative Experience ($E_t$)** based on production workload and sequence order.
* **Outcome:** Transforming static timestamp data into high-fidelity dynamic human-state features.

### 3. [Notebook 03: Human Twin - Predictive Performance Engine](./03_human_twin_predictive_engine.ipynb)
* **Focus:** Machine Learning & Explainable AI (XAI).
* **Key Tasks:** Training a non-linear **XGBoost Regressor** to forecast task durations (`total_time_sec`).
* **Optimization:** Utilized exhaustive hyperparameter tuning via **GridSearchCV** with **5-Fold Cross-Validation** to strictly eliminate overfitting risks. Implemented defensive checks to prevent Data Leakage.
* **Explainable AI:** Integrated the **SHAP (SHapley Additive exPlanations)** framework to open the "black box" of XGBoost, transparently quantifying feature importance and identifying critical fatigue tipping points ($F_t > 0.45$).
* **Model Evaluation Metrics:**
  * **R-squared ($R^2$) Score:** `0.818` (Explains ~82% of human performance variance)
  * **Mean Absolute Error (MAE):** `9.93 seconds`
  * **RMSE:** `12.70 seconds`

### 4. [Notebook 04: Process Twin - Intelligent Optimization & Scheduling](./04_process_twin_simulation.ipynb)
* **Focus:** Bio-Inspired Evolutionary Computing.
* **Key Tasks:** Developing an intelligent prescriptive scheduling engine using a **Genetic Algorithm (GA)**.
* **Mechanism:** Designed a custom permutation-based chromosome representation with **Order Crossover (OX)** and a strict **Fatigue-Penalized Fitness Function**.
* **Validation:** Simulated and benchmarked a full 30-PCB manufacturing shift comparing traditional **FIFO (First-In-First-Out)** sequencing against the **HDT-Optimized** sequence.
* **Industrial Outcome:** Successfully achieved **Peak Shaving** by reducing maximum operator fatigue from `0.639` to `0.536`, while simultaneously decreasing total makespan from `259.9s` to `251.2s` (a pure Win-Win for human well-being and plant throughput).

---

## 🚀 Key Visualizations & Industrial Insights

### 1. Global Feature Importance (SHAP Summary)
The SHAP framework proves the validity of our dynamic features:
* **PCB Complexity** acts as the primary driver of cycle time.
* **Dynamic Fatigue** systematically shifts model outputs in the positive direction (causing delays).
* **Accumulated Experience** shifts outputs in the negative direction, mathematically validating the **Learning Curve effect**.

### 2. Cognitive Fatigue Peak-Shaving (GA vs. FIFO)
The process shunts the traditional industry trade-off: by strategically weaving simpler tasks between highly complex PCBs when the operator approaches the cognitive limit ($0.45$), the system allows for real-time recovery without stalling line production.

---

## 🛠️ Installation & Dependencies

To execute this pipeline locally, clone the repository and install the required core packages:

```bash
git clone [https://github.com/YourUsername/industry5.0-hybrid-digital-twin.git](https://github.com/YourUsername/industry5.0-hybrid-digital-twin.git)
cd industry5.0-hybrid-digital-twin
pip install -r requirements.txt

Core Requirements:
python >= 3.8

xgboost

shap

scikit-learn

pandas

numpy

matplotlib

seaborn

joblib

🧠 Future Scope
Multi-Operator Line Balancing: Scaling the framework from an individual workstation to cooperative cellular lines.

Wearable IoT Feedback Loops: Integrating live biometric data (e.g., heart-rate variability, eye-tracking) directly into the dynamic fatigue state.

Deep Reinforcement Learning (DRL): Exploring continuous actor-critic models for stochastic, real-time disturbances.

Developed as a Master's Thesis Project in Data Science & Advanced Industrial Production Management.
