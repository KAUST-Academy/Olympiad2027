# Day 43 Competition: Damaged Archive

**Sunday 22 November 2026, 10:00 to 16:00 (Riyadh time). 6 hours.** The exam runs from 9:00 to 9:50 before it.

**Join on Kaggle:** https://www.kaggle.com/t/11b8ce2566714f5099cbea7e329562cc (invitation link; sign in with the Kaggle account your instructor linked to your student id, then click Join).

**Competition page:** https://www.kaggle.com/competitions/ai-olympiad-l1-2027-damaged-archive

A photo archive kept **32 grey photographs**. Every photograph was copied many times, and every copy was changed at random before it was stored. Then all the copies were shuffled together. To save space, a copy is not stored as a picture: it is stored as two small arrays of numbers.

**Your task:** sort the copies back into **32 groups**, one group for each original photograph, and beat the starter solution.

Everything you need was taught in the Unsupervised Learning block (Days 40 to 42) and in the weeks before it.

## Timeline

| What | Riyadh time (UTC+3) | UTC |
|---|---|---|
| Exam | Sun 22 Nov, 9:00 to 9:50 | Sun 22 Nov, 06:00 to 06:50 |
| Competition opens, starter notebook and data published | Sun 22 Nov, 10:00 | Sun 22 Nov, 07:00 |
| Competition closes, private leaderboard revealed, notebooks handed in | Sun 22 Nov, 16:00 | Sun 22 Nov, 13:00 |

The clock starts at 10:00 for everybody. Your work is checked as you go: what you show of the data and a first batch for the network count most early, and so does a first file above the baseline in the first 60 minutes.

## Files

| File | What it is |
|---|---|
| `X1.npy` | a NumPy array of `float32`, shape (number of copies, 128, 4) |
| `X2.npy` | a NumPy array of `float32`, shape (number of copies, 4, 128) |
| `sample_submission.csv` | the exact shape of the file you upload: `id`, `target` (a random group for every copy) |

Row `i` of `X1` and row `i` of `X2` belong to the same copy, whose `id` is `i`.

The starter notebook downloads the three files from the public Kaggle dataset `sattamjaltwaim/damaged-archive` with `kagglehub`; on Colab it needs no Kaggle key. The same files are on the competition's Data tab.

## The starter notebook

[`starter.ipynb`](starter.ipynb) runs from top to bottom as it is:

1. **Setup:** installs the checkpoint library, opens your session (replace `PASTE-YOUR-ID` with your own student id), imports, downloads the data.
2. **The network:** `EmbNet`, the only neural network this task allows.
3. **Baseline:** loads the two arrays, groups the copies with KMeans, writes `submission.csv` and checks it with `ck.submit`. Its score is the **baseline**: your points count from it upward.
4. **Your own cells**, then **Finish:** `ck.finish()` hands in your notebook.

Run `ck.submit("submission.csv")` on every file you upload to Kaggle: it checks the file's format and records it.

## Evaluation

The score is the **Adjusted Rand Index** (ARI) between your groups and the true groups, as `sklearn.metrics.adjusted_rand_score` computes it. Only which copies you put together counts, not the numbers you give the groups: `0 0 1 1` and `7 7 3 3` score the same. 1 is a perfect grouping; a random grouping scores about 0.

- The **public leaderboard** scores 40% of the copies and is visible during the competition.
- The **private leaderboard** scores the other 60%. It appears at 16:00 and gives the final ranking.
- There are no labels to validate on: the public leaderboard is your only score, so spend your submissions with care.

## Submission format

A CSV file with a header line and exactly one row for every copy, in any order. `target` is a whole number: the group you put the copy in.

```
id,target
0,17
1,17
2,4
...
```

Each time you write a better file, run `ck.submit("submission.csv")` in the notebook **and** upload the file on Kaggle (Submit Prediction). On Colab, download it first from the Files panel (the folder icon on the left, then the three dots beside `submission.csv`, then Download).

## Rules

1. **Solo only.** Every student competes alone: no teams, no merging, one Kaggle account per student, the account linked to your student id by your instructor.
2. **20 submissions per student.** The whole competition sits inside one Kaggle day, so the counter does not reset.
3. **Your own work, without help.** Nobody helps you with the code: not other students, not the instructors. AI assistants (chatbots, and code completion such as Gemini in Colab or Copilot) are switched off for the whole competition.
4. **One network only.** If you use a neural network, it must be `EmbNet` from the starter, exactly as it is: do not change the class, do not train it, do not fine-tune its weights. Methods without a network (NumPy, pandas, scikit-learn, plotting) are allowed.
5. **No other data and no other pretrained model.** Use only the three files of this competition, and do not search for where the task or the pictures come from.
6. **20-minute notebook.** Your final notebook, restarted and run from top to bottom, must finish in under 20 minutes (a Colab GPU is fine) and write the file you chose as your final submission. Your instructor runs it again after the competition; a notebook that cannot reproduce its file does not keep its score.
7. **One final submission.** Before 16:00, on the Submissions page, tick **Use for Final Score** on the file your final notebook writes. If you choose nothing, Kaggle chooses your best public score, which may not be that file.
8. **Hand in your notebook** by running its last cell, `ck.finish()`, before 16:00. A score without a notebook does not count.
9. **Final ranking:** the private leaderboard.
10. **Your student id is yours alone.** Never share a notebook that holds it.

## Getting started

1. Join the competition with the invitation link above. Open the starter in Colab (course website, November Camp, Day 43), paste your id, and run every cell. Upload its `submission.csv` on Kaggle: you are on the board.
2. Then work as in the case studies: read the statement and the given code, look at the data, list what you notice, and test one idea at a time.

## FAQ

- **Do I have to use the network?** No. Rule 4 only says which network, if you use one.
- **Do the group numbers matter?** No. Any whole numbers work; only which copies share a number counts.
- **Can I use a GPU?** Yes, and the network runs faster on one (Colab: Runtime, then Change runtime type, then T4 GPU).
- **The checkpoint says my file is fine, but where is my score?** The score comes from Kaggle: upload the same file there.

## Licence

The pictures were made from photographs of the Kaggle dataset "Natural Images" by Prasun Roy, licence CC BY-NC-SA 4.0: made grey, cropped, resized, changed at random and compressed. The competition data is shared under the same licence.
