# 🤖 AI/ML Systems: Orange Belt Lessons

## Module 1: Model Serving Fundamentals

### 1.1 Inference vs Training

- **Training**: Learning from data (happens offline, takes hours/days)
- **Inference**: Making predictions (happens online, must be fast, < 100ms)

Training and inference have different requirements:

| Aspect | Training | Inference |
| --- | --- | --- |
| Latency | Minutes to days | < 100ms |
| Throughput | Doesn't matter | 1000s requests/sec |
| Cost Metric | GPU-hours | Cost per prediction |
| Debugging | More forgiving | Strict (customer-facing) |

### 1.2 Serving Strategies

**Batch Inference** (Offline):
- Process 1 million items every night
- Generate recommendations for all users
- Store results in database
- When user requests, lookup precomputed result
- Latency: 0ms (just database read)

**Real-Time Inference** (Online):
- User requests prediction immediately
- Run model inference synchronously
- Return result in < 100ms
- Requires fast inference + caching

**Streaming Inference**:
- Continuous predictions on event stream (Kafka)
- Process as events arrive
- Aggregate results over time

### 1.3 Model Formats & Serialization

Models must be saved and loaded efficiently:

- **Pickle** (Python): Fast, supports complex objects, not portable
- **SavedModel** (TensorFlow): Production-grade, supports multiple frameworks
- **ONNX** (Open Neural Network Exchange): Standard format, works across frameworks
- **joblib**: Like pickle, better for large objects
- **HDF5**: Scientific data, good for matrices

### 1.4 Inference Optimization

Making predictions fast requires optimization:

- **Batch Processing**: Process 100 items together (better hardware utilization)
- **Caching**: Store results for repeated requests
- **Quantization**: Use 8-bit integers instead of 32-bit floats (4x smaller, faster)
- **Pruning**: Remove unimportant weights (model is smaller)
- **Distillation**: Train smaller model to mimic larger one
- **Hardware Acceleration**: Use GPUs or TPUs for matrix operations

---

## Module 2: Feature Engineering & Pipelines

### 2.1 Features vs Raw Data

**Raw Data**: Customer ID, date, product purchased
**Features**: "Days since last purchase", "Total spent in 30 days", "Product category"

Models need features, not raw data.

### 2.2 Feature Stores

Centralized repository for all features:

```
Training: User 123 → Feature Store → "last_purchase_days": 5, "total_spent": 1000
Inference: User 123 → Feature Store → Same features
```

Benefits:
- Consistency (train and serve use same features)
- Reusability (share features across models)
- Monitoring (detect when features change unexpectedly)

### 2.3 Offline vs Online Features

- **Offline Features**: Computed once daily (user's total purchases, account age)
- **Online Features**: Computed in real-time (current time, current page)

Most systems need both.

### 2.4 Feature Drift

Over time, feature distributions change:

- "Average purchase amount" was $50, now it's $75
- Model trained on old distribution, predictions may degrade
- Must monitor and retrain

---

## Module 3: Model Training & Experimentation

### 3.1 Experiment Tracking

Running one experiment at a time is slow. Track many experiments:

```python
import mlflow

mlflow.log_param("learning_rate", 0.001)
mlflow.log_param("batch_size", 32)
mlflow.log_metric("accuracy", 0.95)
mlflow.log_artifact("model.pkl")
```

Compare experiments:
- Which hyperparameters give best accuracy?
- Did changing the dataset help?
- Is the new model better?

### 3.2 Hyperparameter Optimization

Models have hyperparameters (learning rate, tree depth, etc.) that affect performance.

**Grid Search**: Try all combinations (slow)
**Random Search**: Try random combinations (faster)
**Bayesian Optimization**: Smart guessing based on past results (best)

### 3.3 Reproducibility

ML is non-deterministic:
- Random seed initialization
- GPU randomness
- Data order

For reproducibility:
- Set random seeds
- Version your code
- Version your data
- Document all hyperparameters

---

## Module 4: Monitoring & Alerts

### 4.1 Model Performance Decay

Models degrade over time because:

- **Data Drift**: Input distribution changed (new customer demographics)
- **Concept Drift**: Relationship changed (user behavior changed)
- **Model Staleness**: Model is just old

Metrics to monitor:
- **Training Metrics**: Accuracy, F1, AUC (on training data)
- **Production Metrics**: Same metrics on live traffic
- **Business Metrics**: Conversion rate, revenue (does the model help?)

### 4.2 Data Drift Detection

Compare distribution of features in production vs training:

If "average_user_age" was 35 during training but is now 40, features have drifted.

### 4.3 Alerting

Set up alerts:
- If prediction latency > 100ms, alert
- If accuracy drops > 5%, retrain
- If error rate > 1%, rollback model

---

## Key Principles

1. **Train-Serve Consistency**: Train and serve use identical features
2. **Monitoring First**: Measure everything; can't improve what you don't measure
3. **Simplicity**: Start with simple models; add complexity only if needed
4. **Reproducibility**: Can you run the same experiment next year and get the same result?
5. **Operational Excellence**: Production is harder than training; optimize for ops

See [03-orange-belt/daily-exercises.md](daily-exercises.md) for hands-on practice.
