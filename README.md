# Online Sales Analysis (Exploratory Data Analysis in Python)

Exploratory analysis of online store sales data: customer geography, product performance, sales channels, profitability and shipping time. The goal is to find key trends and turn them into insights that support business decisions.

## Project stages

1. **Data overview:** structure and meaning of the three datasets.
2. **Cleaning:** missing values, text normalization, date conversion, column names, duplicates.
3. **Analysis & visualization:** revenue, cost, profit, units sold, shipping time and sales trends by category, country, region, channel, year and weekday.
4. **Conclusions & insights.**

## Data

Three related CSV files:

| File | Rows | Description |
|---|---|---|
| `events.csv` | 1,330 | Sales transactions: order and ship dates, priority, country code, product ID, sales channel, units sold, unit price, unit cost |
| `countries.csv` | 249 | Country names, ISO codes (`alpha-2`, `alpha-3`), region and sub-region |
| `products.csv` | 12 | Product ID and category (`item_type`) |

Relations: `events.Country Code` = `countries.alpha-3`, `events.Product ID` = `products.id`.

## Data cleaning

- **Countries:** missing `region`/`sub-region` for Antarctica filled with the country name; Namibia's `alpha-2` code restored to `NA` (pandas reads the string "NA" as a missing value).
- **Events:** 82 missing `Country Code` values filled with `Unknown` to keep the records; 2 rows with missing `Units Sold` dropped.
- All text columns trimmed and lower-cased, dates converted to `datetime`, column names standardized to snake_case.
- No duplicate rows found in any dataset.
- The three tables are merged with left joins into one analytical DataFrame.

## Calculated metrics

| Metric | Formula |
|---|---|
| `revenue` | `units_sold * unit_price` |
| `cost` | `units_sold * unit_cost` |
| `profit` | `revenue - cost` |
| `days_to_ship` | `ship_date - order_date` (days) |

## Key figures

| Metric | Value |
|---|---|
| Orders | 1,328 |
| Countries covered | 46 |
| Product categories | 12 |
| Total revenue | $1,702,129,408 |
| Total cost | $1,200,694,949 |
| Total profit | $501,434,459 |
| Average order value | $1,281,724 |

Top 5 categories by revenue: office supplies, household, cosmetics, meat, baby food.

## Key insights

- **Geography:** business is heavily concentrated in Europe, which leads in revenue, profit and units sold; Asia contributes a much smaller, stable volume.
- **Products:** office supplies lead in revenue and units sold; cosmetics is the most profitable category.
- **Channels:** online and offline contribute almost equally to revenue, profit and volume.
- **Shipping:** average delivery time differs only slightly by category and region, but varies more by country; no clear relationship between shipping time and profit.
- **Trends:** sales fluctuate over time with peaks around 2012 and 2016; Europe stays dominant throughout the period.
- **Weekdays:** no universal peak day across categories.

## Tech stack

Python, pandas, NumPy, Matplotlib, Seaborn, Google Colab.

## How to run

1. Open the notebook in Google Colab or Jupyter.
2. Put `countries.csv`, `events.csv` and `products.csv` in one folder.
3. Update the path in the data loading cell (the notebook mounts Google Drive and uses `/content/drive/MyDrive/Mate/Final_project`).
4. Run all cells from top to bottom.

## Repository contents

| File | Description |
|---|---|
| `exploratory_data_analysis_online_store.ipynb` | Analysis notebook |
| `README.md` | Project description |

