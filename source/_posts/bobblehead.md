---
title: "LA Dodgers 홍보 효과 분석"
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
        ● 목적
          1) 버블헤드 인형 홍보전략을 통한 <font color=hotpink>야구장 관중 증가 여부 </font>
          2) 야구표로 증가한 구단 수익으로 버블헤드 인형 홍보활동에 투자한 <font color=hotpink>고정비용, 가변비용 충당 가능 여부</font>

  <font color=black size=3>
        ● 라이브러리
          1) 선형 회귀 분석용 함수:  car
          2) 그래픽 패키지:  lattice
  </font>

  <hr/>
        <font color=gray size=1><메이저리그 2012년 다저스 홈경기 데이터></font>
        <img src="/image/bobblehead_csv.PNG" width="1200px">

  <b>ordered_day_of_week</b>
  정렬된 요일 변수
  <img src="/image/day.PNG">

  <b>ordered_month</b>
  정렬된 월 변수
  <img src="/image/month.PNG">
  <hr/>
##### [요일별 dodgers 관중수 분포]
  {% codeblock lang:python %}
  with(data=dodgers,plot(ordered_day_of_week,attend/1000,
  xlab="Day of Week",ylab = "Attendence (thousands)",
  col="violet",las=1))
  {% endcodeblock %}
  <img src="/image/bobblehead_day.PNG" width="1200px">

##### [월별 dodgers 관중수 분포]
  {% codeblock lang:python %}
  with(data=dodgers,plot(ordered_month,attend/1000,
  xlab="Month",ylab="Attendance (thousands)",
  col="light blue",las=1))
  {% endcodeblock %}
  <img src="/image/bobblehead_month.PNG" width="1200px">
  </font>

<font size=3>
<h5> [주간/야간 경기 & 불꽃놀이 유무에 따른 관중수 분포] </h5>
  경기 시간과 날씨 <font size=1 color= gray>(맑음/흐림)</font>에 대한 조건을 설정 → <font color = hotpink>온도와 관중수 간의 관계</font> 파악

  * library(<font color= purple>lattice</font>) <font color=gray size=1.5>(참조: http://visualize.tistory.com/305)</font>
: 직교 형태의 그래픽(Trellis graphic)을 생성하는 코드 포함
1) 다차원의 데이터를 사용하려 할 때, 한번에 많은 플롯 생성 가능
2) 기본 플로팅 시스템의 방법을 'mfrow'와 'mfcall'이라는 인수 통해 활용 가능
<img src="/image/lattice.PNG" width="1200px">

  {% codeblock lang:python %}
  library(lattice) # 플로팅을 위해 사용하는 라이브러리

  group.labels <- c("No Fireworks","Fireworks")
  group.symbols <- c(21,24)
  group.colors <- c("black","black")
  group.fill <- c("black","red")

  xyplot(attend/1000~temp | skies + day_night,
       data=dodgers, groups=fireworks, pch=group.symbols,
       aspect= 1, cex=1.
       악

       * library(<font color=5, col=group.colors, fill=group.fill,
       layout=c(2,2), type=c("p","g"),
       strip=strip.custom(strip.levels=TRUE,strip.names=FALSE, style=1),
       xlab = "Temperature (Degrees Fahrenheit)",
       ylab = "Attendance (thousands)",
       key = list(space="top",
                  text = list(rev(group.labels), col=rev(group.colors)),
                  points= list(pch=rev(group.symbols),col=rev(group.colors),
                              fill = rev(group.fill))
                 ) #list
      ) # xyplot
  {% endcodeblock %}
  <img src="/image/firework_temp.PNG" width="1200px">
> 그래프 분석 결과, 맑은 날씨의 주간경기에는 온도가 높을수록 관중수가 적다.
> 일반적으로 일요일에는 주간경기를 한다.
> 2012년 LA 다저스 구장의 경기는 한 게임을 제외하고 모두 날씨가 좋았다.

<h5> [LA 다저스의 상대팀 기준 다저스 구장 관중수] </h5>
단변량 산점도
{% codeblock lang:python %}
group.labels <- c("Day","Night")
group.symbols <- c(1,20)
group.symbols.size <- c(2,2.75)

bwplot(opponent~attend/1000,data=dodgers, groups=day_night,
       xlab = "Attendance (thousands)",
       panel = function(x,y,groups,subscripts, ...){
           panel.grid(h= (length(levels(dodgers$opponent))-1),v=-1)
           panel.stripplot(x,y,groups=groups, subscripts = subscripts,
                           cex=group.symbols.size, pch=group.symbols, col="darkblue"
                          )
       },
         key= list(space="top", text=list(group.labels,col="black"),
                  points = list(pch=group.symbols, cex=group.symbols.size, col="darkblue")
                  )
      )
{% endcodeblock %}
<img src="/image/day_night.png" width="1200px">
> 도시 규모가 큰 메트로폴리탄 지역을 연고로 하는 팀과 경기를 하는 경우 관중수는 큰 변화 X


<h5> [회귀모형] </h5>
<b>train-test 모형</b>
<img src="/image/train-test.png" width="1200px">
<img src="/image/summary.PNG">
- 버블 헤드 인형을 이용한 홍보활동에 대한 통계적 유의성 검증
- 유형I 분산 분석으로 순차적 검증에 대한 제곱합을 계산
{% codeblock lang:python %}
print(anova(my.model.fit))
{% endcodeblock %}
<img src="/image/anova.PNG">
<b>진단용 plot</b>
<img src="/image/fitted.png" width="1200px">

<h5> [패키지 car 이용해 추가 모형 진단] </h5>
{% codeblock lang:python %}
library(car)
residualPlots(my.model.fit)
marginalModelPlots(my.model.fit)
{% endcodeblock %}
<img src="/image/pearson.png" width="1200px">
<img src="/image/marginal_model_plot.png" width="1200px">
<b> 유의한 outlier 확인</b>
{% codeblock lang:python %}
print(outlierTest(my.model.fit))
{% endcodeblock %}
<img src="/image/p-value.PNG">

> 없는 것으로 확인

<hr/>
<b><다저스의 버블헤드 인형 홍보에 대한 예측모형에 근거></b>
1) 다가오는 시즌에 예측 대상 경기의 관중수 예측 가능
2) 버블헤드 인형을 활용한 홍보에 따른 관중수 예측 가능
3) 관중 예측값 사용해 홍보 유무에 따른 다저스 수익 예측 가능
<hr/>
</font>
