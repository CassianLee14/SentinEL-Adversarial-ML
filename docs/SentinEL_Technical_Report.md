# SentinEL Technical Report
## Adversarial Robustness Analysis of ML-Based Phishing Detection

**Authors:** Mourya Reddy Udumula (ML Architecture, Adversarial Research, Explainability)
**Collaborator:** Jeet Upadhyaya Anand (Operational Pipeline)
**Institution:** Indrashil University, B.Tech CSE Capstone Project (Jan-May 2025)
**Presented at:** Indrashil University Annual Research Symposium 2025

---

## 1. Research Objective

This project investigates the adversarial robustness of machine learning-based phishing URL
detectors. Specifically, we quantify how homoglyph substitution attacks (replacing Latin
characters with visually identical Cyrillic Unicode equivalents) degrade classifier accuracy,
and evaluate the trade-offs between explainability methods in a security operations context.

## 2. Dataset

- Source: PhishTank (phishing URLs) and curated legitimate URL corpus
- Size: 11,000 URLs (5,500 phishing, 5,500 legitimate)
- Split: 80% training (8,800), 20% test (2,200)
- Features: 17 URL-derived features (entropy, length, TLD risk, subdomain count, etc.)

## 3. Baseline Model Performance

- Algorithm: Random Forest Classifier (100 estimators, max_depth=None)
- Clean accuracy: 97.2% on 2,200-URL test set
- Precision: 0.97 | Recall: 0.97 | F1: 0.97

## 4. Adversarial Attack Methodology

- Attack type: Homoglyph substitution (Unicode confusable characters)
- Substitution map: 19 Latin-to-Cyrillic character pairs (a, e, o, etc.)
- Attack scope: Applied to URL domain and path components only (scheme left as ASCII)
- Attack rate: 100% of test set URLs subjected to substitution

## 5. Adversarial Evaluation Results

- Attacked accuracy: 81.4% (degradation: 15.8 percentage points)
- Feature sensitivity analysis: Entropy, keyword frequency, and TLD features
  showed sensitivity to homoglyph substitution on the full 11,000-row corpus
- Note on demo dataset: The 14-row demo dataset included in this repository
  is too small to reproduce the 15.8pp degradation. attack_rate=1.0 confirms
  the attack pipeline executes correctly.

## 6. Explainability Benchmarks

Method                      | Latency   | Ratio vs Baseline | SOC Suitability
----------------------------|-----------|-------------------|-----------------
Gini Impurity (native)      | less than 2ms | 1x baseline   | Real-time
SHAP TreeExplainer          | ~0.23ms   | ~1,600x Gini      | Real-time
LIME TabularExplainer       | ~130ms    | ~870,000x Gini    | Too slow for SOC

**Finding:** Gini impurity attribution meets SOC real-time requirements (less than 2ms)
while SHAP provides richer explanations within acceptable latency. LIME is
unsuitable for real-time threat operations at this scale.

## 7. Limitations

- Demo dataset (14 rows) cannot reproduce full research results
- Homoglyph attack sensitivity depends on byte-length features (UTF-8 encoding artefact)
- Model trained and evaluated on a single dataset split -- cross-validation not performed
- Attack scope limited to homoglyph substitution; other adversarial techniques not evaluated

## 8. Reproduction

Run `python experiments/baseline_eval.py` to train the baseline model.
Run `python experiments/adversarial_eval.py` to reproduce the attack evaluation.
Run `python experiments/explainability_bench.py` to reproduce the explainability benchmarks.
All results saved to `experiments/results_*.json`.
