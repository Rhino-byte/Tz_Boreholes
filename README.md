# A Data-Driven Approach to Waterpoint Functionality and Accessibility

##  Table of Contents
1. [Business Overview](#Business-understanding)
2. [Business Understanding](#Why-It-Matters)
3. [Stakeholders](#Key-Stakeholders)
4. [Success criteria](#Expected-Outcome)
5. [Data Understanding](#Data-Understanding)
6. [EDA](#Exploratory-Data-Analysis🔍🧐)
7. [Modeling 🤖🚀](#Modeling)
8. [Model Performance](#Model-Performance)
9. [model choice](#Model-Comparison)
10. [Recommendations](#Recommendations)
11. [Personal Info](#Links)

![image](https://github.com/user-attachments/assets/a68f7cf9-2cdc-45ed-86e5-b109ef0e7302)

## Business understanding
**Objective**:
The primary business goal is to predict the operational status of waterpoints in Tanzania, classifying them into one of two categories:

1. Functional - Fully operational and providing water as intended.
2. Non-functional - Not operational and failing to provide water.

## *Why It Matters:*
1. *Efficient Resource Allocation:*
Predicting waterpoint conditions allows stakeholders (The Tanzanian Ministry of Water, NGOs) to allocate resources efficiently by prioritizing repairs and maintenance.
2. *Improved Accessibility to Water:*
Ensuring functional water points in rural and urban areas is crucial for providing clean water to communities, improving public health, and reducing waterborne diseases.
3. Cost Optimization:
Proactively predicting failures can prevent unnecessary repair costs, and funds can be channeled to more critical interventions.
4. *Sustainability:*
Understanding patterns in failures helps in better planning for future installations, improving waterpoint durability.

---

## *Key Stakeholders:*
- Government Agencies (Tanzanian Ministry of Water): Responsible for policy-making and infrastructure maintenance.
-NGOs and Charities: Focused on improving access to clean water.
-Local Communities: Beneficiaries of operational waterpoints.
-Donors and Funders: Interested in the impact of their investments in water infrastructure.

---

**Problem Description:**
The dataset provides various features that capture the physical attributes, installation details, geographic location, and usage patterns of the water points. These variables can help answer questions such as:

1. What factors contribute most to waterpoint failures?
2. Are certain geographic areas more prone to non-functional water points?
3. How do management and funding affect waterpoint longevity?
4. Can the age of a waterpoint (construction year) predict its condition?

## **Expected Outcome:**
A machine learning model that:
- Accurately predicts the operational status of a waterpoint.
- Key factors affecting functionality.
- Provides actionable insights for maintaining and repairing water points.

*Potential Challenges:*
a) Data Quality: Missing or inconsistent entries in key variables (e.g., funder, construction year).

b) Class Imbalance: If most water points are functional, predicting minority classes (e.g., non-functional) can be challenging.

c) Geographic and Temporal Variability: Different regions may have unique issues (e.g., drought, poor maintenance) that complicate predictions.

d) Interpretability: Translating complex model outputs into actionable insights for stakeholders.

*Key Deliverables:*
1. **Classification Model:** A robust algorithm to predict waterpoint status.
2. **Feature Analysis Report:** Insights into which factors most influence waterpoint conditions.
3. **Dashboard or Visualization Tools:** To enable stakeholders to view and act on predictions and insights.


## Data Understanding
The data used in this project is from the [Taarifa Competition](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/data/)

Data Understanding The comes from Driven Data - Tanzanian Water Wells

The data did not contain duplicates but it had missing values the majority of which were categorical columns measures taken were to impute the missing values to retain other rows containing information that was useful in the exploratory data analysis and modeling section.


## Exploratory Data Analysis🔍🧐

1. visualized the distribution of water wells and their status

![image](https://github.com/user-attachments/assets/64a98ef6-d993-41fc-9224-23a0732e5115)

2. Visualized water quality from the different water wells

![water_quality](https://github.com/user-attachments/assets/d269141c-32ab-4010-a909-fc3a55d5fd89)

3. Visualizing the key stakeholders who funded the establishment of the water pump

![image](https://github.com/user-attachments/assets/164460ef-18f7-4229-add8-79e0773ab3ad)

The bar chart displays the functionality status of waterpoints across different funders. Among the funders, the **Government of Tanzania** is the largest contributor, supporting over 8,000 waterpoints, with more than half (4,663) being non-functional. **Danida** and **Hesawa** follow as significant contributors, with Danida showing a higher proportion of non-functional water points (1,242 functional vs. 1,713 non-functional). **World Vision** and **World Bank** have a relatively balanced split between functional and non-functional waterpoints, while smaller contributors like **Private Individuals** and **Unicef** demonstrate a higher number of functional waterpoints compared to non-functional ones. This suggests that while the Government of Tanzania contributes heavily to waterpoints, the functionality rate under its funding is relatively lower compared to other funders.

To further determine what association exists between the funders and the functionality of a water pump a chi-square test was performed to test the whether the association exists.
```{python}
# chi-square test
from scipy import stats

crosstab= pd.crosstab(plot_data['funder'],plot_data['status_group'])
print(stats.chi2_contingency(crosstab))
```
*Outputs:*

- A Chi-square statistic (902.8940071619397), an extremely small p-value(1.472005828590181e-188), and a degree of freedom of 9 suggest a strong association between the two categorical variables funder and status group.
- The largest contributors to the Chi-square statistic are likely the Government of Tanzania, DANIDA, and Private Individuals, given their high absolute counts and discrepancies between functional and non-functional water points.

**Insights:**

Funders like the Government of Tanzania and HESAWA may require further analysis to understand why their non-functional water points are so high despite large investments.
Private Individuals might benefit from technical or financial support to improve their success rate in maintaining functional water points.
Focus on funders with a higher proportion of functional water points (e.g., DANIDA ) could offer insights into best practices.


## Modeling

For this section, since we were working with a classification problem the following models were used:
1. *` Logistic models`*
2. *`Decision Trees`*
3. *` Convolution Neural Network`*

**Why This Combination of Models?**
Using a combination of these models ensures a robust analysis:

- *Baseline to Advanced Progression:* Logistic regression serves as a baseline, decision trees handle non-linear relationships, and CNNs explore complex spatial dependencies.
- *Interpretability vs. Complexity Trade-off:* Logistic regression and decision trees offer interpretability, which is crucial for stakeholder understanding, while CNNs provide advanced, potentially higher-performing solutions.
- *Flexibility:* This variety ensures the best fit for the dataset, as the characteristics of the data will determine which model performs best.

This approach balances simplicity, interpretability, and advanced techniques, providing a comprehensive analysis of water pump functionality.


## **Model Comparison**
Since our response variable contains imbalanced classes

![image](https://github.com/user-attachments/assets/f0267309-2711-4cc4-9958-532616d8f96d)

Balancing the classes was tackled by using *SMOTE-NC (Nominal Continuous)* which takes into account when most of the variables in the data are categorical variables.
Also, we will use the F1_score as the metric to measure our model's performance on predicting the classes and other evaluation techniques.
Fine-tuning was necessary to ensure the models were optimized to their best performance while addressing issues like overfitting in the model.

![image](https://github.com/user-attachments/assets/d93bb94e-ec2d-49e6-8213-2b86cdd1c4b9)

The bar chart compares the **F1 scores** of four models used in the classification of water pump functionality: Logistic Regression, Decision Trees (Gini and Entropy), and a Convolutional Neural Network (CNN). 

- The **Decision Tree (Gini)** model achieved the highest F1 score of **73.59%**, slightly outperforming the **Decision Tree (Entropy)** model, which had an F1 score of **72.90%**.
- The **CNN model** followed closely with an F1 score of **72.26%**, demonstrating strong performance despite its complexity.
- The **Logistic Regression** model had the lowest F1 score at **70.10%**, indicating it may not handle non-linear relationships as effectively as the other models.

Overall, the Decision Tree models performed the best, with Gini slightly outperforming Entropy, while the CNN showed competitive results, making it a viable option for more complex patterns. Logistic Regression serves as a good baseline but falls short compared to the others.

![image](https://github.com/user-attachments/assets/2c51ee62-7edf-4041-949a-cdda335aa07e)

**Overall Comparison:**
Models with higher AUC values are better at distinguishing between classes.
- Tree_Gini and Tree_Entropy, with the highest AUC values (0.78), are the best-performing models.
- Logistic regression is the weakest among the models but still acceptable for classification tasks.
- The CNN model is competitive but slightly underperforms compared to the decision tree models.

Based on the F1_score comparison and the ROC_AUC curve I chose the best model as the decision tree using the gini impurities.🥳🥳

To evaluate how the best model performed we will use a confusion matrix
![image](https://github.com/user-attachments/assets/caf4392b-6913-4f5b-9786-356a6b044a35)

**Interpretation:**

**Strengths:** The model performs well in predicting functional items (high true negative rate, 86.6%).
**Weaknesses:** It struggles more with predicting non-functional items, as indicated by a lower recall (69.7%) and a significant false negative count (30.3%).


We can also investigate the top ten performing features in our model. To help our stakeholders capitalize on them to improve pump functionality

![image](https://github.com/user-attachments/assets/b4650e62-c221-4965-a6fb-e6765eeb7061)

**Summary of Insights**

1. Water-related metrics (`quantity_enough`, `quantity_insufficient`, `quantity_seasonal`, and `amount_tsh`) dominate as predictors, highlighting the importance of consistent water supply and flow.
2. Geographic and demographic factors (`gps_height`, `population`, `basin_Lake Victoria`) suggest that environmental and community characteristics play a secondary role.
3. The age of the infrastructure (`decades`) reflects the need for maintenance and modernization.

## Recommendations

1. **` Water Management`:** Prioritize consistent water availability, as the most critical features relate to quantity and seasonality.
2. **`Maintenance Plans`:** Develop targeted maintenance programs for older wells to improve their functionality.
3. **`Regional Focus`:** Investigate wells in the Lake Victoria basin or at extreme elevations to address location-specific challenges.
4. **`Design Optimization`:** Evaluate the least functional water point types under "other" and address design or maintenance shortcomings.
5. **` Population Alignment`:** Ensure wells are appropriately scaled for the population they serve.




## Links

[Tableu Visualization](https://public.tableau.com/views/Waterboreholes_Tz/Sheet1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

[Slides Presentation](https://docs.google.com/presentation/d/1K9nwBTftBDnsCaEZc9Y6jvbgYhUNl60bXdDqdYcrc94/edit?usp=sharing)

For queries or support, reach out via :

Email📩: savinskamau01@gmail.com

LinkedIn: [Savins Nanyaemuny](https://www.linkedin.com/in/nsavins/)

Thanks for your time🙂‍↕️
