# The Path to Crime

## Project Overview

This project examines the relationship between mental illness, drug use and violent crime in the United States. It seeks to understand whether mental health service access plays a role in reducing substance use and whether untreated mental health issues contribute to criminal behavior.

## Motivation

It is hard to understand why people turn to crime. Mental illnesses often go undiagnosed and many people self-medicate with drugs, leading to theft, violence and drug-related crimes. Could better mental health care and early intervention reduce crime? This project explores this connection and uses data science to find insights that can improve public safety and mental health outcomes.

## Hypotheses

**1. H₀:** There is no relationship between untreated mental illness, drug use, and crime rates.  
   **H₁:** Higher rates of undiagnosed mental illnesses are connected with increased use of drugs and this in turn contributes to higher crime rates.

**2. H₀:** The availability of mental health care services has no effect on drug use rates.  
   **H₁:** Areas with limited access to mental health services have significantly higher drug use rates.

**3. H₀:** The severity of untreated mental health disorders does not influence the likelihood of criminal behavior.  
   **H₁:** Individuals with severe, untreated mental health conditions are more likely to engage in criminal activity.
 
## Data Sources

- **SAMHSA – NSDUH State Estimates (2021–2022)**  
  State-level statistics on Any Mental Illness (AMI), Serious Mental Illness (SMI), and illicit drug use.

- **SAMHSA – National Mental Health Services Survey (N-MHSS) 2020**  
  Data on the number of mental health treatment facilities and patients served per state.

- **FBI Uniform Crime Reporting (UCR) 2022**  
  Violent crime rates per 100,000 residents, including assault, robbery, homicide, etc.

- **U.S. Census 2020 State Population Estimates**  
  Used for population normalization (e.g., facilities per 100k).

- **CDC Behavioral Risk Factor Surveillance System (BRFSS)**  
  Used for cross-checking behavioral health trends (not primary source).

- **NIMH (National Institute of Mental Health)**  
  Provided additional context on national-level mental health trends.

## Data Collection and Preparation

Datasets were cleaned and merged by U.S. state.  
Population normalized metrics include:

- Mental illness prevalence (AMI and SMI %)
- Drug use (% past-month illicit use)
- Violent crime rate (per 100,000)
- Number of mental health treatment facilities per 100,000 people

## Exploratory Data Analysis (EDA)

### Mental Illness vs. Drug Use
- Positive trend observed between AMI% and drug use (r ≈ 0.29)
- States like Oregon and Alaska show high AMI and high drug use
- Utah stands out with high AMI but low drug use (possibly due to cultural/religious factors)

### Drug Use vs. Crime
- Mild positive correlation observed (r ≈ 0.34)
- D.C. and New Mexico rank high in both drug use and violent crime
- Maine has high drug use but low crime - a notable outlier

### Service Access vs. Drug Use
- Unexpected result: states with more mental health facilities do not always have lower drug use
- Possible explanation: services are often expanded reactively in response to rising drug problems

### Service Access vs. Crime
- Slight negative trend between facility access and violent crime
- States with higher service access tend to show lower crime, though not universally (e.g. Alaska is an exception)

## Hypothesis Testing

### H1: Service Access → Drug Use
- Test: Two-sample t-test between low and high service access states
- Result: p-value ≈ 0.06 — not statistically significant
- Interpretation: Mixed results; some low-access states show lower drug use

### H2: Untreated Mental Illness → Drug Use / Crime
- AMI% vs. Drug Use: r ≈ 0.29  
- AMI% vs. Crime: r ≈ 0.24  
- Suggests correlation, but not strong enough for statistical significance  
- Example states with large treatment gaps: Oregon, Nevada

### H3: Severe Mental Illness → Crime
- SMI% vs. Crime: r ≈ 0.21  
- Regression model: Crime ~ SMI + Drug Use  
- Drug use is the stronger predictor  
- Conclusion: Weak direct link; the effect is likely mediated through substance use

## Data Description

| Feature | Description |
|--------|-------------|
| **State** | U.S. state name |
| **AMI%** | Percentage of adults with any mental illness |
| **SMI%** | Percentage with serious mental illness |
| **DrugUse%** | Percentage using illicit drugs (past month) |
| **ViolentCrimePer100k** | Violent crime rate per 100,000 population |
| **FacilitiesCount** | Number of mental health facilities |
| **MHClients** | Number of mental health patients served |
| **Population** | State population |
| **Facilities_per_100k** | Facilities per 100,000 people (normalized) |
| **MHClient_per_100k** | Mental health clients per 100,000 people (engineered) |
| **Log_CrimeRate** | Log-transformed crime rate for modeling (engineered) |

## Methods

The analysis began with exploratory data analysis (EDA), followed by hypothesis testing. To quantify relationships between variables, Linear Regression (a fundamental machine learning technique suitable for small, well-structured datasets) was applied.

For each hypothesis, their R² (coefficient of determination) values were used to evaluate explanatory power.
  
## Visualizations
  
### Correlation Heatmap
Shows the relationship between mental illness, drug use, service access and crime.
![Image](https://github.com/user-attachments/assets/97a66ce1-bcca-40a4-99db-2128e253b6eb)
  
### Drug Use vs. Mental Illness Rate (AMI%)
Highlights the positive association between mental illness rates and drug use across states.
![Image](https://github.com/user-attachments/assets/63de2136-7289-44ad-956b-5b91d93e84cf)
  
## Drug Use vs. Violent Crime Rate
Reveals a mild positive correlation between drug use and violent crime rates across states.
![Image](https://github.com/user-attachments/assets/30cce1d4-6be8-4f91-8fe3-1af03911a8ca)
  
## Facilities per 100k by State
Compares the availability of mental health facilities across states on a per capita basis.
![Image](https://github.com/user-attachments/assets/e462265b-b66b-48fd-828b-9f61ab7080d3)
  
## Facilities vs. Drug Use
Examines the relationship between mental health service access and drug use, showing a weak negative trend.
![Image](https://github.com/user-attachments/assets/512b474a-38e3-46ea-a31d-4cd2dd4993f3)
  
## Drug Use from Facility Access
Compares actual and predicted drug use rates based on facility access, highlighting predictive accuracy across states.
![Image](https://github.com/user-attachments/assets/4aaec21e-cb25-480a-ae07-0464d56fa006)

## AMI% vs Drug Use%
Displays a positive linear trend between any mental illness and drug use, showing a potential link between the two.
![Image](https://github.com/user-attachments/assets/8d995040-7813-436c-8776-62901d1df375)
  
## AMI% vs Violent Crime Rate
Shows a mild positive trend, suggesting that higher mental illness rates may slightly relate to increased violent crime.
![Image](https://github.com/user-attachments/assets/3f45bdc7-c53a-4073-a1d1-0de5c6fe6ae8)
  
## RF Prediction of Drug Use from AMI%
Random Forest model estimates state-level drug use based on mental illness rates.
![Image](https://github.com/user-attachments/assets/3f45bdc7-c53a-4073-a1d1-0de5c6fe6ae8)
  
## SMI% vs Violent Crime Rate
Shows a weak positive trend between serious mental illness rates and violent crime.
![Image](https://github.com/user-attachments/assets/34761668-3c5d-49bb-bc67-4af405381e0e)

## RF Prediction: Violent Crime from SMI% and Drug Use%
Visualizes how well the Random Forest model predicts violent crime based on serious mental illness and drug use rates.
![Image](https://github.com/user-attachments/assets/d76960ae-646b-43e1-b45c-855b7c3f45a3)
  
## Prediction Residuals: RF Model for Violent Crime
Shows the difference between actual and predicted violent crime rates by state, highlighting model accuracy.
![Image](https://github.com/user-attachments/assets/9b2315bd-1573-446e-a343-935e9b76544f)

## Key Findings

### Hypothesis 1: Access to Services → Drug Use

- A linear regression between Facilities_per_100k and DrugUse% was conducted.
- The regression line showed a weak negative slope, suggesting that greater access may reduce drug use.
- However, the R² score was low, indicating that other factors are likely influential.

### Hypothesis 2: AMI% → Drug Use / Crime

- Two separate regressions:
  - AMI% vs Drug Use%: A weak to moderate positive trend, supporting the hypothesis.
  - AMI% vs Violent Crime: Slight positive slope but again with a low R².
- Suggests that while mental illness correlates with both outcomes, the relationship is not strong enough alone to explain the variation.

### Hypothesis 3: SMI% + Drug Use% → Violent Crime

- A multiple linear regression using SMI% and Drug Use% as predictors was conducted.
- Drug use emerged as a stronger predictor than SMI%.
- The model performed moderately well (R² around 0.4), indicating partial explanatory power.
  
## Limitations

- Data is aggregated at the state level, potentially hiding regional differences
- No direct measurement of untreated mental illness - proxy indicators were used
- Correlation does not imply causation
- Facility count does not reflect service quality or treatment effectiveness

## Conclusion

This study supports the idea that mental illness and substance use are meaningfully linked to crime, but not in isolation.

- Mental illness, particularly when untreated, is associated with increased drug use.
- Drug use is more strongly associated with violent crime than mental illness alone.
- States with better access to mental health services may see slightly lower substance use, but access alone is not a sufficient predictor.
- Linear regression models helped reveal these patterns, though their explanatory power was moderate at best-highlighting the need for more granular or multi-factor data (e.g., socioeconomic, education, policy).
