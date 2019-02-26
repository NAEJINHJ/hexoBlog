---
title: "NSMC 데이터를 사용한 한국어 영화 리뷰 감정 분석"
categories:
- BIGDATA
- NLP
tags:
- NLP
- 감정분석
- BIGDATA
---
<font size=3>
  <img src="/image/NLP/movie_review.PNG">
  <div style=" text-align:center; vertical-align: middle; padding:30px 0;">
    <hr/>
    <font size=4><b>[목차]</b></font>
    <font size=4><b>
      [NSMC 데이터란?](#section1)
      <br>
      [감정 분석이란?](#section2)
      <br>
      [PRACTICE](#section3)
    </b></font>
    <hr/>
  </div>
  <div style=" text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=4><b>[NSMC 데이터](https://github.com/e9t/nsmc/)</b></font>를 사용해
    <font color=purple><b>영화 리뷰 감정 분석</b></font>을 수행해보자!
    우선, NSMC 데이터에 대해 알아보자
    <div id='section1'/>
    {% codeblock lang:Markdown %}
      $ head ratings_train.txt
      id      document        label
      9976970 아 더빙.. 진짜 짜증나네요 목소리        0
      3819312 흠...포스터보고 초딩영화줄....오버연기조차 가볍지 않구나        1
      10265843        너무재밓었다그래서보는것을추천한다      0
      9045019 교도소 이야기구먼 ..솔직히 재미는 없다..평점 조정       0
      6483659 사이몬페그의 익살스런 연기가 돋보였던 영화!스파이더맨에서 늙어보이기만 했던 커스틴 던스트가 너무나도 이뻐보였다  1
      5403919 막 걸음마 뗀 3세부터 초등학교 1학년생인 8살용영화.ㅋㅋㅋ...별반개도 아까움.     0
      7797314 원작의 긴장감을 제대로 살려내지못했다.  0
      9443947 별 반개도 아깝다 욕나온다 이응경 길용우 연기생활이몇년인지..정말 발로해도 그것보단 낫겟다 납치.감금만반복반복..이드라마는 가족도없다 연기못하는사람만모엿네       0
      7156791 액션이 없는데도 재미 있는 몇안되는 영화 1
    {% endcodeblock %}
  </div>
</font>
