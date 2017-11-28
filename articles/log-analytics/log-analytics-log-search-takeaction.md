---
title: "Log Analytics에서 사용자가 시작한 Azure Automation Runbook 작업 | Microsoft Docs"
description: "이 문서는 요청 시 Log Analytics 검색 결과에서 Automation Runbook을 실행하는 방법을 설명합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: ff938697add98f3d21b4971175432335ee2e39ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a><span data-ttu-id="6b3d0-103">Log Analytics 로그 검색 결과에서 Automation Runbook으로 작업 수행</span><span class="sxs-lookup"><span data-stu-id="6b3d0-103">Take Action with an Automation Runbook from a Log Analytics log search result</span></span>

<span data-ttu-id="6b3d0-104">Azure Log Analytics의 로그 검색 결과에서 이제 Automation Runbook을 실행하도록 **작업 수행**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-104">From a log search result in Azure Log Analytics, you can now select **Take action** to run an Automation runbook.</span></span>  <span data-ttu-id="6b3d0-105">Runbook은 문제를 해결하거나 문제 해결 정보 수집, 전자 메일 전송 또는 서비스 요청 만들기와 같은 다른 작업을 수행하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-105">The runbook can be used to remediate the issue or take some other action such as collect troubleshooting information, send an email, or create a service request.</span></span> 

## <a name="components-and-features-used"></a><span data-ttu-id="6b3d0-106">사용된 구성 요소 및 기능</span><span class="sxs-lookup"><span data-stu-id="6b3d0-106">Components and features used</span></span>
* [<span data-ttu-id="6b3d0-107">Azure Automation 계정</span><span class="sxs-lookup"><span data-stu-id="6b3d0-107">Azure Automation account</span></span>](../automation/automation-offering-get-started.md)
* [<span data-ttu-id="6b3d0-108">Log Analytics 작업 영역</span><span class="sxs-lookup"><span data-stu-id="6b3d0-108">Log Analytics workspace</span></span>](../log-analytics/log-analytics-overview.md)

## <a name="to-initiate-runbook-from-log-search"></a><span data-ttu-id="6b3d0-109">로그 검색에서 Runbook을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="6b3d0-109">To initiate runbook from log search</span></span>

<span data-ttu-id="6b3d0-110">이벤트에서 작업을 수행하고 로그 검색 결과에서 Runbook을 시작하려면 로그 검색을 생성하여 시작하고 결과에서 요청 시 Runbook을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-110">To take action on an event and initiate a runbook from your log search results, you start by creating a log search and from the results you can invoke a runbook on-demand.</span></span>  <span data-ttu-id="6b3d0-111">Azure 또는 [OMS 포털](../log-analytics/log-analytics-log-searches.md)의 로그 검색 기능에서 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-111">This can be achieved from the log search feature in the Azure or [OMS portal](../log-analytics/log-analytics-log-searches.md).</span></span>  <span data-ttu-id="6b3d0-112">이 예제에서는 이 기능의 기본적인 데모를 사용하여 Azure Portal에서 로그 검색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-112">In this example, we perform a log search from the Azure portal with a basic demonstration of this feature.</span></span>

1. <span data-ttu-id="6b3d0-113">Azure Portal의 허브 메뉴에서 **더 많은 서비스**를 클릭하고 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-113">In the Azure portal, on the Hub menu click **More services** and select **Log Analytics**.</span></span>  
2. <span data-ttu-id="6b3d0-114">Log Analytics 블레이드에서 Log Analytics 작업 영역을 선택하고 작업 영역 블레이드에서 **로그 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-114">On the Log Analytics blade, select your Log Analytics workspace and on the workspace blade select **Log Search**.</span></span>  
3. <span data-ttu-id="6b3d0-115">로그 검색 블레이드에서 로그 검색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-115">On the Log Search blade, perform a log search.</span></span>  
4. <span data-ttu-id="6b3d0-116">로그 검색 결과에서 필드 중 하나의 왼쪽에 있는 줄임표를 클릭하고 팝업에서 **작업 수행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-116">From the log search results, click the ellipse to the left of one of the fields and from the popup, select **Take action on**.</span></span><br><br> <span data-ttu-id="6b3d0-117">![검색 결과에서 작업 수행 선택](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png)</span><span class="sxs-lookup"><span data-stu-id="6b3d0-117">![Select Take Action from search result](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png)</span></span> 
5. <span data-ttu-id="6b3d0-118">작업 수행 블레이드에서 **Runbook 실행**을 선택하고 **Runbook 실행** 블레이드에서 Runbook 실행을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-118">From the Take action blade, select **Run a runbook**, and on the **Run a runbook** blade you can select a runbook to run.</span></span>  <span data-ttu-id="6b3d0-119">Log Analytics 작업 영역에 연결된 Automation 계정에서 Runbook을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-119">You can select any runbook in the Automation account that is linked to the Log Analytics workspace.</span></span>  <span data-ttu-id="6b3d0-120">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-120">Note the following:</span></span>

    * <span data-ttu-id="6b3d0-121">Runbook은 태그로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-121">Runbooks are organized by tags</span></span>
    * <span data-ttu-id="6b3d0-122">Runbook 입력 매개 변수 값은 검색 결과의 필드에서 직접 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-122">Runbook input parameter values can be selected directly from the fields of the search result.</span></span>  <span data-ttu-id="6b3d0-123">드롭다운 목록은 선택하는 결과에서 사용할 수 있는 모든 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-123">A drop-down list will appear displaying all the available fields from the result to select from.</span></span>  
    * <span data-ttu-id="6b3d0-124">멤버로 이 컴퓨터만을 포함하는 해당 Hybrid Runbook Worker 그룹이 있는 경우 문제가 있는 컴퓨터에 설치한 [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md)에서 Runbook을 실행하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-124">You can choose to run the runbook on a [hybrid runbook worker](../automation/automation-hybrid-runbook-worker.md) that you have installed on the machine that has the issue if you have a corresponding Hybrid Runbook Worker group that only contains this machine as a member.</span></span>  <span data-ttu-id="6b3d0-125">Hybrid Worker 그룹의 이름이 로그 검색 결과에 있는 컴퓨터의 이름과 일치하는 경우 그룹이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-125">If the name of the Hybrid Worker group matches the name of the computer that is in the log search result, then the group is selected automatically.</span></span>    

6. <span data-ttu-id="6b3d0-126">**실행**을 클릭한 후 작업의 상태를 검토할 수 있도록 Runbook 작업 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-126">After you click **Run**, the runbook job blade will open to allow you to review the status of the job.</span></span>   

<span data-ttu-id="6b3d0-127">[Log Analytics 경고에서 호출](../automation/automation-invoke-runbook-from-omsla-alert.md)되도록 구성된 Runbook을 선택하는 경우 **개체** 유형인 **WebhookData**라는 입력 매개 변수를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-127">If you select a runbook that was configured to be [called from a Log Analytics alert](../automation/automation-invoke-runbook-from-omsla-alert.md), it has an input parameter called **WebhookData** that is **Object** type.</span></span>  <span data-ttu-id="6b3d0-128">입력 매개 변수가 필수인 경우 JSON 형식 문자열을 Runbook 작업에서 참조할 특정 항목을 필터링할 수 있도록 하는 개체 형식으로 변환할 수 있도록 검색 결과를 Runbook에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-128">If the input parameter is mandatory, you need to pass the search results to the runbook so it can convert the JSON-formatted string into an object type allowing you to filter on specific items that you will reference in runbook activities.</span></span>  <span data-ttu-id="6b3d0-129">드롭다운 목록에서 **검색 결과(개체)**를 선택하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-129">You do this by selecting **Search result (Object)** from the drop-down list.</span></span><br><br> <span data-ttu-id="6b3d0-130">![Runbook 매개 변수에 대한 웹후크 데이터 개체 선택](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)</span><span class="sxs-lookup"><span data-stu-id="6b3d0-130">![Select Webhook data object for runbook parameter](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)</span></span>   
    
## <a name="next-steps"></a><span data-ttu-id="6b3d0-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b3d0-131">Next steps</span></span>

* <span data-ttu-id="6b3d0-132">Log Analytics에 제공되는 모든 검색 필드 및 패싯을 보려면 [Log Analytics log search reference](log-analytics-search-reference.md) (Log Analytics 로그 검색 참조)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-132">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
* <span data-ttu-id="6b3d0-133">Automation Runbook을 자동으로 호출하는 방법을 알아보려면 [OMS Log Analytics 경고에서 Azure Automation Runbook 호출](../automation/automation-invoke-runbook-from-omsla-alert.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b3d0-133">To learn how to invoke an Automation runbook automatically, review [calling an Azure Automation runbook from an OMS Log Analytics alert](../automation/automation-invoke-runbook-from-omsla-alert.md).</span></span>  