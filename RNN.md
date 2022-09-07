# RNN(순환 신경망)
- 순차 데이터 학습을 위한 인공신경망
  > 순차 데이터 : 텍스트, 시계열과 같은 순서가 의미가 있는 데이터
  >
  > 과거와 현재 데이터간 상관 관계가 있음

- CNN은 데이터가 앞으로만 전달되는 형태, 이전 데이터를 재사용할 수 있는 구조 필요

![image](https://user-images.githubusercontent.com/86597163/183542022-06f901c7-6ed5-4478-8828-e9d59b6ba272.png)
> 기존 layer(은닉층)을 cell이라고 부름

- rnn 데이터 구조
![image](https://user-images.githubusercontent.com/86597163/183543695-433313cf-3641-430e-b60b-ef38956a58b2.png)


### LSTM
- 기울기 소실 문제 해결을 위해 제안
- time step 사이에 은닉 상태와 더불어 셀 상태도 함께 전달
- 기본 RNN에 비해 파라미터가 많아 학습 시간이 오래 걸림
  ![image](https://user-images.githubusercontent.com/86597163/183543954-3155c1a7-0085-4f98-9b05-61153329fe67.png)





