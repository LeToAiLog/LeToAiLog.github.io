---
title: Lily's memory (타워 디펜스형 게임 with Unity)
description: Unity를 사용하여 대학교 프로젝트로 만든 타워 디펜스 게임.
date: 2020-12-13 17:09:03 +09:00
categories: [Unity Game]
tags: [Unity, Game, Unity 2D, Tower defence, Game character, 게임, 유니티, 2D 유니티, 타워 디펜스, 모바일, 모바일 게임, Mobile game, Mobile, 게임 개발, 1인 개발자, 1인 게임]
pin: true
math: true
mermaid: true
image:
  path: /assets/img/smoothed-particle-hydrodynamics/
  # 대표 이미지의 애니메이션 적용
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 
---
<!--  -->
# **타워 디펜스 게임**
<hr>

## **Lily's Memory**
<br>
<hr>

### **Introduction**

Android를 대상으로 제작된 Lily's Memory는 성 지키기를 모티브로 만들었던 게임이다.
대학교 프로젝트 당시에 교수님께서 발표에 게임의 Story를 무조건 이야기해야 한다는 조건을 넣으셨었다.
당시 수업은 유니티에서 3D를 기반으로 하는 게임을 만드는 것이었지만 평소에 2D 게임에 관심이 많았던 나는 교수님께 허락을 받고 2D로 게임을 제작하게 되었다.

성 지키기 같은 디펜스 게임을 좋아했었던 나는 단지 내가 좋아하는 게임을 한 번 만들어보고 싶은 마음에 시작하게 되었지만 게임의 Story를 생각하는게 쉬운일이 아니었다. 지금은 1인 개발자로써 살아가고 있고 혼자 Story를 짜보는 경험이 지금 나에게 많은 도움이 되었다.

게임 Story는 굉장히 진부한 내용이었다. 지금 생각해보면 손, 발이 오그라드는 설정이다.

> 주인공인 Lily는 20년간 기억이 없다. 이유는 마족이 20년 후 전쟁을 시작할 것이라는 신의 계시를 받지만 여신이 해당 세계의 균형을 위해 지원한 천사가 영혼이 없는 인간 아이의 몸으로 들어가면서 생긴 일종의 패널티라는 설정이다. 이 사실은 왕만 알고 있으며 여신과의 약속때문에 Lily에게 말하지 못하고 출생이 다르다는 이유로 차별 받는 Lily를 지키기위해(사실 게임을 시작하려면 보내야해서) 마족과 경계를 접하고 있는 성에 유배시키면서 게임이 시작된다.
> 유배되어 있던 성에서 왕이 보내준 상자에 담겨있던 꽃잎을 만지자 천계에 있던 천사를 소환하게 된다. 이 후 자신의 기억 단편을 찾게되고 마족과 전쟁하면서 꽃잎을 모아 기억과 운명을 찾아가는 Story.
<hr>

### **Technology**

4주동안 게임 프로젝트만 Unreal로 1개, Unity로 1개를 제작하다 보니 신경을 많이 쓰지 못하였다. 특히 그때 당시에 Asset이 마음에 드는 것이 없어서 직접 제작하여 시간이 더 오래 걸렸다.

캐릭터 디자인과 게임 시작 전 움직이는 하늘 그림, 성, 산, 바닥 등을 직접 그리는 것이 큰 경험이 되어 지금도 게임 개발에서 Ai를 사용하여 초안을 잡고 리터칭으로 내가 원하는 Asset을 제작하고 있다. 물론 상업적으로 이용이 가능한 모델을 사용중이다. 단지 아쉬웠던 것은 한 주만 코드를 작성하는데 시간을 할애했다는 것이다. 언리얼은 블루프린트로 작업하면서 게임 로직에 2주, 에셋 찾고 적용하는데 2주해서 총 4주안에 게임의 구색만 맞췄다.

코드를 한 주 정도만 작성하게 되면서 게임 최적화는 물건너 갔고 원하던 기능도 구현을 다 하지 못했다. Deadline에 크런치 타임을 즐기는 직장인의 모습이 떠올랐었다. 그래도 제한된 시간 내에 내가 얼마만큼 할 수 있는지 객관적으로 평가해 볼 수 있는 시간이어 유의미했다.

#### **Particle system**
파티클 시스템으로 터치시 반짝이는 효과를 주어 게임에 생동감을 넣어줬다. 효과는 확실하게 게임이 지루해보이지 않았다. 다만 리소스 관리는 나락으로 떨어졌다. IEnumerator를 사용하여 생성하고 입자마다 각기 다른 크기와 Vector값을 주어 이 vector를 또 색상에 이용하여 조금 다른 양상을 보이도록 만들었다. 결과 값은 게임에서 보이는대로 이다.

#### **Projectile**
사실 이 부분이 제일 아쉽게 느껴진다. 아무리 촉박한 기한이었어도 화살이 발사되었을 때 머리부분이 고정으로 회전하지 않아 굉장히 어색한 투사체가 완성되었다. 이 때문에 게임을 테스트할 때마다 몰입감이 굉장히 깨졌었다. 몬스터가 특정 범위 안에 들어오면 Instantiate를 통해 투사체를 생성하고 rigid.velocity에 Vector2에서 부딪히는 대상의 x좌표의 값과 y에 중력값을 불러와 투사체가 몬스터를 향해 날아갈 수 있도록 구현했었다.

#### **Moving background**
지정해 둔 속도와 시간값을 곱하여 변수에 저장해둔 뒤 mainTextureOffset 기능을 통해 Vector2의 x좌표에 저장해둔 값을 넣어주어 배경이 움직이는 것 처럼 보이게 구현했었다. 이 당시 궁금했던 점이라면 어차피 움직이는 사물은 구름에 한정되어 있고 그렇다면 배경과 구름을 분리하여 배경은 정적으로 처리하고 구름만 움직이게 한다면 리소스를 절약할 수 있을까라는 생각을 했었다. 결론은 Case by case 였다. 연산량이 부족하고 메모리가 부족하지 않은 환경이라면 지금처럼 배경 전체를 메모리에 올려놓고 한번에 처리하는 것이 좋다. 하지만 메모리가 부족하고 연산량이 충분하다면 구름을 각 Object로 만들어 메모리에 올라갈 용량을 줄이고 구름의 움직임을 각각 연산하는 것이 좋았다.
<hr>

<!-- 이미지 -->
<!-- ![평활 입자 유체역학 커널 그림](/assets/img/smoothed-particle-hydrodynamics/SmoothingKernelFigurewithWhiteBackground.png){:width="500" height="589" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"} 
_**<span style="color:deepskyblue; font-size:150%">Figure 1. </span>
<span style="color:gainsboro;font-size:150%">Particle approximation using particles within the particle range(ℎ), 𝑘ℎ is the particle range, $$r_{ij}$$ is the distance between the neighbor particle and the central particle(red).</span>**_ -->