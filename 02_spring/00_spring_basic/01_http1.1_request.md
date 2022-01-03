### HTTP1.1
- get
- post
- delete
- put

### 통신
- 기본적인 통신을 위해, 서로 다른 두 대상의 Stream이 연결 되어야 한다.
  - Byte stream(8bit)
  - write, read 각 stream
- HTTP1.1통신
  - 약속이 필요하다. 약속된 통신
  - 통신방법 4가지
    - Get
    - Post
    - Put
    - Delete
  
---
>A(Client)가 B(Server)에게 `요청`을 한다. B가 A에게 `응답`을 한다.
<br/>통신방법 4가지 = `요청`의 방법
> client가 응답 할 일은 없다. -> 요청은 client만 한다.
> 요청의 방식 4가지
1. Get : 데이터를 요청 - SELECT
2. Post : 데이터를 추가 - INSERT
3. Put : 데이터를 수정 - UPDATE
4. Delete : 데이터를 삭제 - DELETE

- '어떤' 데이터를 요청,추가,수정,삭제 해 줄까 ?
- C가 S에게 스트림을 연결하고 요청(Request)을 한다.
  - Get 요청 시 -> Get ? X
  - Post 요청 시 -> Post + 어떤 데이터 형태
- '어떤' 데이터의 형태 -> MIME타입