# Student Exam Performance Predictor

An end-to-end machine learning project that predicts a student's mathematics
score from demographic information, parental education, lunch type, test
preparation status, reading score, and writing score.

The project includes the complete workflow needed to take a tabular dataset
from ingestion to a web prediction interface:

- Ingests the student performance dataset and creates reproducible train/test
  splits.
- Preprocesses numerical and categorical features with scikit-learn pipelines.
- Trains and compares multiple regression models, including Random Forest,
  Gradient Boosting, XGBoost, CatBoost, AdaBoost, Decision Tree, and Linear
  Regression models.
- Selects the best model using $R^2$ score and stores the trained model and
  preprocessing object in `artifacts/`.
- Provides a Flask application where users can enter student details and
  receive a predicted mathematics score.

## Project Workflow

1. Read the source data from `notebook/data/stud.csv`.
2. Save the raw data and split it into training and test datasets in
	`artifacts/`.
3. Apply median imputation and standard scaling to numerical features
	(`reading_score` and `writing_score`).
4. Apply most-frequent imputation, one-hot encoding, and scaling to categorical
	features.
5. Tune and evaluate candidate regression models with cross-validation.
6. Save the selected model and use it with the fitted preprocessor for web
	predictions.

## Prediction Inputs

The web form accepts:

- Gender
- Race or ethnicity group
- Parental level of education
- Lunch type
- Test preparation course status
- Reading score out of 100
- Writing score out of 100

The output is the predicted mathematics score.

## Technology Stack

- Python
- Flask
- pandas and NumPy
- scikit-learn
- CatBoost and XGBoost
- seaborn and Matplotlib for exploratory analysis

## Repository Structure

```text
app.py                         Flask application
artifacts/                     Raw, train, test, and serialized model files
notebook/                      Exploratory analysis and model-training notebooks
src/components/                Data ingestion, transformation, and training
src/pipeline/                  Training and prediction pipeline code
templates/                     Flask HTML templates
requirements.txt               Python dependencies
```

## Setup and Usage

Create and activate a virtual environment, then install the dependencies:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Run the Flask application with:

```bash
flask --app app run --debug
```

Open `http://127.0.0.1:5000` in a browser and use the prediction form.

To rebuild the training artifacts from the source dataset, run the ingestion
module from the project root:

```bash
python src/components/data_ingestion.py
```
