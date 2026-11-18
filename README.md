# Telco Customer Churn: Exploratory Data Analysis

An exploratory data analysis (EDA) of a telecom company's customer data in Python, to find out **which customers churn (cancel their service) and what they have in common**.

## Project at a glance

| | |
|---|---|
| **Goal** | Understand which customer traits and services are linked to churn |
| **Dataset** | 7,043 customers, 21 columns, one row per customer |
| **Target column** | `Churn` (Yes / No) |
| **Overall churn rate** | 26.54% (1,869 churned, 5,174 stayed) |
| **Tools** | Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook |
| **Scope** | EDA only (no predictive modelling) |

## Repository structure

```
telco-customer-churn-eda/
├── README.md
├── requirements.txt
├── data/
│   └── Telco-Customer-Churn.csv
├── notebooks/
│   └── EDA_Customer_Churn_Analysis.ipynb
└── reports/
    ├── Executive_Summary_EDA_Telco_Churn_Analysis.pdf
    ├── Telco_Customer_Churn_Dataset_Data_Summary.pdf
    └── EDA_Customer_Churn_Analysis.pdf
```

| File | What it is |
|---|---|
| `data/Telco-Customer-Churn.csv` | The raw dataset (unchanged) |
| `notebooks/EDA_Customer_Churn_Analysis.ipynb` | The full analysis: cleaning, charts and observations |
| `reports/Executive_Summary_EDA_Telco_Churn_Analysis.pdf` | Short business summary of findings and recommendations |
| `reports/Telco_Customer_Churn_Dataset_Data_Summary.pdf` | Data dictionary: what each column means, data quality notes, checklist before analysis |
| `reports/EDA_Customer_Churn_Analysis.pdf` | Static PDF copy of the notebook, for reading without running anything |

## About the data

Each row is one customer. The 21 columns fall into five groups:

- **Profile:** `customerID`, `gender`, `SeniorCitizen`, `Partner`, `Dependents`
- **Time with the company:** `tenure` (months, 0 to 72)
- **Services:** `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`
- **Contract and billing:** `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges`
- **Outcome:** `Churn`

The full column-by-column guide is in `reports/Telco_Customer_Churn_Dataset_Data_Summary.pdf`.

**Dataset source:** [add the link where you downloaded the dataset, and check its license before publishing]

## Data cleaning

The data was clean apart from one issue:

- `TotalCharges` loaded as text because 11 rows contained a blank space instead of a number. All 11 customers have `tenure = 0` (just joined, not billed yet), so the blanks were replaced with `0` and the column converted to `float`.
- `SeniorCitizen` was converted from `0/1` to `No/Yes` so charts read clearly.
- No null values and no duplicate rows (checked on the full row and on `customerID`).

## Key findings

| Driver | Higher-churn group | Churn rate | Comparison |
|---|---|---|---|
| Contract | Month-to-month (1,655 of 3,875) | 42.7% | One year 11.3%, two year 2.8% |
| Payment method | Electronic check (1,071 of 2,365) | 45.3% | Mailed check 19.1%, bank transfer 16.7%, credit card 15.2% |
| Internet service | Fiber optic (1,297 of 3,096) | 41.9% | DSL 19.0%, no internet 7.4% |
| Online security | No OnlineSecurity (1,461 of 3,498) | 41.8% | With it 14.6% |
| Tech support | No TechSupport (1,446 of 3,473) | 41.6% | With it 15.2% |
| Senior citizen | Seniors (476 of 1,142) | 41.7% | Non-seniors 23.6% |
| Gender | Female 26.9% | | Male 26.2% (no real difference) |

Other observations:

- Churn is concentrated in customers with very short tenure (the first 1 to 2 months). Long-tenure customers mostly stay.
- Customers without OnlineBackup (39.9%) or DeviceProtection (39.1%) churn far more than those with them (21.5% and 22.5%).
- Streaming services, phone service and multiple lines show only small differences in churn.
- Month-to-month customers make up 88.6% of all churners.

### Suggested actions (from the executive summary)

1. Move month-to-month customers to one- or two-year contracts.
2. Run a first-90-days onboarding program for new customers.
3. Encourage automatic payment methods for electronic check users.
4. Bundle OnlineSecurity and TechSupport with fiber plans, and investigate fiber pricing and service quality.
5. Offer seniors a simpler plan or dedicated support.

## Limitations

- These results show **correlation, not cause**. Month-to-month contracts, fiber optic and electronic check likely overlap, so the effect of each one on its own is not separated here.
- `MonthlyCharges` and combinations of factors (for example contract by internet service) have not been analyzed yet.
- The dataset is a one-time snapshot with no dates and no stated reason for leaving.

## How to run it

1. **Clone the repo**
   ```bash
   git clone <your-repo-url>
   cd telco-customer-churn-eda
   ```
2. **Install the libraries** (a virtual environment is recommended)
   ```bash
   pip install -r requirements.txt
   ```
3. **Open the notebook**
   ```bash
   jupyter notebook notebooks/EDA_Customer_Churn_Analysis.ipynb
   ```
4. **Check the data path.** The notebook reads the CSV in its first cells. Use a relative path so it works on any machine:
   ```python
   df = pd.read_csv("../data/Telco-Customer-Churn.csv")
   ```
5. Run all cells from top to bottom.

## Next steps

- Analyze `MonthlyCharges` against churn and group `tenure` into buckets with exact churn rates.
- Look at combinations of factors (contract by internet service, payment method by contract).
- Build a Power BI dashboard from the cleaned data.
- Try a simple churn prediction model.

## Author

**Ashish**, Pune, India
