# Introduction

Facial expression analysis is a domain of interest in deep
and transfer learning. The way in which human beings express their emotions has always been a topic of interest in
psychological study. External factors have always proven to
play a major role as different groups of people show different reaction to the same stimuli, and the way of their emotional expression sets them apart from any other group of
interest. The common factors in this change of expressions
are observed as gender, cultural influences, age, and the
environment. Expression of the commonly observed emotions is specific to the individuals, based on their personality
traits. If the training data is an unbiased sample of an underlying distribution, then the learned classification function will make accurate predictions for new samples. However,
if the training data is not an unbiased sample, then there will
be differences between how the training data is distributed
and how the test data is distributed. This becomes the major
challenge in domain adaptation.
In this problem, our main focus is the facial expression
recognition, as the reaction to a stimulus is first observed
through face. As cultural factors influence the display of
emotions, and we are dealing with the Indo-Pak ethnicity,
we show how an ethnicity-specific classifier is built using
the target domain data that is unlabeled. The assumptions
made by our proposed method will not be based on specific features used for emotional representation, so the proposed solution can be applied to a different kind of data also.
We propose to use Cycle-GAN for the purpose of mapping
source domain to target domain, and conduct the comparative analysis with results of conventional GAN model. Furthermore, we applied feature-space domain adaptation to
our problem, which resulted in significant improvements.

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/SystemDiagram.jpg" alt="System Diagram" width="850" height="550">

# Dataset

## Source Dataset 

Real-world Affective Faces Database (RAF_DB) contains 15338 colured images of westren facial expressions, we are using only seven classes although RAF_DB contains more than seven classes and around 30K images.

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Source%20Dataset%20Stat.JPG" alt="Source Dataset">

## Target Dataset

We have collected around 4000 colured Pakistani facial expression images

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Target%20Dataset.JPG" alt="Target Dataset">

# Experiments and Results

We performed a series of experiments. We have used
two target datasets in our experimentation. The first dataset
is used in domain adaptation process and second dataset is
kept unseen in all the ways for testing purposes. This was
done to ensure model performance consistency on target domain. We used two classifiers in our experimentation. One
is VGG16 pre-trained on ImageNet Dataset and second is
ResNET18 pre-trained on ImageNet Dataset. These classifiers were trained on source domain and their accuracies on
source domain are below.

| *Classifier | *Source Domain Training Accuracy* | *Source Domain Testing Accuracy* |
| :--: | :--: | :--: |
| VGG16 | 94.8 | 79.45 |
| ResNET18 | 92.3 | 80.17 |

In our experimentation, we first evaluated our classifiers
(VGG16 and ResNET18) on target domain without doing
any kind of domain adaptation. The baseline results for the
classifiers used are provided in following table

| *Classifier* | *Target Dataset 1 Accuracy (Unseen)* | *Target Dataset 2 Accuracy (Unseen)* |
| :--: | :--: | :--: |
| VGG16 | 52.00 | 37.51 |
| ResNET18 | 50.75 | 33.51 |

Then in our next experiment, we fine-tuned our classifiers directly on target domain to get an upper bound of
accuracies on target domain for each classifier. These accuracies are given below

| *Classifier* | *Target Dataset 1 Accuracy (Used in Fine-tuning)* | *Target Dataset 2 Accuracy (Unseen)* |
| :--: | :--: | :--: |
| VGG16 | 92.23 | 42.75 |
| ResNET18 | 96.47 | 43.03 |

We used three different approaches for domain adaptation purpose.
1. Unsupervised Domain Adaptation using WGAN — WGAN results were not useable. So this approach was discontinued.
2. Semi-supervised Domain Adaptation using CycleGAN.
3. Feature Space Unsupervised Domain Adaptation.

| *Specifications* | *WGAN Arch. 1* | *WGAN Arch. 2* | *WGAN Arch. 3* | 
| :--: | :--: | :--: | :--: |
| Model Type | Linear | Linear | Convolutional |
| Training Epochs | 10K | 1K | 7.5K |
| Training Time | 7 Days | 3 Days | 7 Days | 

Using CycleGAN translated images, we fine-tuned our classifiers and accuracy score on both target datasets are below.

| *Classifier* | *Target Dataset 1 Accuracy (Used in Fine-tuning)* | *Target Dataset 2 Accuracy (Unseen)* |
| :--: | :--: | :--: |
| VGG16 | 50.92 | 37.51 |
| ResNET18 | 50.75 | 33.51 |

Feature Space Unsupervised Domain Adaptation. We retrained both the classifier with an additional domain classifier network in them. This domain classifier network help in making the features used in classifier independent of any domain information.

| *Classifier* | *Target Dataset 1 Accuracy (Used in Fine-tuning)* | *Target Dataset 2 Accuracy (Unseen)* |
| :--: | :--: | :--: |
| VGG16 | 51.36 | 37.37 |
| ResNET18 | 46.72 | 32.41 |


## Baseline Results

Confusion Matrices for baseline results. (a) VGG16 results on Target Dataset 1, (b) VGG16 results on Target Dataset 2, (c) ResNET18 results on Target Dataset 1, (d) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Confusion%20Matrices%20for%20baseline%20results.JPG" alt="Results">

## Fine-tuned on Target Dataset

Classifiers fine-tuned on target dataset directly. (a) VGG16 results on Target Dataset 1, (b) VGG16 results on Target Dataset 2, (c) ResNET18 results on Target Dataset 1, (d) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Classifiers%20fine-tuned%20on%20target%20dataset%20directly.JPG" alt="Results">

## Trained using Feature Space Domain Adaptation

Classifiers trained using feature space domain adaptation approach. (a) VGG16 results on Target Dataset 1, (b) VGG16 results on Target Dataset 2t, (c) ResNET18 results on Target Dataset 1, (d) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Classifiers%20trained%20using%20feature%20space%20domain%20adaptation%20approach.JPG" alt="Results">

# References

1. et al Bousmalis, Konstantinos. Unsupervised pixel-level domain adaptation with generative adversarial networks, 2017. Proceedings of the IEEE conference on computer vision and pattern recognition.
2. et al Ganin, Yaroslav. Domain-adversarial training of neural networks, 2016. The Journal of Machine Learning Research 17.1 (2016): 2096-2030.
3. Xiangjun Wang Wang, Xiaoqing and Yubo Ni. Unsupervised domain adaptation for facial expression recognition using generative adversarial networks, 2018. Computational intelligence and neuroscience.

# Contributers

- Jawad Tariq [MSDS19038@itu.edu.pk]
- Muhammad Sohaib Khalid [MSDS19096@itu.edu.pk]
- Asif Ejaz [MSDS19010@itu.edu.pk]
- Amna Shahbaz [MSDS19060@ity.edu.pk]
- Muhammad Taimur Adil [MSDS19040@itu.edu.pk]
