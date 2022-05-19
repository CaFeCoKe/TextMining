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
<br><br>
- 코사인 유사도 (cosine similarity) : 유사도 계산에 사용되는 척도. 두 벡터가 이루는 각도의 코사인값으로 정의된다.<br><br>
![cosine](https://user-images.githubusercontent.com/86700191/169231619-bdc3d90f-c59c-444a-9d14-b6f92114324c.PNG)
<br><br>
두 개의 벡터가 있을 때 크기는 중요하게 생각하지 않고 방향성만 비교한다는 뜻이 된다. 2차원 상의 벡터가 된다고 하면 각 문서는 단 두개의 단어 빈도로만 이루어져야 하며, 
그 두 단어의 빈도는 각각 x축과 y축이라고 할 수 있다.
<br><br>
- TF-IDF (Term Frequency-Inverse Document Frequency) : 직역 하면 단어빈도-역문서빈도로 해석된다. 카운트 대신 단어의 빈도에 그 단어가 출현한 문서 수의 역수를 곱했다는 뜻이다.<br><br>
![tf-idf](https://user-images.githubusercontent.com/86700191/169234403-b4a07a3e-5d01-4929-86f3-1039af41bf42.PNG)
<br><br>
모든 문서에 다 들어가 있는 단어는 별로 중요하지 않다는 의미를 카운트 벡터에 반영한 것이 바로 TF-IDF이다. 이 값은 단어가 나타난 문서의 수가 클수록 작아지게 되어 중요도가 낮아지게 된다.