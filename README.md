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

The analysis began with exploratory data analysis (EDA), followed by hypothesis testing. To quantify relationships between variables, Linear Regression (a fundamental machine learning technique suitable for small, well-structured datasets) was applied. Additionally, Random Forest Regression (a more flexible, ensemble-based machine learning method) was used to model complex, non-linear relationships for each hypothesis. This provided an alternate view of predictive patterns and was useful for comparing model accuracy.

For each hypothesis, R² (coefficient of determination) values were used to evaluate explanatory power.
  
## Visualizations
  
### Correlation Heatmap
Shows the relationship between mental illness, drug use, service access and crime.
![Image](https://github.com/user-attachments/assets/f0a33cf7-2a74-414f-8fdf-3010a11d4cfa)
  
### Drug Use vs. Mental Illness Rate (AMI%)
Highlights the positive association between mental illness rates and drug use across states.
![Image](https://github.com/user-attachments/assets/b3b5e0d5-e09c-43b6-8c9c-781feef20438)
  
### Drug Use vs. Violent Crime Rate
Reveals a mild positive correlation between drug use and violent crime rates across states.
![Image](https://github.com/user-attachments/assets/1a4e3ac3-74bb-4939-9076-e8805f3fc63c)
  
### Facilities per 100k by State
Compares the availability of mental health facilities across states on a per capita basis.
![Image](https://github.com/user-attachments/assets/3ff9af98-c5c4-420e-8634-ab357add11e3)
  
### Facilities vs. Drug Use
Examines the relationship between mental health service access and drug use, showing a weak negative trend.
![Image](https://github.com/user-attachments/assets/04c015fe-87e1-4873-9223-fdf330b90e91)
  
### RF Prediction of Drug Use from Facility Access
Uses service access to estimate drug use levels, predictions generally align with actual data.
![Image](https://github.com/user-attachments/assets/52bc8135-04dc-403b-9447-8a134a9549e1)

### AMI% vs Drug Use%
Displays a positive linear trend between any mental illness and drug use, showing a potential link between the two.
![Image](https://github.com/user-attachments/assets/697d7474-526e-4fb8-aad3-671d9d544204)
  
### AMI% vs Violent Crime Rate
Shows a mild positive trend, suggesting that higher mental illness rates may slightly relate to increased violent crime.
![Image](https://github.com/user-attachments/assets/54a3db99-d6c4-417b-9422-44b5d4303435)
  
### RF Prediction of Drug Use from AMI%
Estimates state-level drug use based on mental illness rates.
![Image](https://github.com/user-attachments/assets/67c1f166-48b2-42ca-8018-9a7ae1d0a645)
  
### SMI% vs Violent Crime Rate
Shows a weak but positive trend between serious mental illness rates and violent crime.
![Image](https://github.com/user-attachments/assets/64be224c-74e1-4423-be87-8058e80d1793)

### RF Prediction of Violent Crime from SMI% and Drug Use%
Predicts violent crime based on serious mental illness and drug use rates.
![Image](https://github.com/user-attachments/assets/5b1a8fb5-dc2e-4502-88c8-4e6f33fc8df7)
  
### Prediction Residuals: RF Model for Violent Crime
Shows the difference between actual and predicted violent crime rates by state, highlighting accuracy.
![Image](https://github.com/user-attachments/assets/34417578-8cf1-41e3-9298-1012f1948de0)

## Key Findings

### Hypothesis 1: Access to Services → Drug Use

- A linear regression between Facilities_per_100k and DrugUse% was conducted.
- The regression line showed a weak negative slope, suggesting that greater access may reduce drug use.
- However, the R² score was low, indicating that other factors are likely influential.
- A Random Forest Regression model was also applied to predict drug use based on facility access; predictions broadly aligned with actual values, but with limited accuracy

### Hypothesis 2: AMI% → Drug Use / Crime

- Two separate regressions:
  - AMI% vs Drug Use%: A weak to moderate positive trend, supporting the hypothesis.
  - AMI% vs Violent Crime: Slight positive slope but again with a low R².
- A Random Forest Regression was used to predict drug use based on AMI%, providing more flexible, state-level predictions.
- Suggests that while mental illness correlates with both outcomes, the relationship is not strong enough alone to explain the variation.

### Hypothesis 3: SMI% + Drug Use% → Violent Crime

- A multiple linear regression using SMI% and Drug Use% as predictors was conducted.
- Drug use emerged as a stronger predictor than SMI%.
- The model performed moderately well (R² around 0.4), indicating partial explanatory power.
- A Random Forest model was also used to predict violent crime from both variables. Residual analysis revealed model strengths and weaknesses across states.
  
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
To come to these conclusions both Linear Regression and Random Forest Regression models were used. While linear models revealed general trends; Random Forest models provided a more nuanced, non-linear understanding and allowed for comparisons between actual and predicted outcomes.

These findings highlight the complexity of social and behavioral health issues and suggest the need for more granular, multi-factor data (e.g. socioeconomic status, education, local policy) to build more accurate predictive models in the future.
