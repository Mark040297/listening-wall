# Coding procedure

This note explains how the corpus was coded, so that anyone can judge and repeat the procedure.

## Coders

* **Coder 1** is the author, Mark Anthony S. Arcayan. The author's codes are in `data/corpus/coder1_articles.csv` and `data/corpus/coder1_patents.csv`. Labels outside the codebook lists and one column slip were cleaned with fixed rules before publication; `data/corpus/coder1_cleaning_log.csv` lists every changed cell with its original value and the rule applied (see the codebook).
* **Coder 2** is an AI-assisted coder: a large language model (Claude, Anthropic) that read each record and applied the written codebook (`docs/codebook.md`) under the author's supervision. Its codes are in `data/corpus/coder2_articles.csv` and `data/corpus/coder2_patents.csv`. Every row has a short note that states the reason for the codes.

Coder 2 never saw the codes of coder 1 while coding. The comparison was run only after each round was complete.

## What coder 2 read

* **Articles.** For each article, coder 2 read the title, abstract, and source, plus short passages from the full text that a keyword search selected for each variable (network, classification, AI, processing domain, setting, continuous operation). When a decision was unclear, coder 2 searched the full text for further passages before coding. Reference lists were removed from the search.
* **Patents.** Coder 2 read the title and abstract of the search record (`data/corpus/patents_included.csv`). This matches what coder 1 used.

## Rounds

1. **Pilot round.** Fifteen articles (RA1, RA2, RA3 and twelve drawn at random with a fixed seed) and fifteen patents were coded blind with codebook version 1 (`coder2_pilot_v1_*.csv`). The comparison with coder 1 showed where the rules were unclear.
2. **Codebook version 2.** Seven rules were stated more precisely. No rule was changed to copy a value of coder 1; each change makes a judgment rule explicit. The rules are listed at the end of `docs/codebook.md`.
3. **Main round.** The remaining 245 articles and 377 patents were coded blind with version 2. Conventions that came up for cases not covered by version 2 are listed in the codebook with the records they first applied to.
4. **Pilot recode.** The pilot records were recoded with version 2 for completeness. Because this step was not blind, the pilot records are excluded from the reliability estimates.

## Speech classification of patents (coder 1)

Coder 1 did not code speech classification for patents in the main round. It was added afterwards, when the results of coder 2 were already known. Speech classification is part of sound classification, so the 337 patents that coder 1 coded as having no sound classification are no. Coder 1 judged the other 55 patents (sound classification yes or unclear) from the title and abstract, using the codebook rule. The codes are in the column `SPEECH_CLASSIFICATION` of `data/corpus/coder1_patents.csv`. The columns `SPEECH_CLASSIFICATION_BASIS` and `SPEECH_CLASSIFICATION_NOTE` give the basis of each code and the note of coder 1. Because this coding was not blind, speech classification of patents is not used in the reliability estimates.

## Reliability

Reliability is measured on the main round only. The one article that coder 1 could not open (RA33) is left out of the comparison, so the main round compares 244 articles and 377 patents. For each binary indicator the notebook reports percent agreement, Cohen's kappa with a bootstrap 95% confidence interval, and Gwet's AC1. The codes were **not** revised to raise agreement. The disagreement log (`tables/disagreement_log.csv`, written by the notebook) lists every disagreement with coder 2's note and an empty `adjudication` column for a later consensus step.

## Corpus

The coding starts from the records that passed screening: 260 articles (`data/corpus/articles_included.csv`) and 392 patents (`data/corpus/patents_included.csv`). Both coders coded every one of these records. The search and screening counts (Figure 1 of the paper) come from the author's search records, which are not part of this repository.

## Why an AI-assisted coder

Peer-reviewed studies show that large language models can apply a codebook to text at a level close to trained human coders when their output is checked against human coding:

* Gilardi, F., Alizadeh, M., & Kubli, M. (2023). ChatGPT outperforms crowd workers for text-annotation tasks. *PNAS, 120*(30), e2305016120. https://doi.org/10.1073/pnas.2305016120
* Khraisha, Q., Put, S., Kappenberg, J., Warraitch, A., & Hadfield, K. (2024). Can large language models replace humans in systematic reviews? *Research Synthesis Methods, 15*(4), 616–626. https://doi.org/10.1002/jrsm.1715
* Tai, R. H., et al. (2024). An examination of the use of large language models to aid analysis of textual data. *International Journal of Qualitative Methods, 23*. https://doi.org/10.1177/16094069241231168
* Bijker, R., Merkouris, S. S., Dowling, N. A., & Rodda, S. N. (2024). ChatGPT for automated qualitative research: Content analysis. *Journal of Medical Internet Research, 26*, e59050. https://doi.org/10.2196/59050

The paper follows the condition these studies set: the AI codes are compared with a human coder, the agreement is reported as obtained, and both codings are published.
