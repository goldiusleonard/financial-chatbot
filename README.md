# Financial Chatbot

## Understanding the Problem

The goal is to enable users to query their bank transactions in natural language (English) and receive meaningful, accurate responses. The provided solution must:
- Utilize an LLM (e.g., OpenAI APIs) to interpret natural language questions.
- Translate user questions into actionable SQL queries to fetch relevant data from a transaction dataset.
- Prioritize security, data sensitivity, and user experience.
- Handle edge cases gracefully and be robust against poorly phrased questions or invalid inputs.

## Scope

### Financial Assistant for Financial Advices

Based on the given client transaction data, we can derive several metrics and insights from the available columns. These metrics can help clients understand their financial habits, optimize spending, and make informed decisions.

1. Spending Metrics

	These metrics focus on understanding and analyzing spending behavior:
	- Total Spending: Total amount spent in a given time period.
		- Formula: SUM(amt) for all transactions with amt below 0 in the specified period.
	- Spending by Category: Amount spent per category (e.g., groceries, utilities, entertainment).
		- Formula: SUM(amt) for all transactions with amt below 0 grouped by cat.
	- Spending by Merchant: Total spending with specific merchants.
		- Formula: SUM(amt) for all transactions with amt below 0 grouped by merchant.
	- Average Monthly Spending: Average spending per month.
		- Formula: SUM(amt) for all transactions with amt below 0 divided by the number of months in the period.
	- High-Value Transactions: Identification of transactions above a threshold amount.
		- Filter: amt > [threshold].
	- Spending Trend: Month-over-month changes in spending.
		- Formula: SUM(amt) for all transactions with amt below 0 for each month, analyzed over time.

2. Savings Metrics

- Net Savings: Difference between income and spending over a period.
	- Formula: SUM(amt) for all transactions in the specified period.
- Savings Rate: Percentage of saving.
	- Formula: sum(amt)/(sum(amt) for all transactions with amt above 0) * 100.

3. Transaction Analysis Metrics

To analyze and categorize client transactions:
- Transaction Count: Number of transactions in a period.
	- Formula: COUNT(txn_id).
- Average Transaction Value: Average amount spent per transaction.
	- Formula: SUM(amt) / COUNT(txn_id).
- Recurring Payments: Identification of recurring transactions (e.g., subscriptions, bills).
	- Criteria: Transactions with similar desc and periodic dates (txn_date).
- Transaction Frequency: Average frequency of transactions (e.g., daily, weekly).
	- Formula: COUNT(txn_id) divided by the period’s days or weeks.

4. Behavioral Insights

Provide actionable insights to optimize spending and saving:
- Top Spending Categories: Identify categories where the most money is spent.
	- Formula: SUM(amt) for all transcations with amt below 0 for grouped by cat, sorted in descending order.
- Cash Flow: Analysis of inflow (credits) vs. outflow (debits).
	- Formula: SUM(amt) for positive (credits) and negative (debits) amounts.
- Merchant Dependency: Percentage of total spending with a particular merchant.
	- Formula: (SUM(amt) for merchant) / (SUM(amt)) * 100.

5. Time-Based Analysis

Understand how spending patterns evolve over time:
- Weekly/Monthly Spending: Breakdown of spending by week or month.
	- Formula: SUM(amt) grouped by txn_date (week/month).
- Peak Spending Times: Identify time periods with the highest spending.
	- Analysis: Lowest transactions amt grouped by txn_date.

6. Recommendations for Financial Advice

Based on these metrics:
	1.	Budget Suggestions:
		- Recommend a monthly or category-based budget based on historical spending.
	2.	Savings Goals:
		- Suggest savings targets (e.g., saving 20% of income).
	3.	Cost Optimization:
		- Highlight areas for potential savings (e.g., subscriptions, dining out).
	4.	Investment Opportunities:
		- Advise on investing excess savings based on spending habits.

# Features

### Core Features

#### 1. Spending Overview

- Provide a summary of the user’s total spending for specified timeframes.
	- Example: “You spent $1,250 last month. Would you like a breakdown by category or merchant?”

#### 2. Category-Based Spending Insights

- Offer detailed insights into spending across categories such as groceries, dining, travel, etc.
	- Example: “Your top spending category last month was ‘Groceries,’ accounting for 35% of your total spending.”

#### 3. Merchant Analysis

- Identify spending trends with specific merchants.
	- Example: “You spent $300 at Amazon last month. Do you want to explore your Amazon purchases in detail?”

#### 4. Recurring Transactions

- Detect and summarize recurring payments like subscriptions or memberships.
	- Example: “You have recurring payments for Netflix ($15.99) and Spotify ($9.99). Would you like to review these subscriptions?”

#### 5. Weekly and Monthly Trends

- Highlight spending trends over weeks or months, comparing changes.
	- Example: “Your spending increased by 15% last week compared to the previous week.”

### Advisory Features

#### 1. Savings Suggestions

- Recommend ways to save based on spending habits.
	- Example: “You could save $100 monthly by reducing dining-out expenses by 20%.”

#### 2. Expense Optimization

- Suggest alternatives for frequent spending categories or merchants.
	- Example: “You could save on groceries by switching to StoreX, which offers discounts on similar items.”

#### 3. Anomaly Detection

- Identify and alert the user to unusual or high-value transactions.
	- Example: “You had a transaction of $1,200 at ElectronicsWorld yesterday. Was this expected?”

#### 4. Cash Flow Analysis

- Provide insights into inflow versus outflow, highlighting surplus or deficit periods.
	- Example: “Your cash flow last month was positive, with $500 more in inflow than outflow.”

### Advanced Features

#### 1. Comparative Insights

- Compare spending trends to peers or averages (while maintaining privacy).
	- Example: “You spend 25% more on dining out than the average user. Would you like tips to cut back?”

### Security Features

#### 1. Data Privacy

- Guardrail request on other user’s data.
	- Example: “For privacy reasons, I can only provide insights based on your data. Would you like help understanding trends in your transactions instead?”

## How to Setup

### Prerequisites

1. Install Miniconda in your system.

### Environment Initialization and Install Requirements

```bash
conda create -n ml python=3.10
conda activate ml
pip install -r requirements.txt
```

### Run

1. Run the backend code.

```bash
python main.py
```

2. Run the frontend code.

open the `index.html` file.

Note: The user is set to client id = "28". If you want to change the client id, change `client_id` variable in `script.js` line 42.