# Chapter 10. 딥러닝을 이용한 문서 분류

- 워드 임베딩 (Word Embedding) : 아래 그림과 같이 단어를 원핫 벡터(One-Hot Vector)로 표현하고 다시 짧은 길이의 밀집 벡터(Dense Vector)의 형태로 표현하는 방법이다.
![word_embedding](https://user-images.githubusercontent.com/86700191/174529049-709e2782-cee7-4ea8-bc19-1e3a107f4623.jpg)
<br>
임베딩을 하는 이유로는 차원이 큰 원핫 벡터를 쓰면 연산이 비효율적이라는점, 대상 사이의 의미적 유사도를 계산할수 있다는 점, 단어가 의미적인 정보를 함축함으로써 연산이 가능하다는 점, 전이학습(transfer learning)이 가능하게 된다는 점이 있다.
<br><br>

- RNN (Recurrent Neural Networks) : 순환신경망이라고 불리는 RNN은 특정한 규칙성이나 패턴이 있는 시계열 데이터(값이 시간에 따라 변화하는 것)를 다루기 위한 모형으로 알려져 있다. 
일반적인 회귀모형이나 신경망은 입력값 사이에 순차적으로 미친 영향을 모형에 반영하지 못한다는 단점이 있는데 이것을 표현할 수 있는 모형이 바로 RNN이다.
  - RNN의 구조<br><br>
    ![rnn (1)](https://user-images.githubusercontent.com/86700191/174526883-dc1f3220-e39d-4ce3-89e6-29f40053f966.png)
    <br><br>
    이 그림을 식으로 표현하면 아래와 같다.<br><br>
    ![rnn_math](https://user-images.githubusercontent.com/86700191/174527153-07fb45e0-a2a1-4d86-bf32-5091078b8937.PNG)
    <br><br>
    앞의 값들은 은닉층에 있는 노드를 통해 다음 상태에 영향을 미친다. t-1 시간대의 입력값은 t시간대의 은닉노드에 영향을 미치게 되고 다시 t시간대는 t+1시간대에 영향이 미치게 되어 의존성이 앞에서부터 축적된다고 볼 수 있다.
    <br><br>
  - RNN이 문서 분류에 적합한 이유 : 문맥을 이해하는 것이 시계열 데이터와 비슷하다는 점이다. 말은 대체로 순차적으로 들으며 의미를 이해하게 되는데 앞 단어로부터 문맥에 관한 정보가 마지막 노드까지 순차적으로 축적되면 그 정보로 문서를 분류하면 된다.
<br><br>

- LSTM (Long Short-Term Memory) : 장단기 메모리라고 불리는 LSTM은 RNN의 경사소실로 인한 장기 의존성 문제(the problem of Long-Term Dependencies)를 해결하기 위해 나온 RNN의 변형이다.
  - LSTM의 구조<br><br>
  ![lstm](https://user-images.githubusercontent.com/86700191/174530129-b77cd015-58f9-4622-bfd2-2309c44396b1.png)
  <br><br>
   LSTM은 은닉층의 메모리 셀에 입력 게이트, 망각(삭제) 게이트, 출력 게이트를 추가하여 불필요한 기억을 지우고, 기억해야할 것들을 정한다. 요약하면 LSTM은 은닉 상태(hidden state)를 계산하는 식이 RNN보다 조금 더 복잡해졌으며 셀 상태(cell state)라는 값을 추가하여 RNN에 비해 긴 시퀀스를 처리하는 것에 성능이 좋다.
      - 입력 게이트
      - 망각(삭제) 게이트
      - 셀 상태
      - 출력 게이트(은닉 상태)
<br><br>

- GRU (Gated Recurrent Unit) :