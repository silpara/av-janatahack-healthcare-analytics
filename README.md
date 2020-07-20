# Analytics Vidhya JanataHack Healthcare Analytics

I secured 66th rank in the competition and the final model was an xgboost model trained on data with many additional features constructed on dates. The performance is obviously not so great, so I looked at what I missed in the competition. 

Here are my learnings:

1. **Train-Eval Split**: I split train and eval randomly but since test data was out-of-time, out-of-time eval was a better strategy here. Max of Camp_Start_Date in train is 2006-03-30 and min of Camp_Start_Date in test is 2006-04-02. This should have been a clear signal to do out-of-time split. I didnt pay attention to it in the heat of tuning the next model.
2. **Explicit Regularization**: On a few submissions, post competition, I discovered that explicit L1, L2 regularization improved the scores.
3. **Blend-Blend-Blend**: Or Ensemble-Ensemble-Ensemble or Stack-Stack-Stack. I usually dont do blending of models in any competition. This is because in my work has been deployment focussed which is almost always a single model. But I guess Ive to let go of this a bit and work on model blending approaches for better performance in competitions.

Final version of the model I submitted is shared in this repo. 


## Description Of Problem
Given historical data of patients and health camps, predict whether a patient will go to a camp or not.


## Evaluation
The evaluation metric was AUC.


## Data
Data can be downloaded from the contest page [Janatahack: Healthcare Analytics - Problem Statement](https://datahack.analyticsvidhya.com/contest/janatahack-healthcare-analytics/#LeaderBoard)


### Fields in data

**Train & Test**
- Patient_ID
- Health_Camp_ID
- Registration_Date
- Var1
- Var2
- Var3
- Var4
- Var5


**Health Camp Detail**
- Health_Camp_ID
- Camp_Start_Date
- Camp_End_Date
- Category1
- Category2
- Category3


**Patient Profile**
- Patient_ID
- Online_Follower
- LinkedIn_Shared
- Twitter_Shared
- Facebook_Shared
- Income
- Education_Score
- Age
- First_Interaction
- City_Type
- Employer_Category


**First Health Camp Attended**
- Patient_ID
- Health_Camp_ID
- Donation
- Health_Score


**Second Health Camp Attended**
- Patient_ID
- Health_Camp_ID
- Health Score


**Third Health Camp Attended**
- Patient_ID
- Health_Camp_ID
- Number_of_stall_visited
- Last_Stall_Visited_Number


**Submission**
- Patient_ID
- Health_Camp_ID
- Outcome (to be predicted, a score between 0-1)


**Additional Features Constructed**
- Registration_weekday
- Registration_weekofyear
- Registration_month
- Registration_quarter
- Registration_year
- Camp_Start_Date_weekday
- Camp_Start_Date_weekofyear
- Camp_Start_Date_month
- Camp_Start_Date_quarter
- Camp_Start_Date_year
- Camp_End_Date_weekday
- Camp_End_Date_weekofyear
- Camp_End_Date_month
- Camp_End_Date_quarter
- Camp_End_Date_year
- First_Interaction_weekday
- First_Interaction_weekofyear
- First_Interaction_month
- First_Interaction_quarter
- First_Interaction_year
- interation_to_registration
- camp_duration
- camp_weeks
- registration_to_camp_start
- attended_before
- attended_before_flag


## Models
[XGBoost](https://github.com/silpara/av-janatahack-healthcare-analytics/blob/master/xgb-av-janatahack-healthcare-analytics-final-submission.ipynb)
The experimentation largely involved adding features to the model and tuning it for best results on eval set. Model tuning code is not included in the notebook.


## Approach for Best Performing Model
The best performing model for me was xgboost. The training process is as follows:
- **Train-Eval Split:** Random split for train and eval.
- **Training:** Trained xgboost with early stopping on eval set.
- **Final Model:** Trained final model on full data with best iterations learned in previous step.



PS: I write about Data Science, Machine Learning and AI at [dilbertai.com](https://www.dilbertai.com), where I share ideas and concepts I have learned over the course of my work, summarize research papers I read and practical knowledge I have gained from use cases I have worked on.

