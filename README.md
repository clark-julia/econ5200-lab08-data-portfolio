# econ5200-lab08-data-portfolio
# Diagnosing Underpowered Studies and P-Hacking

## Objective
I diagnosed two flawed analyses, an underpowered pilot study and a p-hacked subgroup result, and corrected each one using power analysis and multiple-testing corrections.

## Methodology
- Ran a power analysis on a pilot study with 15 people per group to find its achieved power against the true effect.
- Solved for the sample size per group needed to reach 80% power, then reran the study at that size.
- Tested 20 subgroups of a job training program and applied a Benjamini-Hochberg (BH) correction to the 20 p-values.
- Calculated the theoretical chance of at least one false positive across 20 tests of true nulls.
- Simulated 1,000 replications of 20 true-null tests to see how often at least one p < 0.05 appeared.
- Wrote my own Benjamini-Hochberg function and checked it against statsmodels, then tested it on a set where two subgroups had real effects.
- Compared four tests on heavy-tailed earnings data: Welch's t-test, Yuen's trimmed t-test, a permutation test on the difference in means, and a permutation test on the difference in trimmed means.

## Key Findings
- The pilot study had only 10.9% power with 15 people per group, so its "no evidence" conclusion was not justified. Failing to reject the null did not show the program had no effect.
- 80% power needed 222 people per group. At that size the test gave p = 0.0012, and the effect was detected.
- After the BH correction, 0 of the 20 subgroups stayed significant, so the "significant" subgroup was a chance result.
- In the simulation, 65.8% of 1,000 replications had at least one p < 0.05, against 64.2% in theory.
- My BH function matched statsmodels, and with two real effects planted it flagged 2 subgroups.
- On the heavy-tailed data, the four tests split by the statistic tested, not by parametric versus permutation. The two tests on means were not significant, and the two tests on trimmed means were.
