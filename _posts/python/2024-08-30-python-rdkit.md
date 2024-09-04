---
layout: single
title: "[Python] RDKit"
categories: Python
tag: [python, rdkit]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# rdkit
- smiles를 통해 분자구조를 표현

```py
!pip install rdkit
> import rdkit

# 분자 구조 표현
Chem.MolFromSmiles('SMILES data')
```

```py
분자구조에 인덱스 추가
> IPythonConsole.drawOptions.addAtomIndices = True
```

# 연습

```py
# e.g.
mol = Chem.MolFromSmiles('CC1=CC(CCC1)Br')
mol

# 분자 구조에 원소 인덱스 추가
def mol_with_atom_index(mol):
    for atom in mol.GetAtoms():
        atom.SetAtomMapNum(atom.GetIdx())
    return mol
mol = Chem.MolFromSmiles('CC1=CC(CCC1)Br')
mol_with_atom_index(mol)
```