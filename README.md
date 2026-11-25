# FinAlliance

FinAlliance is a federated fraud-detection platform prototype that combines a transaction/fraud monitoring dashboard with federated learning workflows for collaborative model training across banks.

## Repository Structure

- `app.py` — Flask API server for transactions, fraud alerts, prediction, federated status, and SSE-based training endpoints.
- `src/` — Core ML/federated learning modules (models, client/server logic, aggregation, privacy/DP utilities).
- `backend/` — FastAPI backend variant with auth, transaction, fraud, federated, and trainer routes.
- `frontend-next/` — Next.js dashboard/frontend.
- `data/dataset/` — Dataset directory. The full `creditcard.csv` is ignored; `creditcard_sample.csv` is tracked.
- `demo/` — Demo dataset and training code.
- `show_results.py` — Utility for printing recent federated training results from `results/`.

## Features

- Transaction listing and high-risk fraud alert APIs.
- Fraud prediction endpoint with risk-level classification.
- Federated learning simulation endpoints (status, model update submission, global model download).
- SSE training endpoints for baseline and federated training runs.
- Next.js dashboard for monitoring transactions, alerts, and federated learning status.
- FastAPI backend with modular routes/services for auth, fraud prediction, aggregation, and trainer workflows.

## Tech Stack

- **Frontend:** Next.js 16, React 19, TypeScript, Tailwind CSS, Axios, Framer Motion
- **Flask API:** Flask, Flask-CORS, Gunicorn
- **FastAPI Backend:** FastAPI, Uvicorn, SQLAlchemy, Pydantic, scikit-learn, pandas
- **ML/FL:** PyTorch-based federated learning modules in `src/`

## Getting Started

### Prerequisites

- Python 3.10+
- Node.js 20+
- npm

### 1. Clone the repository

```bash
git clone https://github.com/YuganshS/FinAlliance.git
cd FinAlliance
```

### 2. Run the Flask API (root)

This server powers the main `/api/*` endpoints used by the frontend.

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Flask API runs at `http://localhost:5000`.

### 3. Run the Next.js frontend

```bash
cd frontend-next
npm install
npm run dev
```

Frontend runs at `http://localhost:3000`.

Set the API base URL if needed:

```bash
# frontend-next/.env.local
NEXT_PUBLIC_API_URL=http://localhost:5000
```

### 4. Run the FastAPI backend (optional/alternate backend)

```bash
cd backend
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

FastAPI docs: `http://localhost:8000/api/docs`

## Key API Endpoints (Flask)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/status` | Health/status check |
| GET | `/api/transactions/all` | Fetch sample transactions |
| GET | `/api/fraud/high-risk` | Fetch high-risk flagged transactions |
| POST | `/api/fraud/predict` | Predict fraud risk for a transaction |
| GET | `/api/federated/status` | Federated learning status |
| POST | `/api/train/baseline` | Train baseline model (SSE stream) |
| POST | `/api/train/federated` | Train federated model (SSE stream) |
| POST | `/api/federated/send-update` | Simulate encrypted model update submission |
| GET | `/api/federated/download-model` | Download simulated global model |

## Dataset

- The app uses `data/dataset/creditcard.csv` when available, otherwise falls back to `data/dataset/creditcard_sample.csv`.
- Full dataset files are ignored by git; keep large/local datasets out of commits.

## Development Notes

- `frontend-next` is configured with static export (`output: "export"`).
- The Flask app can optionally download a full dataset at startup if `DATASET_URL` is set.
- Review `TODO.md` and `flask_log.txt` for local development context and known task history.

## License

Add a license file if you plan to distribute this project publicly.
