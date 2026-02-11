# 🚗 Vehicle Insurance Prediction Pipeline

![MLOps](https://img.shields.io/badge/MLOps-DVC%20%7C%20FastAPI%20%7C%20AWS-blue)
![Python](https://img.shields.io/badge/Python-3.10+-yellow)
![Status](https://img.shields.io/badge/Status-Complete-green)

An end-to-end Machine Learning Pipeline designed to predict customer interest in vehicle insurance. This project implements a robust MLOps lifecycle, from data ingestion to automated deployment using modern cloud infrastructure.

---

## 🌟 Project Overview

This project aims to help insurance providers identify potential customers who are likely to respond positively to vehicle insurance offers. By leveraging historical data and machine learning, we optimize marketing strategies and improve conversion rates.

### Key Highlights:
- **Modular Architecture**: Clean, production-grade code following the pipeline design pattern.
- **Automated CI/CD**: Seamless integration and deployment via GitHub Actions.
- **Cloud Native**: Scalable storage with AWS S3 and containerized deployment with Docker & AWS ECR.
- **Dynamic Monitoring**: Logging and exception handling integrated across all components.

---

## 🛠️ Tech Stack

| Domain | Tools & Technologies |
| :--- | :--- |
| **Language** | Python 3.10 |
| **Frameworks** | FastAPI, Scikit-learn, Pandas, NumPy |
| **Database** | MongoDB Atlas |
| **Cloud** | AWS (S3, ECR, EC2) |
| **DevOps** | Docker, GitHub Actions |
| **Visualization** | Plotly, Matplotlib, Seaborn |

---

## � Dataset Features

The model analyzes several key features to predict customer response:

- **Demographics**: Age, Gender, Region Code.
- **Vehicle Info**: Vehicle Age, Vehicle Damage history.
- **Insurance Details**: Annual Premium, Policy Sales Channel, Vintage (how long customer has been with company), Previous Insurance status.
- **Target**: `Response` (1: Interested, 0: Not Interested).

---

## 🚀 Pipeline Workflow

The project follows a systematic 7-stage ML pipeline:

1.  **Data Ingestion**: Fetches raw data from **MongoDB Atlas**, transforms it into a DataFrame, and splits it into Train/Test sets.
2.  **Data Validation**: Performs schema validation and checks for data drift using **YAML reports**.
3.  **Data Transformation**: Handles categorical encoding, scaling (`StandardScaler` & `MinMaxScaler`), and synthetic oversampling for imbalanced data.
4.  **Model Trainer**: Trains an optimized classifier (default: Random Forest/XGBoost) and evaluates performance against a base score.
5.  **Model Evaluation**: Automates model comparison. It pulls the best model from **AWS S3** and compares it with the newly trained one.
6.  **Model Pusher**: If the new model performs better, it's pushed to the production folder in the S3 bucket.
7.  **Prediction Pipeline**: A robust FastAPI wrapper that takes user input and returns real-time predictions.

---

## ☁️ Deployment & CI/CD

This project demonstrates a full MLOps cycle using **AWS** and **GitHub Actions**:

### Deployment Infrastructure:
- **Registry**: AWS ECR (Elastic Container Registry) for storing Docker images.
- **Compute**: AWS EC2 (Ubuntu instance) for hosting the application.
- **Storage**: AWS S3 for model versioning and artifact storage.
- **CI/CD**: GitHub Actions workflows for automated testing, building, and pushing to ECR.

### How it works:
1.  **Continuous Integration**: On every push, GitHub Actions builds a Docker image.
2.  **Continuous Delivery**: The image is pushed to AWS ECR.
3.  **Continuous Deployment**: A self-hosted runner on the EC2 instance pulls the latest image and restarts the container, making the changes live instantly.

---

## 💻 Local Setup

### Prerequisites
- Python 3.10
- MongoDB Atlas Account
- AWS Account (IAM user with S3 & ECR access)

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/agarwalson02/Vehicle-insurance-pipeline.git
   cd Vehicle-insurance-pipeline
   ```

2. **Create Virtual Environment**
   ```bash
   conda create -n vehicle python=3.10 -y
   conda activate vehicle
   pip install -r requirements.txt
   ```

3. **Set Environment Variables**
   ```bash
   # MongoDB
   export MONGODB_URL="your_mongodb_connection_string"

   # AWS
   export AWS_ACCESS_KEY_ID="your_access_key"
   export AWS_SECRET_ACCESS_KEY="your_secret_key"
   ```

4. **Run the Application**
   ```bash
   python app.py
   ```
   Access the app at `http://localhost:5000`

---

## 📊 Results & UI

The application features a modern web interface for:
- **Batch Training**: Trigger model training via the `/train` endpoint.
- **Single Prediction**: Input customer details to get an instant insurance interest prediction.

---

## � Project Structure

```text
├── .github/workflows   # CI/CD pipeline definitions
├── artifact            # Generated pipeline outputs
├── config              # Configuration files (Schema, Models)
├── notebook            # EDA and experimentation
├── src                 # Core source code
│   ├── components      # Ingestion, Validation, Transformation, etc.
│   ├── entity          # Config and Artifact entities
│   ├── pipeline        # Training and Prediction pipelines
│   └── constants       # Global constants
├── app.py              # FastAPI application
└── Dockerfile          # Containerization script
```

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.


