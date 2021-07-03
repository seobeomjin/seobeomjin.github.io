---
layout : post 
title : About task of reading papers
date : 2020-10-13
description : 
published : false
--- 
Here is a repository which I record the flow of read papers. <br>
If want to check details of a certain paper, please check google docs "papers review".  

<!-- ### What I am interested in nowdays 
Natural Language Model <br>
Reinforcement learning <br>
Can we build a model which can generalize -->

### What I would read 

* about meta learning 
    https://lilianweng.github.io/lil-log/2018/11/30/meta-learning.html
    https://talkingaboutme.tistory.com/entry/DL-Meta-Learning-Learning-to-Learn-Fast


* (reading...) Ng, Nathan, Kyunghyun Cho, and Marzyeh Ghassemi. "SSMBA: Self-Supervised Manifold Based Data Augmentation for Improving Out-of-Domain Robustness." arXiv preprint arXiv:2009.10195 (2020).

* Chevalier-Boisvert, Maxime, et al. "Babyai: A platform to study the sample efficiency of grounded language learning." International Conference on Learning Representations. 2018.
    - Luketina, Jelena, et al. "A survey of reinforcement learning informed by natural language." arXiv preprint arXiv:1906.03926 (2019).
        - Petroni, Fabio, et al. "Language models as knowledge bases?." arXiv preprint arXiv:1909.01066 (2019).

* Challenging Common Assumptions in the Unsupervised Learning of Disentangled Representations

* Liquid Time-constant Networks

* Learning De-biased Representations with Biased Representations

### What I've read 

2020-10-20 
* Fast-RCNN <br>
    이 때, classificaiton loss와 bounding box regression을 적절하게 엮어주는 것이 필요하며, 이를 multi task loss라고 합니다.

    즉, CNN 단을 Object Detection에 맞게끔 fine-tuning 하는 것이 성능 향상의 키 포인트 였습니다. 

    object detection 테스크를 푸는 end-to-end 모델을 제시하면서 학습 단계를 간소화시키고 정확도와 성능 모두를 향상시켰다는 의의

    deep ConvNets are adept at directly learning scale invariance ? 

* Faster-RCNN <br>
    그동안 Selective Search를 사용하여 계산해왔던 Region Proposal 단계를 Neural Network 안으로 끌어와서 진정한 의미의 end-to-end object detection 모델을 제시

    RPN은 앞서서 Classification과 Bouding Box Regression을 수행하였는데요, 로스 펑션은 이 두 가지 테스크에서 얻은 로스를 엮은 형태를 취하고 있습니다.

     RPN과 Fast R-CNN 두 네트워크를 사이 좋게 엮어서 학습시키는 방법에 대해서 알아보겠습니다.

     4단계에 걸쳐서 모델을 번갈아서 학습시키는 Alternating Training 기법을 취합니다. 

     



2020-10-18 
* DOTA: A Large-scale Dataset for Object Detection in Aerial Images
    - Abstract - Figures&Tables - Introduction - my conclusion 
    - Summrization by 3 lines 
        1. areal image domain 에서 object detection 
        2. DOTA dataset 제공과 더불어 SOTA 모델 
        3. 

2020-10-17
* De-biased 


2020-10-13

* Ng, Nathan, Kyunghyun Cho, and Marzyeh Ghassemi. "SSMBA: Self-Supervised Manifold Based Data Augmentation for Improving Out-of-Domain Robustness." arXiv preprint arXiv:2009.10195 (2020).
    - Abstract - Figures&Tablse - Conclusion 
        corruption function 을 구성하여 기존의 데이터 x 를 x' 으로 만들고 이를 다시 reconstruction 하여 x_hat 을 만들어 augemented_dataset을 구성한다. 이 때 x'은 manifold 위로 projection하여 x_hat이 만들어진다.
        (th) 이게 어떻게 projection이라고 말할 수 있는걸까? introduction 읽어봐야 할 듯.   




2020-06 ~ 2020-08 
* Öztürk, Hakime, Arzucan Özgür, and Elif Ozkirimli. "DeepDTA: deep drug–target binding affinity prediction." Bioinformatics 34.17 (2018): i821-i829.

* Durrant, Jacob D., and J. Andrew McCammon. "NNScore: a neural-network-based scoring function for the characterization of protein− ligand complexes." Journal of chemical information and modeling 50.10(2010): 1865-1871.

* Jiménez, José, et al. "K deep: Protein–ligand absolute binding affinity prediction via 3d-convolutional neural networks." Journal of chemical information and modeling 58.2 (2018): 287-296.

* Zheng, Liangzhen, Jingrong Fan, and Yuguang Mu. "OnionNet: a Multiple-Layer IntermolecularContact-Based Convolutional Neural Network for Protein–Ligand Binding Affinity Prediction." ACS omega 4.14 (2019): 15956-15965.

* Hassan-Harrirou, Hussein, Ce Zhang, and Thomas Lemmin. "RosENet: Improving Binding Affinity Prediction by Leveraging Molecular Mechanics Energies with an Ensemble of 3D Convolutional Neural Networks." Journal of Chemical Information and Modeling (2020).

* Lim, Jaechang, et al. "Predicting drug–target interaction using a novel graph neural network with 3D structure-embedded graph representation." Journal of chemical information and modeling 59.9 (2019):3981-3988.

* Vaswani, Ashish, et al. "Attention is all you need." Advances in neural information processing systems. 2017.

* Zhou, Bolei, et al. "Learning deep features for discriminative localization." Proceedings of the IEEE conference on computer vision and pattern recognition. 2016. (CAM)

* Selvaraju, Ramprasaath R., et al. "Grad-cam: Visual explanations from deep networks via gradientbased localization." Proceedings of the IEEE international conference on computer vision. 2017. 

* Kipf, Thomas N., and Max Welling. "Semi-supervised classification with graph convolutional networks." arXiv preprint arXiv:1609.02907 (2016).

* Veličković, Petar, et al. "Graph attention networks." arXiv preprint arXiv:1710.10903 (2017).

* Ryu, Seongok, et al. "Deeply learning molecular structure-property relationships using attention-and gate-augmented graph convolutional network." arXiv preprint arXiv:1805.10988 (2018).


2020-05-25 
* A Computational-Based Method for Predicting Drug–Target Interactions by Using Stacked Autoencoder Deep Neural Network
    - Abstract - Figures&Tables - Conclusion - methods(partially)
    - Summarization by 3 lines <br>
        1. 리셉터와 드러그 간의 결합을 classification 하기 위한 Stacked AE 와 FingerPrint 융합을 활용한 데이터 인풋 이용 
        2. 이 후 그것을 RF classifier에 넣어 활용
        3. 성능은 2017 당시 outperform <br><br>
        
* All SMILES Variational Autoencoder
    - Abstract - Figures&Tables - Conclusion - methods
    - Summarization by 3 lines <br>
        1. single molecule에 대해 multiple SMILES를 encoding 함 (stacked RNN, pooling hidden representation , attentional mechanism. 
        2. encoding 이후 regressor를 최적화 시켜, supervised, semi-supervised 에서 최적의 성능을 냄
        3. decoder를 통해 유의미한 SMILES 생성 가능. 
        (th) 다중 스마일스 사용 / 공통 분자, 다른 스마일즈 간의 동일한 의미를 찾아냄 , molecular graph의 모든 pathway에 그 정보가 흐를 수 있도록 함. <br><br>
* Automatic Chemical Design Using a Data-Driven Continuous Representation of Molecules
    - Abstrat - Figures&Tables


2020-05-24 
* Attention Branch Network: Learning of Attention Mechanism for Visual Explanation
    - Abstract - Figures&Tables - Conclusion - Introduction - Methods 
    - Summarization by 3 lines <br>
        1. 기존의 CAM은 response based visual explantion의 모델이지만 CNN의 성능을 낮추는 단점이 있었음. 
        2. Attention mechanism 을 적용하여, 어텐션 맵을 만드는 동시에, 성능 향상에 기여하였음.
        3. 기존의 모델에 비해 성능이 좋고 어텐션 맵을 표현함. 


2020-05-23 
* FP2VEC: a new molecular featurizer for learning molecular properties 2018
    - Abstract - Figures&Tables


2020-05-07
* Development and evaluation of a deep learning model for protein–ligand binding affinity prediction
    - Abstact - Figures&Tables - my conclusion 
    - Summarization by 3 lines <br>
        1. protein-ligand complex + feature vector를 활용한 4차원 데이터 구조 인풋 
        2. CONV layer와 DENSE layer 통과, 여러 지표에서 outperform (다양한 SFs)
        3. 피처들의 특징을 되돌아 볼 수 있음을 시사 (th- 하지만 데이터 구조가 해석이 어려운 이상, 도움이 될지.) <br><br>

* Entangled Conditional Adversarial Autoencoder for de Novo Drug Discovery
    - Abstract - Figures&Tables 


2020-05-06
* An Overview of Scoring Functions Used for Protein–Ligand Interactions in Molecular Docking
    - Abtract - Figures&Tables - my conclusion - conclusion 
    - Summrization by 3 lines <br>
        1. MD에서 사용되는 다양한 SF 함수들이 있음. 
        Physics / Empirical / Knowledge based / ML based / + Hybrid SFs briefly
        2. 해당 함수들의 장단점을 소개 
        3. outperform을 낼 수 있는 ML , 새로운 universal , novel SF from ML based를 강조 <br><br>

* Atomic Convolutional Networks for Predicting Protein-Ligand Binding Affinity
    - Abstract - Figures&Tables - my conclusion - Discussion and Result - Methods 
    - Summrization by 3 lines <br>
        1. 바인딩 어피니티를 예측할 수 있는 새로운 형태의 데이터 인풋을 이용해 크리스탈 스트럭처 기반의 데이터 인풋을 형성한 콘볼루션 형성 
        2. 모델 구성 후 complex delta를 구하기 위해 only protein, only ligand 값을 빼어 계산, 성능은 비슷비슷하고, 오차가 적음, 하지만 일반화 안됨 
        3. ligand scaffold 가 파악되지 못한 경우 등 새로운 구조의 데이터에 대해 어려움이 있음. 일반화 성능이 문제임 


#### inequality problems and AI 
* How Are We Solving Inequality with AI?
https://medium.com/@ODSC/how-are-we-solving-inequality-with-ai-966ce8dc4c32 <br>

* How AI can help reduce inequalities
https://hellofuture.orange.com/en/how-ai-can-help-reduce-inequalities/ <br>

* Artificial Intelligence and the Rise of Economic Inequality
https://towardsdatascience.com/artificial-intelligence-and-the-rise-of-economic-inequality-b9d81be58bec <br>


<!--
all read paper is summarized on google docs "papers review" 

The most important problems are climate change and economic inequality
-->
