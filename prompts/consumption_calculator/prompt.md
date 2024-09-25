# Objective 
Create a HTML+Javascript+CSS pricing calculator from the attached document.
Help the user calculate and forecast expected charges when utilizing the Data Cloud.

Data cloud is licensed for $1,000 per 100,000 credits.
Users may purchase credits in increments of 100,000.

At the top of the page there is a label for "Cost Per 100K Credits" with an input value with default of "1,000", which represents $1,000 USD.

This input value is applied to the Total Batch and Summary charges at the bottom of the page (See section # Total Costs )
The user may adjust this value, which forces a recalculation of the Total Costs.

# Input Data
The resulting HTML table will extend the following, pre-existing rate card markdown table:

| Category                   | Usage Type                              | Unit                           | Batch | Streaming |
|----------------------------|-----------------------------------------|--------------------------------|-------|-----------|
| Connect, Harmonize, and Unify | Data Pipeline                           | Per 1 Million Rows Processed    | 2,000 | 5,000     |
| Connect, Harmonize, and Unify | Data Transforms                         | Per 1 Million Rows Processed    | 400   | 5,000     |
| Connect, Harmonize, and Unify | Unstructured Data Processed             | Per 1 MegaByte (MB) Processed   | 0     | 60        |
| Connect, Harmonize, and Unify | Data Federation or Sharing Rows Accessed| Per 1 Million Rows Accessed     | 0     | 70        |
| Connect, Harmonize, and Unify | Data Share Rows Shared (Data Out)       | Per 1 Million Rows Shared       | 0     | 800       |
| Connect, Harmonize, and Unify | Profile Unification                     | Per 1 Million Rows Processed    | 0     | 100,000   |
| Connect, Harmonize, and Unify | E2E Real-Time Processing Sub-second Real-Time Events | Per 1 Million Events & API | 0     | 70,000    |
| Analyze and Predict         | Calculated Insights                     | Per 1 Million Rows Processed    | 15    | 800       |
| Analyze and Predict         | Inferences                              | Per 1 Million Inferences        | 0     | 3,500     |
| Act                         | Data Queries                            | Per 1 Million Rows Processed    | 2     | 0         |
| Act                         | Streaming Actions (including Lookups)   | Per 1 Million Rows Processed    | 0     | 800       |

The resulting output table will extend this table to include interactive columns for user input and columns for multiplying the consumption rates by user input units to produce "Total Batch" and "Total Streaming" values.

The final row in the table will provide rollup summary (SUM) per column.

# Styles and Layout
The HTML should utilize the Salesforce Lightning Design System (SLDS) for all CSS, fonts, and layouts.
The resulting HTML should ideally be responsize, utilizing data grids that auto-flow and scale to mobile and desktop environments.


# Rate Card
Create an interactive HTML table that looks a behaves like an Excel spreadsheet.
The user will modify input values for the "Consumption" column. When the focus changes on a consumption input, or the user hits the "Enter" or Return key, the table should recalculate the summary values in the last (bottom) row.


## Rate Card (Table Layout)

The HTML table should have columns for:
| Category | Usage Type | Unit | Batch | Streaming | Batch Consumption | Streaming Consumption | Total Batch | Total Streaming |

The static values for Category, Usage Type, Unit, Batch, and Streaming should all be derived from the attached document.

The "Batch Consumption" and "Streaming Consumption" columns contain an interactive input for collecting a numeric value.
The default consumption is always "0".

If the Category "Unit" is "Per 1 Million Rows Processed", then the Consumption input value represents 1 Million rows.

If the Category "Unit" is "Per 1 MegaByte (MB) Processed", the Consumption input value represents 1 MegaByte rows.

The same logic applies to units representing API events, inferences, etc...

For example, if the user enters a value of "5", then they are intending to communicate antipated consumption of "5 Million" rows, MBs, Events or Inferences.

If a usage type supports both "Batch" and "Streaming", then allow input values for both the "Batch Consumption" and "Streming Consumption" cells for each row. 

If a usage type in the attached documents spans both the "Batch" and "Streaming" columns, then assume the usage type is strictly "Streaming". For those usage types, render a user input value in only the "Streaming Consumption" column, and render a fixed value of "0" (non-editable) in the "Batch Consumption" column, and render the background color as grey.


For example, the "Unstructured Data Processed" usage type is charged at 60 credits per 1 MegaByte (MB) Processed.
The resulting row should appear as:

| Category | Usage Type | Unit | Batch | Streaming | Batch Consumption | Streaming Consumption | Total Batch | Total Streaming |
|----------|------------|------|-------|-----------|-------------------|-----------------------|-------------|-----------------|
| Connect, Harmonize, and Unify | Unstructured Data Processed | Per 1 MegaByte (MB) Processed | 60 | 60 | 0 (with grey background-color)  | [input with default value=1]| 0 | 60 |

## Rate Card Calculations

Note that the final 2 columns "Total Batch" and "Total Streaming" are calculated with each change in user input focus, or hitting the retirn key within an input.

They represent the coefficient multiplication of the static "Batch" or "Streaming" values multiplied by the user input for "Batch Consumption" and "Streaming Consumption".

In the example rows above, the "Unstructured Data Processed" usage type is calculated at 60 credits per 1 MegaByte (MB) Processed. If the user provided an input of "2" for the "Streaming Consumption" value, the resulting "Total Batch" and "Total Batch" values are calculated at `0 * 60` and `2 * 60` respectively, resulting in "Total Batch" value = 0 and "Total Streaming" = "120".

## Summary Row Calculation
The last and bottom row of the table should summarize all the input values and total values in the table. The last 4 columns basically are summarized.

The last row contains the label "Summary" as the "Category" value.

The "Batch Consumption" final summary row contains the calculated sum of all "Batch Consumption" values.
The "Streaming Consumption" final summary row contains the calculated sum of all "Streaming Consumption" values.
The "Total Batch" final summary row contains the calculated sum of all "Total Batch" values.
The "Total Streaming" final summary row contains the calculated sum of all "Total Streaming" values.

Note that the calculate() javascript function must recalculate each row to determine the Total Batch and Total Streaming values for each row before summarizing the totals in the final summary row.

# Total Costs
Beneath the rate card table towards the bottom of the page should be 2 large labels and calculated US currency costs for "Total Batch Costs" and Total Steaming Costs"

"Total Batch Costs" is the final summary value across all "Batch Consumption" values, multiplied to factor the "Cost Per 100K Credits" value.

"Total Streaming Costs" is the final summary value across all "Batch Consumption" values, multiplied to factor the "Cost Per 100K Credits" value.

For example, if the "Total Batch" credits consumed is 200,000 and the "Cost Per 100K Credits" is $1,000 then the "Total Batch Costs" are $2,000.

The calculate() javascript function should calculate these values last, after the individual row level calculations and final summary calculations are complete.

# Instructions
Generate the HTML, JS (Javascript) and CSS required to meet the interactive table objectives.
