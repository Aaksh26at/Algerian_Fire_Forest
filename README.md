# FWI Prediction (Forest Weather Index) Web App

**Simple Flask app to predict Fire Weather Index (FWI)** using a pre-trained Ridge regression model and a StandardScaler.

---

## 🔎 Project Overview

This repository contains a Flask web application that accepts environmental inputs (temperature, relative humidity, wind speed, rain, FFMC, DMC, ISI, class, region) through a web form, scales them using a saved `StandardScaler`, and feeds them to a saved `ridge` model to return an FWI prediction.

> ⚠️ **Important:** The repository expects `models/ridge.pkl` and `models/scaler.pkl` to exist. These binary model files are **not** included in the repo by default (you must add them). The app will fail if those files are missing.

---

## 📁 Repository structure (suggested)

```
├── application.py          # Main Flask app
├── templates/
│   ├── index.html         # Home page / form page
│   └── home.html          # Result page (or same as index depending on your setup)
├── models/
│   ├── ridge.pkl          # Trained Ridge model (add this)
│   └── scaler.pkl         # Trained StandardScaler (add this)
├── data/
│   ├── Algerian_forest_fires_cleaned_dataset.csv
│   └── Algerian_forest_fires_dataset_UPDATE.csv
├── requirements.txt       # Python dependencies
└── README.md
```

---

## ✅ Prerequisites

* Python 3.8+ recommended
* Git (for version control and publishing)
* A saved model and scaler (`models/ridge.pkl`, `models/scaler.pkl`) created using scikit-learn

---

## 🛠️ Setup (local)

1. Clone the repo (if not already):

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

2. Create and activate a virtual environment (recommended):

```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Add the required model files:

* Create a folder named `models` at the project root.
* Place your `ridge.pkl` and `scaler.pkl` inside `models/`.

> Example files are not included for security and size reasons.

---

## ▶️ Run the app

```bash
python application.py
```

Open your browser and go to `http://127.0.0.1:5000/` to view the form. Enter numeric inputs and click **Predict**.

---

## 🧪 Example: cURL (submit a POST request)

If you want to test the predict endpoint directly (assuming it accepts form data):

```bash
curl -X POST http://127.0.0.1:5000/predictdata \
  -F "Temperature=25.0" \
  -F "rh=30.0" \
  -F "ws=3" \
  -F "rain=0" \
  -F "ffmc=90.0" \
  -F "dmc=6.0" \
  -F "isi=5.0" \
  -F "classes=1" \
  -F "region=1"
```

Response will be the rendered HTML page; for a JSON response you can modify the Flask route to `jsonify` the value.

---

## 🔒 Common issues & troubleshooting

* **`FileNotFoundError` for models**: Make sure `models/ridge.pkl` and `models/scaler.pkl` exist.
* **`TypeError: float() argument must be a string or a real number, not 'NoneType'`**: Ensure your HTML `name` attributes exactly match the keys used in `request.form.get(...)`. The app uses lowercase names in the example (e.g., `rh`, `ws`, `rain`, `ffmc`, `dmc`, `isi`, `classes`, `region`).
* **Missing templates**: `templates/index.html` and `templates/home.html` should exist; otherwise `render_template` will fail.

---

## 📤 How to publish this folder to GitHub (quick commands)

```bash
# 1. initialize git (if not done already)
git init

# 2. add all files
git add .

# 3. commit
git commit -m "Initial commit: FWI Prediction Flask app"

# 4. add remote (replace URL)
git remote add origin https://github.com/your-username/your-repo-name.git

# 5. push to GitHub
git branch -M main
git push -u origin main
```

---

## 📦 Deploying (optional)

You can deploy this Flask app to services like Heroku, Render, or Railway. Typical steps for Heroku:

1. Create `Procfile` with: `web: python application.py`
2. `pip freeze > requirements.txt` (already included)
3. `git push heroku main`

Each host has its own guide — check their docs.

---

## 📚 Dataset

The repository includes the Algerian forest fires CSV files in `data/` (if present). Use them for training or testing, but do not commit heavy or sensitive files if you want a small repo.

---

## 🧑‍💻 Contributing

If you want to improve the app (add validation, Dockerfile, CI/CD), feel free to open a PR.

---

## 📝 License

Choose a license (e.g., MIT) and add a `LICENSE` file if you want to make this repo open-source.

---

## 📬 Contact

If you need help, open an issue in this repo or reach out to the maintainer.

---

*Generated README — edit as needed before publishing.*
