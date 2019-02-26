---
title: "수소 충전소 최적의 설립 위치 추천

- ① 분석 배경 및 목표"
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
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
  <font size=4>[목차]</font>
  <font size=4>
    [분석 배경](#id-section1)
    [분석 목표](#id-section2)
  </font>
</div>
<hr/>


<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
  <font size=4>[개요]</font>
  <font color = gray size=4>
    ▶ 빅데이터 청년인재
    <b>[빅데이터 분석 기반 지능 SW 과정]</b> 프로젝트
    <hr/>
    ▷ <b>기간</b>
    2018/07/01 ~ 2018/09/07 (약 2개월)
    <hr/>
    ▶ <b>담당 역할</b>
    데이터 수집
    데이터 전처리
    모델링
    <hr/>
    ▷ <b>활용 분석 도구</b>
    Jupyter notebook (python)
    Folium (python)
    Rstudio (R)
    Excel
  </font>
</div>
<hr/>

<div id='id-section1'/>
<font size=6 color= purple><b> 1. 분석 배경 </b></font>
<hr color=purple>
  <img src="/image/dongguk/hydro_roadmap.PNG" width="400px">
  <font size=3 color=gray>▶ 목표치에 따른 수소 충전소 확충 진행률의 부진 확인가능
  </font>

  <hr/>
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
  <b><font color=red>"부지 확보 장기간 소요"</font> >> 주요한 수소 충전소 보급 지연 원인</b>
  <font size=3>
    ▶ 일반 전기차 충전소의 약 20배의 비용 소요
    ▷ 기존 충전소 / 주유소 부지 활용해 최적의 배치 전략 필요
  </font>
</div>
<hr/>


  <img src="/image/dongguk/article1.PNG" width="500px">
    <font size=2 color=gray>[출처] news1뉴스(http://news1.kr,2018.03.22)</font>
    <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
      <font size=3>
        수소 산업 협회는 서울에 한정 짓더라도
        <font color=purple><b>기존의 LPG 충전소를 활용</b></font>하면,
        약 70여곳의 수소 충전소 확보가 가능하다 밝힘
      </font>
    </div>
  <hr/>
<font size=3>
  <img src="/image/dongguk/hydro_price.PNG" width="1200px">
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
    <b>기존의 부지, 건물, 인력을 그대로 활용</b>하는 것이
    비용적인 측면에서 <b>효율적</b>인 것을 확인 가능
  </div>
  <hr/>
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
    <font size=3 color=purple><b>[기타 참조 가능 기사]</b></font>
    - LPG-수소 융‧복합 충전소, 부지 면적 확보가 '핵심'
    <font size=2 color=gray>
        (http://www.gnetimes.co.kr/news/articleView.html?idxno=44757)
    </font>
    - 1145개 LPG충전ㆍ주유소 "수소 복합 충전소 전환 가능"
    <font size=2 color=gray>
        (http://www.energy-news.co.kr/news/articleView.html?idxno=54052)
    </font>
  </div>
</font>



<div id='id-section2'/>
<font size=6 color=purple><b> 2. 분석 목표 </b></font>
<hr color=purple>
<img src="/image/dongguk/object.PNG" width="1200px">
