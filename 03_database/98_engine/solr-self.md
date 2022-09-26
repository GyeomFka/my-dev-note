# SOLR
- 검색엔진 Apache Lucene을 쉽게 사용할 수 있도록 만든 오픈 소스 Solr
- Java환경에서 Solr를 쉽게 사용할 수 있도록 만든 SolrJ
  - [Solr vs Elasticsearch](https://logz.io/blog/solr-vs-elasticsearch/)
  - [Solr Tutorial(Official)](https://solr.apache.org/guide/8_4/solr-tutorial.html)
  - [Solr Downloads](https://solr.apache.org/downloads.html)
    - version JDK 1.8 = Solr 7.x.x
---

## how to use
- Solr에서 제공된 예제 프로젝트로 전반적 개념이해
  - [블로그 링크](https://forest71.tistory.com/200)
- core 파일이라는 instance를 생성한다.

### Solr version
- JDK version에 맞는 Solr version을 선택 후 다운로드
  - JDK version : 1.8 = Solr version : 7.x

## run example of Solr
```shell
> solr create -c techproducts //techproducts라는 core를 생성
> java -jar -Dc=techproducts -Dauto example\exampledocs\post.jar example\exampledocs\*
// solr의 설치경로에서 실행해야한다. ex) C:\tools\solr-7.7.3
// post 명령어 실행
// example\exampledocs\* 는 오류를 발생
// example\exampledocs\*.xml 
// example\exampledocs\*.json 에 나누어 실행
> bin\solr stop -all
> bin\solr start -e techproducts
```

### Solr admin page 
- cd ${path}\solr-7.7.3\bin 경로 이동
  - solr start (-p 8983) : default port=8983
  - solr create -c ${core-name} : ${core-name}의 core 생성 
  - solr restart -p 8983
- localhost:8983 접속 → solr admin page

### Solr Core?
- A place to store indexed data
- 유사한 개념
  - RDBMS => Table
  - Excel => sheet 

### Solr Query 
- Execute Query를 누르면 URL을 제공해준다.
- http://localhost:8983/solr/techproducts/select?q=*%3A* (RESTful API 제공)
  - ★★★★그렇다면 SolrJ(java환경)에서 get호출도 가능?★★★★
    - response.numFound : 찾은 Data갯수
    - response.start : 시작 Row (페이징 처리를 위함)
    - response.docs([]) : 검색된 Data의 Key, Value가 JSON형태로 출력
- 다양한 검색조건 생성 가능.

### detail of URL
- http://localhost:8983/solr/${core-name}/select?q=*%3A*
  - http://localhost:8983/solr → 검색 엔진 서버 주소
  - ${core-name} → 데이터를 저장하는 ***코어***
  - select → 데이터 조회
  - q → Query : 검색식 *:* → (%3A=:) 
    - 모든 필드 : 모든 값 (*대신 찾고자 하는 ${값}을 지정해서 실행하면, 모든 필드에서 지정한 값을 찾는 검색이 된다.)
    - [검색식, 범위식](https://forest71.tistory.com/201?category=628611)
    - [solr docu](https://www.solrtutorial.com/solr-query-syntax.html)
    
### run example products
- [solr-x.x.x install directory standard]
  - bin\solr create -c ${core-name}
  - ${install-path}\example\exampledocs : 기본 색인목록 
  - bin\solr start -e techproducts : 예제 core 실행

### search
- q=${search-keyword} 단독 입력 = *:${search-keyword} 와 같다. (모든필드)
- q=${field}:${search-keyword} 입력 = 해당 필드의 검색어 검색 

### schema
- 데이터를 저장하는 방법 중, 구조(Schema)를 구성 (저장소 구성)
- RDBMS는 데이터의 형태를 미리 정의하고 Data를 가공하지만, Solr는 스키마를 미리 정의하지 않고도 사용 가능
  - Schemaless 하지만, 가급적 정의해서 사용하는 것이 좋다.
  - 첫 데이터에 따라 스키마를 정의하기 때문에, 치명적인 오류가 발생할 수 있다. 
  - ***Schemaless이긴 하지만 꼭 정의하고 사용하자***
- managed-schema.xml : 해당 코어의 스키마에 대해 정의하는 xml
  - [schema정의](https://since.tistory.com/5)

### DIH
- 원본 데이터에서 데이터를 추출해서 저장하는 방법
  - [Data Import Handler](https://forest71.tistory.com/203?category=628611)
  - [field정의](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=webmcr&logNo=220920656568)
- ***각 core에 해당하는 solrconfig.xml에서 data-import-handler 설정을 할 수 있다.***
- datasource path(postgresql-x.x.x.jar)
  - C:\tools\solr-7.7.3\server\solr-webapp\webapp\WEB-INF\lib
  - solr-7.7.3\server\solr-webapp\webapp\WEB-INF\lib [O]
  ![Alt text](solr_ex_erd.png)
- RDBMS는 정규화 개념을 사용하지만, 검색엔진에서는 하나의 데이터로 묶어서 저장한다.
  - RDB에서의 1:n 구성 → 검색엔진에서 배열([]), multiValued로 저장한다.
- dataSource 태그 → 접속 정보입력
- document 태그 → 처리할 데이터를 정의
```xml
<document>
  <entity name="item" query="select * from item"
          deltaQuery="select id from item where last_modified > '${dataimporter.last_index_time}'">
    <field column="NAME" name="name" />
  </entity>
</document>
```
[출처](https://forest71.tistory.com/203?category=628611) : [SW 개발이 좋은 사람:티스토리]
- data변경감지 → delta-import
- DIH 파일에서는 managed-schema에 지정되지 않은 컬럼은 저장되지 않는다.
  - DIH 에서는 Shemaless가 적용되지 않는다.
[DIH solr document](https://solr.apache.org/guide/8_4/uploading-structured-data-store-data-with-the-data-import-handler.html#uploading-structured-data-store-data-with-the-data-import-handler)

---

## etc
- to-do
  1) data-import 기능 import되는 시점 적용 알아보기
    - init, insert, update
  2) 형태소 분석
    - 검색어 자동완성 기능
    ex) 사용자 '홍'입력 → "홍길동", "홍길자", "홍수아" 자동완성 제공
      - was가 내부망이라 클라이언트에서 바로 적용가능한지 여부 확인 (detail)
  3) SolrJ control
  4) 왜 인지는 모르지만, IP검색(string) *42* 바로 검색이 안된다. 하지만 OS검색(string) *M* 검색 후 다시 IP검색을 *42*를 실행하면 실행이
정상적으로 가능하다.
  
## concept
- was내부 검색엔진 활용 개념 자체가
  - query -> datamap 시도할 때 delay되는 시간이 있어 검색엔진을 활용해 delay를 최대한 없애려 한다.
  - solr에 data를 상주시켜 바로 datamap으로 호출을 한다.
  - 그렇다면 solrJ를 활용하여 was를 통해 Database Query조회를 해서 solr 서버에 data를 상주시켜 바로바로 나타내어 준다.
    - 그렇다면 solrJ interface를 활용한
      - ***solr data 추가, 수정, 삭제 등 컨트롤 방법***
      - data update 시점에 solr update ?  
      - data insert 시점에 solr insert ?
  

## ???
[Solr보안이슈](https://www.igloo.co.kr/security-information/apache-solr-dataimport-handler-rce-cve-2019-0193/)
