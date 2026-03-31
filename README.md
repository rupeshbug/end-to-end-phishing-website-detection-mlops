## Phishing Website Detection MLOps Pipeline

An end-to-end machine learning and MLOps project for classifying websites as phishing or legitimate using a pre-engineered phishing feature dataset.

The repository covers the full workflow:

`data ingestion -> validation -> transformation -> model training -> experiment tracking -> artifact saving -> batch inference API -> Docker/AWS deployment`

### Live Demo

The application was deployed on AWS EC2 and served through FastAPI.

API docs:
http://51.21.219.154:8080/docs

> Note: This demo runs on free-tier infrastructure and may be unavailable at times.

---

### Project Overview

This project productionizes a phishing-classification workflow using classical machine learning on tabular cybersecurity features.

Instead of training directly on raw website pages, the model uses engineered signals related to:

- URL structure
- domain characteristics
- SSL and trust indicators
- link and anchor behavior
- redirect and browser-manipulation patterns
- domain visibility and reputation signals

The main goal of the project is not just model training, but building a modular and deployable ML system around that data.

---

### Problem Statement

Phishing websites are a common cybersecurity threat used to steal credentials, financial information, and user trust.

Given a dataset of website risk signals, the objective is to build and deploy a model that classifies each record as:

- `0` = phishing
- `1` = legitimate

In the source dataset, the original label uses `-1` and `1`. During transformation, `-1` is converted to `0` for training consistency.

---

### Why This Project Matters

This project demonstrates:

- modular ML pipeline design
- practical MLOps structure
- reproducible preprocessing and artifact handling
- experiment tracking with MLflow
- batch inference through FastAPI
- containerization with Docker
- deployment workflow using AWS ECR and EC2

It represents the transition from notebook-based experimentation to a more production-style machine learning system.

---

### Dataset

Training data is stored in [Network_Data/phisingData.csv](Network_Data/phisingData.csv).

Dataset summary:

- `11055` rows
- `30` input features
- `1` target column: `Result`

The features are not raw website content. They are pre-engineered phishing heuristics encoded as numeric categories such as `-1`, `0`, and `1`.

Examples of feature groups:

- URL-based features: `having_IP_Address`, `URL_Length`, `Prefix_Suffix`
- trust-related features: `SSLfinal_State`, `age_of_domain`, `DNSRecord`
- link behavior features: `URL_of_Anchor`, `Links_in_tags`, `Request_URL`
- suspicious behavior features: `Submitting_to_email`, `Redirect`, `Iframe`, `popUpWidnow`
- reputation signals: `web_traffic`, `Page_Rank`, `Google_Index`

This makes the project best described as phishing website classification using engineered security features.

---

### Pipeline Architecture

The training workflow is organized into modular components:

1. `Data Ingestion`
   Reads data from MongoDB, stores a feature-store copy, and creates train/test splits.

2. `Data Validation`
   Checks schema consistency and performs train/test drift detection.

3. `Data Transformation`
   Splits features and labels, converts target values, applies preprocessing, and saves transformed arrays plus the preprocessing object.

4. `Model Training`
   Trains and compares multiple classical ML models using grid search and classification metrics.

5. `Experiment Tracking`
   Logs metrics and model artifacts with MLflow.

6. `Artifact Packaging`
   Saves the final model and preprocessing objects for inference.

7. `Serving and Deployment`
   Exposes training and prediction routes via FastAPI and packages the app for Docker/AWS deployment.

---

### Project Structure

```text
networksecurity/
  components/        # ingestion, validation, transformation, training
  entity/            # config and artifact dataclasses
  pipeline/          # training pipeline orchestration
  utils/             # helpers, metrics, model wrapper
  logging/           # custom logging setup
  exception/         # custom exception class
  cloud/             # S3 sync utilities

Network_Data/        # source dataset
data_schema/         # schema contract
templates/           # HTML prediction output
final_model/         # saved model artifacts
.github/workflows/   # CI/CD workflow
app.py               # FastAPI app
main.py              # local training entrypoint
push_data.py         # CSV to MongoDB loader
```

---

### Models Used

The training pipeline compares multiple classical ML models:

- Random Forest
- Decision Tree
- Gradient Boosting
- Logistic Regression
- AdaBoost

Model selection is based on evaluation performance, with MLflow used to log results.

---

### How Prediction Works

The FastAPI inference endpoint accepts a CSV file containing website feature values. This design supports batch predictions, enabling you to classify multiple websites at once.

Prediction flow:

1. Load the uploaded CSV file
2. Apply the saved preprocessing object
3. Run the trained model on all rows
4. Return predictions in an HTML table
5. Save batch output to `prediction_output/output.csv`

This supports batch prediction rather than single-URL live feature extraction.

---

### Tech Stack

**ML and Data**

- pandas
- numpy
- scikit-learn
- MLflow
- DagsHub

**Backend**

- FastAPI
- Uvicorn

**Storage and Data Source**

- MongoDB Atlas
- AWS S3

**Deployment**

- Docker
- AWS ECR
- AWS EC2
- GitHub Actions
