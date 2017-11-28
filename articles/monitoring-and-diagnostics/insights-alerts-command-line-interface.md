---
title: "Azure 서비스-플랫폼 간 CLI에 대 한 경고 aaaCreate | Microsoft Docs"
description: "트리거 전자 메일 알림, 지정한 hello 조건에 해당할 때 자동화 또는 웹 사이트 Url (webhook)를 호출 합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="adcfe-103">Azure 서비스에 대한 Azure Monitor에서 메트릭 경고 만들기 - 플랫폼 간 CLI</span><span class="sxs-lookup"><span data-stu-id="adcfe-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="adcfe-104">포털</span><span class="sxs-lookup"><span data-stu-id="adcfe-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="adcfe-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="adcfe-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="adcfe-106">CLI</span><span class="sxs-lookup"><span data-stu-id="adcfe-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="adcfe-107">개요</span><span class="sxs-lookup"><span data-stu-id="adcfe-107">Overview</span></span>
<span data-ttu-id="adcfe-108">이 문서를 사용 하 여 Azure 메트릭 경고를 tooset 플랫폼 간 명령줄 인터페이스 (CLI) hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="adcfe-109">Azure 모니터는 2016 년 9 월 25 일 때까지 "Azure Insights" 라고 불렀습니다 기능에 대 한 새 이름을 hello는입니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="adcfe-110">그러나 hello 네임 스페이스 및 아래의 hello 명령 insights"hello" 여전히 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="adcfe-111">Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="adcfe-112">**메트릭 값** -hello 트리거를 지정 된 메트릭 hello 값 두 방향에서 모두 할당 하는 임계값을 초과할 때 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="adcfe-113">즉, 트리거합니다 둘 다 때 hello 조건이 충족 먼저 되 고 다음 나중에 조건 하는 더 이상 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="adcfe-114">**활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="adcfe-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="adcfe-115">활동 로그 경고에 대 한 자세한 toolearn [여기를 클릭](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="adcfe-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="adcfe-116">메트릭 경고 toodo hello 다음 표시할 때 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="adcfe-117">보낼 전자 메일 알림 toohello 서비스 관리자 및 공동 관리자</span><span class="sxs-lookup"><span data-stu-id="adcfe-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="adcfe-118">사용자가 지정한 tooadditional 메일 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="adcfe-119">webhook 호출</span><span class="sxs-lookup"><span data-stu-id="adcfe-119">call a webhook</span></span>
* <span data-ttu-id="adcfe-120">(만 hello이 이번에는 Azure 포털)에서 Azure runbook의 실행 시작</span><span class="sxs-lookup"><span data-stu-id="adcfe-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="adcfe-121">다음을 통해 메트릭 경고 규칙에 대한 정보를 구성하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="adcfe-122">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="adcfe-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="adcfe-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="adcfe-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="adcfe-124">명령줄 인터페이스(CLI)</span><span class="sxs-lookup"><span data-stu-id="adcfe-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="adcfe-125">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="adcfe-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="adcfe-126">명령을 입력 하 여 명령에 대 한 도움말을 항상 받을 수 있습니다 및 배치-hello 끝에 있는 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="adcfe-127">예:</span><span class="sxs-lookup"><span data-stu-id="adcfe-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="adcfe-128">Hello CLI를 사용 하 여 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="adcfe-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="adcfe-129">Hello 필수 구성 요소 및 로그인 tooAzure 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="adcfe-130">[Azure Monitor CLI 샘플](insights-cli-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adcfe-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="adcfe-131">즉, hello CLI를 설치 하 고이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="adcfe-132">로그인 하기를 사용 하 고 준비 toorun Azure 모니터 명령을 어떤 구독이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="adcfe-133">리소스 그룹에 대 한 toolist 기존 규칙 양식 다음 hello를 사용 하 여 **경고 규칙 목록 azure insights** *[옵션] &lt;리소스 그룹&gt;*</span><span class="sxs-lookup"><span data-stu-id="adcfe-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="adcfe-134">규칙을 toocreate toohave 몇 가지 중요 한 정보가 필요 정보의 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="adcfe-135">hello **리소스 ID** hello 리소스에 대 한 원하는 tooset에 대 한 경고</span><span class="sxs-lookup"><span data-stu-id="adcfe-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="adcfe-136">hello **메트릭 정의** 해당 리소스에 대해 사용할 수 있는</span><span class="sxs-lookup"><span data-stu-id="adcfe-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="adcfe-137">한 가지 방법은 tooget hello 리소스 ID는 toouse hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="adcfe-138">Hello 리소스를 이미 만든 경우 hello 포털에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="adcfe-139">다음 hello 다음 블레이드를 선택 *속성* hello에서 *설정을* 섹션.</span><span class="sxs-lookup"><span data-stu-id="adcfe-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="adcfe-140">hello *리소스 ID* hello 다음 블레이드에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="adcfe-141">또 다른 방법은 toouse hello [Azure 리소스 탐색기](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="adcfe-142">웹앱에 대한 예제 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="adcfe-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="adcfe-143">tooget hello 사용 가능한 메트릭 및 hello 이전 리소스 예제에서는 다음 CLI 명령을 사용 하 여 hello에 대 한 이러한 메트릭에 대 한 단위 목록:</span><span class="sxs-lookup"><span data-stu-id="adcfe-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="adcfe-144">*PT1M* hello 세분성 hello 사용할 수 있는 측정 (1 분 간격으로)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="adcfe-145">다른 세분성을 사용할 때는 다른 메트릭 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="adcfe-146">toocreate 메트릭을 기반 경고 규칙 hello 양식 뒤의 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="adcfe-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="adcfe-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="adcfe-148">경고를 설정 하는 예제 웹 사이트 리소스에 따라 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="adcfe-149">hello 경고 트리거 일관 되 게 5 분에서 다시 5 분 동안 트래픽이 받는 경우에 대 한 모든 트래픽은 받을 때마다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="adcfe-150">toocreate webhook 또는 송신 메일 메트릭 경고를 발생 시킨 경우에 먼저 hello 전자 메일 및/또는 webhook 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="adcfe-151">Hello 규칙을 즉시 만들 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="adcfe-152">연결할 수 없습니다 webhook 또는 포함 된 전자 메일 이미 hello CLI를 사용 하 여 규칙을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="adcfe-153">개별 규칙을 살펴서 경고가 제대로 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="adcfe-154">toodelete 규칙 hello 폼의 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="adcfe-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="adcfe-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="adcfe-156">이러한 명령은이 문서에서 이전에 만든 hello 규칙을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="adcfe-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="adcfe-157">Next steps</span></span>
* <span data-ttu-id="adcfe-158">[Azure 모니터링의 개요를 얻게](monitoring-overview.md) hello 형식의 정보를 수집 하 고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="adcfe-159">[경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="adcfe-160">[활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="adcfe-161">[Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="adcfe-162">가져오기는 [진단 로그를 수집 하는 작업을 간략하게](monitoring-overview-of-diagnostic-logs.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="adcfe-163">가져오기는 [메트릭 컬렉션의 개요](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="adcfe-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
