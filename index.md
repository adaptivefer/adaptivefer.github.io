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

<figure class="image"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/SystemDiagram.jpg" alt="System Diagram" width="850" height="550"  style="display: block;  margin-left: auto;  margin-right: auto;"><figcaption>(a) Input Space Domain Adaptation, (b) Feature Space Domain Adaptation (Followed from Domain-Adversarial Training of Neural Networks published in Journal of Machine Learning Research 17 (2016)</figcaption></figure>

# Dataset

Used RAF_DB as sourced dataset and Self collected Pakistani facial images as target dataset

<figure class="image"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/RAF_Pak.jpg" alt="System Diagram" style="display: block;  margin-left: auto;  margin-right: auto;"><figcaption></figcaption></figure>

## Source Dataset 

Real-world Affective Faces Database (RAF_DB) contains 15338 coloured images of westren facial expressions, we are using only seven classes although RAF_DB contains more than seven classes and around 30K images.

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Source%20Dataset%20Stat%20upd.JPG" alt="Source Dataset" style="width:90%;display: block;  margin-left: auto;  margin-right: auto;">

## Target Dataset

We have collected around 4000 coloured Pakistani facial expression images

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Target%20Dataset%20Stat%20upd.JPG" alt="Target Dataset" style="width:90%;display: block;  margin-left: auto;  margin-right: auto;">

# Experiments and Results

1. Unsupervised Domain Adaptation using WGAN — WGAN results were not useable. So this approach was discontinued.
2. Semi-supervised Domain Adaptation using CycleGAN.
3. Feature Space Unsupervised Domain Adaptation.

We have used two target datasets in our experimentation. The first dataset
is used in domain adaptation process and second dataset is
kept unseen in all the ways for testing purposes. This was
done to ensure model performance consistency on target domain. We used two classifiers in our experimentation. One
is VGG16 pre-trained on ImageNet Dataset and second is
ResNET18 pre-trained on ImageNet Dataset. These classifiers were trained on source domain and their accuracies on
source domain are below.

## WGAN

### Architecture-1 : Source dataset accuracy results

<table class="table table-bordered">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Classifier</th>
      <th scope="col">Source Domain Training Accuracy</th>
      <th scope="col">Source Domain Testing Accuracy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VGG16</td>
      <td>94.8</td>
      <td>79.45</td>
    </tr>
    <tr>
      <td>ResNET18</td>
      <td>92.3</td>
      <td>80.17</td>
    </tr>
  </tbody>
</table>

In our experimentation, we first evaluated our classifiers
(VGG16 and ResNET18) on target domain without doing
any kind of domain adaptation. The baseline results for the
classifiers used are provided in following table

### Architecture-2 : Baseline results

we first evaluated our classifiers (VGG16 and ResNET18) on target domain without doing any kind of domain adaptation.

<table class="table table-bordered">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Classifier</th>
      <th scope="col">Target Dataset 1 Accuracy (Unseen)</th>
      <th scope="col">Target Dataset 2 Accuracy (Unseen)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VGG16</td>
      <td>50.92</td>
      <td>37.51</td>
    </tr>
    <tr>
      <td>ResNET18</td>
      <td>50.75</td>
      <td>33.51</td>
    </tr>
  </tbody>
</table>

### Architecture-3 : Direct fine-tuning on Target Dataset Accuracy

Then in our next experiment, we fine-tuned our classifiers directly on target domain to get an upper bound of
accuracies on target domain for each classifier.


<table class="table table-bordered">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Classifier</th>
      <th scope="col">Target Dataset 1 Accuracy (Used in Fine-tuning)</th>
      <th scope="col">Target Dataset 2 Accuracy (Unseen)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VGG16</td>
      <td>92.23</td>
      <td>42.75</td>
    </tr>
    <tr>
      <td>ResNET18</td>
      <td>96.47</td>
      <td>43.03</td>
    </tr>
  </tbody>
</table>

### WGAN Results

<figure class="image"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/WGAN%20Results.jpg" alt="System Diagram"  style="display: block;  margin-left: auto;  margin-right: auto;"><figcaption></figcaption></figure>

### Training Specifications of WGAN Models

<table class="table table-bordered">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Specifications</th>
      <th scope="col">WGAN Arch. 1</th>
      <th scope="col">WGAN Arch. 2</th>
      <th scope="col">WGAN Arch. 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Model Type</td>
      <td>Linear</td>
      <td>Linear</td>
      <td>Convolutional</td>
    </tr>
    <tr>
      <td>Training
Epochs</td>
      <td>10K</td>
      <td>1K</td>
      <td>7.5K</td>
    </tr>
    <tr>
      <td>Training Time </td>
      <td>7 Days</td>
      <td>3 Days</td>
      <td>7 Days</td>
    </tr>
  </tbody>
</table>

## CycleGAN

### Fine Tune CycleGAN

Using CycleGAN translated images, we fine-tuned our classifiers and accuracy score on both target datasets are below.

<table class="table table-bordered">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Classifier</th>
      <th scope="col">Target Dataset 1
Accuracy (Used
in Fine-tuning)
</th>
      <th scope="col">Target Dataset 2
Accuracy (Unseen)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ResNET18</td>
      <td>48.13</td>
      <td>33.42</td>
    </tr>
  </tbody>
</table>

Fine-Tuned CycleGAN models are available <a href="https://drive.google.com/drive/folders/1YQMcbfqQBPzH-AnjzQUshtOQNGcIlIF_?usp=sharing" target="_blank">here</a>.

### Feature Space Unsupervised Domain Adaptation CycleGAN
We retrained both the classifier with an additional domain classifier network in them. This domain classifier network help in making the features used in classifier independent of any domain information.


<table class="table table-bordered">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Classifier</th>
      <th scope="col">Target Dataset 1 Accuracy (Used in Fine-tuning)</th>
      <th scope="col">Target Dataset 2 Accuracy (Unseen)</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VGG16</td>
      <td>51.36</td>
      <td>37.37</td>
    </tr>
    <tr>
      <td>ResNET18</td>
      <td>46.72</td>
      <td>32.41</td>
    </tr>
  </tbody>
</table>

## CycleGAN Translated Results

<figure class="image"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/CycleGAN%20translated%20images.jpg" alt="System Diagram"  style="display: block;  margin-left: auto;  margin-right: auto;"><figcaption></figcaption></figure>


## Baseline Results

Confusion Matrices for baseline results. (a) VGG16 results on Target Dataset 1, (b) VGG16 results on Target Dataset 2, (c) ResNET18 results on Target Dataset 1, (d) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Confusion%20Matrices%20for%20baseline%20results.JPG" alt="Results" style="display: block;  margin-left: auto;  margin-right: auto;">

## Fine-tuned on Target Dataset

Classifiers fine-tuned on target dataset directly. (a) VGG16 results on Target Dataset 1, (b) VGG16 results on Target Dataset 2, (c) ResNET18 results on Target Dataset 1, (d) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Classifiers%20fine-tuned%20on%20target%20dataset%20directly.JPG" alt="Results" style="display: block;  margin-left: auto;  margin-right: auto;">

## Trained using Feature Space Domain Adaptation

Classifiers trained using feature space domain adaptation approach. (a) VGG16 results on Target Dataset 1, (b) VGG16 results on Target Dataset 2t, (c) ResNET18 results on Target Dataset 1, (d) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/Classifiers%20trained%20using%20feature%20space%20domain%20adaptation%20approach.JPG" alt="Results" style="display: block;  margin-left: auto;  margin-right: auto;">

## Fine-tuned on CycleGAN translated samples

Classifiers fine-tuned on CycleGAN translated samples. (a) ResNET18 results on Target Dataset 1, (b) ResNET18 results on Target Dataset 2

<img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/CycleGAN%20Confusion%20Matrix.JPG" alt="Results" style="display: block;  margin-left: auto;  margin-right: auto;">

# Contributors

<table style="width:100%; border-collapse: collapse; border: 0px;">
   <tr style="border-collapse: collapse; border: 0px;">
      <td style="border-collapse: collapse; border: 0px;text-align: left;"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/img_avatar.png" alt="Avatar" style="vertical-align: middle;  width: 50px;  height: 50px;  border-radius: 50%;">
         Jawad Tariq
         <a href="mailto:msds19038@itu.edu.pk">MSDS19038@itu.edu.pk</a>
      </td>
      <td style="border-collapse: collapse; border: 0px;text-align: left;"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/img_avatar.png" alt="Avatar" style="vertical-align: middle;  width: 50px;  height: 50px;  border-radius: 50%;">
         Muhammad Sohaib Khalid
         <a href="mailto:msds19096@itu.edu.pk">MSDS19096@itu.edu.pk</a>
      </td>
   </tr>
   <tr style="border-collapse: collapse; border: 0px;">
      <td style="border-collapse: collapse; border: 0px;text-align: left;"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/img_avatar2.png" alt="Avatar" style="vertical-align: middle;  width: 50px;  height: 50px;  border-radius: 50%;">
         Amna Shahbaz
         <a href="mailto:msds19060@ity.edu.pk">MSDS19060@ity.edu.pk</a>
      </td>
      <td style="border-collapse: collapse; border: 0px;text-align: left;"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/img_avatar.png" alt="Avatar" style="vertical-align: middle;  width: 50px;  height: 50px;  border-radius: 50%;">
         Asif Ejaz
         <a href="mailto:msds19010@itu.edu.pk">MSDS19010@itu.edu.pk</a>
      </td>
   </tr>
   <tr style="border-collapse: collapse; border: 0px;">
      <td style="border-collapse: collapse; border: 0px;text-align: left;"><img src="https://raw.githubusercontent.com/adaptivefer/adaptivefer.github.io/master/assets/images/img_avatar.png" alt="Avatar" style="vertical-align: middle;  width: 50px;  height: 50px;  border-radius: 50%;">
         Muhammad Taimur Adil
         <a href="mailto:msds19040@itu.edu.pk">MSDS19040@itu.edu.pk</a>
      </td>
   </tr>
</table>
