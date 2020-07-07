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

RAF_DB contains 12271 colured images of westren facial expressions 

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

| Classifier | Source Domain Training Accuracy | Source Domain Testing Accuracy |
| :--: | :--: | :--: |
| VGG16 | 94.8 | 79.45 |
| ResNET18 | 92.3 | 80.17 |

In our experimentation, we first evaluated our classifiers
(VGG16 and ResNET18) on target domain without doing
any kind of domain adaptation. The baseline results for the
classifiers used are provided in following table

| Classifier | Target Dataset 1 Accuracy (Unseen) | Target Dataset 2 Accuracy (Unseen) |
| :--: | :--: | :--: |
| VGG16 | 52.00 | 37.51 |
| ResNET18 | 50.75 | 33.51 |

Then in our next experiment, we fine-tuned our classifiers directly on target domain to get an upper bound of
accuracies on target domain for each classifier. These accuracies are given below

| Classifier | Target Dataset 1 Accuracy (Used in Fine-tuning) | Target Dataset 2 Accuracy (Unseen) |
| :--: | :--: | :--: |
| VGG16 | 92.23 | 42.75 |
| ResNET18 | 96.47 | 43.03 |

We used three different approaches for domain adaptation purpose.
1. Unsupervised Domain Adaptation using WGAN — WGAN results were not useable. So this approach was discontinued. This approach was presented in [1].
2. Semi-supervised Domain Adaptation using CycleGAN — Approach based on the [2].
3. Feature Space Unsupervised Domain Adaptation —
Approach based on the [3].

The first two approaches basically used Input Space domain adaptation. The third approach as the name suggests,
used Feature Space domain adaptation. In input space domain adaptation we basically use GAN generated samples
to fine-tune our pre-trained classifier on source domain so
that it can adapt to target domain. WGAN in the first approach basically generates new target domain like samples
from random noise input while CycleGAN translates source
samples to target domain like samples. WGAN results were
not satisfactory even though we tried 3 different architectures for it and trained for 2 weeks. Thus this approach
was discontinued. On the other hand, CycleGAN produced
fairly good results and fine-tuning was performed for its
translated samples. In feature space, we basically try to
make feature extracted by our model from input images independent of any domain information. We do this using a
domain classifier network trained in parallel to our classifier and loss generated by this network is fed to the model
as well so that it becomes invariant to any domain information. Feature space domain adaptation techniques don’t
require any GAN to help out in its purpose and thus very
less expensive than input space domain adaptation. It took
us 4 days to train classifiers using third approach.
WGAN generated samples for all three architectures
used are given in fig 3. As it can be that results for WGAN
are not satisfactory and usable. Henceforth, we discontinued this approach. Training specifications for WGAN models are given in table 4.
The next series of experiments are for second approach
“Semi-supervised Domain Adaptation using CycleGAN”.

| Specifications | WGAN Arch. 1 | WGAN Arch. 2 | WGAN Arch. 3 | 
| :--: | :--: | :--: | :--: |
| Model Type | Linear | Linear | Convolutional |
| Training Epochs | 10K | 1K | 7.5K |
| Training Time | 7 Days | 3 Days | 7 Days | 


The results for some of the CycleGAN translated images are
given in fig 4. We trained 7 different CycleGAN for each
emotion class so that CycleGAN don’t mess up the emotion
of the source image while translation. It took us 2 weeks to
train these 7 CycleGAN and translate image through them.
Some of the input and translated images are shown in Fig 4. As we can see that CycleGAN mostly tries to adapt color
features from target domain to source domain input. In order to get better results from CycleGAN, it can be trained
more so that it can capture more feature information from
target domain and map them to source domain input images.
Using these translated Images, we fine-tuned our classifiers and table 5 provides the accuracy score on both target
datasets.
The final series of experimentation is for approach “Feature Space Unsupervised Domain Adaptation”. Here we retrained both the classifier with an additional domain classifier network in them. This domain classifier network help
in making the features used in classifier independent of any
domain information. Table 6 are the results for both classifiers on source and both target datasets.
For better understanding of performance of different approaches, confusion matrices for each experiment can be
found in figures section. In fig 5, confusion matrices for baseline results for each classifier on both target dataset
can be found. In fig 6, confusion matrices for classifiers
fine-tuned on target dataset directly can be found. In fig 7, confusion matrices for classifiers fine-tuned on CycleGAN translated samples can be found. In fig 8, confusion
matrices for classifiers trained using feature space domain
adaptation approach can be found.

# Conclusion

By using “Semi-supervised Domain Adaptation using
CycleGAN”, we are able to produce better results than baseline results. For “feature Space unsupervised domain adaptation”, the accuracy got better for one target dataset and
got a little worse for other dataset. CycleGAN based approach can make a significant change in results if we train
CycleGANs more. Same goes for Feature space based approach. There was an imbalance of classes in source dataset
and target datasets which limited the performance of the approaches used. Along this, there several age groups present
in source dataset as compared to target dataset. If these
things are also dealt carefully, then we can achieve way better results than reported.

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
