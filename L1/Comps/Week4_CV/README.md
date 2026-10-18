# Week 4 Competition: Camera or Generated?

**Sunday 18 October 2026, 16:00 to 22:00 (Riyadh time). 6 hours.**

**Join on Kaggle:** the invitation link is posted in the course channel when the competition opens.

A photo-sharing app receives thousands of tiny thumbnails every day. Some are real photos taken with a camera. Others were made by an image-generation model that was trained to imitate such photos, and the app wants to flag those automatically. For the training pictures you get the picture and the answer; for the test pictures you get only the picture.

**Your task:** decide, for every test picture, whether it was made by the model (`generated` = 1) or taken with a camera (`generated` = 0). Exactly half of the pictures are generated, in train and in test.

This is the week's Lab 2 without the scaffolding: look at the pictures, load them, build the network as a class, write the
training loop, validate, submit. Everything you need was taught between Day 22 and Day 27.

## Timeline

| What | Riyadh time (UTC+3) | UTC |
|---|---|---|
| Competition opens, data and starter notebook published | Sun 18 Oct, 16:00 | Sun 18 Oct, 13:00 |
| Competition closes, private leaderboard revealed | Sun 18 Oct, 22:00 | Sun 18 Oct, 19:00 |
| Notebook hand-in closes (Day 28 Google Form) | Sun 18 Oct, 22:30 | Sun 18 Oct, 19:30 |

## Files

| File | What it is |
|---|---|
| `train/camera/` | 3,500 real photos, 32 x 32 pixels, one PNG per picture, named `<id>.png` |
| `train/generated/` | 3,500 pictures made by the image-generation model, same format |
| `train.csv` | one row per training picture: `id`, `generated` (0 camera, 1 generated), `path` |
| `test/` | 3,000 unlabelled pictures named `<id>.png` |
| `sample_submission.csv` | the exact shape of the file you upload: `id,generated`, one row per test picture, all `0` |

The data lives on the competition's Kaggle page (Data tab). Open the starter notebook there ("Code", then "New Notebook" or
copy the starter) and the data is already attached. On Colab the starter downloads it with `kagglehub`, which needs your
Kaggle account token.

## The pictures, in plain words

Every picture is 32 x 32 pixels in colour (RGB), saved as a PNG. The training set has 3,500 camera pictures in `train/camera/` and 3,500 generated pictures in `train/generated/`; `train.csv` lists each one with its `id`, its `generated` label and its `path`. The test pictures sit in one folder, `test/`, named `<id>.png`, and `sample_submission.csv` lists their ids.

Both classes show the same kinds of things: everyday objects, vehicles and animals. The generator was trained to imitate exactly these kinds of pictures, so the difference is not *what* is in the picture but *how it was made*. Look at textures, edges, colour transitions and backgrounds; a convolutional network can learn such patterns from the pixels, which is what this week was about.

## Evaluation

The score is **accuracy** (Day 22): the share of test pictures whose label you got right.

```
accuracy = (pictures labelled correctly) / (all pictures scored)
```

Two answers you can compute without a model: marking everything `0` scores **0.50**, and so does marking everything `1`, because the two classes are exactly half and half. The starter's baseline scores about **0.72 to 0.75**, depending on the run. A score below 0.50 means the labels are the wrong way round.

- The **public leaderboard** scores 40% of the test pictures (1,200 of them) and is visible all the time.
- The **private leaderboard** scores the other 60% and is revealed at the end. It is the final ranking.
- With 1,200 public pictures, a public score moves by about plus or minus 0.01 from luck alone. Trust your validation accuracy over the public board.

## Submission format

A CSV with a header and exactly one row per test picture, in any order, values `0` or `1` only:

```
id,generated
3,0
5,1
8,0
...
```

Probabilities are not accepted; the starter's `make_submission` function writes the file correctly. You may choose **2 final submissions** on the Kaggle page before the end; by default Kaggle takes your best public scores.

## Rules

1. **Solo only.** Every student competes alone: no teams, no merging, one Kaggle account per student.
2. **10 submissions per student.** The whole window sits inside one Kaggle day, so the counter does not reset.
3. **Allowed tools:** PyTorch, torchvision, NumPy, pandas, matplotlib, scikit-learn, and anything else taught in Weeks 3 and 4.
4. **Pretrained models are allowed** (torchvision weights, the YOLO checkpoints, CLIP, or a network you train yourself), on one condition: your final notebook, restarted and run top to bottom, must finish in **under 30 minutes** on a Kaggle GPU notebook. The starter prints the run time next to the submission file; a handed-in notebook that cannot finish in 30 minutes does not count.
5. **No other pictures.** Pretrained weights are fine; extra training pictures of any kind are not, and no searching for where these pictures come from. Everything you need is in `train/`.
6. **Your own work:** you may discuss ideas with other students, but every line of code in your notebook is written by you.
7. **Hand in your final notebook** (your name in the first cell, outputs kept) through the Day 28 Google Form by 22:30 Riyadh time. A score without a notebook does not count.
8. **Final ranking:** the private leaderboard. Ties are broken by the earlier of the two final submissions.
9. Do not modify the two cells marked *do not modify* in the starter notebook; they keep your file in the right shape and print the run time.

## Getting started

1. Join the competition with the invitation link above. Open the starter notebook from the Kaggle page (or in Colab from this
   folder), turn the GPU on, and run it top to bottom: it writes `submission.csv`.
2. Upload that file. You now have a score on the board and the rest of the 6 hours to beat it.
3. Then follow the Day 27 routine: look at a training batch, make a valid file early, change one thing per run, log every run,
   choose on validation, and keep the same preprocessing for the test pictures.

## FAQ

- **Can I use a pretrained network (a torchvision ResNet, the YOLO weights, CLIP)?** Yes, as long as your whole notebook runs top to bottom in under 30 minutes (rule 4). On Kaggle, downloading weights needs Internet switched on in the notebook settings (a phone-verified account); on Colab it works directly.
- **How is the 30-minute limit checked?** Restart and run all before you hand in. The starter's last cell prints how many minutes passed since the data was loaded, and that line stays in the notebook you upload. Keep it under 30 on a Kaggle GPU.
- **The pictures are tiny. Should I resize them up?** For a network you train yourself it adds no information: a network built for 32 x 32 inputs (three poolings take it to 4 x 4) is enough, and Day 25 shows how to trace the shapes. A pretrained network expects bigger inputs, so resize for it (64 or 96 pixels is plenty) and watch the clock.
- **What is in the pictures?** Everyday objects, vehicles and animals, the same kinds in both classes. The question is how a picture was made, not what it shows.
- **My validation accuracy says 0.78 and the public board says 0.75 (or 0.81).** Both can be right: the public board is 40% of the test pictures, and a score on that many pictures moves by about 0.01 from luck alone. Keep the model your validation prefers, the way Day 27 says.
- **Can I submit probabilities?** No. The score needs `0`/`1` labels. Take `argmax` over the two outputs (or compare the probability with 0.5).
- **Training is slow.** Turn the GPU on (Kaggle: Settings, then Accelerator, then GPU; Colab: Runtime, then Change runtime type). Ten thousand tiny pictures train in about a minute on a GPU, and loading them all into one tensor once makes every epoch faster.
- **My notebook runs on Colab but cannot download the data.** Colab needs your Kaggle API token for `kagglehub`; the simplest path is to work inside a Kaggle notebook, where the data is attached.
