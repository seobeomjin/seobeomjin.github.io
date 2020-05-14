---
layout: post
date: 2020-04-15
title: Machine Learning model releasing with Docker [1]
description: 머신러닝 모델을 웹으로 릴리즈 하기 위한 공부를 하고있습니다. 
comments: true 
---


- https://www.kdnuggets.com/2019/03/deploy-pytorch-model-production.html

### 1. Saving and Loading Models 
### 2. Simple Deployment With Flask 

여기서 flask_app/server.py 가 내가 연습해 온 app.py 의 역할을 한다. 즉, flask에서 직접 server가 돌아가는 역할. <br>

flask_app/settings.py는 sets some basic params to give us more flexibility in the future. data_dir , labels, model_url, port 등. server에 import 된다. <br>











- https://imadelhanafi.com/posts/train_deploy_ml_model/#introduction


- https://towardsdatascience.com/build-a-docker-container-with-your-machine-learning-model-3cf906f5e07e

Using batch job on a single instance with AWS, NOT a web service with API endpoints, NOT distributed parallel jobs <br>
but good contents


- https://towardsdatascience.com/machine-learning-models-as-micro-services-in-docker-a798e1f068a5 

Workflow is well summarized but not specified explanation <br>

1.Build and train the model. <br>
2.Create an API of the model. (Here we have put it in a flask API).<br>
3.Create the requirements file containing all the required libraries.<br>
4.Create the docker file with necessary environment setup and start-up operations.<br>
5.Build the docker image.<br>
6.Now run the container and dance as you are done :)<br>


[REFERENCE]<br>
- https://towardsdatascience.com/build-a-docker-container-with-your-machine-learning-model-3cf906f5e07e
- https://www.kdnuggets.com/2019/03/deploy-pytorch-model-production.html


