# Week 6 Competition: Hidden Hate

**Tuesday 17 November 2026, 10:00 to 16:00 (Riyadh time). 6 hours.**

**Join on Kaggle:** https://www.kaggle.com/t/e05037474f1c49eb951a2051dd6daad4 (invitation link; sign in with the Kaggle account your instructor linked to your student id, then click Join).

**Competition page:** https://www.kaggle.com/competitions/ai-olympiad-l1-2027-hidden-hate

A social network wants to find posts that spread hate **without a single slur**. The hate in these posts hides in hints, jokes, questions and hashtags, so a list of bad words does not find it. For the training posts you get the text and the answer; for the test posts you get only the text.

**Your task:** label every test post as **toxic (1)** or **not toxic (0)**, and beat the starter solution.

**A warning about the data:** these are real posts, and some are offensive. They were collected because they carry hate; that is why a model has to find them. Treat them as data, and do not share them outside the course.

Everything you need was taught in Week 6: TF-IDF (Day 36), recurrent networks (Day 37), attention and BERT (Day 38), and the three labs.

## Timeline

| What | Riyadh time (UTC+3) | UTC |
|---|---|---|
| Competition opens, starter notebook and data published | Tue 17 Nov, 10:00 | Tue 17 Nov, 07:00 |
| Competition closes, private leaderboard revealed, notebooks handed in | Tue 17 Nov, 16:00 | Tue 17 Nov, 13:00 |

Your work is checked as you go and the clock starts at 10:00 for everybody: the task reading counts most in the first 25 minutes, and a first file above the baseline in the first 60.

## Files

| File | Columns | What it is |
|---|---|---|
| `train.csv` | `id`, `text`, `label` | the labelled posts: `label` is 1 for a toxic post, 0 for a post that is not toxic |
| `test.csv` | `id`, `text` | the posts you label |
| `unlabeled.csv` | `text` | more posts from the same network, without a label; you may use them |
| `sample_submission.csv` | `id`, `label` | the exact shape of the file you upload: every test id, all `0` |

The posts are already in lower case, with punctuation split off by spaces (`what ? !`) and with links and user names removed. Hashtags keep their `#`.

The starter notebook downloads the four files from the public Kaggle dataset `sattamjaltwaim/ai-olympiad-l1-2027-week-6-competition-data` with `kagglehub`; on Colab it needs no Kaggle key. The same files are on the competition's Data tab.

## The starter notebook

[`starter.ipynb`](starter.ipynb) is the whole starter solution, part by part, with a checkpoint after each part, and it runs from top to bottom as it is:

1. **Setup:** installs the checkpoint library, opens your session (replace `PASTE-YOUR-ID` with your own student id), imports, downloads the data.
2. **Load and look** at the posts.
3. **Read the task:** five short answers about the metric, two answers that need no model, what the metric rewards, the file format and what you noticed. Each answer cell holds a placeholder (`None`) so that the notebook runs; replace it with your answer.
4. **The starter solution:** a plain recurrent network on word numbers. It writes `submission.csv`. Its score is the **baseline**: your points count from it upward.
5. **Beat the baseline:** your part.
6. **Finish:** `ck.finish()` hands in your notebook.

## Evaluation

The score is **accuracy**: the share of test posts whose label is right. Every post counts the same, toxic or not.

- The **public leaderboard** scores 40% of the test posts and is visible during the competition.
- The **private leaderboard** scores the other 60%. It appears at 16:00 and gives the final ranking.
- A public score on so few posts moves by about plus or minus 0.015 from luck alone. Trust your validation set more than the public board.

## Submission format

A CSV file with a header line and exactly one row for every post of `test.csv`, in any order. `label` is `0` or `1`; probabilities are not accepted.

```
id,label
3908,0
3909,1
3910,0
...
```

Each time you write a better file, run the checkpoint under it in the notebook **and** upload the file on Kaggle (Submit Prediction). On Colab, download it first from the Files panel (the folder icon on the left, then the three dots beside `submission.csv`, then Download).

## Rules

1. **Solo only.** Every student competes alone: no teams, no merging, one Kaggle account per student, the account linked to your student id by your instructor.
2. **20 submissions per student.** The whole competition sits inside one Kaggle day, so the counter does not reset.
3. **Your own work.** You may not get help on the code from other people. AI assistants (chatbots, code completion such as Gemini in Colab or Copilot) are switched off for the whole competition.
4. **Allowed tools:** everything taught in Weeks 1 to 6: Python, NumPy, pandas, scikit-learn, PyTorch, and Hugging Face `transformers`.
5. **Pretrained models are allowed**, such as a BERT or RoBERTa from Hugging Face, with one exception: **no model that was already trained to detect hate, toxicity or offensive language**. Such models learned from posts like these, answers included.
6. **No other data.** No other labelled posts, and no searching for where these posts come from. `unlabeled.csv` belongs to the task and may be used.
7. **20-minute notebook.** Your final notebook, restarted and run from top to bottom, must finish in under 20 minutes (a Colab GPU is fine) and write the file you chose as your final submission. Your instructor runs it again after the competition; a notebook that cannot reproduce its file does not keep its score.
8. **One final submission.** Before 16:00, on the Submissions page, tick **Use for Final Score** on the file your final notebook writes. If you choose nothing, Kaggle chooses your best public score, which may not be that file.
9. **Hand in your notebook** by running its last cell, `ck.finish()`, before 16:00. A score without a notebook does not count.
10. **Final ranking:** the private leaderboard.
11. **Your student id is yours alone.** Never share a notebook that holds it.

## Getting started

1. Join the competition with the invitation link above. Open the starter in Colab (course website, Week 6, Day 39), paste your id, and run every cell. Upload its `submission.csv` on Kaggle: you are on the board.
2. Answer the task reading before minute 25.
3. Then follow the routine of the week's labs: one change at a time, a validation score for each, a new file each time the validation score rises.

## FAQ

- **Can I use a pretrained transformer?** Yes (rule 5), as long as it was not already trained to detect hate or toxic language, and your notebook still runs in under 20 minutes. Turn the GPU on first (Colab: Runtime, then Change runtime type, then T4 GPU).
- **My validation accuracy and the public board disagree.** Both can be right: the public board holds only 40% of the test posts. Keep the model your validation set prefers.
- **Can I submit probabilities?** No. Turn them into `0` and `1` first (for example, `1` when the probability of toxic is above 0.5).
- **Can I use `unlabeled.csv`?** Yes (rule 6). It has no answers, so think about what it can and cannot give a model.
- **The checkpoint says my file is fine, but where is my score?** The score comes from Kaggle: upload the same file there.
