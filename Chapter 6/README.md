# Chapter 6. 차원 축소

- 차원의 저주 (Curse of Dimensionality) : 차원이 증가하면서 학습데이터 수가 차원 수보다 적어져서 정확히는 관측치보다 변수 수가 많아지는 경우 성능이 저하되는 현상이다. 
차원이 증가할수록 변수가 증가하고, 점점 데이터 간 거리가 멀어지는데 이로 인해 생기는 빈공간은 모두 0으로 채워져 데이터 간 거리에 기반한 모델의 경우 성능이 저하될 수밖에 없다.<br><br>
  - 차원의 저주를 해결하는 방법
    - 데이터를 충분히 늘리기 : 차원의 저주 문제를 해결하기 위한 이론적인 해결책이다. 훈련 샘플의 밀도가 충분히 높아질 때까지 데이터를 모아서 훈련 세트의 크기를 키우는 방법이나 
일정 밀도에 도달 하기 위해 필요한 훈련 샘플의 수는 차원의 크기가 늘어남에 따라 기하급수적으로 늘어나 현실적인 방법이 될 수 없다.<br><br>
    - 차원 축소 : BoW로 표현한 문서의 특성 수를 줄임으로써 차원을 축소하는 것이다.
      - 특성 선택 : 현재 있는 특성들 중 대표 특성을 선택하여 나머지 특성의 계수를 0으로 만드는 방법이다. 계수를 0으로 만들면 그 특성은 결과에 영향을 미치지 못한다.
      - 특성 추출 : 기존의 특성 값을 조합하여 새로운 특성을 생성하는 방법이다. 이 새로운 특성은 기존 특성들의 선형 결합으로 표현 되며, PCA나 LSA와 같은 방법이 있다.<br><br>

- PCA (Principal Component Analysis) : 주성분 분석이라 불리며 데이터의 분산을 최대한 보존하는 새로운 축을 찾아 변환하여 차원을 축소하는 방법이다. <br><br>
![image](https://user-images.githubusercontent.com/86700191/172035064-1519b470-9d2c-4aa8-994d-5e75f9c013f3.png)
<br><br>
좌측은 간단한 2차원 데이터셋이고 위에 3개의 축이 표시되어 있다. 우측은 각 축이 1차원에 투영된 결과이다. 가장 위의 실선이 분산을 최대로 보존하고 있고 맨 마지막의 점선은 분산을 가장 적게 보존하고 있다.
원본데이터셋과 투영된 데이터 셋 사이의 평균제곱거리를 최소화하는 축 (원본 데이터의 분산이 최대한 보존이 되는 축)을 선택하기 때문에 이 데이터셋의 첫번째 축(주성분)은 C1이다. 이러한 기법을 이용하는 것이 PCA이다.<br><br>
  - PCA 알고리즘의 작동법
    1. 훈련 세트에서 분산이 최대인 축 찾기
    2. 1번 축에 직교하면서 남은 분산을 최대한 보존하는 두번째 축 찾기
    3. 2번 축에 직교하면서 남은 분산을 최대한 보존하는 세번째 축 찾기
    4. 위의 단계를 반복하면서 데이터셋에 있는 차원의 수만큼 n번째 축 찾기
    5. 주성분을 모두 추출한 후 처음 d개의 주성분으로 정의한 초평면에 투영해 데이터셋을 d차원으로 축소<br><br>

- LSA (Latent Semantic Analysis) : 잠재 의미 분석이라 불리며 기본적으로 DTM이나 TF-IDF 행렬에 절단된 SVD(truncated SVD)를 사용하여 차원을 축소시키고, 단어들의 잠재적인 의미를 끌어내는 방법이다. <br><br>
  - SVD (Singular Value Decomposition) : 특이값 분해라고 불리며 실수 벡터 공간에 한정하여 내용을 설명한다. 그리고 다음과 같이 A가 m × n 행렬일 때, 다음과 같이 3개의 행렬의 곱으로 분해(decomposition)하는 것을 말한다.<br>
  ![svg](https://user-images.githubusercontent.com/86700191/172538628-fbe3de32-1b91-40d5-bd7e-f0378fc83aee.PNG) <br>
  ![svg2](https://user-images.githubusercontent.com/86700191/172538634-ee93f20b-8695-4511-87c1-8536ccd1b5ae.PNG)
    - 절단된 SVD (Truncated SVD) : 위의 SVD를 풀 SVD (full SVD)라고 한다. LSA에서는 절단된 SVD를 사용한다.<br><br>
    ![T-SVD](https://user-images.githubusercontent.com/86700191/172539670-f41fd8cb-b583-4293-8e8c-d0f545915a07.PNG)
    <br><br>
    대각 행렬 Σ의 대각 원소의 값 중에서 상위값 t개만 남게 된다. 절단된 SVD를 수행하면 값의 손실이 일어나므로 기존의 행렬 A를 복구할 수 없게 되며, U행렬과 V행렬도 t열까지만 남긴다. 여기서 t는 우리가 찾고자하는 토픽의 수를 반영한 하이퍼파라미터값이다. <br>
    일부 벡터들을 삭제하는 것을 데이터의 차원을 줄인다고도 말하는데, 데이터의 차원을 줄이게되면 풀 SVD를 했을 때보다 직관적으로 계산 비용이 낮아지는 효과를 얻을 수 있다.
    또한, 계산 비용이 낮아지는 것 외에도 상대적으로 중요하지 않은 정보를 삭제하는 효과를 갖고 있는데 NLP에서는 설명력이 낮은 정보를 삭제하고 설명력이 높은 정보를 남긴다는 의미를 갖고 있다.
  <br><br>
  - 장점 
    - 구현이 빨라서, 빠르게 계산할 때 용이하다.
    - 문서의 유사도 계산에서 좋은 성능을 보여준다.
<br><br>
  - 단점
    - 새로운 data에 대해 업데이트가 어렵다. (->이로 인해 단어의 의미를 벡터화 할 수 있는 RNN, Word Embedding 등이 각광을 받게 됨)
