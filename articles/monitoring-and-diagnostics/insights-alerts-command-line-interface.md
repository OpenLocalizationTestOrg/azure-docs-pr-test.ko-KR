---
title: "Azure 서비스에 대한 경고 만들기 - 플랫폼 간 CLI | Microsoft Docs"
description: "지정한 조건이 충족될 경우 전자 메일, 알림, 웹 사이트 URL 호출(webhook) 또는 자동화를 트리거합니다."
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
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="46220-103">Azure 서비스에 대한 Azure Monitor에서 메트릭 경고 만들기 - 플랫폼 간 CLI</span><span class="sxs-lookup"><span data-stu-id="46220-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46220-104">포털</span><span class="sxs-lookup"><span data-stu-id="46220-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="46220-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46220-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="46220-106">CLI</span><span class="sxs-lookup"><span data-stu-id="46220-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="46220-107">개요</span><span class="sxs-lookup"><span data-stu-id="46220-107">Overview</span></span>
<span data-ttu-id="46220-108">이 문서에서는 플랫폼 간 CLI(명령줄 인터페이스)를 사용하여 Azure 메트릭 경고를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46220-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="46220-109">Azure Monitor는 2016년 9월 25일까지는 "Azure Insights"로 지칭했던 제품의 새로운 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="46220-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="46220-110">하지만 네임스페이스와 아래 명령에서는 "insights"를 계속 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="46220-111">Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="46220-112">**메트릭 값** - 이 경고는 특정 메트릭의 값이 어느 방향으로든 사용자가 할당한 임계값을 초과했을 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="46220-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="46220-113">즉 조건에 처음 부합했을 때와, 조건에 더 이상 부합하지 않게 되었을 때 모두 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="46220-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="46220-114">**활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="46220-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="46220-115">활동 로그 경고에 대해 자세히 알아보려면 [여기를 클릭](monitoring-activity-log-alerts.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="46220-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="46220-116">트리거되면 다음을 수행하도록 메트릭 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="46220-117">서비스 관리자 및 공동 관리자에게 이메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="46220-118">사용자가 지정한 추가 이메일 주소로 이메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="46220-119">webhook 호출</span><span class="sxs-lookup"><span data-stu-id="46220-119">call a webhook</span></span>
* <span data-ttu-id="46220-120">Azure runbook 실행 시작(현재는 Azure 포털에서만 가능)</span><span class="sxs-lookup"><span data-stu-id="46220-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="46220-121">다음을 통해 메트릭 경고 규칙에 대한 정보를 구성하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="46220-122">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="46220-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="46220-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46220-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="46220-124">명령줄 인터페이스(CLI)</span><span class="sxs-lookup"><span data-stu-id="46220-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="46220-125">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="46220-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="46220-126">명령을 입력하고 마지막에 -help를 붙이면 항상 도움말을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="46220-127">예:</span><span class="sxs-lookup"><span data-stu-id="46220-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="46220-128">CLI를 사용하여 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="46220-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="46220-129">필수 구성 요소를 수행한 다음 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="46220-130">[Azure Monitor CLI 샘플](insights-cli-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46220-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="46220-131">즉 CLI를 설치하고 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="46220-132">로그인 후 사용자가 사용하는 구독을 표시하며 Azure Monitor 명령 실행을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="46220-133">리소스 그룹에 대해 기존 규칙을 나열하려면 **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;* 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="46220-134">규칙을 만들려면 먼저 몇 가지 중요한 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="46220-135">경고를 설정할 리소스의 **리소스 ID**</span><span class="sxs-lookup"><span data-stu-id="46220-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="46220-136">리소스에 대해 사용 가능한 **메트릭 정의**</span><span class="sxs-lookup"><span data-stu-id="46220-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="46220-137">리소스 ID를 가져오는 한 가지 방법은 Azure 포털을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="46220-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="46220-138">리소스를 이미 만들었다고 가정하고 포털에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="46220-139">이 후 다음 블레이드에서 *설정* 섹션의 *속성*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="46220-140">*리소스 ID* 는 다음 블레이드의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="46220-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="46220-141">또 다른 방법은 [Azure Resource Explorer](https://resources.azure.com/)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="46220-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="46220-142">웹앱에 대한 예제 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="46220-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="46220-143">이전 리소스 예제에 대한 메트릭의 사용 가능한 메트릭 및 단위 목록을 가져오려면 다음 CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="46220-144">*PT1M* 은 사용 가능한 측정의 세분성입니다(1분 간격).</span><span class="sxs-lookup"><span data-stu-id="46220-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="46220-145">다른 세분성을 사용할 때는 다른 메트릭 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="46220-146">메트릭 기반 경고 규칙을 만들려면 다음 형태의 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="46220-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="46220-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="46220-148">다음 예제에서는 웹 사이트 리소스에 대한 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="46220-149">이 경고는 어느 트래픽이나 5분 동안 계속 수신되면 항상 트리거되며, 트래픽이 5분 동안 수신되지 않으면 다시 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="46220-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="46220-150">메트릭 경고가 발생할 때 Webhook를 만들거나 전자 메일을 보내려면 먼저 이메일 및/또는 웹후크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46220-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="46220-151">그런 다음 바로 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46220-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="46220-152">Webhook나 이메일을 CLI를 통해 이미 생성된 규칙과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="46220-153">개별 규칙을 살펴서 경고가 제대로 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46220-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="46220-154">규칙을 삭제하려면 다음 형태의 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="46220-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="46220-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="46220-156">이 명령은 이 문서에서 앞서 만든 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="46220-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46220-157">Next steps</span></span>
* <span data-ttu-id="46220-158">[Azure 모니터링 개요](monitoring-overview.md) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="46220-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="46220-159">[경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="46220-160">[활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="46220-161">[Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="46220-162">서비스의 상세 고빈도 메트릭을 수집하기 위한 [진단 로그 수집](monitoring-overview-of-diagnostic-logs.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="46220-163">서비스를 사용 가능하며 응답할 수 있는 상태로 유지하기 위한 [메트릭 수집](insights-how-to-customize-monitoring.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="46220-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
