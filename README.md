# HealthGuard Insights – Risk Prediction

Combines the **Transformer-based risk prediction model** (Python) with the **HealthGuard Insights** frontend (React).

## How to Run in VS Code

### 1. Start the Python API (Backend)

Open a terminal in VS Code (`Ctrl+``) and run:

```powershell
cd c:\Users\KISHOR\proj
pip install -r api\requirements.txt
python api\app.py
```

The API starts on **http://localhost:5000**. On first run it will train the model (may take ~1 minute), then serve predictions.

### 2. Start the Frontend

Open a **second** terminal and run:

```powershell
cd c:\Users\KISHOR\proj\healthguard-insights
npm install
npm run dev
```

The app runs at **http://localhost:8080**.

### 3. Use the App

1. Open http://localhost:8080 in your browser  
2. Go to **Predict** (sidebar)  
3. Enter patient data and click **Predict Risk Level**  
4. View risk prediction (Low / Moderate / High) from the Transformer model  

---

## Project Structure

```
proj/
├── api/
│   ├── app.py              # Flask API – loads model, serves /predict
│   └── requirements.txt    # Python dependencies
├── healthguard-insights/   # React frontend (Vite, Tailwind)
│   └── src/
│       └── pages/
│           └── Predict.tsx # Risk prediction page (calls API)
├── risk_prediction_transformer.py  # Transformer model + training
├── model_state.pt          # Saved model (created after first API run)
├── encoders.json           # Categorical encoders (created after first API run)
└── synthetic_risk_data_transformer.csv  # Dataset (created if missing)
```

## Training the Model Standalone (Optional)

To train and save the model without starting the API:

```powershell
python risk_prediction_transformer.py
```

This runs training, evaluation, and saves `model_state.pt` and `encoders.json`. The API will use these files on next start.
