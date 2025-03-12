Statistical Analysis Plan
================
Hyejung Lee <hyejung.lee@utah.edu>
Wed Mar 12, 2025 01:20:43 PM

- [Hypothesis](#hypothesis)
- [Data](#data)

  

# Hypothesis

Advanced non-small cell lung cancer (aNSCLC) patients’ recommended
course of treatments are identified in National Comprehensive Cancer
Network (NCCN) guideline. The guideline suggests each patient to perform
biopsy to identify presence of targetable mutations of certain
biomarkers and PDL1 expression to make a informed decision on 1L therapy
choice. This recommendation is made because targeted therapy is better
for patient’s survival than a standard, generic therapy such as
chemotherapy or immunotherapy.

However, the standard guideline may not always be followed due to
reasons such as clinician’s expert knowledge and ethics. For example,
patients with heavy smoking habits mostly develop NSCLC by smoking
without any targetable mutation. In this case, chemotherapy alone can be
used or if PDL1 expression level is available, any combination of
chemotherapy and immunotherapy may be applied. The choice to proceeding
to 1L without checking for targetable mutation or PDL1 expression arises
due to the fact that a complete panel of tests for biomarkers and PDL1
expression takes 2 to 3 weeks on average. It may take longer if the
biopsy samples were not good and the test results are indeterminate,
requiring another round of biopsy and waiting for the result. This
period of waiting without doing any treatment may be detrimental to
patient’s health and thus becomes an ethical issue. Therefore, the
ultimate choice of whether waiting for the test result or not relies
heavily on the clinician’s decision.

Just like the example of heavy smokers, there are some patient
characteristics that are highly indicative of patient’s likelihood of
targetable mutation status. However, there has not yet been a
quantitative evaluation of effect of proceeding to 1L therapy prior to
knowing targetable mutation status in patients. In this study, we
evaluate causal effect of proceeding right 1L therapy in all aNSCLC
patients, as well as in some subgroups that have previously been
identified as associated with the mutation status.

  

# Data

This study used the nationwide Flatiron Health electronic health record
(EHR)-derived de-identified database. The Flatiron Health database is a
longitudinal database, comprising de-identified patient-level structured
and unstructured data, curated via technology-enabled
abstraction<sup>1,2</sup>. The de-identified data originated from 280
cancer clinics (~800 sites of care) . The study included 85,572 unique
patients diagnosed with aNSCLC (ICD-9 162.x or ICD-10 C34x or C39.9)
from 01 January 2011, to 30 December 2022. Patients with a BirthYear of
1937 or earlier may have an adjusted BirthYear in Flatiron datasets due
to patient de-identification requirements. For more information, please
refer to their webpage<sup>3</sup>.

Patient attrition diagram is shown in . It shows all exclusion criteria.
We excluded all patients who start either the 1L therapy or valid test
before time zero, which is advanced diagnosis date. We will explain what
valid test means in the next section.

<div class="figure" style="text-align: center">

<embed src="patient_attrition_diagram.pdf" title="exclusion diagram" width="25%" type="application/pdf" />
<p class="caption">
exclusion diagram
</p>

</div>

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
