---
layout: post
title:  "뷰포트의 알파, 베타, 그리고 런칭"
date:   2019-01-28 14:10:00 +09:00
author: Park, Sung-oh
categories: devblog
tags: [viewport, game-dev]
thumbnail-img: "/posts/181108-from_alpha_to_launching/cover.jpg"
---

<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/cover.jpg" class="image original-size on-post">

게임 하나를 만드는 데 얼마의 시간이 걸릴까요? 게임잼에선 48시간 만에 만들기도 하고, 급하게 만든 모바일 게임은 몇 달 만에 나오기도 하고, 로스트아크 같은 기대작은 수 년이 걸리기도 하죠.
그렇다면 1인 개발 모바일 퍼즐 게임은 얼마나 걸릴까요? 물론 상황마다 다를 것입니다.
 
한가지 확실한 건 저는 게임 **뷰포트(Viewport)**가 이 정도로 긴 시간과 큰 규모의 프로젝트가 될 줄 몰랐다는 겁니다. 처음에는 그저 다음 작품으로 이어지는 중간 다리 역할을 하는, 조그마한 인디 모바일 게임이 될 줄 알았습니다.
 
---

## 들어가기에 앞서, 뷰포트란?

제가 어떤 게임을 만들고 계신지 모르는 분은 뒤의 내용이 이해가 가지 않을 수 있습니다. 하지만 게임 소개가 주제가 아니니만큼 간단하게만 소개해드리겠습니다.
 
뷰포트는 **스토리 중심 모바일 퍼즐 게임**입니다. 3D 도형을 제공해주면, 그것의 위쪽 · 왼쪽 · 정면의 모습을 맞추는 방식입니다. 주인공은 정체 모를 실험에 참여하게 된 피험자이며, 실험 진행자가 화면에 적어주는 말을 보며 무슨 일이 일어나고 있는 것인지 파악하게 됩니다.

---
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/title-alpha.jpg" class="image original-size on-post"> 
 
인디 게임 뷰포트의 시작은 시간을 거슬러 2016년으로 갑니다. 전역한지 1년도 채 되지 않은 풋풋한 복학생(...)은 자기만의 게임을 만들고 싶었습니다. 고민을 거듭하며 여러 가지 게임을 기획하였고, 그중 가장 마음에 드는 하나를 골랐습니다.

*그러나 그 게임은 뷰포트가 아니었습니다.*
 
제가 선택했던 아이디어는 제 인생 첫 작품으로 만들기에는 스케일이 조금 커 보였습니다. 그래서 그 작품을 만들기 전에 **두어 달 동안 짧게** 빨리 만들 수 있을(것으로 보였던) 습작을 기획하게 됩니다.
 
**그게 바로 뷰포트입니다.**
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/viewport-alpha-03.png" class="image half on-post"> 
<p class="image-description on-post">핵심 기능만 구현한 뷰포트의 프로토타입 스크린샷</p>
 
당시에는 화면을 네 개의 작은 뷰포트로 나누고, 각각의 뷰포트를 조작할 수 있도록 만드는 것이 개발 과정에 있어서 가장 어려운 과제일 거라고 생각했습니다. 그래서 프로토타입을 만들 때 딱 세 가지만 구현해보았습니다.
 
1. 네 개의 뷰포트를 화면에 그린 후 각각의 뷰포트 조작할 수 있게 만들기
2. 하단의 도형 아이템을 끌어서 뷰포트에 내려놓을 수 있게 만들기
3. 놓여진 도형 아이템의 크기와 위치를 조절할 수 있게 만들기
 
다행히 몇 주 만에 상기한 핵심 기능은 구현할 수 있었습니다. 지금도 터치와 관련된 대부분의 코드는 저 시기에 작성한 것을 그대로 쓰고 있습니다. 신기할 따름이죠.
 
<div class="embed-container full-embed on-post">
	<iframe src="https://www.youtube.com/embed/E1HNf5FZ4wM?rel=0&showinfo=0" frameborder="0" allowfullscreen></iframe>
</div>
<p class="image-description on-post">뷰포트(Viewport) 알파 버전 - 테스트 영상</p>
 
화면에 네 개의 작은 뷰포트를 구성하고 그곳에 도형 아이템을 올려놓는 등의 기능은 구현했지만, 사실 정말 겉보기 기능만 구현한 것이지 핵심 시스템은 전혀 구현하지 않았습니다.
 
예컨대 제공된 퍼즐의 정답을 담고있는 파일도 없었고, 플레이어가 그린 그림을 담아낼 자료구조도 없었으며, 플레이어가 그린 그림이 정답과 동일한지 비교할 방법도 없었습니다. 이 부분은 쉬울 거라고 생각해서 프로토타입 버전에는 구현하지 않았거든요. 지나고 나서 생각해보면 그 부분이 제일 어려웠습니다. 헣.
 
덕분에 아예 도형을 그리는 방법 자체를 새로 기획했고, 필요에 의해 외부 에디터까지 만들었습니다. 다만 이곳에는 여백이 부족하므로, 그 얘기는 나중에 길-고 자-세히 작성할 개발 후기에 남기도록 하겠습니다 :)

*(생각해보니 그때 윈도우 앱으로 개발했는데, 지금 맥북으로 갈아타버렸네요. 망했습니다.)*

---
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/title-beta.jpg" class="image original-size on-post"> 
 
여름 방학이 반쯤 지났을 때, 본격적으로 뷰포트(Viewport)를 개발하기 시작했습니다. 무려 한 학기 휴학까지 하면서 말이죠. (여담이지만 한 학기 정도는 휴학을 해보시길 추천합니다. 우리는 몇 달 정도 하고 싶은 일에 몰두해 볼 자격이 있어요.)
 
<div class="image-grid on-post">
	<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/Ailien_Isolation_04.jpg" class="image fit"> 
	<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/Fallout_4_pipboy.png" class="image fit"> 
</div>
<p class="image-description on-post">터미널 스크린 UI를 활용하는 '에일리언 아이솔레이션'과 '폴아웃4'</p>
 
 
저는 프로그래머이기 때문에 예쁘고 화려한 비주얼을 구현할 수 없었습니다. 그래서 최대한 덜 꾸며놓고 원래 이게 컨셉이었던 척 할 수 있을 방안을 모색했죠. 그렇게 **터미널 스크린 컨셉의 UI**를 구상하게 됩니다. *(생계형 디자인)*
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/viewport-beta-04.png" class="image half on-post"> 
<p class="image-description on-post">베타 버전의 인게임 플레이 화면</p>
 
**모든 UI를 단색**으로 칠했고, **곡선은 최대한 지양**했습니다. 오로지 직선 · 사각형 · 텍스트로만 화면을 가득 메웠고, 조금 더 터미널 스크린처럼 보이도록 만들기 위해 화면 가장자리에 휘어짐 효과를 넣기도 했습니다.
 
그리고 처음 생각과 달리 개발 기간이 길어지면서 **스토리의 중요도**도 같이 높아졌습니다. 게임의 전반적인 분위기 자체를 무겁게 설정했고, 스토리도 꽤 진지한 느낌으로 구상했습니다. 스토리를 기획하고 나니 UI 컨셉에 정당성이 부여가 되는 효과도 있었습니다. *'주인공은 정체 모를 실험에 참여하였고, 지금 보고 있는 것은 실험용 화면이다'* 라고 말이죠.
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/viewport-beta-01.png" class="image half on-post"> 
<p class="image-description on-post">베타 버전의 메인 화면</p>
 
베타 버전을 개발하는데 2년 가까운 시간이 걸린 데 별로 특별한 이유는 없습니다. 저는 대학생이었고, 개발 기간 중 세 번의 학기가 끼어있었던 것 뿐이었죠. (2년 사이에 대충 9개월 정도는 개발을 못했다고 보시면 됩니다)
 
2018년 초 스토리를 거의 다 가다듬었고, 5월에 정말 좋은 기회를 통해 유니티 개발자 컨퍼런스인 **유나이트 2018 시연 행사**를 가지게 되었습니다. 이때 받았던 피드백을 통해 베타 테스트 직전에 많은 개선을 할 수 있었죠.
 
<div class="embed-container full-embed on-post">
	<iframe src="https://www.youtube.com/embed/WAb0OW9TGc4?rel=0&showinfo=0" frameborder="0" allowfullscreen></iframe>
</div>
<p class="image-description on-post">뷰포트(Viewport) 베타 버전 - Stage207 플레이 영상</p>
 
유나이트 시연 때 조작과 관련한 피드백을 많이 받아서 **조작감 개선**만 거의 한 달간 진행했습니다. 그리고 동시에 **안드로이드 베타 테스터** 모집도 진행했죠. 2018년 6월에 진행한 안드로이드 베타 테스트엔 50여 분께서 참여해주셨습니다. 참고로 위 영상은 실제로 베타 테스트 때 사용했던 빌드로 촬영한 영상입니다.
 
거의 모든 테스터 분께서 테스트가 끝난 후 후기 설문지를 작성해주셨습니다. 그 소중한 후기가 하나하나 모여 이 게임을 런칭 단계까지 이끌어주었습니다.

---
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/title-launching.jpg" class="image original-size on-post"> 

베타 테스트 후기 중 그래픽 관련 내용 중에선 '눈이 아프도록 밝은 색'과 '어울리지 않는 폰트'에 대한 지적이 제일 많았습니다. 그래서 런칭 버전을 준비할 때 그 두 가지를 가장 먼저 손보았죠.
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/change-01.png" class="image fit on-post"> 
<p class="image-description on-post">메인화면의 변화 (왼쪽이 베타 버전, 오른쪽이 런칭 버전)</p>
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/change-03.png" class="image fit on-post"> 
<p class="image-description on-post">화면 휘어짐 효과의 개선 (왼쪽이 베타 버전, 오른쪽이 런칭 버전)</p>

우선 모든 **눈이 아프게 밝았던 색상을 파스텔톤으로** 바꾸었습니다. 터미널 스크린이라는 디자인 컨셉은 유지하되, 눈의 피로는 줄이는 방향으로 말이죠. 그 외에도 플레이어들을 불편하게 했던 몇 가지 요소들을 개선하였습니다. (가장자리 텍스트가 두 겹으로 보이는 것, 지나치게 잦은 글리치 효과 등)
 
또한 뷰포트 로고를 일러스트레이터로 자체 제작하였고 *(덕분에 살면서 일러 처음 써봤습니다)*, 이전에는 나눔고딕코딩 폰트만 사용했던 것과 달리 **네 가지 폰트**를 상황에 따라 다르게 적용했습니다.
 
<img src="{{ site.baseurl }}/posts/181108-from_alpha_to_launching/change-02.png" class="image fit on-post"> 
<p class="image-description on-post">크기 조절 손잡이의 변화 (왼쪽이 베타 버전, 오른쪽이 런칭 버전)</p>
 
두 방향으로만 크기 조절이 가능하였던 것을 네 방향 모두 조절이 가능하게 개선하였습니다. 그에 따라 크기 조절 손잡이의 디자인도 바뀌게 되었죠. 그 외에도 여기서 보여드릴 순 없지만, 난이도의 흐름을 부드럽게 만들기 위해 열 개가 넘는 퍼즐을 재배치 하고, 없애고, 새로 만들었습니다.

<div class="embed-container full-embed on-post">
	<iframe src="https://www.youtube.com/embed/A0aKY4PPBYs?rel=0&showinfo=0" frameborder="0" allowfullscreen></iframe>
</div>
<p class="image-description on-post">뷰포트(Viewport) 런칭 버전 - Stage207 플레이 영상</p>

그리고 베타 버전에는 없었던 **구글 연동을 통한** 게임 데이터 클라우드 저장 기능, 스코어보드 및 리더보드, 업적 기능이 추가되었습니다. 정말로 런칭을 앞두고 있다는 뜻이죠.

---

## 혼자서는 변화를 만들 수 없었습니다.
 
2016년 7월 프로토타입을 만들기 시작해서, 2018년 11월 런칭 버전이 완성되었습니다. 작업률은 결코 선형적으로 증가하지 않았고, 작업 속도도 결코 안정적이지 않았습니다. 혼자서 개발을 할 때 직면하는 가장 큰 문제는 객관성을 잃어버린다는 것입니다. 아침에 눈을 뜨고 작업 공간에 도착하는 순간부터, 저녁을 먹기 위해 집으로 돌아갈 때까지 같은 화면만 몇 시간을 보게 됩니다. 이게 며칠이고 몇 달이고 반복되다 보면 내가 보고 있는 게임 화면이 예쁜 건지, 직관적인 건지, 바보 같은 건지 분간이 안 가기 시작합니다.
 
**그래서 중요한 게 플레이어의 피드백입니다.**

어떤 방식이든 상관없습니다. 시연 행사든, 베타 테스트든, 가족을 붙잡고 질문을 하든 말이죠. 

...
 
제 게임은 2016년 7월 개발을 시작해서 2018년 5월이 될 때까지 한 번도 외부에 공개된 적이 없었습니다. 그러다가 유나이트 2018에서 시연을 할 기회가 생겨 반강제로(...) 게임을 공개하게 되었죠.
 
이전까지 저는 이 게임의 조작이 어려울 거라고 단 한 번도 생각해 본 적이 없었습니다. 그러나 시연 행사 내내 가장 많이 지적을 받았던 점은 바로 조작감이었죠. 저는 몰랐던 겁니다. 긴 개발 기간 동안 저는 이미 뷰포트 조작에 너무 익숙해져 버렸다는 사실을 말이죠.
 
고작 이틀간의 시연 행사였지만, 느낀 점이 정말 많았습니다. 2년간 바꾼 적 없던 조작 메커니즘을 시연 끝나고 한 달 만에 싹 바꿨으니 가히 대격변이라 부를 만했죠.
 
...
 
그래서 베타 테스트를 정말 꼼꼼히 준비했습니다. 베타 테스트 자체보다는 베타 테스트 후기용 설문조사에서 물어볼 내용을 무지하게 꼼꼼하게 만들었다고 해야겠네요. 그래픽은 어땠는지, 사운드는 어땠는지, 스토리는 이해하기 쉬운지 등... 지금 생각해보니 그렇게 길고 귀찮은 설문지를 어떻게 그렇게 다들 친절하게 채워주셨는지 감사할 따름입니다.
 
베타를 성공적으로 마무리하고, 테스터 분들의 소중한 후기를 모아서 정리했고, 두 번째 대격변을 거치게 되었고, 런칭을 하게 되었습니다.
 
...

플레이어 분들의 피드백이 없으면 게임은 발전할 수 없습니다. 게이머였고, 게임 리뷰어였다가, 이젠 게임을 직접 만들고 있는 저로서, 게임에게 게이머가 얼마나 중요한 존재인지 확실히 느끼게 되었습니다. 플레이어가 없다면, 게임도 없습니다.

---

**뷰포트(Viewport) 구글 플레이 주소:** <https://play.google.com/store/apps/details?id=com.dimareagames.viewport>

<div class="embed-container full-embed on-post">
	<iframe src="https://www.youtube.com/embed/JRfKDSGoIUw?rel=0&showinfo=0" frameborder="0" allowfullscreen></iframe>
</div>
<p class="image-description on-post">뷰포트 공식 트레일러 영상</p>
