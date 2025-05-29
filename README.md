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
  
![Correlation Heatmap](https://private-user-images.githubusercontent.com/182896253/437596287-b7a49625-afac-4dad-8e4f-e47b0700878b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDg1Mjk3ODYsIm5iZiI6MTc0ODUyOTQ4NiwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2Mjg3LWI3YTQ5NjI1LWFmYWMtNGRhZC04ZTRmLWU0N2IwNzAwODc4Yi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNTI5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDUyOVQxNDM4MDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hMjA5MmZhYmQxMGZiYjE5ZGEwN2UxNDRkNTc3ZGQ0YTAwMWJmMzNjNjgwNWJlMGYwYjI3M2I1MDBhMjJmY2RjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.N6JGPEdgpfRTwy4g7DmN481QtYBcuPQdfYLt27Rsy6o)

### Drug Use vs. Mental Illness Rate (AMI%)
Higher AMI rates tend to align with increased drug use.
  
![Drug Use vs. Mental Illness Rate (AMI%)](https://private-user-images.githubusercontent.com/182896253/437596472-fc9a6549-04c4-46d5-ae35-728da71b2ae5.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI2MjAsIm5iZiI6MTc0NTYxMjMyMCwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NDcyLWZjOWE2NTQ5LTA0YzQtNDZkNS1hZTM1LTcyOGRhNzFiMmFlNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDE4NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04ZGM5Nzk4NjBiZDg3MWY2M2VjYjQxMTdhMDE1MjA1MmFhNjY4NGM1YjkxMWJjZDAzMjhlMjdjOWQ1YjI4M2U4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.bKqvvqxOvy6hkLkXD32bneRKXKyjMju9h-6KWH5FdjA)

### Drug Use vs. Violent Crime Rate
Some states with high drug use also show higher violent crime rates.
  
![Drug Use vs. Violent Crime Rate](https://private-user-images.githubusercontent.com/182896253/437596500-dbd3bac2-2204-458b-8525-c1904a531495.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI2MjAsIm5iZiI6MTc0NTYxMjMyMCwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NTAwLWRiZDNiYWMyLTIyMDQtNDU4Yi04NTI1LWMxOTA0YTUzMTQ5NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDE4NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03Zjk1NTk5YWVhOTI1ZTk0OTQ0YjQ0ZTFmYzVkYzFhNTc2Y2ExYTU4NmRmMjliMmJkODZhNWNiYmZmZjNhZjMxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Ha7cErccovV2bJ7PNqk115T-hDgr2JVUC4xY38j13dk)

### Mental Health Facilities per 100k Population
Alaska leads in mental health service access per capita.
  
![Mental Health Facilities per 100k Population](https://private-user-images.githubusercontent.com/182896253/437596524-dab269df-a360-400f-8081-a2df2d7ff938.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI2MjAsIm5iZiI6MTc0NTYxMjMyMCwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NTI0LWRhYjI2OWRmLWEzNjAtNDAwZi04MDgxLWEyZGYyZDdmZjkzOC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDE4NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jMWE1NmMzNjdkMjkzNWE4ZmJlYmNkNTliZDJiZTc5ZGY3ZmNmN2VlOGU5ZmViNTczZWE1Mzk2MmNkYjBjMjljJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.J_VhK8vTyrDOObkqxJ3uy_6MMXHDQah_Ui02Z_bN4rI)

### Average Drug Use by Service Access
Drug use appears lower in states with higher facility access.
  
![Average Drug Use by Service Access](https://private-user-images.githubusercontent.com/182896253/437596557-2768ce67-70d9-4933-886d-968faa3bf583.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI2MjAsIm5iZiI6MTc0NTYxMjMyMCwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NTU3LTI3NjhjZTY3LTcwZDktNDkzMy04ODZkLTk2OGZhYTNiZjU4My5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDE4NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mOTJiZmI4MDY2ZDkwNjgyNjU5NjU1NDZjMmU3YzQxOWI4ZTVmOWQ1ZmQ5OGM2MGY0MTUyYjkxZGZhMDg1MTQ2JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.nAU7hA0yzQV2stA0DFONY3c6ssx6_OJ7hgBC7gh2JJs)

### Drug Use Distribution by Access Level
Visualizes the spread of drug use between high and low access groups.
  
![Drug Use Distribution by Access Level](https://private-user-images.githubusercontent.com/182896253/437596589-42ff7266-199e-41cd-8d88-323ae6a4d8ac.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI4OTQsIm5iZiI6MTc0NTYxMjU5NCwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NTg5LTQyZmY3MjY2LTE5OWUtNDFjZC04ZDg4LTMyM2FlNmE0ZDhhYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDIzMTRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mMDEyNGUzODE3OTlkMzI3ODFlYTQ4Zjc2MzhlZTBlOTdhMjkzYmExN2VmOWY5YzM3ZGYxM2E3MzNmMGY2ZTg1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.wCTD9scjcrc4E3Np4po7kJRRhhlrU4sf0Dwf5wzcwAU)

### AMI% vs. Drug Use% (Regression)
Positive trend between mental illness rates and drug use.
  
![AMI% vs. Drug Use% (Regression)](https://private-user-images.githubusercontent.com/182896253/437596637-2128b492-200a-4d7b-b4ab-ccf5c0fdf58b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI5MDEsIm5iZiI6MTc0NTYxMjYwMSwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NjM3LTIxMjhiNDkyLTIwMGEtNGQ3Yi1iNGFiLWNjZjVjMGZkZjU4Yi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDIzMjFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zYTkwZDdhN2FhNWUyMjZhNWQxYjU4YjMzZjFlY2YyZjJhMGRiMmNiNDQ3NWQ4MGQ5YWZkM2I4YzgyMDM4OTU4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.40Oyr2RCh2HJyd2_5dV-4nw9eYRD7JOY9eU8k-LFWZE)

### AMI% vs. Violent Crime Rate
Slight upward trend in violent crime with higher AMI%.
  
![AMI% vs. Violent Crime Rate](https://private-user-images.githubusercontent.com/182896253/437596666-9aad402e-124a-491d-bd73-9f8087e22284.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI5MDEsIm5iZiI6MTc0NTYxMjYwMSwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NjY2LTlhYWQ0MDJlLTEyNGEtNDkxZC1iZDczLTlmODA4N2UyMjI4NC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDIzMjFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hNWI2MGI0MDMyMzA3Y2M3OTg0MWFmZjg2ZjAzMmQyNzY1ODNiYThiNjE4NmI5M2ZlOGZjZGM2N2MyMTA0NzVjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9._k0pTnwkp4NU1-CmzioI7vWnWw8NEmQU_bbFpoIb4LI)

### SMI% vs. Violent Crime Rate
SMI shows a weak positive correlation with violent crime.
  
![SMI% vs. Violent Crime Rate](https://private-user-images.githubusercontent.com/182896253/437596697-3584c491-0334-42ba-8f01-9b0f0c79534e.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI5MDEsIm5iZiI6MTc0NTYxMjYwMSwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2Njk3LTM1ODRjNDkxLTAzMzQtNDJiYS04ZjAxLTliMGYwYzc5NTM0ZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDIzMjFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03MWY5ZTQ5Y2M2NjkyMmQxY2M1MDgzZjg1MGNlNDUwNDE4MGVjZjc1ZDVhZTcwM2ZkYmI2ZjMyNDQwNmNjZTY4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Wc4BPgbVrqpWZ6zss5vVvaACKXrsTd0OSmnChozhZFA)

### Actual vs. Predicted Crime Rate (Regression)
Model using SMI and drug use predicts crime rates moderately well.
  
![Actual vs. Predicted Crime Rate (Regression)](https://private-user-images.githubusercontent.com/182896253/437596728-110326ee-5d1f-4294-a2d4-9f646e5033e4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDU2MTI5MDEsIm5iZiI6MTc0NTYxMjYwMSwicGF0aCI6Ii8xODI4OTYyNTMvNDM3NTk2NzI4LTExMDMyNmVlLTVkMWYtNDI5NC1hMmQ0LTlmNjQ2ZTUwMzNlNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQyNVQyMDIzMjFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05OWQ1NTIzNzU3ODY1YWFlYzQxZWFhZGUyY2NkNTUyZTA3ZTYyNGE0NWMwYzU3OTI0Y2JmNDM3ZDA4OGQzNWUyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.CesmKX9TG-nDlhubTSxqYMeqHpFqGNcr0Jn6omph71Y)


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
