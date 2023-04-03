---
layout: post
title: Pytorch Randomness Control하기
subtitle: Pytorch Randomness Control 에 대해서 정리합니다. 
categories: Study  # [Paper-review, Study] 
tags: pytorch reproductivity randomness
comments: True
published: True
---

## Summary
- 핵심 요약을 하면 아래 코드와 같다. 
```python
torch.manual_seed(random_seed)
torch.cuda.manual_seed(random_seed)
torch.cuda.manual_seed_all(random_seed) # if use multi-GPU
torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False
np.random.seed(random_seed)
random.seed(random_seed)
```

## Reference 
- <a href="https://hoya012.github.io/blog/reproducible_pytorch/"> Reproducible PyTorch를 위한 randomness 올바르게 제어하기! </a><br>