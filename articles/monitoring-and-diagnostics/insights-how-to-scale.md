---
title: "수동으로 또는 Azure 포털에 자동 크기 조정 인스턴스 수를 aaaScale | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure 서비스입니다."
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
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a><span data-ttu-id="0b0b2-103">수동 또는 자동으로 인스턴스 개수 조정</span><span class="sxs-lookup"><span data-stu-id="0b0b2-103">Scale instance count manually or automatically</span></span>
<span data-ttu-id="0b0b2-104">Hello에 [Azure 포털](https://portal.azure.com/), 서비스의 hello 인스턴스 수를 수동으로 설정할 수 있습니다 또는, toohave 자동으로 크기 조정 요청에 따라 매개 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-104">In hello [Azure Portal](https://portal.azure.com/), you can manually set hello instance count of your service, or, you can set parameters toohave it automatically scale based on demand.</span></span> <span data-ttu-id="0b0b2-105">이 일반적으로 참조 tooas *확장할* 또는 *으로 크기를 조정*합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-105">This is typically referred tooas *Scale out* or *Scale in*.</span></span>

<span data-ttu-id="0b0b2-106">크기 조정 인스턴스 수에 따라, 전에 확장은 영향을 고려해 야 **가격 책정 계층** 더하기 tooinstance 수에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-106">Before scaling based on instance count, you should consider that scaling is affected by **Pricing tier** in addition tooinstance count.</span></span> <span data-ttu-id="0b0b2-107">다른 숫자 코어와 메모리를 가질 수 있습니다 가격대 하 고 hello에 대 한 더 나은 성능을 한 하므로 다른 동일한 인스턴스 수 (변수인 *수직* 또는 *규모 축소*).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-107">Different pricing tiers can have different numbers cores and memory, and so they will have better performance for hello same number of instances (which is *Scale up* or *Scale down*).</span></span> <span data-ttu-id="0b0b2-108">이 문서에서는 특히 *규모 감축* 및 *규모 확장*에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-108">This article specifically covers *Scale in* and *out*.</span></span>

<span data-ttu-id="0b0b2-109">Hello 포털에서 확장할 수 있고 hello를 사용할 수도 있습니다 [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust 수동 또는 자동으로 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-109">You can scale in hello portal, and you can also use hello [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust scale manually or automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="0b0b2-110">이 문서에서는 설명 어떻게 자동 크기 조정 설정 hello 포털에 toocreate [http://portal.azure.com](http://portal.azure.com)합니다. 이 포털에서 만든 자동 크기 조정 설정을 제공할 수 없습니다 hello 클래식 포털 편집할 ([http://manage.windowsazure.com](http://manage.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-110">This article describes how toocreate an autoscale setting in hello portal at [http://portal.azure.com](http://portal.azure.com). Autoscale settings created in this portal cannot be edited it hello classic portal ([http://manage.windowsazure.com](http://manage.windowsazure.com)).</span></span>
> 
> 

## <a name="scaling-manually"></a><span data-ttu-id="0b0b2-111">수동으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0b0b2-111">Scaling manually</span></span>
1. <span data-ttu-id="0b0b2-112">Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **찾아보기**, 다음와 같은 tooscale, 사용 하려는 toohello 리소스 탐색는 **앱 서비스 계획**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-112">In hello [Azure Portal](https://portal.azure.com/), click **Browse**, then navigate toohello resource you want tooscale, such as an **App Service plan**.</span></span>
2. <span data-ttu-id="0b0b2-113">**설정 > 규모 확장(App Service 계획)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-113">Click **Settings > Scale out (App Service plan).**</span></span>
3. <span data-ttu-id="0b0b2-114">Hello의 hello 위쪽 **배율** 블레이드 hello 서비스의 자동 크기 조정 작업의 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-114">At hello top of hello **Scale** blade you can see a history of autoscale actions of hello service.</span></span>
   
    ![크기 조정 블레이드](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > <span data-ttu-id="0b0b2-116">자동 크기 조정에 의해 수행되는 작업만 이 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-116">Only actions that are performed by autoscale will show up in this chart.</span></span> <span data-ttu-id="0b0b2-117">Hello 인스턴스 수를 수동으로 조정 hello 변경이이 차트에 반영 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-117">If you manually adjust hello instance count, hello change will not be reflected in this chart.</span></span>
   > 
   > 
4. <span data-ttu-id="0b0b2-118">Hello 번호를 수동으로 조정할 수 **인스턴스** 슬라이더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-118">You can manually adjust hello number **Instances** with slider.</span></span>
5. <span data-ttu-id="0b0b2-119">Hello 클릭 **저장** 명령과 있습니다 수 거의 즉시 toothat 인스턴스 수를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-119">Click hello **Save** command and you'll be scaled toothat number of instances almost immediately.</span></span>

## <a name="scaling-based-on-a-pre-set-metric"></a><span data-ttu-id="0b0b2-120">미리 설정된 메트릭을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0b0b2-120">Scaling based on a pre-set metric</span></span>
<span data-ttu-id="0b0b2-121">선택 hello에 원하는 메트릭을 hello hello 메트릭에 따라 tooautomatically 조정 인스턴스 수를 원하는 경우 **하 여 확장할** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-121">If you want hello number of instances tooautomatically adjust based on a metric, select hello metric you want in hello **Scale by** dropdown.</span></span> <span data-ttu-id="0b0b2-122">예를 들어 **App Service 계획**의 경우 **CPU 비율**을 기준으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-122">For example, for an **App Service plan** you can scale by **CPU Percentage**.</span></span>

1. <span data-ttu-id="0b0b2-123">메트릭 선택 슬라이더를 얻을 수 및 tooscale 사이의 원하는 텍스트 상자 tooenter hello 인스턴스의 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-123">When you select a metric you'll get a slider, and/or, text boxes tooenter hello number of instances you want tooscale between:</span></span>
   
    ![CPU 비율이 있는 크기 조정 블레이드](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    <span data-ttu-id="0b0b2-125">자동 크기 조정 서비스 또는 부하에 관계 없이 사용자가 설정한 hello 경계를 벗어나는 받아들이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-125">Autoscale will never take your service below or above hello boundaries that you set, no matter your load.</span></span>
2. <span data-ttu-id="0b0b2-126">둘째, hello 메트릭에 대 한 hello 대상 범위를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-126">Second, you choose hello target range for hello metric.</span></span> <span data-ttu-id="0b0b2-127">예를 들어, 선택한 **CPU 비율**, 대상을 설정할 수 있습니다는 hello 평균 CPU에 대 한 hello 인스턴스의 모든 서비스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-127">For example, if you chose **CPU percentage**, you can set a target for hello average CPU across all of hello instances in your service.</span></span> <span data-ttu-id="0b0b2-128">규모 확장 동작이 발생 하는지에 정의한 hello 최대값을 초과 하는 hello 평균 CPU, hello 평균 CPU가 최소 hello 이하가 될 때마다 눈금의 마찬가지로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-128">A scale out will happen when hello average CPU exceeds hello maximum you define, likewise, a scale in will happen whenever hello average CPU drops below hello minimum.</span></span>
3. <span data-ttu-id="0b0b2-129">Hello 클릭 **저장** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-129">Click hello **Save** command.</span></span> <span data-ttu-id="0b0b2-130">자동 크기 조정에 메트릭에 대 한 hello 인스턴스 범위 및 대상에는 모든 몇 분 toomake를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-130">Autoscale will check every few minutes toomake sure that you are in hello instance range and target for your metric.</span></span> <span data-ttu-id="0b0b2-131">서비스가 추가 트래픽을 받으면 아무 작업도 수행하지 않고 더 많은 인스턴스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-131">When your service receives additional traffic,  you will get more instances without doing anything.</span></span>

## <a name="scale-based-on-other-metrics"></a><span data-ttu-id="0b0b2-132">기타 메트릭을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0b0b2-132">Scale based on other metrics</span></span>
<span data-ttu-id="0b0b2-133">이외의 hello에 나타나는 hello 사전 설정에 따라 메트릭 확장할 수 있습니다 **하 여 확장할** 드롭다운을 수도 규모 확장의 복잡 한 집합 및 규칙으로 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-133">You can scale based on metrics other than hello presets that appear in hello **Scale by** dropdown, and can even have a complex set of scale out and scale in rules.</span></span>

### <a name="adding-or-changing-a-rule"></a><span data-ttu-id="0b0b2-134">규칙 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="0b0b2-134">Adding or changing a rule</span></span>
1. <span data-ttu-id="0b0b2-135">Hello 선택 **일정 및 성능 규칙이** hello에 **하 여 확장할** 드롭다운: ![성능 규칙](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span><span class="sxs-lookup"><span data-stu-id="0b0b2-135">Choose hello **schedule and performance rules** in hello **Scale by** dropdown: ![Performance rules](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span></span>
2. <span data-ttu-id="0b0b2-136">자동 크기 조정을 이전에 설치한 경우에 사용 된 hello 정확한 규칙의 보기를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-136">If you previously had autoscale, on you'll see a view of hello exact rules that you had.</span></span>
3. <span data-ttu-id="0b0b2-137">다른 메트릭 클릭 hello에 따라 tooscale **규칙 추가** 행입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-137">tooscale based on another metric click hello **Add Rule** row.</span></span> <span data-ttu-id="0b0b2-138">클릭할 수도 있습니다 hello 메트릭에서 기존 행 toochange hello의 이전에 사용 했던 여 tooscale toohello 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-138">You can also click one of hello existing rows toochange from hello metric you previously had toohello metric you want tooscale by.</span></span>
   <span data-ttu-id="0b0b2-139">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span><span class="sxs-lookup"><span data-stu-id="0b0b2-139">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span></span>
4. <span data-ttu-id="0b0b2-140">이제 tooscale 하 여 원하는 메트릭이 tooselect을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-140">Now you need tooselect which metric you want tooscale by.</span></span> <span data-ttu-id="0b0b2-141">선택 된 메트릭이 있는 경우 몇 가지 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-141">When choosing a metric there are a couple things tooconsider:</span></span>
   
   * <span data-ttu-id="0b0b2-142">hello *리소스* 에서 hello 메트릭을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-142">hello *resource* hello metric comes from.</span></span> <span data-ttu-id="0b0b2-143">일반적으로이 될 hello hello 리소스 조정할 수와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-143">Typically, this will be hello same as hello resource you are scaling.</span></span> <span data-ttu-id="0b0b2-144">그러나 tooscale hello 큐 깊이를 저장 하 여 원하는 hello 리소스는 hello 큐 tooscale 하 여 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-144">However, if you want tooscale by hello depth of a Storage queue, hello resource is hello queue that you want tooscale by.</span></span>
   * <span data-ttu-id="0b0b2-145">hello *메트릭 이름을* 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-145">hello *metric name* itself.</span></span>
   * <span data-ttu-id="0b0b2-146">hello *집계 시간* hello 메트릭.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-146">hello *time aggregation* of hello metric.</span></span> <span data-ttu-id="0b0b2-147">이 컬렉션은 hello를 통해 hello 데이터 결합 되어 감사가 만들어집니다는 어떻게 *기간*합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-147">This is how hello data is combine over hello *duration*.</span></span>
5. <span data-ttu-id="0b0b2-148">프로그램 메트릭을 선택한 후 hello 메트릭 및 hello 연산자에 대 한 hello 임계값을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-148">After choosing your metric you choose hello threshold for hello metric, and hello operator.</span></span> <span data-ttu-id="0b0b2-149">예를 들어 **80%****보다 큼**이라고 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-149">For example, you could say **Greater than** **80%**.</span></span>
6. <span data-ttu-id="0b0b2-150">Hello 동작 선택 tootake 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-150">Then choose hello action that you want tootake.</span></span> <span data-ttu-id="0b0b2-151">다음과 같은 몇 가지 유형의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-151">There are a couple different type of actions:</span></span>
   
   * <span data-ttu-id="0b0b2-152">증가 또는 감소-이 추가 하거나 hello 제거 **값** 정의한 인스턴스 수</span><span class="sxs-lookup"><span data-stu-id="0b0b2-152">Increase or decrease by - this will add or remove hello **Value** number of instances you define</span></span>
   * <span data-ttu-id="0b0b2-153">퍼센트 늘리거나-hello 인스턴스 수는 % 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-153">Increase or decrease percent - this will change hello instance count by a percent.</span></span> <span data-ttu-id="0b0b2-154">예를 들어 hello에서 25를 배치할 수 있습니다 **값** 필드 및 현재 인스턴스 8을 설치한 경우 2는 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-154">For example, you could put 25 in hello **Value** field, and if you currently had 8 instances, 2 would be added.</span></span>
   * <span data-ttu-id="0b0b2-155">-인스턴스 수가 toohello hello 설정 합니다 너무 늘리거나 **값** 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-155">Increase or decrease too- this will set hello instance count toohello **Value** you define.</span></span>
7. <span data-ttu-id="0b0b2-156">마지막으로, 쿨 다운-hello 이전 크기 조정 작업 tooscale 다시 후이 규칙은 대기 시간을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-156">Finally, you can choose cool down - how long this rule should wait after hello previous scale action tooscale again.</span></span>
8. <span data-ttu-id="0b0b2-157">규칙을 구성한 후 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-157">After configuring your rule hit **OK**.</span></span>
9. <span data-ttu-id="0b0b2-158">원하는 hello 규칙을 모두 구성 되 면 수 있는지 toohit hello **저장** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-158">Once you have configured all of hello rules you want, be sure toohit hello **Save** command.</span></span>

### <a name="scaling-with-multiple-steps"></a><span data-ttu-id="0b0b2-159">여러 단계로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0b0b2-159">Scaling with multiple steps</span></span>
<span data-ttu-id="0b0b2-160">위의 hello 예제는 매우 기본적인입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-160">hello examples above are pretty basic.</span></span> <span data-ttu-id="0b0b2-161">그러나 toobe를 지정 하려면 확장 (또는 축소) 하는 방법에 대 한 보다 적극적으로 추가할 수도 있습니다 hello에 대 한 여러 확장 규칙 동일한 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-161">However, if you want toobe more agressive about scaling up (or down), you can even add multiple scale rules for hello same metric.</span></span> <span data-ttu-id="0b0b2-162">예를 들어 CPU 비율에 대해 2개의 크기 조정 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-162">For example, you can define two scale rules on CPU percentage:</span></span>

1. <span data-ttu-id="0b0b2-163">CPU 비율이 60%를 초과하는 경우 1개 인스턴스 규모 확장</span><span class="sxs-lookup"><span data-stu-id="0b0b2-163">Scale out by 1 instance if CPU percentage is above 60%</span></span>
2. <span data-ttu-id="0b0b2-164">CPU 비율이 85%를 초과하는 경우 3개 인스턴스 규모 확장</span><span class="sxs-lookup"><span data-stu-id="0b0b2-164">Scale out by 3 instances if CPU percentage is above 85%</span></span>

![여러 크기 조정 규칙](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

<span data-ttu-id="0b0b2-166">이 추가 규칙을 사용하면 크기 조정 작업 이전에 로드가 85%를 넘는 경우 1개가 아니라 2개의 추가 인스턴스를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-166">With this additional rule, if your load exceeds 85% before a scale action, you will get two additional instances instead of one.</span></span>

## <a name="scale-based-on-a-schedule"></a><span data-ttu-id="0b0b2-167">일정을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0b0b2-167">Scale based on a schedule</span></span>
<span data-ttu-id="0b0b2-168">기본적으로 크기 조정 규칙을 만드는 경우 항상 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-168">By default, when you create a scale rule it will  always apply.</span></span> <span data-ttu-id="0b0b2-169">Hello 프로필 머리글을 클릭할 때를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-169">You can see that when you click on hello profile header:</span></span>

![프로필](./media/insights-how-to-scale/Insights_Profile.png)

<span data-ttu-id="0b0b2-171">그러나 좋습니다 toohave hello 주말에 보다 hello 하루 또는 hello 일주일 동안 간격 보다 적극적으로.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-171">However, you may want toohave more agressive scaling during hello day, or hello week, than on hello weekend.</span></span> <span data-ttu-id="0b0b2-172">근무 외 시간에는 서비스를 완전히 종료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-172">You could even shut down your service entirely off working hours.</span></span>

1. <span data-ttu-id="0b0b2-173">toodo이 있으면 hello 프로필 선택 **되풀이** 대신 **항상** hello hello 프로필 tooapply 되도록 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-173">toodo this, on hello profile you have, select **recurrence** instead of **always,** and choose hello times that you want hello profile tooapply.</span></span>
2. <span data-ttu-id="0b0b2-174">예를 들어 toohave hello 주 hello에 적용 되는 프로필 **일** 드롭다운의 선택을 취소 **토요일** 및 **일요일**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-174">For example, toohave a profile that applies during hello week, in hello **Days** dropdown uncheck **Saturday** and **Sunday**.</span></span>
3. <span data-ttu-id="0b0b2-175">toohave hello 주간, set hello 하는 동안 적용 되는 프로필 **시작 시간** toostart에서 원하는 toohello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-175">toohave a profile that applies during hello daytime, set hello **Start time** toohello time of day that you want toostart at.</span></span>
   
    ![기본 되풀이](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. <span data-ttu-id="0b0b2-177">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-177">Click **OK**.</span></span>
5. <span data-ttu-id="0b0b2-178">다음으로, 다른 시간에 tooapply 되도록 tooadd hello 프로필이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-178">Next, you will need tooadd hello profile that you want tooapply at other times.</span></span> <span data-ttu-id="0b0b2-179">Hello 클릭 **프로필 추가** 행입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-179">Click hello **Add Profile** row.</span></span>
    <span data-ttu-id="0b0b2-180">![근무 외 시간](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span><span class="sxs-lookup"><span data-stu-id="0b0b2-180">![Off Work](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span></span>
6. <span data-ttu-id="0b0b2-181">두 번째 새 프로필에 이름을 지정합니다. 예를 들어 **근무 외 시간**으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-181">Name your new, second, profile, for example you could call it **Off work**.</span></span>
7. <span data-ttu-id="0b0b2-182">다음 선택 **되풀이** 다시이 시간 동안 원하는 hello 인스턴스 수 범위를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-182">Then select **recurrence** again, and choose hello instance count range you want during this time.</span></span>
8. <span data-ttu-id="0b0b2-183">기본 프로필 hello로 선택 하는 hello **일** 있으며 hello 프로필 tooapply이 원하는 **시작 시간** hello 하루 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-183">As with hello Default profile, choose hello **Days** you want this profile tooapply to, and hello **Start time** during hello day.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b0b2-184">자동 크기 조정 hello 일광 절약 규칙을 사용 하 여 작은 값에 대 한 **시간대** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-184">Autoscale will use hello Daylight savings rules for whichever **Time zone** you select.</span></span> <span data-ttu-id="0b0b2-185">그러나 일광 절약 시간 hello UTC 오프셋은 hello 기본 표준 시간대 오프셋이 없습니다 hello 일광 절약 UTC 오프셋을 표시 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-185">However, during Daylight savings time hello UTC offset will show hello base Time zone offset, not hello Daylight savings UTC offset.</span></span>
   > 
   > 
9. <span data-ttu-id="0b0b2-186">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-186">Click **OK**.</span></span>
10. <span data-ttu-id="0b0b2-187">이제 해야 tooadd 있습니다 규칙 무엇이 든 tooapply 두 번째 프로필 시 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-187">Now, you will need tooadd whatever rules you want tooapply during your second profile.</span></span> <span data-ttu-id="0b0b2-188">클릭 **규칙 추가**, 및 hello hello 기본 프로필 실행 되 고 있어야 동일한 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-188">Click **Add Rule**, and then you could construct hello same rule you have during hello Default profile.</span></span>
    
    ![규칙 toooff 작업 추가](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. <span data-ttu-id="0b0b2-190">있는지 toocreate 수평 확장 및 눈금에 대 한 규칙 수를 hello 하는 동안 또는 else 프로필 hello 인스턴스 수만 증가 (하거나 감소 합니다).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-190">Be sure toocreate both a rule for scale out and scale in, or else during hello profile hello instance count will only grow (or decrease).</span></span>
12. <span data-ttu-id="0b0b2-191">끝으로, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-191">Finally, click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b0b2-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b0b2-192">Next steps</span></span>
* <span data-ttu-id="0b0b2-193">[서비스 메트릭스를 모니터링](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-193">[Monitor service metrics](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="0b0b2-194">[모니터링을 활성화 및 진단](insights-how-to-use-diagnostics.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-194">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="0b0b2-195">작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-195">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="0b0b2-196">[응용 프로그램 성능 모니터링](../application-insights/app-insights-azure-web-apps.md) toounderstand 하려면 정확 하 게 코드 작업 수행 방식을 hello 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-196">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want toounderstand exactly how your code is performing in hello cloud.</span></span>
* <span data-ttu-id="0b0b2-197">[이벤트 및 활동 로그 보기](insights-debugging-with-events.md) toolearn 모든 서비스에 발생 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-197">[View events and activity log](insights-debugging-with-events.md) toolearn everything that has happened in your service.</span></span>
* <span data-ttu-id="0b0b2-198">[웹 페이지의 가용성 및 응답성을 모니터링](../application-insights/app-insights-monitor-web-app-availability.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-198">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

