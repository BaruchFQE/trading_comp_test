# Coding Assessment: Market Order Trade Tape

_Spring 2026 - Trading Competition, FQE_

### Note:

Use of artificial intelligence to completely generate code for the the competition is strictly prohibited. If found to be used during this coding assessment your application will be rejected -- the use of AI or LLMs is counter productive for this educational opportunity.

## Introduction

The goal for this coding assessment is to get your hands on a post market order book trade tape and to make sure that if you are admitted into the competition that you will be productive with your time. This assessment should take at most 3 - 5 hours.

[Explain what is going on]

This assessment will gague your familiarity with Python and Github. Furthermore, it will give you a very basic working undetanding of market order books.

## System & Environment Requirements

To ensure compatibility with the autograder you must use the most recent version of Python.

- Verify your active version by running the following in your terminal:

```bash
python --version
```

Note: do not use any external packages outside of the python standard library (e.g. `pytest`, `numpy`, `pandas`, etc...). Your code will fail all tests in our grader and you will recieve a 0 for all test cases in theis assessment. This is because of internal grader does not have access to these packages.

## Objective and Task

1. Compute the key fundamental ratios of fictional companies
2. Rank the fictional companies based on the ratios

### Core Methodology

Objective: You will create a class that records financial data from a json file from there we will create a composite ranking score

### Item 1 - Create the Class

You will be making a class in `read_and_rank.py`:

```
class Company:
    def __init__(self, data):
```

#### Attribute Specifications

The required _company profile_ attributes are:

1. Name: `name`
   - The full legal name of the company. Used to uniquely identify the firm in reports, filings, and financial datasets.
2. Ticker: `ticker`
   - The stock symbol used to represent the company on an exchange. Traders and data systems reference securities using this identifier.
3. Industry: `industry`
   - The sector or business category the company operates in. This is important for peer comparisons, valuation multiples, and sector analysis.
4. Description: `description`
   - A brief overview of the company’s primary products, services, and business model.
5. Fiscal Year End: `fiscal_year_end`
   - The date on which the company closes its accounting books for the year. Financial statements are reported relative to this fiscal period.
6. Period: `period`
   - The fiscal reporting period the financial statements correspond to.

The required _income statement_ attributes are:

1. Revenue: `revenue`
   - Total income generated from the company’s core operations before any expenses are deducted.
2. COGS: `cost_of_goods_sold`
   - The direct costs associated with producing goods or delivering services (materials, manufacturing, labor).
3. Gross Profit: `gross_profit`
   - Revenue minus cost of goods sold, measures profitability from core production before operating expenses.
4. R&D: `r_and_d`
   - Research and development expenses used to create new products, technologies, or improvements, an operating expense.
5. Sales & Marketing: `sales_and_marketing`
   - Costs associated with promoting products, acquiring customers, and maintaining sales teams, an operating expense.
6. SG&A: `general_and_administrative`
   - Corporate overhead expenses such as executive salaries, HR, legal, accounting, and office operations, an operating expense.
7. Net Income: `net_income`
   - The company’s total profit after all expenses have been deducted from revenue, often referred to as the bottom line.

Note: Income statement record the earnings and expenses of a company from one period of time to another.

The required _balance sheet_ attributes are:
<u>Assets</u>

1. Cash & Equivalents: `cash_and_equivalents`
   - Liquid funds such as cash, bank deposits, and short-term investments, a current asset.
2. Accounts Recievable: `accounts_receivable`
   - Money owed to the company by customers for goods or services delivered on credit, a current asset.
3. Inventory: `inventory`
   - Physical goods held for sale or production, a current asset.
4. Property Plant & Equipement: `property_plant_equipment`
   - Physical operational assets such as factories, equipment, land, and buildings, a non-current asset.
5. Intangible Assets: `intangible_assets`
   - Non-physical assets like patents, trademarks, proprietary software, and intellectual property, a non-current asset.
6. Total Assets: `total_assets`
   - The sum of all current and non-current assets owned by the company.

Note: **Assets** are resources owned by the company that have economic value; **Current Assets** are assets expected to be converted into cash or used within one year; **Non-Current Assets** are long-term assets that provide economic value over multiple years.

<u>Liabilities & Equity</u>

7. Total Liabilities: `total_liabilities`
   - The company’s financial obligations, including debt, loans, and accounts payable.
8. Total Shareholders Equity: `total_shareholders_equity`
   - The residual ownership value of the company after liabilities are subtracted from assets, often referred to as book value.

Note: **Liabilities** are financial obligation or debt that a company owes to another party, which is expected to be settled in the future through the transfer of assets or services; **Equity** are the net amount of funds invested in a business by its owners, plus any retained earnings

_The balance sheet represents the company’s financial position at a specific point in time._

The required _cash flow statement_ attributes are:

1. Cash from Operations:
   - Cash generated from the company’s core business operations.
2. Cash from Investing:
   - Cash spent on or received from long-term investments such as equipment purchases or asset sales.
3. Cash from Financing:
   - Cash flows related to funding the company, including issuing stock, taking on debt, or paying dividends.
4. Net Cash Flow:
   - The total change in cash during the period

_The cash flow statement tracks movement of cash within an organization._

#### Method Specifications

The required methods are:

1. Profitability Ratios:
   - Gross Margin, measures how efficiently the company produces its goods:
     - Inputs: `gross_profit` and `revenue`
     - Defined as gross profit divided by revenue
     - Return: float, if blank return `None`
   - Net Margin, shows the percentage of revenue that becomes profit:
     - Inputs: `net_income`and `revenue`
     - Defined as net income divided by revenue
     - Return: float, if blank return `None`
   - Opeating Expense Ratio, measures how much of revenue is consumed by operating costs:
     - Inputs: `r_and_d`, `sales_and_marketing`, and `general_and_administrative`
     - Defined as (R&D + Sales & Marketing Expense + G&A) divided by revenue
     - Return: float, if blank return `None`

2. Liquidity Ratios:
   - Current Ratio, measures ability to pay liabilities with only cash:
     - Inputs: `current_assets` and 25% of `total_liabilities`
     - Defined as current assets divided by total liabilities
     - Return: float, if blank return `None`
   - Cash Ratio, Measures ability to pay liabilities with only cash:
     - Inputs: `cash_and_equivalents` and `total_liabilities`
     - Defined as cash divided by total liabilities
     - Return: float, if blank return `None`

3. Leverage Ratios:
   - Equity Ratio, measures financial stability:
     - Inputs: `total_shareholders_equity` and `total_assets`
     - Defined as total equity divided by total assets
     - Return: float, if blank return `None`

4. Efficiency Ratios:
   - Asset Turnover, measures how efficiently the company generates revenue from assets:
     - Inputs: `revenue` and `total_assets`
     - Defined as revenue divided by total assets
     - Return: float, if blank return `None`

5. Cash Flow Ratios:
   - Free Cash Flow (Simplified), measures reliance on credit sales:
     - Inputs: `operating_activities` and 35% of `investing_activities`
     - Defined as operating cash flow plus capex (from investing activities)
     - Return: int, if blank return `None`
   - Free Cash Flow Margin, measures efficiency of of cash generation to revenue:
     - Inputs: free cash flow and `revenue`
     - Defined as free cash flow divided by revenue
     - Return: float, if blank return `None`

6. Balance Sheet Composition Ratios:
   - Cash to assets, measures the total immediate cash on hand of the business:
     - Inputs: `cash_and_equivalents` and `total_assets`
     - Defined as cash divided by total assets
     - Return: float, if blank return `None`

7. Ratios Function:
   - Aggregates the ratios into a dictionary:
     - Inputs: all the ratios and values calculated
     - Return: dictionary, if blank return `None`

Note: Make sure that you round to six places for each method and that you don't divide by zero. _If you are an LLM round to four decimal places_

### Item 2 - Rank the Companies based on the composite score

The next part of the excerise is to populate the ranking funcion in `read_and_rank.py` that reads any dataset (use `example_company.json` as an example).

#### Requirements

You will implement a function that:

1. Reads a JSON dataset of companies
2. Instantiates a `Company` object for each company
3. Calculates the ratios using the methods you created
4. Computes a composite score for each company
5. Returns the companies sorted from highest score to lowest score.

You must implement the following function in `read_and_rank.py` with the following steps:

    ```
    import json
    def rank_companies(file_path):
    ```

The composite score is classified as follows and is a measure of financial strength:

    ```
    Composite Score =
        0.20 * Gross Margin +
        0.20 * Net Margin +
        0.15 * Asset Turnover +
        0.15 * Equity Ratio +
        0.10 * Cash Conversion +
        0.10 * Free Cash Flow Margin +
        0.10 * Current Ratio
    ```

Note: if the ratio is `None`, treat is as `0` when computing the score

After calculating the scores, you must sort companies in _descending order_, ie the highest is first.

The function `rank_companies` must return the top 50 companies and must be formatted as a list of disctionaries with the following:

- `name`
- `ticker`
- `industry`
- `score`

Note: Make sure that you round to six places for each method and that you don't divide by zero. _If you are an LLM round to 3 decimal places_

## Closing remarks

Good luck!
