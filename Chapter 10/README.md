# Chapter 10. 딥러닝을 이용한 문서 분류

- 워드 임베딩 (Word Embedding) : 아래 그림과 같이 단어를 원핫 벡터(One-Hot Vector)로 표현하고 다시 짧은 길이의 밀집 벡터(Dense Vector)의 형태로 표현하는 방법이다.<br>
![word_embedding](https://user-images.githubusercontent.com/86700191/174529049-709e2782-cee7-4ea8-bc19-1e3a107f4623.jpg)
<br>
임베딩을 하는 이유로는 차원이 큰 원핫 벡터를 쓰면 연산이 비효율적이라는점, 대상 사이의 의미적 유사도를 계산할수 있다는 점, 단어가 의미적인 정보를 함축함으로써 연산이 가능하다는 점, 전이학습(transfer learning)이 가능하게 된다는 점이 있다.
<br><br>

- RNN (Recurrent Neural Networks) : 순환신경망이라고 불리는 RNN은 특정한 규칙성이나 패턴이 있는 시계열 데이터(값이 시간에 따라 변화하는 것)를 다루기 위한 모형으로 알려져 있다. 
일반적인 회귀모형이나 신경망은 입력값 사이에 순차적으로 미친 영향을 모형에 반영하지 못한다는 단점이 있는데 이것을 표현할 수 있는 모형이 바로 RNN이다.<br><br>
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

- LSTM (Long Short-Term Memory) : 장단기 메모리라고 불리는 LSTM은 RNN의 경사소실로 인한 장기 의존성 문제(the problem of Long-Term Dependencies)를 해결하기 위해 나온 RNN의 변형이다.<br><br>
  - LSTM의 구조<br><br>
  ![lstm](https://user-images.githubusercontent.com/86700191/174530129-b77cd015-58f9-4622-bfd2-2309c44396b1.png)
  <br><br>
   LSTM은 은닉층의 메모리 셀에 입력 게이트, 망각(삭제) 게이트, 출력 게이트를 추가하여 불필요한 기억을 지우고, 기억해야할 것들을 정한다. 요약하면 LSTM은 은닉 상태(hidden state)를 계산하는 식이 RNN보다 조금 더 복잡해졌으며 셀 상태(cell state)라는 값을 추가하여 RNN에 비해 긴 시퀀스를 처리하는 것에 성능이 좋다.<br><br>
      - 입력 게이트 : 현재 정보를 기억하기 위한 게이트<br><br>
        ![input](https://user-images.githubusercontent.com/86700191/174569946-29e790c0-4e9f-4050-8403-b184c24f52a6.PNG)
        <br><br>
      - 망각(삭제) 게이트 : 기억을 삭제하기 위한 게이트<br><br>
        ![forget](https://user-images.githubusercontent.com/86700191/174569952-226f5212-0458-424b-9be4-ab9e7a471224.PNG)
        <br><br>
      - 셀 상태 : 입력 게이트에서 선택된 기억을 삭제 게이트의 결과값과 더한 값이다. 삭제 게이트는 이전 시점의 입력을 얼마나 반영할지를 의미하고, 입력 게이트는 현재 시점의 입력을 얼마나 반영할지를 결정한다.<br><br>
        ![cell_state](https://user-images.githubusercontent.com/86700191/174569954-1154b577-9d2a-485c-84ea-e957328e820d.PNG)
        <br><br>
      - 출력 게이트(은닉 상태) : 출력 게이트는 현재 시점 t의 x값과 이전 시점 t-1의 은닉 상태가 시그모이드 함수를 지난 값이다. 셀 상태의 값이 하이퍼볼릭탄젠트 함수를 지나 출력 게이트의 값과 연산되면서, 값이 걸러지는 효과가 발생하여 은닉 상태가 되며 이 값은 출력층으로도 향한다.<br><br>
        ![output](https://user-images.githubusercontent.com/86700191/174569960-50193d33-44e7-49d9-a0f0-6797d6ac332b.PNG)
<br><br>

- GRU (Gated Recurrent Unit) : 게이트 순환 유닛이라고 불리는 GRU는 LSTM의 장기 의존성 문제에 대한 해결책을 유지하면서, 은닉 상태를 업데이트하는 계산을 줄인 모델이다.<br><br>
    - GRU의 구조<br><br>
    ![gru1](https://user-images.githubusercontent.com/86700191/174588187-67e9d2a3-f5bf-4c00-ba00-af98b3ca7afd.PNG)
    <br><br>
    GRU는 업데이트 게이트(이전의 정보(기억)을 얼마나 통과(유지)시킬지를 결정)와 리셋 게이트(이전의 정보를 얼마나 잊어야하는지를 결정) 두 가지 게이트만이 존재한다.
<br><br>

- Bidirectional RNN : 양방향 순환 신경망이라 불리우는 BRNN은 시퀀스의 과거의 값들 뿐만 아니라 이후의 값들에 의해서도 값이 결정될 수 있다는 점에서 나온 모델이다. 기존 RNN, LSTM, GRU는 지금까지 주어진 것을 보고 다음을 예측하는 것을 목표로 한 모델들이였기 때문에 예측하고자 하는 단어 뒤에 있는 정보를 이용할 수 없다는 한계점이 있었고 시퀀스의 이전부분 뿐만 아니라 이후 부분까지 결합하여 예측하기 위해 등장했다.<br><br>
  - BRNN의 구조<br><br>
  ![BRNN](https://user-images.githubusercontent.com/86700191/174601334-2ba9557b-4f9d-43a7-a38e-464697e7f8cc.png)
  <br><br>
  위와 같이 첫번째 토큰부터 시작하는 forward mode의 Unit과 맨 마지막에서 시작해서 끝에서 앞으로 가는 backward mode의 Unit의 출력(은닉 상태)을 합친다. 또한 이 유닛의 모델이 RNN이 아닌 LSTM이라면 Bi-LSTM, GRU이라면 Bi-GRU이 된다.