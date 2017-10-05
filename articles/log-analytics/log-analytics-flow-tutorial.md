---
title: "Microsoft Flow를 사용하여 Azure Log Analytics 프로세스 자동화"
description: "Microsoft Flow를 통해 Azure Log Analytics 커넥터를 사용하여 반복 가능한 프로세스를 신속하게 자동화하는 방법을 알아봅니다."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 4955f90de06cd720d78c5bb60c0adcd7dc633245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="ae729-103">Microsoft Flow용 커넥터를 사용하여 Log Analytics 프로세스 자동화</span><span class="sxs-lookup"><span data-stu-id="ae729-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="ae729-104">[Microsoft Flow](https://ms.flow.microsoft.com)를 사용하면 다양한 서비스에 수백 가지 작업을 통해 자동화된 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="ae729-105">한 작업의 출력을 서로 다른 서비스 간의 통합을 만들 수 있는 다른 작업에 대한 입력으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="ae729-106">Microsoft Flow에 대한 Azure Log Analytics 커넥터를 사용하면 Log Analytics의 로그 검색으로 검색한 데이터를 포함하는 워크플로를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="ae729-107">예를 들어 Microsoft Flow를 통해 Office 365의 전자 메일 알림에서 Log Analytics 데이터를 사용하거나, Visual Studio Team Services에서 버그를 만들거나, Slack 메시지를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="ae729-108">메일이나 트윗이 수신될 때와 같이 연결된 서비스의 일부 작업 또는 단순 일정에서 워크플로를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="ae729-109">Microsoft Flow에 대한 Azure Log Analytics 커넥터를 위해서는 작업 영역을 새로운 Log Analytics 쿼리 언어로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-109">The Azure Log Analytics connector for Microsoft Flow requires your workspace to be upgraded to the new Log Analytics query language.</span></span> <span data-ttu-id="ae729-110">[Azure Log Analytics 작업 영역을 새 로그 검색으로 업그레이드](log-analytics-log-search-upgrade.md)에서 새 언어에 대해 자세히 알아보고 작업 영역을 업그레이드하는 절차를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-110">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="ae729-111">이 문서의 자습서에서는 Microsoft Flow의 Log Analytics 사용 방법에 관한 예제를 통해 Log Analytics 로그 검색의 결과를 전자 메일로 자동으로 보내는 흐름을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-111">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="ae729-112">1단계: 흐름 만들기</span><span class="sxs-lookup"><span data-stu-id="ae729-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="ae729-113">[Microsoft Flow](http://flow.microsoft.com)에 로그인하고 **내 흐름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-113">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="ae729-114">**+빈 페이지에서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="ae729-115">2단계: 흐름에 대한 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="ae729-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="ae729-116">**다양한 커넥터 및 트리거 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="ae729-117">검색 상자에 **일정**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-117">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="ae729-118">**일정**을 선택한 다음, **일정 - 되풀이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="ae729-119">**빈도** 상자에서 **일**을 선택하고 **간격** 상자에 **1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-119">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="ae729-120">![Microsoft Flow 트리거 대화 상자](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="ae729-121">3단계: Log Analytics 작업 추가</span><span class="sxs-lookup"><span data-stu-id="ae729-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="ae729-122">**+새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="ae729-123">**Log Analytics**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="ae729-124">**Azure Log Analytics - 쿼리 실행 및 결과 시각화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="ae729-125">![Log Analytics 쿼리 실행 창](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="ae729-126">4단계: Log Analytics 작업 구성</span><span class="sxs-lookup"><span data-stu-id="ae729-126">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="ae729-127">구독 ID, 리소스 그룹 및 작업 영역 이름을 포함한 작업 영역에 대한 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-127">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="ae729-128">다음 Log Analytics 쿼리를 **쿼리** 창에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-128">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="ae729-129">이는 예제 쿼리일 뿐, 데이터를 반환하는 다른 항목으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="ae729-130">**차트 형식**에 **HTML 테이블**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-130">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="ae729-131">![Log Analytics 작업](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="ae729-132">5단계: 메일을 보내도록 흐름 구성</span><span class="sxs-lookup"><span data-stu-id="ae729-132">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="ae729-133">**새 단계**를 클릭한 다음 **+작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="ae729-134">**Office 365 Outlook**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="ae729-135">**Office 365 Outlook - 이메일 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="ae729-136">![Office 365 Outlook 선택 창](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="ae729-137">**받는 사람** 창에서 수신자의 이메일 주소 및 **제목**에서 전자 메일에 대한 제목을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-137">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="ae729-138">**본문** 상자에서 아무 곳이나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-138">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="ae729-139">이전 작업의 값이 포함된 **동적 콘텐츠** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="ae729-140">**본문**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-140">Select **Body**.</span></span>  <span data-ttu-id="ae729-141">Log Analytics 작업에 대한 쿼리의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-141">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="ae729-142">**고급 옵션 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="ae729-143">**HTML임** 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-143">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="ae729-144">![Office 365 전자 메일 구성 창](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="ae729-145">6단계: 흐름 저장 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ae729-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="ae729-146">**흐름 이름** 상자에 흐름 이름을 추가하고 **흐름 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-146">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="ae729-147">![흐름 저장](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="ae729-148">이제 흐름이 만들어졌으며, 사용자가 지정한 일정인 날짜에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-148">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="ae729-149">즉시 흐름을 테스트하려면 **지금 실행**, **흐름 실행**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-149">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="ae729-150">![흐름 실행](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="ae729-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="ae729-151">흐름이 완료되면 사용자가 지정한 수신자의 메일을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ae729-151">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="ae729-152">다음과 유사한 본문이 있는 메일을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-152">You should have received a mail with a body similar to the following:</span></span><br><br>![샘플 메일](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="ae729-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae729-154">Next steps</span></span>

- <span data-ttu-id="ae729-155">[Log Analytics의 로그 검색](log-analytics-log-search-new.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="ae729-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="ae729-156">[Microsoft Flow](https://ms.flow.microsoft.com)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae729-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



