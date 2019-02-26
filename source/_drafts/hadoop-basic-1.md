---
title: "[빅데이터 분석을 위한 하둡 프로그래밍] – 1강"
categories:
- BIGDATA
- hadoop
tags:
- hadoop
- BIGDATA
---
  <img src="/image/hadoop/hadoop_logo.png">
  <font size=3>
    <font size=5><b><빅데이터 개념 및 3요소></b></font>
    <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
      ● 기존 데이터 베이스 관리 도구의 데이터 수집, 저장, 관리 분석하는 역량을 넘어서는 데이터
      <font size=2>(데이터의 <font color=hotpink>규모</font>에 초점 둔 정의)</font>
      <hr/>
      ● 다양한 종류의 대규모 데이터로부터 저렴한 비용으로 가치를 추출하고, 데이터의 빠른 수집, 발굴/분석을 지원하도록 고안된 차세대 아키텍처
      <font size=2>(업무 수행 방식 초점 둔 정의)</font>
      <hr/>
      ● Volume(크기), Velocity(속도), Variety(다양성)
      <font size=2>이 세가지 중 2가지 이상만 충족을 시키면 빅데이터 요건에 부합</font>
      <img src="/image/hadoop/3v.PNG">
      <b>크기</b>
      조직에 따라 다를 수 있음
      (현재 분산 컴퓨팅 솔루션 – 구글에서 제공하는 GFS, Apache의 Hadoop, 더 대용량인 EMC 등)
      <b>속도</b>
      실시간 처리, 장기적 처리
      <b>다양성</b>
      빅데이터 자체가 다양한 데이터로 구성
      반정형 데이터(xml, html 등 스키마를 이용해 표현하는 데이터)
    </div>
    <br>
    <font size=5><b><하둡(Hadoop)?></b></font>
    <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
    ●	대용량 데이터를 분산 처리할 수 있는 자바 기반의 오픈 소스 프레임 워크
    <font size=2>(Apache top level open source frame work)</font>
    ●	분산파일시스템(HDFS)과 분산처리시스템인 맵리듀스로 구성
    ●	리눅스 기반의 머신이라면 문제 없이 동작
    </div>
  </font>
