---
title: "클래식 포털에서 클라우드 서비스 크기 자동 조정 | Microsoft Docs"
description: "(클래식) 클래식 포털을 사용하여 Azure에서 클라우드 서비스 웹 역할 또는 작업자 역할에 대한 자동 크기 조정 규칙을 구성하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="f46a5-103">클래식 포털에서 클라우드 서비스 크기 자동 조정을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="f46a5-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f46a5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f46a5-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="f46a5-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="f46a5-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="f46a5-106">Azure 클래식 포털의 크기 조정 페이지에서 웹 역할 또는 작업자 역할에 대한 자동 크기 조정 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="f46a5-107">또는 규칙 기반 자동 크기 조정 대신 수동 크기 조정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="f46a5-108">이 문서에서는 클라우드 서비스 웹 및 작업자 역할에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="f46a5-109">가상 컴퓨터(클래식)를 직접 만든 경우 이 가상 컴퓨터는 클라우드 서비스에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="f46a5-110">이 정보 중 일부는 이러한 유형의 가상 컴퓨터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="f46a5-111">가상 컴퓨터 가용성 집합의 크기 조정은 사용자가 구성한 크기 조정 규칙에 따라 설정 및 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="f46a5-112">가상 컴퓨터와 가용성 집합에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f46a5-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="f46a5-113">응용 프로그램의 크기 조정을 구성하기 전에 다음 내용을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="f46a5-114">크기 조정은 코어 사용량의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="f46a5-115">역할 인스턴스가 클수록 더 많은 코어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-115">Larger role instances use more cores.</span></span> <span data-ttu-id="f46a5-116">응용 프로그램의 크기는 구독에 대한 코어 제한 내에서만 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="f46a5-117">예를 들어 구독의 코어 제한이 20이라고 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="f46a5-118">중간 크기의 클라우드 서비스 두 대에서 응용 프로그램을 실행할 경우(총 코어 수 4개), 구독에 있는 다른 클라우드 서비스 배포를 나머지 16코어까지만 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="f46a5-119">크기에 대한 자세한 내용은 [클라우드 서비스 크기](cloud-services-sizes-specs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f46a5-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="f46a5-120">메시지 임계값을 기반으로 응용 프로그램의 크기를 조정하려면 큐를 만든 후 역할에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="f46a5-121">자세한 내용은 [큐 저장소 서비스를 사용하는 방법](../storage/queues/storage-dotnet-how-to-use-queues.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f46a5-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="f46a5-122">클라우드 서비스에 연결되는 리소스의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="f46a5-123">리소스를 연결하는 방법에 대한 자세한 내용은 [방법: 클라우드 서비스에 리소스 연결](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f46a5-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="f46a5-124">응용 프로그램의 가용성을 높이려면 응용 프로그램이 두 개 이상의 역할 인스턴스와 함께 배포되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="f46a5-125">자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f46a5-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="f46a5-126">크기 조정 예약</span><span class="sxs-lookup"><span data-stu-id="f46a5-126">Schedule scaling</span></span>
<span data-ttu-id="f46a5-127">기본적으로 모든 역할은 특정 일정을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="f46a5-128">따라서 변경된 모든 설정은 연중 모든 날짜 및 모든 시간에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="f46a5-129">필요한 경우 다음 모드 중 하나에 대해 수동 또는 자동 크기 조정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="f46a5-130">평일</span><span class="sxs-lookup"><span data-stu-id="f46a5-130">Weekdays</span></span>
* <span data-ttu-id="f46a5-131">주말</span><span class="sxs-lookup"><span data-stu-id="f46a5-131">Weekends</span></span>
* <span data-ttu-id="f46a5-132">주중 야간</span><span class="sxs-lookup"><span data-stu-id="f46a5-132">Week nights</span></span>
* <span data-ttu-id="f46a5-133">주중 오전</span><span class="sxs-lookup"><span data-stu-id="f46a5-133">Week mornings</span></span>
* <span data-ttu-id="f46a5-134">특정 날짜</span><span class="sxs-lookup"><span data-stu-id="f46a5-134">Specific dates</span></span>
* <span data-ttu-id="f46a5-135">특정 날짜 범위</span><span class="sxs-lookup"><span data-stu-id="f46a5-135">Specific date ranges</span></span>

<span data-ttu-id="f46a5-136">이 일정 설정은 [Azure 클래식 포털](https://manage.windowsazure.com/)(</span><span class="sxs-lookup"><span data-stu-id="f46a5-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="f46a5-137">**클라우드 서비스** > **\[클라우드 서비스\]** > **크기** > **\[프로덕션 또는 스테이징\]** 페이지)에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="f46a5-138">변경하려는 각 역할에 대해 **예약 시간 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![일정에 따라 클라우드 서비스 자동 크기 조정][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="f46a5-140">수동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f46a5-140">Manual scale</span></span>
<span data-ttu-id="f46a5-141">**크기 조정** 페이지에서 클라우드 서비스에서 실행 중인 인스턴스의 수를 수동으로 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="f46a5-142">이 설정은 사용자가 만든 각 일정에 대해 구성되거나 일정을 만들지 않은 경우 모든 시간으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="f46a5-143">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f46a5-144">클라우드 서비스가 보이지 않는 경우 **프로덕션**에서 **준비**로 변경하거나 그 반대로 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="f46a5-145">**크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-145">Click **Scale**.</span></span>
3. <span data-ttu-id="f46a5-146">크기 조정 옵션을 변경할 일정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="f46a5-147">정의된 일정이 없는 경우 *예약된 시간 없음*이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="f46a5-148">**메트릭별 크기 조정** 섹션을 찾아서 **없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="f46a5-149">이 설정은 모든 역할의 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="f46a5-150">클라우드 서비스의 각 역할에는 사용할 인스턴스 수를 변경하는 데 사용되는 슬라이더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![클라우드 서비스 역할 크기 수동 조정][manual_scale]
   
    <span data-ttu-id="f46a5-152">더 많은 인스턴스가 필요한 경우 [클라우드 서비스 가상 컴퓨터 크기](cloud-services-sizes-specs.md)를 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="f46a5-153">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-153">Click **Save**.</span></span>  
   <span data-ttu-id="f46a5-154">선택 사항을 기반으로 역할 인스턴스가 추가되거나 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="f46a5-155">![][tip_icon]가 표시될 때마다 여기로 마우스를 이동하면 특정 설정의 기능에 대한 도움말을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="f46a5-156">자동 크기 조정 - CPU</span><span class="sxs-lookup"><span data-stu-id="f46a5-156">Automatic scale - CPU</span></span>
<span data-ttu-id="f46a5-157">이 모드는 평균 CPU 사용률이 지정된 임계값을 초과하거나 임계값 아래로 떨어질 경우 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="f46a5-158">이 경우 역할 인스턴스가 만들어지거나 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="f46a5-159">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f46a5-160">클라우드 서비스가 보이지 않는 경우 **프로덕션**에서 **준비**로 변경하거나 그 반대로 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="f46a5-161">**크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-161">Click **Scale**.</span></span>
3. <span data-ttu-id="f46a5-162">크기 조정 옵션을 변경할 일정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="f46a5-163">정의된 일정이 없는 경우 *예약된 시간 없음*이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="f46a5-164">**메트릭별 크기 조정** 섹션을 찾아서 **CPU**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="f46a5-165">이제 역할 인스턴스의 최소 및 최대 범위, 대상 CPU 사용량(확장 트리거), 확장 및 축소할 인스턴스 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![CPU 로드에 따라 클라우드 서비스 역할 크기 조정][cpu_scale]

> [!TIP]
> <span data-ttu-id="f46a5-167">![][tip_icon]가 표시될 때마다 여기로 마우스를 이동하면 특정 설정의 기능에 대한 도움말을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="f46a5-168">자동 크기 조정 - 큐</span><span class="sxs-lookup"><span data-stu-id="f46a5-168">Automatic scale - Queue</span></span>
<span data-ttu-id="f46a5-169">이 모드는 큐의 메시지 수가 지정된 임계값을 초과하거나 임계값 아래로 떨어질 경우 자동으로 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="f46a5-170">이 경우 역할 인스턴스가 만들어지거나 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="f46a5-171">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f46a5-172">클라우드 서비스가 보이지 않는 경우 **프로덕션**에서 **준비**로 변경하거나 그 반대로 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="f46a5-173">**크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-173">Click **Scale**.</span></span>
3. <span data-ttu-id="f46a5-174">**메트릭별 크기 조정** 섹션을 찾아서 **큐**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="f46a5-175">이제 역할 인스턴스의 최소 및 최대 범위, 각 인스턴스에 대해 처리할 큐 및 큐 메시지 수, 확장 및 축소할 인스턴스 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![메시지 큐에 따라 클라우드 서비스 역할 크기 조정][queue_scale]

> [!TIP]
> <span data-ttu-id="f46a5-177">![][tip_icon]가 표시될 때마다 여기로 마우스를 이동하면 특정 설정의 기능에 대한 도움말을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="f46a5-178">연결된 리소스 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f46a5-178">Scale linked resources</span></span>
<span data-ttu-id="f46a5-179">역할의 크기를 조정할 때 응용 프로그램에 사용 중인 데이터베이스의 크기도 조정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="f46a5-180">데이터베이스를 클라우드 서비스에 연결한 경우 적절한 링크를 클릭하여 해당 리소스에 대한 크기 조정 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="f46a5-181">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f46a5-182">클라우드 서비스가 보이지 않는 경우 **프로덕션**에서 **준비**로 변경하거나 그 반대로 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="f46a5-183">**크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-183">Click **Scale**.</span></span>
3. <span data-ttu-id="f46a5-184">**연결된 리소스** 섹션을 찾아서 **이 데이터베이스에 대한 크기 조정 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f46a5-185">**연결된 리소스** 섹션이 보이지 않는 경우 연결된 리소스가 없는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f46a5-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
