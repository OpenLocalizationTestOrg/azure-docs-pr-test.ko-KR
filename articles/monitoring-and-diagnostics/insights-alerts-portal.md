---
title: "-Azure 서비스에 대 한 경고 aaaCreate Azure 포털 | Microsoft Docs"
description: "트리거 전자 메일 알림, 지정한 hello 조건에 해당할 때 자동화 또는 웹 사이트 Url (webhook)를 호출 합니다."
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
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="817d4-103">Azure 서비스에 대한 Azure Monitor에서 메트릭 경고 만들기 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="817d4-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="817d4-104">포털</span><span class="sxs-lookup"><span data-stu-id="817d4-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="817d4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="817d4-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="817d4-106">CLI</span><span class="sxs-lookup"><span data-stu-id="817d4-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="817d4-107">개요</span><span class="sxs-lookup"><span data-stu-id="817d4-107">Overview</span></span>
<span data-ttu-id="817d4-108">이 문서를 사용 하 여 Azure 메트릭 경고를 tooset Azure 포털을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="817d4-109">Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="817d4-110">**메트릭 값** -hello 트리거를 지정 된 메트릭 hello 값 두 방향에서 모두 할당 하는 임계값을 초과할 때 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="817d4-111">즉, 트리거합니다 둘 다 때 hello 조건이 충족 먼저 되 고 다음 나중에 조건 하는 더 이상 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="817d4-112">**활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="817d4-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="817d4-113">활동 로그 경고에 대 한 자세한 toolearn [여기를 클릭](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="817d4-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="817d4-114">메트릭 경고 toodo hello 다음 표시할 때 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="817d4-115">보낼 전자 메일 알림 toohello 서비스 관리자 및 공동 관리자</span><span class="sxs-lookup"><span data-stu-id="817d4-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="817d4-116">사용자가 지정한 tooadditional 메일 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="817d4-117">webhook 호출</span><span class="sxs-lookup"><span data-stu-id="817d4-117">call a webhook</span></span>
* <span data-ttu-id="817d4-118">(만 hello Azure 포털)에서 Azure runbook의 실행 시작</span><span class="sxs-lookup"><span data-stu-id="817d4-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="817d4-119">다음을 통해 메트릭 경고 규칙에 대한 정보를 구성하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="817d4-120">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="817d4-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="817d4-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="817d4-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="817d4-122">명령줄 인터페이스(CLI)</span><span class="sxs-lookup"><span data-stu-id="817d4-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="817d4-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="817d4-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="817d4-124">Azure 포털 hello로 메트릭을에서 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="817d4-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="817d4-125">Hello에 [포털](https://portal.azure.com/)hello 리소스 모니터링에 관심이 있는 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="817d4-126">선택 **경고** 또는 **규칙 경고** hello 모니터링 섹션에서.</span><span class="sxs-lookup"><span data-stu-id="817d4-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="817d4-127">hello 텍스트 및 아이콘 다른 리소스에 대 한 약간 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![모니터링](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="817d4-129">선택 hello **추가 경고** 명령 및 hello 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Add alert](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="817d4-131">경고 규칙의 **이름**을 지정하고 **설명**을 선택합니다. 알림 이메일에도 표시되는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="817d4-132">선택 hello **메트릭을** toomonitor, 원하는 다음 선택는 **조건** 및 **임계값** hello 메트릭에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="817d4-133">Hello 선택한 **기간** 메트릭을 hello 시간의 규칙 hello 경고 트리거 하기 전에 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="817d4-134">예를 들어 hello 기간 "PT5M"를 사용 하는 경우 경고를 CPU 80% 이상 찾습니다 hello CPU 동안 일관 되 게 위의 80 %5 분 hello 알림을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="817d4-135">Hello 첫 번째 트리거가 발생 한 후 다시 hello CPU 5 분 동안 80% 미만으로 유지 되는 경우를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="817d4-136">CPU 측정 hello 매 1 분 마다 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="817d4-137">확인 **소유자를 전자 메일로 보내기...**  hello 경고 발생 때 관리자와 공동 관리자 toobe 전자 메일로 전송 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="817d4-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="817d4-138">추가 전자 메일 tooreceive 때 hello 알림 경고 발생을 hello에서 추가 **추가 관리자 email(s)** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="817d4-139">여러 전자 메일은 세미콜론(*email@contoso.com;email2@contoso.com*)으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="817d4-140">Hello 유효한 URI에 put **Webhook** 필드 호출 하려는 경우 경고 발생 hello 때.</span><span class="sxs-lookup"><span data-stu-id="817d4-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="817d4-141">Azure 자동화를 사용 하는 경우에 hello 경고가 발생할 때 실행할 Runbook toobe를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="817d4-142">선택 **확인** 하면 done toocreate hello 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="817d4-143">몇 분 안에 hello 경고가 활성 상태 이며 앞에서 설명한 대로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="817d4-144">경고 관리</span><span class="sxs-lookup"><span data-stu-id="817d4-144">Managing your alerts</span></span>
<span data-ttu-id="817d4-145">경고를 만든 후 해당 경고를 선택하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="817d4-146">이전 날짜 hello 메트릭 임계값과 hello hello의 실제 값을 보여 주는 그래프를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="817d4-147">편집 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="817d4-147">Edit or delete it.</span></span>
* <span data-ttu-id="817d4-148">**사용 안 함** 또는 **사용** tootemporarily 중지 하거나 재개 해당 경고에 대 한 알림을 수신 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="817d4-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="817d4-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="817d4-149">Next steps</span></span>
* <span data-ttu-id="817d4-150">[Azure 모니터링의 개요를 얻게](monitoring-overview.md) hello 형식의 정보를 수집 하 고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="817d4-151">[경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="817d4-152">[활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="817d4-153">[Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="817d4-154">서비스의 상세 고빈도 메트릭을 수집하기 위한 [진단 로그](monitoring-overview-of-diagnostic-logs.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="817d4-155">가져오기는 [메트릭 컬렉션의 개요](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="817d4-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
