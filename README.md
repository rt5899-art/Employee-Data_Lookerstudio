# Employee Dashboard

## Project Overview

This repository contains an enterprise workforce analytics project developed using Google Looker Studio. The primary purpose of this project is to aggregate human resource metrics, salary structures, demographic breakdowns, and global distribution patterns into a centralized reporting interface. By consolidating disparate workforce data points, the dashboard addresses the challenge of siloed HR tracking, helping organizational leaders monitor employee counts, identify retention risks, evaluate compensation equity, and make data-driven decisions regarding talent acquisition and resource allocation.

#### Live Project Link: https://datastudio.google.com/s/tAOCWEsKxpI

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

### Requirements

Web Browser: Google Chrome, Mozilla Firefox, Safari, or Microsoft Edge (Latest versions)

Google Account: Required to access, edit, or copy the looker studio report template

Data Source: Standardized human resources database schema or flat files (Google Sheets, BigQuery, or CSV)

Accessibility: Internet connection with permissions enabling third-party map APIs (Google Maps)


---

## Tools and Technologies

Business Intelligence Platform: Google Looker Studio (formerly Data Studio)

Data Connectors: Google Sheets / Local CSV File Upload

Geospatial Service: Integrated Google Maps API

Presentation Layer: Custom Looker Studio Component Layout

---

## Dashboard Layout and Features

The dashboard is organized into a single page with the following components:


![image alt](https://github.com/rt5899-art/Employee-Data_Lookerstudio/blob/main/Empdata_looker%20studio.png?raw=true)

At the top, five KPI cards display the headline metrics: Total Employees (1,000), Working Employees (897), Median Salary ($92,806), Exit Rate (10.30%), and the Female-to-Male Ratio (1.06). Three filters sit in the top-left corner — a department dropdown, an age range slider, and a date range selector — which apply across all visuals simultaneously.

The middle row contains the top-10 salary leaderboard table on the left, a horizontal bar chart showing total annual salary by job title in the center, and a donut chart showing the gender split (53.2% female, 46.8% male) on the right.

The bottom row contains a line chart tracking the number of employee records by hire year from 1993 to 2020 on the left, a treemap showing headcount by department in the center, and a world map visual showing geographic employee distribution on the right.

---

## Key Insights

An evaluation of the metrics processed across the workforce analytics interface reveals the following operational insights:

High-Level Workforce Key Performance Indicators: The platform tracks a Total Employees baseline of 1,000 headcount records. Out of this total pool, the organization registers 897 Active Working Employees. Compensation tracking reveals a Median Salary of 92,806, paired with an overall organizational Exit Rate of 10.30%. The gender distribution metric shows a Female / Male Emp ratio of 1.06.

Top Individual Earners: Compensation analysis isolates individual top earners led by Everett Le at an Annual Salary of 350,690, followed by Harper Castillo at 290,348, Mia Navarro at 279,310, and Robert Rogers at 258,734.

Compensation Allocation by Job Tier: Aggregated salary volume is heavily concentrated within leadership and senior tiers. Vice President positions command the largest total salary footprint at approximately 24M, followed sequentially by Directors at approximately 17M, Sr. Managers at approximately 13M, and Managers at approximately 12M. Technical execution roles such as System Administrator, Cloud Infrastructure Architect, and Network Administrator reflect the lowest total baseline expenditure bars on the chart.

Gender Profile Distribution: The workforce splits into a 53.2% Female representation segment and a 46.8% Male representation segment across the 1,000 tracked individuals.

Historical Hiring Timelines: The historical record count line chart tracks hiring velocity over a multi-decade timeline. Hiring volume remained at a low baseline level between 1993 and 2003, fluctuated with moderate growth spikes between 2008 and 2013, and experienced an exponential surge after 2013, reaching its maximum operational expansion peak around 2018.

Departmental Infrastructure Breakdown: The workforce is distributed across four core operational divisions. Specialty Products leads as the largest department with 266 employees. Corporate and Research & Development share identical footprints with 254 employees each, while Manufacturing accounts for the remaining 226 employees.

Geographic Footprint: Global workforce mapping indicates a heavy distribution bubble centered within North America, paired with smaller, distributed operational footprints across South America and parts of Asia.

---

## Challenges Faced

- Looker Studio does not have a native `MEDIAN` function in calculated fields — computing median salary requires a workaround such as pre-aggregating the value in the data source (Google Sheets formula or BigQuery query) before connecting it to the report.
  
- The exit rate calculation depends on clearly defined employment status values in the data. If the source data uses inconsistent labels for terminated or resigned employees, the rate will be inaccurate without cleaning in the data source first, since Looker Studio has limited data transformation capabilities compared to Power Query.
  
- The age range slider control requires a clean numeric age field. If age is stored as a birth date, a calculated column must be created in Google Sheets or BigQuery to derive current age before it can be used as a filter.
  
- The map visual in Looker Studio uses Google Maps and requires either recognized place names or latitude and longitude columns. Ambiguous location data (e.g., city names that exist in multiple countries) can cause geocoding errors and misplaced pins on the map
  
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
