---
title: "로그 분석 경고에서 Azure 자동화 Runbook aaaCalling | Microsoft Docs"
description: "이 문서에서는 방법 개괄적으로 Microsoft OMS 로그 분석 경고에서 자동화 runbook tooinvoke 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a><span data-ttu-id="813d2-103">OMS Log Analytics 경고에서 Azure Automation Runbook 호출</span><span class="sxs-lookup"><span data-stu-id="813d2-103">Calling an Azure Automation runbook from an OMS Log Analytics alert</span></span>

<span data-ttu-id="813d2-104">경고 로그 분석 toocreate에 구성 된 경우 결과 프로세서 사용률 또는 비즈니스 응용 프로그램의 특정 응용 프로그램 프로세스 중요 toohello 기능에 장기간된 스파이크가 등의 특정 조건에 일치 하는 경우에 경고 레코드 실패 해당 경고 시도 tooauto에서 자동화 runbook를 자동으로 실행할 수 hello Windows 이벤트 로그에는 해당 이벤트를 기록-hello 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-104">When an alert is configured in Log Analytics toocreate an alert record if results match a particular criteria, such as a prolonged spike in processor utilization or a particular application process critical toohello functionality of a business application fails and writes a corresponding event in hello Windows event log, that alert can automatically run an Automation runbook in an attempt tooauto-remediate hello issue.</span></span>  

<span data-ttu-id="813d2-105">있는 경우 두 가지 옵션 toocall runbook hello 경고를 구성 하는 경우</span><span class="sxs-lookup"><span data-stu-id="813d2-105">There are two options toocall a runbook when configuring hello alert.</span></span>  <span data-ttu-id="813d2-106">특히,</span><span class="sxs-lookup"><span data-stu-id="813d2-106">Specifically,</span></span>

1. <span data-ttu-id="813d2-107">웹후크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-107">Using a Webhook.</span></span>
   * <span data-ttu-id="813d2-108">OMS 작업 영역 연결된 tooan 자동화 계정이 없는 경우 이것이 hello 옵션만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-108">This is hello only option available if your OMS workspace is not linked tooan Automation account.</span></span>
   * <span data-ttu-id="813d2-109">자동화 계정 연결 tooan OMS 작업 영역, 이미 있는 경우이 옵션은 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-109">If you already have an Automation account linked tooan OMS workspace, this option is still available.</span></span>  

2. <span data-ttu-id="813d2-110">Runbook을 직접 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-110">Select a runbook directly.</span></span>
   * <span data-ttu-id="813d2-111">이 옵션은 hello OMS 작업 영역은 연결 된 자동화 계정을 tooan 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-111">This option is available only when hello OMS workspace is linked tooan Automation account.</span></span>  

## <a name="calling-a-runbook-using-a-webhook"></a><span data-ttu-id="813d2-112">웹후크를 사용하여 Runbook 호출</span><span class="sxs-lookup"><span data-stu-id="813d2-112">Calling a runbook using a webhook</span></span>

<span data-ttu-id="813d2-113">webhook이 있습니다 toostart를 특정 runbook Azure 자동화에서 단일 HTTP 요청을 통해.</span><span class="sxs-lookup"><span data-stu-id="813d2-113">A webhook allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span>  <span data-ttu-id="813d2-114">Hello를 구성 하기 전에 [로그 분석 경고](../log-analytics/log-analytics-alerts.md#alert-rules) 여 webhook을 사용할지를 사용 하 여 경고를 동작으로 toocall hello runbook 해야 toofirst이이 메서드를 사용 하 여 호출 되는 hello runbook에 대 한 webhook 만들기.</span><span class="sxs-lookup"><span data-stu-id="813d2-114">Before configuring hello [Log Analytics alert](../log-analytics/log-analytics-alerts.md#alert-rules) toocall hello runbook using a webhook as an alert action, you will need toofirst create a webhook for hello runbook that will be called using this method.</span></span>  <span data-ttu-id="813d2-115">검토 하 고 hello의 hello 단계를 따라 [는 webhook 만들기](automation-webhooks.md#creating-a-webhook) 문서 및 hello 경고 규칙을 구성 하는 동안 참조할 수 있도록 toorecord hello webhook URL을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-115">Review and follow hello steps in hello [create a webhook](automation-webhooks.md#creating-a-webhook) article and remember toorecord hello webhook URL so that you can reference it while configuring hello alert rule.</span></span>   

## <a name="calling-a-runbook-directly"></a><span data-ttu-id="813d2-116">Runbook 직접 호출</span><span class="sxs-lookup"><span data-stu-id="813d2-116">Calling a runbook directly</span></span>

<span data-ttu-id="813d2-117">Hello 자동화 있는 & 제어 제품에에서 설치 및 구성 OMS 작업 영역을 hello 경고에 대 한 hello Runbook 작업 옵션을 구성할 때, 경우에 hello에서 모든 runbook을 볼 수 있습니다 **runbook 선택** 드롭다운 목록 및 원하는 응답 toohello 경고 toorun hello 특정 runbook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-117">If you have hello Automation & Control offering installed and configured in your OMS workspace, when configuring hello Runbook actions option for hello alert, you can view all runbooks from hello **Select a runbook** dropdown list and select hello specific runbook you want toorun in response toohello alert.</span></span>  <span data-ttu-id="813d2-118">hello Azure 클라우드 또는 하이브리드 runbook 작업자에서 작업 영역에서 선택한 hello runbook을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-118">hello selected runbook can run in a workspace in hello Azure cloud or on a hybrid runbook worker.</span></span>  <span data-ttu-id="813d2-119">Hello 경고를 만들면 hello runbook 옵션을 사용 하 여 webhook을 사용할지 hello runbook에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-119">When hello alert is created using hello runbook option, a webhook will be created for hello runbook.</span></span>  <span data-ttu-id="813d2-120">Toohello 자동화 계정 이동 하 고 hello 선택한 runbook의 toohello webhook 블레이드를 탐색 하는 경우 hello webhook을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-120">You can see hello webhook if you go toohello Automation account and navigate toohello webhook blade of hello selected runbook.</span></span>  <span data-ttu-id="813d2-121">Hello 경고를 삭제 하면 hello webhook 삭제 되지 않습니다 되지만 hello 사용자 hello webhook을 수동으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-121">If you delete hello alert, hello webhook is not deleted, but hello user can delete hello webhook manually.</span></span>  <span data-ttu-id="813d2-122">Hello webhook 삭제 되지 않은 경우 문제가 이므로 구성 된 자동화 계정을 순서 toomaintain에서 결국 toobe 내용이 고아 항목이 방금 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-122">It is not a problem if hello webhook is not deleted, it is just an orphaned item that will eventually need toobe deleted in order toomaintain an organized Automation account.</span></span>  

## <a name="characteristics-of-a-runbook-for-both-options"></a><span data-ttu-id="813d2-123">Runbook의 특징(두 가지 옵션)</span><span class="sxs-lookup"><span data-stu-id="813d2-123">Characteristics of a runbook (for both options)</span></span>

<span data-ttu-id="813d2-124">두 방법 모두 hello 로그 분석 경고에서 hello runbook 호출 toobe 경고 규칙을 구성 하기 전에 이해 해야 하는 다른 동작이 특징을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-124">Both methods for calling hello runbook from hello Log Analytics alert have different behavior characteristics that need toobe understood before you configure your alert rules.</span></span>  

* <span data-ttu-id="813d2-125">**Object** 유형인 **WebhookData**라는 Runbook 입력 매개 변수가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-125">You must have a runbook input parameter called **WebhookData** that is **Object** type.</span></span>  <span data-ttu-id="813d2-126">이는 필수 사항이거나 선택 사항일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-126">It can be mandatory or optional.</span></span>  <span data-ttu-id="813d2-127">hello 경고가 입력된 매개 변수를 사용 하 여 hello 검색 결과 toohello runbook에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-127">hello alert passes hello search results toohello runbook using this input parameter.</span></span>

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  <span data-ttu-id="813d2-128">코드 tooconvert hello WebhookData tooa PowerShell 개체가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-128">You must have code tooconvert hello WebhookData tooa PowerShell object.</span></span>

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    <span data-ttu-id="813d2-129">*$SearchResults* 개체의 배열이 됩니다; hello 값이 하나의 검색 결과에서 필드를 포함 하는 각 개체</span><span class="sxs-lookup"><span data-stu-id="813d2-129">*$SearchResults* will be an array of objects; each object contains hello fields with values from one search result</span></span>

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a><span data-ttu-id="813d2-130">Hello webhook 옵션 및 runbook 옵션 간의 WebhookData 불일치</span><span class="sxs-lookup"><span data-stu-id="813d2-130">WebhookData inconsistencies between hello webhook option and runbook option</span></span>

* <span data-ttu-id="813d2-131">경고는 toocall 여 webhook을 사용할지를 구성할 때 runbook에 대해 만든 webhook URL을 입력 하 고 hello 클릭 **테스트 Webhook** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-131">When configuring an alert toocall a Webhook, enter a webhook URL you created for a runbook, and click hello **Test Webhook** button.</span></span>  <span data-ttu-id="813d2-132">hello 결과 WebhookData 전송 toohello runbook 포함 하지 않습니다 *합니다. SearchResult* 또는 *합니다. SearchResults*합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-132">hello resulting WebhookData sent toohello runbook does not contain either *.SearchResult* or *.SearchResults*.</span></span>

*  <span data-ttu-id="813d2-133">Hello WebhookData 전송 toohello runbook에 포함 된 hello 경고를 트리거한 다음 hello webhook을 호출 하는 경우 해당 경고를 저장 하면 *합니다. SearchResult*합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-133">If you save that alert, when hello alert triggers and calls hello webhook, hello WebhookData sent toohello runbook contains *.SearchResult*.</span></span>
* <span data-ttu-id="813d2-134">경고를 만들고 toocall (하 여 webhook을 사용할지.dgml 파일)는 runbook을 구성할 때 포함 된 WebhookData toohello runbook 보내는 알림 트리거 hello *합니다. SearchResults*합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-134">If you create an alert, and configure it toocall a runbook (which also creates a webhook), when hello alert triggers it sends WebhookData toohello runbook that contains *.SearchResults*.</span></span>

<span data-ttu-id="813d2-135">따라서 위의 hello 코드 예제에는 필요 tooget *합니다. SearchResult* hello 경고는 webhook을 호출 하 고 tooget 할 *합니다. SearchResults* hello 경고 runbook을 직접 호출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="813d2-135">Thus in hello code example above, you will need tooget *.SearchResult* if hello alert calls a webhook, and will need tooget *.SearchResults* if hello alert calls a runbook directly.</span></span>

## <a name="example-walkthrough"></a><span data-ttu-id="813d2-136">연습 예</span><span class="sxs-lookup"><span data-stu-id="813d2-136">Example walkthrough</span></span>

<span data-ttu-id="813d2-137">다음 예에서는 그래픽 runbook Windows 서비스를 시작 하는 hello를 사용 하 여 작동 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-137">We will demonstrate how this works by using hello following example graphical runbook, which starts a Windows service.</span></span><br><br> ![Windows 서비스 그래픽 Runbook 시작](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

<span data-ttu-id="813d2-139">hello runbook에 하나의 입력된 매개 변수 형식의 **개체** 호출 되 **WebhookData** hello 경고 포함 된에서 전달 된 hello webhook 데이터를 포함 하 고 *합니다. SearchResults*합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-139">hello runbook has one input parameter of type **Object** that is called **WebhookData** and includes hello webhook data passed from hello alert containing *.SearchResults*.</span></span><br><br> <span data-ttu-id="813d2-140">![Runbook 입력 매개 변수](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)</span><span class="sxs-lookup"><span data-stu-id="813d2-140">![Runbook input parameters](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)</span></span><br>

<span data-ttu-id="813d2-141">이 예제에 대 한 로그 분석에서 만든 두 개의 사용자 지정 필드 *SvcDisplayName_CF* 및 *SvcState_CF*, tooextract hello 서비스 표시 이름 및 hello 서비스의 상태 hello (실행 중 또는 중지) hello 이벤트에서 toohello 시스템 이벤트 로그를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-141">For this example, in Log Analytics we created two custom fields, *SvcDisplayName_CF* and *SvcState_CF*, tooextract hello service display name and hello state of hello service (i.e. running or stopped) from hello event written toohello System event log.</span></span>  <span data-ttu-id="813d2-142">경고 규칙이 검색 쿼리를 수행 하는 hello로 만듭니다: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` hello Windows 시스템에 hello 인쇄 스풀러 서비스가 중지 될 때 검색 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-142">We then create an alert rule with hello following search query: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` so that we can detect when hello Print Spooler service is stopped on hello Windows system.</span></span>  <span data-ttu-id="813d2-143">관심 있는 모든 서비스 수는 있지만이 예에서는 참조 하는 hello Windows 운영 체제에 포함 되어 있는 hello 기존 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-143">It can be any service of interest, but for this example we are referencing one of hello pre-existing services that are included with hello Windows OS.</span></span>  <span data-ttu-id="813d2-144">구성 된 tooexecute이이 예제에서 사용 하는 runbook은 hello 대상 시스템에서 설정 된 hello 하이브리드 Runbook 작업자에서 실행 하는 hello 경고 동작.</span><span class="sxs-lookup"><span data-stu-id="813d2-144">hello alert action is configured tooexecute our runbook used in this example and run on hello Hybrid Runbook Worker, which are enabled on hello target systems.</span></span>   

<span data-ttu-id="813d2-145">runbook 코드 활동 hello **LA에서 서비스 이름을 가져올** 개체 유형 및 hello 항목에 대 한 필터에 hello JSON 형식 문자열로 변환 됩니다 *SvcDisplayName_CF* hello의 tooextract hello 표시 이름 Windows 서비스 및이 toorestart 시도 하기 전에 hello 서비스가 중지 되는 확인 된 hello 다음 활동에 전달할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-145">hello runbook code activity **Get Service Name from LA** will convert hello JSON-formatted string into an object type and filter on hello item *SvcDisplayName_CF* tooextract hello display name of hello Windows service and pass this onto hello next activity which will verify hello service is stopped before attempting toorestart it.</span></span>  <span data-ttu-id="813d2-146">*SvcDisplayName_CF* 는 [사용자 지정 필드](../log-analytics/log-analytics-custom-fields.md) 이 예에서는 로그 분석 toodemonstrate에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-146">*SvcDisplayName_CF* is a [custom field](../log-analytics/log-analytics-custom-fields.md) created in Log Analytics toodemonstrate this example.</span></span>

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

<span data-ttu-id="813d2-147">Hello 서비스 중지 될 때 로그 분석의 hello 경고 규칙에서는 검색 일치 하는 및 hello runbook을 트리거할 하 고 hello 경고 컨텍스트 toohello runbook을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-147">When hello service stops, hello alert rule in Log Analytics will detect a match and trigger hello runbook and send hello alert context toohello runbook.</span></span> <span data-ttu-id="813d2-148">hello runbook은 작업을 수행 하는 경우 지금 시도 toorestart 서비스 hello 하 고 확인 하 고 올바르게 시작 하 고 결과 출력 hello tooverify hello 서비스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-148">hello runbook will take action tooverify hello service is stopped, and if so attempt toorestart hello service and verify it started correctly and output hello results.</span></span>     

<span data-ttu-id="813d2-149">또는 자동화 계정 연결 tooyour OMS 작업 영역에 없으면 webhook 작업 tootrigger hello runbook이 포함 된 hello 경고 규칙을 구성 하는 hello runbook tooconvert hello JSON 형식 문자열 및 에대한필터구성*. SearchResult* 앞에서 언급 한 hello 지침.</span><span class="sxs-lookup"><span data-stu-id="813d2-149">Alternatively if you don't have your Automation account linked tooyour OMS workspace, you would configure hello alert rule with a webhook action tootrigger hello runbook and configure hello runbook tooconvert hello JSON-formatted string and filter on *.SearchResult* following hello guidance mentioned earlier.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="813d2-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="813d2-150">Next steps</span></span>

* <span data-ttu-id="813d2-151">로그 분석에는 경고에 대 한 자세한 toolearn toocreate 하나를 참조 하는 방법 및 [로그 분석에서 경고](../log-analytics/log-analytics-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-151">toolearn more about alerts in Log Analytics and how toocreate one, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md).</span></span>

* <span data-ttu-id="813d2-152">tootrigger runbook는 webhook을 사용 하 여 확인 하려면 어떻게 해야 toounderstand [Azure 자동화 webhook](automation-webhooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="813d2-152">toounderstand how tootrigger runbooks using a webhook, see [Azure Automation webhooks](automation-webhooks.md).</span></span>
