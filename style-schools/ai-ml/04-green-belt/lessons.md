# 🤖 AI/ML Systems: Green Belt Lessons

## Module 1: Production ML Pipelines

### 1.1 End-to-End ML Systems

A production ML system has many components beyond the model:

**Data Pipeline**:
- Data collection (logs, events, databases)
- Data validation (schema checks, anomaly detection)
- Data transformation (feature engineering)
- Data versioning (track what trained each model)

**Training Pipeline**:
- Experiment tracking (MLflow, Weights & Biases)
- Hyperparameter tuning (grid search, Bayesian optimization)
- Model validation (hold-out set, cross-validation)
- Model versioning (track lineage)

**Serving Pipeline**:
- Model packaging (containers, serverless)
- Deployment strategies (blue-green, canary)
- Load balancing & scaling
- A/B testing framework

**Monitoring Pipeline**:
- Prediction logging
- Drift detection (data drift, concept drift)
- Performance metrics (accuracy, latency, throughput)
- Alerting & incident response

### 1.2 Feature Stores (Deep Dive)

Centralized feature management for training and serving:

```python
# Training time
features = feature_store.get_historical_features(
    entity_ids=user_ids,
    features=['user_age', 'user_lifetime_value', 'user_churn_risk'],
    timestamp_range=('2024-01-01', '2024-12-31')
)
model.train(features, labels)

# Inference time
features = feature_store.get_online_features(
    entity_id=user_id,
    features=['user_age', 'user_lifetime_value', 'user_churn_risk']
)
prediction = model.predict(features)
```

**Key Capabilities**:
- Point-in-time correctness (avoid data leakage)
- Low-latency serving (< 10ms)
- Feature versioning
- Feature monitoring

### 1.3 Model Versioning & Registry

Track all models in production:

```python
import mlflow

with mlflow.start_run():
    # Train model
    model = train_model(X_train, y_train)
    
    # Log parameters
    mlflow.log_param("learning_rate", 0.01)
    mlflow.log_param("n_estimators", 100)
    
    # Log metrics
    mlflow.log_metric("accuracy", accuracy)
    mlflow.log_metric("f1_score", f1)
    
    # Log model
    mlflow.sklearn.log_model(model, "model")
    
# Register for production
model_uri = f"runs:/{run_id}/model"
mlflow.register_model(model_uri, "fraud_detection")
```

---

## Module 2: Model Monitoring & Observability

### 2.1 Types of Drift

**Data Drift**: Input distribution changes
- Example: Pandemic shifts online shopping behavior
- Detection: Compare recent data to training data distribution

**Concept Drift**: Relationship between features and target changes
- Example: What predicts churn changes over time
- Detection: Model performance degrades on recent data

**Prediction Drift**: Output distribution changes
- Example: Suddenly predicting 80% fraud vs usual 1%
- Detection: Compare recent predictions to historical

### 2.2 Monitoring Metrics

**Model Performance**:
- Accuracy, precision, recall, F1 (for classification)
- MAE, RMSE, R² (for regression)
- Track over time, alert on degradation

**System Performance**:
- Latency (p50, p95, p99)
- Throughput (predictions/second)
- Error rate
- Resource utilization (CPU, memory, GPU)

**Data Quality**:
- Missing values
- Out-of-range values
- Schema violations
- Statistical properties (mean, std, distribution)

### 2.3 Implementing Monitoring

```python
from evidently import ColumnMapping
from evidently.metric_preset import DataDriftPreset
from evidently.report import Report

# Create drift report
report = Report(metrics=[
    DataDriftPreset(),
])

report.run(
    reference_data=train_data,  # Training data
    current_data=prod_data,      # Recent production data
    column_mapping=ColumnMapping()
)

# Get results
results = report.as_dict()
if results['metrics'][0]['result']['dataset_drift']:
    alert("Data drift detected!")
```

---

## Module 3: Scalable Inference

### 3.1 Horizontal Scaling

Serving multiple model replicas:

```yaml
# Kubernetes deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: model-service
spec:
  replicas: 5  # 5 instances
  selector:
    matchLabels:
      app: model
  template:
    metadata:
      labels:
        app: model
    spec:
      containers:
      - name: model
        image: mymodel:v1
        resources:
          requests:
            memory: "2Gi"
            cpu: "1000m"
          limits:
            memory: "4Gi"
            cpu: "2000m"
```

### 3.2 GPU Acceleration

Using GPUs for batch inference:

```python
import torch

# Load model on GPU
model = load_model()
model = model.cuda()

# Batch processing
def batch_predict(inputs, batch_size=32):
    predictions = []
    for i in range(0, len(inputs), batch_size):
        batch = inputs[i:i+batch_size]
        batch_tensor = torch.tensor(batch).cuda()
        
        with torch.no_grad():
            pred = model(batch_tensor)
        
        predictions.extend(pred.cpu().numpy())
    
    return predictions
```

### 3.3 Model Optimization

**Quantization**: Reduce precision for faster inference

```python
import torch.quantization

# Post-training quantization
model_fp32 = load_model()
model_int8 = torch.quantization.quantize_dynamic(
    model_fp32, 
    {torch.nn.Linear}, 
    dtype=torch.qint8
)

# Model is now 4x smaller, 2-3x faster
```

**ONNX Runtime**: Framework-agnostic inference

```python
import onnxruntime as ort

# Convert to ONNX
torch.onnx.export(model, dummy_input, "model.onnx")

# Load with ONNX Runtime
session = ort.InferenceSession("model.onnx")
output = session.run(None, {"input": input_data})
```

---

## Module 4: CI/CD for ML

### 4.1 ML Testing

Unlike traditional software, ML has unique testing needs:

**Unit Tests**: Test data processing functions
```python
def test_feature_engineering():
    raw_data = {"age": 25, "income": 50000}
    features = engineer_features(raw_data)
    assert "age_binned" in features
    assert features["age_binned"] == "20-30"
```

**Integration Tests**: Test model loading and prediction
```python
def test_model_prediction():
    model = load_model("models/v1")
    test_input = create_test_input()
    prediction = model.predict(test_input)
    assert 0 <= prediction <= 1  # Valid probability
```

**Model Tests**: Validate model behavior
```python
def test_model_invariance():
    # Predictions shouldn't change drastically with small input changes
    input1 = [1.0, 2.0, 3.0]
    input2 = [1.01, 2.0, 3.0]
    
    pred1 = model.predict([input1])[0]
    pred2 = model.predict([input2])[0]
    
    assert abs(pred1 - pred2) < 0.01
```

### 4.2 Deployment Strategies

**Blue-Green Deployment**:
```python
# Route 100% traffic to blue (current model)
# Deploy green (new model) but don't route traffic
# Validate green model
# Switch 100% traffic to green
# Keep blue as rollback option
```

**Canary Deployment**:
```python
# Deploy new model version
# Route 5% traffic to new model
# Monitor for 24 hours
# If metrics good, increase to 25%
# Gradually increase to 100%
```

**A/B Testing**:
```python
def predict(user_id, features):
    # Hash user ID to assign to experiment
    if hash(user_id) % 100 < 50:
        # 50% see model A
        return model_a.predict(features)
    else:
        # 50% see model B
        return model_b.predict(features)
```

---

## Module 5: AutoML & Experiment Tracking

### 5.1 Hyperparameter Tuning

**Grid Search**: Try all combinations
```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'max_depth': [3, 5, 7],
    'n_estimators': [50, 100, 200],
    'learning_rate': [0.01, 0.1, 0.3]
}

grid_search = GridSearchCV(
    XGBClassifier(),
    param_grid,
    cv=5,
    scoring='f1'
)
grid_search.fit(X_train, y_train)
best_model = grid_search.best_estimator_
```

**Bayesian Optimization**: Smart search
```python
from hyperopt import fmin, tpe, hp, STATUS_OK

def objective(params):
    model = XGBClassifier(**params)
    score = cross_val_score(model, X_train, y_train, cv=5).mean()
    return {'loss': -score, 'status': STATUS_OK}

space = {
    'max_depth': hp.choice('max_depth', range(3, 10)),
    'n_estimators': hp.choice('n_estimators', range(50, 300, 50)),
    'learning_rate': hp.loguniform('learning_rate', -5, 0)
}

best = fmin(objective, space, algo=tpe.suggest, max_evals=50)
```

### 5.2 Experiment Tracking

Track all experiments systematically:

```python
import wandb

# Initialize experiment
wandb.init(
    project="fraud-detection",
    config={
        "learning_rate": 0.01,
        "n_estimators": 100,
        "max_depth": 5
    }
)

# Train model
for epoch in range(num_epochs):
    train_loss = train_epoch(model, train_loader)
    val_loss = validate(model, val_loader)
    
    # Log metrics
    wandb.log({
        "train_loss": train_loss,
        "val_loss": val_loss,
        "epoch": epoch
    })

# Log final model
wandb.save("model.pkl")
```

---

## Summary

Green Belt focuses on **production-grade ML systems**:

1. **Pipelines**: End-to-end automation from data to deployment
2. **Monitoring**: Detect and respond to model degradation
3. **Scalability**: Serve thousands of predictions per second
4. **CI/CD**: Automated testing and deployment
5. **Optimization**: Make models faster and smaller

**Next Steps**: Practice building complete ML systems, not just models!
