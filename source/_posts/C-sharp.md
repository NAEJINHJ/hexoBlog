---
title: "고 & 스톱"
categories:
- Project
- C#
tags:
- C#
- game
- Project
---
<img src="/image/gostop/main.PNG" width="1200px">
<hr/>
<img src="/image/gostop/summary.PNG" width="800px">
<hr/>
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:30px 0;">
  <font size=4 color=purple><b>[목차]</b></font>
  <font size=4>
    [1. HOME](#section1)
    [2. HOW TO](#section2)
    [3. GAME PLAY](#section3)
    [4. GO STOP](#section4)
    [5. SCORE](#section5)
    [특이 사항](#section6)
  </font>
</div>
<hr/>
<div style="background-color:rgba(0, 0, 0, 0.0470588); text-align:center; vertical-align: middle; padding:5px 0;">
  <font size=3 color=gray>
    <div id='section1'/>
    <font size=5><b>1. HOME</b></font>
    <br>
    <img src="/image/gostop/home.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <font color=purple size=4><b>[START button]</b></font>
      <br>
      <b>MouseMove 이벤트</b>:
      버튼에 마우스 올리면, 웃고 있는 캐릭터 이미지로 변경
      <b>MouseLeave 이벤트</b>:
      마우스가 버튼 밖으로 벗어나면, 다시 원래의 이미지로 돌아감
      <b>Click 이벤트</b>:
       <b>게임 플레이 화면</b>으로 전환
      <hr/>
      <font color=purple size=4><b>[HowTo button]</b></font>
      <br>
      <b>MouseMove 이벤트</b>:
      버튼에 마우스 올리면, 웃고 있는 캐릭터 이미지로 변경
      <b>MouseLeave 이벤트</b>:
      마우스가 버튼 밖으로 벗어나면, 다시 원래의 이미지로 돌아감
      <b>Click 이벤트</b>:
       <b>게임 룰 설명 화면</b>으로 전환
      <hr/>
      <font color=purple size=4><b>[화면 전환 방식]</b></font>
      <br>
      1) HOME 폼을 <b>숨김</b>
      2) 실행하고 싶은 폼의 <b>객체 생성</b>하여 실행 시킴
      3) HOME 폼 <b>닫음</b>
      <br>
    </div>
    <hr/>
    <div id='section2'/>
    <font size=5><b>2. HOW TO</b></font>
    <br>
    <img src="/image/gostop/howto.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <font color=purple size=4><b>[룰 설명]</b></font>
      이미지로 제작, <b>backgroundimage</b>로 설정
      <hr>
      <font color=purple size=4><b>[Click 이벤트]</b></font>
      <b>화살표 버튼 클릭</b> 시, 다시 <b>홈 화면으로 전환<b>
      <br>
    </div>
    <hr/>
    <div id='section3'/>
    <font size=5><b>3. GAME PLAY</b></font>
    <br>
    <img src="/image/gostop/gameplay1.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      총 <b>5개의 패널</b>로 구성
      <hr/>
      <font color=purple size=4><b>[computerCardPanel]</b></font>
      <br>
      위에서 부터 <b>컴퓨터 패</b>를 놓음
      <hr/>
      <font color=purple size=4><b>[computerScorePanel]</b></font>
      <br>
      컴퓨터가 <b>얻은 카드</b> 순서대로 정렬
      <b>점수</b> 출력
      <b>GO를 한 횟수</b>를 출력
      <hr/>
      <font color=purple size=4><b>[playPanel]</b></font>
      <br>
      실제 <b>게임의 필드(바닥)</b>에 해당하는 패널
      <hr/>
      <font color=purple size=4><b>[UserScorePanel]</b></font>
      <br>
      유저가 <b>얻은 카드</b> 순서대로 정렬
      <b>점수</b> 출력
      <b>GO를 한 횟수</b>를 출력
      <hr/>
      <font color=purple size=4><b>[UserCardPanel]</b></font>
      <br>
      <b>유저의 카드 패</b>를 놓음
      카드 패는 <b>버튼으로 구성</b>
      <hr/>
      <font color=purple size=4><b>[Card Setting]</b></font>
      <br>
      <b>카드 클래스</b> 구현
      생성자에서 카드의 인덱스, 이미지, 월과 가치 값 세팅
      <br>
      <b>크기 48의 클래스 배열</b> 생성
      카드를 순서대로 저장시킨 뒤, 랜덤하게 섞어줌
      <br>
      <b>분배</b>
      0~9 : 유저의 카드패
      10~ 19 : 컴퓨터의 카드패
      20 ~ 27: 필드에 깔리는 카드
      28 ~ 47: 뒤집어져 있는 카드 더미
      <hr/>
      <font color=purple size=4><b>[이미지 예외 처리]</b></font>
      <br>
      이미지 세팅 과정에서 <b>필요한 이미지가 존재하지 않을 시</b>,
      <b>예외 처리 에러</b> 실행
      <br>
    </div>
    <img src="/image/gostop/gameplay2.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <font color=purple size=4><b>[GAME START]</b></font>
      <br>
      필드에 카드가 <b>랜덤하게 8장</b> 깔림
      <font size=2>(필드에 깔린 카드들은 <b>리스트</b>로 관리)</font>
      Card Setting 과정에서 분배받은 8장의 카드에 대해,
      <b>picturebox 생성</b>하는 식으로 구현
      동일한 월을 갖는 카드가 있을 시, 일정한 간격으로 겹쳐지게 함
      <font size=2>(각 월마다 기준 좌표가 존재)</font>
      <hr/>
      <font color=purple size=4><b>[User's Card]</b></font>
      <br>
      10개의 버튼(유저패)의 <b>backgroundimage</b>
      분배받은 카드의 이미지
      <br>
      <b>버튼 클릭</b> 시,
      유저가 그 카드를 낸 것으로 간주
      해당 버튼의 사용을 금지시키고, 더이상 보이지 않도록 설정
      <hr/>
      <font color=purple size=4><b>[총통]</b></font>
      <br>
      유저 혹은 상대 패에 <b>같은 월의 카드가 4장</b> 있을 시,
      <b>총통</b>임을 메시지 박스로 보여주고,
      즉시 <b>50점 획득해 승리</b>하도록 함
      <br>
    </div>
    <img src="/image/gostop/gameplay3.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <font color=purple size=4><b>[User's turn]</b></font>
      <br>
      필드에 일치하는 월이 있는지,
      해당 월의 카드가 몇 장 있는지 체크
      조건에 따라 <b>득점되어 필드에 추가</b> or <b>똥 처리</b>
      <br>
      <b>* 득점한 카드</b>
      가치 값에 따라 다른 좌표로 정렬되어
      각 score 패널에 표시
      이후 상대의 turn으로 바뀜
      <hr/>
      <font color=purple size=4><b>[Computer's turn]</b></font>
      <br>
      낸 카드는 숨겨짐
      <b>delay 함수</b> 사용
      카드를 내거나 이벤트가 발생되었을 때,
      육안으로 잘 보이게 하기 위함
      <font size=2>(시간 지연 함수)</font>
      <br>
    </div>
    <img src="/image/gostop/gameplay4.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <font color=purple size=4><b>[Computer's turn]</b></font>
      <br>
      가진 패의 <b>앞에서부터 카드를 내도록</b> 함
      <hr/>
      현재 점수와 고의 횟수에 대한 정보가
      각 스코어 패널의 레이블에 표시 됨
      <hr/>
      <font color=purple size=4><b>[똥 Event]</b></font>
      더미에서 카드를 뒤집고
      <b>3장이 겹치게</b> 되었을 때 발생
      > <b>똥 이미</b>지 출력, 3장의 카드는 <b>그대로 필드에</b> 남김
      <font size=2>(만약 필드에 남은 3장의 카드와 같은 월의 카드를 낸다면 총 4장으 얻게 됨)</font>
      <br>
    </div>
    <img src="/image/gostop/gameplay5.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <font color=purple size=4><b>[Score]</b></font>
      <br>
      각 피의 개수에 따른 점수
      홍단 / 청단 / 초단
      고도리
      3광 / 4광 / 5광
      피박
      고박
      고 횟수 당 1점 추가
      <hr/>
      <font color=purple size=4><b>[Calculating]</b></font>
      <br>
      <b>리스트</b>로 상대와 내가 <b>획득한 카드의 인덱스</b> 저장해,
      이를 토대로 점수 계산
      <br>
      <b>* 이벤트 발생</b> 시,
      <font size=2>(홍단/청단/초단, 고도리, 3광/4광/5광, 똥)</font>
      <b>델리게이트</b>를 사용
      이미지 출력과 점수 계산이 되도록 구현
      <hr/>
      <font color=purple size=4><b>[Game Over]</b></font>
      <br>
      남은 더미 카드 수 소진
      스탑 선택 시
      <br>
    </div>
    <hr/>
    <div id='section4'/>
    <font size=5><b>4. GO STOP</b></font>
    <br>
    <img src="/image/gostop/gostop.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      GO의 여부를 묻는 폼
      <b>7점 이상 획득</b> 시 생성
      <br>
      <b>7점 이하</b>까지는 <b>피박이 적용되지 X</b>
      카드가 추가되어 <b>면박</b>이 될 경우,
      점수가 하락하지만 GO/STOP 선택은 가능
      <hr/>
      <font color=purple size=4><b>[GO 선택]</b></font>
      <br>
      GO 이미지가 뜸
      점수와 GO의 횟수 하나씩 증가
      게임 계속 진행
      <hr/>
      <font color=purple size=4><b>[STOP 선택]</b></font>
      <br>
      <b>유저의 승리</b>로 게임 종료
      게임 종료 시, <b>스코어폼</b>으로 화면 전환
      <hr/>
      <font color=purple size=4><b>[선택 결과 전달]</b></font>
      <br>
      어떠한 버튼을 선택했는지에 대한 정보는
      <b>DialogResult</b>를 통해 게임플레이 폼으로 전달
      어떤 버튼을 선택했는지에 따라
      다른 이미지가 띄워짐
      <br>
    </div>
    <hr/>
    <div id='section5'/>
    <font size=5><b>5. SCORE</b></font>
    <br>
    <img src="/image/gostop/score.PNG" width="800px">
    <div style="background-color:rgba(145, 60, 189, 0.3); text-align:center; vertical-align: middle; padding:5px 0;">
      <b>2개의 패널</b>로 구성
      <font size=2>(컴퓨터용 / 유저용)</font>
      <hr/>
      <font color=purple size=4><b>[게임 결과]</b></font>
      <br>
      색으로 승패 표시
      캐릭터 표정 & 도장 이미지
      승자의 패널에는 <b>점수와 획득 금액 출력</b>
      <font size=2>(무승부 시, 우측과 같은 화면 띄워짐)</font>
      <br>
    </div>
    <hr>
    <div id='section6'/>
    <font color=purple size=4><b>[특이 사항]</b></font>
    <br>
    - 보너스 패, 흔들기 등을 생략해 프로젝트 스케일 조정
    - 게임에 사용된 이미지 직접 제작
    - 버전별 업데이트 내역 관리하여 효율적인 작업 수행
    <br>
  </font>
</div>
