# SOLR
- 검색엔진 Apache Lucene을 쉽게 사용할 수 있도록 만든 오픈 소스 Solr
- Java환경에서 Solr를 쉽게 사용할 수 있도록 만든 SolrJ

---

## how to use
### version
- JDK version에 맞는 Solr version을 선택 후 다운로드
  - JDK version : 1.8 = Solr version : 7.x

### admin page 
- cd ${path}\solr-7.7.3\bin 경로 이동
  - solr start (-p 8983) : default port=8983
  - solr create -c ${core-name} : ${core-name}의 core 생성 
  - solr restart -p 8983
- localhost:8983 접속 → solr admin page

- http://localhost:8983/solr/${core-name}/select?q=*%3A*
  - http://localhost:8983/solr → 검색 엔진 서버 주소
  - ${core-name} → 데이터를 저장하는 코어
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

---

##
- to-do : 형태소 분석 및 검색어 자동완성 기능
## concept
- was내부 검색엔진 활용 개념 자체가
  - query -> datamap 시도할 때 delay되는 시간이 있어 검색엔진을 활용해 delay를 최대한 없애려 한다.
  - solr에 data를 상주시켜 바로 datamap으로 호출을 한다.
  - 그렇다면 solrJ를 활용하여 was를 통해 Database Query조회를 해서 solr 서버에 data를 상주시켜 바로바로 나타내어 준다.
    - 그렇다면 solrJ interface를 활용한
      - ***solr data 추가, 수정, 삭제 등 컨트롤 방법***
      - 