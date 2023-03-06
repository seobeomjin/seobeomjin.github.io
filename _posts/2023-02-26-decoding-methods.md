---
layout: post
title: Decoding Methods For Language Generation 
subtitle: greedy search, beam search, sampling, top-k sampling, top-p (nucleus) sampling 등을 정리합니다. 
categories: Study  # [Paper-review, Study] 
tags: nlp decoding-strategy
comments: True
published: False
---

- All of the following functionalities can be used for auto-regressive language generation (GPT2, XLNet, OpenAi-GPT, CTRL, TransfoXL, XLM, Bart, T5 in both PyTorch and Tensorflow >= 2.0!) In short, auto-regressive language generation is based on the assumption that the probability distribution of a word sequence can be decomposed into the product of conditional next word distributions:

# Greedy Search 
Greedy search simply selects the word with the highest probability as its next word: 
w_t = argmax_w P(w|w_1:t-1) at each timestep t. 
![img](/assets/images/decoding-methods/greedy_search.png)
P(The, nice, woman) = 0.5 * 0.4 

```python
# encode context the generation is conditioned on
input_ids = tokenizer.encode('I enjoy walking with my cute dog', return_tensors='tf')

# generate text until the output length (which includes the context length) reaches 50
greedy_output = model.generate(input_ids, max_length=50)

print("Output:\n" + 100 * '-')
print(tokenizer.decode(greedy_output[0], skip_special_tokens=True))

Output:
----------------------------------------------------------------------------------------------------
I enjoy walking with my cute dog, but I'm not sure if I'll ever be able to walk with my dog. I'm not sure if I'll ever be able to walk with my dog.

I'm not sure if I'll
```
( I enjoy walking with my cute dog ) 이후의 생성. 말이 되지만 반복적인 단어들을 생성했다. 
이는 generation 에서 꽤 빈번한 문제이고, greedy 와 beam saerch에서는 더욱 빈번하다.

Greedy search의 단점은 highest prob 에 가려서 다른 확률의 경우를 보지 못한다는 경우이다. 
위의 figure에서 보더라도, (The, dog, has) 의 경우 0.4*0.9 로, 0.2보다 큰 값을 얻는다. 
이런 단점을 Beam Search가 보완할 수 있다.

# Beam Search 
... reduces the risk of missing hidden high probability word sequences by keepint the most likely num_beams of hypotheses at each time step and eventually choosing the hypothesis that has the overall highest probability.

![img](/assets/images/decoding-methods/beam_search.png)

but is not guaranteed to find the most likely output.

```python
# activate beam search and early_stopping
beam_output = model.generate(
    input_ids, 
    max_length=50, 
    num_beams=5, 
    early_stopping=True # generation is finished when all beam hypotheses reached the EOS token.
)

print("Output:\n" + 100 * '-')
print(tokenizer.decode(beam_output[0], skip_special_tokens=True))

Output:
----------------------------------------------------------------------------------------------------
I enjoy walking with my cute dog, but I'm not sure if I'll ever be able to walk with him again.

I'm not sure if I'll ever be able to walk with him again. I'm not sure if I'll

```
repetition 발생 -> 해결책은 n-grams penalty
A simple remedy is to introduce n-grams (a.k.a word sequences of n words) penalties
~
Nevertheless, n-gram penalties have to be used with care. An article generated about the city New York should not use a 2-gram penalty or otherwise, the name of the city would only appear once in the whole text!
~
~
beam saerch 는 boring 하다는 특성이 있다. 
따라서 좀 더 randomness를 줘보자. 


# Sampling 

# top-k sampling 

# top-p (nucleus) sampling 

# Reference 
- https://littlefoxdiary.tistory.com/46
- https://huggingface.co/blog/how-to-generate?fbclid=IwAR19kbEiW_sF19TeSr4BE4jQZSIqz0GzOFD2013fIGEH32DReW9pAFq6vDMs