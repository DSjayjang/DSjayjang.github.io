---
layout: single
title: "[Python] hydra"
categories: Python
tag: [python, hydra]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Hydra
- to override default parameters

main.py에는 import 해주고, main function위에다가 hydra 호출해야함 configuratiuon load가 필요하다는걸 알려주기 위해

```py
e.g.
import hydra

@hydra.main(config_path = 'conf', config_name = 'config')
# config_path는 conf 폴더이름
# config_name은 config.py
```


```py
e.g. digress
@hydra.main(version_base='1.3', config_path='../configs', config_name='config')
```

![1]({{site.url}}/images/python/hydra/1.png)

![1]({{site.url}}/images/python/hydra/2.png)

- default:로 디폴트 설정이 가능함
- geranl / model / train / dataset은 폴더 이름
- 값들은 yaml 파일 (dataset도 yaml 파일)
- run의 dir 값은 결과물로 output 폴더에 생성될 파일을 말함