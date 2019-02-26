---
title: "124 나라의 숫자"
categories:
- Coding Test
- Python
tags:
- coding test
- python
---

<img src="/image/coding_test/country124/desc.PNG" width="800px">
<hr/>

|  <center>n%3 == 0</center> |  <center>n%3 == 1</center> | <center>n%3 == 2</center> |
|:--------|:--------:|--------:|
| <center>4 </center> | <center>1 </center> | <center>2 </center> |

<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
  <font size=3 color=gray>
    파라미터 n을 3으로 나눈 나머지 (n%3)
    <font color=purple><b>n % 3 == 0 인 경우는 예외 처리</b></font>해야 함
    <font size=2>(n=15일 경우)</font>
    > 이 경우 n-1 값을 n으로!
    <hr/>
    나머지 값을 인덱스로 리스트에 접근하기 위해,
    <font color=purple><b>리스트의 값은 [4,1,2]</b></font>로 설정했음
    <hr/>
    <font size = 2 color=red>(python 3.x 버전은 나눗셈 연산으로 //을 쓸 것!)</font>
    <br>
    {% codeblock lang:python %}
      def solution(n):
      answer = ''
      arr = [4, 1, 2]
      rem = 0
      while(n>0):
          rem = n % 3
          n = n//3
          if rem == 0:
              n -= 1
          answer = str(arr[rem]) + answer
      return answer
    {% endcodeblock %}
  </font>
</div>
