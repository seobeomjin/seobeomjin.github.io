---
layout: post 
title: Docker QuickStart [1]
date: 2020-04-13
description: 도커 퀵스타트를 진행하던 중 만난 어려움 
comments: true 
published : false
---



<a href = "https://docs.docker.com/get-started/part2/"><b>Docker QuickStart</b></a>를 진행하던 중, 만난 어려움이 있어 이 부분을 공유해 보려 한다. 최근 Docker를 통해 구현을 하고 싶은 것이 있어 Docker를 공부 중이다. 현재 Windows 기반에서 Virtual Box 위에서 Docker 실습을 진행 중이다. 

dockerfile의 구성은 아래와 같다.

![docker file]({{site.url}}/assets/img/post_img/Docker/[1]/dockerfile.jpg)
<img src="{{ '/../assets/img/post_img/Docker/[1]/dockerfile.JPG' | prepend: site.url }}" alt=""/> 
<figcaption> [dockerfile] </figcaption>






- **FROM**은 해당 도커파일이 시작할 때 기존에 존재하던 "node:current-slim" 이미지를 활용함을 의미한다. 
- **WORKDIR**은 앞으로의 action들이 image filesystem 안에서 어떤 directory 안에서 수행될 것인지를 지정해준다. 
- **COPY**는 host로부터 current location으로 복사를 해준다. 
- **RUN**은 image filesystem 안에서 수행할 동작을 명시한다. 
- **EXPOSE**는 container가 어떤 port와 연결되어있는지를 Docker에 알려준다. 
- **CMD**는 container가 실행 시, command를 실행한다. 

위와 같이 도커 파일을 확인 후, 다음과 같은 과정을 거쳤다. 

```bash
docker build --tag bulletinboard:1.0 
# docker image 생성 

docker run --p 8000:8080 -d --name bb bulletinboard:1.0 
# start a container based on my image 
#--p 포트연결 / --d background에서 실행 / --name naming 을 의미 

docker rm --force bb 
# delete container
# --force는 running 중인 container 를 지울 때 사용된다. 
# 'docker stop bb'를 통해 정지 후 삭제시킨다면, --force 옵션을 사용할 필요가 없다.  
```

Docker 홈페이지의 bullerin-board를 가져와 localhost에서 실행시키는 중 첫 번째 어려움을 봉착했다. 

![docker ps]({{site.url}}/assets/img/post_img/Docker/[1]/docker-ps.jpg)
<img src="{{ '../assets/img/post_img/Docker/[1]/docker-ps.JPG' | prepend: site.url }}" alt=""/>
<figcaption> [docker ps] </figcaption>

*docker ps* 를 통해 확인해 보면 위와 같은 docker container가 실행 되고 있음을 확인할 수 있다. 브라우저에 'localhost:8000'을 입력해도 원하는 결과가 출력되지 않았다. 알고보니, docker-machine의 IP를 사용했어야 했다. 문제 해결에는 https://github.com/docker/for-win/issues/204 해당 링크를 참고하였다.  

```bash
docker-machine ip 
```
docker-machine 의 ip가 위의 입력을 통해 출력되면, **'ip result:8000'**을 입력하는 것이 해결방법이었다. 정상적인 경우, 아래와 같은 출력을 얻게 된다. 

![docker ps]({{site.url}}/assets/img/post_img/Docker/[1]/bulletinboard-output.jpg)
<figure>
	<img src="{{ '../assets/img/post_img/Docker/[1]/bulletinboard-output.PNG' | prepend: site.url }}" alt=""/> 
	<figcaption> [bullerinboadrd-output] </figcaption>
</figure>



