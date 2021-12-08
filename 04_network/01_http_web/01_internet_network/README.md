### 1. Internet network
#### 1.1. IP(Internet Protocol)
- 특징
  - 지정한 IP주소(IP Address)로 데이터 전달
  - Packet이라는 통신단위로 데이터 전달
    * Packet == Package + Bucket
- 단점
  - Internet Protocol → 한계점이 명확하다(신뢰성, 순서, 누락 등)
    - 신뢰성
    - 순서
    - 소실 등
  
#### 1.2. TCP(Transmission Control Protocol) ; 전송 제어 프로토콜
- TCP Protocol → IP Protocol의 한계점을 해결
- 연결지향 → TCP 3 Way handshake (물리적 연결 X)
- 연결과정  
  1) C → S - 1.SYN : 접속 요청
  2) S → C - 2.SYN + ACK : 접속 요청 + 요청 수락
  3) C → S - 3.ACK : 요청 수락
  4) C ↔ S - 신뢰
- 데이터 전달 보증  

#### 1.3. UDP(User Datagram Protocol)
- UDP Protocol → IP + port 개념
    - 필요 시 Application 개발단계에서 기능 확장이 가능
  
#### 1.4. Port
- Port → 하나의 ip내부의 동작 Application을 구분하기 위함
  - Port는 Packet을 구분해준다. ex) game packet, kakao packet, music packet
  
#### 1.5. DNS(Domain Name System)
- dns → ip주소는 변하기 쉽고, 외우기 어렵다 → domain 이름을 등록해서 사용할 수 있도록 도와준 것.