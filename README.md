# Dengue Early-Warning System

Predicts **ward-level dengue risk (Low / Medium / High / Critical) 2 to 4 weeks ahead** from multi-week lagged rainfall,
temperature, humidity and ward vulnerability, with a dashboard that shows the main weather drivers.

## Team
#Team name: ZeroTrace
| Member | Role |
|---|---|
| Saadman Aziz (Team Leader) | data and ML pipeline |
| Abdullah Al Tousif Habib | UI design and web |
| Aditya Dey | tests, doc preparation |

## Tech stack
Python 3.10+, pandas, NumPy, scikit-learn utilities, LightGBM, joblib, Streamlit, Altair, pytest.

## Quick start (under 3 minutes)
```bash
git clone <your-repo-url>
cd dengue-early-warning
python -m venv .venv
source .venv/bin/activate         
pip install -r requirements.txt
streamlit run app.py
```
The trained models are already in `models/`, so the app starts immediately at http://localhost:8501.

Optional commands:
```bash
python -m src.train       
python -m src.benchmark   
pytest -q                
```

## What is in the repo
- `src/features.py`: per-`ward_id` multi-week lag and rolling features (rainfall lags 0-8 weeks, sums, temperature, humidity, ward vulnerability, season).
- `src/train.py`: chronological split (train 2016-22, validation 2023, test 2024-25), LightGBM per horizon, baselines, ablation, conformal intervals.
- `src/predict.py`, `src/tiers.py`: cached inference, risk tiers, driver explanations.
- `app.py`: dashboard (ward forecast with drivers, city overview, ward heatmap, validation and error panel, efficiency panel).
- `ARCHITECTURE.md`: data-flow diagram, split logic, model rationale, cost controls.
- `data/dengue_dataset.csv`: the provided competition dataset (unmodified).

## Results (test period 2024-2025, never used for fitting)
MAE 1.00 / 1.03 / 1.25 cases per ward-week at 2 / 3 / 4 weeks ahead, versus 3.10 for the ward-average baseline.
Tier accuracy 82-85%. See `ARCHITECTURE.md` and the dashboard's Model validation tab.

## Demo
- Run locally with the commands above.

## AI tools and APIs disclosure

| Tool / API | Used for |
|---|---|
| Claude (Anthropic) | Planning the approach and generating first drafts of the pipeline, training script, dashboard, tests and documentation in this repository; reviewed and edited by the team |
| (ChatGPT, Copilot, Gemini) | (Basic understanding) |
| External APIs at runtime | None. The app makes no API or LLM calls. |

## Attributions
No third-party code snippets were copied. Open-source libraries used under their own licenses: pandas, NumPy, scikit-learn, LightGBM, joblib, Streamlit, Altair, pytest.
