---
layout: post 
title: Meta Dropout, Learning to perturb latent features for generalization
date : 2021-01-24
description: Meta Dropout 논문을 리뷰합니다. 
published : true
comments: true
---

이번 포스트는 <a href = "https://arxiv.org/abs/1905.12914?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%253A+arxiv%252FQSXk+%2528ExcitingAds%2521+cs+updates+on+arXiv.org%2529"><b> Meta Dropout: Learning to Perturb Features for Generalization </b></a> 논문 리뷰를 포스팅합니다. 잘 학습된 모델은 학습 과정에서 보지 않은 데이터에 대해서도 추론과정에서 좋은 성능을 낼 수 있어야 합니다. 이런 우수한 일반화 성능을 내기 위해서 training sample을 적절하게 perturbation시킬 수 있는 방법을 안다면 좋겠지만, 기존의 학습 방법에서는 test sample에 대한 분포를 모르기 때문에 매우 어렵다고 볼 수 있습니다. 따라서 본 논문에서는 meta-learning framework에서 meta-dropout이라는 새로운 regularization 방법을 도입하여, training sample의 latent feature를 교란하는 방법의 학습을 돕는 noise generator를 학습시킵니다. 학습된 noise generator는 meta-test time에 보지 않은 task에 대해서도 뛰어난 일반화 성능을 보여주게 됩니다. 결과적으로 이러한 방법은 기존의 information bottleneck, manifold mixup, information dropout과 같은 regularization 방법론들에 비해 outperformance를 보여주고 있습니다. 

<!-- train/test 샘플 비중에 따라 모델의 confidence param을 만들고,  perturb하게 학습시킬 수는 없을까? 기존의 frame에서도? -->

### Intro

모델의 generalization 성능을 향상시키기 위해 기존에는 variance reduction methods에 치중을 두는 연구들이 주로 이루어지고는 하였습니다. 이러한 방법론들은 input의 변화에 따른 model variance를 감소시키기 위한 방법론이었습니다. model complexity를 control한다거나, input으로부터의 정보를 reducing 한다거나 하는 등의 연구가 그런 방법론의 일부였습니다. 

한편, 더욱 직접적으로 generalization 성능 향상을 위해서, training time에 training example을 교란(?)시켜 test example들을 simulate하는 효과를 내는 방법론들이 등장했습니다. 어떤 training example에 대해 다른 training example의 방향으로 교란시킴으로써, 모델의 학습에 좀 더 혼동을 주고, test example을 흉내내도록 하는 <a href="https://arxiv.org/abs/1710.09412"><b>mixup</b></a>이 그러한 방법입니다. 또한, 이러한 방법을 latent feature space에서 시도한 것이 <a href="https://arxiv.org/abs/1806.05236"><b>manifold mixup</b></a>입니다. 

그러나 이러한 방법론들은, 명시적으로 test time의 일반화 성능을 저하시키려는 목적을 가질 수 없었습니다. test set에 대한 distribution을 train time에서는 볼 수 없기 때문입니다. 본 논문에서는 교란된 학습 데이터들이 test time의 loss를 더욱 감소시키는 것을, 즉 일반화 성능 향상에 직접적으로 도움이 됨을 보일 수 있도록 이를 meta-learning framework에 적용합니다. meta-training step에서는, training step 내의 episodes(tasks)에 대한 train과 test set 모두에 대한 data를 관찰할 수 있고, 이는 즉 noise generator가 meta-test time에서 더욱 잘 일반화될 수 있는 perturbed instances 생성을 학습할 수 있게 합니다. 한편, perturbation을 시켜야 하는 meaningful한 direction은 어디인지, 또 perturbation을 통한 single training instance가 대량의 test instances들을 cover해야 한다는 점에서 "stochastic input-dependent perturbation"을 학습할 수 있는 noise genertator인, meta-dropout을 도입하게 됩니다. 

본 논문에서의 주요 기여는 다음과 같습니다. 

**주요 기여** 
1. stochastic input-dependent perturbation을 생성할 수 있는, "meta-dropout" 이라는 새로운 regularization method를 제안하였고, 이를 통해 few-shot learining model의 일반화 성능 향상에 기여합니다. 

2. information bottleneck, manifold mixup 등과 같은 다른 regularizer와 비교하였습니다. 또한 variational inference framework을 regularize 하는 것을 학습한다는 면에서, 논문에서 제시하는 방법론의 확률론적 해석을 설명하고 있습니다. 

3. few-shot classification task의 여러 benchmark dataset에서 본 논문의 method가 기존의 base model을 개선시킴을 보였습니다.  

**결과**
1. few-shot classification datasets(Omniglot, miniImageNet)에서 기존의 generalization regularization 방법론들에 비해 outperformance를 내었습니다. 

### Main Idea 

1. 왜 Meta-Dropout 일까? 
들어가기에 앞서, 본 논문의 meta-noise generator가 "meta-dropout" 인 이유에 대해서 이야기해 보고자 합니다. 그 동안 Dropout 에 대해서는 특정한 weight를 stochastic 하게 off 함으로서 (마치 뉴런이 커지고, 꺼지는 것과 같이) 모델의 성능을 향상시키는 정도로만 알고 있었는데요, 한편, 세부적으로는 Dropout 은 feature decorrlation, ensemble 효과 등이 뿐만 아니라, network weight의 posterior inference를 위한 variational approximation으로도 해석할 수 있었습니다. 이런 관점에서 dropout regularization은 noise injection 으로 해석될 수 있음을 알게 되었습니다. standard dropout의 경우에는 Bernoulli distribution을 따르는 noise 를 생성하게 되지만, 본 논문에서는 Gaussian multiplicative한 noise를 생성한다는 관점에서 일종의 dropout이라 할 수 있게 됩니다.

2. LEARNING TO PERTURB LATENT FEATURES




방법론적인 이야기 

### 결과 

실험 결과와 그에 대한 분석 

### 마치며 


<!-- mixup - 학습 단계에서 두 개의 인풋 데이터를 랜덤으로 샘플링해서 새로운 인풋을 적절히 섞어 만드는 기법. 이 기법을 적용하면 네트워크는 여기서 샘플링한 값만을 인풋값으로 입력받는다. 데이터를 일부러 식별하기 어렵게 만들어서 학습에 어려움을 주는 것이다. 과적합 문제에 빠지는 것을 방지할 수 있다고 한다. 

manifold mixup - 두 Input x1과 x2의 함수를 취한 결과값 f(x1) 과 f(x2) 두개를 위의 식과 같이 섞어준다는 간단한 말로 표현될 수 있다.

PuzzleMix - 기존의 mixup을 기반으로 한 data augmentation을 수행하는데, contribution 1. sailency(중요한 부분)를 각 이미지(in vision)에서 뽑아내고, sailency를 보존하는 이미지를 만든다. contribution 2. 각 이미지에 존재하는 local statistics를 보존한다...  

Mixtest - 주요 contribution으로 주장하는 것은, mixup idea를 문장에 바로 적용할수가 없으니까, hidden layer에 적용해보자! 이다.

Empirical Risk Minimization (ERM) 관점 - Empirical Risk 라는 것은 Cost와도 같은 의미이다. 즉, Cost function 을 Minimization하는 관점과 같은 것. 

th) data 에 대해서... generalization하고 싶으면,, 그 data의 distribution을 이해하고 있는 것이 중요해. 아니... 근데.. 왜 꼭 데이터 기반이어야 해. 어느 정도는 knowledge based로 가면 안돼? 아니, knowledge를 좀 뽑아내게 할 수는 없을까? data에는 통계만 있어. 그 통계로부터 weight가 적절하게 변형될 뿐이야. 좀 더 knowledge를 학습하게 할 수 없을까. few shot learner,,, 
data 


th) 졸논 주제 1 : text from image project, "can you let me explain that image ?" (TOEIC part 1 image and statement dataset !)
    - can I make it trainable ?  I don't know, let's get it.  -->