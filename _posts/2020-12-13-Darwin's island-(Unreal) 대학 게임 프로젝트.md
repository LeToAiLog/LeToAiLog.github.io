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

승리 UI가 보이게 되면 Player **<span style="color:red;font-size:100%">(8)</span>**의 움직임을 멈추고 더 이상 조종이 불가능하게 Actor를 파괴했다. **<span style="color:red;font-size:100%">(9)</span>**와 같은 방법으로 Player가 죽었을 시 YOU DIED UI를 활성화하고 Actor의 움직임을 멈춘 후 파괴시킨 다음에 마우스 커서를 활성화하여 Quit Game **<span style="color:red;font-size:100%">(7)</span>**을 클릭할 수 있게 만들었다.

<hr>

#### **Artificial Intelligence**

AI는 중립과 적대적 관계로 나누었다. 중립 개체는 게임 시작시 목표 지점을 반복하여 이동하는 Patrol로 구현했고, 적대 개체는 일정 반경안에 Player가 들어올 경우 Player를 추격하고 데미지를 입히도록 구현했다.

![Chase and damage](/assets/img/Darwin's-island/Chase_and_damage.png){:width="564" height="288" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

Chase the Player **<span style="color:red;font-size:100%">(10)</span>**와 Patrol **<span style="color:red;font-size:100%">(11)</span>**은 Custom Event이다. 적대 개체인 드래곤과 바게스트에서는 ActorBeginOverlap Event **<span style="color:red;font-size:100%">(10)</span>**를 통해 Sphere **<span style="color:red;font-size:100%">(13)</span>**의 **<span style="color:red;font-size:100%">(12)</span>** 영역안에 Player의 캐릭터가 Overlap되면 Player in range boolean 변수를 true로 저장하고 Player를 추격하게 했다. Enemy와 Player 캐릭터의 Overlap **<span style="color:red;font-size:100%">(10)</span>**이 끝나게 되면 Player in range의 값을 false로 저장하고 즉시 Enemy가 Player를 추격하는 것을 멈추게했다. Sphere **<span style="color:red;font-size:100%">(13)</span>**는 Player와 부딪혔을때 Player가 Sphere안에 들어갈 수 있도록 하기 위함과 OverlapEvent를 받기 위해 Collision Presets **<span style="color:red;font-size:100%">(14)</span>**을 OverlapAllDynamic으로 설정해주었다.

![Chase and damage](/assets/img/Darwin's-island/Chase_and_damage_sphere_collision.png){:width="722" height="299" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

**<span style="color:red;font-size:100%">(15)</span>**는 Patrol Event의 구현 부분이다. AI Move To를 이용하여 사슴과 바게스트가 맵에 위치 시켜놓은 TargetPoint **<span style="color:red;font-size:100%">(16)</span>** 위치로 반복해서 움직이게 만들었다. Self **<span style="color:red;font-size:100%">(15)</span>**는 움직이는 대상인 Pawn **<span style="color:red;font-size:100%">(15)</span>**위치에 값을 넣어주고 TargetActor에는 목표 위치의 값인 TargetPoint **<span style="color:red;font-size:100%">(16)</span>**가 들어가게 된다. 첫 번째 목표 위치까지 이동이 성공하게 되면 2초동안 해당 위치에 머물렀다가 다시 다음 TargetPoint **<span style="color:red;font-size:100%">(17)</span>**로 이동하게 되고 정해진 위치가 모두 끝나게 되면 다시 처음으로 돌아가서 반복하게 했다.

AI의 움직임을 제어하기 위해서는 NavMeshBoundsVolume **<span style="color:red;font-size:100%">(18)</span>**으로 AI가 움직이는 공간을 지정해줘야 한다. 따라서 NavMeshBoundsVolume **<span style="color:red;font-size:100%">(19)</span>**으로 맵 전체를 감싸주어 맵 내에 있는 Enemy가 움직일 수 있는 공간을 할당해 주었다.

![Patrol Event](/assets/img/Darwin's-island/Patrol_Event.png){:width="1058" height="410" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

![Nav Mesh](/assets/img/Darwin's-island/NavMesh.png){:width="639" height="270" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

![Chase and damage](/assets/img/Darwin's-island/Chase_and_damage_2.png){:width="1244" height="465" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

**<span style="color:red;font-size:100%">(20)</span>**은 Chase The Player Event의 구현 부분이다. Enemy의 상태를 isDead로 확인하여 True일 때 움직임을 멈추고 죽는 애니메이션을 재생한다. False면 AI Move To로 Target Actor인 Player의 위치로 이동하고 일정 범위 안에 Player가 들어오면 Branch로 Enemy의 공격상태를 확인한다. 공격이 가능하다면 Can Attack의 값을 False로 바꾸고 Montage Play를 이용하여 공격 애니메이션을 실행한다. 만약 불가능하다면 다시 Player를 추격하도록 했다. On Completed는 Montage의 Play가 성공적으로 마쳐지면 실행하고 On Interrupted는 Montage의 Play가 중단되면 실행한다. 이와 같은 Blue Print를 작성한 이유는 Enemy의 공격 모션이 Player가 공격하여 Hit 모션으로 바뀌게되면 석상처럼 굳어 아무것도 안하는 일이 발생하게 되어 이와 같은 처리를 했었다.

Enemy는 Player가 Player In Range의 범위안에 있다면 Attack Rate의 값을 받아 Delay로 지연시킨 후 해당 시간이 지난 후에 Can Attack의 값을 True로 변경한 후 다시 Player를 추격하면서 이러한 행동을 반복한다. Player와 Enemy가 공격하는 모든 방식은 AnimNotifyState **<span style="color:red;font-size:100%">(21)</span>**로 구현했기 때문에 일부 변수를 제외하고는 같은 방식으로 구현되었다. 변하는 일부 변수는 공격 범위, Enemy, Player의 Damage와 Get Socket Location에 있는 In Socket Name으로 Enemy나 Player혹은 공격 모션이 있는 모든 Actor의 Skeleton **<span style="color:red;font-size:100%">(22)</span>**을 이루고 있는 각 관절마다의 이름이 포함된다.

![Box Trace By Profile](/assets/img/Darwin's-island/Box_Trace_By_Profile.png){:width="1244" height="465" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

공격 Montage에서 Skeleton에 있는 관절의 이름을 똑같이 작성해야 Get Socket Location에서 값을 읽어 BoxTraceByProfile **<span style="color:red;font-size:100%">(21)</span>**에 전달한다. BoxTraceByProfile에서는 값을 받아서 모션에 해당하는 유효 공격 범위의 크기를 Half Size로 지정한다. 유효 공격 범위를 보기 위해 Draw Debug Type에서 For Duration **<span style="color:red;font-size:100%">(23)</span>**을 이용하여 공격 영향범위에 대해서 **<span style="color:red;font-size:100%">(23)</span>** 시각화했다. 공격 모션 **<span style="color:red;font-size:100%">(23)</span>**을 따라서 생성되는 빨간 박스에 Player가 닿게 되면 녹색으로 박스의 색깔이 변하게 되어 충돌을 알린다. BoxTraceByProfile에서 Out Hit에 있는 요소들 중에 데미지를 받는 Actor를 받아와야 한다. 데미지를 받는 Actor는 Hit Actor **<span style="color:red;font-size:100%">(24)</span>**의 기능을 사용해야 하므로 배열에 요소들을 받아 저장하고 For Each Loop를 통해 요소들을 Break Hit Result로 사용자가 볼 수 있게 해주었다. Hit Actor를 Apply Damage의 Damaged Actor에 연결하여 데미지를 받는 Actor를 설정해주었고 Base Damage에 Enemy의 공격력을 받아와 해당 Damage가 피해를 받는 Actor에 적용되게 했다.

![Anim Notify](/assets/img/Darwin's-island/Anim_Notify.png){:width="1049" height="200" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

![Anim Notify 2](/assets/img/Darwin's-island/Anim_Notify_2.png){:width="1210" height="422" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

Content Browser에서 우클릭으로 Animation Montage **<span style="color:red;font-size:100%">(26)</span>**를 생성하게 되면 Skeleton **<span style="color:red;font-size:100%">(28)</span>**을 선택하는 창이 나온다. 원하는 Skeleton을 클릭하면 해당 Skeleton Mesh를 가지는 이미지로 Montage **<span style="color:red;font-size:100%">(27)</span>**가 생성된다. 여기에서 AnimNotifyState로 설정해 주었던 데미지값들이 제대로 적용되게 하려면 공격 모션에 해당하는 **<span style="color:red;font-size:100%">(25)</span>** 구간에 AnimNotifyState를 설정해 주어야한다.

구간을 설정하기 전에 생성된 Montage에서 공격 모션 **<span style="color:red;font-size:100%">(29)</span>**을 불러와 등록 **<span style="color:red;font-size:100%">(30)</span>**해 주어야 한다. 이후 Notify **<span style="color:red;font-size:100%">(25)</span>** 구간에서 우클릭으로 **<span style="color:red;font-size:100%">(31)</span>**과 같이 추가하면 **<span style="color:red;font-size:100%">(25)</span>**의 빨간 박스안처럼 등록되어 Damage를 구현할 수 있다.

![Anim Notify 3](/assets/img/Darwin's-island/Attack_Notify_3.png){:width="600" height="800" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

![Event Any Damage](/assets/img/Darwin's-island/Event_Any_Damage.png){:width="1122" height="495" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

Any Damage (32)를 통해 Apply Damage에서 받아온 정보를 Branch에 넣어준다. IsPlaying은 Damage를 받지 않는 상태에서 True이고 받는 상태면 False의 값을 반환한다. Attack Montage와 마찬가지로 등록해 놓은 getHitMontage를 재생하여 맞는 Animation을 재생하고 OnBlendOut을 통해 Montage의 BlendOut이 시작되고 중단되지 않았을 때 Current Health의 값을 받은 Damage만큼 빼서 저장하게 한다. 만약 Current Health가 0과 같거나 작아지면 Player는 죽는 Montage를 재생하고 UI에서 YOU DIED와 연결된 기능들을 활성화시켜 Actor의 조종을 막는다.

<hr>

#### **Animation**

Animation Blueprint는 Animation의 전체적인 로직을 관리한다. 이벤트 그래프 **<span style="color:red;font-size:100%">(2)</span>**에서 Animation이 적용될 Actor를 불러와 Dragon REF에 저장하여 Dragon을 움직이는데 필요한 정보들을 불러온다. Dragon REF는 Animation Blueprint에서 선언한 변수로, 불러올 Actor의 이름을 따와 어떤 Actor의 정보를 불러올지 알기 편하게 해주었다.

![Animation Blueprint](/assets/img/Darwin's-island/Animation_Blueprint.png){:width="600" height="400" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

State Machine **<span style="color:red;font-size:100%">(3)</span>**은 Idle/Run 정보를 담고 있다. Idle/Run은 Add State로 상태를 추가하여 애니메이션이 시작되는 Entry에서 Idle/Run으로 연결하여 활성화시켜 준다. Movement Cache **<span style="color:red;font-size:100%">(3)</span>**를 사용함으로써 기존에 있던 움직임들을 저장하고 불러온다. DefaultSlot을 통해 Montage로 지정해 놓았던 Animation들을 Cache에 저장되어 있는 Animation과 Blend시켜 사용한다. 이 정보들을 최종 애니메이션 포즈에 연결하여 각 상태에 맞는 Animation을 표현해준다.

![State Machine](/assets/img/Darwin's-island/State_Machine.png){:width="600" height="400" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}

Idle/Run에서는 **<span style="color:red;font-size:100%">(2)</span>**에서 저장했던 Dragon의 정보 중 움직임의 정보를 받아 Velocity **<span style="color:red;font-size:100%">(5)</span>**에 연결해주어 Actor의 움직임을 감지한다. 이때 움직임은 Chase the Player에서 Player In Range가 True일 때 활성화되면서 애니메이션이 실행되게 된다. Dragon_Anim의 경우 Blend 1D Space **<span style="color:red;font-size:100%">(5)</span>**를 이용하여 가로축의 변화만을 값으로 받아 가로축의 변화를 speed로 두고 Idle상태와 Run상태를 중간지점에서 Blend하여 부드럽게 애니메이션이 전환될 수 있게 해준다. Blend 1D **<span style="color:red;font-size:100%">(6)</span>**는 Content Browser에서 우클릭으로 생성 가능하다.

![Blend 1D](/assets/img/Darwin's-island/Blend_1D.png){:width="600" height="400" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}
![Blend 1D](/assets/img/Darwin's-island/Blend_1D_2.png){:width="600" height="400" style="border:1px solid #eaeaea; border-radius: 10px; padding: 0px;"}
Dragon_Anim은 Blend 1D Space가 만들어진 상태에서 Animation Blueprint **<span style="color:red;font-size:100%">(7)</span>**에서 Drag and Drop으로 추가가 가능하다. 

녹색 점 **<span style="color:red;font-size:100%">(8)</span>**을 기준으로 왼쪽이 Idle상태, 오른쪽이 Run 상태로 Blend를 시켜준다. 상태에 대한 확인은 녹색점을 드래그로 왼쪽, 오른쪽 움직이면서 확인할 수 있다.

Blend 1D Space의 경우 달리기, 서있는 상태를 표현하는데 쓰이고 Blend 2D Space는 달리기, 서있는 상태, 날기 같은 y와 x축 모두 애니메이션에 변화가 있을 때 사용한다. **<span style="color:red;font-size:100%">(9)</span>**에서 **<span style="color:red;font-size:100%">(8)</span>**로 Drag and Drop으로 상태를 추가할 수 있다.

**<span style="color:red;font-size:100%">(8)</span>**에서 표현되는 Speed에 대한 내용으로 속력이 0에 가까우면 서있는 상태에 가까운 애니메이션이 출력되고 350에 가까우면 점점 빨리 달리는 애니메이션으로 출력된다. Speed는 게임에서 실제로 Actor의 달리는 속도이므로 최대 속도가 높으면 최대 속도에 가까울수록 애니메이션 뿐만 아니라 게임내에서도 빨라진다. 다만 애니메이션의 경우 정해진 최대 애니메이션 빠르기를 넘어서지는 못한다.

<hr>

### **Darwin's island Play Video**
{% include embed/youtube.html id='wDahpiRtLeA' %}