# CS-433 Machine Learning — personal working setup (Fall 2026)

Everything of mine lives in `my/`. Upstream (`epfml/ML_course`) never touches this directory, so
course updates can never conflict with my work.

## How the grade is actually made

| Component | Weight | Deadline |
|---|---|---|
| Project 1 | **0%** (not formally graded) | Oct 29 / Nov 1 — *see note* |
| Project 2 | **30%** | Dec 17 |
| Final exam | **70%** | January |

*Note: the course info sheet lists Project 1 as "due Oct 29th" on the assessment page but
"Deadline: Nov 1st" in the Project 1 section. Confirm the real date on the course website / Ed.*

The consequences are worth being blunt about:

- **The exam is the course.** 70% of the grade, and the repo already contains 10 past papers with
  solutions. Effort spent there has the highest and most certain return.
- **Project 1 is ungraded but is not optional.** It is the dress rehearsal for Project 2, and its
  content — linear/logistic regression, gradient descent, cross-validation, all implemented from
  scratch — *is* the core of the exam. Treat it as exam prep that happens to have a leaderboard.
- **Project 2 is the only graded coursework.** 30% from one project. Choosing a good ML4science
  topic and a responsive host lab early matters more than any late-night optimisation.

## Weekly loop

1. **Before the lecture:** skim the PDF in `lectures/`. Ten minutes; just to know what's coming.
2. **After the lecture:** `my/bin/ml-sync` to get new material.
3. **Same week, do the lab:** `my/bin/ml-lab NN`, then work in `my/labs/exNN/`.
   Do *not* look at the solution first. The doctests (`test(fn)`) tell you when you're right.
4. **When the official solution is released:** `my/bin/ml-diff NN <notebook>` and read every
   difference. Where they were more elegant or more vectorised, understand why.
5. **Add to the cheat sheet** (`my/cheatsheet/`) while it's fresh — formula plus the one condition
   you keep forgetting. Five minutes a week beats a panicked day in January.
6. **From October:** one past exam every ~2 weeks, timed. Log it in `my/exam-prep/README.md`.

Exercise sessions are Thursdays 14:15–16:00, room by lastname:
INF1 (A–Da) · INF119 (De–Fr) · INJ218 (Fr–Lin) · INM202 (Lind–Rr) · INR219 (Ru–Z).
Go to them — the TAs are the fastest path past a stuck lab.

## Commands

```bash
conda activate ml-course        # the environment for everything

my/bin/ml-sync                  # pull new course material, merge into my branch
my/bin/ml-lab 02                # scaffold my/labs/ex02/ from the upstream template
my/bin/ml-diff 02 ex02.ipynb    # rich diff: my notebook vs the official solution
jupyter lab                     # kernel: "Python (ml-course)"
```

## Repository layout

```
labs/  lectures/  exam/    read-only mirror of upstream — never edit these
my/
  labs/exNN/       my copies of the templates + my solutions
  cheatsheet/      LaTeX A4 cheat sheet, built up all semester  <- 70% lever
  exam-prep/       past-paper log and topic tally
  notes/           per-lecture notes
  projects/        project1/, project2/
  bin/             ml-sync, ml-lab, ml-diff
```

## Git model

- `main` — pristine mirror of upstream. **Never commit here.** Pulls are always fast-forward.
- `study` — my branch. All my work. `ml-sync` merges `main` into it.

Because my files and upstream's files never overlap, the merge is always trivial. `nbdime` is
configured as the notebook diff/merge driver, so notebook diffs are readable rather than JSON soup.

## Rules to respect

- **Project 1 requires from-scratch implementations** — no scikit-learn for the core methods.
  `sklearn` is installed here for exploration and for Project 2, but keep it out of Project 1's
  graded implementations. Check the project statement for the exact rule when it is released.
- Projects are in **groups of 3**. Start looking for teammates on the Ed forum early; good teams
  are formed in September, not the week before the deadline.
