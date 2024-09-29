---
tags:
  - AI
  - concepts
---
- 어떤 형태로든, 데이터를 활용하기 위해서는 이를 '수'로 바꿔야함
## Word Embedding
- 각 단어를 $R^n$의 벡터로 표현함
- 각 단어 벡터를 dictionary 형태로 사용함
- 차원이 높을수록 다양한 정보를 담을 수 있으며, 학습 전략에 따라 다른 의미를 내포함

## Training Strategy
- 특정 task의 모델을 개발 후, 맨 처음 레이어만 분리해서 사용
### CBoW
- 주변 단어 -> 중심 단어 예측
### Skip-gram
- 중심 단어 -> 주변 단어 예측