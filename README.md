AI-Powered Smart EMR (Electronic Medical Records)

 An AI-powered EMR system that not only stores patient records but actively helps doctors by summarizing history, detecting trends, and providing decision-support alerts.

 Problem Statement

Most existing EMRs are clunky, slow, and passive — they store data but don’t help doctors quickly understand patient history or detect early warning signals. This slows down diagnosis and increases workload.
Our system solves this by making EMRs intelligent:

Summarizes patient history in seconds

Detects long-term health trends

Provides severity and risk alerts

Helps doctors save time and improve patient outcomes

 How It Works

The system integrates three datasets and two ML pipelines:

EMR Snapshot Dataset

One row per patient with latest vitals, labs, demographics.

ML Model: Severity Regression (Gradient Boosting Regressor) → predicts severity score (0–10) and classifies into Low/Moderate/High.

EMR History Dataset

Five-week longitudinal vitals per patient.

ML Model: Trend Classifier (HistGradientBoostingClassifier) → predicts health trend (Improving / Stable / Worsening).

Doctor Records Dataset

Doctor’s notes + patient feedback linked to each patient.

Future integration with LLMs (ChatGPT/OpenAI) to convert notes into insights and summaries.

Fusion Layer

Outputs from snapshot + history + doctor records are fused into a JSON object per patient:

{
  "patient_id": "123",
  "timestamp": "2025-09-18T12:00:00Z",
  "snapshot": {
    "severity_score": 6.8,
    "severity_class": "Moderate"
  },
  "history": {
    "trend_label": "Worsening",
    "probs": {"Improving": 0.1, "Stable": 0.2, "Worsening": 0.7}
  },
  "derived": {
    "risk_score": 0.82,
    "alerts": ["Blood pressure rising", "Glucose unstable"],
    "rationales": ["Trend worsening over 5 weeks", "Snapshot severity moderate-high"]
  }
}


This JSON can then be fed into an LLM for natural language summarization for doctors.

Setup & Usage

Clone the repo:

git clone https://github.com/yourusername/smart-emr.git
cd smart-emr


Install dependencies:

pip install -r requirements.txt


Run ML pipelines:

python train_snapshot.py
python train_history.py
python fusion_pipeline.py


Output JSON files will appear in /outputs and can be passed into an LLM.

 Example Outputs

Severity Score: 7.2 (High Risk)

Health Trend: Worsening

Alerts: Blood sugar increasing, Oxygen saturation dropping

 Future Work

Integrate with real-world EHR datasets (MIMIC-III, PhysioNet).

Deploy as a web-based doctor dashboard.

Enable ChatGPT/LLM integration for natural summaries.

Add reinforcement learning to improve alerts with doctor feedback.

 Tech Stack

Python, Scikit-learn, Pandas, Numpy

Imbalanced-learn (oversampling)

OpenAI API / ChatGPT for summaries

JSON fusion outputs

 License

MIT License – free to use and modify.
