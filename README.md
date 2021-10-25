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

This report records the attempts and models that were tried for a cross-subject cross-age group 6 class sleep staging task as a part of the BEETL-AI NeurIPS Hackathon. 

Point to be noted is that the final model and the predictions of which were submitted for the final test dataset was a model with no Transfer Learning Techniques applied, which performed better than those on which TL techniques were attempted. The TL techniques were flawed in the training due to overfitting over too many epochs. Rather, the fraction below (1) could’ve been used as the upper threshold, past which overfitting could be considered likely.

Upper threshold = (#training epochs) * (#samples in target group/#samples in the training group)  (1)

Despite these, the result to be noted from this attempt is that the Attention Sleep model performed well despite no Transfer Learning, suggesting good generalization ability for cross-subject cross-age group Sleep Staging. Since there is still information to be gained from failed techniques, this report gives a review of all the techniques tried. 

Literature Review for the top techniques tested on the Physionet Sleep Dataset was done primarily through the corresponding [Papers with Code Site](https://paperswithcode.com/dataset/sleep-edf). Sequence-to-Sequence Deep Learning Approaches were rejected due to the formulation of the competition details and the lack of sureity of the presence of temporal unshuffled data in the test datasets.

Initially for a baseline for the performance, a Random Forest Classifier was trained on features extracted using the mne-features library. Then a Multi-Layer Perceptron was trained on the same features. Then the following Deep Learning techniques were attempted directly on the temporal data after z-scoring for each dataset -

## Models Tried - 

1. Self-Supervised Learning (Relative Positioning task)
Corresponding [Paper](https://arxiv.org/abs/2007.16104) and a [code example](https://braindecode.org/auto_examples/plot_relative_positioning.html) (from the Braindecode library).

    a. Pre-text Task - RP is a simple SSL task, in which a neural network is trained to predict whether two randomly sampled EEG windows are close or far apart in time.
    
    b. A CNN model in a Siamese Architecture (Contrastive Net) learns temporally distinguishing features through the pre-text task.
    
    c. This CNN model is then used as a feature extractor on the sleep EEG data, and a Logistic Regression model does the classification using the features as input.
    
    d. After doing SSL on the Phase 1 Target data, the classification performance was not good and hence this model was discontinued after that and not used on the Phase 2 data.

2. Blanco 2020 CNN-based Model - [Paper](https://arxiv.org/ftp/arxiv/papers/2103/2103.16215.pdf)
    a. Data sampled to be balanced epoch-wise during training using [Imbalanced Dataset Sampler](https://github.com/ufoym/imbalanced-dataset-sampler)
    
    b. Tried Transfer Learning by - 
    
        i. Freezing all the layers except the last fully connected layer and fine-tuning only that.
        
        ii. Fine-tuning the entire network.

3. Attention Sleep Model – [Papers with Code Link](https://paperswithcode.com/paper/an-attention-based-deep-learning-approach-for)

    a.	The model is base trained on the group 1 training data.
    
    b.	Transfer Learning Techniques like fine-tuning the model on the target data and freezing all the layers except the last fully connected layer and fine-tuning only that.
    
    c.	The models attempted on the leaderboard however overfitted as mentioned in the introduction and the best performing model was directly the base-trained model.


## Tools

Primary Libraries - Pytorch, Skorch(wrapper on PyTorch to resemble to scikit-learn API) and Braindecode.
[Imbalanced Dataset Sampler](https://github.com/ufoym/imbalanced-dataset-sampler)

[Weights and Biases](https://wandb.ai/) was used to log the model and training - This is optional and was used for convinience to view the results automatically compiled and for comparisons.

Training was done through Google Colab Pro with the GPU varying as per allocation.

## Results 
(TODO)
(Different models, Hyperparameters, Training, Validation accuracy and Leaderboard performance)

Performance = balanced accuracy %


# Links -
[Introduction to BEETL-AI Hackathon](https://beetl.ai/introduction)

[Codalab Competition Site](https://competitions.codalab.org/competitions/33427)

[Starter Kits/Guides](https://github.com/XiaoxiWei/NeurIPS_BEETL)
