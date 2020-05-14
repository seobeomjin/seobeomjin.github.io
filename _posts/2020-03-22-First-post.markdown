---
layout: post
title:  "First Post"
date:   2020-03-22
description: github.io를 개설해보았습니다. 
comments: true
---

<p> 2020년 3월 22일, 명확한 봄 날씨의 일요일이다. 현재 나는 독일에서 COVID19로 인해 stay-home을 실천하고 있다. (상황이 하루 빨리 나아지기를 기원한다.) 오늘은 머릿속으로 계획해왔던 홈페이지 개설을 해 볼 생각이었고 실제로 그랬다. 여러 구글링의 게시글들을 따라하다 보면 꽤나 금방 해결될 것이라 생각되었는데 생각보다 오래 걸렸다. 윈도우에서 Jekyll을 다루는 부분에서 굉장히 어려웠고 (Error를 항상 꼼꼼히 읽고 해결책도 꼼꼼히 읽어보자는 교훈을 얻었다.) 결국은 WSL을 이용해 해낼 수 있게 되었다. WSL을 듣기만 해보았지, 여기서 bash창을 처음 써보지만 아직까지는 불편함이 없다.  </p>

오늘은 오전 11시 경부터 저녁 때까지 이 블로그를 구축하기 위해 많은 시간을 들였다. 그런 시간을 들인 만큼 어느 부분이 어려웠는지에 대해 언급하고 넘어가보려 한다. 

<h3>1. "Can't find gem bundler"</h3> <a href ="http://jekyllthemes.org"><b> 지킬 테마들</b></a>이 collection되어 있는 사이트에서 마음에 드는 깔끔하고 실용적이라 느끼는 테마들을 찾아 나섰다. 몇 개의 테마들은 **bundle** 명령어를 입력하며 계속 오류가 떴었는데 그 중 한번은 version compatibility가 맞지 않았기 때문이다.  이러한 경우, Gemfile.lock의 bundler version을 확인해준 뒤, 해당 버전에 맞는 부분을 재설치 해주어야 한다. 
```bash
cat Gemfile.lock | grep -A 1 "BUNDLED WITH" 
sudo gem install bundler -v 'printed version'
```
위의 경우를 통해 해결 가능 했다. 

<h3>2. "jekyll serve 앞에는 bundle exec을 함께"</h3> jekyll serve 만 실행시키니 Error가 발생했었는데, 그것을 캡쳐해두지 못해 명확한 이유는 기억이 나지 않는다. 유츄해 봤을 때, jekyll은 Gemfile에 dependency를 가지고 있으니, "bundle exec"을 함께 실행 시키는 것으로 보인다. 
```bash
bundle exec jekyll serve 
``` 
따라서 위의 명령을 통해 블로그를 로컬에서 미리 확인할 수 있었다. 

<!--<img src="{{ '/assets/img/touring.jpg' | prepend: site.baseurl }}" alt="">--> 

블로그를 나름대로 생성하고 나니, 깔끔하게 관리해야 겠다는 생각이 든다. 주로 공부에 관한 내용들이 올라오겠지만, 일상적인 내용들도 분류하여 함께 올려보고는 할 생각이다. 
