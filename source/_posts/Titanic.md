---
title: "Titanic: Machine Learning from Disaster - first challenge"
categories:
- BIGDATA
- Kaggle
tags:
- BIGDATA
- modeling
- Kaggle
- python
---
<img src="/image/kaggle/titanic/header.png" width="1200px">
<img src="/image/kaggle/titanic/summary.png" width="1200px">
<hr/>
<img src="/image/kaggle/titanic/dataset.PNG" width="1200px">
<img src="/image/kaggle/titanic/data.png" width="1200px">
<hr/>
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:5px 0;">
  <font size=4 color=purple><b>[Element]</b></font>
  <hr/>
  <font size=3 color=gray>
    <font color=navy><b>Survival</b></font>
    <b>
      NO = 0
      Yes = 1
    </b>
    <hr/>
    <font color=navy><b>Pclass</b></font>
    Ticket class
    <b>
      1st = 1
      2nd = 2
      3rd = 3
    </b>
    <hr/>
    <font color=navy><b>SibSp</b></font>
    <b>동반한 형제, 자매, 배우자의 수</b>
    <hr/>
    <font color=navy><b>Parch</b></font>
    <b>동반한 부모, 자식의 수</b>
    <hr/>
    <font color=navy><b>ticket</b></font>
    <b>티켓 고유 넘버</b>
    <hr/>
    <font color=navy><b>Fare</b></font>
    <b>Passenger fare</b>
    <hr/>
    <font color=navy><b>Cabin</b></font>
    <b>객실 번호</b>
    <hr/>
    <font color=navy><b>Embarked</b></font>
    출발지
    <b>
      Cherbourg = C
      Queenstown = Q
      Southampton = S
    </b>
  </font>
</div>
<hr/>

<img src="/image/kaggle/titanic/table.PNG" width="1000px">

<hr/>
<img src="/image/kaggle/titanic/processing.PNG" width="1000px">
<img src="/image/kaggle/titanic/result.png" width="1000px">

<hr/>
<font color=purple size=4><b>[향후 개선 방안]</b></font>
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:5px 0;">
  <font size=3 color=gray>
    이름의 last name 추출해 <b>가족을 그룹으로</b> 식별해볼 것
    <hr/>
    Age 결측치 다른 값으로 채워보기
    <hr/>
    Partner, sex, age를 고려
    <font size=2>→ 30대 이상일 경우, 부모일 확률 높음</font>
    <hr/>
    참고해 볼 곳 >>
    https://www.kaggle.com/yassineghouzam/titanic-top-4-with-ensemble-modeling
    https://towardsdatascience.com/kaggle-titanic-machine-learning-model-top-7-fa4523b7c40
    https://towardsdatascience.com/how-i-got-98-prediction-accuracy-with-kaggles-titanic-competition-ad24afed01fc
  </font>
</div>
