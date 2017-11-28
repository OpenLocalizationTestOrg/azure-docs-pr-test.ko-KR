---
title: "Azure 로그 분석을 aaaAutomate Microsoft 흐름에 따라 처리"
description: "Microsoft Flow를 사용 하는 방법에 대해 알아봅니다 tooquickly hello Azure 로그 분석 커넥터를 사용 하 여 반복 가능한 프로세스를 자동화 합니다."
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
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="18f8e-103">Microsoft flow hello 커넥터와 함께 로그 분석 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="18f8e-104">[Microsoft Flow](https://ms.flow.microsoft.com) 수백 가지 작업을 사용 하 여 다양 한 서비스에 대 한 자동화 된 toocreate 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="18f8e-105">출력 한 동작을 서로 다른 서비스 간의 toocreate 통합 있도록 입력된 tooanother로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="18f8e-106">Microsoft flow hello Azure 로그 분석 커넥터를 사용 하면 로그 분석에서 로그 검색에서 검색 된 데이터를 포함 하는 toobuild 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="18f8e-107">예를 들어 Microsoft Flow toouse 로그 분석 데이터를 사용 하 여 Office 365에서 전자 메일 알림을에서 Visual Studio Team Services에서 버그를 만들 하거나 Slack 메시지를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="18f8e-108">메일이나 트윗이 수신될 때와 같이 연결된 서비스의 일부 작업 또는 단순 일정에서 워크플로를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="18f8e-109">Microsoft flow hello Azure 로그 분석 커넥터 작업 영역 업그레이드 toobe toohello 새 로그 분석 쿼리 언어를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="18f8e-110">Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="18f8e-111">이 문서의 hello 자습서에서는 전자 메일, 예로, Microsoft Flow의 로그 분석을 사용 하는 방법을 자동으로 전송 하는 흐름 toocreate 로그 분석 로그 검색 결과 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="18f8e-112">1단계: 흐름 만들기</span><span class="sxs-lookup"><span data-stu-id="18f8e-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="18f8e-113">역시 로그인[Microsoft Flow](http://flow.microsoft.com)를 선택 하 고 **내 흐름**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="18f8e-114">**+빈 페이지에서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="18f8e-115">2단계: 흐름에 대한 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="18f8e-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="18f8e-116">**다양한 커넥터 및 트리거 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="18f8e-117">형식 **일정** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="18f8e-118">**일정**을 선택한 다음, **일정 - 되풀이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="18f8e-119">Hello에 **주파수** 상자 선택 **일** 및 hello **간격** 상자에 입력 **1**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="18f8e-120">![Microsoft Flow 트리거 대화 상자](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="18f8e-121">3단계: Log Analytics 작업 추가</span><span class="sxs-lookup"><span data-stu-id="18f8e-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="18f8e-122">**+새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="18f8e-123">**Log Analytics**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="18f8e-124">**Azure Log Analytics - 쿼리 실행 및 결과 시각화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="18f8e-125">![Log Analytics 쿼리 실행 창](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="18f8e-126">Hello 로그 분석 작업을 구성 하는 4 단계:</span><span class="sxs-lookup"><span data-stu-id="18f8e-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="18f8e-127">Hello 구독 ID, 리소스 그룹 및 작업 영역 이름을 포함 하 여 작업 영역에 대 한 hello 세부 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="18f8e-128">로그 분석 쿼리 toohello 다음 hello 추가 **쿼리** 창.</span><span class="sxs-lookup"><span data-stu-id="18f8e-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="18f8e-129">이는 예제 쿼리일 뿐, 데이터를 반환하는 다른 항목으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="18f8e-130">선택 **HTML 표** hello에 대 한 **차트 종류**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="18f8e-131">![Log Analytics 작업](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="18f8e-132">5 단계: hello 흐름 toosend 전자 메일 구성</span><span class="sxs-lookup"><span data-stu-id="18f8e-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="18f8e-133">**새 단계**를 클릭한 다음 **+작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="18f8e-134">**Office 365 Outlook**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="18f8e-135">**Office 365 Outlook - 이메일 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="18f8e-136">![Office 365 Outlook 선택 창](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="18f8e-137">Hello에 받는 사람의 hello 전자 메일 주소를 지정 **를** 창과 hello 전자 메일의 제목을 **주체**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="18f8e-138">Hello에서 아무 곳 이나 클릭 **본문** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="18f8e-139">이전 작업의 값이 포함된 **동적 콘텐츠** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="18f8e-140">**본문**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-140">Select **Body**.</span></span>  <span data-ttu-id="18f8e-141">이 hello 쿼리 결과를 hello hello 로그 분석 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="18f8e-142">**고급 옵션 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="18f8e-143">Hello에 **은 HTML** 상자 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="18f8e-144">![Office 365 전자 메일 구성 창](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="18f8e-145">6단계: 흐름 저장 및 테스트</span><span class="sxs-lookup"><span data-stu-id="18f8e-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="18f8e-146">Hello에 **흐름 이름** 상자, 프로그램 흐름에 대 한 이름을 추가 하 고 클릭 **흐름을 만드는**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="18f8e-147">![흐름 저장](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="18f8e-148">hello 흐름 이제 만들어지고 지정한 hello 일정 인 일 후에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="18f8e-149">tooimmediately 테스트 hello 흐름 클릭 **지금 실행** 차례로 **흐름 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="18f8e-150">![흐름 실행](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="18f8e-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="18f8e-151">Hello 흐름 완료 되 면 사용자가 지정한 hello 수신자의 hello 메일을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="18f8e-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="18f8e-152">본문 비슷한 toohello 다음으로 메일을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![샘플 메일](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="18f8e-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18f8e-154">Next steps</span></span>

- <span data-ttu-id="18f8e-155">[Log Analytics의 로그 검색](log-analytics-log-search-new.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="18f8e-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="18f8e-156">[Microsoft Flow](https://ms.flow.microsoft.com)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="18f8e-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



