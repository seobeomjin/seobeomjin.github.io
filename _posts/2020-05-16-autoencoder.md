---
layout: post 
title: Naver Engineering Autoencoder 발표 정리
subtitle : naver engineering Autoencoder 발표에 대한 정리입니다. 
categories: Study
tags: autoencoder 
comments : true
published : False
---

들어가기 앞서 해당 포스트는 이활석 님의 발표를 보고 정리한 것입니다.<br> <a href = "https://www.youtube.com/watch?v=o_peo6U7IRM" target = "_blank"><b>youtube link</b></a>를 통해 발표 영상을 확인하실 수 있습니다. 


#### part of chaptor 1

- gradient descent 는 optimal problem 을 푸는 하나의 방법으로, optimal theory를 공부할 때 가장 기초적인 방법 
th) 선형대수적 어프록시메이션도 있었음, 한 번에 찾는. <br>
- Loss Update 시, Taylor expansion에서 우리는 first derivate만 쓰니까, 아주 가까운 근방의 approximation만 update를 시킬 수 있음. 그러므로 learning rate를 작게 가져가야 함. learning rate가 크면 첨펑첨펑 함. <br> 
- batch에서 구한 gradient와 전체 평균 gradient가 같을 거라고 approximation을 또 함. 배치 하나 때서 업데이트 배치 하나 때서 업데이트. 평균을 전체 epoch에 대해 구할 수 없으니 배치로 업데이트 함. <br> 

#### back propagation 관점의 Loss function 

- Loss function으로 MSE를 사용하는 경우를 가정해보자. back propagation 시, 수식에 activation function의 미분값이 들어가는데, 예를 들어 activation function으로 sigmoid를 쓰면 sigmoid의 미분은 모자 모양이니까 wx+b가 0에 가까울 수록 업데이트가 잘 되고, wx+b가 0에서 멀어질수록 그 미분값이 더 작아짐 > 고로 업데이트가 더 잘 안됨 > 뒷 단으로 갈수록 그러면 gradient banashing 문제가 일어남 > activation function 변경 필요 > relu를 많이 쓰는 이유  <br>

- 한편, Loss function을 MSE가 아니라 CE를 쓰면, 아예 ativation function term이 back propagation 함수에서 사라지기 때문에 (계속 없는게 아니라 처음에만 사라짐, 처음에만 1/4 안 줄고 가는 것) 초기값에 상관없이 더 학습이 잘 됨. (항상 그런건 아니지만)   <br> 
 
#### Maximum Likelihood Estimation (MLE) 관점의 Loss function 

- 해당 관점의 point는 "네트워크의 출력값이 우리가 원하는 정답이 나올 확률이 높기를 바란다."라는 점. 이 관점에서는 우리가 학습시키는 모델의 파라미터는 우리가 추측하고자 하는 분포의 평균값이 될 수 있음. (예를 들어, Gaussian이라 가정할 때) 우리는 학습을 시킬수록 그 정답의 분포의 평균과 가까워 지는 것임. 
이럴 경우 L = -log(p(y|f_theta(x)) 로 표현 가능. <br>  
이렇게 해석할 경우, 우리는 분포를 예측한 것이기 때문에, 이 분포에서 샘플링을 하여, 고정 입력, 고정 출력이 아니라, **고정입력, 다른 출력**이 가능하게 됨. 
즉, 확률적으로 샘플링이 가능.<br> 

- 확률 분포가 Gaussian이냐 , Bernoulli냐.  <br>
가우시안으로 가정할 경우 Loss Function을 정리하면  MSE와 식이 같아지고 , 베르누이로 가정할 경우, Loss Funtion을 풀면 CE와 같아짐. <br><br>
즉 확률관점에서 만약 우리가 추정하려는 분포가 Gaussian이고 continuous하면 MSE를 쓰는 게 맞고, Bernoulli이고 Discrete하면 CE를 쓰는게 맞음.  <br><br>
이렇게 해석할 수 있다는 것 

- 이를 정리하면 아래의 슬라이드와 같다. <br>
![Yosuha Bengio's slide]({{site.url}}/assets/images/autoencoder/bengio_slide.png)

- 추가 이미지 
![slide]({{site.url}}/assets/images/autoencoder/ch1_1.jpg)
![slide]({{site.url}}/assets/images/autoencoder/ch1_2.jpg)
![slide]({{site.url}}/assets/images/autoencoder/ch1_3.jpg)


#### Dimensionality Reduction slide

![Dimensionality Reduction slide]({{site.url}}/assets/images/autoencoder/dimensionality_reduction.png)

#### GAN 

![slide]({{site.url}}/assets/images/autoencoder/gan.jpg)

#### AutoEncoder and VAE

![slide]({{site.url}}/assets/images/autoencoder/autoencoder/ae.jpg)
![slide]({{site.url}}/assets/images/autoencoder/vae.jpg)
![slide]({{site.url}}/assets/images/autoencoder/vae_2.jpg)
![slide]({{site.url}}/assets/images/autoencoder/vae_3.jpg)

#### AAE 
![slide]({{site.url}}/assets/images/autoencoder/aae.jpg)
![slide]({{site.url}}/assets/images/autoencoder/saae.jpg)


