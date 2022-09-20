# SOLR
- 검색엔진 Apache Lucene을 쉽게 사용할 수 있도록 만든 오픈 소스 Solr
- Java환경에서 Solr를 쉽게 사용할 수 있도록 만든 SolrJ

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

###
- was내부 검색엔진 활용 개념 자체가
  - query -> datamap 시도할 때 delay되는 시간이 있어 검색엔진을 활용해 delay를 최대한 없애려 한다.
  - solr에 data를 상주시켜 바로 datamap으로 호출을 한다.
  - 그렇다면 solrJ를 활용하여 was를 통해 Database Query조회를 해서 solr 서버에 data를 상주시켜 바로바로 나타내어 준다.
    - 그렇다면 solrJ interface를 활용한
      - ***solr data 추가, 수정, 삭제 등 컨트롤 방법***
      - 