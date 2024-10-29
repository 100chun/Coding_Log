# (10/8 ~ 10/17)
Thread, Interface
## Swing
**Swing : GUI 개발용 Library**

## IO Stream
------
* Socket : TCP/IP 기반 네트워크 통신에서 데이터 송수신의 마지막 접점
* Server : 데이터를 송신자
* Client : 데이터 수신자
* Stream : 데이터가 전송되는 통로
  * InputStream : 들어오는 정보
  * OutputStream : 내보내는 정보
* Buffer : 데이터 이동 향상에 필요한 바이트, 문자 변환자

**Client**
```
Socket server = new Socket("192.168.5.50",7000);
		InputStream in = server.getInputStream();
		DataInputStream din = new DataInputStream(in);
		String recv = din.readUTF();
		System.out.println("서버 메세지 : " + recv);
		
		din.close();
		in.close();
		server.close();
```

**Server**

**Refactoring : 코드의 품질 향상**
* 변수 선언, 초기화 -> 변수 정의
* if-else -> 삼항연산자
* if-else -> Switch
* 긴 메서드 -> 여러개의 잛은 메서드 = Extract
* 중복 코드 -> 중복 제거, 메서드 분리
* 디자인 패턴 이용
* 알고리즘, 데이터 최적화
