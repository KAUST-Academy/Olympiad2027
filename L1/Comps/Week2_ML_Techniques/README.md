# Week 2 Competition: Outcome After Treatment

**Friday 2 October 2026, 13:00, to Saturday 3 October 2026, 13:00 (Riyadh time). 24 hours.**

**Join on Kaggle:** https://www.kaggle.com/t/0bc9abf7444a41588f33f496cfcd2bd5 (invitation link; sign in with your Kaggle account, then click Join).

A hospital wrote down facts about each patient when their treatment started: age, the size and the
stage of the illness, how the cells looked under a microscope, two lab tests, and a page of blood
measurements. Later the hospital wrote down how it ended. For the training patients you get both the
facts and the ending; for the test patients you get only the facts.

**Your task:** predict, for every test patient, whether the ending is the worse outcome (`1`) or not
(`0`). About one patient in six ends with `1`.

This is the week's Lab 2 without the scaffolding: load, explore, clean, model, validate, submit.
Everything you need was taught between Day 08 and Day 13.

## Timeline

| What | Riyadh time (UTC+3) | UTC |
|---|---|---|
| Competition opens, data and starter notebook published | Fri 2 Oct, 13:00 | Fri 2 Oct, 10:00 |
| Last moment to merge teams | Sat 3 Oct, 07:00 | Sat 3 Oct, 04:00 |
| Competition closes, private leaderboard revealed | Sat 3 Oct, 13:00 | Sat 3 Oct, 10:00 |
| Notebook hand-in closes (Day 14 Google Form) | Sat 3 Oct, 13:30 | Sat 3 Oct, 10:30 |

Kaggle counts submissions per day in UTC: your 12 submissions reset at 03:00 Riyadh time on
Saturday, so the window holds two counting days.

## Files

| File | What it is |
|---|---|
| `train.csv` | 2,092 patients, one per row, with the `outcome` column |
| `test.csv` | 1,127 patients, same columns, without `outcome` |
| `sample_submission.csv` | the exact shape of the file you upload: `id,outcome`, one row per test patient, all `0` |
| `starter.ipynb` | loads the data, trains a baseline, writes a valid `submission.csv` |

The data lives on the competition's Kaggle page (Data tab). Open the starter notebook there
("Code", then "New Notebook" or copy the starter) and the data is already attached. On Colab the
starter downloads it with `kagglehub`, which needs your Kaggle account token.

## The columns, in plain words

Every row is one patient. The table is exactly as the hospital collected it: some cells are blank,
and some numbers are impossible (a size below zero, a count below zero, a value that cannot be a
measurement). Deciding what to do with those is part of the task.

| column | what it is |
|---|---|
| `id` | row number, not a feature |
| `age` | the patient's age in years, written with decimals as recorded |
| `population_group` | which of three groups of patients the hospital uses: A, B or C (the groups have no order) |
| `living_situation` | who the patient lives with: H1 married, H2 single, H3 divorced, H4 widowed, H5 separated |
| `growth_size_class` | how big the growth was when it was found, in four classes from A1 (smallest) to A4 (largest) |
| `spread_class` | how far the illness had reached into the tissue next to the growth, from B1 (least) to B3 (most) |
| `size_and_spread` | the two classes above written together, for example A2_B1 |
| `overall_stage` | the doctors' overall stage, from C1 (earliest) to C5 (most advanced); blank for some patients |
| `extent` | E1: the illness stayed in one area; E2: it had reached distant parts of the body |
| `cell_appearance` | how the cells look under a microscope: K1 almost normal, K2 somewhat changed, K3 very changed, K4 nothing like normal cells |
| `cell_grade` | the same idea as a number written in text: 1, 2 or 3 (one odd value appears) |
| `growth_size_mm` | the size of the growth in millimetres; blank for some patients, and some values are impossible for a size |
| `test_e` | a lab test, P (positive) or N (negative); a positive test means a common treatment is expected to work |
| `test_p` | a second lab test of the same kind, P or N |
| `tests_e_and_p` | the two test results written together, for example P_N |
| `samples_checked` | how many small tissue samples the doctors checked |
| `samples_affected` | how many of those samples showed the illness |
| `samples_clear` | how many of those samples did not show it |
| `blood_pressure_high` | blood pressure, the upper number |
| `blood_pressure_low` | blood pressure, the lower number |
| `cholesterol` | cholesterol level in the blood |
| `body_temperature` | body temperature in degrees Celsius |
| `blood_oxygen` | oxygen level in the blood, in percent |
| `breaths_per_minute` | breaths per minute |
| `blood_sugar` | sugar level in the blood |
| `bmi` | body mass index: weight compared with height |
| `pulse` | heart beats per minute |
| `creatinine` | a blood test value that doctors use to check the kidneys |
| `uric_acid` | a blood test value |
| `hemoglobin` | the part of the blood that carries oxygen |
| `kidney_filter_rate` | how fast the kidneys filter the blood |
| `sodium` | salt (sodium) level in the blood |
| `potassium` | potassium level in the blood |
| `albumin` | a protein level in the blood |
| `lactate` | a blood test value |
| `outcome` | 0 = the patient was doing well at the end of the follow-up; 1 = the worse outcome, the patient did not recover (about one patient in six); only in train.csv |

**What usually goes together.** You need no medical knowledge. A bigger growth, more affected
samples, a higher overall stage or more spread go with outcome `1` more often. A positive lab test
goes with outcome `0` more often. Whether a blood measurement tells you anything is for you to find
out with the tools of Day 13.

## Evaluation

The score is the **F1 score for outcome = 1** (Day 09): with TP the test patients you correctly
marked `1`, FP the patients you marked `1` who were `0`, and FN the patients you marked `0` who
were `1`,

```
precision = TP / (TP + FP)        recall = TP / (TP + FN)        F1 = 2 * precision * recall / (precision + recall)
```

Two answers you can compute without a model: marking everyone `1` scores **0.27**, marking everyone
`0` scores **0.00**. The starter's baseline scores about **0.37**. The score is computed on your
`0`/`1` labels, so the threshold you choose matters as much as the model.

- The **public leaderboard** scores 40% of the test patients and is visible all the time.
- The **private leaderboard** scores the other 60% and is revealed at the end. It is the final
  ranking.
- With about 170 patients of outcome `1` in the test set, the second decimal of a score is partly
  luck. Trust your cross-validation over the public board (Day 13).

## Submission format

A CSV with a header and exactly one row per test patient, in any order, values `0` or `1` only:

```
id,outcome
3,0
5,1
8,0
...
```

Probabilities are not accepted; the starter's `make_submission` function writes the file correctly.
You may choose **2 final submissions** on the Kaggle page before the end; by default Kaggle takes
your best public scores.

## Rules

1. **Teams** of at most 3 students; solo is allowed. Form or merge a team on the Kaggle page before
   Saturday 07:00 Riyadh time. One team per student.
2. **12 submissions per team per Kaggle day** (reset at 03:00 Riyadh time on Saturday).
3. **Allowed tools:** pandas, NumPy, scikit-learn, matplotlib, and anything else taught in Week 2.
   No other data of any kind, and no searching for where this table comes from. Everything you need
   is in `train.csv`.
4. **Your own work:** you may discuss ideas with other teams, but every line of code in your
   notebook is written by your team.
5. **Hand in your final notebook** (one per team, the team name in the first cell) through the
   Day 14 Google Form by Saturday 13:30 Riyadh time. A score without a notebook does not count.
6. **Final ranking:** the private leaderboard. Ties are broken by the earlier of the two final
   submissions.
7. Do not modify the two cells marked *do not modify* in the starter notebook; they keep your file
   in the right shape.

## Getting started

1. Join the competition with the invitation link above. Open the starter notebook from the Kaggle page
   (or in Colab from this folder) and run it top to bottom: it writes `submission.csv`.
2. Upload that file. You now have a score on the board and the rest of the 24 hours to beat it.
3. Then follow the Day 13 routine: look at the table, choose your folds, build out-of-fold
   predictions, compare models against the spread, refit on all rows, check the file, upload.

## FAQ

- **A cell is blank. Is that an error?** No. It is a patient for whom that value was not recorded.
  Blanks are information: Day 06 and Day 12 show what to do with them.
- **A size or a count is negative, and some sizes are enormous.** The table is as collected. Decide
  what such values mean and what to do with them; `describe()` and `value_counts()` are the tools.
- **What does a blood measurement mean?** A number the hospital recorded. You do not need to know
  more about it than its name; the question is whether it helps the model, and Day 13's
  permutation importance answers that.
- **My cross-validation says 0.40 and the public board says 0.36 (or 0.45).** Both can be right: the
  public board is 40% of the test patients, and F1 on a rare class moves a lot between samples.
  Keep the model your cross-validation prefers.
- **Can I submit probabilities?** No. The score needs `0`/`1` labels. Choose the threshold on
  out-of-fold predictions (Day 13), then apply it to the test probabilities.
- **My notebook runs on Colab but cannot download the data.** Colab needs your Kaggle API token for
  `kagglehub`; the simplest path is to work inside a Kaggle notebook, where the data is attached.
