# TSA Screening Analysis: Firearm Confiscation Patterns and Airport Operations

## Project Overview
This project analyzes 2022 Transportation Security Administration (TSA) checkpoint traffic and firearm confiscation data to examine passenger throughput, airport-level confiscation patterns, and temporal variation in screening activity.


This was completed as a final exam project for DATA 2100 (Introduction 
to Data Analytics) at the University of Pennsylvania. I reframed the findings through a security analytics lens to explore how data analysis can support security operations, resource planning, and the identification of patterns.


**Original Assignment:** Analyze TSA checkpoint and firearm confiscation data 
to identify patterns and insights.

**Security Analytics Focus:** Examine firearm confiscation rates, passenger traffic patterns, and differences in screening activity across airports and checkpoints.
 


## Key Investigations

### 1. Philadelphia International Airport: Checkpoint Activity

**Question:** How many people passed through Terminal B at Philadelphia International Airport (PHL) at 8:00 AM on January 5, 2022?

**Approach:**

- Loaded the TSA checkpoint data for January 2–8, 2022.
- Filtered the dataset by airport, checkpoint, date, and hour.
- Retrieved the corresponding passenger check-in count.

**Finding:** A total of 486 people passed through Checkpoint B at Philadelphia International Airport at 8:00 AM on January 5, 2022.

**Security and operational implications:**

Checkpoint-level traffic data provides a snapshot of passenger-processing demand at a specific time and location. This information can support analysis of checkpoint utilization and help establish a baseline for understanding how passenger volumes vary throughout the day.

### 2. TSA Checkpoint Dataset Construction

**Question:** How can all TSA checkpoint records from 2022 be combined into a single dataset, and what are its dimensions?

**Approach:**

- Loaded the available 2022 TSA checkpoint CSV files using a loop.
- Combined the individual datasets into one data frame.
- Examined the dimensions of the resulting dataset.

**Finding:** The combined dataset contained 2,708,662 observations and 12 variables.

Combining multiple files into a single dataset provides a consistent foundation for analyzing passenger traffic across airports, checkpoints, and time periods for producing meaningful operational and security-related findings.

### 3. Philadelphia International Airport: Daily Checkpoint Traffic

**Question:** How many people passed through each Philadelphia checkpoint each day in 2022?

**Approach:**

- Filtered the combined dataset to include Philadelphia International Airport.
- Aggregated passenger check-ins by checkpoint and date.
- Used the resulting data to compare daily traffic patterns across checkpoints.

**Finding:**

Checkpoint D/E consistently recorded the highest passenger throughput in the resulting analysis, followed by Checkpoint B, A East, Checkpoint C, A West Sec 7, and Checkpoint F.

The relative ordering appeared stable throughout the year, suggesting that passenger traffic was not distributed evenly across checkpoints.

**Security and operational implications:**

Differences in checkpoint traffic can help identify locations with greater passenger-processing demand. Checkpoints handling larger volumes may require corresponding staffing, lane capacity, and operational resources. However, higher passenger throughput alone does not indicate a higher security threat.

### 4. Temporal Passenger Throughput Analysis

**Question:** When are Newark (EWR), John F. Kennedy (JFK), and LaGuardia (LGA) airports busiest on average?

**Approach:**

Developed a reusable R function to identify the time of day associated with the highest average passenger throughput at a specified airport.
Applied the function to EWR, JFK, and LGA using the 2022 TSA checkpoint dataset.

**Findings:**

Newark (EWR): 4:00 PM
John F. Kennedy (JFK): 5:00 PM
LaGuardia (LGA): 9:00 AM

These are the peak hours identified by the analysis.

**Security and operational implications:**

Identifying peak passenger throughput periods can support staffing decisions, queue management, and checkpoint resource allocation. From an operational security perspective, understanding when screening demand is highest can help planners anticipate workload.

Passenger volume should not be interpreted as a direct measure of threat likelihood. Further data would be needed to determine whether firearm confiscations or other security incidents also vary by time of day.

### 5. National Firearm Confiscation Volume

**Question:** Which airport confiscated the most firearms in 2022, and how many were confiscated?

**Approach:**

- Loaded the 2022 TSA firearm confiscation dataset.
- Counted confiscation records by airport.
- Identified the airport with the highest total.

**Finding:** Hartsfield–Jackson Atlanta International Airport (ATL) recorded 448 firearm confiscations, the highest total identified in the dataset.

**Security and operational implications:**

Firearm confiscation counts provide an indicator of the volume of detected firearms associated with airport screening. Airports with higher totals may have greater screening workloads or serve larger passenger populations.

Absolute counts do not establish which airport has the highest underlying security risk. Passenger throughput, screening practices, and other contextual factors should be considered when comparing airports.

### 6. Airport-Level Firearm Confiscation Rates

**Question:** Among airports with more than 10 firearm confiscations, which had the highest confiscation rate relative to passenger throughput?

**Approach:**

- Aggregated annual TSA checkpoint check-ins by airport.
- Aggregated firearm confiscation records by airport.
- Merged the datasets and recorded zero confiscations for airports without matching confiscation records.
- Calculated confiscations relative to passenger throughput.
- Restricted the comparison to airports with more than 10 confiscations.

**Finding:** Orlando International Airport (MCO) recorded the highest reported confiscation rate among airports meeting the more-than-10-confiscations threshold, at 7.34 in the reported calculation.


**Security and operational implications:**

Normalizing firearm confiscation counts by passenger throughput enables more meaningful comparisons than raw totals alone. An airport with fewer travelers may record fewer confiscations overall but have a higher confiscation rate.

An elevated rate may warrant further investigation into contributing factors. However, the rate measures detected firearms relative to recorded passenger throughput, not the total number of firearms carried or the airport's underlying security risk.

### 7. Firearm Confiscations Compared with Passenger Throughput

**Question:** Which airports stand out when firearm confiscation counts are compared with passenger volume?

**Approach:**

- Filtered the merged airport dataset to include airports with more than 10 firearm confiscations.
- Created a scatterplot comparing passenger throughput with firearm confiscation counts.
- Examined airports that appeared notably high or low relative to the general pattern.

**Findings:**

Several airports stood out:

Hartsfield–Jackson Atlanta International Airport (ATL): Recorded 448 firearm confiscations, the highest absolute total.
Dallas/Fort Worth International Airport (DFW): Also showed a comparatively high confiscation count.
Los Angeles International Airport (LAX) and Miami International Airport (MIA): Had lower confiscation counts relative to their passenger volumes in the initial comparison.

These observations highlight differences in the relationship between passenger throughput and detected firearm confiscations. The exact relative positions and rates should be confirmed against the annual totals used in the final visualization.

![Daily Checkpoint Traffic](visualizations/checkpoint_traffic.png) 

**Security and operational implications:**

Comparing confiscation counts with passenger throughput provides additional context for interpreting airport-level screening patterns. High absolute counts may indicate greater screening workload, while higher normalized rates can identify airports for further investigation.

Neither measure independently establishes screening effectiveness or the prevalence of firearms among travelers. Differences may reflect passenger volume, traveler behavior, screening procedures, and other factors that require additional data to evaluate.

## Technical Implementation
### Data Processing:

- Loaded and combined multiple TSA checkpoint CSV files using loops.
- Filtered and subsetted records by airport, checkpoint, date, and time.
- Aggregated passenger check-ins by checkpoint, date, and airport.
- Merged annual checkpoint traffic and firearm confiscation datasets.
- Handled missing confiscation counts when merging datasets.

### Analytical Techniques:
- Exploratory data analysis (EDA).
- Geographic and temporal comparisons.
- Aggregation and grouping across multiple dimensions.
- Calculation of normalized firearm confiscation rates.
- Development of reusable R functions.
- Identification and interpretation of patterns in passenger throughput and confiscation data.

### Tools and Technologies: 
- R: Data manipulation, aggregation, functions, and statistical summaries.
- dplyr and tidyr: Data transformation and reshaping.
- ggplot2: Data visualization.
- Base R: Loops, filtering, aggregation, merging, and function development.
  
## Key Takeaways:
**Security Analytics Insights:**
Passenger throughput varies across checkpoints and time periods. These patterns can inform operational planning and resource allocation.
Absolute confiscation counts and normalized rates provide different perspectives. ATL had the highest confiscation count, while MCO had the highest reported rate among airports with more than 10 confiscations.
Comparative analysis identifies patterns for further investigation. Differences between airports become more interpretable when confiscation counts are considered alongside passenger throughput.
Operational indicators require context. Neither passenger volume nor firearm confiscation rates alone establish underlying security risk or screening effectiveness.

**Technical Skills Demonstrated:**
- Combining and validating large datasets.
- Automating data ingestion with loops.
- Developing reusable functions for analysis.
- Aggregating data across geographic and temporal dimensions.
- Calculating and interpreting normalized metrics.
- Creating visualizations to communicate analytical findings.



By combining checkpoint traffic records with firearm confiscation data, I examined both absolute counts and normalized rates to identify patterns that raw totals alone might not reveal. 

The findings provide a descriptive view of recorded screening activity rather than a definitive assessment of airport security risk. 


---

**Author:** Sakina Sarfraz   
**Institution:** University of Pennsylvania, BASc Mathematics & Data Analytics
