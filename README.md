# Regulating the Listening Wall: data and reproducibility notebook

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mark040297/listening-wall/blob/main/listening_wall_reproduction.ipynb)

This repository holds the data and code for:

> Arcayan, M. A. S. *Regulating the Listening Wall: Privacy-by-Design Requirements for Intelligent Noise Control Systems in Smart Cities. A Patent, Policy, and Signal Level Study with Lessons for Korea and ASEAN.*

The notebook `listening_wall_reproduction.ipynb` rebuilds every number, table, and figure in the paper that comes from data: the search and screening flow (Figure 1), the corpus results for both coders (Figures 2 to 5, Table B2), the inter-coder reliability (Table B1), the three experiments (Figures 7 to 9, Tables 6 and 7), and the control framework diagram (Figure 6). Its last cell compares every value, table, and figure with what is printed in the paper and reports any difference.

## Run it

1. Click **Open in Colab** above.
2. Choose **Runtime > Run all**.
3. The first code cell installs the exact library versions used for the paper. If anything has to be installed, the runtime restarts once. Choose **Runtime > Run all** again.

A full run takes about 45 to 60 minutes on a standard Colab CPU runtime, mostly for Experiment A. To rebuild only the figures and tables from the cached experiment results, set `RECOMPUTE_EXPERIMENTS = False` in the settings cell; this takes a few minutes.

To run locally instead, use Python 3.12, install `requirements.txt`, and open the notebook from the repository folder.

A full recompute uses floating point arithmetic, so on a different processor the last bits of some experiment results can change. The last cell therefore reports each value and table cell as identical, within one unit of its last printed digit, or different, and each figure as identical or as the share of pixels that changed. With the cached results (`RECOMPUTE_EXPERIMENTS = False`) every value, table, and figure is identical on any machine.

## Contents

| Path | What it holds |
|---|---|
| `listening_wall_reproduction.ipynb` | The notebook |
| `data/corpus/articles_included.csv` | The 260 included research articles (year, title, source, DOI) |
| `data/corpus/patents_included.csv` | The 392 included patents (application year, patent office, title, abstract) |
| `data/corpus/coder1_*.csv` | Coding sheets of coder 1 (the author) for the included records |
| `data/corpus/coder1_cleaning_log.csv` | Every cell of the coder 1 sheets that was cleaned before publication, with its original value and the rule applied |
| `data/corpus/coder2_*.csv` | Coding sheets of coder 2 (AI-assisted), with a note for every record and the round (pilot or main) |
| `data/corpus/coder2_pilot_v1_*.csv` | Pilot codes of coder 2 before the codebook was revised |
| `data/corpus/pilot_ids.json` | The 15 articles and 15 patents of the pilot round |
| `data/experiments/manifest.json` | Every audio file the experiments read, with SHA-256 checksums and dataset commits |
| `data/experiments/results_*.json` | Cached experiment results (used when `RECOMPUTE_EXPERIMENTS = False`) |
| `data/expected/` | What the paper prints: every quoted value (`paper_values.json`), every table, and every figure. The last cell of the notebook compares a new run with these files |
| `docs/codebook.md` | Codebook versions 1 and 2 and the conventions fixed during coding |
| `docs/coding_procedure.md` | How the two coders worked |
| `figures/`, `tables/`, `results/` | Written by the notebook |

## Data sources and licenses

* Patent records: Korea Intellectual Property Rights Information Service (KIPRIS), queries `"acoustic metamaterial" *AD=[20150101~20251231]` and `"active noise control" *AD=[20150101~20251231]`. The `office` column keeps the KIPRIS office code (for example US, EP, WO for PCT applications, JP, KR, CN, and TA for Taiwan).
* Research articles: Scopus, Web of Science, IEEE Xplore, and Google Scholar (2015 to 2025).
* Speech: MS-SNSD, `clean_test` folder (MIT License), https://github.com/microsoft/MS-SNSD, commit `fe61c4b`.
* Urban sound: ESC-50 (CC BY-NC 3.0), https://github.com/karolpiczak/ESC-50, commit `33c8ce9`.

The repository holds the records that passed screening. The search and screening counts shown in Figure 1 come from the author's search records, which are not included. The audio is downloaded by the notebook and is not stored in this repository. Full texts and abstracts of the research articles are not shared because of publisher copyright.

The code is released under the MIT License (`LICENSE`). The coding sheets and documentation are released under CC BY 4.0. Patent titles and abstracts in `patents_included.csv` come from KIPRIS and remain subject to its terms of use.
