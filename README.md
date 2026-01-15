# 🛡️ SentinEL: Ultima Intelligence Engine
**SecOps Lead:** Jeet Anand Upadhyaya | **Architect:** Mourya Reddy Udumula

---

## 📦 Operational Triage & Threat Intelligence
My primary contribution to SentinEL was architecting the **High-Velocity Triage Pipeline** and the **Incident Response Layer**:

1. **High-Velocity Ingestion**: Utilized Python `ThreadPoolExecutor` to parallelize the processing of threat feeds, achieving a **5x reduction in batch processing latency**.
2. **Active Learning Feedback**: Implemented a session-persistent **Manual Override** mechanism, allowing SOC analysts to mitigate False Positives in real-time.
3. **Robust Ingestion Engine**: Developed a fail-safe CSV parser capable of auto-detecting URL columns in "dirty" or headerless threat intel feeds.
4. **Actionable XAI**: Integrated an attribution panel that translates ML probability into forensic justifications (e.g., SSL age, TLD reputation) for rapid auditing.

## 📊 Operational Evidence
![Triage Dashboard](assets/triage_dashboard.png)
*Figure 1: Automated Triage Dashboard showing concurrent IOC processing and distribution.*

![Audit Compliance](assets/audit_compliance.png)
*Figure 2: System Audit Logs providing a transparent trail of all diagnostic actions.*

## 📂 Responsibility Matrix
| Module | Lead Author | Primary Responsibility |
| :--- | :--- | :--- |
| `app.py` (Tab 2) | **Jeet Upadhyaya** | Triage Pipeline & Operational UX |
| `app.py` (Logging) | **Jeet Upadhyaya** | Forensic Audit Ledger |
| `ml_engine.py` | Mourya Udumula | Random Forest & XAI Attribution Core |
| `feature_extractor.py`| Mourya Udumula | 16-Dimensional Forensic Vectorization |

## 🔧 Installation
```bash
git clone https://github.com/CassianLee14/SentinEL-Adversarial-ML.git
pip install -r requirements.txt
streamlit run app.py
