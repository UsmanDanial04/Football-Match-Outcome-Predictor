# ⚽ Football Match Outcome Predictor

A machine learning project that predicts the outcome of a football match — **Home Win**, **Away Win**, or **Draw** — using a Random Forest Classifier, served via a Flask API and connected to an interactive web UI.

<br>

## 👤 Author

**Usman Danial**
[![GitHub](https://img.shields.io/badge/GitHub-UsmanDanial04-181717?style=flat&logo=github)](https://github.com/UsmanDanial04)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-usman--danial-0A66C2?style=flat&logo=linkedin)](https://www.linkedin.com/in/usman-danial-b4568b289)

<br>

## 📁 Project Structure

```
football-match-predictor/
│
├── football_match_dataset.csv        # Dataset with match scores and outcomes
├── Football_Match_Predictor.ipynb    # Jupyter notebook (EDA + training + Flask API)
└── football_predictor.html           # Interactive web UI
```

<br>

## 🧠 How It Works

```
User enters scores (HTML UI)
        ↓
  POST /predict → ngrok tunnel
        ↓
  Flask API (running in Colab)
        ↓
  Trained Random Forest model
        ↓
  Returns: outcome label + probabilities
        ↓
  UI displays result with confidence bars
```

<br>

## 📊 Dataset

| Column       | Description                          |
|--------------|--------------------------------------|
| `home_team`  | Name of the home team                |
| `away_team`  | Name of the away team                |
| `home_score` | Goals scored by the home team        |
| `away_score` | Goals scored by the away team        |
| `tournament` | Type of match (Friendly, Qualifier…) |
| `result`     | Match outcome (Home Win / Away Win / Draw) |

<br>

## 🔬 Notebook Walkthrough

| Section | Description |
|---------|-------------|
| 1. Imports & Setup | Libraries, plot styling, global constants |
| 2. Load & Explore Data | Shape, info, missing values, statistics |
| 3. Feature Engineering | Derive `result` column from score comparison |
| 4. Data Visualization | Outcome distribution, score histogram, scatter plot |
| 5. Train / Test Split | 80/20 split with `random_state=42` |
| 6. Model Training | `RandomForestClassifier` with 100 trees |
| 7. Model Evaluation | Accuracy, classification report, confusion matrix, feature importances |
| 8. Predict a Match | Single match prediction with probability breakdown |

<br>

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/UsmanDanial04/football-match-predictor.git
cd football-match-predictor
```

### 2. Open the notebook in Google Colab

Upload `Football_Match_Predictor.ipynb` and `football_match_dataset.csv` to Colab, then run all cells top to bottom.

### 3. Install dependencies

The notebook installs everything needed. For local use:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn flask flask-cors pyngrok
```

### 4. Start the Flask API

Run the final cell in the notebook. It starts a Flask server and exposes it via ngrok:

```python
from pyngrok import ngrok
ngrok.set_auth_token("YOUR_NGROK_TOKEN")  # get free token at ngrok.com
public_url = ngrok.connect(5000).public_url
print(f"API live at: {public_url}/predict")
```

### 5. Connect the web UI

Open `football_predictor.html` in a text editor and paste your ngrok URL:

```javascript
const API_URL = "https://your-url.ngrok-free.app/predict";
```

Save and open in any browser — the UI is now connected to your live model.

<br>

## 🌐 API Reference

**Endpoint:** `POST /predict`

**Request body:**
```json
{
  "home_score": 2,
  "away_score": 1
}
```

**Response:**
```json
{
  "prediction": 0,
  "label": "Home Win",
  "probabilities": {
    "home_win": 0.82,
    "away_win": 0.06,
    "draw": 0.12
  }
}
```

<br>

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Python 3 |
| ML Model | scikit-learn — Random Forest Classifier |
| Data | pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| API | Flask, Flask-CORS |
| Tunnel | ngrok / pyngrok |
| Frontend | HTML, CSS, Vanilla JS |

<br>

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
