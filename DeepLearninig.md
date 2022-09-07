# 딥러닝
- 여러 층을 가진 인공신경망을 사용하여 머신러닝 학습을 수행


<br/>


## 인공신경망(Aritificial Neural Network)
- 인간의 뇌가 가지는 생물학적 특성 중 뉴런의 연결 구조를 가리키는 신경망을 네트워크 구조로 구현한 것
  ![image](https://user-images.githubusercontent.com/86597163/181756679-db75de62-3432-44d1-a8e5-7a20cf56825f.png)

  > 입력층을 통해 데이터 입력
  >
  > 여러 단계의 은닉층을 지나며 출력층을 통해 결과 출력

<br/>

## 퍼셉트론(perceptron)
![image](https://user-images.githubusercontent.com/86597163/181756731-8337bb4d-0a1c-4526-89fe-3250facd3073.png)
- 두 종류의 클래스를 직선으로 분류하는 선형 분류기
- 로젠블라트 : 입력층과 출력층만으로 구성된 단층 퍼셉트론 개념 제안
- 다층 퍼셉트론(MLP) : 단층 퍼셉트론을 조합하여 복잡한 비선형 문제 해결


<br/>


## 오차 역전파
![image](https://user-images.githubusercontent.com/86597163/181396766-3e832484-9637-49cd-a60b-3e449a957b5a.png)
- mlp(multi layer perceptron)를 학습시킬 수 있는 알고리즘
- 각 오차를 더해 네트워크 뒤로 전달하여 w를 갱신시키는 과정
- 역전파는 각 노드가 최종 값에 얼마나 영향을 주었는지 판단하고 그 값에 맞게 가중치에 영향을 줄 수 있게 함
- w5를 업데이트 시키는 방법 : w5값에서 Etotal을 w5로 미분한 값 x 학습률을 빼줌


<br/>

## 기울기 소실
- 깊은 레이어를 가진 신경망의 경우 입력층으로 갈수록 역전파 과정에서 미분값이 사라지며 학습이 안되는 현상
  
  <br/>

  ![함수](https://wikidocs.net/images/page/163752/Fig_6.png)

- 시그모이드 함수의 영향
  > 시그모이드의 미분값이 연속적으로 곱해지며 기울기 소실 발생(미분값이 거의 0)
- Relu 함수를 사용하면 양의 구간에서 미분값이 전부 1이기 때문에 기울기 손실 문제를 해결할 수 있다. 


<br/>
<br/>


## 딥러닝 학습 관련 기술
### 활성화 함수
1. 시그모이드 함수
   - Logistic 함수라고 부르기도 함
    ![image](https://user-images.githubusercontent.com/86597163/181758006-7d3ef72b-7d82-41c8-95a7-c44f6d11e517.png)

    - 함수값이 (0,1)로 제한
    - 기울기 손실 현상 발생 : 역전파시 미분값이 소실될 가능성이 크다
    - 중심값이 0.5

2. tanh 함수
   - 시그모이드 함수를 transformation 함
    ![image](https://user-images.githubusercontent.com/86597163/181758327-99639979-821e-41b6-86ec-80a78e812868.png)

   - 중심값이 0
   - 기울기 소실 문제 발생
   - 자연어 처리에 자주 사용됨

3. Relu 함수
    ![image](https://user-images.githubusercontent.com/86597163/181758789-2dbc0226-2d8a-4ea4-a0c9-cface2cda093.png) 
   - x > 0 이면 기울기 1의 직선, x < 0이면 0
   - 음수값은 기울기가 0이기 때문에 뉴런이 죽을 수 있다
- > Leakly Relu : Relu의 뉴런이 죽는 현상 해결, 음수일 때 0이 아닌 매우 작은 값을 출력

4. PRelu
   - Leakly Relu와 유사, 새로운 파라미터 a를 추가해 음수에서 기울기를 학습할 수 있게 함

5. ELU
   - Relu의 장점을 포함
   - 뉴런이 죽는 현상(Dying Relu) 해결
   - Relu와 달리 exp함수를 계산하는 비용 발생


<br/>

### Optimizer
1. SGD 
   - 확률적 경사 하강법
   - 매개변수 값을 조정하여 전체 데이터가 아니라 랜덤으로 선택한 하나의 데이터에 대해서만 계산
   - 적은 데이터를 사용하여 빠르게 계산함
  ![image](https://user-images.githubusercontent.com/86597163/181763717-251fb679-12bd-4fef-adf3-13d7c6db639a.png)
  

2. Momentum
   - 관성을 응용한 방법
   - SGD에서 계산된 접선의 기울기에 한 시점 전의 접선의 기울기 값을 일정한 비율만큼 반영
   - 로컬 미니멈에 빠지는 것을 벗어날 수 있다.
  ![image](https://user-images.githubusercontent.com/86597163/181764152-34ce40f4-692c-4012-aed6-8975b6934f8c.png)
  ![image](https://user-images.githubusercontent.com/86597163/181764214-3a976a01-f9a3-48d4-9d30-b0a181ab04c9.png)

3. Adagrad
   - 변수의 업데이트 횟수에 따라 학습률을 조절하는 옵션이 추가된 최적화 방법
   - 많이 변하지 않은 변수들은 학습률을 크게하고 반대의 변수는 학습률을 적게한다.

4. RMSprop
   - Adagrad의 문제점 개선을 위해 등장
   - 최근 반복에서 비롯된 그레이언트만 누적시킴
  ![image](https://user-images.githubusercontent.com/86597163/181764826-9ff1ac6c-f22b-40ac-92a6-f90d76e7c2eb.png)

5. Adam
   - RMSprop와 Momentum을 합친 방법
   - 기울기 값과 기울기의 제곱값의 지수이동평균을 활용하여 step 변화량을 조절
   - 학습률 하이퍼파라미터를 튜닝할 필요가 적음
  ![image](https://user-images.githubusercontent.com/86597163/181765171-f8191754-949e-4366-90c3-2c24bfc858a9.png)


<br/>
<br/>


### 과적합 방지
1. 가중치 제한 
   - 가중치 값이 작아지도록 학습하여 과적합을 방지함
   - 가중치 초깃값
     > Xavier 초깃값
     > - 앞 계층의 노드가 n개일 때 표준편차가 1/루트h인 분포 사용
     > - 고정된 표준편차를 사용하지 않고 각 층들의 입/출력 노드 개수에 따라 파라미터 값 초기화
     > - 시그모이드에서 주로 사용
     >
     > He 초깃값
     > - 입력 노드의 개수에만 의존하는 형태
     > - 모든 층에 균일하게 분포
     > - Relu에서 주로 사용

<br/>


2. 드롭아웃(Dropout)
   - 은닉층의 각 노드들은 학습에서 제외될 확률 발생
   - epoch마다 Dropout되는 노드들이 랜덤하게 선택(일부 노드를 랜덤하게 제외)
   - epoch마다 다른 인공 신경망 구성을 학습하게 하여 과적합 방지


<br/>

### 배치 정규화 
- 활성화함수의 활성화값 또는 출력값을 정규화(정규분포로 만듦)하는 작업
- 학습 시 미니 배치를 한 단위로 정규화

<br/>

### 데이터 증강
- 충분한 양의 데이터가 없을 경우 과적합 발생
- 데이터를 변형시켜 추가 데이터 셋을 증강하여 사용

<br/>

### Early Stopping
- validation loss가 최소가 되는 순간에 학습을 멈춤

<br/>

### 전이학습
- 방대한 양의 데이터셋에서 추출한 정보를 불러와서 테스트 셋의 정확도를 극대화해주는 기법
- 기존의 학습 결과를 가져와 유사한 프로젝트에 사용
