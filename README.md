# Scalable Machine Learning and Deep Learning - Assignment 1

This repository contains the first assignment for the course **Scalable Machine Learning and Deep Learning (ID2223)**.[ID2223](https://www.kth.se/student/kurser/kurs/ID2223?l=en). Further information regarding the steps followed in this repository can also be found in the O'Reilly book **Building Machine Learning Systems with a Feature Store: Batch, Real-Time, and LLMs**.

## Authors
This work was conducted collaboratively by Davide Nascivera and Andrei Tuturea. All steps performed align with the instructions provided in the lab guide, 1-6.

## Steps Overview

### Steps 1-5:
- All steps from 1 to 5 have been successfully implemented in the corresponding files.

### Step 6:
- Integrates a rolling window feature into the pipeline, improving both training and inference processes by reducing the Mean Squared Error (MSE) from 150 to 124 during model training.

---

## Step 6: Rolling Window Feature Integration
The following files were modified to integrate the rolling window feature:

### **Modified Files**
1. **`2_air_quality_feature_pipeline.ipynb`**  
   - Added the creation of a new feature group, `air_quality_roll_fg`, including the rolling average (`pm25_rolling`) column.

   Example of the new feature group:

   | **date**               | **pm25** | **country** | **city**  | **street** | **url**                                 | **pm25_rolling** |
   |-------------------------|----------|-------------|-----------|------------|-----------------------------------------|------------------|
   | 2024-11-20 00:00:00+00:00 | 78.0    | italy       | toscana   | pisa       | [Link](https://api.waqi.info/feed/@9432) | 78.0            |
   | 2024-11-19 00:00:00+00:00 | 78.0    | italy       | toscana   | pisa       | [Link](https://api.waqi.info/feed/@9432) | 78.0            |

2. **`3.1_air_quality_training_pipeline_ROLLING.ipynb`**  
   - Incorporated the new rolling window feature (`pm25_rolling`) into the training dataset.

3. **`4_air_quality_batch_inference_ROLLING.ipynb`**  
   - Updated the batch inference logic to retrieve rolling feature values and handle missing data (`NaN`) for future timestamps.

   Example of the prepared dataset:

   | **city**   | **date**               | **pm25** | **pm25_rolling** | **temperature_2m_mean** | **precipitation_sum** | **wind_speed_10m_max** | **wind_direction_10m_dominant** |
   |------------|------------------------|----------|------------------|--------------------------|-----------------------|------------------------|------------------------------|
   | toscana    | 2017-01-05 00:00:00+00:00 | 50.0    | 49.0            | 3.77                    | 1.9                   | 26.37                  | 26.37                        |
   | toscana    | 2017-01-04 00:00:00+00:00 | 82.0    | 58.0            | 5.16                    | 0.4                   | 9.59                   | 9.59                         |
   | toscana    | 2024-11-23 00:00:00+00:00 | NaN     | NaN             | 11.70                   | 0.0                   | 2.04                   | 2.04                         |

---

## Summary

This project demonstrates the integration of rolling window features to improve air quality predictions through an end-to-end pipeline. The addition of `pm25_rolling` significantly enhanced model performance during training and streamlined batch inference. Future work may focus on adding more environmental features and experimenting with advanced machine learning models to further reduce prediction error.

---

## Summary
This project demonstrates the integration of lagged features into the machine learning pipeline for improved air quality predictions. Each notebook plays a key role in ensuring a seamless end-to-end workflow, from feature engineering to model training and inference.


### Dashboard  
Explore the results of the pipeline on the interactive [Dashboard](https://davidenascivera.github.io/mlfs-book/air-quality/).

