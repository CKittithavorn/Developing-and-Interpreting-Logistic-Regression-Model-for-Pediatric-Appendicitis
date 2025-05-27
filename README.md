# Developing-and-Interpreting-Logistic-Regression-Model-for-Pediatric-Appendicitis
## Objective
Build a model that is both predictive and interpretable.

## Datasets
The dataset used in this project is the **Regensburg Pediatric Appendicitis Dataset**, obtained from [Zenodo](https://zenodo.org/records/7711412), and introduced in [this study](https://arxiv.org/abs/2302.14460v2). It contains ultrasound images depicting various region of interests along with tabular data extracted manually by the experts. These data include physical examination, laboratory, scoring results and ultrasound findings. 
</br></br> For this project, only tabular data was used.

## Methods
### Data Preprocessing
- Missing data:
  * Variables with excessive missingness were removed.
  * Rows of the remaining variables with missing values were removed.
  * The variable Appendix_Diameter was kept despite containing many missing value due to its importance. Instead, the missingness was modeled with another variable.
- Outliers and influential points:
  * Numerical explanatory variables were individually plotted to inspect their distributions. Questionable observations (e.g. body temperature of 27°C) were flagged and removed manually.
- Data splitting:
  * The dataset was split into training and test sets to assess how the model performs on unseen data.
- Feature scaling:
  * Numerial explanatory variables were standardized with mean and standard deviation of the training data.
### Exploratory Data Analysis (EDA)
  * Simple exploratory data analysis was performed to inspect for pattern and see the distribution of data.
  * Empirical logit plot was utilized to check the relationship between the logit of the response variable and numerical explanatory variables.
### Logistic Regression Model
- Fitting the initial model:
  * Some variables are scoring systems (e.g. Alvarado_Score) which contain overlapping information with clinical findings. In this case, variables containing raw data were prioritized.
- Model selection:
  * Backward stepwise regression was performed on the full model, with AIC as the selection criterion.
### Model Diagnostics and Evaluation
- Multicollinearity:
  * Variance Inflation Factor (VIF) was measured for all explanatory variables. 
- Goodness of fit:
  * Hosmer-Lemeshow test was performed to measure how well the models fit the data.
- LRT test:
  * LRT test was performed to compare nested model.
- Prediction:
  * Models were evaluated on the test dataset, and various evaluation metrics were computed.

## Results
Explanatory variables retained in the reduced model align with existing medical knowledge; symptoms such as pain in the lower right abdomen, pain on coughing and nausea remained, along with inflammatory markers like white blood cell (WBC) count and C-reactive protein (CRP). Though the strongest, most important predictor was appendix diameter.
</br></br>The reduced model managed to get the prediction accuracy of 97.2% while the full model (named trimmed model in the code) got 96.6%. This is likely due to stepwise regression removing weak or redundant predictors from the reduced model. 
</br></br>As an experiment, I fitted a model using only clinical and lab findings, while explicitly excluding ultrasound findings. The yielded much lower prediction accuracy at 70.3%, further demostrating how important ultrasound is in diagnosing appendicitis in children.

## Reference
Marcinkevičs, R., Reis Wolfertstetter, P., Klimiene, U., Chin-Cheong, K., Paschke, A., Zerres, J., Denzinger, M., Niederberger, D., Wellmann, S., Ozkan, E., Knorr, C., & Vogt, J. E. (2024). Interpretable and intervenable ultrasonography-based machine learning models for pediatric appendicitis. _Medical image analysis_, 91, 103042. https://doi.org/10.1016/j.media.2023.103042

## Afterthoughts
At first, I thought this would be a straightforward project, but soon realized that there are a lot more nuance to it than I thought. There are many things I learnt while doing this project and many more that I'd like to try out. I'm starting to like coding in R a lot. Statistical model is also very neat, because of how interpretable it is.
