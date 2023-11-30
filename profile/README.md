## Hi there 👋

- This is smart clock project

## Info
- [tableClock_Architecture_v2](https://whimsical.com/tableclock-architecture-v2-HWLmeFVgNLASRoacF3mKFD)
- [clock widget issues](https://github.com/smart-clock/stm32_widget/issues)
- [clock widget project board](https://github.com/orgs/smart-clock/projects/1)

## Setting
1. 도시
2. 노선 번호, 정류소 번호
3. 주식 종목
4. ...

## Protocol

1. 모든 데이터는 `char` 타입
2. UART BAUDRATE `115200`

### STM -> ESP

| SOF | P_ID | DATA (ex) | EOF | 설명                                  | 주기  |
| --- | ---- | --------- | --- | ------------------------------------- | ----- |
| *   | BZ^   | 1         | '\n'   | 0 : Buzzer Off <br> 1 : Buzzer Toggle | Event |

### ESP -> STM

| SOF | P_ID | DATA (ex)                               | EOF | 설명                                           | 주기  |
| --- | ---- | --------------------------------------- | --- | ---------------------------------------------- | ----- |
| *   | WF^   | MJU_WIFI                                | '\n'   | 연결된 WiFi ID                                | 부팅 후 1회   |
| *   | ST^   | 192.168.1.135                           | '\n'   | 설정 웹서버 IP                                | 부팅 후 1회   |
| *   | TM^   | 2023-11-21 07:20:11                     | '\n'   | YYYY-MM-dd HH:mm:ss                            | 부팅 후 1회   |
| *   | BA^   | 78%,1h20m                     | '\n'   | 잔량 퍼센트, 남은 시간                                  | 1분   |
| *   | WT^   | Yongin,clear sky,25                     | '\n'   | 도시, 날씨, 기온                               | 1분   |
| *   | GC^   | 2,class1,08:00,10:00,class2,13:00,15:00 | '\n'   | 일정 개수, 일정, 시각                          | 1일   |
| *   | BS^   | 5003,명지대 입구,7,20                         | '\n'   | 노선 번호, 정류소 이름, 도착 시간1, 도착 시간2 | 30초  |
| *   | SK^   | AAPL,178.72                             | '\n'   | 종목 명, 실시간 주식 가격                      | 1일   |
| *   | SM^   | AAPL,178.72,179.42,,, 180.31            | '\n'   | 종목 명, 주식 가격 일별 22개 (최근 한달 종가)        | 1일   |
| *   | US^   | 1                                       | '\n'   | 0 : 사용자 인식 X <br> 1 : 사용자 인식 O       | Event |
| *   | BT^   | 1                                       | '\n'   | 1 : 버튼 한 번 누름 <br> 2 : 버튼 길게 누름    | Event |


## Scenario

1. 사용자 인식 O -> Robot Eye 표정 출력
2. 버튼 한 번 누름 -> Home 위젯으로 전환
3. 버튼 길게 누름 -> 화면 끄기

## Open API

1. STOCK -> [Finnhub](https://finnhub.io/docs/api/)

## Arduino IDE

1. board : LOLIN S3
