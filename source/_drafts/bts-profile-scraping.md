---
title: "프로필 스크레이핑"
categories:
- BIGDATA
- Machine Learning
- Web scraping
tags:
- python
- web scraping
---
<hr/>
<font size=3>
  <b>
    <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
      위키피디아로 스크레이핑 실습하는건 질렸당!
      <br>
      <img src="/image/bts/penguin.gif" width="300px">
      <br>
      좀 더 색다르게 연습해보기 위해
      최애의 프로필을 긁어오기로 했따!
      <br>
      <br>
      <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
        우선 프로필을 긁어올 사이트에 접속 :)
        <font size=2 color=purple>(http://bts.ibighit.com/bts.php)</font>
        <img src="/image/bts/bighit_profile.PNG" width="1200px">
        <hr/>
        <br>
        F12를 눌러 개발자 도구를 띄운당
        <img src="/image/bts/site_code.PNG" width="1200px">
        <hr/>
        <br>
        프로필 사진을 포함하고 있는 태그를 확인한다!
        <img src="/image/bts/code.PNG" width="600px">
        <br>
        <font color=purple>img 태그</font>에 마우스를 살포시 올려놔보자!
        <img src="/image/bts/code_mouse.PNG" width="1200px">
        <br>
        (울먹)
        <img src="/image/bts/uu.PNG" width="400px">
        <hr/>
        <br>
        본격적으로 <font color=orange>Jupyter Notebook</font>을 사용해
        프로필을 긁어와보자!
        <br>
        {% codeblock lang:python %}
        from bs4 import BeautifulSoup
        import urllib.request as req
        {% endcodeblock %}
        <div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:10px 0;">
          <font color=purple><b>[BeautifulSoup]</b></font>
          HTML과 XML에서 간단히 정보 추출 가능
          <b>태그를 활용</b>해 필요한 데이터를 수집
          <font color=gray size=2>(태그 중심으로 분리 가능)</font>
          <hr/>
          <font color=purple><b>[urllib]</b></font>
          urllib는 URL을 다루는 모듈을 모아놓은 패키지
          <b>urllib.request 모듈</b>은 웹사이트에 있는 데이터에 접근하는 기능 제공
          인증, redirect, 쿠키처럼 인터넷을 이용한 다양한 요청과 처리 지원
          <hr/>
          <font color=purple size=2>(참조: https://medium.com/@katekim720/%EC%9B%B9-%ED%81%AC%EB%A1%A4%EB%A7%81%EA%B3%BC-%EC%8A%A4%ED%81%AC%EB%A0%88%EC%9D%B4%ED%95%91-%EB%B6%80%ED%84%B0-e32e237da3db)</font>
        </div>
        <br>
        {% codeblock lang:python %}
        url = "http://bts.ibighit.com/bts.php"
        res = req.urlopen(url)
        soup = BeautifulSoup(res,"html.parser")
        {% endcodeblock %}
        <br>
        {% codeblock lang:python %}
        profile_img = {"class":"bts-img"}
        eee = soup.find_all("img",profile_img)  #img 태그 전체 검색
        for m in eee:
          print("http://bts.ibighit.com/" + m.get("src") + "\n")
        {% endcodeblock %}
        <img src="/image/bts/print1.PNG" width="300px" height="400px">
        프로필 설명 img도 같은 방식으로 긁어오자!
        {% codeblock lang:python %}
        profile_desc = {"class":"bts-desc"}
        ddd = soup.find_all("img",profile_desc)
        for k in ddd:
          print("http://bts.ibighit.com/"+k.get("src")+"\n")
        {% endcodeblock %}
        <hr/>
        긁어온 png 이미지들을 화면에 뿌려보자!
        {% codeblock lang:python %}
        from IPython.display import Image
        for n in eee:
          link = "http://bts.ibighit.com/"+n.get("src")+"\n"
          display(Image(url = link))
        {% endcodeblock %}
        <img src="/image/bts/result1.PNG" width="600px">
        <hr/>
        <br>
        잘 출력되는 것을 확인해 봤다면,
        프로필 설명과 함께 뿌려보자!
        <img src="/image/bts/result2.PNG" width="600px" height="500px">
      </div>
      <br>
      <br>
      <img src="/image/bts/panda.PNG" width="400px">
      다음번엔 웹크롤링으로
      <font color=purple size=2>https://ef7890.ibighit.com/main/index?gclid=Cj0KCQiAg_HhBRDNARIsAGHLV53HBymFXA4mlwSGXjnhpGNO_6JUqV6wmYVUILp-HHucbMGNx9bpV5caAmGeEALw_wcB</font>
      여길 긁어보겠다!
      <br>
    </div>
  </b>
</font>
