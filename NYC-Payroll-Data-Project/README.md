# NYC Payroll Exploratory Data Analysis

This notebook explores New York City payroll records across fiscal years 2014–2017. It uses pandas for preparation and analysis, with Matplotlib and Seaborn for charts.

## Questions and workflow

1. **Load and profile the source.** Read `Citywide_Payroll_Data__Fiscal_Year_.csv`, inspect its columns, types, summary statistics, and missing values.
2. **Prepare fields.** Convert pay amounts to numeric values, parse the agency start date, and trim agency and job-title text.
3. **Check data quality.** Drop rows with missing values and duplicates, then inspect numeric fields for outliers. An IQR-filtered subset of base salary and regular gross pay is used for a follow-up box plot; the notebook retains the broader cleaned dataframe for its main analyses.
4. **Analyze and visualize.** Compare employee counts and salary totals by agency, common job titles, overtime by agency, compensation trends by fiscal year, and the relationship between regular and overtime hours.

## Notebook structure

```text
NYC-Payroll-Data-Project/
├── README.md
└── DataAnalysis.ipynb
```

The notebook currently reads the CSV from its working directory. The dataset is not included in this folder, so download the source file and place it beside the notebook before running it:

[NYC Citywide Payroll Data (Kaggle)](https://www.kaggle.com/datasets/new-york-city/nyc-citywide-payroll-data)

## Tools

- Python 3
- pandas and NumPy
- Matplotlib and Seaborn
- Jupyter Notebook

## Interpretation note

The notebook drops every row with a missing value before analysis. This choice can remove useful records and may affect the results. The IQR filtering is applied to the plotting subset described above; it is not a general replacement for the full cleaned dataframe.
