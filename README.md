# The Path to Crime

## Project Overview

This project examines the relationship between the use of drugs and crime rates in the context of the role played by untreated mental illnesses in the use of drugs.

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
- Maine has high drug use but low crime — a notable outlier

### Service Access vs. Drug Use
- Unexpected result: states with more mental health facilities do not always have lower drug use
- Possible explanation: services are often expanded reactively in response to rising drug problems

### Service Access vs. Crime
- Slight negative trend between facility access and violent crime
- States with higher service access tend to show lower crime, though not universally (e.g. Alaska is an exception)

## Hypothesis Testing

### H1: Service Access → Drug Use
- **Test**: Two-sample t-test between low and high service access states
- **Result**: p-value ≈ 0.06 — not statistically significant
- **Interpretation**: Mixed results; some low-access states show lower drug use

### H2: Untreated Mental Illness → Drug Use / Crime
- **AMI% vs. Drug Use**: r ≈ 0.29  
- **AMI% vs. Crime**: r ≈ 0.24  
- Suggests correlation, but not strong enough for statistical significance  
- Example states with large treatment gaps: Oregon, Nevada

### H3: Severe Mental Illness → Crime
- **SMI% vs. Crime**: r ≈ 0.21  
- **Regression model**: Crime ~ SMI + Drug Use  
  - Drug use is the stronger predictor  
- **Conclusion**: Weak direct link; the effect is likely mediated through substance use

## Visualizations

### Correlation Heatmap
Shows the relationship between mental illness, drug use, service access, and crime.
![Correlation Heatmap](https://private-user-images.githubusercontent.com/182896253/437596287-b7a49625-afac-4dad-8e4f-e47b0700878b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI2MjAsIm5iZiI6MTc0NTYxMjMyMCwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2Mjg3LWI3YTQ5NjI1LWFmYWMtNGRhZC04ZTRmLWU0N2IwNzAwODc4Yi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDE4NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lYTgxM2QyZDM1Mjk3NGM3YjVhZDI4ZWU5MGUyZDA2NzYyMDhjNjAxZjFjYjI1OTc3ODQ0MDYxZjAyOTI1ZWE0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Llse84dK28yiWm6VZowhBmipsMks98kMrNMwzyAP7Og)
## Key Findings

- Drug use and mental illness show a moderate correlation
- Drug use has a stronger statistical relationship with crime than mental illness alone
- An increase in facilities does not guarantee improvement — local context matters
- States with poor access to mental healthcare often face higher public health burdens

## Limitations

- Data is aggregated at the state level, potentially hiding regional differences
- No direct measurement of untreated mental illness — proxy indicators were used
- Correlation does not imply causation
- Facility count does not reflect service quality or treatment effectiveness

## Future Work

- Include additional socioeconomic variables (income, education, housing access)
- Apply machine learning models to predict high-risk regions (planned for May 23 milestone)
- Assess the impact of mental health policies and treatment program availability on long-term crime trends
