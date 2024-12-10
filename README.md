# A Data-Driven Approach to Waterpoint Functionality and Accessibility

##  Table of Contents
1. [Business Overview](#Business-understanding)
2. [Business Understanding](#Why-It-Matters)
3. [Stakeholders](#Key-Stakeholders)
4. [Success criteria](#Expected-Outcome)
5. [Data Understanding](#Data-Understanding)
6. [EDA](#Exploratory-Data-Analysis)
7. [Data Visualisations](#Data-Visualisations)
8. [Model Performance](#Model-Performance)
9. [model choice](#model-choice)
10. [Recommendations](#Recommendations)
11. [Thank You](#THANK-YOU)

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


## Exploratory Data Analysis

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

The very high Chi-square statistic (902.8940071619397) and extremely small p-value(1.472005828590181e-188) and a degree of freedom of 9 suggest a strong association between the two categorical variables funder and status group.

The largest contributors to the Chi-square statistic are likely Government of Tanzania, DANIDA, and Private Individual, given their high absolute counts and discrepancies between functional and non-functional water points.

Insights:

Funders like Government of Tanzania and HESAWA may require further analysis to understand why their non-functional water points are so high despite large investments.
Private Individuals might benefit from technical or financial support to improve their success rate in maintaining functional water points.
Focus on funders with a higher proportion of functional water points (e.g., DANIDA ) could offer insights into best practices.






[Tableu Visualization](https://public.tableau.com/views/Waterboreholes_Tz/Sheet1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
