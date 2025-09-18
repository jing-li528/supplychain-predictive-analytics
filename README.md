### Project Title 
**Predicting Shipment Delivery Time for the Shipping Optimization Challenge**

**Author**
Jing Li

#### Executive summary
This project aims to predict **shipping time** for shipments based on their attributes — such as route, mode (Air/Ocean), weight, cost, and shipping company details. Using the Kaggle Shipping Optimization Challenge dataset, I performed data cleaning, feature engineering, and exploratory data analysis (EDA) to understand key drivers of shipping time. Early results show that **shipment mode** (Air vs. Ocean) and **route/company combinations** are the dominant predictors, with significant differences in average transit time and variance. This sets the foundation for building predictive models that can improve estimated times of arrival (ETAs) and help logistics teams make better planning decisions.

#### Rationale
Accurate shipment time predictions are crucial for logistics companies. Overly optimistic ETAs can lead to missed service-level agreements (SLAs), customer dissatisfaction, and added operational costs, while overly conservative ETAs may reduce competitiveness. Understanding which factors drive shipping time enables businesses to proactively manage routes, allocate capacity, and set realistic customer expectations — ultimately improving efficiency and customer trust.

#### Research Question
Can we accurately predict shipment delivery time based on shipment characteristics (route, mode, cost, weight, company, etc.) so that we can provide reliable ETAs and optimize logistics planning?

#### Data Sources
The primary data source is the **[Shipping Optimization Challenge dataset on Kaggle](https://www.kaggle.com/datasets/salil007/1-shipping-optimization-challenge)**.  
- **Training data:** Shipment-level records with columns such as `shipment_mode`, `pick_up_point`, `drop_off_point`, `source_country`, `destination_country`, `freight_cost`, `gross_weight`, `shipment_charges`, `shipping_company`, and the target `shipping_time`.  
- **Company details file:** Enrichment data with cut-off times, processing days, turnaround times, and capacity bands for each company/route combination.  

#### Methodology
1. **Data Cleaning:**  
   - Removed whitespace from categorical columns, coerced numerics, and parsed `send_timestamp` into year, month, day, and hour.  
   - Merged training data with company details file on `(shipping_company, pick_up_point, drop_off_point)` to add operational features.

2. **Exploratory Data Analysis (EDA):**  
   - Examined target distribution (`shipping_time`) → multimodal with Air clustered near 5 days and Ocean around 20–25 days but with longer tails.  
   - Analyzed missingness patterns and confirmed sufficient data coverage for key fields.  
   - Created visualizations: histograms, boxplots by `shipment_mode`, scatterplots vs. `gross_weight` and `freight_cost`.  
   - Produced grouped statistics by route, company, and mode to surface key drivers of variability.

#### Results
Key findings from EDA:
- **Shipment Mode is the strongest driver** — Air shipments are tightly clustered (~5 days), while Ocean shipments are much slower and have wider variance.  
- **Route & Company combinations matter** — e.g., Ocean shipments from `A→Y` via SC1 have average times near 20 days, but with a long tail, suggesting operational variability.  
- **Numeric drivers (gross_weight, freight_cost)** show weaker but noticeable correlation with shipping time, suggesting larger/heavier shipments can have slightly longer transit.  
- Missing values are minimal for most key features, so data is relatively clean for modeling.

#### Next steps
- **Feature Engineering:** Convert `cut_off_time`, `tat`, and `processing_days` into numerical or categorical features (e.g., weekday flags, minutes past midnight).  
- **Modeling:** Build baseline supervised regression models (Linear Regression, Random Forest, XGBoost) to predict `shipping_time`.  
- **Advanced Approaches:** Explore separate models for Air vs. Ocean shipments, or interaction features between route and company.  
- **Performance Metrics:** Evaluate models using MAE, RMSE, and P50/P90 prediction intervals to assess ETA accuracy and reliability.  
- **Business Alignment:** Define operational KPI such as “% of orders predicted within ±12h of actual time” to translate model accuracy into business value.

#### Outline of project
https://github.com/jing-li528/supplychain-predictive-analytics/blob/main/capstone_initial_EDA.ipynb


##### Contact and Further Information
jing.li5282013@gmail.com
