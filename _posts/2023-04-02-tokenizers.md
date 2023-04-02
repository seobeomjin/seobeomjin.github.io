---
layout: post
title: Tokenizer Summary (in progress)
subtitle: BPE, WordPiece, SentencePiece tokenizer 를 정리합니다 .
categories: Study  # [Paper-review, Study] 
tags: tokenizer nlp 
comments: True
published: True
---

## Intro 
- 분절 규칙의 update 과정 
    공백 분절 -> 구두점 및 여러 symbol들이 포함됨 -> 구두점 분절 -> ex) [Don, ', t] 와 같이 분절이 됨 -> new rule 이 필요하다! 
- BERT style tokenizer doesn't fit to the GPT model input 
- Transformer XL 은 공백/구두점을 기준으로 분절 수행 -> vocab size = 267,735 개 
    - large size embedding matrix -> memory 이슈가 발생할 수도 있음
      (Adaptive Embedding 으로 일부는 해소)
- word 기반 tokenizer 
    word representation 의미를 잘 담고 있지만, vocab size가 커지고, memory 이슈가 발생할 수 있음
- char 기반 tokenizer
    vocab 사이즈는 작아서 memory 이슈는 적겠지만, word 의 의미가 깨져서 학습 성능을 저하함
- subword 기반 tokenizer 의 등장 
    - word 기반 tokenizer 와 char 기반 tokenizer 사이의 중간 지점. 
    - 자주 등장하는 word는 그대로 두고, 자주 등장하지 않지만 의미를 가진 부분을 sub-word로 표현 
    - 장점
        -> 적절한 vocab size 구성 가능 & word representation 학습 가능 
        -> 훈련과정에서 만나지 않은 단어도 분절가능 
    - corpus 를 통해 분절 규칙을 훈련을 시키고, vocab을 구성해야 함 
    - ex) BPE tokenizer, WordPiece tokenizer, Unigram tokenizer, SentencePiece tokenizer 


## Byte Pair Encoding Tokenizer (feat.GPT3)
- **HOW TO MAKE VOCABS**
    1. corpus를 단어 단위(or rule 기반)로 pre-tokenize 해주고, 단어들을 1 charater로 split 함. (-> 초기 vocab 구성) 
    2. bi-pair window를 sliding 하며 각 pairs freqeuncy 를 계산함. 
        (특정 단어들이 얼마나 자주 등장하는지도 따라서 중요하다. 자주 등장하는 단어 내의 pair는 빈도가 높아질테니)
    3. 가장 빈번하게 등장하는 pair를 vocab에 추가해줌 & merge rule 에 추가해줌 
    4. splits 에서 해당 빈번한 pair가 update됨 (2 chars split 이 등장) 
    ---
    5. 2번, 3번에서와 같이 가장 pairs freq 를 계산하고, vocab에 추가해줌 
    6. 4번과 같이 splits이 업데이트 됨 
    7. vocab size가 desired size가 될 때까지 반복함

- **HOW TO TOKENIZE A WORD using trained tokenizer**
    1. “hugs” 라는 단어가 들어옴. char 단위로 split 해줌 
    2. merge rule에 따라서 merge 될 수 있는 token들을 반복해줌 
        1. 위의 예시에서는 h+u → hu 로 , [hu, g, s] 가 됨 
        2. hu+g → hug 로, [hug, s] 가 됨. 
    3. merge rule을 다 거쳐서 [hug, s] 가 됨. 
    4. 만약 vocab에 없는 token이 나올 경우, [UNK] 의 unknown token 이 생성됨.

## byte-level BPE tokenizer 

## Word Piece Tokenizer (feat.BERT)
- **HOW TO MAKE VOCABS**
    1. corpus를 단어 단위(or rule 기반)로 pre-tokenize 해주고, 각 단어들을 char 단위로 split 함. 
        단어의 맨 앞에 오는 char은 간단히 쓰고, 단어의 중간과 끝은 앞에 “##”을 삽입해서 이어지는 부분임을 표시 → (초기 vocab 구성) 
        "##" 심볼은 해당 심볼을 지닌 토큰은 해당 토큰 이전에 등장한 토큰과 공백 없이 합쳐져야 한다는 의미를 가짐. 
    2. 순서대로의 bi-pair window가 sliding 하면서 score를 계산함
        score  = ([1,2]-bi-pair 등장 횟수) / { (첫 번째 split 등장 횟수) * (두 번째 split 등장 횟수) }  를 계산함 
    3. highest score 를 가지는 bi-pair 를 vocab에 추가해줌 
    4. 새로운 vocab을 기준으로 splits 를 재구성 ( 2개 이상의 char 조합이 하나의 split이 됨) 
    5. 2,3,4번을 desired vocab size를 만족할 때까지 반복함

- **HOW TO TOKENIZE A WORD using trained tokenizer**
    1. “huggingface” 라는 단어가 들어옴. char 단위로 split 해줌 
    [h, ##u, ##g, ##g, ##i, ##n, ##g, ##f, ##a, ##c, ##e] 
    2. 가장 앞 부분부터 vocab 내에서 매칭될 수 있는 가장 긴 token과 matching 시킴 
    [h, ##u, ##g, ##g, ##i, ##n, ##g, ##f, ##a, ##c, ##e] 
    → [huggi, ##n, ##g, ##f, ##a, ##c, ##e] 
    → [huggi, ##n, ##gfac, ##e]
    (vocab 내에 위와 같은 token들이 있다고 가정)
    3. 만약 vocab에 없는 token이 나올 경우, [UNK] 의 unknown token 이 생성됨.

## Sentence Piece Tokenizer


## Unigram Tokenizer 


## Summary 
- 즉, tokenizer 를 학습시키는 것은, 주어진 corpus를 활용헤ㅐ 거기서 vocab을 만들고, vocab을 활용하여 tokenizing rule을 배우는 것과 같다. 

- Tokenizer 는 기본적으로 tokenizing 즉 단어를 나누는 역할을 하고 (이때 토크나이제이션 기법을 뭘 쓰냐에 따라 나뉘는 방법이 다름) 
- Encoding 이라 하면, 그에 맞게 mapping 되는 lookup table index를 내줌 
- Decoding 하면 다시 그 단어로 변환된 값을 줌

- tokenizer = Tokenizer.from_file("data/tokenizer-wiki.json")
    - 이건 이미 wiki를 통해 학습된, configuration 과 vocab이 들오있게 되는 것임 
    - 그 학습된 tokenizer를 그대로 불러와서 이 vocab과 merge rule 같은 걸로 unseen text 를 tokenizing 할 수 있는 것임

    
## Reference 
- <a href="https://www.youtube.com/watch?v=HEikzVL-lZU"> Byte Pair Encoding Tokenization </a><br>
- <a href="https://www.youtube.com/watch?v=HEikzVL-lZU"> WordPiece Tokenization </a><br>
- <a href="https://huffon.github.io/2020/07/05/tokenizers/"> HuggingFace 내 토크나이저 종류 살펴보기 </a><br>