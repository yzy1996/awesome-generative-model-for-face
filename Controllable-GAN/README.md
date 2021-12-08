# <p align=center>`Controllable Generation`</p>

![](https://img.shields.io/badge/-WIP-green)

A collection of resources on Controllable Generation.

> Some key words: interpreting, latent space navigation, steerable, interpretable, semantics, manual annotation, meaningful directions, Semantic image editing.

*PS: this repo does **not** contains style transfer, I would tend to classify it as artistic creation (mix and interpolate features from different images).*

[toc]

## Introduction

Conventional generative models excel at generating random realistic samples with statistics resembling the training set. However, controllable and interactive matters rather than random. GANs do not provide an inherent way of comprehending or controlling the underlying generative factors. But some researches show that a well-trained GAN is able to encode different semantics inside the latent space. Therefore, a key problem of Generative Models is to gain explicit control of the synthesis process or results.

The goal is to generate or modify images satisfying our specific requirement. The requirement should be sementical meaningful interpretable and easy to distinguish without affecting other attributes (e.g. object pose,). The manipulation could be single or multi attributes of interest.

The first line proposes conditional GANs to generate with $p(z|y)$ or employ auxiliary classifiers to enforce the gan network generate desired results.

Another line is to utilize the latent space of a pretrained generator for image manipulation. In this line, we could also control and modify a given real image by inversing the image into latent code (**inversion**). The main idea behind this method is to disentangle the latent space. A common practice is to analyze and dissect GANs’ latent spaces, finding disentangled latent variables suitable for editing. The disentangled latent variables sometimes are interpretable directions $d$. Careful modifications of the latent embeddings then translate to desired changes in generated output.
$$
x = G(z_0) \rightarrow x' = G(z_0 + \alpha d)
$$
these directions should be better orthogonal do not interfere with each other, moving in these directions corresponds to 

These valid direction could be seen as some manifold of the latent space, meaningful subspaces corresponding to the human-understandable attributes.





:dart: **Summary**

We mainly focus on the *disentanglement in the latent space* of a generative model. We hope:

- disentangle in an unsupervised manner
- find more disentangled directions that do not interfere with each other
- provide continuous manipulation of multiple attributes simultaneously

One more thing is the interaction mode:

- provide segmentation mask to change specific area.



:eyes: **What can we edit/control?**

Meaningful human interpretable directions can refer to either domain-specific factors (e.g., facial expressions) or domain-agnostic factors (e.g., zoom scale).

Some examples including:

- change facial expressions in portraits
- change view-point or shapes and textures of cars
- interpolate between different images

some simple transformation (rotation, zooming)

[add some image]



:paperclip: **Futher Impact**

- browse through the concepts that the GAN has learned

- training a general model requires enormous computational resources, so interpret and extend the capabilities of existing GANs

- for artistic visualization, design, photo enhancement





## Methods Taxonomy



This is the summary of controllable GAN including;

- [training stage] conditional GAN mode 
- [test stage] modify a pre-trained GAN model
- [test stage] modify a latent code of a given image





- Conditional GANs and Auxiliary Classifier

  > different conditioning lead different outputs
  >
  > auxiliary attribute classifiers to guide synthesis 
  >
  > :speech_balloon: requires large labeled datasets. These methods are limited to image types for which large annotated datasets are available, like **portraits**. Limited editing control 

- 2.2 Analyze and dissect GANs’ latent spaces, finding disentangled latent variables suitable for editing

  > :speech_balloon: do not enable detailed editing and are often slow.
  >
  > used in real-time on different images and with different edits

- 2.3 change network weight

  > 



前两者can only discover researchers expectation directions. 需要想象力；后者能实现你所想不到



global semantics

local semantics



:pushpin: **Problem Statement**

a (<u>pretrained</u>) fixed GAN model consisting of a generator **G** and a discriminator **D**

latent vector $\boldsymbol{z} \in \mathbb{R}^m$ from a known distribution $P(\boldsymbol{z})$, and sample $N$ random vectors $\mathbb{Z} = \{\boldsymbol{z}^{(1)}, \dots, \boldsymbol{z}^{(N)}\}$

We want to discover K non-linear interpretable paths on the latent space 



an Autoencoder do assume two parametric models 1) $f: \mathcal{X} \rightarrow \mathcal{Z}$ and 2) $g: \mathcal{Z} \rightarrow \mathcal{X}$. 

we want to minimize the reconstruction loss $



The most straightforward way is to first generate a collection of image synthesis, then label these images regarding a target attribute, and finally find the latent separation boundary through supervised training.



In view of the annotation drawbacks of previous method, finding steerable directions of the latent space in an unsupervised manner is another direction, such as using PCA.



The common issue of the existing approaches is the limitation of global semantics, we would like to focus on some particular image region



current methods required 

- carefully designed loss functions

- introduction of additional attribute labels or features
- special architectures to train new models





### Tricks

[GLO](#GLO): 通常是假设 z 服从高斯分布，而这样导致点不太可能落在离球面 $\mathcal{S}(\sqrt{d}, d, 2)$ 太远的地方。又因为投影到球体上很容易且数值友好，因此会时刻让 z 映射到一个球体上。使用中，也会不使用 $\sqrt{d}$ 的球体，而是直接用单位球。



## Literature



### Survey

Representation learning: A review and new perspectives





### 1.1 Conditional GAN

click to see detailed notes

- [StarGAN: Unified Generative Adversarial Networks for Multi-Domain Image-to-Image Translation](https://arxiv.org/pdf/1711.09020.pdf)  
  Yunjey Choi, Minje Choi, Munyoung Kim, Jung-Woo Ha, Sunghun Kim, Jaegul Choo  
  [CVPR 2018] (Korea University)

- [MaskGAN: Towards Diverse and Interactive Facial Image Manipulation](https://arxiv.org/pdf/1907.11922.pdf)  
  *Cheng-Han Lee, Ziwei Liu, Lingyun Wu, Ping Luo*  
  **[`CVPR 2020`] (`SenseTime, CUHK`)**

- [Cascade EF-GAN: Progressive Facial Expression Editing with Local Focuses](https://arxiv.org/pdf/2003.05905.pdf)  
  *Rongliang Wu, Gongjie Zhang, Shijian Lu, Tao Chen*  
  **[`CVPR 2020`] (`NTU`)**

- [SEAN: Image Synthesis with Semantic Region-Adaptive Normalization](https://arxiv.org/pdf/1911.12861.pdf)  
  Peihao Zhu, Rameen Abdal, Yipeng Qin, Peter Wonka  
  [CVPR 2020]

- [Deep Generation of Face Images from Sketches](https://arxiv.org/pdf/2006.01047.pdf)  
  *Shu-Yu Chen, Wanchao Su, Lin Gao, Shihong Xia, Hongbo Fu*   
  **[`TOG 2020`] (`CAS, CityU`)**

- [Semantic Image Synthesis with Spatially-Adaptive Normalization](https://arxiv.org/pdf/1903.07291.pdf)  
  *Taesung Park, Ming-Yu Liu, Ting-Chun Wang, Jun-Yan Zhu* 
  **[`CVPR 2019`] (`UCB, NVIDIA`)**

- [High-Resolution Image Synthesis and Semantic Manipulation with Conditional GANs](https://arxiv.org/pdf/1711.11585.pdf)  
  *Ting-Chun Wang, Ming-Yu Liu, Jun-Yan Zhu, Andrew Tao, Jan Kautz, Bryan Catanzaro*   
  **[`CVPR 2018`] (`NVIDIA`)**





### 1.2 Auxiliary Classifier

- [GuidedStyle: Attribute Knowledge Guided Style Manipulation for Semantic Face Editing](https://arxiv.org/pdf/2012.11856.pdf)  
  *Xianxu Hou, Xiaokang Zhang, Linlin Shen, Zhihui Lai, Jun Wan*  

- [AttGAN: Facial Attribute Editing by Only Changing What You Want](https://arxiv.org/pdf/1711.10678.pdf)  
  *Zhenliang He, Wangmeng Zuo, Meina Kan, Shiguang Shan, Xilin Chen*  
  **[`TIP 2019`] (`CAS`)**



### 2.1 Encode

> encode a given image into a latent representation of the manipulated image



- [Face Identity Disentanglement via Latent Space Mapping](https://arxiv.org/pdf/2005.07728.pdf)  
  *Yotam Nitzan, Amit Bermano, Yangyan Li, Daniel Cohen-Or*  
  **[`TOG 2020`] (`Tel-Aviv University`)**

- [Encoding in Style: a StyleGAN Encoder for Image-to-Image Translation](https://arxiv.org/pdf/2008.00951.pdf)  
  *Elad Richardson, Yuval Alaluf, Or Patashnik, Yotam Nitzan, Yaniv Azar, Stav Shapiro, Daniel Cohen-Or*  
  **[`CVPR 2021`] (`Penta-AI, Tel-Aviv University`)**

- [Only a Matter of Style: Age Transformation Using a Style-Based Regression Model](https://arxiv.org/pdf/2102.02754.pdf)  
  *Yuval Alaluf, Or Patashnik, Daniel Cohen-Or*  
  **[`SIGGRAPH 2021`] (`Tel-Aviv University`)**



### 2. Modify GAN Model

control GANs' network parameters

click to see detailed notes

> Good: one model can produce countless new images following the modified rules.



- [Rewriting a Deep Generative Model](https://arxiv.org/pdf/2007.15646.pdf)  
  *David Bau, Steven Liu, Tongzhou Wang, Jun-Yan Zhu, Antonio Torralba*  
  **[`ECCV 2020`] (`MIT, Adobe`)**

- [Navigating the GAN Parameter Space for Semantic Image Editing](https://arxiv.org/pdf/2011.13786.pdf)  
  *Anton Cherepkov, Andrey Voynov, Artem Babenko*  
  **[`CVPR 2021`] (`MIPT`)**

- [Semantic Photo Manipulation with a Generative Image Prior](https://arxiv.org/pdf/2005.07727.pdf)  
  *David Bau, Hendrik Strobelt, William Peebles, Jonas Wulff, Bolei Zhou, Jun-Yan Zhu, Antonio Torralba*  
  **[`ECCV 2020`] (`MIT`)**  



### 2.2. Modify Latent Code

> analyze and dissect latent space,finding disentangled latent variables suitable for editing.

the discovered directions   linear / nonlinear path

their evaluation relies either on visual inspection or on laborious human labeling.



- [EditGAN: High-Precision Semantic Image Editing](https://arxiv.org/pdf/2111.03186.pdf)  
  *Huan Ling, Karsten Kreis, Daiqing Li, Seung Wook Kim, Antonio Torralba, Sanja Fidler*  
  **[`NeurIPS 2021`] (`NVIDIA, Toronto`)**

- [DatasetGAN: Efficient Labeled Data Factory with Minimal Human Effort](https://arxiv.org/pdf/2104.06490.pdf)  
  *Yuxuan Zhang, Huan Ling, Jun Gao, Kangxue Yin, Jean-Francois Lafleche, Adela Barriuso, Antonio Torralba, Sanja Fidler*  
  **[`CVPR 2021`] (`NVIDIA, Toronto`)**

- [Semantic Segmentation with Generative Models: Semi-Supervised Learning and Strong Out-of-Domain Generalization](https://arxiv.org/pdf/2104.05833.pdf)  
  *Daiqing Li, Junlin Yang, Karsten Kreis, Antonio Torralba, Sanja Fidler*  
  **[`CVPR 2021`] (`NVIDIA, Toronto`)**





#### Supervised 

> domain-specific transformations (adding smile or glasses)
>
> **weakness**: need human labels or pretrained models, expensive to obtain

pipeline: randomly sample a large amount of latent codes, then synthesize corresponding images and annotate them with labels, and finally use these labeled samples to learn a separation boundary in the latent space.

存在的问题：需要预定义的语义，需要大量采样

either by explicit human annotation, or by the use of pretrained semantic classifiers.

improves the memorability of the output image

- [Ganalyze: Toward visual definitions of cognitive image properties](https://arxiv.org/pdf/1906.10112.pdf)  
  *Lore Goetschalckx, Alex Andonian, Aude Oliva, Phillip Isola*  
  **[`CVPR 2019`] (`MIT, KU Leuven`)**

- [Interpreting the latent space of gans for semantic face editing](https://arxiv.org/pdf/1907.10786.pdf)  
  *Yujun Shen, Jinjin Gu, Xiaoou Tang, Bolei Zhou*  
  **[`CVPR 2020`] (`CUHK`)**

- [Semantic hierarchy emerges in deep generative representations for scene synthesis](https://arxiv.org/pdf/1911.09267.pdf)  
  *Ceyuan Yang, Yujun Shen, Bolei Zhou*  
  **[`IJCV 2021`] (`CUHK`)**

- [InterFaceGAN: Interpreting the Disentangled Face Representation Learned by GANs](https://arxiv.org/pdf/2005.09635.pdf)  
  *Yujun Shen, Ceyuan Yang, Xiaoou Tang, Bolei Zhou*  
  **[`TPAMI 2020`] (`CUHK`)**

- [Disentangled Image Generation Through Structured Noise Injection](https://arxiv.org/pdf/2004.12411.pdf)  
  *Yazeed Alharbi, Peter Wonka*  
  **[`CVPR 2020`] (`KAUST`)**

- [GAN Dissection: Visualizing and Understanding Generative Adversarial Networks](https://arxiv.org/pdf/1811.10597.pdf)  
  *David Bau, Jun-Yan Zhu, Hendrik Strobelt, Bolei Zhou, Joshua B. Tenenbaum, William T. Freeman, Antonio Torralba*  
  **[`ICLR 2019`] (`MIT, CUHK`)**

- [Semantic Photo Manipulation with a Generative Image Prior](https://arxiv.org/pdf/2005.07727.pdf)  
  *David Bau, Hendrik Strobelt, William Peebles, Jonas Wulff, Bolei Zhou, Jun-Yan Zhu, Antonio Torralba*   
  **[`TOG 2019`] (`MIT`)**

- [Controlling generative models with continuous factors of variations](https://arxiv.org/pdf/2001.10238.pdf)  
  *Antoine Plumerault, Hervé Le Borgne, Céline Hudelot*  
  **[`ICLR 2020`] (`CEA`)**





> explores the hierarchical semantics in the deep generative representations for scene synthesis

Use the classifiers pretrained on the CelebA dataset to predict certain face attributes

Add labels to latent space and separate a hyperplane. A normal to this hyperplane becomes a direction that captures the corresponding attribute.



- [StyleFlow: Attribute-conditioned Exploration of StyleGAN-Generated Images using Conditional Continuous Normalizing Flows](https://arxiv.org/pdf/2008.02401.pdf)  
  *Rameen Abdal, Peihao Zhu, Niloy Mitra, Peter Wonka*  
  **[`TOG 2021`] (`KAUST, UCL`)**



#### Self-Supervised Learning

> domain agnostic transformations (zooming or translation)
>
> (image augmentations) - [simple transformations]



- [On the "steerability" of generative adversarial networks](https://arxiv.org/pdf/1907.07171.pdf)  
  *Ali Jahanian, Lucy Chai, Phillip Isola*  
  **[`ICLR 2020`] (`MIT`)**

- [Controlling generative models with continuous factors of variations](https://arxiv.org/pdf/2001.10238.pdf)  
  *Antoine Plumerault, Hervé Le Borgne, Céline Hudelot*  
  **[`ICLR 2020`] (`Université Paris-Saclay`)**

solve the optimization problem in the latent space that maximizes the score of the pretrained model, predicting image memorability



#### Unsupervised

> are often less effective at providing semantic meaningful directions and all too often change image identity during an edit
>
> demanding training process that requires drawing large numbers of random latent codes and regressing the latent directions
>
> **weakness**: subjective visual inspection & laborious human labeling



- [GANSpace: Discovering Interpretable GAN Controls](https://arxiv.org/pdf/2004.02546.pdf)  
  *Erik Härkönen, Aaron Hertzmann, Jaakko Lehtinen, Sylvain Paris*  
  **[`NeurIPS 2020`] (`Adobe, NVIDIA`)** [[Code](https://github.com/harskish/ganspace)]

- [Unsupervised Discovery of Interpretable Directions in the GAN Latent Space](https://arxiv.org/pdf/2002.03754.pdf)  
  *Andrey Voynov, Artem Babenko*
  **[`ICML 2020`] (`Russia`)**  [[Code](https://github.com/anvoynov/GANLatentDiscovery)]

- [WarpedGANSpace: Finding non-linear RBF paths in GAN latent space](https://arxiv.org/pdf/2109.13357.pdf)  
  *Christos Tzelepis, Georgios Tzimiropoulos, Ioannis Patras*  
  **[`ICCV 2021`] (`QMUL`)** [[Code](https://github.com/chi0tzp/WarpedGANSpace)]





do not use any optimization

- [On the "steerability" of generative adversarial networks](https://arxiv.org/pdf/1907.07171.pdf)  
  *Ali Jahanian, Lucy Chai, Phillip Isola*  
  **[`ICLR 2020`] (`MIT`)**

- [GAN ”steerability” without optimization](https://arxiv.org/abs/2012.05328)  
  *Nurit Spingarn-Eliezer, Ron Banner, Tomer Michaeli*  
  **[`ICLR 2021`] (`Intel, IIT`)**





Unsure

[Closed-Form Factorization of Latent Semantics in GANs](https://arxiv.org/pdf/2007.06600.pdf)  
*Yujun Shen, Bolei Zhou*  
**[`CVPR 2021`] (`CUHK`)**

A geometric analysis of deep generative image models and its applications



<span id="LowRankGAN"></span>
[Low-Rank Subspaces in GANs](https://arxiv.org/pdf/2106.04488.pdf)  
*Jiapeng Zhu, Ruili Feng, Yujun Shen, Deli Zhao, Zhengjun Zha, Jingren Zhou, Qifeng Chen*  
**[`NeurIPS 2021`] (`HKUST, Alibaba, USTC`)**  