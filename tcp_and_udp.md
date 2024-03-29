# TCP (Transmission Control Protocol)
- 신뢰성 있는 데이터 전송을 보장하는 연결 지향적 프로토콜


1. 연결 지향적 프로토콜
  - TCP는 통신을 시작하기 전에 연결을 설정하고, 통신이 완료되면 연결을 종료함
  - 이러한 연결 기반 접근 방식은 신뢰성 있는 통신을 가능하게 함
  - 연결 설정 단계에서는 세그먼트를 교환하여 송수신자 간에 초기화된 연결을 설정함
  
2. 신뢰성
   - TCP는 데이터의 전송 및 수신 여부를 확인하기 위해 확인 응답 메커니즘을 사용함
   - 송신자가 데이터를 보내면 수신자는 해당 데이터를 수신했다는 확인 메시지를 다시 송신자에게 보냄
   - 만약 확인 응답이 오지 않으면 송신자는 데이터를 다시 전송함
   - 이를 통해 손실된 데이터를 신속하게 감지하고 재전송함으로싸 데이터의 신뢰성을 보장함

3. 순서 보장
   - TCP는 데이터를 전송하는 순서대로 수신측에서 데이터를 재조립함
   - 따라서 데이터가 전송되는 순서가 유지되어야 하는 경우에 유용하고, 데이터의 무결성을 보장함
4. 흐름 제어 및 혼잡 제어
    - TCP는 송신자와 수신자 간의 통신 속도를 조절하여 네트워크 혼잡을 방지하고, 효율적인 통신을 유지함
    - 흐름 제어는 수신측의 버퍼가 오버플로우되지 않도록 송신자의 전송 속도를 제어함
    - 혼잡 제어는 네트워크 혼잡을 감지하고, 네트워크의 부하를 조절하여 네트워크 성능을 최적화함




# UDP (User Datagram Protocol)
- 인터넷 프로토콜 스위트에서 신뢰성 없는 데이터그램 서비스를 제공하는 프로토콜


1. 비연결 지향적 프로토콜
   - UDP는 연결을 설정하지 않고 데이터를 전송하기 때문에 비연결 지향적임
   - 따라서 데이터 전송의 신뢰성과 순서 보장을 보장하지 않음
   - 이는 데이터그램을 독립적으로 처리하고 도착 순서에 관계없이 처리하기 때문
2. 빠른 전송
   - UDP 는 데이터의 신뢰성을 보장하지 않기 때문에 TCP 보다 더 빠른 전송이 가능함
   - 데이터를 전송하는 속도가 중요한 응용 프로그램에 적합
   - 예 : 동영상 스트리밍, 실시간 멀티미디어 스트리밍
3. 사용 사례
   - 동영상 스트리밍 : UDP는 동영상 스트리밍에서 빠른 전송 속도를 제공하여 실시간으로 동영상을 전송하는 데 사용됨
   - DNS 조회 : UDP는 DNS 조회에서 사용됨. DNS 쿼리 및 응답은 작은 크기의 데이터그램으로 전송되고, 신뢰성이 크게 중요하지 않음
     

**TCP와 UDP의 비교:**

| 기능 | TCP | UDP |
|---|---|---|
| 연결 방식 | 연결형 | 비연결형 |
| 신뢰성 | 높음 | 낮음 |
| 순서 보장 | 있음 | 없음 |
| 흐름 제어 | 있음 | 없음 |
| 속도 | 느림 | 빠름 |
| 적용 분야 | 웹 브라우징, 파일 전송, 이메일 | 스트리밍 미디어, VoIP, 게임 |

