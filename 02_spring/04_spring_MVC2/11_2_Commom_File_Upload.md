## 공통기능 개발
- 개발 된 공통 기능 사용법 제공
- 솔루션 도입(innorix) 상황 고려
  - Solution을 Front, Back 어떻게 Interface되어 있는지 파악
    - 사용법 제공
- 앞서 Controller와 Service의 역할에 대한 깊은 고민
  - [tistory](https://choibulldog.tistory.com/52)

### File upload, download 공통기능 개발
- Upload(다중 업로드)
  - Server directory에 실제 파일 저장
  - Database file info 저장
- Download
  - client PC download ?
  - browser ?
- Exception, Error 처리

## Design
### Create
- 저장 Event발생 시 첨부파일 존재 여부 파악
  - 첨부파일 有
    - 확장자 체크
      - back, front 예외처리 ?
      - 확장자 별도 관리 (DB Insert)
    - 첨부 파일의 갯수 체크
      - 1 개, N개 동일하게 
        - 첨부파일 server dir 저장
        - originalName, storeName 별도 관리
  - 첨부파일 無

### Read

### Update

### Delete
