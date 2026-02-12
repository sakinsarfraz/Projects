# Platform Safety Intelligence: Geographic Threat Pattern Analysis

## Project Overview
Analysis of Snapchat's H1 2024 Transparency Report examining platform safety enforcement patterns across 200+ countries. This project demonstrates threat intelligence analysis skills including geographic threat distribution, category-based risk assessment, content moderation effectiveness metrics, and repeat offender detection.

## Why This Is Security Work

**Content moderation IS security operations:**
- Detecting harmful content = Detecting malicious activity
- Categorizing violations = Categorizing security incidents  
- Geographic threat patterns = Understanding attack origins
- Response time metrics = Incident response performance
- Enforcement effectiveness = Security control effectiveness

Major tech companies employ entire Trust & Safety teams (security professionals) to handle exactly this type of analysis. These teams work alongside traditional cybersecurity teams to protect users and platforms.

## Dataset
- **Source:** Snapchat Transparency Report (H1 2024)
- **Scale:** 22,988 enforcement records
- **Coverage:** 200+ countries, 15+ violation categories
- **Metrics:** Total enforcements, unique accounts impacted, median response times

## Key Investigations

### 1. Repeat Offender Detection
**Question:** Which enforcement patterns suggest repeat offenders vs. distributed threats?

**Approach:**
Created new metric: Enforcements per unique account
- High ratio = concentrated violations (repeat offenders)
- Low ratio = distributed threats across many accounts

**Finding:**
Paraguay weapons violations: 14 enforcements from 1 unique account (14:1 ratio) - the highest enforcement-per-account ratio globally. This suggests a single repeat offender posting multiple weapons violations rather than widespread weapons content.

**Code:**
```r
tands$enforcements_per_account <- 
  tands$total_enforcements / tands$total_unique_accounts_enforced

max_row <- tands[which.max(tands$enforcements_per_account), ]
# Result: Paraguay, Weapons category, 14:1 ratio
```

**Security Implication:**
Detecting repeat offenders enables targeted account removal rather than reactive content moderation. This metric could trigger automatic escalation for accounts with ratios > 5:1, flagging potential coordinated bad actors or persistent violators.

### 2. Geographic Concentration Analysis
**Question:** What percentage of global enforcement comes from specific countries?

**Approach:**
- Calculated total worldwide enforcements
- Isolated United States enforcement totals
- Computed percentage of global activity

**Finding:**
United States accounts for 38% of all global enforcements despite being one country among 200+ covered in the report.

**Code:**
```r
total_worldwide <- sum(tands$total_enforcements, na.rm = TRUE)
us_total <- sum(tands$total_enforcements[tands$country == "United States"], 
                na.rm = TRUE)
us_percent <- (us_total / total_worldwide) * 100
# Result: 38.09%
```

**Security Implication:**
Geographic concentration suggests either:
- Higher actual violation rates in certain regions
- More effective detection/reporting mechanisms
- Cultural/usage pattern differences

Further analysis would be needed to distinguish between these possibilities. Understanding geographic distribution helps allocate moderation resources and develop region-specific detection strategies.

### 3. Threat Category Distribution
**Question:** What types of harmful content require the most enforcement action?

**Approach:**
- Filtered dataset by violation type
- Aggregated total enforcements by category
- Analyzed category-level threat volume

**Finding:**
Weapons-related content: 234,512 total enforcements worldwide across all countries.

**Code:**
```r
weapons_rows <- tands[tands$type == "Weapons", ]
total_weapons <- sum(weapons_rows$total_enforcements, na.rm = TRUE)
# Result: 234,512
```

**Security Implication:**
Understanding threat category prevalence helps:
- Allocate detection resources to high-volume categories
- Prioritize automation efforts
- Benchmark platform safety effectiveness
- Identify emerging threat patterns

### 4. Response Effectiveness Analysis
**Question:** How quickly does the platform respond to different threat types across regions?

**Approach:**
- Analyzed median turnaround time by violation category
- Examined relationship between response time and enforcements per account
- Focused on EU countries (27 nations) for weapons-related content

**Finding:**
Response times vary significantly by threat type and geography. Created visualization showing the relationship between response speed and enforcement concentration for EU weapons violations.

**Visualization:**
```r
eu_countries <- c("Austria", "Belgium", "Bulgaria", "Croatia", "Cyprus", 
                  "Czech Republic", "Denmark", "Estonia", "Finland", "France", 
                  "Germany", "Greece", "Hungary", "Italy", "Latvia", "Lithuania", 
                  "Luxembourg", "Malta", "Netherlands", "Poland", "Portugal", 
                  "Romania", "Slovakia", "Slovenia", "Spain", "Sweden")

eu_weapons <- tands[tands$country %in% eu_countries & tands$type == "Weapons", ]

ggplot(eu_weapons, aes(x = median_turnaround_time_minutes, 
                       y = enforcements_per_account, label = country)) +
  geom_point(size = 1) +
  geom_text(vjust = -0.5, size = 2) +
  coord_flip() +
  labs(title = "EU: Enforcements per Account vs Median Turnaround Time (Weapons)",
       x = "Median Turnaround Time (minutes)",
       y = "Enforcements per Account")
```

**Security Implication:**
Response time metrics reveal operational effectiveness and help identify bottlenecks in content moderation workflows. Faster response times for high-severity violations (like child exploitation) vs. lower-severity violations (like spam) would indicate appropriate prioritization.

## Technical Challenges

### Data Tidying (The Hard Part)
This dataset required extensive cleaning before analysis was possible:

**Challenges faced:**
- Data arrived in long format (22,988 rows × 7 columns)
- Values stored as character strings instead of numeric
- Multi-level categorical structure (section → category → sub_category)
- Needed to reshape for country-violation analysis
- Missing values requiring NA handling

**Data transformation process:**
```r
# Convert character values to numeric
snapchat$value <- as.numeric(snapchat$value)

# Filter to relevant enforcement data
tands <- snapchat[snapchat$section == "Overview of Our T&S Enforcements" & 
                  snapchat$category == "Country", ]

# Remove redundant columns
tands$section <- NULL
tands$category <- NULL
tands$period <- NULL

# Rename for clarity
names(tands)[names(tands) == "sub_category_1"] <- "country"
names(tands)[names(tands) == "sub_category_2"] <- "type"

# Reshape from long to wide format
tands <- spread(tands, key = metric, value = value)
```

**Result:** Transformed messy transparency report data into analysis-ready format where each row represents a unique country-violation type pairing with all metrics accessible.

**Lesson learned:** Real-world security data is rarely clean. Data wrangling skills are as important as analytical skills.

### Geographic Analysis
- Compiled list of 27 EU countries for regional analysis
- Cross-referenced country lists with violation types
- Created focused visualizations for regional threat patterns
- Handled country name variations and missing data

## Skills Demonstrated

### Threat Intelligence
- Geographic threat distribution analysis
- Threat categorization and prioritization
- Pattern recognition across threat types
- Enforcement effectiveness assessment
- Repeat offender detection methodology

### Data Analytics
- Complex data reshaping (long to wide format)
- Multi-condition filtering and subsetting
- Calculated metrics creation
- Geographic data analysis
- Statistical analysis (percentages, ratios, distributions)
- Missing data handling

### Technical Skills
- **R** (tidyr, dplyr, ggplot2)
- Data cleaning and validation
- Categorical data analysis
- Data visualization
- Metric development

## Blue Team Relevance

### Trust & Safety = Security Operations

This analysis demonstrates the same skills that Trust & Safety teams (security roles at tech companies) use daily:

**1. Threat Pattern Detection**
Identifying where threats originate and concentrate (like analyzing attack sources and geographic distribution in cybersecurity)

**2. Threat Categorization**
Classifying violations by type and severity (like categorizing security incidents: malware, phishing, DDoS, etc.)

**3. Response Time Analysis**
Measuring how quickly threats are addressed (incident response performance metrics)

**4. Geographic Intelligence**
Understanding regional threat patterns (like analyzing botnet locations or attack origins by country)

**5. Effectiveness Metrics**
Calculating enforcements per account (like measuring SOC alert-to-incident ratios or false positive rates)

**6. Repeat Offender Detection**
Identifying persistent bad actors (like tracking repeat attackers or insider threats)

### Real-World Context

- **Meta** employs 40,000+ content moderators (security/safety professionals)
- **Google's** Trust & Safety team works alongside traditional cybersecurity teams
- **TikTok, Snap, Reddit** all have dedicated safety operations centers
- These roles require exactly this type of threat pattern analysis and geographic intelligence

Trust & Safety job postings specifically request skills in:
- Abuse pattern analysis ✓
- Data-driven investigation ✓
- Threat categorization ✓
- Geographic distribution analysis ✓
- Metrics development ✓

## Personal Context & Domain Knowledge

Understanding platform dynamics informed this analysis. Snapchat's primary demographic (ages 13-24) and common use cases create specific threat profiles that differ from other social platforms.

**Domain knowledge applied:**
- Why certain violation categories appear more frequently on ephemeral messaging platforms
- How platform features (disappearing messages, location sharing) create unique safety challenges
- Platform-specific risks vs. general social media threats

**Security lesson:** Domain expertise significantly improves threat analysis quality. Understanding the environment you're protecting is as important as the analytical techniques themselves.

## Key Takeaways

### Analytical Insights
- **Geographic concentration:** 38% of global enforcements from one country suggests uneven threat distribution or detection capabilities
- **Repeat offenders exist:** High enforcement-per-account ratios (14:1) indicate persistent bad actors requiring different mitigation strategies
- **Threat category volumes:** 234K+ weapons violations globally shows scale of platform safety challenges
- **Pattern over volume matters:** Most interesting insights came from relative patterns (ratios, percentages) rather than absolute numbers

### Technical Lessons
- **Data cleaning is unglamorous but essential:** Spent more time reshaping data than analyzing it - this reflects real-world security work
- **Context drives interpretation:** Understanding Snapchat's user base and features improved pattern recognition
- **Metrics tell stories:** Simple calculated metrics (enforcements per account) revealed patterns invisible in raw data
- **Visualization clarifies complexity:** Geographic and categorical visualizations made 22K+ records understandable

## Future Enhancements

Potential extensions of this analysis:

**Time-Series Analysis:**
- Compare multiple transparency reports over time
- Identify trending threat categories
- Measure enforcement effectiveness changes
- Detect emerging threat patterns

**Cross-Platform Comparison:**
- Benchmark Snapchat vs. Instagram vs. TikTok
- Identify platform-specific threat profiles
- Compare response time effectiveness
- Analyze category distribution differences

**Predictive Modeling:**
- Build models to predict high-risk countries/categories
- Forecast enforcement resource needs
- Identify early warning indicators for emerging threats

**Deep-Dive Regional Analysis:**
- Investigate why certain countries show unusual patterns
- Correlate with external factors (regulations, events, demographics)
- Develop region-specific safety strategies

## Code & Reproducibility

Full analysis code available in repository. All findings are reproducible from the source Snapchat Transparency Report data (H1 2024).

**Analysis workflow:**
1. Data import and exploration
2. Data cleaning and reshaping
3. Metric calculation
4. Geographic and categorical analysis
5. Visualization creation

---

**Author:** Sakina [Last Name]  
**Contact:** [LinkedIn] | [Email]  
**Institution:** University of Pennsylvania, BASc Mathematics & Data Analytics



## Research Context

**Background:**
This project emerged from interest in the intersection of platform safety, 
criminal threat intelligence, and regional security dynamics. As a data 
analytics researcher based in the Gulf region, I wanted to understand how 
high-severity platform violations manifest in this specific geographic and 
cultural context.

**Why high-severity categories?**
Child exploitation, weapons trafficking, drug distribution, and terrorism 
represent the most serious threats on digital platforms. Unlike policy 
violations, these categories:
- Have criminal statutes across jurisdictions
- Require law enforcement coordination
- Cause real-world physical harm
- Are priority areas for trust & safety operations

**Why the GCC specifically?**
The Gulf region offers a unique analytical lens:
- Shared regulatory frameworks
- Common cultural and legal context
- High social media penetration among youth (primary user demographic)
- Coordinated law enforcement structures

**Regional expertise:**
Being based in the region provides contextual understanding of factors that 
influence both violation patterns and platform response strategies—insights 
that aggregate global analysis might miss.

**Career relevance:**
This work demonstrates skills directly applicable to Trust & Safety analyst, 
Threat Intelligence analyst, and SOC analyst roles requiring:
- Criminal threat pattern recognition
- Geographic risk assessment
- Severity-based prioritization
- Cross-border threat analysis




### Finding: Enforcement Concentration

**Observation:**
Saudi Arabia accounts for [X]% of high-severity enforcements among GCC 
countries, significantly higher than other nations in the region.

**Potential Explanations:**

This pattern could reflect several factors:

1. **User Base Size:** Saudi Arabia has the largest population among GCC 
   countries (~35M vs. UAE ~10M, Qatar ~3M). If Snapchat penetration is 
   similar, higher absolute numbers are expected.

2. **Detection Effectiveness:** Higher enforcement numbers may indicate more 
   effective violation detection rather than higher violation rates.

3. **Reporting Culture:** User reporting behavior may differ across countries, 
   with some markets more likely to flag violations.

4. **Usage Demographics:** If Saudi Snapchat skews younger (the primary 
   demographic for platform violations), this could explain higher volumes.

5. **Platform Prioritization:** Snapchat may allocate more moderation resources 
   to larger markets.

**Critical Note:** 
Without user population data, we cannot determine whether this represents 
higher violation *rates* or simply reflects larger user base size. Absolute 
numbers must be contextualized with user population to draw meaningful conclusions.

**Further Analysis Needed:**
- User population estimates by country
- Violations per capita or per user
- Comparison of violation rates (not just totals)




## GCC High-Severity Threat Analysis

### Key Findings

#### 1. Geographic Risk Distribution
**Analysis:** Calculated total enforcements and repeat offender rates across GCC countries.

**Finding:**
Saudi Arabia accounts for [X]% of high-severity enforcements in the GCC region, 
with [Y] total violations across [Z] categories.

**Key Metric - Repeat Offender Rate:**
- Saudi Arabia: [rate] enforcements per account
- UAE: [rate] enforcements per account
- Qatar: [rate] enforcements per account

**Interpretation:** 
[After you run the code, interpret whether Saudi's high total is due to volume 
(more users) or rate (more violations per user). If rate is similar to UAE, 
it's a population effect. If rate is higher, it's an actual pattern difference.]

#### 2. Violation Category Breakdown (Saudi Arabia)
**Analysis:** Examined which high-severity categories drive enforcement numbers.

**Finding:**
Top violation categories in Saudi Arabia:
1. [Category]: [number] enforcements
2. [Category]: [number] enforcements
3. [Category]: [number] enforcements

**Interpretation:**
[After seeing the data - is it CSE? Weapons? Sexual content? 
Explain what this might mean without jumping to conclusions]

#### 3. Regional Comparison: Saudi Arabia vs. UAE
**Analysis:** Compared two largest GCC markets across violation categories.

**Finding:**
[Create a simple comparison - where are they similar? Where different?]

**Interpretation:**
Similar patterns suggest regional norms; differences suggest market-specific factors 
(demographics, usage patterns, or detection effectiveness).

#### 4. Platform Response Effectiveness
**Analysis:** Measured average response times for high-severity violations by country.

**Finding:**
Average response times:
- [Country]: [X] minutes
- [Country]: [Y] minutes
- GCC average: [Z] minutes

**Interpretation:**
[Are response times similar across countries? Or does Saudi get faster/slower service?]

#### 5. Threat Concentration Patterns
**Analysis:** Identified repeat offender patterns (high enforcements per account).

**Finding:**
Categories with highest repeat offender rates in Saudi Arabia:
[Top 3 categories with high enforcements-per-account ratios]

**Security Implication:**
High ratios suggest concentrated threats from persistent bad actors rather than 
distributed violations across many users. These accounts warrant enhanced monitoring 
or immediate removal.



## Key Findings: GCC High-Severity Threat Analysis

### 1. Enforcement Volume vs. Rate

**Observation:**
Saudi Arabia accounts for 34,389 high-severity enforcements (55% of GCC total), 
significantly higher than other countries.

**Critical Finding:**
However, when adjusting for user base size, Saudi Arabia's violation rate 
(1.68 enforcements per account) is actually LOWER than Kuwait (1.94), Bahrain 
(1.78), and Qatar (1.70).

**Interpretation:**
The high enforcement volume reflects Saudi Arabia's larger Snapchat user base 
rather than higher violation rates. This is a population effect, not a behavioral 
pattern.

**Methodology Note:**
Without exact user population data, "enforcements per account" serves as a proxy 
for violation rate. Similar or lower rates suggest proportional violation patterns.

---

### 2. Category Distribution: Sexual Content Dominates

**Finding:**
Sexual content violations represent 75% of Saudi Arabia's high-severity 
enforcements (25,971 of 34,389 total).

**Category Breakdown:**
1. Sexual Content: 25,971 (75.6%)
2. Child Sexual Exploitation: 7,361 (21.4%)
3. Drugs: 5,738 (16.7%)
4. Weapons: 4,214 (12.3%)
5. Self-Harm & Suicide: 614 (1.8%)

**Note:** Percentages exceed 100% as individual accounts may violate multiple categories.

---

### 3. Repeat Offender Patterns

**Finding:**
Weapons violations show the highest repeat offender rate (1.89 enforcements 
per account), despite lower total volume.

**Security Implication:**
- **Weapons:** Concentrated threat (same users, multiple violations) → Targeted account removal
- **CSE:** Distributed threat (1.36 rate, different users) → Improved detection needed
- **Sexual Content:** Mixed pattern (1.80 rate) → Both approaches required

This distinction informs enforcement strategy prioritization.

---

### 4. Regional Comparison: Saudi Arabia vs. UAE

**Sexual Content:** Proportional to user base (1.2x difference)
**Drugs:** Disproportionate (7.4x difference)  
**Weapons:** Disproportionate (8.5x difference)
**Self-Harm:** Highly disproportionate (13x difference)

**Interpretation:**
While sexual content violations scale with population, drugs, weapons, and 
self-harm show significant concentration in Saudi Arabia beyond what user 
base size would explain.

**Potential Factors:**
- Detection effectiveness differences
- Reporting culture variations
- Demographic/usage pattern differences
- Platform feature adoption rates

Further research needed to identify root causes.

---

### 5. Platform Response Consistency

**Finding:**
Average response times range from 11-18 minutes across all GCC countries, 
with no significant outliers.

**Interpretation:**
Snapchat maintains consistent enforcement prioritization regardless of market 
size. Saudi Arabia (15.3 min) receives similar response times to smaller 
markets like Bahrain (11.4 min) and Qatar (11.7 min).

This suggests equitable resource allocation across the region.


# ===== INTERPRETATION SUMMARY =====

# Key Finding 1: Saudi has highest VOLUME but NOT highest RATE
# Conclusion: Population effect, not behavioral difference

# Key Finding 2: Sexual Content drives numbers (75%)
# Conclusion: This is the primary enforcement category

# Key Finding 3: Weapons show highest repeat offender rate (1.89)
# Conclusion: Concentrated threat requiring targeted removal

# Key Finding 4: Drugs/Weapons disproportionate in Saudi vs UAE
# Conclusion: Requires further investigation - not explained by population alone

# Key Finding 5: Response times consistent across GCC (11-18 min)
# Conclusion: Platform treats region equitably




