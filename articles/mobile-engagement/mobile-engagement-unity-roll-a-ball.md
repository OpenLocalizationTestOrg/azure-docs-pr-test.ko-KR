---
title: "aaaUnity 롤 볼 자습서"
description: "단계 toocreate hello 클래식 Unity 롤 모든 Mobile Engagement Unity 자습서에 대 한 필수 인 볼 게임"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="6db5b-103"><a id="unity-roll-a-ball"></a>Unity Roll a Ball 게임 만들기</span><span class="sxs-lookup"><span data-stu-id="6db5b-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="6db5b-104">이 자습서에서는 약간 수정 된에 대 한 hello 주요 단계를 안내 [Unity 롤 볼 자습서](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="6db5b-105">이 샘플 게임은 hello 응용 프로그램 사용자에 의해 제어 되는 '플레이어' 구면 개체 및 hello 게임의 hello 목적은 too'collect' 수집 가능한 이러한 개체와 다른 점을 지정 hello 플레이어 개체에 의해 수집 가능한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="6db5b-106">이 자습서는 여러분이 Unity 편집기 환경에 대한 기본 지식을 갖춘 것으로 가정하고 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="6db5b-107">모든 문제를 실행 하면 toohello 전체 자습서를 참조 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="6db5b-108">Hello 게임 설정</span><span class="sxs-lookup"><span data-stu-id="6db5b-108">Setting up hello game</span></span>
<span data-ttu-id="6db5b-109">다음 hello 단계는 hello에서 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="6db5b-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="6db5b-110">**Unity 편집기**를 열고 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="6db5b-111">**프로젝트 이름** & **위치**를 입력하고, **3D**를 선택한 다음 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="6db5b-112">Hello 이름와 마찬가지로 hello 새 프로젝트의 일부로 방금 만든 hello 기본 장면 저장 **MiniGame** 새  **\_장면** 아래에 폴더 **자산** 폴더:</span><span class="sxs-lookup"><span data-stu-id="6db5b-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="6db5b-113">만들기는 **3D 개체 평면->** hello 재생 필드 및로이 평면 개체의 이름을 **명확 하 게**</span><span class="sxs-lookup"><span data-stu-id="6db5b-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="6db5b-114">이 대 한 hello 변형 구성 요소 리셋 **명확 하 게** 개체 hello 원본 아래에 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="6db5b-115">선택을 취소 **눈금 표시** 에서 **Gizmos 메뉴** hello에 대 한 **명확 하 게** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="6db5b-116">업데이트 hello **배율** hello에 대 한 구성 요소 **명확 하 게** toobe 개체 [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="6db5b-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="6db5b-117">새로 추가 **3D 개체 구->** 이 구 개체로 toohello 프로젝트 및 이름 바꾸기 **플레이어**합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="6db5b-118">선택 hello **플레이어** 개체를 클릭 하 여 **변형 다시 설정** 비슷한 toohello 평면 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="6db5b-119">업데이트 **변환 위치-> Y 좌표를->** 0.5로 플레이어 Y hello에 대 한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="6db5b-120">라는 새 폴더를 만들어 **자료** hello 프로젝트 hello 자재 toocolor hello 플레이어를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="6db5b-121">이 폴더에 **백그라운드**라고 하는 새 **재질**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="6db5b-122">Hello를 업데이트 하 여 hello 재료의 hello 색 업데이트 **Albedo** 의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="6db5b-123">[0,32,64]의 hello RGB 값을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="6db5b-124">이 자료 hello 장면 보기 tooapply 색 toohello 끌어 **명확 하 게** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="6db5b-125">Hello를 마지막으로 업데이트 **변환 회전-> Y->** too60 hello 방향성 광원 개체에 대 한 쉽게 구별할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="6db5b-126">이동 hello 플레이어</span><span class="sxs-lookup"><span data-stu-id="6db5b-126">Moving hello player</span></span>
<span data-ttu-id="6db5b-127">다음 hello 단계는 hello에서 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="6db5b-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="6db5b-128">추가 **RigidBody** 구성 요소 toohello **플레이어** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="6db5b-129">라는 새 폴더를 만들어 **스크립트** hello 프로젝트에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="6db5b-130">**구성 요소 추가 -> 새 스크립트 -> C# 스크립트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="6db5b-131">이름을 **PlayerController**로 지정하고 **만들기 및 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="6db5b-132">만들고 스크립트 toohello 플레이어 개체 연결.</span><span class="sxs-lookup"><span data-stu-id="6db5b-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="6db5b-133">이 스크립트 hello에서 이동 **스크립트** hello 프로젝트의 폴더에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="6db5b-134">즐겨 찾는 스크립트 편집기에서 편집할 hello 스크립트를 열거나, 코드 다음 hello로 hello 스크립트 코드를 업데이트 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="6db5b-135">사용 하 여 위에 hello 스크립트를 사용 하는 참고는 **속도** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="6db5b-136">Hello Unity 편집기에서 hello 속도 속성 too10를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="6db5b-137">적중 **재생** hello Unity 편집기에서에서.</span><span class="sxs-lookup"><span data-stu-id="6db5b-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="6db5b-138">이제 수 toocontrol hello 볼 hello 키보드를 사용 해야 하며 회전 하 고 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="6db5b-139">이동 hello 카메라</span><span class="sxs-lookup"><span data-stu-id="6db5b-139">Moving hello camera</span></span>
<span data-ttu-id="6db5b-140">다음 hello 단계는 hello에서 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) hello를 연결 하는 **Main 카메라** toohello **플레이어** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="6db5b-141">업데이트 hello **Transform.Position** toobe X = 0, Y =-Z = 10 10.5.</span><span class="sxs-lookup"><span data-stu-id="6db5b-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="6db5b-142">업데이트 hello **Transform.Rotation** toobe X = 45, Y, Z, 0 = = 0.</span><span class="sxs-lookup"><span data-stu-id="6db5b-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="6db5b-143">호출 되는 새 스크립트 추가 **CameraController** toohello **MainCamera** hello Scripts 폴더 아래로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="6db5b-144">편집을 위해 hello 스크립트를 열고 hello 코드에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="6db5b-145">-Unity 환경에서 hello 두 대가 서로 연결 되도록 hello 플레이어 변수를 hello Main 카메라 개체에 대 한 hello 플레이어 슬롯으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="6db5b-146">이제 재생 hello Unity 편집기와 회전 hello 플레이어 볼 개체에서 발생 하면 hello 카메라 hello 이동에 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="6db5b-147">Hello 재생 영역 설정</span><span class="sxs-lookup"><span data-stu-id="6db5b-147">Setting up hello Play area</span></span>
<span data-ttu-id="6db5b-148">다음 hello 단계는 hello에서 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141)합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="6db5b-149">Hello 플레이어 볼 개체 하지 않는 자동 전송 hello 재생 영역 이동에 있도록 명확 하 게 hello를 둘러싼 hello 벽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="6db5b-150">**만들기 -> 빈 항목 만들기 -> Game 개체**를 클릭하고 이름을 **벽**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="6db5b-151">이 벽 개체에서 새 **3D 개체 -> 큐브**를 만들고 이름을 "서쪽 벽"으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="6db5b-152">업데이트 hello **변환 위치->** 및 **변환 눈금->** 이 서쪽 벽 개체에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="6db5b-153">Hello 서쪽 벽 toocreate 복제는 **동부 벽** 업데이트 hello로 위치 및 크기 조정 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="6db5b-154">Hello 동부 벽 toocreate 복제는 **북부 벽** 업데이트 hello로 위치 및 크기 조정 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="6db5b-155">Hello 북부 벽을 복제 하 고 만들는 **남부 벽** 업데이트 hello로 위치 및 크기 조정 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="6db5b-156">수집 가능한 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="6db5b-156">Creating Collectible objects</span></span>
<span data-ttu-id="6db5b-157">다음 hello 단계는 hello에서 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141)합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="6db5b-158">몇 가지 매력적인 hello 집합이 있는 hello 플레이어 볼 개체 too'collect 만들어야 하는 수집 가능한 개체를 구성할 수 있는 개체를 찾고 만듭니다 '와 충돌 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="6db5b-159">새 **3D 큐브 개체** 를 만들고 이름을 Pickup으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="6db5b-160">Hello 조정 **변환 회전->** & **변환 눈금->** hello 픽업 개체의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="6db5b-161">만들기 및 연결는 **새 C# 스크립트** 호출 **Rotator** toohello 픽업 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="6db5b-162">Hello Scripts 폴더에서 있는지 tooput hello 스크립트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="6db5b-163">편집을 위해이 스크립트를 열고 다음 toobe hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="6db5b-164">이제 적중된 hello 재생 모드 hello Unity 편집기와 픽업 개체 표시에서 해당 축에 회전 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="6db5b-165">프로젝트에서 **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="6db5b-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="6db5b-166">끌어서 hello **픽업** 개체 hello Prefabs 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="6db5b-167">**Pickups**라고 하는 **빈 게임 개체**를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="6db5b-168">해당 위치 tooorigin 다시 설정 하 여이 게임 개체에서 hello 픽업 개체를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="6db5b-169">중복 된 hello **픽업** 개체 및 hello에 분산 시킬 **명확 하 게** hello 기준 개체 **플레이어** hello를 업데이트 하 여 개체 **Transform.Position의 X 및 Z**  값을 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="6db5b-170">만들기는 **새 자료** 호출 **픽업** hello를 업데이트 하 여 색의 빨강 toobe 업데이트 **Albedo 속성** 비슷한 toowhat म 않았습니다 hello 명확 하 게 업데이트에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="6db5b-171">Hello 자재 tooall 4 hello 픽업 개체를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="6db5b-172">Hello 픽업 개체를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="6db5b-173">다음 hello 단계는 hello에서 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141)합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="6db5b-174">Hello 플레이어 수 too'collect를 업데이트할 것 ' 픽업 개체와 충돌 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="6db5b-175">Hello를 열고 **PlayerController** 편집을 위해 연결 된 toohello 플레이어 개체 하 고 다음 toohello 업데이트:</span><span class="sxs-lookup"><span data-stu-id="6db5b-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="6db5b-176">새 **태그** 호출 **위로 선택** (일치 해야 hello 스크립트에 포함 된 내용)</span><span class="sxs-lookup"><span data-stu-id="6db5b-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="6db5b-177">적용이 **태그** toohello Prefab 픽업 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="6db5b-178">사용 하도록 설정 **IsTrigger** hello Prefab 개체에 대 한 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="6db5b-179">고정 된 관계로 본문 tooPickup Prefab 개체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="6db5b-180">성능 최적화를 위해 hello 정적 collider tooa 동적 collider 사용 했음을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="6db5b-181">마지막으로 hello 확인 **IsKinematic** hello prefab 개체에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="6db5b-182">적중 **재생** hello Unity 편집기에서 됩니다 수 tooplay이 **볼 롤** 이동 하 여 게임 hello 방향 입력에 대 한 키보드 키를 사용 하 여 플레이어 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="6db5b-183">업데이트 hello 플레이용 모바일 게임</span><span class="sxs-lookup"><span data-stu-id="6db5b-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="6db5b-184">Unity에서 기본 자습서 아니거나 hello 위에 hello 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="6db5b-185">이제 수정 됩니다. 여기서 hello 게임 toomake 것 모바일 장치를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="6db5b-186">Note hello 테스트용 지금까지 게임에 대 한 키보드 입력을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="6db5b-187">이제 우리 수정 제어할 수 있도록 hello의 hello 동작을 사용 하 여 hello 플레이어 즉,가 속도계 hello 입력으로 사용 하 여 전화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="6db5b-188">Hello를 열고 **PlayerController** 편집 및 업데이트 hello에 대 한 스크립트 **FixedUpdate** hello 속도계 toomove hello 플레이어 개체에서 메서드 toouse hello 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="6db5b-189">이 자습서는 Unity와 기본 게임 작성 끝나고 선택 tooplay hello 게임의 장치에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6db5b-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













