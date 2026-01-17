# 🤖 AI/ML Systems: Getting Started

## Prerequisites

- ✅ Completed **04-green-belt** from core belts
- ✅ Comfortable with Python (pandas, numpy)
- ✅ Basic ML knowledge (training vs inference, overfitting, etc.)
- ✅ Understanding of distributed systems concepts (from 05-purple-belt)

## What You'll Build

### Orange Belt Projects

1. **ML API Server**: Serve a trained model via REST API (using FastAPI)
2. **Feature Pipeline**: Build a feature engineering pipeline (Pandas → database)
3. **Experiment Tracker**: Track model training runs (hyperparameters, metrics)
4. **Batch Prediction**: Process millions of items for inference overnight

### Green Belt Projects

1. **Feature Store**: Centralized repository for features (real-time + batch)
2. **ML Data Pipeline**: End-to-end data → train → serve (Airflow)
3. **Model Monitoring**: Detect data drift and model decay
4. **Production A/B Test**: Deploy two models, measure which performs better

## Tech Stack Setup

Choose your tools:

**Minimal Stack** (to start):
- **Model Training**: scikit-learn (simple, fast)
- **Serving**: Flask + Gunicorn (lightweight)
- **Storage**: PostgreSQL (features + metadata)

**Full Stack** (production-grade):
- **Model Training**: PyTorch or TensorFlow
- **Serving**: TensorFlow Serving or Triton
- **Feature Store**: Feast
- **Pipelines**: Airflow
- **Monitoring**: DataDog

## Getting Started

### Step 1: Train a Model

```python
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
import pickle

iris = load_iris()
model = RandomForestClassifier(n_estimators=100)
model.fit(iris.data, iris.target)

# Save model
with open('model.pkl', 'wb') as f:
    pickle.dump(model, f)
```

### Step 2: Serve It via API

```python
from fastapi import FastAPI
import pickle

app = FastAPI()

with open('model.pkl', 'rb') as f:
    model = pickle.load(f)

@app.post("/predict")
def predict(features: list[float]):
    prediction = model.predict([features])
    return {"prediction": int(prediction[0])}

# Run: uvicorn main:app --reload
```

### Step 3: Start Orange Belt

Begin with [03-orange-belt/lessons.md](03-orange-belt/lessons.md).

You now have:
- [ ] A trained model
- [ ] An API server
- [ ] Ready to learn ML systems engineering
