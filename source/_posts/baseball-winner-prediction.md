---
title: "메이저리그 야구 승률 예측 - ① 게임-데이 시뮬레이션"
categories:
- BIGDATA
- Modeling
- R
tags:
- R
- modeling
---
<font size=3>
  <hr/>
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=4><b>[목차]</b></font>
    <font size=4>
      [개요](#section1)
      [데이터 분석](#section2)
      [게임-데이 시뮬레이션](#section3)
    </font>
  </div>
  <hr/>
  <div id='section1'/>
  <img src="/image/baseball/win_prediction/modeling_framework.PNG" width="800px">
  <font size=2 color=gray>(승리하는 팀을 가려내기 위한 예측 모델링 프레임 워크)</font>
  <br>
  <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
    <font size=5 color=purple><b>[개요]</b></font>
    <hr/>
    <font size=4>
      일반에 공개된 메이저 리그 야구 데이터를 사용하여
      <b>타우트</b> 없이 <font color=hotpink>승리팀을 가려낼 수 있는 데이터 기반 분석</font>
      <font size=2 color=gray>(타우트 - 경마나 스포츠 경기에서 도박 정보나 팁을 파는 사람)</font>
    </font>
    <hr/>
    <font color=gray>
      <font color=purple>▶ <b>설명 변수</b></font>
      <b>과거 선수의 역량</b><font size=2>(타율, 방어율 등)</font>과 <b>팀의 승률</b>과 관련
      이러한 변수에 근거해 <B>상대팀의 득점 예측</b>
      이외에도 게임이 진행될 장소와 시기,
      게임 결과에 영향을 줄 수 있는 다른 모든 조건 고려
      <hr/>
      <font color=purple>▷ <b>반응 변수</b></font>
      승 / 패/ 득점 수
      <font size=2>(득점 스코어 - 게임, 팀, 시간 or 일정으로 구성)</font>
      <hr/>
      <font color=purple>▶ <b>분석 방법</b></font>
      일반적인 분석과 동일하게,
      <font color=hotpink><b>훈련-테스트 방법</b></font> 이용해 모형 평가
      <hr/>
      <font color=purple>▷ <b>승점 모형</b></font>
      전통적 방법, 데이터 적응<font size=2>(data adaptive) 방법
      두 가지 방법의 조합
    </font>
  </div>
  <br>
  <br>
  <div id='section2'/>
  <font size=5><b>* 데이터 분석</b></font>
  <hr/>
  <div style="text-align:center; vertical-align: middle; padding:10px 0;">
    <font size=4><b>미래 득점 예측 위해 <font color=hotpink>과거 승리 기록</font> 참조</b></font>
    <b>2007년 시즌 분석</b> 위해
    <b>메츠와 양키스 간</b> 해당 시즌에 대한 데이터 선택
    <font size=2 color=gray>(이전 시즌에 얻은 팀 통계와 2007년 프리시즌 기록은 무시)</font>
    <hr/>
    <b>[<font color=hotpink>뉴욕 메츠</font>의 경기와 득점에 대한 모든 정보]</b><font size=2 color=gray>(4/1~6/15)</font>
    <br>
    <img src="/image/baseball/win_prediction/newyork_mets.PNG">
    홈/ 원정 경기에서 모두 상대팀보다 많은 점수 기록
    <br>
    <hr/>
    <b>[<font color=hotpink>뉴욕 양키스</font>의 경기와 득점에 대한 모든 정보]</b><font size=2 color=gray>(4/1~6/15)</font>
    <br>
    <img src="/image/baseball/win_prediction/newyork_yankees.PNG">
    원정 경기에서 상대팀보다 많은 점수 기록
    but 홈 경기에서 적은 점수 기록
    <br>
    <hr/>
    <font color=hotpink><b>
      5월 18일 양키스 2: 메츠 3
      5월 19일 양키스 7: 메츠 10
      5월 20일 양키스 6: 메츠 2
    </b></font>
    이와 같은 세 경기의 결과를 사용하여
    <b>6월 15~17일</b>의 게임 결과를 예측
  </div>
  <hr/>
  <br>
  <br>
  <div id='section3'/>
  <font size=5><b>* 게임-데이 시뮬레이션</b></font>
  <hr/>
  <div style="text-align:center; vertical-align: middle; padding:10px 0;">
    <b>뉴욕 메츠</b>의 대부분의 경기가 <b>지명 타자가 없는</b> 내셔널 리그라는 점
    <b>뉴욕 양키스</b>는 대부분 <b>지명타자가 있는</b> 아메리칸 리그 경기를 한다는 점
    <b>고려하지 X</b>
    <br>
    <br>
    <font size=4 color=purle><b>[첫번째 시뮬레이션]</b></font>
    <hr/>
    분석 대상의 실점은 고려하지 X
    <font color=hotpink><b>득점에만 초점</b></font>을 둔 경우
    <img src="/image/baseball/win_prediction/simul1.PNG">
    {% codeblock lang:R %}
      # 파일 읽어오기
      # 깨지는 헤더 수정
      library(reshape)

      mets <- read.csv("./data/NY_m.csv",header=TRUE,encoding = "UTF-8")
      mets <- rename(mets, c("X.U.FEFF.hometeam" = "hometeam"))

      yankees <- read.csv("./data/NY_y.csv",header=TRUE,encoding = "UTF-8")
      yankees <- rename(yankees, c("X.U.FEFF.hometeam" = "hometeam"))

      # 원정팀 메츠의 득점과 홈팀 양키스의 득점
      away_mets <- mets$away_NY_m
      away_mets <- away_mets[-c(32:34)] # 결측값과 평균값 삭제 위함

      home_yankees <- yankees$home_NY_y
      home_yankees <- home_yankees[-c(32:34)]
    {% endcodeblock %}
    away_mets와 home_yankees의 <b>득점값을 랜덤으로 추출</b>
    가상 게임을 돌림
    <font size=2 color=gray>(랜덤으로 추출된 숫자 비교)</font>
    <b>동점일 경우 카운트하지 X</b>
    {% codeblock lang:R %}
      # 득점 값 랜덤 추출
      random_mets <- sample(away_mets, 50000, replace=TRUE)
      random_yankees <- sample(home_yankees, 50000, replace=TRUE)

      # 각 팀이 몇번 승리하였는지 카운트 할 변수
      mets_win_cnt = 0
      yankees_win_cnt = 0

      for(i in 1:length(random_mets)){
          if (random_mets[i] > random_yankees[i])
              mets_win_cnt <- mets_win_cnt + 1
          else if(random_mets[i] < random_yankees[i])
              yankees_win_cnt <- yankees_win_cnt + 1
          else
              next

      }

      # 승률
      mets_win_rate = mets_win_cnt/length(random_mets)
      yankees_win_rate = yankees_win_cnt/length(random_mets)
      cat('뉴욕 메츠의 승률 : ', mets_win_rate,'\n')
      cat('뉴욕 양키스의 승률 : ', yankees_win_rate)
    {% endcodeblock %}
    <img src="/image/baseball/win_prediction/simul1_result.PNG">
    <br>
    <br>
    <font size=4 color=purle><b>[두번째 시뮬레이션]</b></font>
    <hr/>
    공격과 수비 모두 고려 <font size=2 color=gray>(득점과 실점)</font>
    - 공격 득점<font size=2 color=gray>(대상팀의 득점)</font>과 수비 실점<font size=2 color=gray>(상대팀의 득점)</font>
    - 각 팀의 예상 득점을 추정하기 위해서는,<br>해당 팀이 <b>획득한 득점과 허용한 실점</b>에 대한<br>경험적 분포에서 추출한 <b>임의의 랜덤 값</b>을 사용
    - 상대팀의 공격과 수비 숫자를 평균
    <img src="/image/baseball/win_prediction/simul2.PNG">
    메츠와 양키스가 서로 상대로 한 게임을 분석하기 위해서는,
    <font color=hotpink><b>공격과 수비</b></font> 성적 데이터를 모두 고려해야 함!
    <font size=2 color=gray>양키스 경기장에서 열린 게임에서<br>원정팀인 뉴욕 메츠는 홈팀인 양키스를 대상으로 공격<br>홈팀 양키스는 워정팀 메츠를 대상으로 공격</font>
    {% codeblock lang:R %}
      # 메츠의 득점과 실점
      away_mets <- mets$away_NY_m
      away_mets <- away_mets[-c(32:34)]
      away_mets_runs <- mets$home_score
      away_mets_runs <- away_mets_runs[-c(32:34)]
      awaymets_for_graph <- data.frame(away_mets,away_mets_runs)

      # 양키스 득점과 실점
      home_yankees <- yankees$home_NY_y
      home_yankees <- home_yankees[-c(32:34)]
      home_yankees_runs <- yankees$home_score
      home_yankees_runs <- home_yankees_runs[-c(32:34)]
      homeyankees_for_graph <- data.frame(home_yankees,home_yankees_runs)
    {% endcodeblock %}
    <b>ggplot 라이브러리</b> 사용해
    <b>공격과 수비</b>를 모두 고려한 메츠 원정팀, 양키스 홈팀의
    <font color=hotpink><b>득실 빈도 그래프</b></font>를 그려보면
    <img src="/image/baseball/win_prediction/mets_yankees_att_def.PNG">
    {% codeblock lang:R %}
      # 메츠의 득점 요인
      random_mets_attack <- sample(away_mets, 50000, replace=TRUE)
      random_mets_defence <- sample(away_mets_runs, 50000, replace=TRUE)
      avg_mets <- 0

      # 양키스의 득점 요인
      random_yankees_attack <- sample(home_yankees, 50000, replace=TRUE)
      random_yankees_defence <- sample(home_yankees_runs, 50000, replace=TRUE)
      avg_yankees <- 0

      for(i in 1:length(random_mets_attack)){
      avg_mets <- append((random_mets_attack[i]+random_mets_defence[i])/2,avg_mets)
      avg_yankees <- append((random_yankees_attack[i]+random_yankees_defence)/2,avg_yankees)
      }

      # 각 팀이 몇번 승리하였는지 카운트 할 변수
      mets_win_cnt = 0
      yankees_win_cnt = 0

      for(i in 1:length(avg_mets)){
          if (avg_mets[i] > avg_yankees[i])
              mets_win_cnt <- mets_win_cnt + 1
          else if(avg_mets[i] < avg_yankees[i])
              yankees_win_cnt <- yankees_win_cnt + 1
          else
              next
      }

      # 승률
      mets_win_rate = mets_win_cnt/length(avg_mets)
      yankees_win_rate = yankees_win_cnt/length(avg_mets)

      cat('뉴욕 메츠의 승률 : ', mets_win_rate,'\n')
      cat('뉴욕 양키스의 승률 : ', yankees_win_rate)
    {% endcodeblock %}
    <img src="/image/baseball/win_prediction/simul2_result.PNG">
  </div>
</font>
