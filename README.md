# 소음 탐지기
이 프로젝트는 2018년 서운고 과학탐구대회 "컴퓨터 인터페이스를 통한 학교 내 공사장 소음 연구 및 아두이노를 사용한 소음탐지기 제작" 중 **소음 탐지기** 부분입니다.

## 개요
소리가 일정 크기 이상이 되면 감지하고 알려주는 소음 탐지기

## 알고리즘
- 소리 센서는 진폭의 크기를 아두이노로 아날로그의 형태로 입력시킨다.
- 소리 센서가 입력시킨 값은 전압의 크기를 아날로그의 형태로 0~1023의 범위로 입력시킨 값이다. 그런데 우리는 실생활에서 소리의 크기의 단위로 데시벨(dB)를 사용하므로 우리가 실생활에서 이 기기를 사용하려면 데시벨을 사용하는 것이 편하다. 그러므로 우리는 아날로그 형태의 값을 데시벨로 변환시켜주는 식을 사용하여 기기 사용을 좀 더 편하게 한다.
- 이때 소리센서가 입력시킨 값과 데시벨 값은 정밀한 측정을 위해 실수 형태로 저장한다.
- 변환시킨 데시벨 값을 I2C LCD에 출력하도록 한다. 이때 출력한 값은 실시간으로 변하도록 한다.
- LCD에 출력되는 값과 실제 값이 맞는지 확인하기 위해 시리얼 모니터와 통신하여 확인하도록 한다.
- 소리 센서가 입력한 데시벨이 65dB 이상이면 빨간색 LED를 켜고 능동 부저에서 소리가 나도록 한다.
- 소리 센서가 입력한 데시벨이 65dB 미만이면 초록색 LED를 켜고 능동 부저에서 소리가 나지 않도록 한다.

## 회로 설계
![image](https://user-images.githubusercontent.com/65582244/132721730-7dd44ea7-d4f1-469d-b41f-6721e9349f6e.png)
- ‘Tinkercad’ 프로그램에는 소리 센서가 없어서 IR센서로 대체하여 설계하였다.
- ‘Tinkercad’ 프로그램에는 I2C LCD가 없어서 16*2 Character LCD로 대체하여 설계하였는데 GND, VCC핀은 똑같게 설계하였으며 I2C LCD의 SDA핀과 SCL핀을 각각 DB0, DB1핀으로 대체하여 설계하였다.
- ‘Tinkercad’ 프로그램에는 능동 부저가 없어서 피소 스피커로 대체하여 설계하였다.

## 제작
![image](https://user-images.githubusercontent.com/65582244/132722046-7634c18a-38a2-4eea-a65c-38d9932f54ee.png)
- 소리 센서를 연결한 후 테스트를 진행하며 소리 센서의 가변저항을 돌려가며 최적의 값으로 조정하였다.
-부저 중 능동 부저를 사용하였는데, 그 이유는 이 기기는 부저를 이용하여 경고음만 내면 되기 때문에 이 용도에 적합한 능동 부저를 사용하였다.
- LED는 일반적으로 3.3V의 전압으로 작동하는데 아두이노의 디지털 핀은 5V의 전압만 출력할 수 있어 바로 연결하면 LED가 망가져 버리기 때문에 저항(220Ω)을 이용하여 LED에 가해지는 전압을 낮춰주었다.
- LCD 중 I2C LCD를 사용하였는데 그 이유는 이 기기는 많은 센서를 연결하지 않아 간단하게 작동되는 I2C LCD가 적합하기 때문이다.
- I2C LCD는 원래 5V의 전압으로 구동되는 모듈이다. 하지만 I2C LCD를 5V의 전압으로 작동을 시키게 되면 아두이노 전체에 과부하가 걸려 작동을 못 하게 된다. 그래서 우리는 여러 시도를 한 끝에 3.3V의 전압으로 작동을 시키면 글자 선명도와 백라이트 밝기는 낮아지지만 그래도 작동은 성공적으로 한다는 것을 깨닫고 3.3V의 전압을 출력하는 핀에 연결하였다.

## 소스 코드
https://github.com/choi92/Noise_Meter/blob/main/noise_detector.ino

## 작동
![image](https://user-images.githubusercontent.com/65582244/132722400-ebd8463e-e815-4857-9772-4978255ec7d7.png)

