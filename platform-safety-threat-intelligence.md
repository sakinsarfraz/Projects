## Project Overview
Analysis of Snapchat's H1 2024 Transparency Report examining platform safety 
enforcement patterns across 200+ countries. This project demonstrates threat 
intelligence analysis skills including geographic threat distribution, category-based 
risk assessment, and content moderation effectiveness metrics.

## Why This Is Security Work

**Content moderation IS security operations:**
- Detecting harmful content = Detecting malicious activity
- Categorizing violations = Categorizing security incidents  
- Geographic threat patterns = Understanding attack origins
- Response time metrics = Incident response performance
- Enforcement effectiveness = Security control effectiveness

Major tech companies employ entire Trust & Safety teams (security professionals) 
to handle exactly this type of analysis.

## Dataset
- **Source:** Snapchat Transparency Report (H1 2024)
- **Scale:** 22,988 enforcement records
- **Coverage:** 200+ countries, 15+ violation categories
- **Metrics:** Enforcements, unique accounts, response times

## Key Investigations

### 1. Geographic Threat Distribution
**Question:** Where do different types of harmful content originate?

**Finding:** 
- United States accounts for 38% of global enforcements
- Afghanistan shows highest child exploitation enforcement rate
- Paraguay has highest enforcements-per-account ratio (14:1 for weapons)

**Security Implication:** 
Geographic patterns reveal where specific threat types concentrate, enabling 
targeted prevention and faster response.

### 2. Threat Category Analysis  
**Question:** What types of harmful content are most prevalent?

**Approach:**
- Analyzed enforcement distribution across 15 violation categories
- Calculated total enforcements by threat type
- Identified highest-risk categories

**Finding:**
Weapons-related content: 234,512 total enforcements worldwide

**Security Implication:**
Understanding threat category distribution helps prioritize detection resources.

### 3. Response Effectiveness Metrics
**Question:** How quickly does the platform respond to different threat types?

**Approach:**
- Analyzed median turnaround time by violation category
- Examined relationship between response time and enforcements per account
- Focused on EU countries for weapons-related content

**Finding:**
Response times vary significantly by threat type and geography, suggesting 
different detection mechanisms and severity prioritization.

### 4. Enforcement Efficiency Analysis
**Question:** Which enforcement patterns suggest repeat offenders vs. mass violations?

**Created metric:** Enforcements per unique account
- High ratio = repeat offenders or multi-violation accounts
- Low ratio = distributed threats across many accounts

**Finding:**
Paraguay weapons violations show 14:1 ratio - suggesting concentrated threat 
from small number of accounts vs. widespread violations.

## Technical Challenges

### Data Tidying (The Hard Part)
This dataset required extensive cleaning:
- Converted character values to numeric
- Reshaped long data (22,988 rows) into analysis-ready format
- Pivoted metrics into columns for country-category analysis
- Handled missing values and NA coercion
- Filtered multi-level categorical data

**Code example:**
```r
# Multi-condition filtering for specific threat intelligence
tands <- snapchat[snapchat$section == "Overview of Our T&S Enforcements" & 
                  snapchat$category == "Country", ]

# Reshaping for analysis
tands <- spread(tands, key = metric, value = value)

# Creating enforcement effectiveness metric
tands$enforcements_per_account <- 
  tands$total_enforcements / tands$total_unique_accounts_enforced
```

### Geographic Analysis
- Filtered 27 EU countries for regional threat analysis
- Cross-referenced country lists with violation types
- Created visualizations showing response time vs. enforcement patterns

## Skills Demonstrated

**Threat Intelligence:**
- Geographic threat distribution analysis
- Threat categorization and prioritization
- Pattern recognition across threat types
- Enforcement effectiveness assessment

**Data Analytics:**
- Complex data reshaping (long to wide)
- Multi-condition filtering
- Calculated metrics creation
- Geographic data analysis
- Statistical analysis (percentages, ratios, distributions)

**Technical:**
- R (tidyr, dplyr, ggplot2)
- Data cleaning and validation
- Missing data handling
- Categorical data analysis

## Blue Team Relevance

### Trust & Safety = Security Operations

This analysis mirrors what Trust & Safety teams (security roles at tech companies) do:

1. **Abuse Pattern Detection:** Identifying where threats originate (like analyzing attack sources)

2. **Threat Categorization:** Classifying violations by type (like categorizing security incidents)

3. **Response Time Analysis:** Measuring how quickly threats are addressed (incident response metrics)

4. **Geographic Intelligence:** Understanding regional threat patterns (like analyzing attack origins by country)

5. **Effectiveness Metrics:** Calculating enforcements per account (like measuring SOC alert-to-incident ratios)

**Real-world application:**
- Meta employs 40,000+ content moderators (security professionals)
- Google's Trust & Safety team works alongside traditional security
- These roles require exactly this type of threat pattern analysis

## Personal Context

Understanding platform dynamics informed this analysis. Snapchat's primary 
demographic (13-24 year olds) and use cases (ephemeral messaging, dating) 
create specific threat profiles. This domain knowledge helps interpret patterns:

- Why child exploitation enforcement is high in certain regions
- Why weapons content appears on a messaging platform
- Platform-specific risks vs. general social media threats

**Security lesson:** Domain expertise improves threat analysis quality.

## Key Findings Summary

- **Geographic concentration:** 38% of enforcements from US despite global platform
- **Threat category:** 234K+ weapons-related enforcements globally
- **Response efficiency:** Turnaround times vary by threat type and region
- **Enforcement patterns:** High enforcements-per-account ratios suggest 
  concentrated threats vs. distributed violations

## Lessons Learned

**Data cleaning is unglamorous but essential:**
The most challenging part wasn't the analysis - it was reshaping messy 
transparency report data into analyzable format. Real-world security data 
is never clean.

**Context matters:**
Understanding the platform (Snapchat's demographics, use cases, features) 
improved interpretation of enforcement patterns.

**Pattern recognition over volume:**
The interesting insights weren't in total numbers but in relative patterns - 
which countries had disproportionate violations, which categories showed 
concerning trends.

## Future Analysis

- Time-series analysis across multiple transparency reports
- Correlation between enforcement actions and public safety incidents
- Comparison across platforms (Snapchat vs. Instagram vs. TikTok)
- Predictive modeling for emerging threat categories

---

**Author:** Sakina [Last Name]  
**Contact:** [LinkedIn] | [Email]  
**Institution:** University of Pennsylvania, BASc Mathematics & Data Analytics
