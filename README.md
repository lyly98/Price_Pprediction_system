# Price Prediction System

A machine learning pipeline for house price prediction built with ZenML and MLflow. This project demonstrates a complete MLOps workflow including data ingestion, preprocessing, model training, evaluation, and deployment.

## 🎯 Project Overview

This project implements an end-to-end machine learning pipeline for predicting house prices using various features such as lot area, overall quality, year built, and other property characteristics. The system uses ZenML for pipeline orchestration and MLflow for experiment tracking and model deployment.

### Key Features

- **Data Pipeline**: Automated data ingestion and preprocessing
- **Model Training**: Machine learning model training with evaluation metrics
- **Experiment Tracking**: MLflow integration for tracking experiments
- **Model Deployment**: REST API endpoint for real-time predictions
- **MLOps Workflow**: Complete CI/CD pipeline for machine learning

## 📚 Course Attribution

This project was created as part of a course provided by [ZenML Tutorial](https://www.youtube.com/watch?v=o6vbe5G7xNo). The course covers MLOps fundamentals and demonstrates how to build production-ready machine learning pipelines.

## 🛠️ Prerequisites

- Python 3.8 or higher
- Git
- Virtual environment tool (venv, conda, or virtualenv)

## 📦 Installation

### 1. Install ZenML

First, install ZenML following the official installation guide:
- [ZenML Installation Guide](https://docs.zenml.io/getting-started/installation)

### 2. Clone the Repository

```bash
git clone <your-repository-url>
cd Price_Pprediction_system
```

### 3. Create Virtual Environment

Create and activate a virtual environment:

**Using venv:**
```bash
python -m venv zenml_env
source zenml_env/bin/activate  # On Windows: zenml_env\Scripts\activate
```

**Using conda:**
```bash
conda create -n zenml_env python=3.10
conda activate zenml_env
```

**For detailed virtual environment setup, follow this guide:**
- [Virtual Environment Setup Guide](https://youtu.be/GZbeL5AcTgw?si=uj7B8-10kbyEytKo)

### 4. Install Dependencies

Once your virtual environment is activated, install the required packages:

```bash
pip install -r requirements.txt
```

### 5. Install ZenML Integrations

For deployment functionality, install the MLflow integration:

```bash
zenml integration install mlflow -y
```

### 6. Configure ZenML Stack

The project requires a ZenML stack with MLflow experiment tracker and model deployer components. Configure the stack as follows:

```bash
# Install MLflow integration
zenml integration install mlflow -y

# Register MLflow experiment tracker
zenml experiment-tracker register mlflow_tracker --flavor=mlflow

# Register MLflow model deployer
zenml model-deployer register mlflow --flavor=mlflow

# Register and set the complete stack
zenml stack register local-mlflow-stack -a default -o default -d mlflow -e mlflow_tracker --set
```

## 🚀 Usage

### Training Pipeline

To train the model and run the complete ML pipeline:

```bash
python run_pipeline.py
```

This will:
- Ingest and preprocess the data
- Train the machine learning model
- Evaluate the model performance
- Track experiments in MLflow

### Model Deployment

To deploy the model and start the prediction service:

```bash
python run_deployment.py
```

This will:
- Deploy the trained model as a REST API service
- Start the MLflow prediction server
- Provide the API endpoint for predictions

### Making Predictions

Once the deployment is running, you can make predictions using the sample script:

```bash
python sample_predict.py
```

Or make direct API calls to the prediction endpoint:
```bash
curl -X POST http://127.0.0.1:8000/invocations \
  -H "Content-Type: application/json" \
  -d '{"dataframe_records": [{"Order": 1, "PID": 5286, "MS SubClass": 20, ...}]}'
```

### Stopping the Service

To stop the deployed prediction service:

```bash
python run_deployment.py --stop-service
```

## 📊 Monitoring and Visualization

### MLflow UI

After running the training pipeline, you can view experiment results in the MLflow UI:

```bash
mlflow ui --backend-store-uri <tracking_uri>
```

The tracking URI will be displayed after running the pipeline.

### ZenML Dashboard

Access the ZenML dashboard to monitor pipeline runs:

```bash
zenml up
```

## 📁 Project Structure

```
Price_Pprediction_system/
├── src/                    # Source code modules
│   ├── ingest_data.py     # Data ingestion pipeline
│   ├── data_splitter.py   # Data splitting utilities
│   └── model_building.py  # Model training logic
├── steps/                  # ZenML pipeline steps
│   └── model_building_step.py
├── pipelines/             # Pipeline definitions
│   ├── training_pipeline.py
│   └── deployment_pipeline.py
├── analysis/              # Data analysis notebooks
│   └── EDA.ipynb
├── data/                  # Data files
├── requirements.txt       # Python dependencies
├── run_pipeline.py       # Training pipeline runner
├── run_deployment.py     # Deployment pipeline runner
└── sample_predict.py     # Sample prediction script
```

## 🔧 Configuration

The project uses a `config.yaml` file for configuration. Key settings include:
- Data paths
- Model parameters
- Evaluation metrics
- Deployment settings

## 📈 Model Performance

The trained model typically achieves:
- **R² Score**: ~0.92
- **Mean Squared Error**: ~0.011

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request
