---
title: "NoSQL이란?"
categories:
- DB
- NoSQL
tags:
- DB
- NoSQL
- MongoDB
---
<font size=3>
  <img src="/image/mongodb/nosql/NoSQL_logo.PNG">
  <hr/>
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=4><b>[목차]</b></font>
    <font size=4>
      [개념](#section1)
      [특징](#section2)
      [장점](#section3)
      [단점](#section4)
      [종류](#section5)
      [MongoDB EcoSystem](#section6)
    </font>
  </div>
  <hr/>
  <div id='section1'/>
  <font size=5><b>1. 개념</b></font>
  <div style="text-align:center; vertical-align: middle; padding:30px 0;">
    <b>Not Only SQL</b>의 약자<br>
    기본 RDBMS의 한계를 극복하기 위해 만들어진 새로운 형태의 데이터베이스<br>
    <font color=purple><b>분산 환경</b></font>에서 대용량의 데이터를 빠르게 처리하기 위해 개발 됨<br>
    분산형 구조를 통해 여러대의 서버에 분산하여 저장하고,
    상호 복제하여 데이터 유실이나 서비스 중지에 대비<br>
    핵심은 <b>Horizontal Scalability</b>(수평확장)과 <b>High Availability</b>(고가용성)<br>
    릴레이션이 아니므로 <b>고정된 스키마가 없고<font size=2 color=gray>(Schema-less)</font> 조인이 힘듦</b><br>
    거대한 Map으로서 <b>key-value 형식</b>을 지원<br>
    대부분 <font color=hotpink><b>CAP 이론</b></font>을 따름
  </div>
  <div style="background-color:rgba(0, 0, 0, 0.0470588);text-align:center;vertical-align: middle; padding:30px 0;">
    <font size=4 color=hotpink><b> CAP 이론</b></font><br>
    <b>[Consistency]</b><font size=2 color=gray>-일관성</font>
    분산된 노드 중, 어느 노드로 접근하더라도 데이터 값이 같아야 함
    <font size=2>(데이터 복제 중에 쿼리가 되는 시스템, 즉 일관성을 제공하지 않는 시스템의 경우 다른 데이터 값이 쿼리 될 수 있음)</font><hr/>
    <b>[Availability]</b><font size=2 color=gray>-가용성</font>
    클러스터링된 노드 중 하나 이상의 노드가 실패라도
    정상적으로 요청을 처리할 수 있는 기능을 제공<hr/>
    <b>[Partition Tolerance]</b><font size=2 color=gray>-분산 허용</font>
    클러스터링 노드 간에 통신하는 네트워크가 장애가 나더라도
    정상적으로 서비스를 수행
    노드간 물리적으로 전혀 다른 네트워크 공간에 위치도 가능
    <hr/>
    <b>이 중 2가지만 만족할 수 있음</b>
    - RDBMS는 일반적으로 일관성과 가용성 만족
    - NoSQL [가용성/분산허용 만족] or [일관성/분산허용 만족] 제품군으로 나뉨
  </div>
  <div style="background-color:rgba(0, 0, 0, 0.0470588);text-align:center;vertical-align: middle; padding:30px 0;">
    <b>[RDBMS의 한계]</b><br>
    많은 데이터양과 처리량이 계속적으로 증가한다면,
    <hr/>
    ● 스키마 문제:
    빅데이터를 RDB의 스키마에 맞춰 변경해서 넣으려면 매우 긴 시간의 down time 발생
    <hr/>
    ● 스케일업의 한계:
    관계 모델과 트랜잭션의 연산, 일관성, 속성을 유지하면서 분산환경(스케일 아웃)에서 RDBMS를 조작하는 것은 어려움
  </div>
  <hr/>
  <div id='section2'/>
  <font size=5><b>2. 특징</b></font>
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=4><b>[Document-oriented storage]</b></font><br>
    <img src="/image/mongodb/nosql/cp_table.PNG">
    MongoDB는 database > collections > documents 구조
    document는 key-value 형태의 BSON<font size=2>(Binary JSON)</font>
    <hr/>
    <font size=4><b>[Full Index Support]</b></font><br>
    다양한 인덱싱 제공
    <b>Single Field Indexes</b>
    <b>Compound Indexes</b>
    <b>Multikey Indexes</b>
    <b>Geospatial Indexes and Queries</b>
    <b>Text Indexes</b>
    <b>Hashed Index</b>
    <hr/>
    <font size=4><b>[Replication & High Availability]</b></font><br>
    간단한 설정만으로 데이터 복제 지원, 가용성 향상
    <hr/>
    <font size=4><b>[Auto-Sharding]</b></font><br>
    처음부터 자동으로 데이터를 분산하여 저장
    하나의 컬렉션처럼 사용 가능
    수평적 확장 가능
    <hr/>
    <font size=4><b>[Querying]</b></font><font size=2>(documented-based query)</font><br>
    다양한 종류의 쿼리문 지원
    <font size=2>(필터링, 수집, 정렬, 정규표현식)</font>
    <hr/>
    <font size=4><b>[Fast In-Pace Updates]</b></font><br>
    고성능의 atomic operation 지원
    <hr/>
    <font size=4><b>[Map/Reduce]</b></font><br>
    분산/병렬 시스템 운용 지원
    <hr/>
    <font size=4><b>[GridFS]</b></font><br>
    자동으로 분산 파일 저장
    실제 파일이 어디에 저장되어 있는지 신경쓸 필요 X
    복구 역시 자동
    <hr/>
    <font size=4><b>[Commercial Support]</b></font><br>
    10gen에서 관리하는 오픈 소스
  </div>
  <hr/>
  <div id='section3'/>
  <font size=5><b>3. 장점</b></font>
  <div style="text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=4><b>● 클라우드 컴퓨팅 환경에 적합</b></font>
    Open Source임
    하드웨어 확장에 유연한 대처가 가능
    RDBMS에 비해 <b>저렴한 비용으로 분산 처리와 병렬 처리</b> 가능
    <br>
    <font size=4><b>● 유연한 데이터 모델임</b></font>
    <b>비정형 데이터 구조 설계</b>로 설계 비용 감소
    관계형 데이터베이스의 <b>Relationship과 Join구조를 Linking과 Embedded로</b> 구현해 성능이 빠름
    <font size=2 color=gray>(join을 피할 수 있기 때문)</font>
    <br>
    <font size=4><b>● 빅데이터 처리에 효과적</b></font>
    Memory Mapping 기능을 통해 Read/Write가 빠름
    기존의 OS와 H/W에 구축 가능
    기존 RDB와 동일하게 데이터 처리 가능
  </div>
  <hr/>
  <div id='section4'/>
  <font size=5><b>4. 단점</b></font>
  <div style="text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=4>
      ● 정합성이 떨어지므로 트랜잭션이 필요한 경우에는 부적합
      <font size=2 color=gray>(ex. 금융, 결제 등)</font><br>
      ● JOIN이 없기 때문에, join이 필요없도록 데이터 구조화 필요<br>
      ● memory mapped file으로 파일 엔진 DB
        <font size=3>메모리 관리를 OS에 위임<br>메모리에 의존적, 메모리 크기가 성능 좌우</font><br>
      ● SQL 완전히 이전 불가<br>
      ● B트리 인덱스 사용해 인덱스 생성, 크기가 커질 수록 입력/삭제 성능 저하
    </font>
  </div>
  <hr/>
  <div id='section5'/>
  <font size=5><b>5. 종류</b></font>
  <div style="text-align:center; vertical-align: middle; padding:30px 0;">
    MongoDB
    Casandra
    HBASE
    CouchDB
    Riak
    Redis
    <br/>
    <div style="background-color:rgba(0, 0, 0, 0.0470588);text-align:center;vertical-align: middle; padding:30px 0;">
      <b>[참조 사이트]</b><br>
      http://nosql-database.org
      http://www.mongodb.org
      http://hbase.apache.org/
      http://couchdb.apache.org/
    </div>
  </div>
  <hr/>
  <div id='section6'/>
  <font size=5><b>4. MongoDB EcoSystem</b></font>
  <div style="text-align:center; vertical-align: middle; padding:30px 0;">
    <img src="/image/mongodb/nosql/mongodb_ecosystem.PNG">
    <font size=4><b>[Sharding System]</b></font>
    빅데이터의 효율적인 <font color=hotpink>분산 저장</font><br>
    <font size=4><b>[ReplicaSets]</b></font>
    데이터의 안전한 <font color=hotpink>복제 저장</font><br>
    <font size=4><b>[Text Search Engine / Full Indexing 기법]</b></font>
    저장된 데이터를 보다 빠르게 추출<br>
    <font size=4><b>[MapReduce / Aggregation FrameWork]</b></font>
    데이터의 <font color=hotpink>빠른 분석, 가공처리</font><br>
    <font size=4><b>[GridFs]</b></font>
    <font color=hotpink>비정형 데이터</font>의 효율적인 저장 및 관리<br>
    <font size=4><b>[OPS Manager / Compass]</b></font>
    각 Sub System이 효율적으로 운영되고 있는지 <font color=hotpink>모니터링</font>
    <br>
    <img src="/image/mongodb/nosql/ecosystem.PNG">
  </div>
  <div style="background-color:rgba(0, 0, 0, 0.0470588);text-align:center;vertical-align: middle; padding:30px 0;">
    <b>[참조]</b><br>
    MongoDB Master가 해설하는 New NoSQL & mongoDB - 주종면 저
    NoSQL (개념, 특징과 장점, CAP 이론, 데이터모델 분류)
    <font size=2>출처: https://sjh836.tistory.com/97 [빨간색코딩]</font>
  </div>
</font>
