Statistical Analysis Plan
================
Hyejung Lee <hyejung.lee@utah.edu>
Thu Mar 20, 2025 02:02:59 PM

- [Hypothesis](#hypothesis)
- [Objectives](#objectives)
- [Study Design and Population](#study-design-and-population)
  - [Study Design](#study-design)
  - [Study Population](#study-population)
- [Data Strucutre](#data-strucutre)
- [Cohort](#cohort)
  - [Directed acyclic graph (DAG)](#directed-acyclic-graph-dag)
- [Appendices](#appendices)
  - [Appendix A: List of baseline covariates](#sec-appA)
- [Tables](#tables)
  - [Table 1](#table-1)
- [Key variables](#key-variables)
  - [Valid targetable mutation test or PDL1
    test](#valid-targetable-mutation-test-or-pdl1-test)
  - [Cohort](#cohort-1)

  

# Hypothesis

Advanced non-small cell lung cancer (aNSCLC) patients’ recommended
course of treatments are identified in National Comprehensive Cancer
Network (NCCN) guideline. The guideline suggests each patient to perform
biopsy to identify presence of targetable mutations of certain
biomarkers and PDL1 expression to make a informed decision on 1L therapy
choice. This recommendation is made because targeted therapy is better
for patient’s survival than a standard, genetic therapy such as
chemotherapy or immunotherapy. Usually, at least 1 positive mutation or
2 negative mutation status among all targetable biomarkers should be
obtained to make informed decision about targetable therapy. Thus having
at least 1 positive mutation or 2 negative mutation status will be
referred to as *useful* mutation test result from here onward.
Similarly, obtaining PDL1 expression level (from 0-100%) level, as
opposed to result such as missing expression level or indeterminate
result, will be referred to as *useful* PDL1 test result.

The standard NCCN guideline, however, may not always be followed due to
reasons such as clinician’s expert knowledge and ethics. For example,
heavy smokers who develop lung cancer is most likely due to smoking
rather than genetic mutation. Patients who fall into this category then
may receive chemotherapy right away, instead of performing and waiting
for genetic or PDL1 test results. One reason for not waiting until the
useful test comes out is that a complete panel of test results (combined
mutation and PDL1 expression tests) usually takes about 2-3 weeks to
become available. It may take longer if the biopsy samples were not good
and the test results are indeterminate, requiring another round of
biopsy and waiting for the result. This period of waiting without doing
any treatment may be detrimental to patient’s health and thus becomes an
ethical issue. Therefore, the ultimate choice of whether waiting for the
test result or not relies heavily on the clinician’s decision.

Just like the example of heavy smokers, there are some patient
characteristics that are highly indicative of patient’s likelihood of
targetable mutation status. However, there has not yet been a
quantitative evaluation of effect of proceeding to 1L therapy prior to
knowing targetable mutation status in patients. In this study, we
evaluate causal effect of proceeding right 1L therapy in all aNSCLC
patients, as well as in some subgroups that have previously been
identified as associated with the mutation status.

  

# Objectives

**Primary Objective**: Using marginal structural model, we will develop
and evaluate the effect of proceeding to 1L therapy prior to obtaining
useful targetable mutation status

- Limit the number of weeks.
- For entire observation.

**Secondary Objective**: Test impact of proceeding to 1L before useful
tests become available in the following subgroups: male, female, have
history of smoking, do not have history of smoking, baseline Eastern
Cooperative Oncology Group (ECOG) score 0-2, baseline ECOG score 3-4,
baseline albumin \< 35g/L, baseline albumin \>= 35 g/L, and Asian.

- These are the subgroups identified by Wally as having either higher or
  lower probability of having targetable mutation, and thus would more
  or less likely wait for the useful test results to become available
  prior to initiating 1L therapy.

  

# Study Design and Population

## Study Design

Retrospective Cohort Study

## Study Population

**Data**: A nationwide Flatiron Health electronic health record
(EHR)-derived de-identified database. The Flatiron Health database is a
longitudinal database, comprising de-identified patient-level structured
and unstructured data, curated via technology-enabled
abstraction<sup>1,2</sup>. The de-identified data originated from 280
cancer clinics (~800 sites of care). Patients with a BirthYear of 1937
or earlier may have an adjusted BirthYear in Flatiron datasets due to
patient de-identification requirements. For more information, please
refer to their webpage<sup>3</sup>.

**Inclusion criteria**: People who got diagnosed with aNSLC (ICD-9 162.x
or ICD-10 C34x or C39.9) from 01 January 2011, to 30 December 2022 from
Flatiron Health network.

1.  Index date is date of aNSCLC diagnosis.

**Exclusion criteria**:

1.  Initiate who receive first-line (1L) therapy on or after the index
    date.
2.  Receive any useful test result (either PDL1 or targetable mutation)
    prior to the index date
3.  Missing death or censoring date

Patient attrition diagram is shown below. It shows all exclusion
criteria. We excluded all patients who don’t have valid survival end
time and who start either the 1L therapy or valid test before advanced
diagnosis date. We will explain what valid test means in the next
section.

<div class="figure">

<img src="./image/patient_attrition_diagram.png" alt="Figure XX: Patient attrition diagram" width="70%" />
<p class="caption">
Figure XX: Patient attrition diagram
</p>

</div>

# Data Strucutre

There are 9 data sets of wide and long formats. Data sets containing
repeated measurements such as visits, PDL1 or targetable mutation test,
or lab values will be long format. The unit of observation differs by
the dataset.

1.  Create a single date variable where useful PDL1 test results are
    observed in each patient.
2.  Create a single date variable where useful targetable mutation test
    results are observed in each patient.
3.  For each consecutive week after the index date, create a binary
    indicator variable indicating who initiated 1L therapy before
    receiving any useful test is out. (Cohort identification)
4.  Create baseline covariates as listed in @ref(sec-appA)

<!-- -->

1.  report the percent missing of each variable overall by exposure
    group as in @ref(tab:baseline-missing-mock)

<!-- -->

5.  For each consecutive week after the index date, a long dataset is
    created for each patient’s weekly time-varying follow-up variables
    listed in Appendix B. There will be a variable named $k$ which shows
    number of weeks since index date. When $k=0$, it refers to baseline.
    Suppose for an example, albumin measurement at $k=1$ represent
    measurements taken between $(0,7]$ days, and at $k=2$ will represent
    measurements taken between $(7,14]$ days.  
6.  Impute censoring date using visit and oral medication record

  

| Patient ID |   k | Gender | SmokingStatus      |  Albumin | Platelet | cohort |
|:-----------|----:|:-------|:-------------------|---------:|---------:|-------:|
| A          |   0 | M      | History of smoking | 37.20139 |      214 |      0 |
| A          |   1 | M      | History of smoking | 17.87623 |      210 |      0 |
| A          |   2 | M      | History of smoking | 37.51583 |      198 |      0 |
| B          |   0 | M      | History of smoking | 29.80779 |      236 |      0 |
| B          |   1 | M      | History of smoking | 41.01908 |      262 |      0 |
| B          |   2 | M      | History of smoking | 52.88518 |      257 |      0 |
| B          |   3 | M      | History of smoking | 35.94656 |      262 |      1 |
| B          |   4 | M      | History of smoking | 40.00766 |      302 |      1 |
| B          |   5 | M      | History of smoking | 44.05353 |      283 |      1 |

Table 1. Example dataset: An expected sample of the dataset for the
baseline and follow-up variables for two patients. Gender and smoking
status are baseline covariates that do not change over time. Albumin and
Platelet are the tiem-dependent covariates that are measured each week
(k). Cohort is the exposure variables that can change over time.

  

# Cohort

## Directed acyclic graph (DAG)

<div class="figure">

<img src="./image/DAG.jpg" alt="Figure XX: Directed acyclic graph. Y refers to survival outcome, A's refer to time-dependent cohort status, L's refer to time-dependent measured confounders, and U's refer to time-dependent unmeasured confounders. Index 0 is the baseline measruement. Thus, L0 contains variable such as gender and race/ethnicity. L1 then has a subset of variables of L0, where only time-varying variables are contained. The time index (k) goes from 1 through K_i, where i refers to a patient. Each patient has different number of weeks of follow-up until censored or dead." width="70%" />
<p class="caption">
Figure XX: Directed acyclic graph. Y refers to survival outcome, A’s
refer to time-dependent cohort status, L’s refer to time-dependent
measured confounders, and U’s refer to time-dependent unmeasured
confounders. Index 0 is the baseline measruement. Thus, L0 contains
variable such as gender and race/ethnicity. L1 then has a subset of
variables of L0, where only time-varying variables are contained. The
time index (k) goes from 1 through K_i, where i refers to a patient.
Each patient has different number of weeks of follow-up until censored
or dead.
</p>

</div>

@ref{fig-DAG}

  

# Appendices

## Appendix A: List of baseline covariates

| variable | Definition |
|:---|:---|
| Gender | Male or Female (from Demographics.csv file) |
| Age | Age of patient in years calculated on the index date (from Enhanced_AdvancedNSCLC.csv file) based on their year of birth (from Demographics.csv file). Approximation due to incomplete data(missing month and day) for de-identification purposes. |
| Race/Ethnicity | A single variable derived by pasting Race (Asian, Black or African American, Hispanic or Latino, White, Other Race) and Ethnicity (Not Hispanic or Latino, Hispanic or Latino) variables. |
| Smoking Status | Smoking status of patient (History, no history, unknown) (from Enhanced_AdvancedNSCLC.csv file). |
| Histology | Squamous cell carcinoma, Non-squamous cell carcinoma, NSCLC histology NOS (from Enhanced_AdvancedNSCLC.csv file) |
| BMI | Body mass index (kg\_\_m^2) (from Vitals.csv file) |
| ECOG score | Eastern Cooperative Oncology Group score, ranging from 0 to 4. (from ECOG.csv file) |
| Complete metabolic panel (CMP) | Lab measurement of following analytes: Albumin, Alkaline, ALT, Bilirubin, Calcium, Chloride, Creatinine, eGFR, Potassium, Protein, Sodium. Each of these variables are to be defined below. (from Lab.csv file) |
| Albumin | albumin \[mass\_\_volume\] in serum or plasma measrued in g\_\_L |
| Alkaline | alkaline phosphatase \[enzymatic activity\_\_volume\] in serum or plasma measrued in U\_\_L |
| ALT | alanine aminotransferase \[enzymatic activity\_\_volume\] in serum or plasma measrued in U\_\_L |
| AST | aspartate aminotransferase \[enzymatic activity\_\_volume\] in serum or plasma measrued in U\_\_L |
| Bilirubin | bilirubin.total \[mass\_\_volume\] in serum or plasma measrued in mg\_\_dL |
| Calcium | calcium \[mass\_\_volume\] in serum or plasma measrued in mg\_\_dL |
| Carbon dioxide | carbon dioxide, total \[moles\_\_volume\] in serum or plasma measrued in mmol\_\_L |
| Chloride | chloride \[moles\_\_volume\] in serum or plasma measrued in mmol\_\_L |
| Creatinine | creatinine \[mass\_\_volume\] in serum or plasma measrued in mg\_\_dL |
| Glucose | glucose \[mass\_\_volume\] in serum or plasma measrued in mg\_\_dL |
| Potassium | potassium \[moles\_\_volume\] in serum or plasma measrued in mmol\_\_L |
| Protein | protein \[mass\_\_volume\] in serum or plasma measrued in g\_\_L |
| Sodium | sodium \[moles\_\_volume\] in serum or plasma measrued in mmol\_\_L |
| eGFR_mdrd | glomerular filtration rate predicted \[volume rate\_\_area\] in serum, plasma or blood by creatinine-based formula (mdrd), measrued in ml\_\_min\_\_1.73m\*2. Some observations specificially state that the values are precited among non-blacks, blacks, or females mutually exclusively. |
| eGFR_ckd_epi | glomerular filtration rate predicted \[volume rate\_\_area\] in serum, plasma or blood, measrued in ml\_\_min\_\_1.73m\*2. Some observations specify whether the test as creatinine-based formula (ckd-epi), creatinine-based formula (ckd-epi 2021), or cystatin c-based formula. Also, some observations people specificially states whether the values are precited among non-blacks or blacks, mutually exclusively. |
| Categorical CMP | Categorical version of the above…. Should we do this? I won’t for now. |
| Complete Blood Panel (CBP) | lab measurement of following analytes: RBC, WBC, HCT, HGB, Platelet, Lymphocyte \#, Neutrophil \#. Each of these variables are to be defined below. (from Lab.csv file) |
| HCT | hematocrit \[volume fraction\] of blood measrued in % |
| HGB | hemoglobin \[mass\_\_volume\] in blood measrued in g\_\_dL |
| Lymphocyte \# | lymphocytes \[#\_\_volume\] in blood measrued in 10\*9\_\_L |
| Neutrophil \# | neutrophils \[#\_\_volume\] in blood measrued in 10\*9\_\_L |
| Platelet | platelets \[#\_\_volume\] in blood measrued in 10\*9\_\_L |
| RBC | erythrocytes \[#\_\_volume\] in blood measrued in 10\*12\_\_L |
| WBC | leukocytes \[#\_\_volume\] in blood measrued in 10\*9\_\_L |
| Categorical CBP | Categorical version of the above…. Should we do this? I won’t for now. |

- Gender: Demographics.csv/Gender
- Age at diagnosis:
  - Demographics.csv/BirthYear
  - Enhanced_AdvancedNSCLC.csv/AdvancedDiagnosisDate
  - difference in the two above dates
- Race/Ethnicity:
  - Demographics.csv/Race
  - Demographics.csv/Ethnicity
  - Append the two variables
- Smoking status: Enhanced_AdvancedNSCLC.csv/SmokingStatus
- Histology: Enhanced_AdvancedNSCLC.csv/Histology
- BMI:
  - Vitals.csv/Test : choose the entries equal to “body weight” and
    “body height”. Body weight is in kg, and the body height is in cm.
    generate BMI (kg/m^2) from these two entries.
- ECOG score: ECOG.csv/EcogValue
- Complete metabolic panel(CMP) (Albumin, Alkaline, ALT, Bilirubin,
  Calcium, Carbon dioxide, Chloride, Creatinine, eGFR, Potassium,
  Protein, Sodium, HCT, HGB, Lymphocyte \#, Neutrophil \#) :
  - Lab.csv/TestResultCleaned
  - Lab.csv/TestBaseName : filter to the CMP
- Categorical CMP: Take CMP, and discretize into Above, Average, Below
  using website
  (<https://www.ucsfhealth.org/medical-tests/comprehensive-metabolic-panel>)
  - <https://www.ncbi.nlm.nih.gov/books/NBK204/#>:~:text=The%20normal%20serum%20protein%20level,according%20to%20the%20individual%20laboratory.
- Complete blood count(CBC) (Platelet, RBC, WBC) :
  - Lab.csv/TestResultCleaned
  - Lab.csv/TestBaseName : filter to the CBC
- Categorical CBC: Take CBC, and discretize into Above, Average, Below
  using website
  - <https://www.ncbi.nlm.nih.gov/books/NBK2263/table/ch1.T1/>

  

# Tables

## Table 1

| variable                       | Overall (n=) | Wait (n=) | Do not wait (n=) |
|:-------------------------------|:-------------|:----------|:-----------------|
| Gender                         |              |           |                  |
| Age                            |              |           |                  |
| Race/Ethnicity                 |              |           |                  |
| Smoking Status                 |              |           |                  |
| Histology                      |              |           |                  |
| BMI                            |              |           |                  |
| ECOG score                     |              |           |                  |
| Complete metabolic panel (CMP) |              |           |                  |
| Albumin                        |              |           |                  |
| Alkaline                       |              |           |                  |
| ALT                            |              |           |                  |
| AST                            |              |           |                  |
| Bilirubin                      |              |           |                  |
| Calcium                        |              |           |                  |
| Carbon dioxide                 |              |           |                  |
| Chloride                       |              |           |                  |
| Creatinine                     |              |           |                  |
| Glucose                        |              |           |                  |
| Potassium                      |              |           |                  |
| Protein                        |              |           |                  |
| Sodium                         |              |           |                  |
| eGFR_mdrd                      |              |           |                  |
| eGFR_ckd_epi                   |              |           |                  |
| Categorical CMP                |              |           |                  |
| Complete Blood Panel (CBP)     |              |           |                  |
| HCT                            |              |           |                  |
| HGB                            |              |           |                  |
| Lymphocyte \#                  |              |           |                  |
| Neutrophil \#                  |              |           |                  |
| Platelet                       |              |           |                  |
| RBC                            |              |           |                  |
| WBC                            |              |           |                  |
| Categorical CBP                |              |           |                  |

Table1: Mock table demonstrating format of reporting proportion missing.

# Key variables

- time zero: Enhanced_AdvancedNSCLC.csv/AdvancedDiagnosisDate
- death date: Enhanced_Mortality_V2.csv/DateOfDeath
- censoring date:
  - Visit.csv/VisitDate
  - Enhanced_AdvNSCLC_Orals.csv/EndDate
  - maximum of the two columns
- 1L therapy date:
  - LineOfTherapy.csv/StartDate
  - LineOfTherapy.csv/LineName : must be equal to 1
  - LineOfTherapy.csv/IsMaintenanceTherapy : must be FALSE
- useful PDL1 test result:
  - Enhanced_AdvNSCLCBiomarkers.csv/PercentStaining
  - Enhanced_AdvNSCLCBiomarkers.csv/ResultDate : must have result date
  - Enhanced_AdvNSCLCBiomarkers.csv/PercentStaining : should not be
    empty
- useful mutation test result:
  - Enhanced_AdvNSCLCBiomarkers.csv/BiomarkerStatus
  - Enhanced_AdvNSCLCBiomarkers.csv/ResultDate : must have result date
  - Enhanced_AdvNSCLCBiomarkers.csv/BiomarkerStatus : must have one of
    the following entries to be a positive mutation result: “Mutation
    positive”, “PD-L1 positive”, “Rearrangement present”, “Rearrangement
    positive”, “Amplification positive”, “Protein expression positive”,
    “PD-L1 positive”,
  - Enhanced_AdvNSCLCBiomarkers.csv/BiomarkerStatus : must have one of
    the following entries to be a negative mutation result: “Mutation
    negative”, “Negative”, “PD-L1 negative/not detected”, “Rearrangement
    not present”
- Gender: Demographics.csv/Gender
- Age at diagnosis:
  - Demographics.csv/BirthYear
  - Enhanced_AdvancedNSCLC.csv/AdvancedDiagnosisDate
  - difference in the two above dates
- Race/Ethnicity:
  - Demographics.csv/Race
  - Demographics.csv/Ethnicity
  - Append the two variables
- Smoking status: Enhanced_AdvancedNSCLC.csv/SmokingStatus
- Histology: Enhanced_AdvancedNSCLC.csv/Histology
- BMI:
  - Vitals.csv/Test : choose the entries equal to “body weight” and
    “body height”. Body weight is in kg, and the body height is in cm.
    generate BMI (kg/m^2) from these two entries.
- ECOG score: ECOG.csv/EcogValue
- Complete metabolic panel(CMP) (Albumin, Alkaline, ALT, Bilirubin,
  Calcium, Carbon dioxide, Chloride, Creatinine, eGFR, Potassium,
  Protein, Sodium, HCT, HGB, Lymphocyte \#, Neutrophil \#) :
  - Lab.csv/TestResultCleaned
  - Lab.csv/TestBaseName : filter to the CMP
- Categorical CMP: Take CMP, and discretize into Above, Average, Below
  using website
  (<https://www.ucsfhealth.org/medical-tests/comprehensive-metabolic-panel>)
  - <https://www.ncbi.nlm.nih.gov/books/NBK204/#>:~:text=The%20normal%20serum%20protein%20level,according%20to%20the%20individual%20laboratory.
- Complete blood count(CBC) (Platelet, RBC, WBC) :
  - Lab.csv/TestResultCleaned
  - Lab.csv/TestBaseName : filter to the CBC
- Categorical CBC: Take CBC, and discretize into Above, Average, Below
  using website
  - <https://www.ncbi.nlm.nih.gov/books/NBK2263/table/ch1.T1/>

Albumin: 3.4 to 5.4 g/dL (34 to 54 g/L) Alkaline phosphatase: 20 to 130
U/L ALT (alanine aminotransferase): 4 to 36 U/L AST (aspartate
aminotransferase): 8 to 33 U/L BUN (blood urea nitrogen): 6 to 20 mg/dL
(2.14 to 7.14 mmol/L) Calcium: 8.5 to 10.2 mg/dL (2.13 to 2.55 mmol/L)
Chloride: 96 to 106 mEq/L (96 to 106 mmol/L) CO2 (carbon dioxide): 23 to
29 mEq/L (23 to 29 mmol/L) Creatinine: 0.6 to 1.3 mg/dL (53 to 114.9
µmol/L) Glucose: 70 to 100 mg/dL (3.9 to 5.6 mmol/L) Potassium: 3.7 to
5.2 mEq/L (3.70 to 5.20 mmol/L) Sodium: 135 to 145 mEq/L (135 to 145
mmol/L) Total bilirubin: 0.1 to 1.2 mg/dL (2 to 21 µmol/L) Total
protein: 6.0 to 8.3 g/dL (60 to 83 g/L)

  

## Valid targetable mutation test or PDL1 test

The point of conducting this analysis is whether proceeding to provide
1L therapy before knowledge of PDL1 expression level or targetable
mutation status would impact the survival. Thus, valid PDL1 test refers
to test results with non-missing PDL1 expression level in the dataset.
<span style="color:red;">PDL1 expression levels indicate patient’s
susceptibility to immumotherapy, with higher percentage indicating
immunotherapy will work well on the patient.</span>

On the other hand for the targetable mutation, we have 8 different
biomarkers for which we can test for mutation. They are: ALK, EGFR,
BRAF, KRAS, MET, RET, ROS1, and NTRK. Clinicians typically find it
useful to have at least 1 positive mutation or 2 negative mutations to
make informed 1L therapy decision. Thus, any patient who have either 1
positive mutation or 2 negative mutation results are considered to have
valid targetable mutation result. We identified a biomarker to be
mutation positive if it had any one of the following entries in
“BiomarkerStatus” column. :

- Mutation positive

- PD-L1 positive

- Rearrangement present

- Rearrangement positive

- Amplification positive

- Protein expression positive

- PD-L1 positive

Similarly, we identified a biomarker to be mutation negative if it had
any one of the following entries in the same column. :

- Mutation negative

- Negative

- PD-L1 negative/not detected

- Rearrangement not present

  

## Cohort

In our analysis, we assess impact of proceeding to 1L therapy without
either valid PDL result or targetable mutation result. Here, we identify
two cohorts. First cohort is those who proceeded to 1L therapy before
either valid PDL1 or targetable mutation result were observed. Second
cohort is those who received 1L therapy after observing either valid
PDL1 or targetable mutation result. Therefore, cohort is a function of
time from time zero until either valid PDL1 or targetable mutation
result date and 1L therapy start date.

That is, if a patient has a record of 1L before either valid PDL1 or
targetable mutation result, then the patient is identified as a

<div id="refs" class="references csl-bib-body" entry-spacing="0"
line-spacing="2">

<div id="ref-ma2020comparison" class="csl-entry">

<span class="csl-left-margin">1.
</span><span class="csl-right-inline">Ma, X., Long, L., Moon, S.,
Adamson, B. J. & Baxi, S. S. Comparison of population characteristics in
real-world clinical oncology databases in the US: Flatiron health, SEER,
and NPCR. *Medrxiv* 2020–03 (2020).</span>

</div>

<div id="ref-birnbaum2020model" class="csl-entry">

<span class="csl-left-margin">2.
</span><span class="csl-right-inline">Birnbaum, B. *et al.*
Model-assisted cohort selection with bias analysis for generating
large-scale cohorts from the EHR for oncology research. *arXiv preprint
arXiv:2001.09765* (2020).</span>

</div>

<div id="ref-zhang2025" class="csl-entry">

<span class="csl-left-margin">3.
</span><span class="csl-right-inline">Zhang, S. BirthYear overview and
data considerations.
<https://flatironlifesciences.zendesk.com/hc/en-us/articles/11186051513229-BirthYear-Overview-and-Data-Considerations>.</span>

</div>

</div>
