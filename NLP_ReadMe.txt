# Enterprise Consumer Complaint Intelligence Platform

## Project Overview

The **Enterprise Consumer Complaint Intelligence Platform** is an NLP-based machine learning solution that automatically analyzes consumer complaint narratives and predicts:

1. **Product Category** (for example: Credit Card, Mortgage, Student Loan, Checking Account)
2. **Issue Category** specific to the predicted product

The project simulates how financial institutions can automate complaint routing, reduce manual effort, and improve customer service by directing complaints to the appropriate business teams.

---

# Business Problem

Financial institutions receive thousands of customer complaints every day.

Manual review of each complaint is:

* Time-consuming
* Expensive
* Inconsistent
* Difficult to scale

The objective of this project is to automate complaint classification using Natural Language Processing (NLP) and Machine Learning.

---

# Project Objectives

* Automatically identify the product associated with a complaint.
* Predict the issue category within the identified product.
* Reject low-confidence predictions using confidence thresholds.
* Improve complaint routing accuracy.
* Demonstrate an end-to-end enterprise NLP workflow.

---

# Dataset

**Source:**

Consumer Financial Protection Bureau (CFPB) Consumer Complaint Database

The dataset contains real consumer complaints submitted against financial institutions.

---

# Features Used

* Consumer Complaint Narrative
* Product
* Issue

---

# Project Workflow

```
Consumer Complaint
        │
        ▼
Text Cleaning
        │
        ▼
TF-IDF Vectorization
        │
        ▼
Product Classification (LinearSVC)
        │
        ▼
Confidence Validation
        │
        ├───────────────► Reject (Low Confidence)
        │
        ▼
Product-specific Issue Model
        │
        ▼
Predicted Issue
```


# Machine Learning Pipeline

## Step 1 – Text Preprocessing

Complaint narratives were cleaned using:

* Convert text to lowercase
* Remove URLs
* Remove email addresses
* Remove HTML tags
* Remove punctuation
* Remove numbers
* Remove extra spaces
* Stopword removal
* Lemmatization

---

## Step 2 – Product Classification

The complaint text is transformed into numerical features using **TF-IDF Vectorization**.

### TF-IDF Parameters

* max_features = 10000
* ngram_range = (1,2)
* min_df = 2
* max_df = 0.95
* sublinear_tf = True

### Model

Linear Support Vector Classifier (LinearSVC)

The model predicts one of the financial product categories.

Examples include:

* Credit Card
* Mortgage
* Student Loan
* Vehicle Loan
* Checking or Savings Account
* Money Transfer
* Debt Collection
* Prepaid Card

---

## Step 3 – Confidence Threshold

The LinearSVC decision score is used as a confidence measure.

A confidence threshold filters low-confidence predictions.

Predictions below the threshold are classified as:

```
Unknown
```

instead of assigning an unreliable product.

---

## Step 4 – Issue Classification

After predicting the product, the complaint is passed to a dedicated issue classification model trained specifically for that product.

Each product has:

* Individual TF-IDF Vectorizer
* Individual LinearSVC Model

This two-stage architecture improves issue prediction by restricting predictions to issues relevant to the selected product.

---

# Model Explainability

The project includes an explanation function that identifies the words contributing most to the predicted product.

Contribution Score:

```
TF-IDF Weight × LinearSVC Coefficient
```

Example:

```
credit        0.94
card          1.14
fraud         0.71
payment       0.53
```

This improves model transparency and interpretability.

---

# Model Evaluation

Product prediction was evaluated using:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix

# Key Results

* Product Classification Accuracy: **~81%**
* Product-specific Issue Prediction using dedicated models
* Confidence-based rejection for uncertain predictions
* Explainable predictions using feature contribution analysis


# Skills Demonstrated

* Natural Language Processing (NLP)
* Text Preprocessing
* Feature Engineering
* TF-IDF Vectorization
* Machine Learning
* Multi-stage Classification
* Model Evaluation
* Error Analysis
* Confidence-based Prediction
* Explainable AI
* Model Serialization using Joblib

---

# Business Impact

The solution demonstrates how organizations can:

* Reduce manual complaint triage.
* Improve complaint routing accuracy.
* Accelerate issue resolution.
* Increase operational efficiency.
* Support scalable customer service operations using machine learning.

---

# Conclusion

This project demonstrates an end-to-end NLP pipeline for consumer complaint intelligence. By combining TF-IDF feature extraction, LinearSVC classification, confidence-based validation, and product-specific issue models, the solution provides an efficient and explainable approach for automating complaint classification in financial services.
