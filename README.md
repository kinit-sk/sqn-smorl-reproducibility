# Supplementary material for the paper:
# _Are We Proving Progress or Repeating Mistakes? A Case Study in Multi-stakeholder Recommender Systems_

This repository contains additional supplementary materials for the paper _Are We Proving Progress or Repeating Mistakes? A Case Study in Multi-stakeholder Recommender Systems_. It provides sufficient artifacts and instructions to reproduce our experiments and analysis organized to following directories:

 - `Patches/`   - patch files that transform the original implementation into the modified version used in our experiments
 - `Results/`   - files with our experimental results
 - `Plots/`     - complete set of plots representing our experiments


Our experiments are based on modification of [original code](https://github.com/sisinflab/MORS_reproducibility) by Vincenzo Paparella, Vito Walter Anelli, Ludovico Boratto, and Tommaso Di Noia for their [paper](https://dl.acm.org/doi/10.1145/3604915.3609493) _Reproducibility of Multi-Objective Reinforcement Learning Recommendation: Interplay between Effectiveness and Beyond-Accuracy Perspectives_. 

> **_NOTE:_** As the original source code is protected by copyright, we do not redistribute it. Instead, we provide patch files and instructions for applying them to the original implementation

## How to obtain executable code

To obtain source codes and datasets necessary to reproduce our results:
1. Download archive provided by authors of original work at this [link](https://drive.google.com/file/d/1L40DnK4N9_iR0tXtGLWpXW6QfGcoUZVI/view) and extract it to get original code.
2. Enter SMORL directory
   ```bash
   cd /path/to/extracted/files/SMORL```
3. Download and apply [patches](Patches) 
   ```bash
   for p in /path/to/Patches/*.patch; do
       git apply --verbose "$p";
   done
   ```

## How to pre-process datasets

Extracted files contain full rc15 and RetailRocket datasets in /div4rec/rc15_data and/div4rec/retail_rocket_data directories, respectivelly. However, these directories contain also files produced by original pre-processing procedures. 
