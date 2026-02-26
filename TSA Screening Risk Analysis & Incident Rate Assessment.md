# TSA Screening Risk Analysis & Incident Rate Assessment

## Project Overview
Analysis of TSA checkpoint records from 2022 to assess airport-level risk patterns and incident rates. This project demonstrates data analytics skills applicable to security operations and threat intelligence.


This analysis was completed as a final exam project for DATA 2100 (Introduction 
to Data Analytics) at the University of Pennsylvania. The project has been 
reframed with a security analytics lens to demonstrate skills applicable to 
threat detection and security operations.


**Original Assignment:** Analyze TSA checkpoint and firearm confiscation data 
to identify patterns and insights.

**Security-Focused Reframe:** Displayed my findings through a security lens - 
risk assessment and threat patterns.

**Note:** This represents foundational analytical work.  

## Dataset
- **Source:** Transportation Security Administration (TSA) checkpoint data (2022)
- **Coverage:** All major US airports, hourly checkpoint data
- **Additional data:** Firearm confiscation records (2022)

## Key Investigations

### 1. High-Risk Airport Identification
**Question:** Which airports show high security threat indicators?

**Approach:**
- Calculated firearm confiscation rates 
- Identified statistical outliers
- Analyzed risk relative to airport size

**Finding:** 
Orlando International (MCO) shows a confiscation rate of 7.3 per 100K travelers - significantly higher than comparable airports. Among airports with 10+ confiscations, MCO represents the highest relative risk.

**Security Implication:** Elevated relative detection rate suggests further investigation may be warranted to understand contributing factors.

### 2. Temporal Threat Pattern Analysis
**Question:** When are security risks most concentrated?

**Approach:**
- Built function to identify peak threat windows by airport
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

![Daily Checkpoint Traffic](visualizations/checkpoint_traffic.png)

### 4. Threat Volume Analysis
**Question:** Which airports detected the most security threats in 2022?

**Finding:**
Hartsfield-Jackson Atlanta (ATL) confiscated 448 firearms - the highest in the nation. However, when adjusted for passenger volume, smaller airports show higher relative risk rates.


## Technical Implementation

### Data Processing
- Cleaned and validated checkpoint names across airports
- Merged checkpoint volume data with security incident data
- Handled missing values and data inconsistencies

### Analysis Techniques
- Aggregation and grouping across temporal and geographic dimensions
- Statistical risk scoring 

### Tools & Technologies
- **R** (data manipulation, statistical analysis)
- **ggplot2** (data visualization)
- **dplyr** (data transformation)
- Base R (loops, functions, aggregation)

## Skills Demonstrated

**For Security Operations:**
- Anomaly detection in large datasets (critical for SIEM log analysis)
- Risk scoring and threat assessment (prioritizing alerts)
- Temporal pattern recognition (identifying attack windows)
- Data-driven investigation (threat hunting methodology)

**For Data Analytics:**
- Large-scale data processing (2.7M records)
- Statistical analysis and outlier detection
- Data merging and integration
- Visualization for stakeholder communication



## Key Takeaways

- **Volume ≠ Risk:** Largest airports don't always have highest relative threat rates
- **Temporal Patterns:** Security threats concentrate at specific times requiring adaptive resource allocation  
- **Outlier Detection:** Statistical analysis reveals security anomalies not visible in aggregate data
- **Data-Driven Security:** Large-scale data analysis enables proactive rather than reactive security postures

## Future Enhancements

- Integrate weather data to assess environmental impact on security incidents
- Analyze seasonal patterns in threat detection
- Build predictive models for security resource planning
- Expand analysis to include other security incident types beyond firearms

## Code & Reproducibility

Full analysis code available in `analysis.Rmd`. All visualizations and findings are reproducible from the source data.

---

**Author:** Sakina Sarfraz 
**Contact:** sarfraz1@sas.upenn.edu  
**Institution:** University of Pennsylvania, BASc Mathematics & Data Analytics
