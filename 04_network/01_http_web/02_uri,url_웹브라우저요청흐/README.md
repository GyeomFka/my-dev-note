### 1. URI, URL, URN
- URI
    - U → Uniform : 리소스 식별하는 통일된 방식 
    - R → Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
        - I → Identifier : 다른 항목과 구분하는데 필요한 정보
        - L → Locator : 리소스가 있는 위치를 '지정'
        - N → Name : 리소스에 이름을 '부여'
        - 위치는 변할 수 있지만, 이름은 변하지 않는다.
        - URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
        - 사실상 URI == URL 같은의미로 보겠다. 
    
#### 1.1. URL 분석
- https://google.com:443/search?q=hello&hl=ko
- scheme://[userinfo@]host[:port][/path][?query][#fragment]
    - host : dns or ip address
    - port : 생략가능하며 scheme에 따라 고정값 부여
        - http : 80
        - https : 443
        - 나머지는 생략해도 상관없음
    - query : query parameter, query string, 모두 문자열인 상태

### 2. 웹 브라우저 요청흐름

- https://google.com:443/search?q=hello&hl=ko
1) DNS조회 (host) → IP정보 + Port → 웹 브라우저가 HTTP 요청 메시지 생성
2) Socket lib를 통해 TCP/IP 연결 (IP, Port)
3) SYN, SYN+ACK, SYN
4) TCP/IP 패킷 생성 후 전송 (패킷 내부 HTTP 메시지)

/*추후 재작성*/


 
    
    