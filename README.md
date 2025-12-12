## Phishing Detection MLOps Pipeline

An end-to-end **MLOps pipeline** for detecting phishing websites using classical machine learning.  
The project covers the full lifecycle: **data ingestion → validation → transformation → model training → tracking → packaging → deployment on AWS** with an inference API built using **FastAPI**.

---

### 🚀 Project Overview

This project builds a production-ready ML workflow to classify websites as **phishing** or **legitimate** based on handcrafted URL, domain, and JavaScript-related features.  
The solution follows real-world MLOps practices including:

- Automated pipeline orchestration  
- Reproducible experimentation with MLflow  
- Versioned datasets and artifacts  
- Docker containerization  
- Cloud deployment on AWS  
- API-based model inference  

**Dataset**: The dataset used for training is located at Network_Data/phisingData.csv and contains handcrafted features extracted from website URLs and metadata.

---

### 📌 Problem Statement

Phishing websites are one of the most common cybersecurity threats.  
Given a dataset of website features (URL structure, domain age, JavaScript flags, etc.), the goal is to:

> **Build and deploy a model that classifies websites as phishing (0) or legitimate (1).**

This project demonstrates how such a system can be built using proper MLOps principles.

---

### 🧠 Key Features

- ✔️ End-to-end ML pipeline (training + prediction)
- ✔️ Modular architecture with clean component design  
- ✔️ MLflow tracking for metrics, params, and artifacts  
- ✔️ AWS S3 for model & artifact storage  
- ✔️ Dockerized application for reproducible deployment  
- ✔️ FastAPI for real-time inference and batch CSV predictions  
- ✔️ AWS ECR + EC2 deployment  
- ✔️ Data validation, schema checks, and transformations  
- ✔️ Custom exception handling and logging framework  

---

#### 🧾 How Prediction Works

The FastAPI inference endpoint accepts a CSV file containing website feature values. This design supports batch predictions, enabling you to classify multiple websites at once (common in real MLOps use cases). The system applies the saved preprocessing pipeline and model to generate phishing/legitimate predictions and returns the results as an HTML table or downloadable CSV.

### 🛠️ Tech Stack & Tools Used

### **MLOps**
- **MLflow** – Experiment tracking & model registry  
- **DagsHub** – Remote repository and MLflow backend  
- **Docker** – Environment reproducibility  
- **AWS S3, ECR, EC2** – Cloud deployment  

### **Backend**
- **FastAPI**  
- **Uvicorn**  

### **Storage**
- **MongoDB Atlas**  
- **AWS S3** 
