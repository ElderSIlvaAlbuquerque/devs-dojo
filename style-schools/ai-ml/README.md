# 🤖 AI/ML Systems Engineering Dojo

Welcome to **AI/ML Systems Engineering**, the style school for building production AI/ML systems at scale.

**Why ML Systems Engineering is Unique**:
- **Convergence of Code + Data**: Classic software engineering + data science
- **Reproducibility Challenges**: Non-deterministic models, data drift, versioning
- **Operational Complexity**: Monitoring model performance, retraining pipelines
- **High Latency**: Models may take seconds to run (vs milliseconds for traditional APIs)
- **Continuous Learning**: Models degrade over time; they need retraining
- **Resource Constraints**: GPUs are expensive; optimize carefully
- **Regulatory Implications**: Model bias, fairness, interpretability matter

---

## What You'll Learn

### Core ML Systems Concepts

- **Model Serving**: Running trained models in production (inference)
- **Feature Engineering & Pipelines**: Preprocessing data for models
- **Experiment Tracking**: Managing model versions, hyperparameters, results
- **Data Pipelines**: ETL for feeding models with training data
- **Model Monitoring**: Detecting data drift, model decay
- **Inference Optimization**: Making predictions fast and cheap
- **GPU/TPU Management**: Maximizing hardware efficiency
- **Real-Time Predictions**: Sub-second inference at scale
- **Batch Predictions**: Processing millions of items offline
- **Model Retraining**: Keeping models fresh as data changes

### Technical Skills

- Building feature stores (centralized feature management)
- Designing data pipelines (Airflow, dbt, Kafka)
- Deploying models (Docker, Kubernetes, serverless)
- Optimizing models (quantization, pruning, distillation)
- Monitoring data drift and model performance
- A/B testing models in production
- Debugging model failures and performance issues

---

## Structure

### 🟠 Orange Belt (03-orange-belt/)

**Topics**: Model serving basics, simple inference APIs, feature engineering, experiment tracking

**Duration**: 4-6 weeks

### 🟢 Green Belt (04-green-belt/)

**Topics**: Advanced serving (real-time, batch), data pipelines, monitoring, retraining, optimization

**Duration**: 6-8 weeks

---

## Prerequisites

- ✅ Completed **04-green-belt** from core belts
- ✅ Completed or concurrent with **05-purple-belt**
- ✅ Basic Python (pandas, NumPy, scikit-learn)
- Preferred: Completed an ML intro course (Andrew Ng's, FastAI, etc.)

---

## Tech Stack Suggestions

**Model Training**: PyTorch, TensorFlow, scikit-learn
**Serving**: TensorFlow Serving, Triton Inference Server, FastAPI
**Feature Store**: Feast, Tecton
**Data Pipelines**: Airflow, dbt, Kafka
**Experiment Tracking**: MLflow, Weights & Biases
**Monitoring**: DataDog, Evidently AI
**Deployment**: Docker, Kubernetes, AWS SageMaker

---

## Why ML Systems Engineering?

With AI models handling increasingly critical tasks (recommendations, credit decisions, medical diagnosis), the engineering behind them is more important than the models themselves. This school teaches you to build systems that:

- Scale inference to millions of predictions/day
- Keep models fresh with automated retraining
- Detect when models are failing
- A/B test safely in production
- Optimize costs without sacrificing accuracy

Let's build some ML systems!
