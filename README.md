# Employee Dashboard

## Project Overview

This project is an interactive employee analytics dashboard built to give HR teams and business leaders a consolidated view of workforce data. It tracks headcount, salary distribution, attrition, gender balance, departmental composition, hiring trends over time, and geographic presence — all in a single-page layout. The dashboard is designed to support workforce planning, compensation benchmarking, and diversity monitoring at a glance.

---

## Dataset

The underlying dataset contains records for 1,000 employees with the following key attributes:

- `Full Name` — employee identifier used in the top earners table
- `Annual Salary` — individual compensation figure
- `Department` — one of four departments: Specialty Products, Research and Development, Corporate, or Manufacturing
- `Job Title / Level` — hierarchical role from Analyst up to Vice President, plus technical roles (System Administrator, Cloud Infrastructure Architect, Network Administrator)
- `Gender` — used for the female-to-male ratio calculation
- `Age` — used as a filter slider in the dashboard
- `Hire / Record Date` — used for the hiring trend time series (1993–2020)
- `Employment Status` — active (Working Employee) vs. exited, used to compute the exit rate
- `Location` — geographic coordinates or region used to plot employees on the world map

---

## Requirements

### Looker Studio
- A free Google account — Looker Studio is entirely browser-based and requires no installation
- Access to Looker Studio at lookerstudio.google.com
- The source data uploaded to Google Sheets, BigQuery, or connected via a supported Looker Studio connector
- Familiarity with Looker Studio's calculated fields for custom metrics (median salary, exit rate, gender ratio)

### Data Source
- A structured employee table in Google Sheets, BigQuery, or a CSV imported via a Looker Studio connector
- A date field for the hiring trend time series and date range filter
- Latitude/longitude columns or a recognized geographic field (country, state, city) for the map visual

---

## Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| Looker Studio | Dashboard design, layout, and publishing (browser-based, no installation) |
| Looker Studio Calculated Fields | Custom metrics — median salary, exit rate, gender ratio, record count over time |
| Google Sheets / BigQuery | Data source connection via native Looker Studio connectors |
| Google Maps Visual | Geographic distribution of employees worldwide |
| Treemap Chart | Department headcount breakdown |
| Donut Chart | Female vs. male employee proportion |
| Horizontal Bar Chart | Annual salary by job title and level |
| Time Series / Line Chart | Hiring record count trend from 1993 to 2020 |
| Table Visual | Top 10 highest-paid employees |
| Scorecard Visuals | Summary metrics — total employees, working employees, median salary, exit rate, gender ratio |
| Filter Controls | Department filter (dropdown), Age filter (range slider), Date range selector |
| Excel / CSV | Source data format |

---

## Dashboard Layout and Features

The dashboard is organized into a single page with the following components:

At the top, five KPI cards display the headline metrics: Total Employees (1,000), Working Employees (897), Median Salary ($92,806), Exit Rate (10.30%), and the Female-to-Male Ratio (1.06). Three filters sit in the top-left corner — a department dropdown, an age range slider, and a date range selector — which apply across all visuals simultaneously.

The middle row contains the top-10 salary leaderboard table on the left, a horizontal bar chart showing total annual salary by job title in the center, and a donut chart showing the gender split (53.2% female, 46.8% male) on the right.

The bottom row contains a line chart tracking the number of employee records by hire year from 1993 to 2020 on the left, a treemap showing headcount by department in the center, and a world map visual showing geographic employee distribution on the right.

---

## Key Insights

- Out of 1,000 total employees, 897 are currently active, giving an exit rate of 10.30% — a figure that warrants monitoring, particularly if concentrated in specific departments or seniority levels.
- The median annual salary of $92,806 suggests a mid-to-senior workforce composition, which aligns with the salary bar chart showing Vice Presidents and Directors commanding the highest total salary pools.
- The female-to-male ratio of 1.06 indicates a near-equal gender split with a slight female majority (53.2% female vs. 46.8% male), which is a positive signal for gender representation.
- Specialty Products is the largest department with 266 employees, closely followed by Research and Development and Corporate at 254 each, with Manufacturing being the smallest at 226.
- The top earner (Everett Le at $350,690) earns significantly more than the next nine highest-paid employees, who are clustered in a narrow band between $257,000 and $290,000, suggesting a pronounced outlier at the top.
- The hiring trend line shows steady but low hiring activity from 1993 through the early 2010s, followed by a sharp acceleration toward 2018–2020, indicating rapid organizational growth in recent years.
- The world map shows employee presence in North America and Asia as the dominant regions, with smaller clusters visible in other continents, pointing to a globally distributed workforce.
- Analyst and Analyst II roles contribute relatively little to the total salary pool compared to managerial and VP-level roles, which is expected but confirms that compensation is heavily weighted toward leadership tiers.

---

## Challenges Faced

- Looker Studio does not have a native `MEDIAN` function in calculated fields — computing median salary requires a workaround such as pre-aggregating the value in the data source (Google Sheets formula or BigQuery query) before connecting it to the report.
- The exit rate calculation depends on clearly defined employment status values in the data. If the source data uses inconsistent labels for terminated or resigned employees, the rate will be inaccurate without cleaning in the data source first, since Looker Studio has limited data transformation capabilities compared to Power Query.
- The age range slider control requires a clean numeric age field. If age is stored as a birth date, a calculated column must be created in Google Sheets or BigQuery to derive current age before it can be used as a filter.
- The map visual in Looker Studio uses Google Maps and requires either recognized place names or latitude and longitude columns. Ambiguous location data (e.g., city names that exist in multiple countries) can cause geocoding errors and misplaced pins on the map.
- Looker Studio's filter controls (date range, dropdown, slider) apply to all charts by default, but cross-filtering behavior between charts is limited compared to tools like Power BI. Achieving consistent interactive filtering across all visuals required careful configuration of each filter's scope.
- The treemap chart in Looker Studio has limited sorting and label customization options, which can make smaller segments harder to read when department sizes are close to each other.
- The sharp spike in the hiring trend line near 2018–2020 may reflect real growth or could be a data quality issue (e.g., missing historical hire dates defaulting to a recent date). This needs validation against the source system.
- Looker Studio reports are tied to a Google account, and sharing with external stakeholders requires managing view permissions carefully to avoid unintended public access.

---

## Recommendations for Improvement

- Add an attrition breakdown chart — a bar or stacked column showing exit rate by department, gender, and job level — so HR can identify which segments are driving the overall 10.30% exit rate rather than seeing it as a single aggregate number.
- Pre-compute the median salary in the data source (via a BigQuery query or Google Sheets formula) and bring it into Looker Studio as a ready-made field, rather than attempting to approximate it with calculated fields, which are unreliable for median calculations.
- Include a salary distribution histogram or grouped bar chart to show the spread of compensation within each department or job level, providing more context than the current total-salary bar chart.
- Add a tenure analysis chart showing average years of service by department or role, complementing the hiring trend line and helping identify retention patterns.
- Replace or supplement the world map with a table or bar chart showing headcount by country or region, since map dots are difficult to interpret precisely when employee counts are small in certain regions.
- Add a headcount over time chart showing active employee count by month rather than raw record count by hire year, giving a cleaner picture of net workforce growth.
- Create a second report page dedicated to attrition detail, and link to it from the exit rate scorecard using Looker Studio's page navigation feature, so the summary page stays clean while deeper analysis is still accessible.
- Add conditional formatting to the top-10 salary table to visually flag employees who are significantly above or below the median for their job level.
- Use Looker Studio's scheduled email delivery feature to automatically send a PDF snapshot of the dashboard to HR stakeholders on a weekly or monthly basis, removing the need for them to log in manually.
- Add a "data last updated" date scorecard to the dashboard so viewers always know how current the figures are, especially if the Google Sheets source is updated manually rather than on an automated schedule.
