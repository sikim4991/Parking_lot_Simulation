# Parking_lot_Simulation
## 설계 목표
현대사회에 있어 한 가구당 차량을 여러대를 가지고 있어서 마트나 공공시설에서의 주차공간을 찾기란 쉽지가 않다.
그리고 주차하는데 어려움을 겪는분들을 위해 시스템을 설계해보았다.

주차관리 시스템을 만들어 주차장에 자리의 유/무를 미리 확인할 수 있고, 주차에 어려움을 겪는 사람들이 주차장에 설치된 3단계로 나눠진 LED와 부저센서의 소리를 이용하여 편리하고 쉽게 주차할 수 있도록 도움을 주는 장치를 만들었다.

## 사회 경제적 파급효과
마트나 병원등에서 주차자리의 유/무를 확인할 수 있는 장치들은 종종 보이곤한다.
하지만 소리센서와 LED등을 이용하여 보다 더 세밀하고 정밀한 기능까지 추가되었을때는 많은 사람들이 보다 편리하게 이용할 수 있을 것이다.
 
## 제한사항
1. 주차 완료상태를 가정했을 때, 조도센서에 빛이 들어가지 않아야 하는데 브레드보드 위에 구현하다보니 빛의 양을 조절하는데 어려움을 겪었다.

2. 센서가 거리에 따라서 LED와 소리 간격이 달라지기 때문에 앞,뒤 간격만 알 뿐 좌,우 간격에 따라선 알 수 없다.

3. 부저 센서가 파일 열기만 해도 동작되어 어려움을 겪었다. 듀티 값을 조절해도 말을 듣지 않아 중간중간 딜레이를 넣어 경고음을 조절했다.

4. 가끔씩 초음파 센서가 읽어들이는 데이터가 튀어 거리 값이 비정상적으로 뛸 때가 있었다.

## 사용 보드
<img src="https://t1.daumcdn.net/cfile/tistory/2203E639592CC67E24" width="350" height="350">

* ARTIK053

* OS : Tizen RT

* 응용 제품을 위한 32비트 ARM Cortex R4(320MHz 기준)

* IEEE802.11b/g/n Wi-Fi 2.4GHz 무선 통신 인증

* UART, I2C, SPI, PWM, ADC, 및 GPIO I/O

* 29개 전용 GPIO 포트, SPI 2개, UART(2핀) 4개, ADC 4개, JTAG 1개, I2C 2개

* 5VDC ~ 12VDC 입력 전압

## 사용 모듈
<img src="https://www.baldengineer.com/wp-content/uploads/2011/12/LED-banner.png" width="300" height="150">

LED - LED 3개는 주차 공간 옆에 설치되고 나머지 2개는 앞의 천장에 설치되어 있다고 가정한다. 주차할 공간이 있는지 없는지 알려주는 역할과 거리에 따라 지정된 색깔이 켜진다.

<img src="https://2.bp.blogspot.com/-rM3AcVshwnw/Vpg0Iqm74oI/AAAAAAAAASY/f0T9mbqAQtI/s320/S-0200.jpg" width="250" height="200">

조도 센서 - 주차 공간 바닥에 설치되어 있다고 가정한다. 조도값이 높다면 차량이 주차되어 있지않아 주차할 공간이 있다는 의미이고, 조도값이 낮다면 차량이 주차되어있어 조도 센서에 빛이 가해지지 않아 주차할 공간이 없다는 의미이다.

<img src="https://mblogthumb-phinf.pstatic.net/MjAxNzAyMDNfMjY4/MDAxNDg2MTAwMTU4OTk2.EdxOHwOiM3AxyYSdv_es4HHABFamx44klAY1wzW6b4Ig.NKnZV5mbncZTKx-UZGlNHbgLqw0zkXBw970PDMpTgUMg.PNG.boilmint7/1.PNG?type=w2" width="200" height="200">

초음파 센서 - 주차 공간 뒤에 설치된다. 차량과 초음파센서의 거리를 측정하여 주차공간을 파악한다.

<img src="http://vctec.co.kr/web/product/big/201611/10424_shop1_334112.jpg" width="200" height="200">

부저 센서 - 차량과 초음파 센서의 거리가 가까워질수록 소리의 빈도가 증가한다.

## 역할
김상인 : 소스코드 구현, 오류 검출, 의견제시

박재문 : 피드백, 오류 수정, 의견제시

## 상세기능 설명
주차하는데 어려움을 겪는 사람 또는 모든 운전자가 보다 편리하게 주차를 할 수 있도록 주차장 자체에 센서를 부착해보았다.
우선 주차를 시작할 때 초음파 센서가 있는 곳이 벽면이라고 가정하고 초음파 센서에 가까워 질수록 초록불, 노란불, 빨간불 순서로 불이 켜진다.

이 때 부저센서가 함께 울리게 되고 초록불, 노란불, 빨간불 순서에 가까워 질수록 소리 간격이 빨리져서 벽면과 가까워짐을 운전자에게 알려준다. 그리고 조도센서는 주차장 앞의 LED 2개(사진을 보면 초음파 센서 뒤에 설치되어 있지만, 주차 공간 앞의 천장에 설치되어 있다고 가정)와 연동되어 있어 조도센서에 빛이 인식될 때는 초록불이 켜지면서 주차할 공간이 있음을 나타내고, 조도센서에 빛이 인식되지 않을때는 빨간불이 켜지면서 주차할 공간이 없다는 표시이다.

## 결과물
<img src="https://user-images.githubusercontent.com/73647861/105343087-82533000-5c24-11eb-8f48-0204e0d5a4a8.jpg" width="280" height="200">

초록불 점등 - 주차가능한 공간임을 나타내는 왼쪽 아래편에 초록색 LED가 켜져있고,차량 주차를 시작할 때, 초록색 LED가 차량이 진입중임을 알려주고 경고음이 시작된다.

<img src="https://user-images.githubusercontent.com/73647861/105343382-e4139a00-5c24-11eb-8516-d8da430afba7.jpg" width="280" height="200">

노란불 점등 - 어느 정도 차량이 들어갔을 때, 노란색 LED가 켜지고, 경고음 간격이 좁아져서 벽면에 가까워 지고 있을을 알려준다.

<img src="https://user-images.githubusercontent.com/73647861/105343546-1c1add00-5c25-11eb-9b90-4d810f10b8b0.jpg" width="280" height="200">

빨간불 점등 - 벽면과 거리가 얼마남지 않았을 때, 빨간색 LED가 켜지고, 긴박함을 나타내기 위해 경고음이 유지가 된다.

<img src="https://user-images.githubusercontent.com/73647861/105343708-53898980-5c25-11eb-98c1-dba9a85cb1fb.jpg" width="280" height="200">

주차 완료 상태 - 조도 센서가 주차공간 바닥에 설치되어있다는 가정하에 주차가 완료되면 빛이 들어오지 않을 것이다.
그러므로 조도센서가 기준치의 빛을 받지 못하면 10초 동안 카운트하고 그 이상일 경우 주차 완료로 인식해서 빨간 LED에 불이 켜진다.
차량이 주차장에서 빠져나올 때는 역순으로 발생한다.
