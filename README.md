# Insurance ML Web App (Flask + PyCaret)

## Summary
A lightweight web application that serves a pre-trained **insurance ML pipeline** via **Flask**. The app loads a serialized model (`insurance_pipeline.pkl`) and returns predictions from a simple web form, enabling quick “what-if” analysis without notebooks or IDEs.

## Goal
- Put a trained model behind a clean, minimal UI for **fast, self-serve predictions**.
- Demonstrate an **end-to-end path**: train → serialize → serve via API/UI → (optionally) deploy to a cloud host.

## Procedure
1. **Modeling (offline)**
   - Prepare data, select algorithms, and tune using **PyCaret**.
   - Export the best pipeline as `insurance_pipeline.pkl`.
2. **Serving (app)**
   - Build a **Flask** app with routes for home (form) and predict (POST).
   - Load the pipeline at startup and validate inputs server-side.
3. **UI**
   - Simple HTML form styled with `style.css` for a clean, single-page experience.
4. **Deployment (optional)**
   - Add a production server command (e.g., `gunicorn app:app`) and a `Procfile` for platforms like Heroku.

## Result
- **Functional web app** that accepts user inputs and returns immediate predictions.
- **Reproducible pipeline** (single `.pkl`) decoupled from training code, making it easy to swap models as they improve.
- **Low friction UX**: single page, clear inputs, instant feedback.

> _Tip:_ Include your latest model scorecard here (e.g., MAE/RMSE for regression or AUC/F1 for classification) so readers see objective performance.

## Business Impact
- **Faster decision support:** Business users can simulate scenarios (e.g., customer attributes) and see risk/premium estimates in seconds.
- **Operational efficiency:** Reduces analyst time spent running ad-hoc predictions.
- **Model adoption:** A clickable UI helps stakeholders trust and iterate on the model.

## Next Steps to Make It Better
- **Input validation & tooltips:** Add ranges, examples, and inline checks.
- **Monitoring:** Log inputs/predictions for drift and add a simple health endpoint.
- **Versioning:** Store model metadata (training date, features, metrics) and expose it in an “About Model” panel.
- **Explainability:** Add SHAP/feature importance summaries for each prediction.
- **Batch mode / API:** Provide a `/predict_json` endpoint and a CSV upload flow.
- **CI/CD:** Tests for schema, serialization, and a smoke test that loads the pipeline and runs one prediction.

## Tech Stack
- **Modeling:** PyCaret  
- **Serving:** Flask  
- **UI:** HTML/CSS (`style.css`)

## Project Structure (suggested)
```

.
├── app.py                  # Flask app (routes + model loading)
├── insurance\_pipeline.pkl  # serialized PyCaret pipeline
├── requirements.txt        # minimal deps (Flask, PyCaret)
├── static/
│   └── style.css           # page styles
└── README.md

````

## Quickstart
```bash
# 1) Create environment
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 2) Install dependencies
pip install -r requirements.txt

# 3) Run locally
export FLASK_APP=app.py            # Windows (PowerShell): $env:FLASK_APP="app.py"
flask run                          # then open http://127.0.0.1:5000/

# (Optional) Production
# pip install gunicorn
# gunicorn app:app --bind 0.0.0.0:8000
````

## Notes

* Keep the training notebook/code outside the app; only the **pipeline artifact** is required at runtime.
* If you retrain the model, **overwrite `insurance_pipeline.pkl`** and restart the app—no code changes needed.


