# Ecommerce Customer Data Analysis Project

This project explores an ecommerce customer dataset to understand customer value, engagement behavior, purchase patterns, review sentiment, and data quality risks. The analysis is built as a Python/Jupyter workflow and is intended to turn raw customer-level data into practical business insights for retention, marketing, and customer experience decisions.

## Business Questions

The project is organized around these questions:

- Which customer behaviors are most associated with higher lifetime value?
- How do engagement signals such as login frequency, session duration, email open rate, wishlist items, and cart abandonment relate to customer value?
- Are there customer segments, such as gender, age group, membership tenure, or purchase frequency, that show materially different outcomes?
- What data quality issues may affect the reliability of the analysis?
- What review sentiment patterns are visible, and how might they connect to customer value or experience?

## Dataset

The dataset used in this project is:

```text
Dataset/ecommerce_customer_dataset_with_reviews.csv
```

Current dataset size:

```text
50,000 rows
25 columns
```

Each row represents one customer record with profile information, ecommerce engagement behavior, purchase activity, account status, and review text.

Key column groups:

- Customer profile: `Age`, `Gender`, `Country`, `City`, `Membership_Years`, `Signup_Quarter`
- Engagement behavior: `Login_Frequency`, `Session_Duration_Avg`, `Pages_Per_Session`, `Wishlist_Items`, `Email_Open_Rate`, `Social_Media_Engagement_Score`, `Mobile_App_Usage`
- Purchase behavior: `Total_Purchases`, `Average_Order_Value`, `Lifetime_Value`, `Discount_Usage_Rate`, `Cart_Abandonment_Rate`, `Days_Since_Last_Purchase`
- Service and risk signals: `Returns_Rate`, `Customer_Service_Calls`, `Credit_Balance`, `Churned`
- Text data: `Reviews`

Countries represented in the dataset:

```text
Australia, Canada, France, Germany, India, Japan, UK, USA
```

## Project Structure

```text
.
├── Data processing/
│   └── ecommerce data analysis_Sheldon.ipynb
├── Dataset/
│   └── ecommerce_customer_dataset_with_reviews.csv
├── outputs/
│   ├── PPT_ecommerce_customer_analysis_Sheldon.pdf
│   ├── PPT_ecommerce_customer_analysis_Sheldon.pptx
│   └── ecommerce_ppt/
│       ├── analysis_summary.json
│       ├── charts/
│       └── preview/
├── .gitignore
└── README.md
```

Notes:

- `Data processing/ecommerce data analysis_Sheldon.ipynb` is the main analysis notebook.
- `Dataset/ecommerce_customer_dataset_with_reviews.csv` is the source dataset currently committed to the repository.
- `outputs/` contains generated charts, presentation files, previews, and summary artifacts. These are local generated outputs and are ignored by Git.
- `AGENTS.md` contains local agent instructions and is ignored going forward.

## Tools And Libraries

The analysis notebook uses Python with the following main libraries:

- `pandas` for data loading, cleaning, aggregation, and tabular analysis
- `numpy` for numeric operations
- `matplotlib` and `seaborn` for visualization
- `nltk` and `SentimentIntensityAnalyzer` for review sentiment analysis

Suggested setup:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install pandas numpy matplotlib seaborn nltk jupyter
```

If the sentiment analysis cell needs the VADER lexicon, run this once in Python:

```python
import nltk
nltk.download("vader_lexicon")
```

## How To Run The Analysis

From the project root:

```bash
jupyter notebook
```

Then open:

```text
Data processing/ecommerce data analysis_Sheldon.ipynb
```

Recommended workflow:

1. Load the dataset.
2. Confirm row grain and column types.
3. Check missing values, duplicate rows, invalid values, and outliers.
4. Explore distributions for customer profile, engagement, purchase behavior, and value metrics.
5. Compare lifetime value across customer groups and behavioral segments.
6. Review correlations between numeric variables and `Lifetime_Value`.
7. Analyze review sentiment using NLTK VADER.
8. Convert findings into business recommendations with limitations clearly stated.

## Data Quality Notes

Initial quality checks found:

- Duplicate rows: `0`
- Several columns contain missing values, especially:
  - `Social_Media_Engagement_Score`: about 12%
  - `Credit_Balance`: about 11%
  - `Mobile_App_Usage`: about 10%
  - `Returns_Rate`: about 9%
  - `Wishlist_Items`: about 8%
- Some invalid or suspicious values were flagged:
  - `Age > 100`: 20 rows
  - `Age < 18`: 30 rows
  - `Cart_Abandonment_Rate > 100%`: 30 rows
  - `Discount_Usage_Rate > 100%`: 207 rows
  - High-end outliers in `Average_Order_Value` and `Lifetime_Value`

These issues should be interpreted before removing or transforming records. For example, unusually high lifetime value may represent either valid VIP customers or data errors, so it should not be deleted automatically.

## Analysis Highlights

Based on the generated analysis summary:

- Median customer age is about 38.
- Median membership tenure is about 2.5 years.
- Median average order value is about 112.97.
- Median lifetime value is about 1,243.42.
- Raw churn rate is about 28.9%.
- Review sentiment is mostly positive:
  - Positive: about 74.4%
  - Neutral: about 7.6%
  - Negative: about 18.0%

Top observed correlations with `Lifetime_Value`:

| Feature | Correlation With Lifetime Value |
|---|---:|
| `Total_Purchases` | 0.623 |
| `Session_Duration_Avg` | 0.542 |
| `Pages_Per_Session` | 0.515 |
| `Login_Frequency` | 0.499 |
| `Cart_Abandonment_Rate` | -0.495 |
| `Email_Open_Rate` | 0.460 |
| `Wishlist_Items` | 0.459 |
| `Customer_Service_Calls` | -0.295 |

These are associations, not proof of causation. They are useful for prioritizing deeper analysis, customer segmentation, and business experiments.

## Business Interpretation

The strongest positive signals for customer lifetime value are purchase count, session engagement, login frequency, page depth, email engagement, and wishlist behavior. This suggests that high-value customers are not only buying more, but also showing repeated browsing and engagement behavior before or between purchases.

Cart abandonment has a meaningful negative relationship with lifetime value. This may point to checkout friction, price sensitivity, poor product fit, or promotion expectations. Because this is observational data, the next step should be targeted diagnostics rather than assuming abandonment directly causes lower value.

Customer service calls also show a negative relationship with lifetime value. This may indicate that unresolved support issues or high-friction experiences are connected to lower customer value and possible churn risk.

## Recommended Next Steps

- Investigate high cart abandonment segments by country, device behavior, purchase frequency, and discount usage.
- Compare high-value and low-value customers using sample sizes and medians, not only means.
- Validate whether missing values are random or concentrated in specific customer groups.
- Treat invalid rates above 100% and unusual age values as quality flags before final modeling.
- Build a churn-focused follow-up analysis using `Churned` as the target variable.
- Consider regression or classification only after data cleaning decisions are documented.
- Turn the most actionable findings into retention, email, checkout, and service improvement experiments.

## Generated Outputs

The local `outputs/` folder includes generated analysis artifacts such as:

- PowerPoint presentation: `outputs/PPT_ecommerce_customer_analysis_Sheldon.pptx`
- PDF version: `outputs/PPT_ecommerce_customer_analysis_Sheldon.pdf`
- Chart images under `outputs/ecommerce_ppt/charts/`
- Rendered slide previews under `outputs/ecommerce_ppt/preview/`
- Structured summary: `outputs/ecommerce_ppt/analysis_summary.json`

These files are ignored by Git because they are generated artifacts and can become large. Keep source data, notebooks, and reproducible logic under version control; regenerate outputs when needed.

## Limitations

- The dataset appears to be customer-level and observational, so findings should not be interpreted as causal.
- Missing values and invalid values may affect group comparisons and correlations.
- Outliers in monetary metrics can distort averages, so medians and distribution checks are important.
- Review sentiment from VADER is a useful proxy, but it may miss nuance, sarcasm, domain-specific language, or multilingual review text.
- `Signup_Quarter` contains quarter labels but no full year, limiting time-series and cohort analysis.

## Repository Notes

- `.gitignore` excludes local system files, generated outputs, virtual environments, secrets, temporary files, and local agent instructions.
- The CSV dataset was intentionally committed for this version of the project.
- Future generated reports and charts should remain in `outputs/` unless there is a specific reason to version them.
