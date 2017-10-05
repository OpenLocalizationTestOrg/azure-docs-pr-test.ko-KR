---
title: "포털에서 클라우드 서비스의 크기를 자동으로 조정하는 방법 | Microsoft Docs"
description: "포털을 사용하여 Azure에서 클라우드 서비스 웹 역할 또는 작업자 역할에 대한 자동 크기 조정 규칙을 구성하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e9683d4c5779450fd67fa42ab13095c7f201b4cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="828a4-103">포털에서 클라우드 서비스 크기 자동 조정을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="828a4-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="828a4-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="828a4-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="828a4-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="828a4-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="828a4-106">규모 감축 또는 규모 확장 작업을 트리거하는 클라우드 서비스 작업자 역할에 대해 조건을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="828a4-107">역할에 대한 조건은 CPU, 디스크 또는 역할의 네트워크 부하를 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="828a4-108">메시지 큐 또는 구독에 연결된 일부 다른 Azure 리소스의 메트릭을 기준으로 조건을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="828a4-109">이 문서에서는 클라우드 서비스 웹 및 작업자 역할에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="828a4-110">가상 컴퓨터(클래식)를 직접 만든 경우 이 가상 컴퓨터는 클라우드 서비스에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="828a4-111">표준 가상 컴퓨터를 [가용성 집합](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에 연결하여 규모를 조정하고 수동으로 켜거나 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="828a4-112">고려 사항</span><span class="sxs-lookup"><span data-stu-id="828a4-112">Considerations</span></span>
<span data-ttu-id="828a4-113">응용 프로그램의 크기 조정을 구성하기 전에 다음 내용을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="828a4-114">크기 조정은 코어 사용량의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="828a4-115">역할 인스턴스가 클수록 더 많은 코어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-115">Larger role instances use more cores.</span></span> <span data-ttu-id="828a4-116">응용 프로그램의 크기는 구독에 대한 코어 제한 내에서만 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="828a4-117">예를 들어 구독의 코어 제한이 20이라고 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="828a4-118">중간 크기의 클라우드 서비스 두 대에서 응용 프로그램을 실행할 경우(총 코어 수 4개), 구독에 있는 다른 클라우드 서비스 배포를 나머지 16코어까지만 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="828a4-119">크기에 대한 자세한 내용은 [클라우드 서비스 크기](cloud-services-sizes-specs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="828a4-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="828a4-120">큐 메시지 임계값에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="828a4-121">큐 사용 방법에 대한 자세한 내용은 [큐 저장소 서비스를 사용하는 방법](../storage/queues/storage-dotnet-how-to-use-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="828a4-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="828a4-122">구독에 연결된 다른 리소스의 크기도 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="828a4-123">응용 프로그램의 가용성을 높이려면 응용 프로그램이 두 개 이상의 역할 인스턴스와 함께 배포되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="828a4-124">자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="828a4-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="828a4-125">크기 조정 기능이 제공되는 위치</span><span class="sxs-lookup"><span data-stu-id="828a4-125">Where scale is located</span></span>
<span data-ttu-id="828a4-126">클라우드 서비스를 선택하면 클라우드 서비스 블레이드가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-126">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="828a4-127">클라우드 서비스 블레이드의 **역할 및 인스턴스** 타일에서 클라우드 서비스의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-127">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="828a4-128">**중요**: 역할 아래에 있는 역할 인스턴스가 아니라 클라우드 서비스 역할을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-128">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="828a4-129">**크기 조정** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-129">Select the **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="828a4-130">자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="828a4-130">Automatic scale</span></span>
<span data-ttu-id="828a4-131">**수동** 또는 **자동**의 두 가지 모드 중 하나를 사용하여 역할에 대한 크기 조정 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="828a4-132">수동에서는 예상할 수 있는 절대 인스턴스 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-132">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="828a4-133">하지만 자동을 사용하면 크기 조정 방법과 정도를 제어하는 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-133">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="828a4-134">**크기 조정 기준** 옵션을 **일정 및 성능 규칙**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-134">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![프로필 및 규칙을 사용하는 클라우드 서비스 크기 조정 설정](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="828a4-136">기존 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-136">An existing profile.</span></span>
2. <span data-ttu-id="828a4-137">부모 프로필에 대한 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-137">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="828a4-138">다른 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-138">Add another profile.</span></span>

<span data-ttu-id="828a4-139">**프로필 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-139">Select **Add Profile**.</span></span> <span data-ttu-id="828a4-140">프로필은 **항상**, **되풀이**, **고정 날짜** 중에서 크기 조정에 사용할 모드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-140">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="828a4-141">프로필 및 규칙을 구성한 후 맨 위에 있는 **저장** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-141">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="828a4-142">프로필</span><span class="sxs-lookup"><span data-stu-id="828a4-142">Profile</span></span>
<span data-ttu-id="828a4-143">프로필은 크기 조정의 최소 및 최대 인스턴스와 이 크기 조정 범위가 활성화되는 경우를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-143">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="828a4-144">**항상**</span><span class="sxs-lookup"><span data-stu-id="828a4-144">**Always**</span></span>

    <span data-ttu-id="828a4-145">항상은 이 범위의 인스턴스를 항상 사용 가능하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-145">Always keep this range of instances available.</span></span>  

    ![항상 크기를 조정하는 클라우드 서비스](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="828a4-147">**되풀이**</span><span class="sxs-lookup"><span data-stu-id="828a4-147">**Recurrence**</span></span>

    <span data-ttu-id="828a4-148">크기를 조정할 요일 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-148">Choose a set of days of the week to scale.</span></span>

    ![되풀이 일정을 사용하는 클라우드 서비스 크기 조정](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="828a4-150">**고정 날짜**</span><span class="sxs-lookup"><span data-stu-id="828a4-150">**Fixed Date**</span></span>

    <span data-ttu-id="828a4-151">역할 크기를 조정할 고정된 날짜 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-151">A fixed date range to scale the role.</span></span>

    ![고정 날짜를 사용하는 클라우드 서비스 크기 조정](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="828a4-153">프로필을 구성한 후 프로필 블레이드 아래쪽에 있는 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-153">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="828a4-154">규칙</span><span class="sxs-lookup"><span data-stu-id="828a4-154">Rule</span></span>
<span data-ttu-id="828a4-155">규칙이 프로필에 추가되고 크기 조정을 트리거하는 조건을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-155">Rules are added to a profile and represent a condition that triggers the scale.</span></span>

<span data-ttu-id="828a4-156">규칙 트리거는 조건 값을 추가할 수 있는 클라우드 서비스(CPU 사용량, 디스크 작업 또는 네트워크 작업)의 메트릭을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-156">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="828a4-157">또한 메시지 큐 또는 구독에 연결된 일부 다른 Azure 리소스의 메트릭을 기준으로 트리거가 작동되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-157">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="828a4-158">규칙을 구성한 후 규칙 블레이드 아래쪽에 있는 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-158">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="828a4-159">수동 크기 조정으로 돌아가기</span><span class="sxs-lookup"><span data-stu-id="828a4-159">Back to manual scale</span></span>
<span data-ttu-id="828a4-160">[크기 조정 설정](#where-scale-is-located)으로 이동한 후 **크기 조정 기준** 옵션을 **수동으로 입력한 인스턴스 수**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-160">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![프로필 및 규칙을 사용하는 클라우드 서비스 크기 조정 설정](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="828a4-162">이 설정은 역할에서 자동 크기 조정이 제거되고 인스턴스 수를 직접 설정할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-162">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span>

1. <span data-ttu-id="828a4-163">크기 조정(수동 또는 자동) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-163">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="828a4-164">크기 조정할 인스턴스를 설정하기 위한 역할 인스턴스 슬라이더입니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-164">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="828a4-165">크기를 조정할 역할의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-165">Instances of the role to scale to.</span></span>

<span data-ttu-id="828a4-166">크기 조정 설정을 구성한 후 맨 위에 있는 **저장** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="828a4-166">After you have configured the scale settings, select the **Save** icon at the top.</span></span>
