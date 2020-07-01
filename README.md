## Overview
This repo provides the source code for our work on "Identification of common inflammatory macrophage phenotypes in COVID-19 using integrated transcriptional single-cell reference map of inflamed tissues in 5 disease".
Using an integrative strategy, we built a reference by meta-analyzing > 300,000 immune cells from COVID-19 and 5 inflammatory diseases including rheumatoid arthritis (RA), ulcerative colitis (UC), Crohn’s disease (CD), lupus, and interstitial lung disease, which is effective to investigate connections between other inflammatory diseases with COVID-19.


## Structure

The files in the repo are organized as follows:

    .
    ├── code
    |── data

`data/` has metadata and R files with processed data ready for analysis.

`code/` has code for our integrative pipeline, analysis, and figures:

+ Linear model to model HTO single-cell macrophage data for different conditions: `code/mac_stimuli_linear_model.ipynb`

Send us an email if you have any questions!
