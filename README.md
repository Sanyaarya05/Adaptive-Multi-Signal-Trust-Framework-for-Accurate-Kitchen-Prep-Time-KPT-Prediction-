🍽️ Adaptive Multi-Signal Trust Framework for KPT Prediction

Zomathon 2026 — Problem Statement 1 | Team: The Zomatechs

Adaptive KPT Prediction Framework that corrects noisy merchant signals using rider arrival data and error-based feedback loops. Detects and fixes marking biases (LPEM & EPLM) via confidence-weighted overrides. Includes a gamified merchant trust-scoring system to improve signal reliability at scale.

📌 Problem
Zomato's Kitchen Prep Time (KPT) prediction relies on merchant-marked "Food Order Ready" events — which are frequently inaccurate due to human bias and manipulation. This leads to:

🚴 Increased rider waiting time
📉 ETA fluctuations (P50/P90 errors)
❌ Higher order delays and cancellations


Core Insight: The problem isn't model capability — it's signal reliability.


💡 Solution
We shift the focus from model optimization → signal trust optimization using rider arrival time as a ground-truth proxy for real kitchen rush.
Core Formula
KPT_new = KPT₀ + (α × E)

where:
  E = W - B  (Rider Wait Time - Target Buffer)
  α = Learning rate (0.1 to 0.5)
Smoothing Function
KPT_final = (1 - β) × KPT_old + (β × KPT_new)
Dead Zone Band (Stability Control)
W < 3 min  →  Decrease KPT
W > 5 min  →  Increase KPT
3 ≤ W ≤ 5  →  No change  ✅

🔍 Bias Detection & Correction
Case 1 — LPEM (Late Prepared, Early Marked)
Merchant falsely marks food as ready before it actually is.

Detection: High gap between rider arrival and actual dispatch time
Fix: Discard merchant timestamp; use actual dispatch time as true P
Penalty: Repeated offenders get inputs deprioritized by the algorithm

Case 2 — EPLM (Early Prepared, Late Marked)
Food is ready but merchant delays marking it (often until rider arrives).

Fix: Adaptive KPT reduction auto-converges to true prep time limit
Prevention: Gamified trust-score incentive system encourages real-time logging


🏆 Merchant Trust Scoring
CategoryTrust LevelSystem Action✅ Usually On-TimeHighManual inputs fully trusted🟡 Usually EarlyMediumModerate scrutiny applied🔴 Usually LateLowInputs deprioritized

🔄 Closed-Loop System
Incentivize  →  Detect  →  Correct  →  Improve
The system is fully self-regulating — merchants cannot game it, and behavior gradually aligns with reality over time.

📊 Simulation & Validation
Python-based simulation (Google Colab) across 50 orders demonstrating:

Rider waiting time fluctuation around the 4-min target buffer
Error (W - B) convergence over time
Progressive KPT stabilization from ~20 min → ~17.5 min

Tech Stack
- Python (Simulation & Validation)
- Google Colab
- Matplotlib (Visualization)

Team
**The Zomatechs** — Sanya Arya, Manas Dhamija
