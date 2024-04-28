---
title: 1. Lily's memory (타워 디펜스형 게임 with Unity)
description: Unity를 사용하여 대학교 프로젝트로 만든 타워 디펜스 게임.
date: 2020-12-13 17:09:03 +09:00
categories: [Unity Game]
tags: [Unity, Game, Unity 2D, Tower defence, Game character, 게임, 유니티, 2D 유니티, 타워 디펜스, 모바일, 모바일 게임, Mobile game, Mobile]
pin: true
math: true
mermaid: true
image:
  path: /assets/img/smoothed-particle-hydrodynamics/SmoothingKernelFigurewithWhiteBackground.png
  # 대표 이미지의 애니메이션 적용
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Particle approximation using particles within the particle range(ℎ), 𝑘ℎ is the particle range, $r_{ij}$ is the distance between the neighbor particle and the central particle(red).
---
<!--  -->
# **타워 디펜스 게임**
<hr>

## **Lily's Memory**
<br>
<hr>

### **Introduction**
<hr>

Android를 대상으로 제작된 Lily's Memory는 성 지키기를 모티브로 만들었던 게임이다.
대학교 프로젝트 당시에 교수님께서 발표에 게임의 Story를 무조건 이야기해야 한다는 조건을 넣으셨었다.
당시 수업은 유니티에서 3D를 기반으로 하는 게임을 만드는 것이었지만 평소에 2D 게임에 관심이 많았던 나는 교수님께 허락을 받고 2D로 게임을 제작하게 되었다.

성 지키기 같은 디펜스 게임을 좋아했었던 나는 단지 내가 좋아하는 게임을 한 번 만들어보고 싶은 마음에 시작하게 되었지만 게임의 Story를 생각하는게 쉬운일이 아니었다. 지금은 1인 개발자로써 살아가고 있고 혼자 Story를 짜보는 경험이 지금 나에게 많은 도움이 되었다.

게임 Story는 굉장히 진부한 내용이었다. 지금 생각해보면 손, 발이 오그라드는 설정이다.
<!-- 이미지 -->
<!-- ![평활 입자 유체역학 커널 그림](/assets/img/smoothed-particle-hydrodynamics/SmoothingKernelFigurewithWhiteBackground.png){:width="500" height="589" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"} 
_**<span style="color:deepskyblue; font-size:150%">Figure 1. </span>
<span style="color:gainsboro;font-size:150%">Particle approximation using particles within the particle range(ℎ), 𝑘ℎ is the particle range, $$r_{ij}$$ is the distance between the neighbor particle and the central particle(red).</span>**_ -->