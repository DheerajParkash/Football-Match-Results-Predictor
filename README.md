# ⚽ Football Match Results Predictor

## 📋 Project Overview
This repository implements a machine-learning based football match results predictor using historical international match results and FIFA world rankings. The system predicts match outcomes (win / draw / loss) and can simulate championship tournaments with group and knockout stages.

---

## 📊 Key Features
- **Data Integration:** Merges historical match results (1872–2023) with FIFA rankings (1992–2023).
- **Feature Engineering:** Builds features such as recent performance metrics, head-to-head stats, and ranking momentum.
- **Multiple ML Models:** Implements Logistic Regression, Random Forest, and Neural Network (MLP).
- **Hyperparameter Tuning:** Uses `GridSearchCV` to find optimal model parameters.
- **Championship Simulation:** Simulates tournaments with group and knockout stages (CSV-driven).
- **Model Persistence:** Saves trained models with `joblib` for deployment and reuse.

---

## 🏗️ Project Structure
```
Football-Match-Results-Predictor/
│
├── Data/
│   ├── FIFA_World_Ranking_1992-2023/
│   └── International_football_results_from_1872-2023/
│
├── ChampionShipData/
│   ├── GroupStage/
│   ├── Knockout1/
│   ├── Knockout2/
│   ├── Knockout3/
│   └── Knockout4/
│
├── Models/
│   ├── RegressorRF.joblib
│   └── RegressorNN.joblib
│
├── Notebooks/
│   ├── Preprocessing_Football match results predictor.ipynb
│   ├── ModelTraining_Football match results predictor.ipynb
│   └── Championship.ipynb
│
├── Dataset/
│   └── rera.csv (processed dataset)
│
├── Reports/
│   └── Project Report.pdf
│   └── presentation.pptx
│
└── README.md
```

---

## 📁 Datasets
1. **International Football Results (1872–2023)** (Kaggle)  
   - Records: 45,100+ matches  
   - Typical features: `date`, `home_team`, `away_team`, `home_score`, `away_score`, `tournament`, `country`, `neutral`

2. **FIFA World Rankings (1992–2023)** (Kaggle)  
   - Features: `rank`, `country`, `total_points`, `rank_changes`, `confederation`

---

## 🔧 Data Preprocessing Pipeline
1. **Cutting Year Selection (2003)** — remove matches before 2003 to standardize country names after political changes.  
2. **Country Name Standardization** — map alternate names to canonical country names (e.g., `"Cabo Verde" → "Republic of Cabo Verde"`).  
3. **Data Resampling** — upsample FIFA rankings to daily frequency and forward-fill to ensure continuous series.  
4. **Dataset Merging** — join results with ranking timeseries to create the unified `rera` dataset (results + rankings).  
5. **Feature Engineering** — build rolling features such as:  
   - Average goals (last 5 matches)  
   - Average points (last 5 matches)  
   - Rank change (last 5 matches)  
   - Head-to-head performance metrics

---

## 🤖 Machine Learning Models & Performance (Summary)
| Model | Accuracy | Notes |
|---|---:|---|
| Logistic Regression | **98.44%** | Good baseline and interpretable |
| Random Forest (base) | 89.06% | Robust, handles non-linearities |
| Random Forest (tuned) | **92.20%** | Best performer after `GridSearchCV` |
| Neural Network (MLP) | ~41.98% | Challenged by limited training data; MSE: 0.47 |

**Key findings:** Random Forest performed best after tuning. Recent performance features (rolling goals/points and rank momentum) were among the most important predictors.

---

## 🏆 Championship Simulation
**Tournament mechanics:**  
- Group stage: round-robin, 3 points for a win, 1 for a draw.  
- Knockout: single-elimination bracket.  
- Input format: CSV (semicolon-separated) where groups are represented as columns.

**Main functions / capabilities:**  
- `runChampionShip()` — main tournament simulation runner.  
- Automated bracket generation and match scheduling.  
- Points table management and team progression tracking.  
- Winner determination and champion output.

---

## 🚀 Installation & Usage

**Prerequisites** (example install command):
```bash
pip install pandas numpy scikit-learn matplotlib seaborn joblib jupyter
```

**Run notebooks** (recommended flow):
- Data preprocessing:  
  ```bash
  jupyter notebook "Notebooks/Preprocessing_Football match results predictor.ipynb"
  ```
- Model training & evaluation:  
  ```bash
  jupyter notebook "Notebooks/ModelTraining_Football match results predictor.ipynb"
  ```
- Championship simulation:  
  ```bash
  jupyter notebook "Notebooks/Championship.ipynb"
  ```

**Load trained models (example):**
```python
import joblib

# Load Random Forest model
rf_model = joblib.load('Models/RegressorRF.joblib')

# Load Neural Network model
nn_model = joblib.load('Models/RegressorNN.joblib')
```

---

## 📈 Results & Performance (detailed)
| Model | Accuracy | Precision | Recall | F1-Score | Notes |
|---|---:|---:|---:|---:|---|
| Logistic Regression | **98.44%** | High | High | High | Excellent baseline |
| Random Forest (Base) | 89.06% | 83–93% | 71–95% | 77–94% | Good overall |
| Random Forest (Tuned) | **92.20%** | 90–100% | 88–100% | 89–100% | Best performer after tuning |
| Neural Network (MLP) | 41.98% | Low | Low | Low | Data limitations impacted NN |
 
**Notes:** Feature importance analysis shows recent performance metrics (rolling averages and rank momentum) as top predictors. Clean, consistent data significantly improves model performance.

---

## 👥 Team Contributions
| Team Member | Responsibilities |
|---|---|
| Muhammad Ahmed | Data preprocessing and cleaning |
| Dheeraj Parkash | Model training, ML pipelines, championship Simulation |
| Alireza Foroutan | Documentation, championship planning |

---

## 🔮 Future Improvements
- Expand dataset and timeframe to improve neural network performance.  
- Add player-level statistics and match-day conditions (weather, injuries).  
- Implement ensemble methods and stacking for improved predictions.  
- Build a web interface for real-time predictions and interactive simulations.

---

## 📚 References
- Kaggle datasets: *International Football Results*, *FIFA World Rankings*  
- Libraries: Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Joblib  
- Educational resources: University Nice Côte d'Azur – Neural Networks course; Scikit-learn documentation; Machine Learning Mastery articles

---

## 📄 License
**Academic Project** — University Nice Côte d'Azur — M1 Informatique

---

## 🙏 Acknowledgments
- Professor Enrico Formenti — project guidance  
- Kaggle community — dataset contributors  
- Scikit-learn developers — ML tools

---
