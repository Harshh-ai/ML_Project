# Student Exam Performance Prediction

An end-to-end machine learning project that predicts student math scores based on demographic and academic features. The project implements a complete MLOps pipeline including data ingestion, transformation, model training, and deployment via a Flask web application.

**Live Demo:** https://ml-project-2-x0ss.onrender.com

## Project Overview

This project demonstrates a production-ready machine learning pipeline architecture following software engineering best practices including modular design, custom exception handling, and comprehensive logging. The system predicts student math performance using regression models trained on student demographic and academic data.

## Problem Statement

Given student demographic and academic information, predict the math score a student is likely to achieve. The model can help educational institutions identify students who may need additional support.

### Features Used for Prediction

- Gender
- Race/Ethnicity
- Parental Level of Education
- Lunch Type (standard/free-reduced)
- Test Preparation Course Status
- Reading Score
- Writing Score

### Target Variable

- Math Score (Regression)

## Technical Architecture

### Project Structure

```
ML_Project/
|-- application.py              # Flask application entry point
|-- requirements.txt            # Python dependencies
|-- runtime.txt                 # Python version specification
|-- setup.py                    # Package configuration
|
|-- src/
|   |-- __init__.py
|   |-- exception.py            # Custom exception handling
|   |-- logger.py               # Logging configuration
|   |-- utils.py                # Utility functions (save/load objects)
|   |
|   |-- components/
|   |   |-- data_ingestion.py      # Data loading and train-test split
|   |   |-- data_transformation.py # Feature preprocessing pipeline
|   |   |-- model_trainer.py       # Model training and evaluation
|   |
|   |-- pipeline/
|       |-- train_pipeline.py      # Training pipeline orchestration
|       |-- predict_pipeline.py    # Prediction pipeline for inference
|
|-- artifacts/                  # Generated model artifacts
|   |-- train.csv               # Training data
|   |-- test.csv                # Test data
|   |-- preprocessor.pkl        # Serialized preprocessing pipeline
|   |-- model.pkl               # Trained model
|
|-- templates/                  # HTML templates for web interface
|   |-- index.html
|   |-- home.html
|
|-- notebook/
    |-- data/
        |-- stud.csv            # Raw dataset
```

### Pipeline Components

#### 1. Data Ingestion

- Loads raw data from CSV
- Performs train-test split (80-20)
- Saves processed data to artifacts directory

#### 2. Data Transformation

- **Numerical Features**: Median imputation + Standard scaling
- **Categorical Features**: Most frequent imputation + One-hot encoding + Standard scaling
- Saves preprocessing pipeline as pickle file for inference

#### 3. Model Training

Evaluates multiple regression models and selects the best performer:

- Linear Regression
- Random Forest Regressor
- Decision Tree Regressor
- Gradient Boosting Regressor
- K-Nearest Neighbors Regressor
- XGBoost Regressor
- CatBoost Regressor
- AdaBoost Regressor

Model selection is based on R-squared score on test data. The best performing model is serialized and saved for production use.

## Model Performance

The best performing model achieved an R-squared score of approximately 0.88 on the test set, indicating strong predictive capability for student math scores.

## Installation

### Prerequisites

- Python 3.11 or higher
- pip package manager

### Setup

1. Clone the repository:
```bash
git clone https://github.com/Harshh-ai/ML_Project.git
cd ML_Project
```

2. Create and activate virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Install the package in development mode:
```bash
pip install -e .
```

## Usage

### Training the Model

Run the training pipeline to generate model artifacts:

```bash
python -m src.components.data_ingestion
```

Or use the training pipeline directly:

```bash
python -m src.pipeline.train_pipeline
```

### Running the Web Application

Start the Flask development server:

```bash
python application.py
```

Access the application at `http://localhost:5000`

### Making Predictions

1. Navigate to the web interface
2. Enter student information:
   - Select gender
   - Select race/ethnicity group
   - Select parental education level
   - Select lunch type
   - Select test preparation status
   - Enter reading score (0-100)
   - Enter writing score (0-100)
3. Submit to receive predicted math score

## Deployment

### Render Cloud Deployment

This application is configured for deployment on Render cloud platform.

**Configuration:**

- Build Command: `pip install -r requirements.txt`
- Start Command: `gunicorn application:app --bind 0.0.0.0:$PORT`
- Python Version: Specified in `runtime.txt`

**Deployment Steps:**

1. Push code to GitHub repository
2. Create new Web Service on Render
3. Connect GitHub repository
4. Set build and start commands
5. Deploy

## Technologies Used

| Category | Technologies |
|----------|-------------|
| Language | Python 3.11 |
| Web Framework | Flask |
| Machine Learning | scikit-learn, XGBoost, CatBoost |
| Data Processing | pandas, numpy |
| Model Serialization | pickle |
| Production Server | gunicorn |
| Cloud Platform | Render |
| Version Control | Git |

## Key Features

- **Modular Architecture**: Separated components for ingestion, transformation, and training
- **Custom Exception Handling**: Detailed error messages with file and line number tracking
- **Comprehensive Logging**: Timestamped logs stored in dedicated directory
- **Automated Model Selection**: Evaluates multiple algorithms and selects best performer
- **Production Ready**: Configured for cloud deployment with gunicorn
- **Reproducible Pipeline**: Fixed random states for consistent results

## Future Improvements

- Implement hyperparameter tuning using GridSearchCV
- Add data validation and schema checking
- Implement model versioning and experiment tracking
- Add unit tests for pipeline components
- Implement REST API endpoints for programmatic access
- Add model explainability using SHAP values

## Author

Harshdeep Singh

## License

This project is open source and available under the MIT License.