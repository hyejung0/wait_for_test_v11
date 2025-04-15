Landmark Analysis
================
Hyejung Lee <hyejung.lee@utah.edu>
Tue Apr 15, 2025 11:07:44 AM

- [Context](#context)

# Context

2025 April 14

I had a meeting with Tom and Ben on last friday. Ben suggested that I
restrict the patients to those who have:

- survived to 4 weeks
- have received test result by 4 weeks
- Start time zero on the first day of 5th day
- have Albumin, ECOG, and weight change by 4th week

Yesterday, Tom and I chatted. We will do 2 separate analysis where

- **Primary Analysis**: Have time dependent covariate by the end of 1st
  week
- **Secondary Analysis**: Have time dependent covariate by the end of
  4th week

The purposes of this is because if we let the baseline covariate to be
observed until 4th week, then there is a problem when the test result or
1L therapy starts before the baseline covariate. Suppose the 1L therapy
started 1st week, but the 1st ever Albumin was observed after 2nd week.
Then the baseline covariate could be affected by 1L therapy. The fact
that we are letting the baseline to be anywhere between advanced
diagnosis and end of 4th week is that we are assuming all time in these
4 weeks are instantaneous and that whether the 1L therapy is received
before or after the first lab shouldn’t matter. This assumption
obviously doesn’t hold so we are putting that as our secondary analysis.

  

\#Exclusion

We will subset samples to have:

- survived to 4 weeks
- have received test result by 4 weeks
