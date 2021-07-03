---
layout : post 
title : 2020,08,28 what did I search ?
date : 2020-08-28
description : record of something to learn briefly
comments : true 
published : false
--- 


1. meta learning 
메타 러닝은 "Learning to learn"이라고 불린다. 
학습되지 않은 데이터, 학습되지 않은 환경에서, 새로운 데이터, 새로운 환경을 만났을 때에 사람처럼 빠르게 학습할 수 있는 학습에 대해 말한다. 
https://lilianweng.github.io/lil-log/2018/11/30/meta-learning.html 
더 자세한 내용에 대해 

2. federated learning 
federated learning 은 사용자가 직접 사용하는 기기에서 데이터를 처리해 저용량 모델을 학습시키고 그 모델들을 모아 더 정교한 모델들을 만들어 재배포하는 학습 방식이다. 페이스북이 안드로이드와 ios환경에서 원활하게 머신러닝을 실행, 배포할 수 있는 'pytorch mobile'라는 새로운 프레임워크를 내놓았으며, 이는 연합학습에도 용이하다. 

보통 의료 시나리오에 배치된 AI 알고리즘은 궁극적으로 임상 등급의 정확도에 도달해야 한다. 이는 적용되는 응용 프로그램의 표준을 충족하거나 능가한다는 의미인 것이다. 또 의료 전문가와 동일한 등급을 충족하는 모델을 교육하려면 AI 알고리즘에 많은 사례가 제공되어야 한다. 그리고 이러한 예는 사용될 임상 환경을 충분히 나타내야 한다.

개인 정보 등 민감한 임상 데이터를 서로 직접 공유할 필요가 없이 여러 번의 반복 학습 과정에서 공유 모델은 단일 조직이 자체적으로 보유한 것 보다 훨씬 광범위한 데이터를 얻게되는 것으로 기관에서는 더욱 매력적인 것


3. Adversarial robustness 
Adversarial Attack ; 딥러닝 모델들이 작은 noise 에도 오작동하는 모습들을 보임
                        (ref. Black-Box Attack against RNN based Malware Detection Algoritms, 2017, Hu and Tan)
Adversarial Deffense ; 그를 방어하려는 목적 

    " Q . 정말 딥러닝은 사람처럼 세상을 인식하고 있을까?
        A . 대답은, 아니다. 정리해보면, 
            1. 현재의 딥러닝 구조 및 학습법은 adversarial attack으로부터 자유롭지 못하다 
            2. (짧은 시간이었지만) 다양한 연구 결과들이 나왔고, 이들은 adversarial attack을 함께 학습함으로써, 혹은 detecting이나 denoising함으로써 이를 보완하는 결과를 보였다. 
            3. natural variance에 robust하지 못한 현재의 구조를 개선하며 Capsule Network이 제안되었지만, 아직 검증은 되지 못했다 
            4. adversarial attack problem이 해결된다 하더라도 또 다른 부분이 발견될 수 있다.(아직 할게 많다)
    " 
    더 자세한 내용은 https://www.slideshare.net/NaverEngineering/ss-86897066


4. Shoud I do a Ph.D ? 

1) You have an irrational LOVE for research
2) You enjoy challenging assumptions
    The most successful PhDs I know have always worked on projects that are fundamentally challenging an assumption in their field. Essentially, these people have such a strong desire for the truth, that unless it breaks a thermodynamic law, they believe it is possible!
    >>> 
    I am enjoying challenging a assumption, actually I was so impressed when I found dot production attention myself (even though it was already existed)
3) You know exactly why you want a PhD
    You should do a PhD ONLY if you know exactly what you want to accomplish at the end of the PhD. Remember, the PhD is a path, not an end. 
    >>> 
    I wanna make a general artificial intelligence to solve high level solution. For instance, climate problem, poverty, capitalism, government issue , and so on. 
4) You have a desire to invent
    A PhD is one of the best ways to have intellectual freedom to invent things you are passionate about. I have been fortunate to have had this opportunity several times and trust me, it’s an awesome feeling. If you are lucky, you invent something so critical that the marketplace licenses it from you and your impact translates from lab to the ‘real world.’ While this does not always happen, having the desire to produce is instrumental in having a successful PhD.
    >>> 
    And I want to provide it whole world. for releasing people to be own happy life. 
5) You enjoy the learning-teaching process.
    Unlike other jobs, where you acquire a skill and produce a lot based on that skill. Research is quite different in that you have to constantly stay updated, read papers, learn new techniques or ideas, and so on. So even if you don’t want to be a professor after the PhD, you have to enjoy the process.
    >>> I love it , almost studies. 

more specific article is here https://www.linkedin.com/pulse/should-i-do-phd-top-5-reasons-good-idea-rishabh-jain/

>>> but sometimes, the desire what I want to make end-product and provide it is, similar with research. 
