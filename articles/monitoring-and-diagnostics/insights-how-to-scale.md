---
title: "Azure Portal에서 수동 또는 자동 크기 조정으로 인스턴스 수 조정 | Microsoft 문서"
description: "Azure에서 서비스 크기를 조정하는 방법을 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: d171538ea57839eccddcc74ca099a39aee34ea10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a><span data-ttu-id="d5381-103">수동 또는 자동으로 인스턴스 개수 조정</span><span class="sxs-lookup"><span data-stu-id="d5381-103">Scale instance count manually or automatically</span></span>
<span data-ttu-id="d5381-104">[Azure 포털](https://portal.azure.com/)에서 서비스의 인스턴스 개수를 수동으로 설정하거나, 수요에 다라 자동으로 크기가 조정되도록 매개 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-104">In the [Azure Portal](https://portal.azure.com/), you can manually set the instance count of your service, or, you can set parameters to have it automatically scale based on demand.</span></span> <span data-ttu-id="d5381-105">이를 일반적으로 *규모 확장* 또는 *규모 감축*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-105">This is typically referred to as *Scale out* or *Scale in*.</span></span>

<span data-ttu-id="d5381-106">인스턴스 개수에 따라 크기를 조정하기 전에 인스턴스 개수뿐 아니라 **가격 책정 계층** 도 크기 조정에 영향을 준다는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-106">Before scaling based on instance count, you should consider that scaling is affected by **Pricing tier** in addition to instance count.</span></span> <span data-ttu-id="d5381-107">가격 책정 계층마다 다른 코어 및 메모리 수를 가질 수 있으므로 인스턴스 수가 동일할 때 성능이 더 높습니다(*강화* 또는 *규모 축소*).</span><span class="sxs-lookup"><span data-stu-id="d5381-107">Different pricing tiers can have different numbers cores and memory, and so they will have better performance for the same number of instances (which is *Scale up* or *Scale down*).</span></span> <span data-ttu-id="d5381-108">이 문서에서는 특히 *규모 감축* 및 *규모 확장*에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-108">This article specifically covers *Scale in* and *out*.</span></span>

<span data-ttu-id="d5381-109">포털에서 규모를 감축할 수 있으며, [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)를 사용하여 수동 또는 자동으로 크기를 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-109">You can scale in the portal, and you can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to adjust scale manually or automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="d5381-110">이 문서에서 포털([http://portal.azure.com](http://portal.azure.com))에서 자동 크기 조정 설정을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-110">This article describes how to create an autoscale setting in the portal at [http://portal.azure.com](http://portal.azure.com).</span></span> <span data-ttu-id="d5381-111">이 포털에서 만든 자동 크기 조정 설정은 클래식 포털([http://manage.windowsazure.com](http://manage.windowsazure.com))에서 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-111">Autoscale settings created in this portal cannot be edited it the classic portal ([http://manage.windowsazure.com](http://manage.windowsazure.com)).</span></span>
> 
> 

## <a name="scaling-manually"></a><span data-ttu-id="d5381-112">수동으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d5381-112">Scaling manually</span></span>
1. <span data-ttu-id="d5381-113">[Azure Portal](https://portal.azure.com/)에서 **찾아보기**를 클릭한 다음 크기를 조정할 리소스(예: **App Service 계획**)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-113">In the [Azure Portal](https://portal.azure.com/), click **Browse**, then navigate to the resource you want to scale, such as an **App Service plan**.</span></span>
2. <span data-ttu-id="d5381-114">**설정 > 규모 확장(App Service 계획)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-114">Click **Settings > Scale out (App Service plan).**</span></span>
3. <span data-ttu-id="d5381-115">**크기 조정** 블레이드의 맨 위에서 서비스의 자동 크기 조정 작업 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-115">At the top of the **Scale** blade you can see a history of autoscale actions of the service.</span></span>
   
    ![크기 조정 블레이드](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > <span data-ttu-id="d5381-117">자동 크기 조정에 의해 수행되는 작업만 이 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-117">Only actions that are performed by autoscale will show up in this chart.</span></span> <span data-ttu-id="d5381-118">인스턴스 개수를 수동으로 조정하는 경우 이 차트에 변경 내용이 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-118">If you manually adjust the instance count, the change will not be reflected in this chart.</span></span>
   > 
   > 
4. <span data-ttu-id="d5381-119">슬라이더를 사용하여 수동으로 **인스턴스** 수를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-119">You can manually adjust the number **Instances** with slider.</span></span>
5. <span data-ttu-id="d5381-120">**저장** 을 클릭하면 거의 즉시 해당 인스턴스 수로 크기가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-120">Click the **Save** command and you'll be scaled to that number of instances almost immediately.</span></span>

## <a name="scaling-based-on-a-pre-set-metric"></a><span data-ttu-id="d5381-121">미리 설정된 메트릭을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d5381-121">Scaling based on a pre-set metric</span></span>
<span data-ttu-id="d5381-122">메트릭을 기준으로 인스턴스 수를 자동으로 조정하려는 경우 **크기 조정 기준** 드롭다운에서 원하는 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-122">If you want the number of instances to automatically adjust based on a metric, select the metric you want in the **Scale by** dropdown.</span></span> <span data-ttu-id="d5381-123">예를 들어 **App Service 계획**의 경우 **CPU 비율**을 기준으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-123">For example, for an **App Service plan** you can scale by **CPU Percentage**.</span></span>

1. <span data-ttu-id="d5381-124">메트릭을 선택하면 슬라이더 및/또는 크기를 조정할 인스턴스 수의 범위를 입력할 수 있는 텍스트 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-124">When you select a metric you'll get a slider, and/or, text boxes to enter the number of instances you want to scale between:</span></span>
   
    ![CPU 비율이 있는 크기 조정 블레이드](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    <span data-ttu-id="d5381-126">자동 크기 조정은 부하에 관계없이 설정된 경계 아래나 위로 서비스를 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-126">Autoscale will never take your service below or above the boundaries that you set, no matter your load.</span></span>
2. <span data-ttu-id="d5381-127">메트릭의 목표 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-127">Second, you choose the target range for the metric.</span></span> <span data-ttu-id="d5381-128">예를 들어 **CPU 비율**을 선택한 경우 서비스의 모든 인스턴스에 대한 평균 CPU 목표를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-128">For example, if you chose **CPU percentage**, you can set a target for the average CPU across all of the instances in your service.</span></span> <span data-ttu-id="d5381-129">평균 CPU가 정의된 최대값을 초과하면 규모 확장이 발생하고, 평균 CPU가 최소값 아래로 떨어지면 규모 감축이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-129">A scale out will happen when the average CPU exceeds the maximum you define, likewise, a scale in will happen whenever the average CPU drops below the minimum.</span></span>
3. <span data-ttu-id="d5381-130">**저장** 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-130">Click the **Save** command.</span></span> <span data-ttu-id="d5381-131">자동 크기 조정은 몇 분마다 검사하여 메트릭에 대한 인스턴스 범위 및 목표 내에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-131">Autoscale will check every few minutes to make sure that you are in the instance range and target for your metric.</span></span> <span data-ttu-id="d5381-132">서비스가 추가 트래픽을 받으면 아무 작업도 수행하지 않고 더 많은 인스턴스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-132">When your service receives additional traffic,  you will get more instances without doing anything.</span></span>

## <a name="scale-based-on-other-metrics"></a><span data-ttu-id="d5381-133">기타 메트릭을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d5381-133">Scale based on other metrics</span></span>
<span data-ttu-id="d5381-134">**크기 조정 기준** 드롭다운에 표시되는 기본 설정 이외의 메트릭을 기준으로 크기를 조정할 수 있으며, 규모 확장 및 규모 감축 규칙의 복합 집합을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-134">You can scale based on metrics other than the presets that appear in the **Scale by** dropdown, and can even have a complex set of scale out and scale in rules.</span></span>

### <a name="adding-or-changing-a-rule"></a><span data-ttu-id="d5381-135">규칙 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="d5381-135">Adding or changing a rule</span></span>
1. <span data-ttu-id="d5381-136">**크기 조정 기준** 드롭다운에서 **일정 및 성능 규칙**을 선택합니다. ![성능 규칙](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span><span class="sxs-lookup"><span data-stu-id="d5381-136">Choose the **schedule and performance rules** in the **Scale by** dropdown: ![Performance rules](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span></span>
2. <span data-ttu-id="d5381-137">이전에 자동 크기 조정을 사용한 경우 사용된 정확한 규칙의 뷰가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-137">If you previously had autoscale, on you'll see a view of the exact rules that you had.</span></span>
3. <span data-ttu-id="d5381-138">다른 메트릭을 기준으로 크기를 조정하려면 **규칙 추가** 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-138">To scale based on another metric click the **Add Rule** row.</span></span> <span data-ttu-id="d5381-139">기존 행 중 하나를 클릭하여 이전에 사용한 메트릭에서 크기 조정 기준으로 사용하려는 메트릭으로 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-139">You can also click one of the existing rows to change from the metric you previously had to the metric you want to scale by.</span></span>
   <span data-ttu-id="d5381-140">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span><span class="sxs-lookup"><span data-stu-id="d5381-140">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span></span>
4. <span data-ttu-id="d5381-141">이제 크기 조정 기준으로 사용하려는 메트릭을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-141">Now you need to select which metric you want to scale by.</span></span> <span data-ttu-id="d5381-142">메트릭을 선택할 때는 다음 몇 가지 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-142">When choosing a metric there are a couple things to consider:</span></span>
   
   * <span data-ttu-id="d5381-143">메트릭을 가져오는 *리소스* .</span><span class="sxs-lookup"><span data-stu-id="d5381-143">The *resource* the metric comes from.</span></span> <span data-ttu-id="d5381-144">일반적으로 크기를 조정할 리소스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-144">Typically, this will be the same as the resource you are scaling.</span></span> <span data-ttu-id="d5381-145">그러나 저장소 큐의 깊이를 기준으로 크기를 조정하는 경우 리소스는 크기 조정 기준으로 사용하려는 큐에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-145">However, if you want to scale by the depth of a Storage queue, the resource is the queue that you want to scale by.</span></span>
   * <span data-ttu-id="d5381-146">*메트릭 이름* 자체</span><span class="sxs-lookup"><span data-stu-id="d5381-146">The *metric name* itself.</span></span>
   * <span data-ttu-id="d5381-147">메트릭의 *시간 집계* .</span><span class="sxs-lookup"><span data-stu-id="d5381-147">The *time aggregation* of the metric.</span></span> <span data-ttu-id="d5381-148">*기간*동안 데이터가 결합된 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-148">This is how the data is combine over the *duration*.</span></span>
5. <span data-ttu-id="d5381-149">메트릭을 선택한 후 메트릭에 대한 임계값과 연산자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-149">After choosing your metric you choose the threshold for the metric, and the operator.</span></span> <span data-ttu-id="d5381-150">예를 들어 **80%****보다 큼**이라고 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-150">For example, you could say **Greater than** **80%**.</span></span>
6. <span data-ttu-id="d5381-151">그런 다음 수행할 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-151">Then choose the action that you want to take.</span></span> <span data-ttu-id="d5381-152">다음과 같은 몇 가지 유형의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-152">There are a couple different type of actions:</span></span>
   
   * <span data-ttu-id="d5381-153">증가 또는 감소(개수) - **값** 으로 정의한 개수의 인스턴스를 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-153">Increase or decrease by - this will add or remove the **Value** number of instances you define</span></span>
   * <span data-ttu-id="d5381-154">증가 또는 감소(퍼센트) - 퍼센트만큼 인스턴스 개수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-154">Increase or decrease percent - this will change the instance count by a percent.</span></span> <span data-ttu-id="d5381-155">예를 들어 **값** 필드에 25를 입력하고 현재 8개의 인스턴스가 있으면 2개가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-155">For example, you could put 25 in the **Value** field, and if you currently had 8 instances, 2 would be added.</span></span>
   * <span data-ttu-id="d5381-156">다음 개수로 증가 또는 감소 - 인스턴스 개수를 정의한 **값** 으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-156">Increase or decrease to - this will set the instance count to the **Value** you define.</span></span>
7. <span data-ttu-id="d5381-157">끝으로, 정지 기간을 선택할 수 있습니다. 정지 기간은 이전 크기 조정 작업 이후 이 규칙이 다시 크기를 조정하기 위해 대기해야 하는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-157">Finally, you can choose cool down - how long this rule should wait after the previous scale action to scale again.</span></span>
8. <span data-ttu-id="d5381-158">규칙을 구성한 후 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-158">After configuring your rule hit **OK**.</span></span>
9. <span data-ttu-id="d5381-159">원하는 규칙을 모두 구성했으면 **저장** 명령을 눌러야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-159">Once you have configured all of the rules you want, be sure to hit the **Save** command.</span></span>

### <a name="scaling-with-multiple-steps"></a><span data-ttu-id="d5381-160">여러 단계로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d5381-160">Scaling with multiple steps</span></span>
<span data-ttu-id="d5381-161">위의 예제는 상당히 기본적입니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-161">The examples above are pretty basic.</span></span> <span data-ttu-id="d5381-162">그러나 보다 적극적으로 강화(또는 규모 축소)하려는 경우 동일한 메트릭에 대해 여러 개의 크기 조정 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-162">However, if you want to be more agressive about scaling up (or down), you can even add multiple scale rules for the same metric.</span></span> <span data-ttu-id="d5381-163">예를 들어 CPU 비율에 대해 2개의 크기 조정 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-163">For example, you can define two scale rules on CPU percentage:</span></span>

1. <span data-ttu-id="d5381-164">CPU 비율이 60%를 초과하는 경우 1개 인스턴스 규모 확장</span><span class="sxs-lookup"><span data-stu-id="d5381-164">Scale out by 1 instance if CPU percentage is above 60%</span></span>
2. <span data-ttu-id="d5381-165">CPU 비율이 85%를 초과하는 경우 3개 인스턴스 규모 확장</span><span class="sxs-lookup"><span data-stu-id="d5381-165">Scale out by 3 instances if CPU percentage is above 85%</span></span>

![여러 크기 조정 규칙](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

<span data-ttu-id="d5381-167">이 추가 규칙을 사용하면 크기 조정 작업 이전에 로드가 85%를 넘는 경우 1개가 아니라 2개의 추가 인스턴스를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-167">With this additional rule, if your load exceeds 85% before a scale action, you will get two additional instances instead of one.</span></span>

## <a name="scale-based-on-a-schedule"></a><span data-ttu-id="d5381-168">일정을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d5381-168">Scale based on a schedule</span></span>
<span data-ttu-id="d5381-169">기본적으로 크기 조정 규칙을 만드는 경우 항상 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-169">By default, when you create a scale rule it will  always apply.</span></span> <span data-ttu-id="d5381-170">프로필 머리글을 클릭하면 이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-170">You can see that when you click on the profile header:</span></span>

![프로필](./media/insights-how-to-scale/Insights_Profile.png)

<span data-ttu-id="d5381-172">그러나 주말보다 주중이나 낮 시간 동안 더 적극적으로 크기를 조정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-172">However, you may want to have more agressive scaling during the day, or the week, than on the weekend.</span></span> <span data-ttu-id="d5381-173">근무 외 시간에는 서비스를 완전히 종료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-173">You could even shut down your service entirely off working hours.</span></span>

1. <span data-ttu-id="d5381-174">이렇게 하려면 프로필에서 **항상** 대신 **되풀이**를 선택한 다음 프로필을 적용할 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-174">To do this, on the profile you have, select **recurrence** instead of **always,** and choose the times that you want the profile to apply.</span></span>
2. <span data-ttu-id="d5381-175">예를 들어 주중에 적용되는 프로필을 설정하려면 **요일** 드롭다운에서 **토요일** 및 **일요일**을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-175">For example, to have a profile that applies during the week, in the **Days** dropdown uncheck **Saturday** and **Sunday**.</span></span>
3. <span data-ttu-id="d5381-176">낮 시간 동안 적용되는 프로필을 설정하려면 **시작 시간** 을 시작할 시간으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-176">To have a profile that applies during the daytime, set the **Start time** to the time of day that you want to start at.</span></span>
   
    ![기본 되풀이](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. <span data-ttu-id="d5381-178">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-178">Click **OK**.</span></span>
5. <span data-ttu-id="d5381-179">다음에는 다른 시간에 적용할 프로필을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-179">Next, you will need to add the profile that you want to apply at other times.</span></span> <span data-ttu-id="d5381-180">**프로필 추가** 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-180">Click the **Add Profile** row.</span></span>
    <span data-ttu-id="d5381-181">![근무 외 시간](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span><span class="sxs-lookup"><span data-stu-id="d5381-181">![Off Work](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span></span>
6. <span data-ttu-id="d5381-182">두 번째 새 프로필에 이름을 지정합니다. 예를 들어 **근무 외 시간**으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-182">Name your new, second, profile, for example you could call it **Off work**.</span></span>
7. <span data-ttu-id="d5381-183">**되풀이** 를 다시 선택한 다음 이 시간 동안 원하는 인스턴스 개수 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-183">Then select **recurrence** again, and choose the instance count range you want during this time.</span></span>
8. <span data-ttu-id="d5381-184">기본 프로필과 마찬가지로, 이 프로필을 적용할 **요일** 및 **시작 시간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-184">As with the Default profile, choose the **Days** you want this profile to apply to, and the **Start time** during the day.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d5381-185">자동 크기 조정은 선택한 **표준 시간대** 에 대한 일광 절약 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-185">Autoscale will use the Daylight savings rules for whichever **Time zone** you select.</span></span> <span data-ttu-id="d5381-186">그러나 일광 절약 시간제 동안 UTC 오프셋은 일광 절약 UTC 오프셋이 아니라 기본 표준 시간대 오프셋을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-186">However, during Daylight savings time the UTC offset will show the base Time zone offset, not the Daylight savings UTC offset.</span></span>
   > 
   > 
9. <span data-ttu-id="d5381-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-187">Click **OK**.</span></span>
10. <span data-ttu-id="d5381-188">이제 두 번째 프로필 중에 적용할 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-188">Now, you will need to add whatever rules you want to apply during your second profile.</span></span> <span data-ttu-id="d5381-189">**규칙 추가**를 클릭한 다음 기본 프로필과 동일한 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-189">Click **Add Rule**, and then you could construct the same rule you have during the Default profile.</span></span>
    
    ![근무 외 시간에 규칙 추가](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. <span data-ttu-id="d5381-191">규모 확장 및 규모 감축에 대한 규칙을 모두 만들어야 합니다. 그렇지 않으면 프로필 중에 인스턴스 개수가 증가(또는 감소)하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-191">Be sure to create both a rule for scale out and scale in, or else during the profile the instance count will only grow (or decrease).</span></span>
12. <span data-ttu-id="d5381-192">끝으로, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-192">Finally, click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5381-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5381-193">Next steps</span></span>
* <span data-ttu-id="d5381-194">[서비스 메트릭을 모니터링](insights-how-to-customize-monitoring.md) 하여 서비스를 사용 가능하며 응답할 수 있는 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-194">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="d5381-195">[모니터링 및 진단을 사용](insights-how-to-use-diagnostics.md) 하여 서비스의 자세한 고빈도 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-195">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="d5381-196">[경고 알림을 수신](insights-receive-alert-notifications.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-196">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="d5381-197">[응용 프로그램 성능을 모니터링](../application-insights/app-insights-azure-web-apps.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-197">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="d5381-198">[이벤트 및 활동 로그를 보고](insights-debugging-with-events.md) 서비스에서 발생한 모든 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-198">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span></span>
* <span data-ttu-id="d5381-199">[웹 페이지의 가용성 및 응답성을 모니터링](../application-insights/app-insights-monitor-web-app-availability.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5381-199">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

