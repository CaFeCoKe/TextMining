# Chapter 4. 카운트 기반의 문서 표현

- 카운트 기반 문서 표현 : 문서에 나타나는 단어의 통계를 이용하여 문서의 내용을 파악하는 것
- BoW (Bag of Word) : 단어들의 순서는 전혀 고려하지 않고, 단어들의 출현 빈도(frequency)에만 집중하는 텍스트 데이터의 수치화 표현 방법<br><br>

  ![BoW](https://user-images.githubusercontent.com/86700191/168757001-e81b3777-f143-41f2-b147-e9468cc513c5.png)
<br><br>

    - 희소 벡터 (sparse vector) : 대부분의 특성의 값이 0인 특성 벡터<br><br>

- BoW 기반의 특성 벡터 추출과정<br><br>
![feature](https://user-images.githubusercontent.com/86700191/168760569-6b2406fc-8420-420e-9210-81e37e9ed068.png)
<br><br>
- Sckikit-learn의 `CountVectorizer`를 이용한 특성 벡터 추출과정<br><br>
![scikit_feature](https://user-images.githubusercontent.com/86700191/168762743-ea8248af-f893-43ac-8f49-8b64d4cf2654.png)