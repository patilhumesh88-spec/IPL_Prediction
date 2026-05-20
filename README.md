# IPL CRUNCH '26 — Submission

**Hackathon :** [IPL CRUNCH '26 by Wooble](https://wooble.org/hackathon/crunch-26)  
**Tagline :** *Five Seasons of IPL Data. Find Out What Actually Wins Matches.*  
**Dataset :** Ball-by-ball IPL data · Seasons 2020/21 – 2024 · 339 matches · ~290,000 deliveries

---

## What this project does

Three questions. Three honest answers. All numbers come directly from the dataset — no external stats sites, no manual lookups.

| # | Question | Answer |
|---|----------|--------|
| 1 | Do toss winners win more? | No — they win only **47.2%** of matches |
| 2 | Which phase is most linked to winning? | **Middle overs** (ov 7–15), gap of +8.1 runs |
| 3 | Top 5 batters and bowlers? | See tables below |

---

## Project structure

```
ipl_analysis.ipynb        ← main notebook (all analysis + charts)
att_0_1778303821_c3a907.csv  ← raw dataset (place in same folder)
chart1_toss_effect.png    ← saved from notebook cell 6
chart2_phase_runs.png     ← saved from notebook cell 8
README.md                 ← this file
```

---

## How to run

```bash
# 1. Install dependencies (standard data stack)
pip install pandas matplotlib jupyter

# 2. Put the CSV in the same folder as the notebook

# 3. Launch the notebook
jupyter notebook ipl_analysis.ipynb

# 4. Run All Cells — charts save automatically as PNG files
```

Python 3.8 or above. No internet connection needed once the CSV is present.

---

## Q1 — Does winning the toss help?

**Short answer : No.**

Across 339 matches with a result, teams that won the toss won **160 times (47.2%)**.  
Teams that lost the toss won **179 times (52.8%)**.

| Group | Matches won | Win rate |
|-------|-------------|----------|
| Toss winner | 160 | 47.2% |
| Toss loser | 179 | **52.8%** |

Breaking it down by toss decision:

| Choice made | Toss winner win rate |
|-------------|----------------------|
| Bat first | 42.9% |
| Field first | 49.0% |

Even when toss winners made the supposedly smarter call (fielding first), they still only won roughly half the time. The toss has almost no bearing on who lifts the trophy.

**Chart 1** shows these two numbers as a horizontal bar chart with a 50% reference line, so it is immediately obvious which group is above and below the coin-flip mark.

---

## Q2 — Which over phase is most linked to winning?

Overs are split into three phases:

| Phase | Overs |
|-------|-------|
| Powerplay | 1 – 6 |
| Middle overs | 7 – 15 |
| Death overs | 16 – 20 |

For every innings, runs are summed inside each phase. Those totals are then averaged separately for match-winning and match-losing innings.

| Phase | Winning innings avg | Losing innings avg | Gap |
|-------|--------------------|--------------------|-----|
| Powerplay | 53.2 | 46.8 | **+6.4** |
| Middle overs | 76.9 | 68.8 | **+8.1** ← largest |
| Death overs | 49.3 | 45.4 | **+3.9** |

The middle overs produce the biggest separation. Winning teams outscore losing teams by 8.1 runs in overs 7–15 — more than double the death-over gap. This makes sense: the powerplay has field restrictions and the death overs have all-out aggression, but the middle overs reward consistent batting partnerships and smart bowling rotations. That is where matches are quietly won.

**Chart 2** uses a grouped bar chart with the run-gap annotated above each phase pair, so any reader can see the conclusion without calculating anything themselves.

---

## Q3 — Top performers (2020/21 – 2024)

### Top 5 batters by total runs

| Rank | Batter | Runs |
|------|--------|------|
| 1 | F du Plessis | 2,718 |
| 2 | Shubman Gill | 2,717 |
| 3 | KL Rahul | 2,706 |
| 4 | V Kohli | 2,592 |
| 5 | RD Gaikwad | 2,380 |

*Source column : `runs_batter`, summed across all regular innings (innings 1 and 2 only).*

### Top 5 bowlers by total wickets

| Rank | Bowler | Wickets |
|------|--------|---------|
| 1 | YS Chahal | 105 |
| 2 | Rashid Khan | 94 |
| 3 | HV Patel | 92 |
| 4 | Mohammed Shami | 87 |
| 5 | K Rabada | 86 |

*Source column : `wicket_player_out` (not null) and `wicket_kind` ≠ run out. Run-outs are excluded because they are fielding dismissals, not credited to the bowler.*

---

## Surprising finding

> **Winning the toss is a slight disadvantage — and even choosing to field first barely helps.**

Most cricket commentary treats the toss as a significant moment. Captains take time deciding, analysts debate conditions, and broadcasters frame it as the first strategic move of the match.

The data tells a different story. Over 339 IPL matches spanning five seasons, toss winners won less often than toss losers. When toss winners specifically chose to field first — the conventional "smart" play in T20 cricket, exploiting dew and knowing the target — their win rate was still only 49.0%. That is essentially a coin flip.

This is genuinely surprising because it contradicts a belief that is repeated every match day. The data suggests that in modern IPL, teams are good enough at batting first or second that the toss edge has been completely neutralised.

---

## Methodology notes

- Super overs and tied-match extras are excluded (innings numbers 3 and above are dropped).
- No-result matches (where `winner` is null) are excluded from toss win-rate calculations only; their deliveries still count toward batter/bowler totals.
- All aggregations are done in pandas with no helper libraries — every step is visible in the notebook.

---

*Submitted to IPL CRUNCH '26 on Wooble — wooble.org/hackathon/crunch-26*
