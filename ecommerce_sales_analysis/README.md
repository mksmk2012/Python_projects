# E-commerce Sales & Traffic Analysis (BigQuery + Python + Tableau)

Analysis of web sessions, orders and registered users of an online furniture store for **November 1, 2020 – January 31, 2021**. The project covers exploratory analysis, sales dynamics, pivot tables, correlation analysis and statistical tests, and ends with business conclusions and recommendations.

## Goal

Understand where sales come from (markets, products, traffic sources, devices), how they change over time, and which differences between segments are statistically significant.

## Data

Data is queried from BigQuery (project `data-analytics-mate`, dataset `DA`) and joined into one session-level table (349,545 sessions, 18 columns).

| Table | Used for |
|---|---|
| `session` | Session ID and date |
| `session_params` | Continent, country, device, browser, mobile model, operating system, language, channel, medium |
| `account_session`, `account` | Registered user ID, email verification and unsubscribe flags |
| `order`, `product` | Purchased product: category, name, price, description |

All tables are joined to `session` with `LEFT JOIN`, so sessions without an account or an order contain `NULL` values in the corresponding columns (this is expected, not a data error).

## Analysis stages

1. **Initial data exploration:** structure, unique sessions, date range, missing values.
2. **Sales and customer analysis:** sales by continent, country, product category, device and mobile model, traffic source; email verification and newsletter subscription; registered users by country.
3. **Sales dynamics:** daily sales overall and by continent, traffic source and device type.
4. **Pivot tables:** sessions by channel and device, sales by category and country, sessions by weekday and device.
5. **Relationships (Pearson correlation):** sessions vs. sales, and sales across continents, traffic sources, product categories and device types.
6. **Differences between groups (statistical tests):** Mann-Whitney U, Kruskal-Wallis, two-proportion z-test.
7. **Business conclusions and recommendations.**

## Key findings

| Area | Result |
|---|---|
| Markets | Americas lead with about $17.67M, then Asia ($7.60M) and Europe ($5.93M); the United States alone generates about $13.94M |
| Products | Sofas & armchairs ($8.39M), Chairs ($6.15M) and Beds ($4.92M) are the top categories |
| Traffic sources | Organic Search 35.76%, Paid Search 26.62%, Direct 23.44% of sales (85.82% combined) |
| Devices | Desktop Chrome 27.84%, desktop Safari 20.30%, mobile iPhone 20.08% of sales |
| Email | 71.70% of registered users verified their email; 16.94% unsubscribed |
| Weekdays | Traffic peaks on Tuesday–Thursday and is lowest on weekends |

### Statistical results

| Question | Method | Result |
|---|---|---|
| Daily sessions vs. daily sales | Pearson correlation | r = 0.791, p < 0.001 (strong positive) |
| Sales across top 3 continents | Pearson correlation | r = 0.77–0.79, all significant |
| Sales across traffic sources | Pearson correlation | r = 0.455–0.870, all significant |
| Sales across device types | Pearson correlation | desktop vs. mobile r = 0.873; tablet 0.57–0.60 |
| Daily sales: registered vs. unregistered users | Mann-Whitney U | p < 0.0001, significant difference |
| Daily sessions across traffic channels | Kruskal-Wallis | H = 368.98, p < 0.001, significant difference |
| Share of organic sessions: Europe vs. Americas | Two-proportion z-test | 35.6% vs. 35.5%, p = 0.772, no significant difference |

## Business recommendations (summary)

- Prioritize the United States and other high-value markets.
- Build promotions and cross-selling around the leading categories.
- Keep investing in Organic Search, Paid Search and Direct traffic, and track channel efficiency (CAC, ROAS).
- Monitor the desktop and mobile purchase funnels separately.
- Plan campaigns around weekday patterns and investigate the December and January sales peaks.
- Analyze customer-level metrics (sales per customer, AOV, retention) before judging the value of newsletter subscribers.

## Dashboard

Interactive Tableau dashboard: [Sales Dashboard on Tableau Public](https://public.tableau.com/views/Book2_17906375676700/SalesDashboard)

## Tech stack

Python (pandas, NumPy, SciPy, statsmodels, Matplotlib, Seaborn), Google BigQuery, Google Colab, Tableau.

## How to run

1. Open the notebook in Google Colab.
2. Authenticate with an account that has access to the BigQuery project `data-analytics-mate` (the notebook uses `auth.authenticate_user()`).
3. Run all cells from top to bottom.

## Repository contents

| File | Description |
|---|---|
| `ecommerce_sales_analysis.ipynb` | Analysis notebook |
| `README.md` | Project description |
