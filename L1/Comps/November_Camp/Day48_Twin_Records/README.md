# Day 48 Competition: Twin Records

**Friday 27 November 2026, 10:00 to 16:00 (Riyadh time). 6 hours.** The Tabular ML exam runs before it.

**Join on Kaggle:** https://www.kaggle.com/t/5242c57ddfe54d95b5749f664f209ace (invitation link; sign in with the Kaggle account your instructor linked to your student id, then click Join).

**Competition page:** https://www.kaggle.com/competitions/ai-olympiad-l1-2027-twin-records

![Two records of one trip](banner.png)

A railway company records every train trip twice. The **timetable log** knows the plan and the dispatchers' reports: how many stops the train has, how long the trip should take, how late it left and how late it arrived. A **GPS box** on the train only knows what it measured about once a minute: how long the train moved, how far it went, how often it stopped and how fast it was.

A failed software update lost the number that linked the two records of a trip, for every trip after 1 September, and shuffled the rows. Only the day and the hour of departure survived. So the records come in **blocks**: a block holds all the trips that left in one hour of one day, the same trips in both tables, in a different order and with different numbers.

**Your task:** for every September GPS record, find the log entry of the same trip, and beat the starter solution.

## Timeline

| What | Riyadh time (UTC+3) | UTC |
|---|---|---|
| Competition opens, starter notebook and data published | Fri 27 Nov, 10:00 | Fri 27 Nov, 07:00 |
| Competition closes, private leaderboard revealed, notebooks handed in | Fri 27 Nov, 16:00 | Fri 27 Nov, 13:00 |

The clock starts at 10:00 for everybody.

## Files

| File | What it is |
|---|---|
| `train.csv` | 59,848 earlier trips (14 August to 1 September) in 435 blocks: the log columns and the GPS columns side by side, so every pair is known |
| `test_a.csv` | the September timetable log: `a_id`, `block`, `hour` and the 11 log columns (22,868 rows, 156 blocks) |
| `test_b.csv` | the September GPS records: `b_id`, `block`, `hour` and the 17 GPS columns (the same trips in the same blocks) |
| `sample_submission.csv` | the exact shape of the file you upload: `b_id`, `a_id` (a random matching inside every block) |

The meaning of every column is in the starter notebook. The starter downloads the files from the public Kaggle dataset `sattamjaltwaim/twin-records` with `kagglehub`; on Colab it needs no Kaggle key. The same files are on the competition's Data tab.

## The starter notebook

[`starter.ipynb`](starter.ipynb) runs from top to bottom as it is, in about a minute (no GPU needed).

1. **Setup:** installs the checkpoint library, opens your session (replace `PASTE-YOUR-ID` with your own student id), imports, downloads the data.
2. **Loading the files** and a first look at each table.
3. **Validation:** 40 blocks of `train.csv` shuffled like the test (`val_a`, `val_b`, and `val_key` with the right pairs), and `accuracy`: measure your ideas here before you upload.
4. **Baseline:** a random matching inside every block, then `save_submission`, which checks the file and writes `submission.csv`, and `ck.submit`. Its score is the **baseline**: your points count from it upward.
5. **Your own cells**, then **Finish:** `ck.finish()` hands in your notebook.

Run `ck.submit("submission.csv")` on every file you upload to Kaggle: it checks the file's format and records it.

## Evaluation

The score is **accuracy**: the share of GPS records matched to the right log entry.

- The **public leaderboard** scores 40% of the GPS records and is visible during the competition.
- The **private leaderboard** scores the other 60%. It appears at 16:00 and gives the final ranking.
- The validation blocks in the notebook give you a score of your own before you spend a submission.

## Submission format

A CSV file with the header `b_id,a_id` and exactly one row for every GPS record of `test_b.csv` (22,868 rows), in any order.

```
b_id,a_id
100000,200000
100001,200001
...
```

Each time you write a better file, run `ck.submit("submission.csv")` in the notebook **and** upload the file on Kaggle (Submit Prediction). On Colab, download it first from the Files panel (the folder icon on the left, then the three dots beside `submission.csv`, then Download).

## Rules

1. **Solo only.** Every student competes alone: no teams, no merging, one Kaggle account per student, the account linked to your student id by your instructor.
2. **20 submissions per student.** The whole competition sits inside one Kaggle day, so the counter does not reset.
3. **Your own work, without help.** Nobody helps you with the code: not other students, not the instructors. AI assistants (chatbots, and code completion such as Gemini in Colab or Copilot) are switched off for the whole competition.
4. **Allowed libraries.** NumPy, pandas, SciPy, scikit-learn and matplotlib. No other library and no pretrained model.
5. **No other data.** Use only the files of this competition, and do not search for where the task or the data come from: an answer key found elsewhere is other data.
6. **20-minute notebook.** Your final notebook, restarted and run from top to bottom, must finish in under 20 minutes and write the file you chose as your final submission. Your instructor runs it again after the competition; a notebook that cannot reproduce its file does not keep its score.
7. **One final submission.** Before 16:00, on the Submissions page, tick **Use for Final Score** on the file your final notebook writes. If you choose nothing, Kaggle chooses your best public score, which may not be that file.
8. **Hand in your notebook** by running its last cell, `ck.finish()`, before 16:00. A score without a notebook does not count.
9. **Final ranking:** the private leaderboard.
10. **Your student id is yours alone.** Never share a notebook that holds it.

## Getting started

1. Join the competition with the invitation link above. Open the starter in Colab (course website, November Camp, Day 48), paste your id, and run every cell. Upload its `submission.csv` on Kaggle: you are on the board.
2. Then work as in the case studies: read the statement and the given code, look at the data, list what you notice, and test one idea at a time on the validation blocks.

## FAQ

- **Do I need a GPU?** No.
- **The checkpoint says my file is fine, but where is my score?** The score comes from Kaggle: upload the same file there.

## Licence

Adapted from a national AI olympiad task, licence CC BY-NC-SA 4.0 (attribution in full after the competition). The competition data is shared under the same licence.
