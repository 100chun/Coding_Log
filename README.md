# 1. SW_Basic - OSI 7 계층 (7/30)
```
Network : 정보 교환을 위해 통신 장치를 연결한 통신망
1. LAN (Local Area Network) : 근거리 고속 통신망
2. WAN (Wide Area Network) : 원거리 (광대역) 안정적 통신망

Internet : 전 세계적 통신망의 집합
Protocol : 네트워크 통신을 위한 규칙 (문법 + 의미 + 순서)
Network Model : 호환을 위한 통신망 제작 모델 / 문제 해결

부호 : 의미를 가지는 약속된 기호
신호 (Signal) : 부호가 특정 매개체를 이용해 전달되는 상태
 -전기 에너지, 통신망 필요
```

7 OSI 계층
----------
|7 OSI 모델|TCP/IP|역할|
|-|-|-|
|애플리케이션 + 프레젠테이션 + 세션 계층|애플리케이션 계층|APP 작업|
|전송 계층 |전송 계층|송신, 수진지의 데이터 신뢰성 확보|
|네트워크 계층|인터넷 계층|경로 탐색|
|데이터 링크 계층|Network Interface 계층|장치 간 데이터 전송 방식|
|물리 계층|Network Interface 계층|장치 연결, 신호 전달|

1. OSI 물리 계층 : 신호 전달을 위한 물리적 연결
 * 케이블 : 장치, 네트워크를 연결하는 물리적 매체로 데이터를 전송하는 전선 -LAN Cable : UTP, FTP, STP
  * 리피터 : 신호 증폭, 재생
   * 허브 : 네트워크 장치를 연결하여 데이터 중계, 전송 -> 스위치로 대체
 
