---
title: "Unity Roll a Ball 자습서"
description: "모든 Mobile Engagement Unity의 필수 조건인 고전 Unity Roll a Ball 게임을 만드는 단계를 설명합니다."
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
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="31563-103"><a id="unity-roll-a-ball"></a>Unity Roll a Ball 게임 만들기</span><span class="sxs-lookup"><span data-stu-id="31563-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="31563-104">이 자습서에서는 약간 수정된 [Unity Roll a Ball 자습서](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)의 주요 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="31563-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="31563-105">이 샘플 게임은 앱 사용자에 의해 제어되는 구 모양의 '플레이어' 개체로 구성되며, 플레이어 개체를 수집 가능한 개체와 충돌하여 수집 가능한 개체를 '수집'하는 것이 이 게임의 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="31563-106">이 자습서는 여러분이 Unity 편집기 환경에 대한 기본 지식을 갖춘 것으로 가정하고 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="31563-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="31563-107">문제가 발생하면 전체 자습서를 참조하셔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="31563-108">게임 설정</span><span class="sxs-lookup"><span data-stu-id="31563-108">Setting up the game</span></span>
<span data-ttu-id="31563-109">아래 단계는 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="31563-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="31563-110">**Unity 편집기**를 열고 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="31563-111">**프로젝트 이름** & **위치**를 입력하고, **3D**를 선택한 다음 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="31563-112">방금 위에서 새 프로젝트의 일부로 만든 기본 장면을 **Assets** 폴더의 새로운 **\_Scenes** 폴더 안에 **MiniGame**이라는 이름으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="31563-113">플레이 필드로 **3D 개체 -> 평면**을 만들고 이 평면 개체의 이름을 **Ground**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="31563-114">이 **Ground** 개체가 원점에 위치하도록 변환 구성 요소를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="31563-115">**Ground** 개체의 **Gizmos 메뉴**에서 **눈금 표시**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="31563-116">**Ground** 개체의 **규모** 구성 요소를 [X = 2,Y = 1, Z = 2]로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="31563-117">프로젝트에 새로운 **3D 개체 -> 구**를 추가하고 이 구 개체의 이름을 **Player**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="31563-118">**Player** 개체를 선택하고 평면 개체와 마찬가지로 **변형 다시 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="31563-119">Player Y의 **변형 -> 위치 -> Y 좌표** 구성 요소를 0.5로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="31563-120">프로젝트에서 **Materials** 라는 새 폴더를 만들고 여기서 플레이어에게 색을 입힐 재질을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="31563-121">이 폴더에 **백그라운드**라고 하는 새 **재질**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31563-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="31563-122">재질의 **Albedo** 속성을 업데이트하여 재질 색상을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="31563-123">RGB 값으로 [0,32,64]를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="31563-124">이 재질을 장면 보기로 끌어서 **Ground** 개체에 색상을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="31563-125">마지막으로 선명도를 높이기 위해 [Directional Light] 개체에서 **변형 -> 회전 -> Y**를 60으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="31563-126">플레이어 업데이트</span><span class="sxs-lookup"><span data-stu-id="31563-126">Moving the player</span></span>
<span data-ttu-id="31563-127">아래 단계는 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="31563-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="31563-128">**Player** 개체에 **RigidBody** 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="31563-129">프로젝트에서 **Scripts** 라고 하는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31563-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="31563-130">**구성 요소 추가 -> 새 스크립트 -> C# 스크립트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="31563-131">이름을 **PlayerController**로 지정하고 **만들기 및 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="31563-132">그러면 스크립트가 생성되어 플레이어 개체에 연결될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="31563-133">이 스크립트를 프로젝트의 **Scripts** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="31563-134">스크립트를 편집하기 위해 선호하는 스크립트 편집기에서 스크립트를 열고, 다음 코드를 사용하여 스크립트 코드를 업데이트하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
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
6. <span data-ttu-id="31563-135">위의 스크립트는 **Scripts** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="31563-136">Unity 편집기에서 Scripts 속성을 10으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="31563-137">Unity 편집기에서 **Play** 를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="31563-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="31563-138">이제 키보드를 사용하여 공을 회전하고 주변을 이동하면서 제어할 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="31563-139">카메라 이동</span><span class="sxs-lookup"><span data-stu-id="31563-139">Moving the camera</span></span>
<span data-ttu-id="31563-140">아래 단계는 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141)에서 가져온 것이며 **주 카메라**를 **Player** 개체에 연결할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="31563-141">**Transform.Position**을 X = 0, Y = 10.5, Z=-10으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="31563-142">**Transform.Rotation** 을 X = 45, Y = 0, Z = 0으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="31563-143">**MainCamera**에 **CameraController**라고 하는 새 스크립트를 추가하고 해당 스크립트를 [Scripts] 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="31563-144">편집을 위해 해당 스크립트를 열고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-144">Open up the script for editing and add the following code in it:</span></span>
   
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
5. <span data-ttu-id="31563-145">Unity 환경에서 플레이어 변수를 주 카메라 개체의 플레이어 슬롯으로 끌어다 놓아 서로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="31563-146">이제 Unity 편집기에서 Play를 누르고 플레이어 볼 개체를 회전하면 환경에서 카메라가 플레이어 볼 개체를 따라다니는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="31563-147">플레이 영역 설정</span><span class="sxs-lookup"><span data-stu-id="31563-147">Setting up the Play area</span></span>
<span data-ttu-id="31563-148">아래 단계는 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141)에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="31563-149">플레이어 볼 개체가 이동하다가 플레이 영역에서 떨어지지 않도록 그라운드를 둘러싸는 벽을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="31563-150">**만들기 -> 빈 항목 만들기 -> Game 개체**를 클릭하고 이름을 **벽**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="31563-151">이 벽 개체에서 새 **3D 개체 -> 큐브**를 만들고 이름을 "서쪽 벽"으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="31563-152">이 서쪽 벽 개체의 **변형 -> 위치** 및 **변형 -> 규모**를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="31563-153">서쪽 벽을 복제하고 변환 위치 및 배율을 업데이트하여 **동쪽 벽** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31563-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="31563-154">동쪽 벽을 복제하고 변환 위치 및 배율을 업데이트하여 **북쪽 벽**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31563-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="31563-155">북쪽 벽을 복제하고 변환 위치 및 배율을 업데이트하여 **남쪽 벽**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31563-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="31563-156">수집 가능한 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="31563-156">Creating Collectible objects</span></span>
<span data-ttu-id="31563-157">아래 단계는 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141)에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="31563-158">수집 가능한 개체 집합을 형성하는 멋진 개체를 만들어 보겠습니다. 플레이어 볼 개체는 수집 가능한 개체와 충돌하여 '수집'할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="31563-159">새 **3D 큐브 개체** 를 만들고 이름을 Pickup으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="31563-160">Pickup 개체의 **변형 -> 회전** & **변형 -> 규모**를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="31563-161">**Rotator**라고 하는 **새 C# 스크립트**를 만들어서 Pickup 개체에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="31563-162">이 스크립트를 Scripts 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="31563-163">편집을 위해 이 스크립트를 열고 다음과 같이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="31563-164">이제 Unity 편집기에서 Play를 누르면 Pickup 개체가 축에서 회전할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="31563-165">프로젝트에서 **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="31563-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="31563-166">**Pickup** 개체를 Prefabs 폴더에 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="31563-167">**Pickups**라고 하는 **빈 게임 개체**를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31563-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="31563-168">이 게임 개체의 위치를 원점으로 다시 설정한 다음 Pickup 개체를 이 게임 개체 아래로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="31563-169">**Pickup** 개체를 복제하고 **Transform.Position의 X 및 Z** 값을 적절하게 업데이트하여 **Player** 개체 주변의 **Ground** 개체에 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="31563-170">**Pickup**이라고 하는 **새 재질**을 만들고 Ground 개체를 업데이트했던 것과 비슷한 방법으로 **Albedo 속성**을 빨간색으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="31563-171">Pickup 개체 4개 모두에 재질을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="31563-172">Pickup 개체 수집</span><span class="sxs-lookup"><span data-stu-id="31563-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="31563-173">아래 단계는 [Unity 자습서](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141)에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="31563-174">플레이어가 Pickup 개체와 충돌하는 방법으로 Pickup 개체를 '수집'할 수 있도록 플레이어를 업데이트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="31563-175">편집을 위해 Player 개체에 연결된 **PlayerController** 스크립트를 열고 다음과 같이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
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
2. <span data-ttu-id="31563-176">**Pick Up**이라고 하는 새 **태그**를 만듭니다(스크립트에 있는 것과 일치해야 함).</span><span class="sxs-lookup"><span data-stu-id="31563-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="31563-177">이 **태그** 를 Prefab Pickup 개체에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="31563-178">Prefab 개체의 **IsTrigger** 확인란을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="31563-179">Pickup Prefab 개체에 Rigid 바디를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="31563-180">성능 최적화를 위해 동적 충돌체에 사용된 정적 충돌체를 업데이트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="31563-181">마지막으로 Prefab 개체의 **IsKinematic** 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="31563-182">Unity 편집기에서 **플레이**를 누르면 키보드의 방향 키로 Player 개체를 이동하여 이 **Roll a Ball** 게임을 플레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="31563-183">모바일 플레이가 가능하도록 게임 업데이트</span><span class="sxs-lookup"><span data-stu-id="31563-183">Updating the game for mobile play</span></span>
<span data-ttu-id="31563-184">Unity의 기본 자습서는 위의 섹션에서 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="31563-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="31563-185">이제 모바일 장치에서 쉽게 플레이할 수 있도록 게임을 수정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="31563-186">지금까지는 게임 테스트에서 키보드 입력을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="31563-187">이제 우리 수정 플레이어 즉, 전화의 동작을 사용 하 여 제어할 수 있도록</span><span class="sxs-lookup"><span data-stu-id="31563-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="31563-188">가 속도계 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="31563-189">편집을 위해 **PlayerController** 스크립트를 열고, 가속도계의 동작을 사용하여 Player 개체를 이동하도록 **FixedUpdate** 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31563-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="31563-190">이 자습서는 Unity를 사용하여 기본적인 게임을 만드는 방법을 설명하며, 만든 게임을 원하는 장치에 배포하여 플레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31563-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

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













