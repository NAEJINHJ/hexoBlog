---
title: "뉴스 댓글 WordCloud 분석"
categories:
- BIGDATA
- NLP
tags:
- NLP
- BIGDATA
---
<font size=3>
  <img src="/image/NLP/wordcloud.png">
  <div style=" text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=5><b>[목적]</b></font>
    오늘은 뉴스의 댓글을 분석해,
    해당 뉴스에서 가장 많이 언급 된 단어를 알 수 있는
    <font color=hotpink size=4><b>wordcloud 분석</b></font>을 수행해보겠다.
    이 분석으로 우리는 해당 기사의 여론을 알 수 있다.
    <br>
    분석할 뉴스는 아래와 같다.
    <img src="/image/NLP/news.PNG">
    <img src="/image/NLP/comment_ratio.PNG">
    <font size=2 color=gray>(링크: https://news.naver.com/main/ranking/read.nhn?rankingType=popular_memo&oid=056&aid=0010672808&date=20190220&type=2&rankingSectionId=102&rankingSeq=2)</font>
    <br>
    댓글 분석을 위해 먼저,
    <b>총 9,809개의 댓글을 크롤링</b>한다
    <br>
    <font size=5><b>[크롤링]</b></font>
    {% codeblock lang:Python %}
      # 라이브러리
      from bs4 import BeautifulSoup
      import requests
      import re
      import sys
      import pprint

      # 댓글 저장 리스트 초기화
      List=[]

      # 네이버 뉴스 url을 입력
      url="https://news.naver.com/main/ranking/read.nhn?rankingType=popular_memo&oid=056&aid=0010672808&date=20190220&type=2&rankingSectionId=102&rankingSeq=2"
      oid=url.split("oid=")[1].split("&")[0]
      aid=url.split("aid=")[1]
      page=1
      header = {
        "User-agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36",
        "referer":url,
      }
      while True :
        c_url="https://apis.naver.com/commentBox/cbox/web_neo_list_jsonp.json?ticket=news&templateId=default_society&pool=cbox5&_callback=jQuery1707138182064460843_1523512042464&lang=ko&country=&objectId=news"+oid+"%2C"+aid+"&categoryId=&pageSize=20&indexSize=10&groupId=&listType=OBJECT&pageType=more&page="+str(page)+"&refresh=false&sort=FAVORITE"
      # 파싱
        r=requests.get(c_url,headers=header)
        cont=BeautifulSoup(r.content,"html.parser")
        total_comm=str(cont).split('comment":')[1].split(",")[0]

        match=re.findall('"contents":([^\*]*),"userIdNo"', str(cont))
      # 댓글을 리스트에 중첩
        List.append(match)
      # 한번에 댓글이 20개씩 보이기 때문에 한 페이지씩 댓글 크롤링.
      # 페이지 내, 댓글의 개수가 20개보다 적을 시 마지막 페이지임을 식별
        if int(total_comm) <= ((page) * 20):
            break
        else :
            page+=1


      # 여러 리스트들을 하나로 묶는 함수
      def flatten(l):
        flatList = []
        for elem in l:
            # if an element of a list is a list
            # iterate over this list and add elements to flatList
            if type(elem) == list:
                for e in elem:
                    flatList.append(e)
            else:
                flatList.append(elem)
        return flatList


      # 리스트 결과 확인
      # flatten(List)

      import codecs
      file = codecs.open("./comment/news_test_set.txt",'w',encoding='utf8')
      # file = codecs.open("./comment/news_test_set.txt",'a',encoding='utf8')
      file.write("\n".join(str(v) for v in List))
      file.close()
    {% endcodeblock %}
    <br>
    크롤링된 댓글은 다음과 같이
    <b>txt 파일로 저장</b>된다.
    <br>
    <img src="/image/NLP/crolling_result.PNG">
    <br>
    크롤링된 댓글에서 <b>명사를 추출</b>하고,
    어떤 단어가 가장 많이 나왔는 지 <b>빈도수를 체크</b>한다.
    <b><font color=hotpink>언급 된 빈도가 큰 150가지의 단어</font></b>들로 wordcloud를 만든다.
    <br>
    pytagcloud의 경우, 한글을 지원하지 않으므로
    한글 폰트<font size=2>(ttf,otf 파일)</font>를 다운받아 <b>pytagcloud\fonts</b> 폴더 내에 저장하고,
    해당 경로 내, <b>fonts.json 파일</b>에 아래 처럼 코드를 추가한다.
    <br>
    {% codeblock lang:json %}
      [
        {
          "name": "Korean",
          "ttf": "본인이 다운 받은 한글 파일",
          "web": "http://fonts.googleapis.com/css?family=Nobile"
        },
        {
          "name": "Nobile",
          "ttf": "nobile.ttf",
          "web": "http://fonts.googleapis.com/css?family=Nobile"
        },
    {% endcodeblock %}
    <br>
    <font size=5><b>[WordCloud]</b></font>
    {% codeblock lang:Python %}
      import os
      import matplotlib.pyplot as plt
      from collections import Counter
      # KoNLPy v0.4.5. 상위 버전부터 Twitter가 Okt로 대체
      # twitter로 쓴다면 이하의 에러 발생
      # "Twitter" has changed to "Okt" since KoNLPy v0.4.5.
      from konlpy.tag import Okt
      import pytagcloud

      f = open("./comment/news_test_set.txt",'r',encoding="UTF8")
      data = f.read()

      spliter = Okt()
      nouns = spliter.nouns(data)

      count = Counter(nouns)
      tag = count.most_common(150)
      taglist = pytagcloud.make_tags(tag,maxsize=80)

      pytagcloud.create_tag_image(taglist, './wordcloud/news_wordcloud.jpg', size=(900, 600), fontname='Korean', rectangular=False)
      f.close()
    {% endcodeblock %}
    <br>
    가장 <b>많이 언급된 단어들을 나열</b>해보자.
    <img src="/image/NLP/count_30.PNG">
    <br>
    <b><font color=hotpink>wordcloud 분석의 결과</font></b>는
    다음과 같다.
    <br>
    <img src="/image/NLP/news_wordcloud.jpg">
    <br>
    <font size=5><b>[결론]</b></font>
    해당 분석을 통해
    <b>뉴스에 대한 여론이 꽤나 <font color=red>부정적임</font>을 알 수 있었다.</b>
    <br>
    <br>
    <br>
    <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
    <font size=5><b>[출처]</b></font>
    네이버 뉴스 댓글 크롤링
    https://m.blog.naver.com/PostView.nhn?blogId=seodaeho91&logNo=221273565367&proxyReferer=https%3A%2F%2Fwww.google.com%2F
    <hr/>
    텍스트마이닝 : 파이썬 워드클라우드 만들기
    http://blog.naver.com/PostView.nhn?blogId=imsam77&logNo=221260319159&categoryNo=13&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView
    </div>
  </div>
</font>
