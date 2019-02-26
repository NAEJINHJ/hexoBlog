---
  title: "수소 충전소 최적의 설립 위치 추천

  - ② 데이터 분석"

  categories:
  - Project
  - BIGDATA
  tags:
  - BIGDATA
  - modeling
  - Project
  - python
  - R
---
<hr/>
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
  <font size=4>[목차]</font>
  <font size=4>
    [데이터 목록 및 전처리](#section1)
    [분석 방법 - AHP 개요](#section2)
    - [의사결정 계층화](#section3)
    - [요소 선정](#section4)
    - [평가 기준 비교](#section5)
    - [가중치 추정](#section6)
    - [일관성 검증](#section7)
  </font>
</div>
<hr/>

<div id='section1'/>
<font size=6 color= purple><b> [데이터 목록 및 전처리] </b></font>
<hr color = purple>
<font size=4><b>1. 사용 데이터 목록</b></font>

<img src="/image/dongguk/data_list.PNG" width="1200px">

<hr/>

<font size=4><b>2. 전처리 과정</b></font>

<img src="/image/dongguk/preprocessing.PNG" width="1200px">

<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:5px 0;">
  <font size=3>
    csv 형태의 원본 데이터를 <b>python pandas</b>를 이용,
    dataframe 형태로 가져옴
    <hr/>
    <b>장소명과 도로명 주소</b> 데이터 추출
    <hr/>
    <b>지오코딩 API</b> 이용
    >> 해당 장소의 좌표값(위도, 경도) 얻음
    <hr/>
    <font color=purple><b>하버사인 공식</b></font> 사용
    >> 좌표값을 기반으로, 곡면에서 두 지점간의 거리 계산
  </font>
</div>
<hr/>



<div id='section2'/>
<font size=6 color= purple><b> [분석 방법 - AHP] </b></font>
<hr color = purple>
<font size=3>
  <b><font size=4>1. <font color=purple>AHP</font>란?</font></b>

  <img src="/image/dongguk/AHP_explanation.PNG" width="1000px">
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:5px 0;">
    고려한 데이터가 대부분 <b>거리 데이터</b>였고,
    타 논문 참고 결과, <b>입지 선정시 AHP 기법을 가장 많이 활용</b>한 것을 확인
  </div>

  <img src="/image/dongguk/AHP.PNG" width="1000px">

  <hr/>
  <div id='section3'/>
  <b><font size=4>2. <font color=purple>의사결정 계층</font></font></b><font size=3>- 분석 기준 설정</font>

  <img src="/image/dongguk/decision_tree.PNG" width="1200px">
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:5px 0;">
    <font size=4 color=purple><b>[상위 단계]</b></font>
    <b>최종 목표(overall goal)</b>
    <hr/>
    <font size=4 color=purple><b>[Level.1 단계]</b></font>
    <b>평가 기준</b>
    1) 안정성
    2) 설립 비용
    3) 운영 효율성
    <hr/>
    <font size=4 color=purple><b>[Level.2 단계]</b></font>
    평가 기준에 대한 <b>선택 대안</b>
    1) 제 1 보호지역과의 거리
    2) 서울 자치구별 화재 발생
    3) 2km 반경 내 타 LPG 충전소 존재 유무
    4) 버스 차고지와의 거리
  </div>

  <hr/>
  <div id='section4'/>
  <b><font size=4>3. <font color=purple>요소 선정</font></font></b>

  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    <font size=4 color=navy><b>[안정성]</b></font>
    <hr/>
    1) <b>제 1종 보호시설</b>과의 거리
    <img src="/image/dongguk/type1_protection.PNG" width="400px">
    주유소의 <b>폭발 위험성을 고려</b>하여, 제 1 보호시설 간의 거리를 분석 요소로 선정
    <font size=2 color=gray>(초중고,유치원 데이터 이용)</font>
    <font color=purple>
    제 1종 보호시설과 LPG 주유소간의 거리가 <b>멀수록,
    가중치 값 더 크게</b> 산정
    </font>
    <hr/>
    2) <b>자치구별 화재 발생률</b>
    <img src="/image/dongguk/fire.PNG" width="800px">
    수소의 경우, 타가스에 폭발했을 시 <b>[위험 피해율]</b>이 크고,
    <b>수소 위험성에 대한 인식</b>이 수소 충전소 설립에 큰 영향을 미칠 수 있기에
    분석 요소로 선정하였음
  </div>
  <hr/>
  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    <font size=4 color=navy><b>[설립 비용]</b></font>
    <hr/>
    <b> 2km 반경 타 LPG 충전소</b> 존재 유무
    <img src="/image/dongguk/other_LPG.PNG" width="500px">
    <b>LPG 주유소가 밀집</b>되어 있다면,
    밀집된 LPG 주유소 중 <b>한 곳을 수소 충전소</b>로
    대체하는 방안 고려
  </div>
  <hr/>
  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    <font size=4 color=navy><b>[운영 효율성]</b></font>
    <hr/>
    <b> 버스 차고지</b>와의 거리
    <img src="/image/dongguk/bus_article2.PNG" width="500px">
    <img src="/image/dongguk/bus_article1.PNG" width="500px">
    2027년까지, <b>수도권의 경유 버스 → 수소/전기 버스</b> 등으로 전면 교체
    향후 <b>버스 차고지 근처에 수소 충전소가 설립</b>될 경우,
    <b>충전소 운영에 영향</b>을 미칠 것이라 판단
    <hr/>
    <font size=2 color=gray>
      매일 경제 (http://news.mk.co.kr/,2018.05.14)
      월간 수소 경제 (http://www.h2news.kr/2018.07.10)
    </font>
  </div>
  <hr/>

  <div id='section5'/>
  <b><font size=4>4. <font color=purple>평가 기준 비교</font></font></b>

  <img src="/image/dongguk/compare.PNG" width="1200px">
  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    앞서 선정한 4가지 요인들에 대해,
    <b>중앙값을 기준</b>으로 4개의 그룹으로 나눠, <b>그룹 번호</b> 부여
    <hr/>
    <font size=2 color=gray>
      모든 것들이 다 [커지면 좋거나/ 작아지면 좋거나]의 기준 이었기 때문에,
      <b>중앙값을 기준</b>으로 grouping하기로 판단함
    </font>
  </div>

  <img src="/image/dongguk/compare2.PNG" width="1200px">
  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    <font size=2 color=gray>
      (타 논문을 참고하여, 쌍대비교치 3,5,7로 설정)
    </font>
    <hr/>
    대안별 중요 순위는 <font color=purple><b>주관적으로 설정</b></font>됨
    검증을 위해 이후 <font color=purple><b>일관성 검증</b></font>을 진행하였음
    <hr/>
    <font size=4 color=navy><b>[쌍대비교표 설명]</b></font>
      차고지 기준으로 화재는 <b>매우 중요</b>
      >> <b>7</b> 부여
      1종 보호시설은 화재보다는 덜 중요 즉, <b>적당히 중요</b>
      >> <b>5</b> 부여
      차고지 기준 2km 이내의 타 충전소의 개수는 <b>약간 중요</b>
      >> <b>3</b> 부여
    <hr/>
    <font size=4 color=navy><b>[쌍대비교 결과]</b></font><font size=3>- 버스차고지</font>
    <img src="/image/dongguk/compare3.PNG" width="1200px">
    <b>구별 화재 발생률, 제 1종 보호시설, 주변 LPG 주유소 요인</b>에 대해서도
    동일하게 쌍대비교 수행
  </div>

  <div id='section6'/>
  <b><font size=4>5. <font color=purple>가중치 추정</font></font></b>
  <img src="/image/dongguk/weight.PNG" width="1200px">
  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    <font size=4 color=navy><b>고유치 방법(Eigenvalue Method)</b></font>
    쌍별 비교된 <b>의사 결정 요소들 간의 쌍대적 가중치</b> 계산
    <hr/>
    <b>k = 평가 기준</b>
    <font size=2 color=gray>(버스 차고지, LPG 주유소 밀집도, 제 1종 보호시설, 자치구별 화재 비율)</font>
    상단의 수식을 통해 <font color=purple><b>최종 행렬(nX1)</b></font>을 만들어 냄
  </div>

  <div id='section7'/>
  <b><font size=4>6. <font color=purple>일관성 검증</font></font></b>
  <div style="background-color:rgba(0, 0, 0, 0.0470588);  text-align:center; vertical-align: middle; padding:5px 0;">
    <img src="/image/dongguk/consistency.PNG" width="1200px">
    상단의 수식을 통해 <b>일관성 검증</b> 수행
    <img src="/image/dongguk/consistency_result.PNG" width="1200px">
  </div>
</font>
