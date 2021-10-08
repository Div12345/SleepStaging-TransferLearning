# Sleep Staging - Transfer Learning
Cross-Subject across Age Groups Transfer Learning techniques applied on the Physionet Sleep dataset for the NeurIPS BEETL-AI Hackathon 2021 - Task 1.

"The task is an essential use case for the development of ready-to-use medical diagnostics developed on a standard, large user base that has to be then transferred to many different clinically relevant subpopulations for which respectively only a few subjects worth of data can be collected."

# The Data and the Challenge
![image](https://user-images.githubusercontent.com/47829318/136428698-bac43191-e429-46c3-b2b9-cecae0cb5794.png)
"For the Physionet sleep data set (Sleep Cassette Study, around 150 sessions), we will provide (train) subjects aged from 25-64 with full labels as resources and (target 1) 5 subjects aged from 65 to 79 as example subject of this age group; we will test the performance of the algorithm on more (test 1) subjects aged from 65 to 79. Similarly, we will provide (target 2) 5 subjects aged from 80 to 95 as example subjects of this age group, we will test the performance of the algorithm on more (test 2) subjects aged from 80 to 95."

The target data is provided for Transfer Learning and Domain Transfer techniques for adapting the algorithm for better prediction on the test data.

6 class classification task - Wake, REM, S1, S2, S3, S4.
The data from the classes is also very imbalanced.

# This Repository -
Literature Review for the top techniques tested on the Physionet Sleep Dataset was done primarily through the corresponding [Papers with Code Site](https://paperswithcode.com/dataset/sleep-edf)

Sequence-to-Sequence Deep Learning Approaches were rejected due to the formulation of the competition details and the lack of sureity of the presence of temporal unshuffled data in the test datasets

## Models Tried - 
1. Self Supervised Learning through Relative Positioning Pre-Text Task - Based on this [Paper](https://arxiv.org/abs/2007.16104) and this [code example](https://braindecode.org/auto_examples/plot_relative_positioning.html#) from Braindecode - A library focussed on Deep Learning approaches to be applied to EEG data.
2. Transfer Learning through the [AttnSleep Model](https://paperswithcode.com/paper/an-attention-based-deep-learning-approach-for)

## Tools and Techniques

Primary Libraries - Pytorch, Skorch(wrapper on PyTorch to resemble to scikit-learn API) and Braindecode.

[Weights and Biases](https://wandb.ai/) was used to log the model and training - This is optional and was used for convinience to view the results automatically compiled and for comparisons.

Training was done through Google Colab Pro with the GPU varying as per allocation.

# Links -
[Introduction to BEETL-AI Hackathon](https://beetl.ai/introduction)

[Codalab Competition Site](https://competitions.codalab.org/competitions/33427)

[Starter Kits/Guides](https://github.com/XiaoxiWei/NeurIPS_BEETL)
