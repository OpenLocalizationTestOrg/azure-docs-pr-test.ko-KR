---
title: "aaaAutomate Application Insights Azure 논리 앱을 사용 하 여 처리 합니다."
description: "Hello Application Insights 커넥터 tooyour 논리 앱을 추가 하 여 반복 가능한 프로세스 신속 하 게 자동화할 수 방법을 알아봅니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="43df5-103">Logic Apps를 사용하여 Application Insights 프로세스 자동화</span><span class="sxs-lookup"><span data-stu-id="43df5-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="43df5-104">반복 실행 hello 동일한 쿼리 원격 분석 데이터 toocheck 프로그램 서비스가 제대로 작동 하는지 여부를 사용자가 직접 하십니까?</span><span class="sxs-lookup"><span data-stu-id="43df5-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="43df5-105">다음 주위에 맞게 워크플로 작성 및 찾고 tooautomate 찾기 추세와 비정상 상태에 대해 이러한 쿼리는? 논리 앱에 대 한 hello Azure Application Insights 커넥터 (preview)는이 목적을 위해 hello 오른쪽 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="43df5-106">이 통합 덕분에 코드를 전혀 작성하지 않고도 수많은 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="43df5-107">논리 앱을 만들 수 있습니다 커넥터 tooquickly hello Application Insights로 모든 Application Insights 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="43df5-108">작업을 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-108">You can add additional actions as well.</span></span> <span data-ttu-id="43df5-109">Azure 앱 서비스의 hello 논리 앱 기능을 사용 하면 수백 가지 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="43df5-110">예를 들어 논리 앱을 사용하여 이메일 알림을 자동으로 보내거나 Visual Studio Team Services에서 버그를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="43df5-111">사용할 수도 있습니다 hello 중 사용 가능한 많은 [템플릿](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp hello 논리 앱을 만드는 과정을 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="43df5-112">Application Insights에 대한 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="43df5-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="43df5-113">이 자습서에서는 toocreate 분석 autocluster 알고리즘 toogroup hello를 사용 하는 논리 앱 특성 방식을 웹 응용 프로그램에 대 한 hello 데이터에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="43df5-114">hello 흐름 전자 메일, 예로, 사용 하는 방법을 응용 프로그램 통찰력 분석 및 논리 앱 함께 hello 결과 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="43df5-115">1단계: 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="43df5-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="43df5-116">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43df5-117">Hello에 **새로** 창 선택 **웹 + 모바일**를 선택한 후 **논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![새 논리 앱 창](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="43df5-119">2단계: 논리 앱에 대한 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="43df5-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="43df5-120">Hello에 **논리가 응용 프로그램 디자이너** 창 아래에서 **일반적인 트리거 시작**선택, **되풀이**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![논리 앱 디자이너 창](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="43df5-122">Hello에 **주파수** 상자 **일** 선택한 다음 hello **간격** 상자에 입력 합니다 **1**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![논리 앱 디자이너 "되풀이" 창](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="43df5-124">3단계: Application Insights 작업 추가</span><span class="sxs-lookup"><span data-stu-id="43df5-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="43df5-125">**새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="43df5-126">Hello에 **동작 선택** 검색 상자에서 **Azure Application Insights**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="43df5-127">**작업**에서 **Azure Application Insights – Analytics 쿼리 시각화 미리 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![논리 앱 디자이너 "작업 선택" 창](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="43df5-129">4 단계: tooan Application Insights 리소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="43df5-130">toocomplete이이 단계에서는 리소스에 대 한 응용 프로그램 ID와 API 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="43df5-131">Hello 다음 다이어그램에에서 나와 있는 것 처럼 hello Azure 포털에서에서 해당를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Hello Azure 포털에서에서 응용 프로그램 ID](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="43df5-133">연결, hello 응용 프로그램 ID 및 hello API 키에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![논리 앱 디자이너 흐름 연결 창](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="43df5-135">5 단계: hello 분석 쿼리 및 차트 종류를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="43df5-136">다음 예제는 hello, hello 쿼리 hello 마지막 날짜 내 hello 실패 요청을가 선택 하 고 상호 관련 시켜 hello 작업의 일부로 발생 하는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="43df5-137">분석은 hello operation_Id 식별자에 따라 hello 실패 요청을 연관 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="43df5-138">그런 다음 hello 쿼리 hello autocluster 알고리즘을 사용 하 여 hello 결과 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="43df5-139">사용자 고유의 쿼리를 만드는 경우를 정상적으로 작동 하는지 분석에서 tooyour 흐름 추가 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="43df5-140">Hello에 **쿼리** 상자 hello 다음 분석 쿼리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-140">In hello **Query** box, add hello following Analytics query:</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. <span data-ttu-id="43df5-141">Hello에 **차트 종류** 상자 **Html 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Analytics 쿼리 구성 창](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="43df5-143">6 단계: hello 논리 앱 toosend 전자 메일 구성</span><span class="sxs-lookup"><span data-stu-id="43df5-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="43df5-144">**새 단계**를 클릭한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="43df5-145">Hello 검색 상자에 입력 **Office 365 Outlook**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="43df5-146">**Office 365 Outlook - 이메일 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook 선택](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="43df5-148">Hello에 **전자 메일 보내기** 창에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="43df5-149">a.</span><span class="sxs-lookup"><span data-stu-id="43df5-149">a.</span></span> <span data-ttu-id="43df5-150">Hello 수신자의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="43df5-151">b.</span><span class="sxs-lookup"><span data-stu-id="43df5-151">b.</span></span> <span data-ttu-id="43df5-152">Hello 전자 메일의 제목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="43df5-153">c.</span><span class="sxs-lookup"><span data-stu-id="43df5-153">c.</span></span> <span data-ttu-id="43df5-154">Hello에서 아무 곳 이나 클릭 **본문** 상자를 선택한 다음 선택 hello 동적 콘텐츠 메뉴에서 hello 오른쪽에 열리는 **본문**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="43df5-155">d.</span><span class="sxs-lookup"><span data-stu-id="43df5-155">d.</span></span> <span data-ttu-id="43df5-156">**고급 옵션 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-156">Click **Show advanced options**.</span></span>

      ![Office 365 Outlook 구성](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="43df5-158">동적 콘텐츠 메뉴 hello에서 수행 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="43df5-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="43df5-159">a.</span><span class="sxs-lookup"><span data-stu-id="43df5-159">a.</span></span> <span data-ttu-id="43df5-160">**첨부 파일 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="43df5-161">b.</span><span class="sxs-lookup"><span data-stu-id="43df5-161">b.</span></span> <span data-ttu-id="43df5-162">**첨부 파일 콘텐츠**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="43df5-163">c.</span><span class="sxs-lookup"><span data-stu-id="43df5-163">c.</span></span> <span data-ttu-id="43df5-164">Hello에 **은 HTML** 상자 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Office 365 메일 구성 화면](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="43df5-166">7단계: 논리 앱 저장 및 테스트</span><span class="sxs-lookup"><span data-stu-id="43df5-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="43df5-167">클릭 **저장** toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="43df5-168">Hello 트리거 toorun hello 논리 앱을 기다릴 수 있습니다 또는 선택 하 여 hello 논리 앱을 즉시 실행할 수 있습니다 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![논리 앱 만들기 화면](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="43df5-170">논리 앱을 실행할 때 hello 전자 메일 목록에 지정 된 hello 받는 사람이 전자 메일을 다음과 같은 hello 받을:</span><span class="sxs-lookup"><span data-stu-id="43df5-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![논리 앱 이메일 메시지](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="43df5-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43df5-172">Next steps</span></span>

- <span data-ttu-id="43df5-173">[Analytics 쿼리](app-insights-analytics-using.md) 만들기에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="43df5-174">[Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="43df5-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





