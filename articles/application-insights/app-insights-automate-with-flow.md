---
title: "Microsoft Flow를 사용하여 Azure Application Insights 프로세스 자동화"
description: "Microsoft Flow를 통해 Application Insights 커넥터를 사용하여 반복 가능한 프로세스를 신속하게 자동화하는 방법을 알아봅니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="50257-103">Microsoft Flow용 커넥터를 사용하여 Azure Application Insights 프로세스 자동화</span><span class="sxs-lookup"><span data-stu-id="50257-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="50257-104">서비스가 제대로 작동하는지 확인하기 위해 원격 분석 데이터에 대해 같은 쿼리를 반복적으로 실행하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="50257-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="50257-105">추세와 비정상을 찾기 위해 이러한 쿼리를 자동화하고 여기에 관련된 고유한 워크플로를 빌드하기를 원하나요?</span><span class="sxs-lookup"><span data-stu-id="50257-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="50257-106">Microsoft Flow용 Azure Application Insights 커넥터(미리 보기)가 이러한 용도에 적합한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="50257-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="50257-107">이 통합 덕분에 이제 코드 한 줄 작성하지 않고도 수많은 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="50257-108">Application Insights 작업을 사용하여 흐름을 만들고 나면 이 흐름에서 Application Insights Analytics 쿼리가 자동으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="50257-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="50257-109">작업을 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-109">You can add additional actions as well.</span></span> <span data-ttu-id="50257-110">Microsoft Flow는 수백 개의 작업을 사용할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="50257-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="50257-111">예를 들어 Microsoft Flow를 사용하여 자동으로 메일 알림을 보내거나 Visual Studio Team Services에서 버그를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="50257-112">Microsoft Flow용 커넥터에 사용할 수 있는 많은 [템플릿](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="50257-113">이러한 템플릿을 사용하면 흐름 만들기 프로세스를 빠르게 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="50257-114">Application Insights 흐름 만들기</span><span class="sxs-lookup"><span data-stu-id="50257-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="50257-115">이 자습서에서는 Analytics autocluster 알고리즘을 사용하여 웹 응용 프로그램에 대한 데이터에서 특성을 그룹화하는 흐름을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="50257-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="50257-116">흐름은 자동으로 메일을 통해 결과를 보내며, 이는 Microsoft Flow 및 Application Insights Analytics를 함께 사용하는 방법의 한 가지 예일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="50257-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="50257-117">1단계: 흐름 만들기</span><span class="sxs-lookup"><span data-stu-id="50257-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="50257-118">[Microsoft Flow](http://flow.microsoft.com)에 로그인한 다음 **My Flows**(내 흐름)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="50257-119">**빈 곳에서 흐름 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="50257-120">2단계: 흐름에 대한 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="50257-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="50257-121">**일정**을 선택한 다음, **일정 - 되풀이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="50257-122">**빈도** 상자에서 **일**을 선택하고 **간격** 상자에 **1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Microsoft Flow 트리거 대화 상자](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="50257-124">3단계: Application Insights 작업 추가</span><span class="sxs-lookup"><span data-stu-id="50257-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="50257-125">**새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="50257-126">**Azure Application Insights**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="50257-127">**Azure Application Insights – Analytics 쿼리 시각화 미리 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Analytics 쿼리 실행 창](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="50257-129">4단계: Application Insights 리소스에 연결</span><span class="sxs-lookup"><span data-stu-id="50257-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="50257-130">이 단계를 완료하려면 리소스의 응용 프로그램 ID 및 API 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="50257-131">다음 다이어그램에 표시된 것처럼 Azure Portal에서 리소스의 응용 프로그램 ID 및 API 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Azure Portal의 응용 프로그램 ID](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="50257-133">응용 프로그램 ID 및 API 키와 함께 연결의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Microsoft Flow 연결 창](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="50257-135">5단계: Analytics 쿼리 및 차트 종류 지정</span><span class="sxs-lookup"><span data-stu-id="50257-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="50257-136">이 예제 쿼리에서는 어제 중에 실패한 요청을 선택하여 작업의 일부로 발생한 예외와 상관 관계를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="50257-137">Analytics에서는 operation_Id 식별자를 기반으로 하여 상관 관계를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="50257-138">그런 다음 쿼리는 autocluster 알고리즘을 사용하여 결과를 세그먼트화합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="50257-139">사용자 고유의 쿼리를 만드는 경우 이러한 쿼리를 흐름에 추가하기 전에 먼저 Analytics에서 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="50257-140">다음 Analytics 쿼리를 추가하고 HTML 테이블 차트 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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
    
    ![Analytics 쿼리 구성 창](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="50257-142">6단계: 메일을 보내도록 흐름 구성</span><span class="sxs-lookup"><span data-stu-id="50257-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="50257-143">**새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="50257-144">**Office 365 Outlook**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="50257-145">**Office 365 Outlook – 메일 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook 선택 창](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="50257-147">**메일 보내기** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="50257-148">a.</span><span class="sxs-lookup"><span data-stu-id="50257-148">a.</span></span> <span data-ttu-id="50257-149">받는 사람의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="50257-150">b.</span><span class="sxs-lookup"><span data-stu-id="50257-150">b.</span></span> <span data-ttu-id="50257-151">이메일의 제목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-151">Type a subject for the email.</span></span>

   <span data-ttu-id="50257-152">c.</span><span class="sxs-lookup"><span data-stu-id="50257-152">c.</span></span> <span data-ttu-id="50257-153">**본문** 상자의 임의의 위치를 클릭한 다음, 오른쪽에서 열리는 동적 콘텐츠 메뉴에서 **본문**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="50257-154">d.</span><span class="sxs-lookup"><span data-stu-id="50257-154">d.</span></span> <span data-ttu-id="50257-155">**고급 옵션 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-155">Click **Show advanced options**.</span></span>

    ![Office 365 Outlook 구성](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="50257-157">동적 콘텐츠 메뉴에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="50257-158">a.</span><span class="sxs-lookup"><span data-stu-id="50257-158">a.</span></span> <span data-ttu-id="50257-159">**첨부 파일 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="50257-160">b.</span><span class="sxs-lookup"><span data-stu-id="50257-160">b.</span></span> <span data-ttu-id="50257-161">**첨부 파일 콘텐츠**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="50257-162">c.</span><span class="sxs-lookup"><span data-stu-id="50257-162">c.</span></span> <span data-ttu-id="50257-163">**HTML임** 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Office 365 메일 구성 창](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="50257-165">7단계: 흐름 저장 및 테스트</span><span class="sxs-lookup"><span data-stu-id="50257-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="50257-166">**흐름 이름** 상자에 흐름 이름을 추가하고 **흐름 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50257-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![흐름 만들기 창](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="50257-168">트리거가 이 작업을 실행하도록 기다리거나 [요청 시 트리거를 실행](https://flow.microsoft.com/blog/run-now-and-six-more-services/)하여 흐름을 즉시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="50257-169">흐름이 실행되면 메일 목록에 지정한 받는 사람이 다음과 같은 메일 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="50257-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![샘플 메일](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="50257-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50257-171">Next steps</span></span>

- <span data-ttu-id="50257-172">[Analytics 쿼리](app-insights-analytics-using.md) 만들기에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="50257-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="50257-173">[Microsoft Flow](https://ms.flow.microsoft.com)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="50257-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





