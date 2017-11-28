---
title: "Azure 논리 앱에 통합 하는 함수 aaaCreate | Microsoft Docs"
description: "Azure 논리 앱 및 Azure Cognitive 서비스 toocategorize 윗 의미와 통합 하는 함수를 만들고 감성 나쁘지 경우 알림을 보내도록 합니다."
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
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="764aa-104">Azure Logic Apps와 통합하는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="764aa-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="764aa-105">Azure 논리 앱 azure 함수 hello 논리 앱 디자이너에에서 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="764aa-106">이러한 통합에는 오케스트레이션에 서 다른 Azure 및 타사 서비스와 함수의 컴퓨팅 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="764aa-107">이 자습서에서는 toouse Twitter 게시물에서 논리 앱 및 Azure Cognitive 서비스 tooanalyze 의미와 어떻게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="764aa-108">트리거된 HTTP 함수 트 윗 녹색, 노랑 또는 빨강 hello 감성 점수를 기준으로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="764aa-109">불량 감정이 감지되면 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-109">An email is sent when poor sentiment is detected.</span></span> 

![논리 앱 디자이너에서 앱의 처음 2단계를 보여 주는 이미지](media/functions-twitter-email/designer1.png)

<span data-ttu-id="764aa-111">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="764aa-112">Cognitive Services 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="764aa-113">트윗 감정을 분류하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="764aa-114">TooTwitter 연결 하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="764aa-115">감성 검색 toohello 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="764aa-116">Hello 논리 앱 toohello 함수를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="764aa-117">Hello 함수에서 hello 응답에 따라 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="764aa-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="764aa-118">Prerequisites</span></span>

+ <span data-ttu-id="764aa-119">활성 [Twitter](https://twitter.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="764aa-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="764aa-120">[Outlook.com](https://outlook.com/) 계정(알림 전송용).</span><span class="sxs-lookup"><span data-stu-id="764aa-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="764aa-121">이 항목에서 만든의 시작 지점 hello 자원으로 사용 하 여 [hello Azure 포털에서에서 첫 번째 사용자 함수를 만들어](functions-create-first-azure-function.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="764aa-122">그렇게 이미 하지 않은 경우 이러한 단계 지금 toocreate 함수 앱을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="764aa-123">Cognitive Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="764aa-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="764aa-124">Cognitive 서비스 계정은 모니터링 되는 트 윗의 필요한 toodetect hello 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="764aa-125">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="764aa-126">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="764aa-127">**데이터 + 분석** > **Cognitive Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="764aa-128">그런 다음 hello 설정으로 사용 hello 테이블에 지정 된 hello 조건에 동의 하 고 확인 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Cognitive 계정 만들기 블레이드](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="764aa-130">설정</span><span class="sxs-lookup"><span data-stu-id="764aa-130">Setting</span></span>      |  <span data-ttu-id="764aa-131">제안 값</span><span class="sxs-lookup"><span data-stu-id="764aa-131">Suggested value</span></span>   | <span data-ttu-id="764aa-132">설명</span><span class="sxs-lookup"><span data-stu-id="764aa-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="764aa-133">**Name**</span><span class="sxs-lookup"><span data-stu-id="764aa-133">**Name**</span></span> | <span data-ttu-id="764aa-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="764aa-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="764aa-135">고유한 계정 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="764aa-136">**API 형식**</span><span class="sxs-lookup"><span data-stu-id="764aa-136">**API type**</span></span> | <span data-ttu-id="764aa-137">Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="764aa-137">Text Analytics API</span></span> | <span data-ttu-id="764aa-138">API는 tooanalyze 텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="764aa-139">**위치**:</span><span class="sxs-lookup"><span data-stu-id="764aa-139">**Location**</span></span> | <span data-ttu-id="764aa-140">미국 서부</span><span class="sxs-lookup"><span data-stu-id="764aa-140">West US</span></span> | <span data-ttu-id="764aa-141">현재 텍스트 분석은 **미국 서부**만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="764aa-142">**가격 책정 계층**</span><span class="sxs-lookup"><span data-stu-id="764aa-142">**Pricing tier**</span></span> | <span data-ttu-id="764aa-143">F0</span><span class="sxs-lookup"><span data-stu-id="764aa-143">F0</span></span> | <span data-ttu-id="764aa-144">가장 낮은 계층 hello로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-144">Start with hello lowest tier.</span></span> <span data-ttu-id="764aa-145">호출 부족 하면 tooa 상위 계층의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="764aa-146">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="764aa-146">**Resource group**</span></span> | <span data-ttu-id="764aa-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="764aa-147">myResourceGroup</span></span> | <span data-ttu-id="764aa-148">사용 하 여 hello 동일이 자습서의 모든 서비스에 대 한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="764aa-149">클릭 **만들기** toocreate 계정.</span><span class="sxs-lookup"><span data-stu-id="764aa-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="764aa-150">Hello 계정을 만든 후 새 Cognitive 서비스 계정 toohello 고정 된 대시보드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="764aa-151">Hello 계정에서 클릭 **키**의 hello 값을 복사 하 고 **키 1** 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="764aa-152">이 키 tooconnect hello 논리 앱 tooyour Cognitive 서비스 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![구성](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="764aa-154">Hello 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="764aa-154">Create hello function</span></span>

<span data-ttu-id="764aa-155">함수는 좋은 방법 toooffload 논리 앱 워크플로 처리 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="764aa-156">이 자습서에서는 트리거된 HTTP 함수 tooprocess 윗 감성에서 점수를 인식 서비스 및 범주 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="764aa-157">함수 앱 확장을 hello 클릭  **+**  너무 단추 옆**함수**, hello 클릭 **HTTPTrigger** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="764aa-158">형식 `CategorizeSentiment` hello 함수에 대 한 **이름** 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![함수 앱 블레이드, 함수 +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="764aa-160">Hello run.csx 파일의 내용을 hello hello 코드를 다음으로 대체 한 다음 클릭 **저장**:</span><span class="sxs-lookup"><span data-stu-id="764aa-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
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
    <span data-ttu-id="764aa-161">이 함수 코드 hello 요청에서 받은 hello 감성 점수를 기준으로 색 범주를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="764aa-162">tootest hello 함수 클릭 **테스트** hello 맨 오른쪽 tooexpand hello 테스트 탭에 있습니다. 값을 입력 `0.2` hello에 대 한 **요청 본문**, 클릭 하 고 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="764aa-163">값이 **빨간색** hello hello 응답 본문에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Hello Azure 포털의에서 테스트 hello 함수](./media/functions-twitter-email/test.png)

<span data-ttu-id="764aa-165">이제 감정 점수를 분류하는 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="764aa-166">다음으로 Twitter 및 Cognitive Services 계정과 함수를 통합하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="764aa-167">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="764aa-167">Create a logic app</span></span>   

1. <span data-ttu-id="764aa-168">Hello Azure 포털에서 클릭 hello **새로 만들기** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="764aa-169">**엔터프라이즈 통합** > **논리 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="764aa-170">그런 다음 확인 서 hello 설정 사용 hello 테이블에 지정 된 **Pin toodashboard**를 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="764aa-171">다음을 입력 한 **이름** 같은 `TweetSentiment`, hello 테이블에 지정 된 hello 설정을 사용 하 여 hello 조건에 동의 및 확인 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Hello Azure 포털에서에서 논리 앱 만들기](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="764aa-173">설정</span><span class="sxs-lookup"><span data-stu-id="764aa-173">Setting</span></span>      |  <span data-ttu-id="764aa-174">제안 값</span><span class="sxs-lookup"><span data-stu-id="764aa-174">Suggested value</span></span>   | <span data-ttu-id="764aa-175">설명</span><span class="sxs-lookup"><span data-stu-id="764aa-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="764aa-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="764aa-176">**Name**</span></span> | <span data-ttu-id="764aa-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="764aa-177">TweetSentiment</span></span> | <span data-ttu-id="764aa-178">앱에 적절한 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="764aa-179">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="764aa-179">**Resource group**</span></span> | <span data-ttu-id="764aa-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="764aa-180">myResourceGroup</span></span> | <span data-ttu-id="764aa-181">API는 tooanalyze 텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="764aa-182">**위치**:</span><span class="sxs-lookup"><span data-stu-id="764aa-182">**Location**</span></span> | <span data-ttu-id="764aa-183">미국 동부</span><span class="sxs-lookup"><span data-stu-id="764aa-183">East US</span></span> | <span data-ttu-id="764aa-184">위치 닫기 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="764aa-185">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="764aa-185">**Resource group**</span></span> | <span data-ttu-id="764aa-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="764aa-186">myResourceGroup</span></span> | <span data-ttu-id="764aa-187">선택 이전과 같은 기존 리소스 그룹 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="764aa-188">클릭 **만들기** toocreate 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="764aa-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="764aa-189">Hello 앱을 만든 후 새 논리 앱 toohello 고정 된 대시보드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="764aa-190">그런 다음 hello 논리 앱 디자이너에서에서 아래로 스크롤하여 하 고 hello 클릭 **빈 논리 앱** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="764aa-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![빈 논리 앱 템플릿](media/functions-twitter-email/blank.png)

<span data-ttu-id="764aa-192">이제 hello 논리 앱 디자이너 tooadd 서비스 및 트리거 tooyour 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="764aa-193">TooTwitter 연결</span><span class="sxs-lookup"><span data-stu-id="764aa-193">Connect tooTwitter</span></span>

<span data-ttu-id="764aa-194">먼저 연결 tooyour Twitter 계정 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="764aa-195">트 윗 hello 앱 toorun를 트리거하는 hello 논리 앱이 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="764aa-196">Hello 디자이너에서 클릭 hello **Twitter** 서비스를 마우스 클릭 hello **새 윗이 게시 될 때** 트리거.</span><span class="sxs-lookup"><span data-stu-id="764aa-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="764aa-197">Tooyour Twitter 계정에에서 로그인 하 고 논리 앱 toouse 사용자 계정에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="764aa-198">Hello 테이블에 지정 된 hello Twitter 트리거 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Twitter 커넥터 설정](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="764aa-200">설정</span><span class="sxs-lookup"><span data-stu-id="764aa-200">Setting</span></span>      |  <span data-ttu-id="764aa-201">제안 값</span><span class="sxs-lookup"><span data-stu-id="764aa-201">Suggested value</span></span>   | <span data-ttu-id="764aa-202">설명</span><span class="sxs-lookup"><span data-stu-id="764aa-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="764aa-203">**검색 텍스트**</span><span class="sxs-lookup"><span data-stu-id="764aa-203">**Search text**</span></span> | <span data-ttu-id="764aa-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="764aa-204">#Azure</span></span> | <span data-ttu-id="764aa-205">Hello 선택한 간격에 toogenerate 새 트 윗에 대 한 충분 한 인기 있는 hashtag를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="764aa-206">Hello 무료 계층 및 사용자 hashtag 사용 하 여 너무 많이 사용 되 면 사용할 수 있습니다 신속 하 게 hello 트랜잭션을 Cognitive 서비스 계정에서.</span><span class="sxs-lookup"><span data-stu-id="764aa-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="764aa-207">**Frequency(빈도)**</span><span class="sxs-lookup"><span data-stu-id="764aa-207">**Frequency**</span></span> | <span data-ttu-id="764aa-208">분</span><span class="sxs-lookup"><span data-stu-id="764aa-208">Minute</span></span> | <span data-ttu-id="764aa-209">Twitter 폴링에 사용 되는 hello 빈도 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="764aa-210">**간격**</span><span class="sxs-lookup"><span data-stu-id="764aa-210">**Interval**</span></span> | <span data-ttu-id="764aa-211">15</span><span class="sxs-lookup"><span data-stu-id="764aa-211">15</span></span> | <span data-ttu-id="764aa-212">빈도 단위에서 Twitter 요청 간에 경과 된 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="764aa-213">클릭 **저장** tooconnect tooyour Twitter 계정.</span><span class="sxs-lookup"><span data-stu-id="764aa-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="764aa-214">이제 앱에 연결 된 tooTwitter입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="764aa-215">다음으로, 수집 된 트 윗의 tootext 분석 toodetect hello 정서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="764aa-216">감정 검색 추가</span><span class="sxs-lookup"><span data-stu-id="764aa-216">Add sentiment detection</span></span>

1. <span data-ttu-id="764aa-217">**새 단계**를 클릭한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-217">Click **New Step**, and then **Add an action**.</span></span>

    ![새 단계 후 작업 추가](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="764aa-219">**동작 선택**, 클릭 **텍스트 분석**, hello를 클릭 한 다음 **감성 검색** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![감정 검색](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="764aa-221">같은 연결 이름을 입력 `MyCognitiveServicesConnection`Cognitive 서비스를 저장 하는 계정에 대 한 hello 키를 붙여 넣고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="764aa-222">클릭 **텍스트 tooanalyze** > **텍스트 윗**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![감정 검색](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="764aa-224">감성 검색을 구성 했으므로 hello 감성 점수가 출력을 사용 하는 연결 tooyour 함수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="764aa-225">연결 감성 출력 tooyour 함수</span><span class="sxs-lookup"><span data-stu-id="764aa-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="764aa-226">Hello 논리 앱 디자이너, 클릭 **새 단계** > **동작 추가**, 클릭 하 고 **Azure 함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="764aa-227">클릭 **Azure 함수 선택**선택, hello **CategorizeSentiment** 앞에서 만든 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Azure 함수 선택을 보여 주는 Azure 함수 상자](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="764aa-229">**요청 본문**에서 **점수**, **저장**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="764aa-231">이제 함수 hello 논리 앱에서 감성 점수를 전송할 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="764aa-232">색으로 구분 된 범주는 toohello 논리 앱 hello 함수에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="764aa-233">다음으로 감성 값 보내는 전자 메일 알림을 추가 **빨간색** hello 함수에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="764aa-234">전자 메일 알림 추가</span><span class="sxs-lookup"><span data-stu-id="764aa-234">Add email notifications</span></span>

<span data-ttu-id="764aa-235">hello 워크플로의 마지막 부분 hello hello 감성 점수로 때 tootrigger 전자 메일은 _빨간색_합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="764aa-236">이 항목에서는 Outlook.com 커넥터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="764aa-237">유사한 단계 toouse Gmail 또는 Office 365 Outlook 커넥터를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="764aa-238">논리 앱 디자이너 hello 클릭 **새 단계** > **조건 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="764aa-239">**값 선택**을 클릭한 다음 **본문**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="764aa-240">**같음**을 선택하고 **값 선택**을 클릭하고 `RED`를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![조건 toohello 논리 앱을 추가 합니다.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="764aa-242">**그러한 경우 아무 작업도 수행**, 클릭 **동작 추가**, 검색할 `outlook.com`, 클릭 **전자 메일 보내기**, tooyour Outlook.com 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Hello 조건에 대 한 작업을 선택 합니다.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="764aa-244">Outlook.com 계정이 없는 경우 Gmail 또는 Office 365 Outlook과 같은 다른 커넥터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="764aa-245">Hello에 **전자 메일 보내기** hello 테이블에 동작을 사용 하 여 hello 전자 메일 설정으로 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Hello 송신 전자 메일 작업에 대 한 hello 전자 메일을 구성 합니다.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="764aa-247">설정</span><span class="sxs-lookup"><span data-stu-id="764aa-247">Setting</span></span>      |  <span data-ttu-id="764aa-248">제안 값</span><span class="sxs-lookup"><span data-stu-id="764aa-248">Suggested value</span></span>   | <span data-ttu-id="764aa-249">설명</span><span class="sxs-lookup"><span data-stu-id="764aa-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="764aa-250">**To**</span><span class="sxs-lookup"><span data-stu-id="764aa-250">**To**</span></span> | <span data-ttu-id="764aa-251">메일 주소 입력</span><span class="sxs-lookup"><span data-stu-id="764aa-251">Type your email address</span></span> | <span data-ttu-id="764aa-252">hello 알림을 수신 하는 hello 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="764aa-253">**제목**</span><span class="sxs-lookup"><span data-stu-id="764aa-253">**Subject**</span></span> | <span data-ttu-id="764aa-254">부정적인 트윗 감정 검색</span><span class="sxs-lookup"><span data-stu-id="764aa-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="764aa-255">hello hello 전자 메일 알림의 제목 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="764aa-256">**본문**</span><span class="sxs-lookup"><span data-stu-id="764aa-256">**Body**</span></span> | <span data-ttu-id="764aa-257">트윗 텍스트, 위치</span><span class="sxs-lookup"><span data-stu-id="764aa-257">Tweet text, Location</span></span> | <span data-ttu-id="764aa-258">Hello 클릭 **텍스트 윗** 및 **위치** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="764aa-259">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-259">Click **Save**.</span></span>

<span data-ttu-id="764aa-260">Hello 워크플로 완료 했으므로 hello 논리 앱을 사용 하도록 설정 하 고 직장에서 hello 함수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="764aa-261">테스트 hello 워크플로</span><span class="sxs-lookup"><span data-stu-id="764aa-261">Test hello workflow</span></span>

1. <span data-ttu-id="764aa-262">Hello 논리가 응용 프로그램 디자이너에서에서 클릭 **실행** toostart hello 앱.</span><span class="sxs-lookup"><span data-stu-id="764aa-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="764aa-263">Hello 왼쪽된 열에서 클릭 **개요** hello 논리 앱의 toosee hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![논리 앱 실행 상태](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="764aa-265">(선택 사항) Hello 실행 toosee 세부 hello 실행 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="764aa-266">Tooyour 함수 이동한 hello 로그를 확인 한 다음 감성 값 수신 및 처리 된 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![함수 로그 보기](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="764aa-268">잠재적으로 부정적인 감정이 검색되면 전자 메일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="764aa-269">전자 메일을 받지 못한 경우 될 때마다 hello 함수 코드 tooreturn 빨간색을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="764aa-270">전자 메일 알림을 확인 한 후 뒤로 toohello 원본 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="764aa-271">이 자습서를 완료 한 후에 hello 논리 앱을 비활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="764aa-272">Hello 앱을 사용 하지 않도록 설정, 수행 하 고 hello 트랜잭션을 Cognitive 서비스 계정에서 사용 하 여 실행에 대 한 청구 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="764aa-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="764aa-273">이제 얼마나 쉬운지 논리 앱 워크플로로 toointegrate 함수에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="764aa-274">Hello 논리 앱을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="764aa-274">Disable hello logic app</span></span>

<span data-ttu-id="764aa-275">toodisable hello 논리 앱 클릭 **개요** 클릭 하 고 **사용 하지 않도록 설정** hello hello 화면 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="764aa-276">그러면 hello 논리 앱에서 실행 되 고 hello 앱을 삭제 하지 않고 요금이 발생 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![함수 로그](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="764aa-278">다음 단계</span><span class="sxs-lookup"><span data-stu-id="764aa-278">Next steps</span></span>

<span data-ttu-id="764aa-279">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="764aa-280">Cognitive Services 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="764aa-281">트윗 감정을 분류하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="764aa-282">TooTwitter 연결 하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="764aa-283">감성 검색 toohello 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="764aa-284">Hello 논리 앱 toohello 함수를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="764aa-285">Hello 함수에서 hello 응답에 따라 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="764aa-286">다음 자습서 toolearn toohello 어떻게 발전 toocreate 서버가 없는 API 함수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="764aa-287">Azure Functions를 사용하여 서버 없는 API 만들기</span><span class="sxs-lookup"><span data-stu-id="764aa-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="764aa-288">논리 앱에 대해 자세히 toolearn 참조 [Azure 논리 앱](../logic-apps/logic-apps-what-are-logic-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="764aa-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

