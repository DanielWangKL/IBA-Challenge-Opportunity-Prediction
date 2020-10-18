# International Business Analytics (IBA) Challenge - Opportunity Realization Prediction
Participants of IBA are required to propose recommendations on how to leverage the wealth of data in AIESEC to achieve its business goal.

One of the recommendation will be leveraging binary classification model to quantify the likelihood of realisation of each opportunity to allow the staff to optimise their marketing effort. Also, this model could also be leveraged to enhance the intelligence of the online platform when promoting opportunities. This is to answer the second question from AIESEC which is listed in the background below.

This repository will present the end-to-end machine learning process for the proof-of-concept of this recommendation.

The whole process will be a combination of R and Python. Since I had a stronger knowledge in business analytics with R(dplyr, ggplot) and machine learning knoweldge with Python (Keras, scikit-learn) by then, I just used the corresponding tools to quickly prototype the model.

# Background
"In January 2019, AIESEC has decided to use the large amount of data it has accumulated over time to help it become more efficient in realizing its mission and to guide its numerical transformation. However, AIESEC does not currently have enough data scientists to assist it on this task. As a result, AIESEC has approached your firm to help them explore and generate value from their data given their current challenges. Your company specializes in business translation for data science and your team of experts has been hired to help AIESEC find solutions using the data they have at their disposal.

AIESEC currently has three main questions it would like you to answer using its data:
1. How to increase the number of exchange opportunities posted by organizations on aiesec.org?
2. How to increase the proportion of posted opportunities that find a suited candidate (realized traineeships)?
3. How to define and measure AIESEC impact on exchange participants leadership?"

# Table of contents
1. IBA_Basic_Data_Processing_v0.1.Rmd
   - Description
     - This script provides basic data processing for the opportunity and application tables. The processed document is further distributed for other teammates analysis and the ML feature engineering.
   - Language: R
   - Contents
     - Data type conversion (e.g. factor -> date)
     - Data filtering (e.g. NA, Null)
     - Table creation (e.g. skills required in a string -> analysis ready table structure)
     - New status creation by mapping to actual application process
     
2. IBA_Exploratory_Data_Analysis_v0.1.Rmd
   - Description
     - This script provides a descriptive analytics and insights on the trends and composition of the data after the basic data processing.
   - Language: R
   - Contents
     - Status analysis
     - Times series visualisation
     - Realisation by different attributes
     
3. IBA_Data_Process_for_Realisation_Prediction_v0.1.Rmd
   - Description
     - This script is for advanced data processing specifically for further ML purpose.
   - Language: R
   - Contents
     - Mapping open data
     - Mapping with industry insight
     - Handling outliers
     - Handling missing values
     - Feature engineering
     
4. Realised_opportunities_prediction_v0.1.ipynb
   - Description
     - This script will perform machine learning on the dataset processed by the third script.
   - Language: Python
   - Contents
     - Correlation analysis
     - One-hot encoding
     - Modelling
       - Multi-layer perception
       - Naive Bayes
       - Decision tree
       - Logistics regression
     - Model evaluation
5. Bay Consulting_Final_compressed.pdf
   - Description
      - The deck used during the final presentation to the senior executives of AIESEC and the panel judges from different tier-1 consulting firms.
