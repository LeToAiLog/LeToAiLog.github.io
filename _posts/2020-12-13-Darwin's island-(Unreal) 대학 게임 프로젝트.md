---
title: Darwin's island (with Unreal engine)
description: Unreal engine을 사용하여 대학교 프로젝트로 만든 게임.
date: 2020-12-13 12:15:39 +09:00
categories: [Unreal Engine]
tags: [Unreal Engine, Game, Unreal Engine 3D, 게임, 언리얼 엔진, 3D 언리얼 엔진, PC, PC 게임, PC game, Computer game, 게임 개발, 1인 개발자, 1인 게임, 배틀 로얄, 서바이벌]
pin: true
math: true
mermaid: true
image:
  path: /assets/img/Darwin's-island/darwing_main_img.png
  # 대표 이미지의 애니메이션 적용
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Darwin's island
---
<!--  -->
# **Unreal Engine 게임 개발**
<hr>

## **Darwin's island**
<br>
<hr>

### **Introduction**
Darwin's island는 내가 재미있게 했던 워크래프트3에서 유즈맵인 다윈의 섬을 모티브로 만들어졌다. 여기에 스토리를 조금 더 가미해 국가간의 분쟁을 해소하는 방법으로 전쟁이 아닌 유전자 조작으로 만들어낸 몬스터(Player)로 서로 경쟁시켜 승리하는 국가가 보상을 받는 규칙을 설정했었다.
게임 제목인 Darwin's island처럼 몬스터(Player)들은 서로를 먹거나 섬내에 있는 동물들을 먹어 유전자 변이를 통해 환경에 극적으로 적응하면서 점점 강해질 수 있다.
>Darwin은 진화론의 아버지라 불린다
{: .prompt-info }

<hr>

### **Technology**

#### **Map**

##### **Land scape**
Map을 제작할 때 Landscape **<span style="color:red;font-size:100%">(1)</span>**에서 조각 **<span style="color:red;font-size:100%">(2)</span>** 을 선택하여 조각툴 **<span style="color:red;font-size:100%">(3)</span>** 로 마우스 좌클릭(지형 올림) 혹은 Shift + 마우스 좌클릭(지형 내림)을 통하여 굴곡진 지형 **<span style="color:red;font-size:100%">(4)</span>**을 만들고 조각툴 **<span style="color:red;font-size:100%">(3)</span>**외에 스무드, 평탄화, 침식, 수상침식, 노이즈를 이용하여 지형에 효과를 주었다. 또, Tool Settings에서 Tool Strength를 이용하면 지형 변화의 폭을 조절할 수 있고, Brush Settings에서 Brush Size로 영향 범위를 조절할 수 있다.
![Land scape](/assets/img/Darwin's-island/landscape.png){:width="258" height="424" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

완성된 Landscape에 Grass, Ground, Rock 등의 Texture를 입히기위해 Market Place에서 다운로드 받은 Texture Color Image(5)와 Texture의 Normal을 Import하여 가져온 후 Material(6)를 생성하여 편집했다.


#### **Moving background**


#### **Collision**


#### **Artificial inteligence(Enemy)**


<hr>

### **Reformation**

1. Server와 연동하여 Client 관리
2. Business model
3. Story 추가
4. 성 내부 구현
5. 유지, 보수의 효율성을 위한 Code refactoring
6. UI 개선
7. 몬스터 추가
8. Stage 추가
9. Sound and Effect 추가

등등 추가해야 할 일이 엄청 많았지만 욕심과 적절한 타협을 볼 수 밖에 없는 기간이었다.

<hr>

### **Darwin's island Play Video**
{% include embed/youtube.html id='wDahpiRtLeA' %}
<!-- 이미지 -->
<!-- ![평활 입자 유체역학 커널 그림](/assets/img/smoothed-particle-hydrodynamics/SmoothingKernelFigurewithWhiteBackground.png){:width="500" height="589" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"} 
_**<span style="color:deepskyblue; font-size:150%">Figure 1. </span>
<span style="color:gainsboro;font-size:150%">Particle approximation using particles within the particle range(ℎ), 𝑘ℎ is the particle range, $$r_{ij}$$ is the distance between the neighbor particle and the central particle(red).</span>**_ -->