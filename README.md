# International Business Analytics (IBA) Challenge - Opportunity Realization Prediction
Participants of IBA Challenge are required to propose recommendations on how to leverage the wealth of data in AIESEC for its digital transformation journey to achieve its business goals.

One of the recommendation will be leveraging machine learning to quantify the likelihood of realisation of each opportunity to allow the staff to optimise their marketing effort. Also, this model could be leveraged to enhance the intelligence of the online platform when promoting opportunities. This is to answer the second question from AIESEC which is listed in the background below.

This repository will present the end-to-end machine learning process for the proof-of-concept of this recommendation.

The whole process will be a combination of R and Python. Since I had a stronger knowledge in business analytics with R(dplyr, ggplot) and machine learning knoweldge with Python (Keras, scikit-learn) by then, I just used the corresponding tools to quickly prototype the model.

# Background
"In January 2019, AIESEC has decided to use the large amount of data it has accumulated over time to help it become more efficient in realizing its mission and to guide its numerical transformation. However, AIESEC does not currently have enough data scientists to assist it on this task. As a result, AIESEC has approached your firm to help them explore and generate value from their data given their current challenges. Your company specializes in business translation for data science and your team of experts has been hired to help AIESEC find solutions using the data they have at their disposal."

AIESEC currently has three main questions it would like you to answer using its data:
1. How to increase the number of exchange opportunities posted by organizations on aiesec.org?
2. How to increase the proportion of posted opportunities that find a suited candidate (realized traineeships)?
3. How to define and measure AIESEC impact on exchange participants leadership?

The second question translates to a binary classification problem of whether an opportunity is predicted to be realized or not.

# Problem Identification

After inteviewing with the local AIESEC committee, we found out that the local committee will be selected yearly and they will usually be composed of the year 2 students. When they are making decisions on which opportunity to promote, it will be based on their one year experience in AIESEC. Therefore, the machine learning approach is recommended to leverage the 15 years+ data to allow the local committee to make informed data-driven decisions.

# Dataset

**Opportunities table**

Each row corresponds to an opportunity posted on aiesec.org. An opportunity can correspond to several similar internships.

**Opportunities application table**

Each row corresponds to an exchange participant application on an opportunity.

# Data Insights - EDA

Some interesting insights from the opportunities and applications tables.

### **Opportunities**

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Opportunity_by_programmeid.png)

**Observations**

The number of "Global Volunteer" and "Global Entrepreneur" increases significantly. The number of "Global Talent" keeps at a moderate pace.

**Comments**

We can partner with more startups for more opportunities in "Global Entrepreneur" programme as we can see there is a upward trend starting from 2015. We can keep explore opportunities in "Global Volunteer".


![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Opportunity_by_region.png)

**Observations**

Middle East and Africa and Asia Pacific contribute a significant amount in the increase of the opportunities.

There is a trend that opportunities will usually peak after the start of the year and after the mid-year.

**Comments**

As both Asia Pacific and Middle East and Africa are experiencing strong growth now, we can keep explore the opportunities in the regions.

### **Application**

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/application_by_region.png)

**Observations**

Most people apply for Europe opportunities, followed by America, Asia Pacific and Middle East and Africa. Across the regions, the trends are similar.

**Comments**

This aligns to my general understanding as this correlates to the popularity of travelling for each region.

### **Realization**

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/realization_by_programmeid.png)

**Observations**

global volunteer has the highest realized rate followed by global talent and entreprenuer.

**Comments**

From the data insight, there are two potential directions for improvements. On the one hand, increasing the number of global volunteer opportunities will yield more realizaed opportunities. On the other hand, the marketing effort could be put in promoting the other two programmes as high quality experience to students to improve the realization rate.

# Modelling Results
For this binary classification problem, majority classifier is taken as a baseline for benchmarking and the baseline accuracy is 59.7%.

After training with 4 models, deep learning yields the highest accuracy of 68.7%.

**Model Basics**

Data Set Shape: (381484, 160)

Regularization: L2 and Dropout

Activation Function: Hidden Layer: Relu, Output Layer: Sigmoid

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Deep_Learning_Model_Architecture.PNG)

**Hyperparameter Tuning**

4 Hyperparameters are selected for performing grid search.

Only a sub-set (50000) of the training set is selected to perform hyperparameter tuning.

-------------------------------------------------------------------------------------------------

batch_size = [32, 64, 128, 256]

epochs = [10, 20]

init_mode = ['uniform', 'normal', 'glorot_normal', 'glorot_uniform']

dropout = [0.1, 0.3, 0.5]

-------------------------------------------------------------------------------------------------

The best performing configuration is used for training the model.

{'batch_size': 256, 'dropout': 0.5, 'epochs': 20, 'init_mode': 'glorot_normal'}

**Accuracy Score**

Deep Learning: 68.7%

Naive Bayes: 62.11%

Decision Tree: 68.48%

Logistics regression: 65.97%

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Deep_Learning_Accuracy.PNG)
![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Deep_Learning_Loss.PNG)

By looking at the training results, we can observe that the model doesn't suffer from overfitting problem since both the accuracy and loss don't bounce back.

**Confusion Matrix**

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Deep_Learning_Confusion_Matrix.PNG)

**ROC Curve**

![alt text](https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/Graphics/Deep_Learning_ROC.PNG)

**Model Usage**

Sigmoid function is used as the output function which the range will be 0-1. The score will be served to measure the attractiveness of each opportunity and the local marketing team could leverage this model to prioritise their marketing efforts with 15 years+ of data.

# Future Enhancement

**Status Mapping Enhancement**

For the current opportunity status creation, it's embedded into the program logic. This is a quick and dirty way of data processing but not the most flexible practice. After working for a large scale ETL project, the best approach would be setting aside the frequently udpated mapping as separate configuration tables to allow flexiblity and expandability to the program design.

**Backgrounds, Skills and Languages Processing**

Due to time constraint, only the required background is processed for modelling. The unstructured nature of the features makes it hard for a quick prototype. Yet, the skills and languages are important features which could help classify the uniqueness of each opportunity and hence improve the model performance.

**Web API Deployment**

Flask API could be further developed to enable a more interactive and realistic POC to showcase to the clients on how the model could help with the current operation.

# Table of contents
**1. IBA_Basic_Data_Processing_v0.1.html**
   - Description
     - This script provides basic data processing for the opportunity and application tables. The processed document is further distributed for other teammates analysis and the ML feature engineering.
   - Rendered Markdown
      - https://htmlpreview.github.io/?https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/1.%20IBA_Basic_Data_Processing_v0.1.html
   - Language: R
   - Contents
     - Data type conversion (e.g. factor -> date)
     - Data filtering (e.g. standardized time range)
     - Data Cleansing (e.g. NA, Null)
     - Table creation (e.g. skills required in a string -> analysis ready table structure)
     - New status creation by mapping to actual application process
 
**2. IBA_Exploratory_Data_Analysis_v0.1.html**
   - Description
     - This script provides a descriptive analytics and insights on the trends and composition of the data after the basic data processing.
   - Rendered Markdown
      - https://htmlpreview.github.io/?https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/2.%20IBA_Exploratory_Data_Analysis_v0.1.html
   - Language: R
   - Contents
     - Status analysis
     - Times series visualisation
     - Realisation by different attributes
     
**3. IBA_Data_Process_for_Realisation_Prediction_v0.1.html**
   - Description
     - This script is for advanced data processing specifically for further ML purpose.
   -  Rendered Markdown
      - https://htmlpreview.github.io/?https://github.com/klwangaa/IBA-Challenge-Opportunity-Prediction/blob/main/3.%20IBA_Data_Process_for_Realisation_Prediction_v0.1.html
   - Language: R
   - Contents
     - Mapping open data
     - Mapping with industry insight
     - Handling outliers
     - Handling missing values
     - Feature engineering
     
**4. Realised_opportunities_prediction_v0.1.ipynb**
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

**5. Bay Consulting_Final_compressed.pdf**
   - Description
      - The deck used during the final presentation to the senior executives of AIESEC and the panel judges from different tier-1 consulting firms.
