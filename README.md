# Does Increasing the Advertising Budget Have a Statistically Significant Effect on Sales?

*Using regression and the inferential tools from descriptive and inferential statistics, I test this hypothesis and let the evidence decide.*

**Author:** Nitesh Talukdar
**Role (project framing):** Marketing Data Scientist
**Dataset:** [Google Ads, Data Analytics Course Sales (Kaggle)](https://www.kaggle.com/datasets/nayakganesh007/google-ads-sales-dataset)

---

## About this project

I worked through this project as if I were the marketing data scientist at a company that sells a Data Analytics course through Google Ads. The marketing team spends money on ads every quarter, and they wanted an answer to one simple question:

> If we spend more money on ads, do we actually get more sales?

So my goal was to look at the data and find out if there is a real connection between how much we spend (`Cost`) and how much we sell (`Sale_Amount`), and to test that properly instead of guessing.

## My hypothesis

- **H0 (null):** The ad budget has no effect on sales.
- **H1 (alternative):** The ad budget does have an effect on sales.

I wrote these down before looking at any results, so that I would let the evidence decide the answer.

## The short answer

I **fail to reject H0**. Based on this data, increasing the advertising budget does **not** have a statistically significant effect on sales. The key result from the regression was a **p-value of 0.598** (far above the 0.05 cutoff) and an **R-squared of 0.000**.

This is a real and useful finding. A "no effect" answer is just as valuable to a business as a "yes" answer, because it stops the company from spending more money on something that does not work.

---

## What I did, step by step

1. **Loaded and inspected the data** to spot problems before touching anything.
2. **Cleaned the data:**
   - Removed the `$` sign from `Cost` and `Sale_Amount` and turned them into real numbers.
   - Fixed the `Ad_Date` column, which had dates in several different formats.
   - Tidied the messy text columns (`Device`, `Location`, `Campaign_Name`).
   - Handled the missing values.
3. **Looked at descriptive statistics** to understand the spread of each column.
4. **Made a scatter plot** of budget against sales to see the relationship with my own eyes.
5. **Measured the correlation** between budget and sales, then between all the numeric columns using a heatmap.
6. **Ran a formal linear regression** to test the hypothesis with a p-value.
7. **Wrote an honest business conclusion** with recommendations for what to do next.

## How I handled the data cleaning decisions

A few choices in this project were judgment calls, so here is my reasoning:

- **Missing values:** I dropped the rows that were missing `Sale_Amount` or `Cost`, because those are the target and the main predictor, and I did not want to invent values for them. For the supporting columns I filled the gaps with the **median**, since the median is steadier than the mean when data is messy. The dataset started with 2600 rows and ended with 2366 clean rows, so I still had a large sample.
- **Text columns with one real value:** Both `Location` and `Campaign_Name` turned out to have only one true value each (Hyderabad, and the Data Analytics Course). This told me the data covers a single campaign in a single city, which is an important limit on what the analysis can say.

## What the evidence showed

Every step pointed to the same answer:

| Evidence | Result | Meaning |
|---|---|---|
| Scatter plot | A flat, shapeless cloud | No visible trend |
| Correlation (r) | About 0.011 | Almost no linear link |
| Regression p-value | 0.598 | Not statistically significant |
| R-squared | 0.000 | Budget explains almost none of the change in sales |

I also checked every other feature (clicks, impressions, leads, conversions) and none of them had a meaningful link with sales either. So this is not a case of picking the wrong input. The sales in this dataset seem to be driven by something that was not captured in the data at all.

## Why I stopped where I did

I imported scikit-learn at the start because I planned to also build a predictive model. But once the regression showed no real relationship, building a predictive model would only confirm that it cannot predict sales, which I already knew. So I made the deliberate choice to stop rather than add code that would give no new insight. Knowing when to stop is part of doing this well.

## What I would recommend to the business

- Do not assume that raising the ad budget will raise sales. There is no evidence for it here.
- Collect richer data that might actually explain sales, such as product price, customer type, season, or ad creative quality.
- Run a controlled A/B test, raising the budget for one group and keeping it steady for another, to get cleaner evidence than this observational data can give.

---

## Tools used

- **Python**
- **pandas**, **numpy** for handling and cleaning the data
- **matplotlib**, **seaborn** for the charts
- **statsmodels** for the regression and the significance test
- **scipy** for supporting statistics

## How to run this

1. Download the dataset from the Kaggle link above.
2. Place the CSV file in the same folder as the notebook.
3. Open the notebook in Jupyter and run the cells from top to bottom (Kernel > Restart and Run All).

## Files in this repo

- `Does_Increasing_the_Advertising_Budget_Have_a_Statistically_Significant_Effect_on_Sales.ipynb` — the full analysis notebook.
- `GoogleAds_DataAnalytics_Sales_Uncleaned.csv` — the raw dataset (or download it from Kaggle).
- `README.md` — this file.

---

*This project was built as a portfolio piece to practice the full data analysis pipeline: cleaning, exploring, and testing a hypothesis honestly, and reporting the result whatever it turned out to be.*
