# Chapter 11. Word2Vec, ELMo, Doc2Vec의 이해

- 워드투벡터 (Word2Vec) : 단어 벡터 간 유의미한 유사도를 반영할 수 있도록 단어의 의미를 수치화 할 수 있는 방법중 하나이다.<br><br>
  - 희소 표현 (Sparse Representation) : 원-핫 인코딩을 통해서 얻은 원-핫 벡터는 표현하고자 하는 단어의 인덱스의 값만 1이고, 나머지 인덱스에는 전부 0으로 표현되는 벡터 표현 방법이다. 이와 같이 벡터 또는 행렬의 값이 대부분이 0으로 표현되는 방법을 희소 표현이라 한다.<br>
이러한 표현 방법은 각 단어 벡터간 유의미한 유사성을 표현할 수 없다는 단점이 있다.<br><br>
  - 분산 표현 (Distributed Representation) : 단어의 의미를 다차원 공간에 벡터화하는 방법을 사용하는데 이러한 표현을 분산 표현이라 한다. 기본적으로 분포 가설(distributional hypothesis)이라는 가정 하에 만들어진 표현 방법이며, 이 가정은 '비슷한 문맥에서 등장하는 단어들은 비슷한 의미를 가진다' 라는 것이다.<br>
원-핫 벡터의 차원이 단어 집합(vocabulary)의 크기인것과 달리 분산 표현으로 임베딩 된 벡터는 차원이 단어 집합의 크기가 될 필요가 없이 사용자가 설정한 차원의 수를 가지는 벡터가 된다.<br>
요약하자면 희소 표현이 고차원에 각 차원이 분리된 표현 방법이었다면, 분산 표현은 저차원에 단어의 의미를 여러 차원에다가 분산하여 표현하는 방법이다. 이런 표현 방법을 사용하면 단어 벡터 간 유의미한 유사도를 계산할 수 있게 된다.<br><br>
  - 학습 방식
    - CBOW (Continuous Bag of Words) : 주변에 있는 단어들을 입력으로 중간에 있는 단어들을 예측하는 방법이다.<br><br>
    ![cbow](https://user-images.githubusercontent.com/86700191/174987777-a32389f2-151a-4e28-993e-371c14426359.PNG)
    <br><br>
    여러 개의 단어가 있기 때문에, 은닉층에서 입력 벡터와 행렬 W의 곱으로 구성된 단어 벡터의 평균을 구하게 된다. 이는 분산된 많은 정보에 대해 평활화 시키기 때문에 작은 데이터 세트에 대해 성능이 좋다고 할 수 있다. 
    또한, Word2Vec의 은닉층은 일반적인 은닉층과는 달리 활성화 함수가 존재하지 않으며 룩업 테이블이라는 연산을 담당하는 층으로 투사층(projection layer)이라고 부르기도 한다.<br><br>
    - Skip-gram : 중심 단어들을 입력으로 주변 단어들을 예측하는 방법이다.<br><br>
    ![Skip-gram](https://user-images.githubusercontent.com/86700191/174987771-8d11d67c-5860-4288-ab65-cb7d67b83d1b.png)
    <br><br>
    CBOW와는 반대의 구조이며, 한개의 중심 단어에 대해서 주변 단어를 예측하므로 은닉(투사)층에서 벡터들의 평균을 구하는 과정은 없다. 보통 CBOW보다 성능이 좋다고 알려져 있다.
<br><br>
- ELMo (Embeddings from Language Model) : 언어 모델로 하는 임베딩 방법인 ELMo의 가장 큰 특징은 사전 훈련된 언어 모델(Pre-trained language model)을 사용한다는 점이다. 기본 아이디어로는 같은 표기의 단어라도 문맥에 따라서 다르게 워드 임베딩을 할 수 있으면 자연어 처리의 성능을 올릴 수 있을 수 있다는 점이며, 이를 문맥을 반영한 워드 임베딩(Contextualized Word Embedding).이라 한다. <br><br>
  - Word2Vec의 단점 : 동음이의어의 문제가 크다. 언어는 같은 단어여도 문맥에 따라 다른 의미를 보여주는 단어들이 있는데, Word2Vec은 이를 모두 동일한 벡터로 처리하게 되어 전혀 다른 의미임에도 불구하고 같은 의미로 처리 된다는 점이다.<br><br>
  - ELMo의 구조 : 기본적으로 biLM(Bidirectional Language Model)으로 사전 학습을 한다. biLM 중 Bi-LSTM과 비슷한 사전 학습을 하게 되는데 이 차이점은 순방향, 역방향 은닉층을 concat 시키는 Bi-LSTM 구조가 아닌 2개의 순방향, 역방향 언어 모델을 각각 학습시키는 구조로 되어 있다<br><br>
    - ELMo의 biLM 과 Bi-LSTM의 차이점 (갈색 박스 부분)<br><br>
    ![ELMo](https://user-images.githubusercontent.com/86700191/175290222-7a710323-8e1c-4a1c-9de8-a76303dcbeb0.PNG)
    <br><br>
    ![2-Bi-LSTM](https://user-images.githubusercontent.com/86700191/175290282-094bd908-685a-4c89-880b-7169689ae9dc.png)