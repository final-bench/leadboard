# LEADBOARD

**Open the board:** https://huggingface.co/spaces/FINAL-Bench/leadboard

A benchmark for drug property prediction tools. One yardstick, one discipline at a time.

Submit predictions for a held-out set of molecules. They are scored against labels that are
never released, and the tool is placed on the board for that discipline.

Run by [VIDRAFT](https://vidraft.net). A Hugging Face login is required to submit.

## Why the split matters

Most published benchmarks split their molecules at random. That is the wrong question. A tool is
used to rank compounds nobody has measured yet, so the honest test is to train on what was known
by a cut-off year and predict what came after.

The same data and the same model were run under both splits. On the hERG cardiotoxicity board,
AUROC was **0.818** under a random split and **0.606** under a time split. Same molecules, same
code. Only the question changed. Every board here uses the harder one.

## What is published before any entry arrives

| Published | Why it matters |
|---|---|
| Untrained baselines | Constant prediction, nearest neighbour, Morgan plus LightGBM. If a tool cannot beat these, the board says so. |
| Experimental noise floor | How far apart two laboratories land when they measure the same compound. Nothing can be measured below it. |
| Split grade and answer grade | Exactly how the test set was cut, and whether the labels can be looked up anywhere. |
| Data and scorer fingerprints | The SHA of the exact test file and scoring code behind every score. |

A score without its noise floor is a number without a unit. Both are shown.

## Grading notation

Each board carries two letters, for example `[T/P2]`.

**Split grade**, what the board asks of a tool

| | |
|---|---|
| `T` | time split by first-report year |
| `S` | scaffold split by Murcko core |
| `R` | random split. These are not opened. |

**Answer grade**, whether an entrant can look the answer up

| | |
|---|---|
| `P1` | public source, our curation |
| `P2` | public source, our unit conversion and selection define this revision |
| `P3` | labels held privately |
| `P4` | prospective. The answer does not exist yet. |

## Boards

46 boards across 14 of 16 disciplines, 57,698 held-out compounds. 96 boards are planned.

| Discipline | Boards |
|---|---|
| Absorption | Solubility, LogP, Caco2 |
| Distribution | PPB, Vdss |
| Metabolism | CYP3A4, CYP2D6, CYP2C9 |
| Excretion | HalfLife |
| Toxicity | hERG, LD50 |
| Potency | AChE, MAOB, COX2, Nav17 |
| Epigenetics | BRD4, HDAC1 |
| Nuclear receptors | ERalpha, AR |
| Proteases | BACE1, Thrombin, FactorXa |
| Kinase & Selectivity | EGFR, JAK2, PI3Ka, FLT3, VEGFR2, CDK2, HER2, ABL1, BRAF, KIT, ALK, Selectivity |
| Receptors & GPCR | D2, HT2A, MuOpioid, KappaOpioid, A2A, CB1 |
| Cell & Phenomics | Phenotype |
| Anti-infective & whole-cell | Malaria, SEpidermidis, MTB, SAureus |
| Clinical in-silico | Withdrawal |

### A note on the withdrawal board

Withdrawal rate tracks the approval decade: 7.8 percent in the 1990s, 1.2 percent in the 2010s.
A predictor that reads nothing but the approval year therefore scores AUROC 0.636. After the
controls are year-matched it scores 0.504, which is chance. That matched version is the one
that was opened.

## How to enter

1. Pick a board and download its test set. Structures only, no labels.
2. Predict with your own tool. A trained model, a physics engine, a language model or a rule of
   thumb are all accepted.
3. Upload a CSV of `compound_id,prediction` and sign in with a Hugging Face account.
4. Scoring runs off-platform on hardware that holds the labels. The Space never sees them.

The Space carries a filled-in prompt and a runnable skeleton for each board, so a first entry
does not require building anything from scratch.

### Repeated submissions

A new score is revealed under the ladder rule (Blum and Hardt, ICML 2015): it replaces a previous
best only when it beats that best by more than the noise floor. Otherwise the previous best
stands. This is what stops a board from being won by whoever submits the most times.

## Data and licences

| Source | Licence |
|---|---|
| ChEMBL 37 (EMBL-EBI) | CC BY-SA 3.0. Re-curated, and attribution travels with every board card. |
| JUMP Cell Painting Consortium | CC0 |
| Withdrawal board | Assembled from public regulatory records |

Non-commercial research benchmark. Test sets carry structures only. Labels are never distributed.

## What is in this repository

Public benchmark facts: the disciplines and boards, the grading notation, what is published
before entry, how to enter, and the data licences.

The held-out labels, the scoring implementation and the hardware that holds the labels are not
published. That is the point of the benchmark.

## Related

| | |
|---|---|
| Open Discovery Challenge | https://github.com/final-bench/open-discovery-challenge |
| Open Materials Challenge | https://github.com/final-bench/open-materials-challenge |
| Hugging Face organisation | https://huggingface.co/FINAL-Bench |

Specification v1.1, eight clauses. FINAL-Bench / VIDRAFT.

## Contact

vidraft@mail.vidraft.net · [vidraft.net](https://vidraft.net) · X [@VIDRAFT_ai](https://x.com/VIDRAFT_ai) · Threads [@vidraft_lab](https://www.threads.com/@vidraft_lab)
