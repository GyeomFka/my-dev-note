# File upload
## Introduction
- HTML Form을 통한 파일 업로드를 이해하려면 Form을 전송하는 두 가지 방식의 차이를 이해해야 한다.
- HTML Form 전송 방식
  - application/x-www-form-urlencoded : 기본적인, 일반적인 방식(HTTP Content-Type default)
    - 문자를 전송하는 방식
  - multipart/form-data
    - 파일은 문자가 아니라 binary data
    
- 문제점 : 일반적인 Form의 경우 {이름, 나이, 첨부파일} 한 번에 전송을 해야 하는데 ***text와 binary data를 동시에 전송*** 해야 하는 상황. 
```
- 이름
- 나이
- 첨부파일
```
- 해결책 : HTTP `multipart/form-data`전송 방식 제공
```html
<form action="/path" method="post" enctype="multipart/form-data">
    <input type="text" name="a">
    <input type="text" name="a">
    <input type="file" name="file"> 
    <button type="submit">전송</button>
</form>
```
- 위의 form tag를 기반으로 web browser가 생성한 요청 HTTP메시지는 ?
![Alt text](01.png)
- boundary 값 : random한 값
- boundary 값을 기준으로 구분된 header + body 가 생성이 된다.
  - 여러개의 다른 스타일의 data style을 한 번에 보낸다.

- 정리
  - `multipart/form-data` 여러 종류의 `content-type`을 한 번에 전송을 한다. 그래서 이름이 `multipart`
  - `application/x-www-form-urlencoded`와 비교해서 매우 복잡하다 
  - ***`part`로 구분되어져 있는 복잡한 HTTP 메시지를 서버에서는 어떻게 사용할까 ?***

## 멀티파트 사용 옵션
- 업로드 사이즈 제한
```properties
spring.servlet.multipart.max-file-size=1MB
spring.servlet.multipart.max-request-size=10MB
```
사이즈를 넘으면 `SizeLimitExceededException` 발생

- enabled off (default=true)
```properties
spring.servlet.multipart.enabled=false
```
multipart 처리를 하지 않겠다는 설정