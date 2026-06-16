# RealPlay Collection Album: A Coupon-Collector Model

A full 81-card album costs about **101 Card Packs** on average, and the last 10 cards alone are **59% of the total**. This repo models a social-casino collection feature with a closed-form anchor, a 60,000-run simulation, and an interactive browser version.

## At a glance

- 81 cards in 9 sets, packs of 4 random cards, duplicates allowed
- Closed form for a uniform drop: (81 / 4) · H_81 = **100.8 packs**
- Simulation across 60,000 albums: **mean 101, median 97**
- The tail: the first half of the album is **14%** of the packs, the last 10 cards are **59%**, the final card alone is **20%**

## Try it and read it

- **Live simulator:** https://taljacob28.github.io/realplay-collection-album-simulator/ . Drop weights, pity, and pack size are adjustable, and every figure redraws on each run.
- **Notebook:** [`packs_to_complete.ipynb`](packs_to_complete.ipynb) . The closed form, the simulation, and the tail decomposition, with the charts.
- **Configuration:** the parameters the model runs on are in the [Google Sheet](https://docs.google.com/spreadsheets/d/1foRnmhvBxSKDBGWecdrQu3VuKdiemkG_giFvcAoH800/edit?usp=sharing).

## The question

How many Card Packs does a player open, on average, to complete the album? The answer sizes the feature. It sets how far completion sits from a typical player, and it shows where the chase turns into a grind.

## What the model shows

The average is a fair summary here. The median, 97, sits close to the mean, 101, so the count is concentrated rather than skewed. The real story is where the packs fall inside the album. The first half is nearly free. The last 10 cards carry most of the weight, and the final card alone is a fifth of the whole run.

Two findings follow, and both are testable against this uniform baseline. Completion is rare, so the feature lives in the journey, through set rewards and visible near-completion, not the full-album prize. And the levers attacking the tail, pity, a targeted offer for a missing card, or trading, are the ones to A/B test.

---

## Method

The closed form treats the album as a coupon-collector problem. For a uniform drop, the expected number of single-card draws to collect all n cards is n · H_n, where H_n is the harmonic number. Dividing by 4 cards per pack gives 100.8 expected packs.

The simulation draws packs until all 81 cards appear, across 60,000 albums, and recovers the full distribution, the percentiles, and the tail. It agrees with the closed form at 101.2 packs, the small gap being whole-pack rounding. The same function extends to pity and weighted drops, where no clean formula exists.

## Run it

```bash
pip install numpy matplotlib
jupyter notebook packs_to_complete.ipynb
```

The notebook is self-contained. A configuration block at the top holds the parameters, so no external files are needed.
