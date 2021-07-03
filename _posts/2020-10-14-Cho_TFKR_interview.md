---
layout: post 
date: 2020-10-14
title: TFKR X 조경현 교수님 Interview 
description: TFKR에서 진행한 조경현 교수님 인터뷰에서 인상깊은 부분을 정리해 보았습니다.
published: True
--- 

##### TFKR에서 50,000명 그룹 달성 기념으로 진행한 event의 일부로 조경현 교수님과의 인터뷰를 가볍게 정리해 보았습니다. 
<br>
<교육>
카이스트 컴공에서는 probablistic robotics 하나 듣고 > 헬싱키 유럽 데이타마이닝 프로그램 지원 Master에서 하며 머신러닝을 시작  <br>

<br>
<일과> 
일하고 밥먹고 일찍자고..... <br>
학생들과 소통하고 그러며.. <br>
"다른 생각하고 새로운 것을 읽어보고 접하는 시간이 있어야 하는데" 그런 시간이 줄어든다.<br>
<br>
<아이디어> <br>
아이디어가 너무 많아도 문제고.. 아이디어가 많을 수록 verifiy할 수 있어야 해. 주요 아이디어를 키울 수 있도록. <br>
새로운 아이디어도 많지 않은 듯하다. 새로운 아이디어라 해서 진득히 앉아서 써보고 수학으로 써보고 구글에 리터려쳐링 해보면 대부분 5년에서 50년 전 사이 누군가가 생각해서 써 놓은 경우가 많아. 괜찮은 건 계속 pursue하지만. <br>
"아이디어 > formulize > 실험 > 논문" <br>
과정 보다는 아이디어들이 valid, prove한지, literature review해보는 데에 시간을 많이 쓴다. <br>
<br>
<풀고 싶은 문제> <br>
그동안은 상황을 봐가며 재밌어 보이는 것을 쫓았음. 하지만 가장 목표는 공통적으로 NLP나 전반적 AI 연구자들은 intelligence가 무엇인지 찾고 싶어 함. 지능이 무엇이냐. reverse engineering, how to make it, components of intelligence 를 하고.. <br>
궁극적인 목표는 인텔리전스가 무엇인지 define하고 what is intelligence 라고 물을 때 답할 수 있기를. <br>
Q.교수님이 생각하는 intelligence란 <br>
인텔리전스는 멀티디멘셔날해서. high dimensional vector와 같이 유사한. <br>
<br>
<도메인> <br>
Q.한국어를 위한 기술들? <br>
<br>
Q. 트랜스포머 이후의 모델들은 스케일업만 하는 것 같다. 대안은? >>> 스케일업이 나쁜 것이 아니다. 스케일 업은 계속해서 필요하다. 다만 모두가 할 수 없을 뿐인데, 스케일업을 해야 하는데 대기업에 해주어 연구논문을 발표해주니 이런 결과가 나옴을 확인할 수 있어 고맙다. 다만, 스케일업을 해서 풀리지 않는 문제들은 왜 그러는지, 어떻게 풀어야 하는지 , 대안이라기보다는 프라블럼 셋업문제인지, 알고리즈믹하게 바꾸어야 하는지, 혹은 풀었지만 evaluation을 못하는 건지 생각을 해봐야 한다. 큰 파이프라인을 보며 문제를 생각해야 함 <br>
<br>
Q. RNN의 입지는 줄어드는 것 같다. 이에 대한 생각은? <br>
>>> history compression을 어떻게 할 것인지에 초점을 맞춰야. RL같은 데에서도 attention을 할 때 중요한데, future reward를 어떻게 할지를 고려해야 함. 그렇다면 learning algorithm이 어떻게 되어야 하는지. 다시 말해 short-term의 문제의 경우 transformer쓰겠지만 logn-term의 문제의 RNN을 쓰겠죠. A or B가 아니라 풀고 싶은 문제에 따라 적절한 모델을 취사 선택, 조합 등을 통해 활용해야 하는가. 따라서 continual learning이 lifelong scale로 갈 때 모델이 하이브리드 하게 가지 않을까 생각. learning alg는 어떻게 될지 의문. <br>
temporal difference learning with bootstraping을 한다는데 년 단위로 할 수 있는 것도 아니고,, RNN verse Transformer가 아니라 이런 식으로 생각하는게 맞지 않을까 싶음.   <br>
<br>
Q. 후배 연구자들에게 조언?<br>
어느 새 보니 메인스트림에 있었는데, 이 분야가 메인스트림의 메인스트림일 수는 없는 것 아닌가. 물론 AI는 항사 메인스트림이었음. CS보다 오랜 역사로 메인스트림이었음. 새로운 걸 하려면 남들이 하라는 걸 안하는 게 낫지 않을까. <br>
<br>
Q. 미국에서 취업하기 위해서는? 교수님과 같은 펠로우에서 일하고자 한다면? <br>
박사 졸업할 떄 즘은 학력이라는 게 의미가 없는 거 같다. 경력도. 박사를 졸업할 때 즘이면 어떤 연구를 해왔고 어떤 연구를 할 줄 알고 그 연구로 학계나 산업계에 어떤 임팩트를 남겼는가가 중요. 논문을 잘 썼나, 오픈소스로 릴리즈하고 사람들이 많이 사용하였는지 등이 더 중요. 물론 학력도 지도교수 네트웤 같은 거에 쉽게 들어가는 장점이 있을 수 있겠지만, '저 교수 밑에서 했구나. 그래서 뭘 했는데?' 이렇게 됨. 그렇다기보다는 유명한 학교가 아니더라도 연구 등을 통해 임팩트 남기는 것이 더 중요. <br>
<br>
Q. 뉴욕에서 교수님께 배우려면? <br>
답이 없다! 한가지라면, 원서 준비 시 모든 aspect에 대해 준비해야 함. 실제로 모든 application을 다 읽어봄.<br> 모든 걸 준비를 잘 해야함. 합격 학생들에 대해 correlation 은 없음. 와서 어떻게 하는지가 더 중요. <br>
<br>
(김성훈 교수님) 관심있는 분들은 자신감을 가지고 지원해보고, 교수님과 열심히 하면 된다. <br>
<br>
probabilistic programming - Frank Wood<br>
<br>
Q. 다양한 주제에 대해 학생들에게 어떻게 advice해 주는지 <br>
ex. 다음 미팅 때는 관심있는 주제 3,4개에 대해 literature review를 해와봐라. <br>
<br>
Q. Yoshua가 최근 casual inference 에 대해 연구하고 있는 것으로 알고 있다. 이에 대한 생각은?  <br>
문제 프레이밍을 어떻게 하는지가 중요하지 안을까 생각. <br>
이걸 Facebook의 리온부트 에게 물었을 때 pixel level data에 적용해 본다고 생각해보라. 라고 답함. casual inference가 variable이 2,3개 일때도 하기 어려운데, 굉장히 assumptions이 satify할 때 해야.. <br>
deep learning의 경우 high dimensional한 raw data를 가지고 할 때 잘되었던 것 <br>
그 뜻은 casual inference 를 바로 적용하기보다는 여기서 나오는 lesson들 이용해서 <br>
어떻게 하면 casual inference나 low dimensional representation 을 찾는 것이 더 중요한 것으로 보이는데, Yoshua는 요새 causally corelent 한 factor, mechanism을 찾는 데 focus를 찾는 것 같고. 본인은 casually incorrelent한 요소를 걸러내는 것에 초점. 왜냐면 variable들이 생겨야 그 다음 ~ 인데, low dimensional variable 찾는 게 더 어려운 것 같아서..  







