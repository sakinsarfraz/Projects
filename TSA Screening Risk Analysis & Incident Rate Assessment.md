# TSA Screening Risk Analysis & Incident Rate Assessment

## Project Overview
This project analyzes TSA checkpoint records/data from 2022 to assess airport-level risk patterns and incident rates. This project demonstrates data analytics skills applicable to security operations and threat intelligence.


This was completed as a final exam project for DATA 2100 (Introduction 
to Data Analytics) at the University of Pennsylvania. The project has been 
reframed with a security analytics lens to demonstrate skills applicable to 
threat detection and security operations.


**Original Assignment:** Analyze TSA checkpoint and firearm confiscation data 
to identify patterns and insights.

**Security-Focused Reframe:** Displaying the findings through a security lens with risk assessment and threat patterns.
 


## Key Investigations

### 1. High-Risk Airport Identification
**Question:** Which airports show a high security threat indicator?

**Approach:**
- Calculate firearm confiscation rates 

**Finding:** 
Orlando International (MCO) shows a confiscation rate of 7.3 per 100K travelers - significantly higher than comparable airports. Among airports with 10+ confiscations, MCO represents the highest relative risk.

**Security Implication:** Elevated rate suggests that further investigation may be needed to understand contributing factors.

### 2. Temporal Threat Pattern Analysis
**Question:** When are security risks most concentrated?

**Approach:**
- Built function to identify peak passenger throughput by airport
- Analyzed hourly checkpoint volume patterns
- Correlated temporal patterns with operational needs

**Findings:**
- Newark (EWR): Highest average passenger throughput at at 16:00 (4 PM)
- JFK: Highest average passenger throughput at 17:00 (5 PM)  
- LaGuardia (LGA): Highest average passenger throughput at 09:00 (9 AM)

**Security Implication:** These high-volume windows represent periods of increased exposure and may warrant proportional security staffing.

### 3. Checkpoint-Level Risk Assessment
**Question:** How is threat exposure distributed across airport terminals?

**Approach:**
- Aggregated daily traffic by checkpoint
- Analyzed traffic concentration patterns
- Identified high-volume security bottlenecks

**Finding:**
At Philadelphia International, Checkpoint D/E processes 3x more passengers than other checkpoints, creating a concentrated security exposure point.


### 4. Threat Volume Analysis
**Question:** Which airports detected the most security threats in 2022?

**Finding:**
Hartsfield-Jackson Atlanta (ATL) confiscated 448 firearms which was the highest in the nation.

![Daily Checkpoint Traffic](visualizations/checkpoint_traffic.png)


## Technical Implementation

### Data Processing
- Cleaned and validated checkpoint names across airports
- Handled missing values and data inconsistencies

### Analysis Techniques
- Aggregation and grouping across temporal and geographic dimensions
- Statistical risk scoring 

### Tools & Technologies
- **R** (data manipulation, statistical analysis)
- **ggplot2** (data visualization)
- **dplyr** (data transformation)
- Base R (loops, functions, aggregation)



---

**Author:** Sakina Sarfraz 
**Contact:** sarfraz1@sas.upenn.edu  
**Institution:** University of Pennsylvania, BASc Mathematics & Data Analytics
