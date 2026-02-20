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
1. Download archive provided by authors of original work at this [link](https://drive.google.com/file/d/1L40DnK4N9_iR0tXtGLWpXW6QfGcoUZVI/view) and extract it to get original code. There are two directories, but only directory *SMORL* is relevant for our purposes
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

Extracted files contain full rc15 and RetailRocket datasets in div4rec/ directory. However, this directory contains also files produced by original pre-processing procedures. We recommend to clean subdirectories in /div4rec to obtain following structure:

```text
div4rec/
├── rc15_data
│   ├── data_statis.df                  # basic dataset statistics
│   ├── yoochoose-buys.dat              # original rc15 dataset file
│   └── yoochoose-clicks.dat            # original rc15 dataset file
├── rc15_models
│   └── gru_embedding.pt                # gru embeddings
├── rc15_results
├── retail_rocket_data
│   ├── data_statis.df                  # basic dataset statistics
│   └── events.csv                      # original RetailRocket dataset file
├── retail_rocket_models
│   └── gru_embedding.pt                # gru embeddings
└── retail_rocket_results
```

To process rc15 dataset, execute scripts in following order:
1. sample_data_rc15.py
2. merge_and_sort_rc15.py
3. split_data.py (uncomment rc15 and comment RetailRocket lines)
4. nov_items_rewards.py (uncomment rc15 and comment RetailRocket lines)
5. replay_buffer_rc15.py

And to process Retail Rocket dataset:
1. preprocess_retail_rocket.py
2. split_data.py (comment rc15 and uncomment RetailRocket lines)
3. nov_items_rewards.py (comment rc15 and uncomment RetailRocket lines)
4. replay_buffer_retail_rocket.py

As a result, you should obtain following files:
```text
div4rec/                                div4rec/   
└── rc15_data                           └── retail_rocket_data
    ├── binary_nov_reward.csv               ├── binary_nov_reward.csv
    ├── data_statis.df                      ├── data_statis.df
    ├── less_popular_items.pkl              ├── events.csv
    ├── replay_buffer.df                    ├── less_popular_items.pkl
    ├── sampled_clicks.df                   ├── replay_buffer.df
    ├── sampled_sessions.csv                ├── sampled_test.df
    ├── sampled_sessions.df                 ├── sampled_train.df
    ├── sampled_test.df                     ├── sampled_val.df
    ├── sampled_train.df                    ├── sorted_events.csv
    ├── sampled_val.df                      └── sorted_events.df
    ├── yoochoose-buys.dat
    └── yoochoose-clicks.dat
```

## How to execute experiments

Please find files ```Caser.py```, ```CaserSMORL.py```, ```NextItNet.py```, ```NextItNetSMORL.py```, ```SASRec.py```, ```SASRecSMORL.py```, ```GRU.py``` and ```GRUSMORL.py``` in src/ directory. You can run experiments by executing these files. Note, however, that it is necessary to modify cetrain parameters in the Args class, as we keep parameters hardcoded. Mainly:

- `dataset` - indicates whether "rc15" or "retail_rocket" dataset should be used
- `arfix`   - indicates whether modified code for accuracy reward should (True) or should not (False) be used
- `smorl_weights_set` - defines set of weight vectors that are considered
- `smorl_loss_mults` - defines set of smorl loss weights that are considered

If `smorl_loss_mults` and `smorl_weights_set` are used without modification, experiments for all combinations of $w$ and $\alpha$ will be executed.

