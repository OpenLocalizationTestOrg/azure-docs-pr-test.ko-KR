---
title: "Azure 서비스에 대한 경고 만들기 - Azure portal | Microsoft Docs"
description: "지정한 조건이 충족될 경우 전자 메일, 알림, 웹 사이트 URL 호출(webhook) 또는 자동화를 트리거합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="8f247-103">Azure 서비스에 대한 Azure Monitor에서 메트릭 경고 만들기 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8f247-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f247-104">포털</span><span class="sxs-lookup"><span data-stu-id="8f247-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="8f247-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f247-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="8f247-106">CLI</span><span class="sxs-lookup"><span data-stu-id="8f247-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="8f247-107">개요</span><span class="sxs-lookup"><span data-stu-id="8f247-107">Overview</span></span>
<span data-ttu-id="8f247-108">이 문서에서는 Azure Portal을 사용하여 Azure 메트릭 경고를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="8f247-109">Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="8f247-110">**메트릭 값** - 이 경고는 특정 메트릭의 값이 어느 방향으로든 사용자가 할당한 임계값을 초과했을 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="8f247-111">즉 조건에 처음 부합했을 때와, 조건에 더 이상 부합하지 않게 되었을 때 모두 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="8f247-112">**활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="8f247-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="8f247-113">활동 로그 경고에 대해 자세히 알아보려면 [여기를 클릭](monitoring-activity-log-alerts.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="8f247-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="8f247-114">트리거되면 다음을 수행하도록 메트릭 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="8f247-115">서비스 관리자 및 공동 관리자에게 이메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="8f247-116">사용자가 지정한 추가 이메일 주소로 이메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="8f247-117">webhook 호출</span><span class="sxs-lookup"><span data-stu-id="8f247-117">call a webhook</span></span>
* <span data-ttu-id="8f247-118">Azure runbook 실행 시작(현재는 Azure 포털에서만 가능)</span><span class="sxs-lookup"><span data-stu-id="8f247-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="8f247-119">다음을 통해 메트릭 경고 규칙에 대한 정보를 구성하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="8f247-120">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8f247-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="8f247-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f247-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="8f247-122">명령줄 인터페이스(CLI)</span><span class="sxs-lookup"><span data-stu-id="8f247-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="8f247-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="8f247-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="8f247-124">Azure 포털에서 메트릭에 대한 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="8f247-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="8f247-125">[포털](https://portal.azure.com/)에서 모니터링하려는 리소스를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="8f247-126">MONITORING 섹션에서 **경고** 또는 **경고 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="8f247-127">텍스트와 아이콘은 리소스마다 약간씩 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-127">The text and icon may vary slightly for different resources.</span></span>  

    ![모니터링](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="8f247-129">**Add alert** 명령을 선택하고 필드에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Add alert](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="8f247-131">경고 규칙의 **이름**을 지정하고 **설명**을 선택합니다. 알림 이메일에도 표시되는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="8f247-132">모니터링할 **메트릭**을 선택하고 해당 메트릭에 대한 **조건** 및 **임계값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="8f247-133">경고를 트리거하기 전에 메트릭 규칙을 만족해야 하는 **기간** 도 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="8f247-134">예를 들어, "PT5M" 기간을 사용하고 경고가 80% 이상인 CPU를 찾는다면 이 경고는 CPU가 5분 동안 계속 80%를 넘으면 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="8f247-135">첫 번째 트리거가 발생한 후 CPU가 5분 동안 80% 미만을 유지하면 다시 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="8f247-136">CPU 측정은 1 분마다 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="8f247-137">경고가 발생했을 때 관리자 및 공동 관리자에게 이메일을 보내려면 **소유자에게 이메일 보내기...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="8f247-138">경고가 발생했을 때 다른 이메일 주소에서 알림을 받으려면 해당 이메일을 **추가 관리자 이메일** 필드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="8f247-139">여러 전자 메일은 세미콜론(*email@contoso.com;email2@contoso.com*)으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="8f247-140">경고가 발생했을 때 호출하려면 **Webhook** 필드에 유효한 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="8f247-141">Azure Automation을 사용하는 경우 경고가 발생할 때 실행할 Runbook을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="8f247-142">경고 만들기가 완료되면 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="8f247-143">앞서 설명한 대로 몇 분 안에 경고가 활성화 및 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="8f247-144">경고 관리</span><span class="sxs-lookup"><span data-stu-id="8f247-144">Managing your alerts</span></span>
<span data-ttu-id="8f247-145">경고를 만든 후 해당 경고를 선택하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="8f247-146">전날의 메트릭 임계값 및 실제 값을 표시하는 그래프 확인</span><span class="sxs-lookup"><span data-stu-id="8f247-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="8f247-147">편집 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="8f247-147">Edit or delete it.</span></span>
* <span data-ttu-id="8f247-148">해당 경고에 대한 알림 수신을 일시 중지 또는 재개하려면 **사용 중지** 또는 **사용**하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f247-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f247-149">Next steps</span></span>
* <span data-ttu-id="8f247-150">[Azure 모니터링 개요](monitoring-overview.md) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="8f247-151">[경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="8f247-152">[활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="8f247-153">[Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="8f247-154">서비스의 상세 고빈도 메트릭을 수집하기 위한 [진단 로그](monitoring-overview-of-diagnostic-logs.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="8f247-155">서비스를 사용 가능하며 응답할 수 있는 상태로 유지하기 위한 [메트릭 수집](insights-how-to-customize-monitoring.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f247-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
