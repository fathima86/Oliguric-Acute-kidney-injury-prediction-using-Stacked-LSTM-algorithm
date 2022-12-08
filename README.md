# Oliguric-Acute-kidney-injury-prediction-using-Stacked-LSTM-algorithm
This is an implementation of stacked Long-Short term Memory (LSTM) network for the task of Oliguric Acute Kidney Injury (AKI) prediction in ICU settings.

Running
The LSTM model can be run via the stacked_LSTM.ipynb; the other baseline models can be run using the base_models.ipynb notebook.

To run the models some preliminary steps are needed to set-up the dataset and extract the data (see Section Data below).

Dependencies
torch
numpy
sklearn
pandas
captum
matplotlib
seaborn
Data
The MIMIC III dataset was used. The expected data files are:

kdigo_stages_measured.csv containing time-series measurements of creatinine, urine output for the last 12 and 24 hours and the respective labels.
icustay_detail-kdigo_stages_measured.csv containing non-temporal variables of patient demographics such as: age (numerical), gender (binary), ethnicity group (categorical) and type of admission (categorical).
labs-kdigo_stages_measured.csv containing time-series data of the laboratory tests.
vitals-kdigo_stages_measured.csv containing time-series data of the measurements of vital signs.
vents-vasopressor-sedatives-kdigo_stages_measured.csv containing temporal information on whether mechanical ventilation, vasopressor or sedative medications were applied.
To generate such data files some preliminary step are needed:

Set-up MIMIC III
Run the following SQL scripts in MIMIC-III datatset:
mimic-iii/concepts/echo-data.sql
mimic-iii/concepts/demographics/icustay_detail.sql
mimic-iii/concepts/durations/weight-durations.sql
mimic-iii/concepts/durations/vasopressor-durations.sql
mimic-iii/concepts/durations/ventilation-durations.sql
mimic-iii/concepts/fluid-balance/urine-output.sql
mimic-iii/concepts/organfailure/kdigo-creatinine.sql
mimic-iii/concepts/organfailure/kdigo-stages-48hr.sql
mimic-iii/concepts/organfailure/kdigo-stages-7day.sql
mimic-iii/concepts/organfailure/kdigo-stages.sql
mimic-iii/concepts/organfailure/kdigo-uo.sql
Run the SQL scripts. The extract_data.sql should be run after all the other scripts. These scripts builds on and extends the scripts from the MIMIC code repository mentioned at point 2.
Extracted data are saved as CSV files and used for implementation
imputation
Selection and pattern mixture model

Models
Continuous AKI prediction

stacked LSTM
Prediction 48 hours before the onset of AKI
XGBoost
Random forest
LSTM
The features includes demographics data, vital signs measured at the bedsidesuch as heart rate, arterial blood pressure, respiration rate, etc. laboratory test results such as blood urea nitrogen, hemoglobin, white blood count, etc. average of urine output, theminimum value of estimated glomerular filtration rate (eGFR) and creatinine. We also included co-morbidities such as congestive heart failure, hypertension, diabetes, etc.
