# mlfs-book
O'Reilly book - Building Machine Learning Systems with a feature store: batch, real-time, and LLMs

# Scalable Machine Learning and Deep Learning - Assignment 1

This repository contains the first assignment for the course **Scalable Machine Learning and Deep Learning (ID2223)**.[ID2223](https://www.kth.se/student/kurser/kurs/ID2223?l=en). Further information regarding the steps followed in this repository can also be found in the O'Reilly book **Building Machine Learning Systems with a Feature Store: Batch, Real-Time, and LLMs**.

## Authors
This work was conducted collaboratively by Davide Nascivera and Andrei Tuturea. The lagged weather feature was exclusively implemented in this repository. 
All steps performed align with the instructions provided in the lab guide, 1-7.

---


## Edited Files

### **1_air_quality_feature_backfill.ipynb**
The `air_quality` FeatureGroup was updated to include lagged PM2.5 values. The following columns were added:

| **date**         | **pm2_5** | **pm2_5_lag_1** | **pm2_5_lag_2** | **pm2_5_lag_3** | **country** | **city**      | **street**      | **url**                              |
|-------------------|-----------|-----------------|-----------------|-----------------|-------------|---------------|----------------|--------------------------------------|
| 2024-11-04        | 7.0       | 6.0             | 5.0             | 8.0             | Sweden      | Stockholm     | Hornsgatan     | [Link](https://api.waqi.info/feed/@10009/) |
| 2024-11-05        | 11.0      | 7.0             | 6.0             | 5.0             | Sweden      | Stockholm     | Hornsgatan     | [Link](https://api.waqi.info/feed/@10009/) |

### **2_air_quality_feature_pipeline.ipynb**
A daily GitHub Actions workflow runs this notebook. It appends a new row to the FeatureGroup, updating the lagged PM2.5 features by shifting the historic data accordingly.

### **3_air_quality_training_pipeline.ipynb**
The training pipeline now incorporates lagged PM2.5 features (`pm2_5_lag_1`, `pm2_5_lag_2`, and `pm2_5_lag_3`) for predictions. Below is an example of the training data:

| **date**               | **temperature_2m_mean** | **precipitation_sum** | **wind_speed_10m_max** | **wind_direction_10m_dominant** | **pm2_5_lag_1** | **pm2_5_lag_2** | **pm2_5_lag_3** | **predicted_pm25** | **city**      |
|-------------------------|-------------------------|------------------------|-------------------------|-------------------------------|-----------------|-----------------|-----------------|--------------------|---------------|
| 2024-07-15 00:00:00+00:00 | 13.02                  | 8.0                    | 22.0                    | 171.0                         | 16.0            | 9.0             | 8.0             | 32.128326         | Stockholm     |

### **4_air_quality_batch_inference.ipynb**
This notebook performs daily batch predictions for future PM2.5 levels. It uses the last three lagged PM2.5 values and other weather features. An example of the prediction dataset:

| **date**               | **temperature_2m_mean** | **precipitation_sum** | **wind_speed_10m_max** | **wind_direction_10m_dominant** | **pm2_5_lag_1** | **pm2_5_lag_2** | **pm2_5_lag_3** | **predicted_pm25** |
|-------------------------|-------------------------|------------------------|-------------------------|-------------------------------|-----------------|-----------------|-----------------|--------------------|
| 2024-11-18 00:00:00+00:00 | 2.50                  | 0.0                    | 10.895576               | 277.594543                    | 7.0             | 16.0            | 16.0            | 32.128326         |

---

## Summary
This project demonstrates the integration of lagged features into the machine learning pipeline for improved air quality predictions. Each notebook plays a key role in ensuring a seamless end-to-end workflow, from feature engineering to model training and inference.

## ML System Examples


[Dashboards for Example ML Systems](https://featurestorebook.github.io/mlfs-book/)

## Course Comparison

| Course                         | MLOps | LLLMs             | Feature/Training/Inference | Working AI Systems | Focus |
|--------------------------------|-------|----------------------------|--------------------|------------------|
| Building AI Systems (O'Reilly) | Yes   | Fine-Tuning & RAG | Yes                        | High               | Project-based, Software Engineering, Fundamentals    |
| [Made With ML](https://madewithml.com/)                   | No          | Yes   | No                         | No                 | Software Engineering, Model Training   |
| [7 Steps MLOps](https://www.pauliusztin.me/courses/the-full-stack-7-steps-mlops-framework)            | Yes   | Separate Course    | Yes                        | Low                | Learning Tools and Project    |


### win user
[Dashboard](https://davidenascivera.github.io/mlfs-book/air-quality/)
