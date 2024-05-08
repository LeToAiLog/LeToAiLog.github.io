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
Map은 게임에 있어서 그 게임만의 독창적인 분위기를 이끌어낼 수 있는 중요한 수단이다. 어떤 느낌의 그래픽을 가진 Asset들을 사용하는지에 따라 Player에게 주고 싶은 느낌을 게임 제작자의 의도와 맞게 끌어낼 수도 있지만 의도와는 다른 방향으로 Player들이 받아들일 수도 있다. 몰입감과 특유의 분위기로 매력을 어필할 수 있어서 매우 중요한 역할을 하지만 무작정 고사양의 Asset들을 가져다 쓸 경우 그 방대한 용량과 렌더링에 있어서 프레임드랍을 야기할 수 있으므로 적절한 선에서 타협해야 한다. 여기에서는 Landscape를 통해 지형에 변화를 주었고 Foliage를 통해 식생들을 배치하며 Percent Triangle을 조절해 생성되는 Polygon을 조절하였다.

##### **Landscape**
Map을 제작할 때 Landscape **<span style="color:red;font-size:100%">(1)</span>**에서 조각 **<span style="color:red;font-size:100%">(2)</span>** 을 선택하여 조각툴 **<span style="color:red;font-size:100%">(3)</span>** 로 마우스 좌클릭(지형 올림) 혹은 Shift + 마우스 좌클릭(지형 내림)을 통하여 굴곡진 지형 **<span style="color:red;font-size:100%">(4)</span>**을 만들고 조각툴 **<span style="color:red;font-size:100%">(3)</span>**외에 스무드, 평탄화, 침식, 수상침식, 노이즈를 이용하여 지형에 효과를 주었다. 또, Tool Settings에서 Tool Strength를 이용하면 지형 변화의 폭을 조절할 수 있고, Brush Settings에서 Brush Size로 영향 범위를 조절할 수 있다.

![Landscape](/assets/img/Darwin's-island/landscape.png){:width="258" height="424" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

완성된 Landscape에 Grass, Ground, Rock 등의 Texture를 입히기위해 Market Place에서 다운로드 받은 Texture Color Image **<span style="color:red;font-size:100%">(5)</span>**와 Texture의 Normal을 Import하여 가져온 후 Material **<span style="color:red;font-size:100%">(6)</span>**를 생성하여 편집했다.
![Landscape](/assets/img/Darwin's-island/Texture.png){:width="518" height="296" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

LandscapeCoords **<span style="color:red;font-size:100%">(7)</span>**의 디테일 패널에서 Mapping Scale을 조절하여 한 타일에 들어갈 텍스쳐 이미지의 크기를 조절하였고, 이 값을 UVs와 연결시켜 Texture Sample에 넣었다. 여기에서 RGB로 나가는 값들은 Normal **<span style="color:red;font-size:100%">(8)</span>** 의 경우 Texture에 저장되어 있는 RGB 가중치로 각 색의 세기 비율이고, 색 이미지 **<span style="color:red;font-size:100%">(9)</span>**의 경우 RGB값과 Alpha값으로 색과 투명정도의 값을  Layer Blend **<span style="color:red;font-size:100%">(10)</span>** 에 넘겨주었다. Layer Blend **<span style="color:red;font-size:100%">(10)</span>** 에서 Layer를 Texture image의 수만큼 늘려 Texture image들에 해당하는 이름을 가진 값들을 받아 Material **<span style="color:red;font-size:100%">(11)</span>** 에 넣었다. 들어가는 값들로는 Tile에 표현될 기본 색(RGB), 거칠기 (Alpha), Normal값(총 3개의 Layer Blend가 필요) Metallic (값이 높을수록 쇠와 가까운 질감을 표현)을 넣었고 Metallic의 값은 여기에서 0이다.

Material을 저장 후 World Outliner에서 Landscape **<span style="color:red;font-size:100%">(12)</span>**를 선택하여 디테일 패널 Landscape Material **<span style="color:red;font-size:100%">(13)</span>**에서 M_landscapemap을 넣고 해당 값들을 받아 Ground, Grass, Rock을 표현할 수 있도록 준비했다. Landscape **<span style="color:red;font-size:100%">(1)</span>**에서 Paint **<span style="color:red;font-size:100%">(15)</span>**를 선책하고 Layer **<span style="color:red;font-size:100%">(14)</span>**를 추가하여 Map에서 제일 많이 표현되는 Texture image를 선택 후 Map 전체를 덮고 나머지 Layer들로 세부적인 부분들을 표현했다. Texture sample**<span style="color:red;font-size:100%">(8, 9)</span>**은 Texture를 끌어다 놓기로 생성이 가능하다.
 
![Landscape](/assets/img/Darwin's-island/Layer_blending.png){:width="313" height="360" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

<hr>

##### **Foliage**

Market Place에서 다운로드 받은 식생을 Import 하여 폴리지 **<span style="color:red;font-size:100%">(18)</span>** 타입에 끌어다 놓아 추가했다. 브러시 **<span style="color:red;font-size:100%">(17)</span>** 크기로 배치할 식생들의 범위 **<span style="color:red;font-size:100%">(19)</span>** 를 지정해주고 페인트 밀도로 식생들이 얼마나 빽빽하게 배치될지를 정해 주었다. 식생들을 배치하게 될 때 고퀄리티의 그래픽이 중요하다면 표현되는 식생들의 디테일이 매우 중요하겠지만 대부분의 게임에서 식생들의 역할은 그 중요도가 낮기때문에 렌더링에 걸리는 시간과 소모되는 메모리를 줄이기 위해 각각의 식생들의 속성에 들어가 Percent Triangle **<span style="color:red;font-size:100%">(20)</span>**의 수치를 낮추어 주었다. 이 수치가 낮아지게 되면 식생의 면을 표현할 때 사용되는 삼각형의 수가 적어지게 되므로 적어지는 만큼 메모리를 아낄 수 있어 게임 환경을 쾌적하게 만드는 것이 가능하다.

![Landscape](/assets/img/Darwin's-island/Foliage.png){:width="538" height="298" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

<hr>

#### **User Interface**

![Blood effect](/assets/img/Darwin's-island/FBlood_effect_HUDoliage.png){:width="1869" height="378" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

게임의 몰입도를 위해서는 가능하면 기본 배치되는 글이나 버튼들은 숨기는게 좋다. 하지만 게임의 독특한 특성으로 인해 사용자에게 전달되어야 하는 정보까지 숨기게 되면 오히려 사용자의 불편함을 야기하게 된다. 따라서 User Interface는 각 게임에 따라 화면에 어떤 버튼들과 설명들이 출력되어야 하는지 반드시 고민해야 할 항목이다.

Darwin's island는 굉장히 간단한 조작법으로 인해 화면에 출력되는 글이 필요없었다. 다만 Hit point를 사용자가 알게 하기 위해서는 Bar형태로 표시하거나 숫자로 화면에 출력하거나 하는 방법을 사용해야만 했다. 하지만 깔끔한 Interface를 더 선호하는 나는 Bar나 Hit Point로 표시하기 보다 피가 없을때 이미지의 Alpha값을 조절하여 핏자국이 점점 보일 수 있도록 했다.

피가 없을때 핏자국을 표현하기 위해 Image_37 **<span style="color:red;font-size:100%">(1)</span>**에 들어가는 핏자국 이미지의 Alpha값을 0으로 초기설정 후 Text 0 **<span style="color:red;font-size:100%">(1)</span>** 에 Player의 Level 값을 불러올 수 있게 GetText 0 **<span style="color:red;font-size:100%">(2)</span>** 함수를 만들어 반환시키고 바인딩 **<span style="color:red;font-size:100%">(3)</span>** 했다.

![Blood effect](/assets/img/Darwin's-island/Blood_effect_BluePrint.png){:width="624" height="239" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

앞서 이미지에서 0으로 설정했었던 Alpha값을 Player **<span style="color:red;font-size:100%">(4)</span>**의 Health에서 CurrentHealth를 MaxHealth로 나누어 CurrentHealth가 작아질수록 0에 가까운 값을 받아 $1-$CurrentHealth $/$ MaxHealth의 식을 통해 LinearColor에서 Alpha값에 들어가는 값이 1에 가깝게하면 CurrentHealth가 0에 가까울수록 핏자국 이미지의 Alpha값이 1에 가까워지므로 이미지가 선명해진다. 아래는 핏자국 효과를 보여주는 결과 이미지이다.

![Blood effect](/assets/img/Darwin's-island/Blood_effect_image.jpg){:width="564" height="253" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

게임 승리와 패배의 이미지 **<span style="color:red;font-size:100%">(6)</span>** 를 나누고 같은 로직을 적용하여 Quit Game **<span style="color:red;font-size:100%">(7)</span>** 을 클릭시에 게임을 종료할 수 있게 만들었다. 게임을 종료하기 위해 Quit Game **<span style="color:red;font-size:100%">(7)</span>** 을 누를 수 있게 하려면 마우스 커서 활성화를 해야한다. Get Player Controller **<span style="color:red;font-size:100%">(8)</span>** 를 받아와 Show Mouse Cursor 이벤트에서 True로 설정하여 마우스 커서 활성화를 하였고, Player의 레벨이 10이상이거나 드래곤이 죽었을 때 승리 이벤트 **<span style="color:red;font-size:100%">(9)</span>**를 발생시키도록 했다.

![You died](/assets/img/Darwin's-island/You_died.png){:width="1375" height="339" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

![You died player](/assets/img/Darwin's-island/You_died_player.png){:width="1553" height="524" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

![You died widget](/assets/img/Darwin's-island/You_died_widget.png){:width="1557" height="328" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

승리 UI가 보이게 되면 Player (8)의 움직임을 멈추고 더 이상 조종이 불가능하게 Actor를 파괴했다. (9)와 같은 방법으로 Player가 죽었을 시 YOU DIED UI를 활성화하고 Actor의 움직임을 멈춘 후 파괴시킨 다음에 마우스 커서를 활성화하여 Quit Game (7)을 클릭할 수 있게 만들었다.

<hr>

#### **Artificial Intelligence**

AI는 중립과 적대적 관계로 나누었다. 중립 개체는 게임 시작시 목표 지점을 반복하여 이동하는 Patrol로 구현했고, 적대 개체는 일정 반경안에 Player가 들어올 경우 Player를 추격하고 데미지를 입히도록 구현했다.

![Chase and damage](/assets/img/Darwin's-island/Chase_and_damage.png){:width="564" height="288" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

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