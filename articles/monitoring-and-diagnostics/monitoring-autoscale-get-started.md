---
title: "Azure에서 자동 크기 조정이 시작 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure의 리소스입니다."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="242de-103">Azure에서 자동 크기 조정 시작</span><span class="sxs-lookup"><span data-stu-id="242de-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="242de-104">이 문서에서는 설명 어떻게 tooset hello Microsoft Azure 포털에서 리소스에 대 한 자동 크기 조정 설정 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="242de-105">Azure 모니터의 자동 크기 조정 toovirtual 컴퓨터 크기 집합, 클라우드 서비스, Azure 앱 서비스 계획 및 앱 서비스 환경에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="242de-106">구독에서 hello 자동 크기 조정 설정을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="242de-107">자동 크기 조정 Azure 모니터에 적용 되는 모든 hello 리소스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="242de-108">단계별 연습에 대 한 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="242de-109">열기 hello [Azure 포털입니다.][1]</span><span class="sxs-lookup"><span data-stu-id="242de-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="242de-110">Hello 왼쪽된 창의 hello Azure 모니터 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="242de-111">![Azure Monitor 열기][2]</span><span class="sxs-lookup"><span data-stu-id="242de-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="242de-112">클릭 **자동 크기 조정** tooview 모든 hello 리소스는 자동 크기 조정에 대 한 현재 자동 크기 조정 상태와 함께 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="242de-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="242de-113">![Azure Monitor에서 자동 크기 조정 검색][3]</span><span class="sxs-lookup"><span data-stu-id="242de-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="242de-114">특정 리소스 그룹, 특정 리소스 종류 또는 특정 리소스의 hello 목록 tooselect 리소스 아래로 상위 tooscope hello에 hello 필터 창을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="242de-115">각 리소스에 대 한 hello 현재 인스턴스 수 및 hello 자동 크기 조정 상태를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="242de-116">자동 크기 조정 상태 hello 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="242de-117">**구성되지 않음**: 이 리소스에 대해 자동 크기 조정 설정을 아직 사용하도록 설정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="242de-118">**사용**: 이 리소스에 대해 자동 크기 조정 설정을 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="242de-119">**사용 안 함**: 이 리소스에 대해 자동 크기 조정 설정을 사용하지 않도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="242de-120">첫 번째 자동 크기 조정 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="242de-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="242de-121">보겠습니다 진행 간단한 단계별 연습 toocreate 첫 번째 자동 크기 조정 설정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="242de-122">열기 hello **자동 크기 조정** 블레이드에서 Azure 모니터를 tooscale 원하는 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="242de-123">(hello 다음 단계 사용 하 여 웹 앱에 연결 된 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="242de-124">[Azure에서 5분 내에 첫 번째 ASP.NET 웹앱을 만들 수 있습니다.][4]</span><span class="sxs-lookup"><span data-stu-id="242de-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="242de-125">참고 hello 현재 인스턴스 수는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="242de-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="242de-126">**자동 크기 조정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="242de-127">![새 웹앱에 대한 크기 조정 설정][5]</span><span class="sxs-lookup"><span data-stu-id="242de-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="242de-128">Hello 크기 조정 설정에 대 한 이름을 입력 한 다음 **규칙 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="242de-129">Hello 오른쪽의 컨텍스트 창으로 열려면 hello 크기 조정 규칙 옵션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="242de-130">기본적으로이 hello 옵션 tooscale 인스턴스 수가 1 hello CPU 비율 hello 리소스의 70%를 초과 하는 경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="242de-131">규칙을 기본값으로 유지하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="242de-132">![웹앱에 대한 크기 조정 설정 만들기][6]</span><span class="sxs-lookup"><span data-stu-id="242de-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="242de-133">이제 첫 번째 크기 조정 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-133">You've now created your first scale rule.</span></span> <span data-ttu-id="242de-134">UX 최선의 방법 및 없다는 것을 권장 하는 hello 참고 "toohave 것이 좋습니다 규칙에서 눈금이 최소 하나 이상 있습니다."</span><span class="sxs-lookup"><span data-stu-id="242de-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="242de-135">toodo 하므로:</span><span class="sxs-lookup"><span data-stu-id="242de-135">toodo so:</span></span>
  
    <span data-ttu-id="242de-136">a.</span><span class="sxs-lookup"><span data-stu-id="242de-136">a.</span></span> <span data-ttu-id="242de-137">**규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="242de-138">b.</span><span class="sxs-lookup"><span data-stu-id="242de-138">b.</span></span> <span data-ttu-id="242de-139">설정 **연산자** 너무**미만**합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="242de-140">c.</span><span class="sxs-lookup"><span data-stu-id="242de-140">c.</span></span> <span data-ttu-id="242de-141">설정 **임계값** 너무**20**합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="242de-142">d.</span><span class="sxs-lookup"><span data-stu-id="242de-142">d.</span></span> <span data-ttu-id="242de-143">설정 **작업** 너무**수를 줄이려면**합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="242de-144">이제 CPU 사용량을 기준으로 확장/축소하는 크기 조정 설정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="242de-145">![CPU 기준 크기 조정][8]</span><span class="sxs-lookup"><span data-stu-id="242de-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="242de-146">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-146">Click **Save**.</span></span>

<span data-ttu-id="242de-147">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-147">Congratulations!</span></span> <span data-ttu-id="242de-148">이제 웹 응용 프로그램 CPU 사용량에 따라 첫 번째 눈금 설정을 tooautoscale 프로그램 성공적으로 만드는 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="242de-149">hello 동일한 단계는 적용 가능한 tooget 시작 가상 컴퓨터 크기 집합 또는 클라우드 서비스 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="242de-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="242de-150">기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="242de-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="242de-151">일정을 기준으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="242de-151">Scale based on a schedule</span></span>
<span data-ttu-id="242de-152">또한 CPU에 따라 tooscale를 설정할 수 있습니다 눈금 다르게 hello 주 중 특정 일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="242de-153">**크기 조정 조건 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="242de-154">Hello 크기 조정 모드와 hello 규칙 설정는 hello 동일 hello 기본 조건으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="242de-155">선택 **특정 날짜를 반복** hello 일정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="242de-156">Hello 일과 hello 크기 조정 상태를 적용 해야 하는 경우에 대 한 hello 시작/종료 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![일정 기준 크기 조정 조건][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="242de-158">특정 날짜에 대해 다르게 크기 조정</span><span class="sxs-lookup"><span data-stu-id="242de-158">Scale differently on specific dates</span></span>
<span data-ttu-id="242de-159">또한 CPU에 따라 tooscale를 설정할 수 있습니다 눈금 다르게 특정 날짜에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="242de-160">**크기 조정 조건 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="242de-161">Hello 크기 조정 모드와 hello 규칙 설정는 hello 동일 hello 기본 조건으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="242de-162">선택 **시작/종료 날짜 지정** hello 일정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="242de-163">Hello 시작/종료 날짜와 hello 크기 조정 상태를 적용 해야 하는 경우에 대 한 hello 시작/종료 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![날짜 크기 조정 조건][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="242de-165">리소스의 hello 눈금 기록 보기</span><span class="sxs-lookup"><span data-stu-id="242de-165">View hello scale history of your resource</span></span>
<span data-ttu-id="242de-166">리소스 확장 또는 축소할, 때마다 hello 활동 로그에 이벤트가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="242de-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="242de-167">Toohello 전환 하 여 hello에 대 한 리소스의 크기 조정 기록을 hello 지난 24 시간을 볼 수 있습니다 **실행 기록이** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![실행 기록][11]

<span data-ttu-id="242de-169">Tooview hello 전체 눈금 기록 하려는 경우 (에 대 한 일 수까지)을 선택 **여기를 클릭 toosee 자세한 내용을 보려면**합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="242de-170">리소스와 범주를 위해 미리 선택 된 자동 크기 조정이 hello 활동 로그가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="242de-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="242de-171">리소스의 hello 눈금 정의 보기</span><span class="sxs-lookup"><span data-stu-id="242de-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="242de-172">자동 크기 조정은 Azure Resource Manager의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="242de-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="242de-173">Toohello 전환 하 여 JSON에서 hello 눈금 정의 볼 수 **JSON** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![크기 조정 정의][12]

<span data-ttu-id="242de-175">필요한 경우 JSON에서 직접 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="242de-176">이러한 변경 내용은 저장하고 나면 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="242de-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="242de-177">자동 크기 조정을 사용하지 않도록 설정하고 인스턴스 크기를 수동으로 조정</span><span class="sxs-lookup"><span data-stu-id="242de-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="242de-178">있을 시간 원하는 toodisable 현재 크기 조정 설정 하 고 리소스를 수동으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="242de-179">Hello 클릭 **자동 크기 조정 사용 안 함** hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="242de-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="242de-180">![자동 크기 조정 사용 안 함][13]</span><span class="sxs-lookup"><span data-stu-id="242de-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="242de-181">이 옵션은 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-181">This option disables your configuration.</span></span> <span data-ttu-id="242de-182">그러나 돌아갈 수 있습니다 tooit 다시 자동 크기 조정을 사용 하도록 설정한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="242de-183">이제 hello tooscale toomanually 되도록 하는 인스턴스 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242de-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![수동 크기 조정 설정][14]

<span data-ttu-id="242de-185">클릭 하 여 tooAutoscale를 항상 반환할 수 있습니다 **조정을 사용할** 차례로 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="242de-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="242de-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="242de-186">Next steps</span></span>
- [<span data-ttu-id="242de-187">활동 로그 경고 toomonitor 구독에 대 한 모든 자동 크기 조정 엔진 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="242de-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="242de-188">만들기 작업 로그 경고 toomonitor 구독에 대해 실패 한 모든 자동 크기 조정 눈금-/ 스케일 아웃 작업</span><span class="sxs-lookup"><span data-stu-id="242de-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

