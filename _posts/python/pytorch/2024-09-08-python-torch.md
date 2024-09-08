---
layout: single
title: "[Python] Pytorch"
categories: Python
tag: [python, pytorch]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# from torch_geometric.data import InMemoryDataset
주로 그래프 데이터를 다룰 때 사용됩니다. 이 클래스는 데이터셋을 메모리에 한 번에 로드하여, 이후 빠르게 접근할 수 있도록 하는 역할을 합니다.

## 일반적인 사용 패턴

InMemoryDataset을 상속받아 커스텀 데이터셋 클래스를 정의하고, 데이터를 로드하는 방법을 구현하는 것이 일반적입니다. 
이 과정에서 __init__, download, process 등의 메서드를 오버라이드하여 데이터셋의 로딩, 전처리, 다운로드 등의 기능을 구현할 수 있습니다.

