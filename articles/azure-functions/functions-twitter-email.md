---
title: "Azure Logic Apps와 통합하는 함수 만들기 | Microsoft Docs"
description: "Azure Logic Apps 및 Azure Cognitive Services와 통합하는 함수를 만들어 트윗 감정을 분류하고 감정이 나쁠 경우 알림을 보냅니다."
services: functions, logic-apps, cognitive-services
keywords: "워크플로, 클라우드 앱, 클라우드 서비스, 비즈니스 프로세스, 시스템 통합, Enterprise Application Integration, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="77bac-104">Azure Logic Apps와 통합하는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="77bac-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="77bac-105">Azure Functions는 논리 앱 디자이너에서 Azure Logic Apps와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="77bac-106">이 통합을 통해 다른 Azure 및 타사 서비스와 함께 오케스트레이션에서 함수의 컴퓨팅 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="77bac-107">이 자습서에서는 Logic Apps 및 Azure Cognitive Services와 함께 함수를 사용하여 Twitter 게시물에서 감정을 분석하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="77bac-108">HTTP 트리거된 함수는 감정 점수를 기준으로 트윗을 녹색, 노랑 또는 빨강으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="77bac-109">불량 감정이 감지되면 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-109">An email is sent when poor sentiment is detected.</span></span> 

![논리 앱 디자이너에서 앱의 처음 2단계를 보여 주는 이미지](media/functions-twitter-email/designer1.png)

<span data-ttu-id="77bac-111">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77bac-112">Cognitive Services 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="77bac-113">트윗 감정을 분류하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="77bac-114">Twitter에 연결하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="77bac-115">논리 앱에 감정 검색을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="77bac-116">함수에 논리 앱을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="77bac-117">함수의 응답에 따라 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77bac-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="77bac-118">Prerequisites</span></span>

+ <span data-ttu-id="77bac-119">활성 [Twitter](https://twitter.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="77bac-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="77bac-120">[Outlook.com](https://outlook.com/) 계정(알림 전송용).</span><span class="sxs-lookup"><span data-stu-id="77bac-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="77bac-121">이 항목에서는 [Azure Portal에서 첫 번째 함수 만들기](functions-create-first-azure-function.md)에서 만든 리소스를 시작점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="77bac-122">아직 만들지 않았다면 지금 이러한 단계를 수행하여 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="77bac-123">Cognitive Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="77bac-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="77bac-124">Cognitive Services 계정은 모니터링되는 트윗의 감정을 검색하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="77bac-125">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="77bac-126">Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="77bac-127">**데이터 + 분석** > **Cognitive Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="77bac-128">그런 다음 테이블에 지정된 설정을 사용하고 약관에 동의하고 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Cognitive 계정 만들기 블레이드](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="77bac-130">설정</span><span class="sxs-lookup"><span data-stu-id="77bac-130">Setting</span></span>      |  <span data-ttu-id="77bac-131">제안 값</span><span class="sxs-lookup"><span data-stu-id="77bac-131">Suggested value</span></span>   | <span data-ttu-id="77bac-132">설명</span><span class="sxs-lookup"><span data-stu-id="77bac-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="77bac-133">**Name**</span><span class="sxs-lookup"><span data-stu-id="77bac-133">**Name**</span></span> | <span data-ttu-id="77bac-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="77bac-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="77bac-135">고유한 계정 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="77bac-136">**API 형식**</span><span class="sxs-lookup"><span data-stu-id="77bac-136">**API type**</span></span> | <span data-ttu-id="77bac-137">Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="77bac-137">Text Analytics API</span></span> | <span data-ttu-id="77bac-138">텍스트를 분석하는 데 사용되는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="77bac-139">**위치**:</span><span class="sxs-lookup"><span data-stu-id="77bac-139">**Location**</span></span> | <span data-ttu-id="77bac-140">미국 서부</span><span class="sxs-lookup"><span data-stu-id="77bac-140">West US</span></span> | <span data-ttu-id="77bac-141">현재 텍스트 분석은 **미국 서부**만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="77bac-142">**가격 책정 계층**</span><span class="sxs-lookup"><span data-stu-id="77bac-142">**Pricing tier**</span></span> | <span data-ttu-id="77bac-143">F0</span><span class="sxs-lookup"><span data-stu-id="77bac-143">F0</span></span> | <span data-ttu-id="77bac-144">가장 낮은 계층으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-144">Start with the lowest tier.</span></span> <span data-ttu-id="77bac-145">호출에서 실행하는 경우 더 높은 계층으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="77bac-146">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="77bac-146">**Resource group**</span></span> | <span data-ttu-id="77bac-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="77bac-147">myResourceGroup</span></span> | <span data-ttu-id="77bac-148">이 자습서에서 모든 서비스에 대해 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="77bac-149">**만들기**를 클릭하여 사용자의 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-149">Click **Create** to create your account.</span></span> <span data-ttu-id="77bac-150">계정이 만들어지면 대시보드에 고정된 새 Cognitive Services 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="77bac-151">계정에서 **키**를 클릭한 다음 **키1**의 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="77bac-152">이 키를 사용하여 논리 앱을 Cognitive Services 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![구성](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="77bac-154">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="77bac-154">Create the function</span></span>

<span data-ttu-id="77bac-155">함수는 논리 앱 워크플로에서 처리 작업을 오프로드하는 훌륭한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="77bac-156">이 자습서는 HTTP 트리거된 함수를 사용하여 Cognitive Services에서 트윗 감정 점수를 처리하고 범주 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="77bac-157">함수 앱을 확장하고 **함수** 옆에 있는 **+** 단추를 클릭하고 **HTTPTrigger** 템플릿을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="77bac-158">함수 **이름**에 `CategorizeSentiment`를 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![함수 앱 블레이드, 함수 +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="77bac-160">run.csx 파일 내용을 다음 코드로 바꾼 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="77bac-161">이 함수 코드는 요청에서 받은 감정 점수를 기준으로 색 범주를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="77bac-162">함수를 테스트하려면 오른쪽 끝의 **테스트**를 클릭하여 테스트 탭을 확장합니다. **요청 본문**에 `0.2` 값을 입력한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="77bac-163">응답의 본문에 **빨강** 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![Azure Portal에서 함수 테스트](./media/functions-twitter-email/test.png)

<span data-ttu-id="77bac-165">이제 감정 점수를 분류하는 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="77bac-166">다음으로 Twitter 및 Cognitive Services 계정과 함수를 통합하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="77bac-167">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="77bac-167">Create a logic app</span></span>   

1. <span data-ttu-id="77bac-168">Azure Portal에서 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="77bac-169">**엔터프라이즈 통합** > **논리 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="77bac-170">그런 다음 테이블에 지정된 설정을 사용하고 **대시보드에 고정**을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="77bac-171">그런 다음 `TweetSentiment`와 같이 **이름**을 입력하고 테이블에 지정된 설정을 사용하고 약관에 동의하고 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Azure Portal에서 논리 앱 만들기](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="77bac-173">설정</span><span class="sxs-lookup"><span data-stu-id="77bac-173">Setting</span></span>      |  <span data-ttu-id="77bac-174">제안 값</span><span class="sxs-lookup"><span data-stu-id="77bac-174">Suggested value</span></span>   | <span data-ttu-id="77bac-175">설명</span><span class="sxs-lookup"><span data-stu-id="77bac-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="77bac-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="77bac-176">**Name**</span></span> | <span data-ttu-id="77bac-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="77bac-177">TweetSentiment</span></span> | <span data-ttu-id="77bac-178">앱에 적절한 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="77bac-179">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="77bac-179">**Resource group**</span></span> | <span data-ttu-id="77bac-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="77bac-180">myResourceGroup</span></span> | <span data-ttu-id="77bac-181">텍스트를 분석하는 데 사용되는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="77bac-182">**위치**:</span><span class="sxs-lookup"><span data-stu-id="77bac-182">**Location**</span></span> | <span data-ttu-id="77bac-183">미국 동부</span><span class="sxs-lookup"><span data-stu-id="77bac-183">East US</span></span> | <span data-ttu-id="77bac-184">가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="77bac-185">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="77bac-185">**Resource group**</span></span> | <span data-ttu-id="77bac-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="77bac-186">myResourceGroup</span></span> | <span data-ttu-id="77bac-187">이전과 동일한 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="77bac-188">**만들기**를 클릭하여 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="77bac-189">앱이 만들어지면 대시보드에 고정된 새 논리 앱을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="77bac-190">그런 다음 논리 앱 디자이너에서 아래로 스크롤하고 **빈 논리 앱** 템플릿을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![빈 논리 앱 템플릿](media/functions-twitter-email/blank.png)

<span data-ttu-id="77bac-192">이제 논리 앱 디자이너를 사용하여 앱 서비스 및 트리거를 앱에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="77bac-193">Twitter에 연결</span><span class="sxs-lookup"><span data-stu-id="77bac-193">Connect to Twitter</span></span>

<span data-ttu-id="77bac-194">먼저 Twitter 계정에 대한 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="77bac-195">논리 앱은 앱이 실행되도록 트리거하는 트윗에 대해 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="77bac-196">디자이너에서 **Twitter** 서비스를 클릭하고 **새 트윗이 게시된 경우** 트리거를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="77bac-197">Twitter 계정에 로그인하고 계정을 사용하도록 Logic Apps에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="77bac-198">표에 지정된 것처럼 Twitter 트리거 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Twitter 커넥터 설정](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="77bac-200">설정</span><span class="sxs-lookup"><span data-stu-id="77bac-200">Setting</span></span>      |  <span data-ttu-id="77bac-201">제안 값</span><span class="sxs-lookup"><span data-stu-id="77bac-201">Suggested value</span></span>   | <span data-ttu-id="77bac-202">설명</span><span class="sxs-lookup"><span data-stu-id="77bac-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="77bac-203">**검색 텍스트**</span><span class="sxs-lookup"><span data-stu-id="77bac-203">**Search text**</span></span> | <span data-ttu-id="77bac-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="77bac-204">#Azure</span></span> | <span data-ttu-id="77bac-205">선택한 간격에서 새 트윗을 생성하는 데 많이 사용되는 해시태그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="77bac-206">무료 계층을 사용하고 사용자 해시태그가 너무 많이 사용되면 Cognitive Services 계정에서 트랜잭션을 신속하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="77bac-207">**Frequency(빈도)**</span><span class="sxs-lookup"><span data-stu-id="77bac-207">**Frequency**</span></span> | <span data-ttu-id="77bac-208">분</span><span class="sxs-lookup"><span data-stu-id="77bac-208">Minute</span></span> | <span data-ttu-id="77bac-209">Twitter 폴링에 사용되는 빈도 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="77bac-210">**간격**</span><span class="sxs-lookup"><span data-stu-id="77bac-210">**Interval**</span></span> | <span data-ttu-id="77bac-211">15</span><span class="sxs-lookup"><span data-stu-id="77bac-211">15</span></span> | <span data-ttu-id="77bac-212">빈도 단위에서 Twitter 요청 간 경과된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="77bac-213">**저장**을 클릭하여 Twitter 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="77bac-214">이제 앱이 Twitter에 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="77bac-215">다음으로 텍스트 분석에 연결하여 수집된 트윗의 감정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="77bac-216">감정 검색 추가</span><span class="sxs-lookup"><span data-stu-id="77bac-216">Add sentiment detection</span></span>

1. <span data-ttu-id="77bac-217">**새 단계**를 클릭한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-217">Click **New Step**, and then **Add an action**.</span></span>

    ![새 단계 후 작업 추가](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="77bac-219">**작업 선택**에서 **텍스트 분석**을 클릭한 다음 **감정 검색** 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![감정 검색](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="77bac-221">`MyCognitiveServicesConnection`과 같은 연결 이름을 입력하고 Cognitive Services 계정에 저장한 키를 붙여 넣고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="77bac-222">**분석할 텍스트** > **트윗 텍스트**를 클릭한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![감정 검색](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="77bac-224">감정 검색을 구성했으므로 감정 점수 출력을 사용하는 함수에 연결을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="77bac-225">함수에 감정 출력 연결</span><span class="sxs-lookup"><span data-stu-id="77bac-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="77bac-226">논리 앱 디자이너에서 **새 단계** > **작업 추가**를 클릭한 다음 **Azure Functions**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="77bac-227">**Azure 함수 선택**을 클릭하고 앞에서 만든 **CategorizeSentiment** 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Azure 함수 선택을 보여 주는 Azure 함수 상자](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="77bac-229">**요청 본문**에서 **점수**, **저장**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="77bac-231">이제 논리 앱에서 감정 점수를 보낼 때 함수가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="77bac-232">색으로 지정된 범주는 함수에 의해 논리 앱에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="77bac-233">다음으로 **빨강** 감정 값이 함수에서 반환될 때 전송되는 전자 메일 알림을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="77bac-234">전자 메일 알림 추가</span><span class="sxs-lookup"><span data-stu-id="77bac-234">Add email notifications</span></span>

<span data-ttu-id="77bac-235">워크플로의 마지막 부분은 감정이 _빨강_으로 점수가 매겨질 때 전자 메일을 트리거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="77bac-236">이 항목에서는 Outlook.com 커넥터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="77bac-237">비슷한 단계를 수행하여 Gmail 또는 Office 365 Outlook 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="77bac-238">논리 앱 디자이너에서 **새 단계** > **조건 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="77bac-239">**값 선택**을 클릭한 다음 **본문**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="77bac-240">**같음**을 선택하고 **값 선택**을 클릭하고 `RED`를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![논리 앱에 조건을 추가합니다.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="77bac-242">**예인 경우 아무 작업도 수행하지 않습니다**에서 **작업 추가**를 클릭하고 `outlook.com`을 검색하고 **전자 메일 보내기**를 클릭하고 Outlook.com 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![조건에 대한 작업을 선택합니다.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="77bac-244">Outlook.com 계정이 없는 경우 Gmail 또는 Office 365 Outlook과 같은 다른 커넥터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="77bac-245">**전자 메일 보내기** 작업에서 테이블에 지정된 대로 전자 메일 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![전자 메일 보내기 작업에 대한 전자 메일을 구성합니다.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="77bac-247">설정</span><span class="sxs-lookup"><span data-stu-id="77bac-247">Setting</span></span>      |  <span data-ttu-id="77bac-248">제안 값</span><span class="sxs-lookup"><span data-stu-id="77bac-248">Suggested value</span></span>   | <span data-ttu-id="77bac-249">설명</span><span class="sxs-lookup"><span data-stu-id="77bac-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="77bac-250">**To**</span><span class="sxs-lookup"><span data-stu-id="77bac-250">**To**</span></span> | <span data-ttu-id="77bac-251">메일 주소 입력</span><span class="sxs-lookup"><span data-stu-id="77bac-251">Type your email address</span></span> | <span data-ttu-id="77bac-252">알림을 받는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="77bac-253">**제목**</span><span class="sxs-lookup"><span data-stu-id="77bac-253">**Subject**</span></span> | <span data-ttu-id="77bac-254">부정적인 트윗 감정 검색</span><span class="sxs-lookup"><span data-stu-id="77bac-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="77bac-255">전자 메일 알림의 제목 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="77bac-256">**본문**</span><span class="sxs-lookup"><span data-stu-id="77bac-256">**Body**</span></span> | <span data-ttu-id="77bac-257">트윗 텍스트, 위치</span><span class="sxs-lookup"><span data-stu-id="77bac-257">Tweet text, Location</span></span> | <span data-ttu-id="77bac-258">**트윗 텍스트** 및 **위치** 매개 변수를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="77bac-259">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-259">Click **Save**.</span></span>

<span data-ttu-id="77bac-260">이제 워크플로를 완료했으므로 논리 앱을 활성화하고 작업 시 함수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="77bac-261">워크플로 테스트</span><span class="sxs-lookup"><span data-stu-id="77bac-261">Test the workflow</span></span>

1. <span data-ttu-id="77bac-262">논리 앱 디자이너에서 **실행**을 클릭하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="77bac-263">왼쪽 열에서 **개요**를 클릭하여 논리 앱의 상태를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![논리 앱 실행 상태](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="77bac-265">(선택 사항) 실행 중 하나를 클릭하여 실행의 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="77bac-266">함수로 이동하고 로그를 보고 감정 값이 수신 및 처리되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![함수 로그 보기](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="77bac-268">잠재적으로 부정적인 감정이 검색되면 전자 메일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="77bac-269">전자 메일을 수신하지 않은 경우 항상 빨강을 반환하도록 함수 코드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="77bac-270">전자 메일 알림을 확인한 후 원래 코드로 다시 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="77bac-271">이 자습서를 완료 한 후 논리 앱을 비활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="77bac-272">앱을 비활성화하여 Cognitive Services 계정에서 실행에 대한 요금 부과 및 트랜잭션 소모를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="77bac-273">이제 Logic Apps 워크플로로 함수를 통합하는 것이 얼마나 쉬운지 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="77bac-274">논리 앱 비활성화</span><span class="sxs-lookup"><span data-stu-id="77bac-274">Disable the logic app</span></span>

<span data-ttu-id="77bac-275">논리 앱을 비활성화하려면 **개요** 클릭한 다음 화면 맨 위의 **비활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="77bac-276">그러면 앱을 삭제하지 않고 논리 앱의 실행 및 요금 청구를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![함수 로그](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="77bac-278">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77bac-278">Next steps</span></span>

<span data-ttu-id="77bac-279">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77bac-280">Cognitive Services 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="77bac-281">트윗 감정을 분류하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="77bac-282">Twitter에 연결하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="77bac-283">논리 앱에 감정 검색을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="77bac-284">함수에 논리 앱을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="77bac-285">함수의 응답에 따라 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="77bac-286">함수에 대한 서버 없는 API를 만드는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="77bac-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="77bac-287">Azure Functions를 사용하여 서버 없는 API 만들기</span><span class="sxs-lookup"><span data-stu-id="77bac-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="77bac-288">Logic Apps에 대해 자세히 알아보려면 [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77bac-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

