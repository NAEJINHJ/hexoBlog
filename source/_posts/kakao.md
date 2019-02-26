---
title: "python으로 카카오톡 대화 분석하기"
categories:
- BIGDATA
- NLP
tags:
- NLP
- BIGDATA
---
<font size=3>
  <img src="/image/NLP/kakao.gif">
  <div style=" text-align:center; vertical-align: middle; padding:30px 0;">
    오늘은 <font size=4 color=purple><b>카카오톡 대화</b></font>를 분석해보려 한다.
    분석할 데이터는 다음과 같은 방식으로 얻는다!
    <font color=hotpink><b>(삼지창 메뉴 > 대화 내용 > 대화 내보내기)</b></font>
    <br>
    <img src="/image/NLP/kakao_txt.png" width=400 height=500>
    <br>
    <img src="/image/NLP/kakao_file.PNG" >
    <br>
    얻은 파일의 구조는 위와 같다.
    데이터 분석을 위해 먼저 파일을 불러오자!
    <br>
    {% codeblock lang:Python %}
      path = "./data/KakaoTalk.txt"
      f = open(path,'r',encoding="utf-8")
      data = f.read()
    {% endcodeblock %}
    <br>
    본격적인 분석에 들어가기 앞서,
    <font size=4 color=purple><b>데이터 전처리</b></font>를 수행한다.
    <br>
    <font color=hotpink><b>1. 시간 삭제</b></font>
    <font size=2 color=gray>ex) [오후 1:40]</font>
    <b><font color=red>[</font> 부터 시작해 <font color=red>]</font>로 끝나는 문자</b>를 모두 삭제
    {% codeblock lang:Python %}
      # \\란 해당 문자 다음에 위치한 기호를 '기호 자체'로 지칭하기 위함
      result = re.sub('\\[.+\\]', '', data)
    {% endcodeblock %}
    <br>
    <font color=hotpink><b>2. 요일 삭제</b></font>
    <font size=2 color=gray>ex) --------------- 2019년 2월 18일 월요일 ---------------</font>
    {% codeblock lang:Python %}
      result = re.sub('(--------------- 20).+(요일 ---------------)', '', result)
    {% endcodeblock %}
    <br>
    <font color=hotpink><b>3. 자음 & 모음 삭제</b></font>
    <font size=2 color=gray>ex) ㅋㅋㅋㅋㅋ / ㅠㅠㅠㅠㅠ</font>
    {% codeblock lang:Python %}
      result = re.sub('[ㄱ-ㅎ]', '', result)
      result = re.sub('(ㅜ|ㅠ)+', '', result)
    {% endcodeblock %}
    <br>
    <font color=hotpink><b>4. 기호 및 이모티콘 삭제</b></font>
    {% codeblock lang:Python %}
      result = re.sub('[~!@#$%^&*()_+=?]<>', '', result)
      result = re.sub('\\(이모티콘\\)', '', result)
    {% endcodeblock %}
    <br>
    <br>
    이제 <font size=4 color=purple><b>본격적인 대화 분석</b></font>에 들어가보자!
    우선 분석에 <b>필요한 라이브러리</b>를 불러오고,
    <b>명사를 추출</b>한다.
    {% codeblock lang:Python %}
      import os
      import matplotlib.pyplot as plt
      from wordcloud import WordCloud
      from collections import Counter
      from konlpy.tag import Twitter
      import pytagcloud

      spliter = Twitter()
      split = spliter.nouns(result)
    {% endcodeblock %}
    <br>
    추출된 명사에 포함된 의미 없는 단어를 삭제한다.
    한국어는 stopwords를 직접 지정해주어야 한다.
    {% codeblock lang:Python %}
      stopwords = ["나","진짜","난","날","넌","내","너","얘","쟤","거","그","뭐","개","때","안",
             "애","그거","더","이","것","앜","임","엌","저","수","또","앗","응","걸","오",
            "막","알","니","데","곳","모","전","도","머","자","함","해","번","앞","걔","곸","중",
            "줄","찌","구","네","고","뎈","옹","아낰","바","후","웅","제"]
      filtered_split= [word for word in split if word not in stopwords]
    {% endcodeblock %}
    <br>
    stopwords를 모두 삭제했다면,
    가장 많이 언급된 단어 <b>100개</b>를 뽑아
    <font size=4 color=purple><b>wordcloud 분석</b></font>을 수행한다.
    {% codeblock lang:Python %}
      count = Counter(filtered_split)
      count.most_common(50)

      tag = count.most_common(100)
      taglist = pytagcloud.make_tags(tag,maxsize=80)

      pytagcloud.create_tag_image(taglist, './kakao_wordcloud.jpg', size=(900, 600), fontname='Korean', rectangular=False)
      f.close()
    {% endcodeblock %}
    <br>
    해당 분석을 수행한 결과 wordcloud는
    다음과 같다.
    <img src="/image/NLP/kakao_wordcloud.jpg" >
    <font size=2 color=gray>(모자이크 된 부분은 이름들과 약간의 비속어임)</font>
    <br>
    <img src="/image/cat.jpg" width=500 height=500>
    생각보다 언급된 비속어 빈도수가 커서 당황스러웠따...
    이제부터 진짜 예쁜 말만 쓰자구욧...
  </div>
</font>
