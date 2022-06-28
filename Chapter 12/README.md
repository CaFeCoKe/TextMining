# Chapter 12. CNN을 응용한 문서 분류

- CNN (Convolutional Neural Network) : 합성곱 신경망이라고 불리는 CNN은 본래 시각적 영상을 분석하는 데 사용되는 모델이다. 기존 Fully-Connected Layer로 이루어진 인공 신경망의 입력 데이터는 1차원(배열) 형태로 한정되어 3차원인 이미지 정보를 1차원으로 축소시 정보가 손실이 생기게 된다. 
이로 인해 정확도를 높이는 것에 한계가 있다. 하지만 CNN은 이미지의 공간 정보를 유지한 상태로 학습이 가능한 모델이기 때문에 정확도가 FC로 이루어진 신경망에 비해 높다. <br><br>
  - Fully Connected Neural Network에 비해 가지는 차별성
    - 각 레이어의 입출력 데이터의 형상 유지
    - 이미지의 공간 정보를 유지하면서 인접 이미지와의 특징을 효과적으로 인식
    - 복수의 필터로 이미지의 특징 추출 및 학습
    - 추출한 이미지의 특징을 모으고 강화하는 Pooling 레이어
    - 필터를 공유 파라미터로 사용하기 때문에, 일반 인공 신경망과 비교하여 학습 파라미터가 매우 적음
  <br><br>
  - CNN의 구조<br><br>
  ![CNN](https://user-images.githubusercontent.com/86700191/176134232-f14e78d2-e309-4f0b-b1b7-a9c02b6f0542.png)
  <br><br>

- 자연어 처리에서의 CNN <br><br>
  - 입력 : 각 말뭉치는 임베딩 층(embedding layer)을 지나서 각 단어가 임베딩 벡터가 된다. 이 각각의 임베딩 벡터를 Matrix형태로 쌓은 상태를 보게 되면 다음과 같은 형태를 가지게 된다. (n : 문장의 길이, k : 임베딩 벡터의 차원)<br><br>
  ![1](https://user-images.githubusercontent.com/86700191/176142444-1fa97e97-2633-42ed-9069-ee4d6cada428.PNG)
  <br><br>
  흑백 이미지 데이터(채널이 1)와 같은 텐서 형태가 되어 CNN의 입력으로 쓸 수 있는 형태가 되어있다.
  <br><br>
  - 구조
  ![conv_maxpooling_steps](https://user-images.githubusercontent.com/86700191/176168128-78bfa753-55e0-4326-99c7-e7a9ff6cb147.gif)
  신경망의 구조는 이미지를 처리하는 것이나 자연어를 처리하는 것이나 동일하다. 차이점이 있다면 이미지를 처리하는 CNN은 두개의 축을 고려하기 때문에 보통 2D 필터를 쓰지만 자연어 처리에서의 CNN은 하나의 축만 고려하면 되기 때문에 1D 필터를 쓴다는 점이다.
  <br><br>