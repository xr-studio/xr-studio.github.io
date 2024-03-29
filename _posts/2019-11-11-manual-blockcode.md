---
title : "XR-Studio 블럭코드 개요"
date : 2019-11-11 14:40:00 +0900
categories: VR AR XR-Studio Blockcode update
---

# 1. XR-Studio 블럭코드 스크립트 
## 1. XR-Studio의 블럭코드 개요 
XR-Studio에서는 블럭코드를 사용하여 가상세계 및 이 세계에 속하는 오브젝트들의 동작과 반응을 쉽게 코딩할 수 있습니다.
이러한 블럭코드는 스크래치나 네이버 엔트리등에서 사용하는 블럭코드와 매우 유사하며 배우기가 매우 쉽습니다. 
다만, XR-Studio가 3차원 공간에서 오브젝트를 정의, 변형(Transformation)을 통해 컨텐츠를 만들기 때문에, 이와 관련한 블럭들은 그 의미는 미리 학습하고 사용하는 것이 편할 것 입니다.
이 온라인 매뉴얼에서는 일반적인 블럭코드의 설명은 제외하고 XR-Studio에서 제공하는 3차원 오브젝트의 조작과, 컨텐츠 실행을 제어하는데 필요한 이벤트 시스템에 대해서만 설명하도록 합니다.

XR-Studio는 자바스크립트(Javascript)를 기본 프로그래밍 언어로 사용하고 있으며, 여러분들이 작성하는 블럭코드도 자바스크립트 언어로 변환되어 실행됩니다. 
(블럭코드가 변환된 자바스크립트 코드는 스크립트 에디터 우측 상단의 '자바스크립트 코드'를 누르면 볼 수 있습니다.)
여러분이 자바스크립트 언어를 사용할 수 있다면 XR-Studio로 할 수 있는 일들이 훨씬 많아집니다. 

XR-Studio 블럭코드 그룹

블럭 |  설명 
---|---
System(시스템) | 3D 그래픽스, VR/AR의 실행명령 블럭<br> XR-Studio를 이용해 컨텐츠를 제작하는데 가장 중요한 블럭들이 여기에 있습니다. 
Logic(논리) | if .. then .. 등 논리식 및 조건문에 해당하는 블럭 
Loops(반복) | for, while 등 반복문에 해당하는 블럭 
Math(수학) | 산술연산식 
Text(텍스트) | 문장(텍스트) 처리 블럭 
Lists(리스트) | 리스트 형식의 데이터 구조를 조작할 수 있는 블럭 
Color(색) | rgb 컬러의 표기 
Public Variable | 클래스의 Public 변수의 관리 블럭 
Private Variable | 클래스의 Private 변수의 관리 블럭 
Event(신호) | 이벤트의 생성 / 이벤트 처리 핸들러 블럭 
Functions(함수) | 함수의 정의 및 매개변수

## 2. 시스템 블럭
프로그램은 하나 이상의 서브프로그램(명령문(Statement)들의 집합)으로 나뉩니다. 이러한 서브프로그램은 함수(Function) 또는 프로시져(Procedure)라고도 불립니다.
모든 서브프로그램은 제각각 이름을 가지고 있으며, 서브프로그램 구성하는 실제 명령문들은 대체로 작성된 순서대로 실행됩니다.

![XR-Studio 블럭코드](https://xr-studio.github.io/resources/2019-11-14/xr-studio-Blockcode-system-01.png)

블럭 이름 | 구분 | 설명 
---|---|---
시작되었을 때 | 시스템 호출 함수 | 프로그램, 컨텐츠가 처음 시작할 때 자동으로 호출되어 한번만 동작합니다. 
매 프레임마다 | 시스템 호출 함수 | 화면을 그리는 매 프레임마다 코드가 호출되어 동작합니다.<br> '프레임간격(초)'는 이전 프레임을 그린 후 현재까지 지연된 시간(초)을 알려줍니다.
충돌이 [시작/종료] 할때 | 시스템 호출 함수 |  오브젝트가 다른 오브젝트와 충돌을 [시작하면] 또는 충돌이 끝나면 호출됩니다. 
마우스 컨트롤 | 시스템 호출 함수 |  마우스를 클릭, 또는 버튼 다운/업, 커서의 이동 등에 대한 처리를 구현합니다. <br>VR HMD 컨트롤러의 트리거에게도 신호가 갈 수 있으니 사용에 주의하시기 바랍니다. 
컨트롤러의 [무엇인가 ]를  [조작]했을 때 | 시스템 호출 함수 |  '무엇'은 VR/AR 장비의 컨트롤러에 장착된 기능버튼 등의 입력 수단입니다. (별도 표2-2 참조) <br> '조작'은 입력수단에 대한 가능한 '조작'입니다. 예를 들면 버튼은 '누를'수 있고, 스틱은 '움직일'수 있습니다. <br> 이 블럭 안의 코드들은 해당 컨트롤러의 입력 수단을 조작할 때 호출되어 실행됩니다. 
컨트롤러의 [무엇]의 상태가 변경되었을 때 | 시스템 호출 함수 |  컨트롤러의 기본 동작 이후의 후속 동작으로 실행됩니다. 
컨트롤러의 Thumbstick을 움직였을 때 | 시스템 호출 함수 |  컨트롤러의 stick을 움직여 가리킨 위치를 x,y좌표로 반환합니다. 
레이캐스트를 [받거나/나갈] 때 | 시스템 호출 함수 |  컨트롤러의 레이(Ray)로 오브젝트를 가르켜 오브젝트가 레이를 받았을 때에 실행되거나, 레이가 오브젝트를 벗어날 때 실행됩니다. 

 
조작가능한 입력수단 | 설명 
---|---
트리거(Trigger) | 컨트롤러에 손가락으로 잡아당겨 누를 수 있는 버튼. <br> 주로 총의 방아쇠 등 컨트롤러의 주기능을 동작시키는 용도로 사용됩니다. 
스틱(Thumb-stick) | 엄지손가락으로 집고 상하좌우 자유롭게 움직일 수 있는 스틱. 
쥐기(Grip) | 주로 컨트롤러의 측면에 있는 버튼으로, 오브젝트를 쥐는 모션에 대응하는 버튼 
a-버튼 | 임의 기능을 배치할 수 있습니다. 
b-버튼 | 임의 기능을 배치할 수 있습니다. 
x-버튼 | 임의 기능을 배치할 수 있습니다. 
y-버튼 | 임의 기능을 배치할 수 있습니다. 
surface | 스틱과 동일한 기능을 터치방식으로 구현한 입력수단 |


시작 블럭에는 어떤 오브젝트와 연결되는지 명확하게 지정하지 않고 있습니다. 
XR-Studio에 의해 제작되는 컨텐츠는 ECS(Entity Component System)에 의해 동작하는데, 하나의 컴포넌트는 여러 엔티티(오브젝트)에 의해 공유되어 사용될 수 있습니다. 
블럭코드나 자바스크립트 코드 블럭도 컴포넌트에 하나로서 어떤 엔티티(오브젝트)에도 적용될 수 있습니다. 
따라서 특정 오브젝트에 대해서만 동작하는 코드를 작성하고 싶다면, 해당 오브젝트에 대해서만 동작하는 코드 블럭을 추가하거나 특정 이벤트를 호출하는 방식으로 구현하는 것이 좋습니다. 
시스템 호출 함수 블럭 중에는 시스템에서 매개변수를 전달하는 블럭이 있습니다. 이들 매개변수는 해당 블럭을 캔버스에 가져다 놓으면 'Functions' 카테고리에 자동으로 나타납니다.

![XR-Studio 블럭코드](https://xr-studio.github.io/resources/2019-11-14/xr-studio-Blockcode-system-02.png)

XR-Studio는 3D 그래픽스 엔진을 사용하여 입체적인 시각효과를 제공하는 컨텐츠를 제공합니다. 
여기에 사용되는 엔진은 Three.js라는 3D 그래픽스 라이브러리와 WebXR 기술에 기반하고 있습니다.
3D 공간에서 위치의 지정에는 x,y,z의 세 좌표값이 필요합니다. 우리는 이를 하나로 묶어 Vector3 또는 3차원 벡터라고 부릅니다.
오브젝트의 위치, 크기, 방향 모두 3차원 공간에서는 3개의 좌표값이 필요합니다.
따라서 XR-Studio에서 다루는 모든 오브젝트들도 기본적으로 위치, 크기, 방향의 세가지 속성을 갖는데, 이들 모두 x,y,z의 세가지 값을 필요로 합니다. 
XR-Studio에서는 이들 x,y,z를 각각 적색(Red), 녹색(Green), 청색(Blue)의 세가지 색상으로 나타내어 쉽게 파악할 수 있도록 돕고 있습니다.
3D 그래픽스 엔진 코드에서는 컴퓨터가 생성하는 3차원의 가상 공간안에 3D 오브젝트를 배치하고, 오브젝트의 기본 형태(위치,크기,방향)을 시간에 따라 변형(Transformation)함으로서 실제와 같은 영상을 구현하도록 해줍니다. 
이들 블럭들 중 어떤 블럭들은 가상현실 또는 증강현실 컨텐츠에서만 의미를 가지고 동작하는 블럭코드도 있으므로 사용에 주의해야 합니다.

블럭 이름 |  구분 | 내용 
---|---|---
오브젝트에 속성 지정 | 실행 블럭 | 오브젝트의 속성 값을 정의합니다. <br> 해당 오브젝트가 가진 모든 컴포넌트들의 속성값을 변경할 수 있습니다. 
오브젝트의 속성 변경 | 실행 블럭 | 오브젝트의 임의의 속성을 주어진 시간에 따라 변화시킵니다. <br> 변화되는 속성과 변화되는 시간을 조정함으로서 애니메이션 효과를 얻을 수 있습니다. 
오브젝트의 속성 값 | 속성 가져오기 | 지정된 오브젝트의 속성 값을 가져옵니다. 
 기다린 후 실행 | 실행 블럭 | 주어진 시간동안 대기한 후 내포하고 있는 코드 블럭을 수행합니다. 
VR환경에서 나갑니다 | 실행 블럭 | 가상현실 모드에 있는 경우, 이 블럭을 사용하면 다시 일반적인 브라우저 환경으로 돌아옵니다. (VR Only)|
매 시간마다 코드를 실행 | 실행 블럭 | 주어진 시간마다 주어진 횟수를 반복합니다.<br> 코드 블럭은 실행 전, 실행 코드, 반복 완료 후 코드의 세 부분으로 구분되어 지정합니다. <br> 실행 전, 실행 후는 각각 반복 시작 전과 후에 한번씩만 불리며, 실행 코드는 주어진 시간동안 반복 호출, 실행됩니다. 
현재 오브젝트를 재생 | 실행 블럭 |  동영상 오브젝트 등의 특정 유형 컨텐츠를 재생합니다. 
현재 오브젝트를 정지 | 실행 블럭 | 위에 의해 재생중이던 오브젝트의 재생을 중지합니다. 
사운드 | 실행 블럭 | 음향을 재생/일시정지/중지 합니다. 
부모 지정 | 실행 블럭 | 오브젝트의 상위, 즉 부모오브젝트를 지정합니다. <br> 일단 지정되고 난 이후, 해당 오브젝트는 부모 오브젝트의 속성에 영향을 받습니다. <br> 예를 들어 (손)에 (총)을 쥔 상태의 경우, (총) 오브젝트의 부모는 (손)으로서 손의 움직임에 따라 총도 움직이게 되는 것 입니다. 
물리엔진 속성 지정 | 실행 블럭 | 오브젝트의 운동에 따른 속도/회전 값(Vector3)를 지정합니다. (물리엔진 블럭) 
컨트롤러 (속도/회전력) | 속성 가져오기 | 좌/우측 컨트롤러의 현재 속성 값을 가져옵니다. <br> 왼손(또는 왼쪽 컨트롤러), 오른손(오른쪽 컨트롤러)에 대해서만 사용이 가능합니다.
속력(이동속도) | 속성 가져오기 | 오브젝트의 지정된 방향으로 이동속도를 가져옵니다. <br> 앞쪽은 오브젝트가 향하고 있는 현재 방향으로 정렬됩니다. <br> 이동속도는 m/s로 표기 됩니다. 
방향 | 속성 값 | 오브젝트가 현재 향하고 있는 방향을 기준으로 앞쪽/뒷쪽 등 상대적인 방향을 의미합니다. 
현재 블럭꾸러미의 실행을 중단 |  실행 블럭 | break 
Vector2 | 속성 | x,y 벡터 
Vector3 | 속성 | x,y,z 벡터 
2차원 좌표 (x,y)로부터 3차원 공간에 hit된 트랜스폼 정보를 구함 | AR 전용 실행 블럭 | 2D 스크린 상의 지정 위치에 해당하는 3D 오브젝트의 위치, 방향, 크기 값을 읽어 옵니다. 
화면의 속성 | 속성 | 브라우저 영역의 속성으로 실제 렌더링이 가능한 캔버스 영역의 속성입니다. 
오브젝트 | 속성 | 블럭코드로 오브젝트 가져오기 

![XR-Studio 블럭코드](https://xr-studio.github.io/resources/2019-11-14/xr-studio-Blockcode-system-03.png)

## 3. 이벤트 
XR-Studio의 코드는 이벤트 주도(Event-driven) 방식의 프로그래밍을 지원합니다.
사용자가 이벤트(Event)를 정의하고, 이 이벤트가 호출될 때 필요한 처리를 수행하는 이벤트 핸들러(Evnet Handler)를 구현합니다.
필요한 적절한 상황에서 이벤트를 발생시키면 시스템에 의해 자동으로 이벤트 핸들러가 호출되는 방식으로 동작합니다. 
이벤트 핸들러는 가급적 간결하게 작성하는 것이 좋습니다. 이벤트가 많아질수록 컴퓨터가 해야 할 일이 많아져 컨텐츠의 동작이 느려지는 등의 부작용이 나타날 수 있기 때문에 사용에 주의해야 합니다. 

![XR-Studio 블럭코드](https://xr-studio.github.io/resources/2019-11-14/xr-studio-blockcode-event.png)

## 4. 함수
반복 사용되는 코드를 따로 만들어 필요할 때 호출하여 사용하는 것이 컴퓨터 언어에서의 함수(function) 입니다. 
수학에서 함수와는 다른 면이 있습니다.
XR-Studio의 블럭코드에서도 함수를 만들어 사용할 수 있습니다. 
함수는 호출하는 쪽에서 부를 수 있는 고유의 이름을 가지고 있고, 함수의 실행을 위해 인자(argument)를 전달할 수 있으며, 실행의 결과를 돌려 받을 수도 있습니다.
인자가 없거나 결과 값이 없는 함수도 있을 수 있습니다. 
함수의 인자가 만드는 함수별로 다양하므로 함수를 만들때 마다 톱니바퀴 모양의 '설정' 버튼을 통해 그때그때 설정하여 사용할 수 있습니다. 

주의) 블럭코드 스크립트에서 사용되는 모든 함수의 매개변수는 이 함수 카테고리 페이지에 나타납니다. 

![XR-Studio 블럭코드](https://xr-studio.github.io/resources/2019-11-14/xr-studio-blockcode-functions.png)
