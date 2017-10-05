---
title: "시나리오 - Azure 서버를 사용하지 않고 Customer Insights 대시보드 만들기 | Microsoft Docs"
description: "Azure Logic Apps 및 Azure Functions를 사용하여 고객 피드백, 소셜 데이터 등을 관리하는 대시보드를 구축할 수 있는 방법의 예입니다."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: 0b6e118cb13ab8185d8eeb42bec6147155967967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="20196-103">Azure Logic Apps 및 Azure Functions를 사용하여 실시간 Customer Insights 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="20196-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="20196-104">Azure 서버를 사용하지 않는 도구는 인프라에 대한 염려 없이 클라우드에서 응용 프로그램을 빠르게 구축하고 호스팅하는 강력한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="20196-105">이 시나리오에서는 고객 피드백을 트리거하고 기계 학습으로 피드백을 분석하고 Power BI 또는 Azure Data Lake와 같은 원본 정보를 게시하는 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20196-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="20196-106">시나리오 및 사용하는 도구 개요</span><span class="sxs-lookup"><span data-stu-id="20196-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="20196-107">이 솔루션을 구현하기 위해 Azure에서 서버를 사용하지 않는 앱의 두 개의 주요 구성 요소인 [Azure Functions](https://azure.microsoft.com/services/functions/) 및 [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="20196-108">Logic Apps는 클라우드에서 서버를 사용하지 않는 워크플로 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="20196-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="20196-109">서버가 없는 구성 요소에 오케스트레이션을 제공하고 100개 이상의 서비스 및 API에도 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="20196-110">이 시나리오에서는 고객의 피드백을 트리거하기 위한 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20196-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="20196-111">고객 피드백에 응답하는 데 도움이 되는 일부 커넥터는 [웹 형식에서](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/) Outlook.com, Office 365, Survey Monkey, Twitter 및 HTTP 요청을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="20196-112">아래 워크플로의 경우 Twitter에 대한 해시 태그를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="20196-113">함수는 클라우드에서 서버를 사용하지 않는 계산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="20196-114">이 시나리오에서는 일련의 미리 정의된 키워드에 따라 고객의 트윗을 플래그 지정하기 위해 Azure Functions를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="20196-115">전체 솔루션은 [Visual Studio에서 작성](logic-apps-deploy-from-vs.md) 및 [리소스 템플릿의 일부분으로 배포](logic-apps-create-deploy-template.md)될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="20196-116">[Channel 9에](http://aka.ms/logicappsdemo) 시나리오의 연습 동영상이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="20196-117">고객 데이터를 트리거하는 논리 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="20196-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="20196-118">Visual Studio 또는 Azure Portal에서 [논리 앱을 만든](logic-apps-create-a-logic-app.md) 후:</span><span class="sxs-lookup"><span data-stu-id="20196-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="20196-119">Twitter에서 **새 트윗**에 대한 트리거 추가</span><span class="sxs-lookup"><span data-stu-id="20196-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="20196-120">키워드 또는 해시 태그에 대한 트윗을 수신하도록 트리거를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="20196-121">트리거에 대한 되풀이 속성이 논리 앱이 폴링 기반 트리거에 대한 새 항목을 확인하는 주기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Twitter 트리거의 예][1]

<span data-ttu-id="20196-123">이 앱은 이제 모든 새 트윗에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="20196-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="20196-124">그런 다음 해당 트윗 데이터를 가져오고 더 자세한 데이터 표현을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="20196-125">이를 위해 [Azure 인식 서비스](https://azure.microsoft.com/services/cognitive-services/)를 사용하여 텍스트의 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="20196-126">**새 단계** 클릭</span><span class="sxs-lookup"><span data-stu-id="20196-126">Click **New Step**</span></span>
1. <span data-ttu-id="20196-127">**텍스트 분석** 커넥터 선택 또는 검색</span><span class="sxs-lookup"><span data-stu-id="20196-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="20196-128">**데이터 감지** 작업 선택</span><span class="sxs-lookup"><span data-stu-id="20196-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="20196-129">메시지가 나타나는 경우 텍스트 분석 서비스에 대한 올바른 Cognitive Services 키 제공</span><span class="sxs-lookup"><span data-stu-id="20196-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="20196-130">분석할 텍스트로 **트윗 텍스트**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="20196-131">이제 트윗에 대한 트윗 데이터 및 정보가 있으므로 다양한 다른 커넥터가 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="20196-132">Power BI - 스트리밍 데이터 집합에 행 추가: 보Power BI 대시보드에서 실시간으로 트윗을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="20196-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="20196-133">Azure Data Lake - 파일 추가: 분석 작업에 포함할 Azure Data Lake 데이터 집합에 고객 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="20196-134">SQL - 행 추가: 나중의 검색을 위해 데이터베이스에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="20196-135">Slack - 메시지 보내기: 작업을 필요로 하는 부정적인 피드백에 대한 Slack 채널을 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="20196-136">Azure 함수는 데이터 외에 더 많은 사용자 지정 계산을 수행하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="20196-137">Azure 함수를 사용하여 데이터 보강</span><span class="sxs-lookup"><span data-stu-id="20196-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="20196-138">함수를 만들려면 먼저 Azure 구독에 함수 앱이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="20196-139">포털에서 Azure 함수를 만드는 자세한 내용은 [여기에서 찾을 수](../azure-functions/functions-create-first-azure-function-azure-portal.md) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="20196-140">논리 앱에서 직접 호출될 함수의 경우 HTTP 트리거 바인딩이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="20196-141">**HttpTrigger** 템플릿을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="20196-142">이 시나리오에서 Azure 함수의 요청 본문은 트윗 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="20196-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="20196-143">함수 코드에서 단순히 트윗 텍스트가 키워드 또는 구를 포함하는 경우에 대한 논리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="20196-144">함수 자체는 시나리오의 필요에 따라 간단하거나 복잡하게 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="20196-145">함수 끝에서 일부 데이터로 논리 앱에 대한 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="20196-146">간단한 부울 값(예: `containsKeyword`) 또는 복잡한 개체일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![구성된 Azure 함수 단계][2]

> [!TIP]
> <span data-ttu-id="20196-148">논리 앱의 함수에서 복잡한 응답에 액세스할 때 JSON 구문 분석 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="20196-149">함수가 저장된 후 위에서 만든 논리 앱에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="20196-150">논리 앱에서:</span><span class="sxs-lookup"><span data-stu-id="20196-150">In the logic app:</span></span>

1. <span data-ttu-id="20196-151">**새 단계**를 클릭하여 추가</span><span class="sxs-lookup"><span data-stu-id="20196-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="20196-152">**Azure Functions** 커넥터 선택</span><span class="sxs-lookup"><span data-stu-id="20196-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="20196-153">기존 함수를 선택하고 만든 함수로 이동하려면 선택</span><span class="sxs-lookup"><span data-stu-id="20196-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="20196-154">**요청 본문**에 대한 **트윗 텍스트**에 전송</span><span class="sxs-lookup"><span data-stu-id="20196-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="20196-155">솔루션 실행 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="20196-155">Running and monitoring the solution</span></span>

<span data-ttu-id="20196-156">Logic Apps에서 서버를 사용하지 않는 오케스트레이션 제작의 이점 중 하나는 풍부한 디버그와 모니터링 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="20196-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="20196-157">Visual Studio, Azure Portal 내에서 또는 REST API 및 SDK를 통해 모든 실행(현재 또는 기록)을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="20196-158">논리 앱을 테스트하는 가장 쉬운 방법 중 하나는 디자이너에서 **실행** 단추를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20196-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="20196-159">**실행**을 클릭하면 이벤트가 감지될 때까지 5초마다 트리거 폴링이 계속되고 실행이 진행됨에 따라 라이브 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="20196-160">Azure Portal의 개요 블레이드 또는 Visual Studio 클라우드 탐색기를 사용하여 이전 실행 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="20196-161">자동화된 배포를 위한 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="20196-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="20196-162">솔루션이 개발되었으므로 Azure 배포 템플릿을 통해 전 세계 모든 Azure 지역에 캡처 및 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="20196-163">이 워크플로의 다양한 버전에 대한 매개 변수 수정뿐만 아니라 빌드 및 릴리스 파이프라인에서 이 솔루션을 통합하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="20196-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="20196-164">배포 템플릿 만들기에 대한 자세한 내용은 [이 문서에서](logic-apps-create-deploy-template.md) 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="20196-165">Azure Functions는 모든 종속성과 함께 전체 솔루션을 단일 템플릿으로 관리할 수 있도록 배포 템플릿에 통합될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="20196-166">함수 배포 템플릿의 예는 [Azure 빠른 시작 템플릿 리포지토리](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20196-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20196-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20196-167">Next steps</span></span>

* [<span data-ttu-id="20196-168">Azure Logic Apps 다른 예제 및 시나리오 참조</span><span class="sxs-lookup"><span data-stu-id="20196-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="20196-169">종단 간 이 솔루션을 만드는 연습 동영상 시청</span><span class="sxs-lookup"><span data-stu-id="20196-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="20196-170">논리 앱 내에서 예외를 처리 및 catch하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="20196-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png