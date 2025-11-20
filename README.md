# Probabilistic Strong Bimodal Branch Predictor

## Overview
This project implements a modified **bimodal branch predictor** for the O3 CPU that enhances the traditional design by introducing a **controlled probabilistic mechanism** in low-confidence states. The goal is to improve branch prediction behavior while keeping the predictor simple and hardware-friendly.

---

## What I Did

I modified the classic bimodal predictor in the following ways:

1. **Upgraded Counter Size**
   - Used a 3-bit saturating counter (0–7) instead of the traditional 2-bit counter.
   - This provides finer confidence tracking for each branch.

2. **Controlled Probabilistic Prediction**
   - Normal prediction is done using the counter value threshold.
   - When the counter is in a low-confidence state (middle value), a small probability is used to flip the prediction.
   - This probabilistic behavior is only applied when:
     ```
     counter == MAX_COUNTER / 2
     ```
     which represents an uncertain state.

3. **Standard Learning Mechanism**
   - After the actual branch outcome is known, the counter is updated using the usual saturating increment/decrement strategy.

---

## Prediction Logic

- Prediction rule:
- If counter ≥ 4 → predict Taken
- If counter < 4 → predict Not Taken

- If counter == 3 (low confidence):
- A random number is generated.
- With 1% probability, the prediction is flipped.

This keeps predictions stable for strong branches while adding adaptability for unstable ones.

---

## Key Features

- Strong bimodal base prediction
- 3-bit saturating counter (0–7)
- Probabilistic flip only in uncertain state
- Low hardware complexity
- Maintains high prediction accuracy



- Each branch instruction is mapped to an entry in a table using:
