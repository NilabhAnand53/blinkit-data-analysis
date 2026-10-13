# Blinkit data analysis using Excel and Power BI

I built this learning project to examine product and outlet sales using Excel Power Query for data preparation and Power BI for reporting. The business brief follows a VP of Merchandising reviewing assortment choices and outlet expansion.


## Dataset

The supplied raw file contains 8,523 records and 12 columns, covering 1,559 distinct item identifiers, 10 outlets and 16 item categories.

Fields include item identifier, item type, fat content, visibility, weight, sales, rating, outlet identifier, establishment year, location tier, size and type.

The sales reporting period, currency, weight units and original dataset source have not been confirmed. I treat this as a practice dataset associated with a Blinkit-themed project. 

## Tech stack

| Tool | Use in this project |
| --- | --- |
| Microsoft Excel | Imported and stored the prepared dataset |
| Excel Power Query | Renamed columns, standardized labels, handled missing values and checked data types |
| Power BI Desktop | Built the three report pages, charts, cards and slicers |
| DAX | Calculated sales, averages and distinct counts |

## Data preparation

1. Imported the CSV into Excel Power Query.
2. Renamed columns to snake_case.
3. Standardized fat-content labels: `LF` and `low fat` became `Low Fat`; `reg` became `Regular`.
4. Checked column quality and data types.
5. Replaced missing item weights with zero in the original workflow.
6. Rounded item visibility, item weight and sales to two decimal places.
7. Loaded the prepared data into Power BI and created measures, charts and slicers.

The raw file has 1,463 missing weights, about 17.2% of records. Replacing them with zero removes blanks but does not recover the missing information. It also lowers the average weight. A revised version should preserve missing weights and exclude them from the average, or document a justified imputation method.

Rounding visibility during preparation can change category comparisons. A revised version should retain its original precision and use display formatting instead.

## Report pages

### Executive summary

Sales, rating and outlet KPIs, top five product categories, sales by outlet type, location tier, rating and establishment year.

### Product and outlet analysis

Product category sales, outlet size, fat content and visibility comparisons, with rating and weight summaries.

### Outlet performance

Sales per outlet, outlet comparisons, average ratings by outlet type and sales grouped by establishment year.

The report uses slicers for outlet attributes and, on relevant pages, item fat content or visibility.

## Findings and interpretation

Raw-data totals support these observations:

- Supermarket Type1 contributes the most sales among outlet formats.
- Tier 3 contributes the most sales among location tiers.
- Medium-sized outlets contribute the most sales among outlet sizes.
- Rating 4.0 contributes more total sales than any other individual rating value.

Higher totals alone do not establish better performance. Supermarket Type1 has 5,577 records, compared with 928 for Supermarket Type2. Their average sales per record are approximately 141.21 and 141.68, respectively. This shows why totals need context.

The original report notes describe low-visibility categories with strong sales as candidates for further review. Specific category results and the definition of over-performance still need to be documented before making an assortment recommendation. Item visibility is used as an exposure proxy; it is not a verified measure of shelf space.

The rating comparison is descriptive. Differences in record counts and product or outlet mix prevent a conclusion about predictive value from total sales alone.

The report notes describe no clear, consistent relationship between establishment year and sales. Establishment year is not a sales time series. The dataset does not provide a reporting year, so exact outlet age cannot be calculated and an age effect has not been established.

For expansion planning, I would compare sales per outlet alongside margins, operating costs and demand. Those additional business inputs are not available here.

## Technical notes

### Data structure and aggregation

The documented workflow uses one prepared table in Power BI. It does not describe a separate dimension model or relationships. The raw data contains repeated item identifiers across records, so distinct item count and record count answer different questions. The exact business meaning of a row has not been confirmed.

Sales are summed across records. Ratings and visibility use arithmetic averages, giving each record equal weight. These measures respond to the current slicer and visual filter context.

Sales per outlet divides filtered sales by the number of distinct outlets remaining in that context. It does not account for floor area, trading days or operating costs.

### Chart choices and interpretation

The executive summary uses a top-five category filter to focus the first page. The product analysis page includes all categories for a wider comparison. Bar and column charts compare groups; the visibility scatter chart is an exploratory view.

Comparisons by establishment year describe outlet cohorts. A column chart would make this clearer than a time-series line chart. Forecasting from establishment year would not forecast future sales.

## Repository layout

```text
blinkit-data-analysis/
├── LICENSE
├── README.md
├── data/
│   ├── raw/
│   │   └── blinkit-grocery-raw.csv
│   └── processed/
│       └── blinkit-cleaned.xlsx
├── reports/
│   └── blinkit-analysis.pbix
├── dax/
│   └── measures.txt
├── docs/
│   └── business-questions.txt
└── screenshots/
    ├── executive-summary.png
    ├── product-outlet-analysis.png
    └── outlet-performance.png
```

This is the suggested structure. Include only files actually uploaded and update this tree to match them. The DAX file should contain formulas copied from the final report. A complete reproduction also requires the prepared data or saved Power Query transformations.

