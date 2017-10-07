---
title: "Azure 스트림 분석을 사용 하 여 aaaReal 타임 Twitter 감성 분석 | Microsoft Docs"
description: "자세한 내용은 방법 실시간 Twitter 감성 분석에 대 한 스트림 분석 toouse 합니다. 라이브 대시보드 이벤트 생성 toodata에서 단계별 지침입니다."
keywords: "실시간 twitter 분석 추세, 정서 분석, 소셜 미디어 분석, 추세 분석 예제"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="7196e-105">Azure Stream Analytics에서 실시간 Twitter 감정 분석</span><span class="sxs-lookup"><span data-stu-id="7196e-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="7196e-106">자세한 내용은 toobuild 실시간으로 전환 하 여 소셜 미디어 분석에 대 한 감성 분석 솔루션 Azure 이벤트 허브로 이벤트를 Twitter 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="7196e-107">Azure 스트림 분석 쿼리 tooanalyze hello 데이터와 둘 중 어떤 저장소 hello 나중에 사용에 대 한 결과 또는 대시보드를 사용 하 여 작성할 수 있습니다 및 [Power BI](https://powerbi.com/) tooprovide insights 실시간으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="7196e-108">소셜 미디어 분석 도구는 조직에서 추세 항목을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="7196e-109">추세 항목은 소셜 미디어에 많은 게시물을 발생시키는 주제 및 입장입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="7196e-110">감성 분석 라고도 함 *의견 마이닝*, 제품, 아이디어 및에 대 한 소셜 미디어 분석 도구 toodetermine 태도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="7196e-111">실시간 Twitter 추세 분석 hello hashtag 구독 모델 toolisten toospecific 키워드 (해시)을 사용 하면 때문에 분석 도구를 보여 주는 좋은 예는 및의 피드 hello 감성 분석을 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="7196e-112">시나리오: 소셜 미디어 실시간 감정 분석</span><span class="sxs-lookup"><span data-stu-id="7196e-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="7196e-113">뉴스 미디어 웹 사이트에 있는 회사에서는 사이트 콘텐츠 즉시 관련 tooits 판독기는을 통해 경쟁 업체의 이점을 활용에 관심이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="7196e-114">hello 회사 Twitter 데이터의 실시간 감성 분석을 수행 하 여 관련 tooreaders 되는 항목에서 소셜 미디어 분석을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="7196e-115">Twitter에서 실시간으로에서 tooidentify 추세 항목 hello 회사 hello 윗 볼륨 및 주요 항목에 대 한 의미에 대 한 실시간 분석 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="7196e-116">즉, hello 필요는 감성 분석 분석 엔진 피드이 소셜 미디어 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7196e-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7196e-117">Prerequisites</span></span>
<span data-ttu-id="7196e-118">이 자습서에서는 tooTwitter 연결 하 고 (다음을 설정할 수 있습니다)는 특정 붙일 있는 트 윗 찾습니다 하는 클라이언트 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="7196e-119">순서 대로 toorun hello 응용 프로그램 및 Azure 스트리밍 분석을 사용 하 여 트 윗, 있어야 hello 다음 hello 분석:</span><span class="sxs-lookup"><span data-stu-id="7196e-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="7196e-120">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="7196e-120">An Azure subscription</span></span>
* <span data-ttu-id="7196e-121">Twitter 계정</span><span class="sxs-lookup"><span data-stu-id="7196e-121">A Twitter account</span></span> 
* <span data-ttu-id="7196e-122">Twitter 응용 프로그램, 그리고 hello [OAuth 액세스 토큰](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) 해당 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="7196e-123">방법에 대 한 고급 지침 제공 toocreate 나중에 Twitter 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="7196e-124">hello TwitterWPFClient 응용 프로그램을 읽는 hello Twitter 피드입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="7196e-125">tooget이 응용 프로그램, 다운로드 hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) GitHub에서 파일을 컴퓨터의 폴더에 다음 hello 패키지 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="7196e-126">Toosee hello 소스 코드를 원하는 고 디버거에서 hello 응용 프로그램을 실행에서 hello 소스 코드를 얻을 수 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="7196e-127">Streaming Analytics 입력을 위한 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="7196e-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="7196e-128">hello 샘플 응용 프로그램 이벤트를 생성 하며 tooan Azure 이벤트 허브를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="7196e-129">Azure 이벤트 허브는 hello 기본 설정 방법 스트림 분석에 대 한 이벤트 수집입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="7196e-130">자세한 내용은 참조 hello [Azure 이벤트 허브 설명서](../event-hubs/event-hubs-what-is-event-hubs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="7196e-131">이벤트 허브 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="7196e-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="7196e-132">이 절차에서는 이벤트 허브 네임 스페이스를 먼저 만들어야 하 고 이벤트 허브 toothat 네임 스페이스를 추가 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="7196e-133">이벤트 허브 네임 스페이스는 사용 toologically 그룹 관련 이벤트 버스 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="7196e-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="7196e-134">클릭 하 고 toohello Azure 포털에 로그인 **새로** > **사물 인터넷** > **이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="7196e-135">Hello에 **네임 스페이스 만들기** 블레이드에서 같은 네임 스페이스 이름 입력 `<yourname>-socialtwitter-eh-ns`합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="7196e-136">Hello 네임 스페이스에 대 한 모든 이름을 사용할 수 있습니다 하지만 hello 이름은 URL에 유효 해야 하 고 Azure 전체에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="7196e-137">구독을 선택하고 리소스 그룹을 만들거나 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![이벤트 허브 네임스페이스 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="7196e-139">Hello 네임 스페이스 배포 완료 되 면 Azure 리소스 목록에 hello 이벤트 허브 네임 스페이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="7196e-140">Hello 새 네임 스페이스를 클릭 하 고 hello 네임 스페이스 블레이드에서 클릭  **+ &nbsp;이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="7196e-141">새 이벤트 허브를 만들기 위한 hello 이벤트 허브 추가 단추</span><span class="sxs-lookup"><span data-stu-id="7196e-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="7196e-142">이름 hello 새 이벤트 허브 `socialtwitter-eh`합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="7196e-143">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-143">You can use a different name.</span></span> <span data-ttu-id="7196e-144">이렇게 하면 hello 이름을 나중에 필요 하기 때문에, 메모를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="7196e-145">Hello 이벤트 허브에 대 한 다른 옵션 tooset를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-145">You don't need tooset any other options for hello event hub.</span></span>

    ![새 이벤트 허브를 만들기 위한 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="7196e-147">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="7196e-148">권한 부여 액세스 toohello 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="7196e-148">Grant access toohello event hub</span></span>

<span data-ttu-id="7196e-149">프로세스 tooan 이벤트 허브 데이터를 보낼 수 있습니다, 전에 hello 이벤트 허브에 적절 한 액세스를 허용 하는 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="7196e-150">hello 액세스 정책 권한 부여 정보를 포함 하는 연결 문자열을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="7196e-151">Hello 이벤트 네임 스페이스 블레이드에서 클릭 **이벤트 허브** 새 이벤트 허브의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="7196e-152">이벤트 허브 블레이드에서 hello 클릭 **공유 액세스 정책을** 클릭 하 고  **+ &nbsp;추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7196e-153">Hello 이벤트 허브 네임 스페이스가 아니라 hello 이벤트 허브를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="7196e-154">**클레임**에 대해 `socialtwitter-access`라는 이름의 정책을 추가하고 **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![새 이벤트 허브 액세스 정책을 만들기 위한 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="7196e-156">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-156">Click **Create**.</span></span>

5.  <span data-ttu-id="7196e-157">정책이 배포 된 hello 후, 공유 액세스 정책의 hello 목록에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="7196e-158">찾기 hello 상자 **연결 문자열-기본 키** hello 복사 단추 다음 toohello 연결 문자열을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Hello 액세스 정책에서 hello 기본 연결 문자열 키를 복사합니다.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="7196e-160">연결 문자열을 hello를 텍스트 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="7196e-161">몇 가지 약간의 편집 tooit를 변경한 후이 연결 문자열 hello 다음 섹션에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="7196e-162">hello 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="7196e-163">Hello 연결 문자열을 세미콜론으로 구분 된 여러 키-값 쌍이 들어: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, 및 `EntityPath`합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="7196e-164">보안을 위해 hello 예제에서 hello 연결 문자열의 일부 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="7196e-165">Hello 텍스트 편집기에서 제거 hello `EntityPath` hello 연결 문자열에서 쌍 (tooremove hello 세미콜론 앞에 오는 반드시 함).</span><span class="sxs-lookup"><span data-stu-id="7196e-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="7196e-166">완료 되 면 hello 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="7196e-167">구성 되 고 hello Twitter 클라이언트 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="7196e-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="7196e-168">클라이언트 응용 프로그램 hello Twitter에서 직접 윗 이벤트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="7196e-169">그렇게 toodo 주문에서 권한 toocall hello 스트리밍 Api Twitter 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="7196e-170">tooconfigure 권한, 응용 프로그램에서 만드는 Twitter 고유 자격 증명 (예: OAuth 토큰)를 생성 하는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="7196e-171">구성할 수 있습니다 클라이언트 응용 프로그램 toouse hello 이러한 자격 증명 API를 호출할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="7196e-172">Twitter 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="7196e-172">Create a Twitter application</span></span>
<span data-ttu-id="7196e-173">이 자습서에 사용할 수 있는 Twitter 응용 프로그램이 아직 없는 경우 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="7196e-174">Twitter 계정이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="7196e-175">응용 프로그램 만들기 및 hello 키, 암호, 및 토큰을 가져오는 Twitter의 정확한 프로세스 hello 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="7196e-176">이러한 지침은 hello Twitter 사이트에 표시 되는 내용 일치 하지 않으면 toohello Twitter 개발자 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7196e-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="7196e-177">Toohello 이동 [Twitter 응용 프로그램 관리 페이지](https://apps.twitter.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="7196e-178">새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-178">Create a new application.</span></span> 

    * <span data-ttu-id="7196e-179">Hello 웹 사이트 URL에 대 한 올바른 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="7196e-180">없기 toobe 라이브 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-180">It does not have toobe a live site.</span></span> <span data-ttu-id="7196e-181">(`localhost`만 지정할 수는 없음)</span><span class="sxs-lookup"><span data-stu-id="7196e-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="7196e-182">Hello 콜백 필드를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-182">Leave hello callback field blank.</span></span> <span data-ttu-id="7196e-183">이 자습서에 사용할 클라이언트 응용 프로그램 hello 콜백이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Twitter에서 응용 프로그램 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="7196e-185">필요에 따라 tooread 전용 hello 응용 프로그램의 사용 권한을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="7196e-186">Hello 응용 프로그램을 만들면 이동 toohello **키와 액세스 토큰이** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7196e-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="7196e-187">Hello 단추 toogenerate 액세스 토큰 및 액세스 토큰 암호를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="7196e-188">Hello 다음 절차에서 필요 하므로이 정보를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="7196e-189">hello 키와 hello Twitter 응용 프로그램에 대 한 암호 tooyour Twitter 계정 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="7196e-190">중요 하 게이 정보를 처리, Twitter 암호와 같은으로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="7196e-191">예를 들어 tooothers를 지정 하는 응용 프로그램에서이 정보를 포함 하지 않음.</span><span class="sxs-lookup"><span data-stu-id="7196e-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="7196e-192">Hello 클라이언트 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="7196e-192">Configure hello client application</span></span>
<span data-ttu-id="7196e-193">TooTwitter 데이터를 사용 하 여 연결 하는 클라이언트 응용 프로그램 작성 했습니다 [Twitter의 스트리밍 Api](https://dev.twitter.com/streaming/overview) 항목의 특정 집합에 대 한 트 윗 이벤트 toocollect 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="7196e-194">hello 응용 프로그램 hello를 사용 하 여 [Sentiment140](http://help.sentiment140.com/) 감성 값 tooeach 윗 다음 hello를 할당 하는 오픈 소스 도구:</span><span class="sxs-lookup"><span data-stu-id="7196e-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="7196e-195">0 = 부정적</span><span class="sxs-lookup"><span data-stu-id="7196e-195">0 = negative</span></span>
* <span data-ttu-id="7196e-196">2 = 중립</span><span class="sxs-lookup"><span data-stu-id="7196e-196">2 = neutral</span></span>
* <span data-ttu-id="7196e-197">4 = 긍정적</span><span class="sxs-lookup"><span data-stu-id="7196e-197">4 = positive</span></span>

<span data-ttu-id="7196e-198">Hello 윗 이벤트 감성 값 할당 된, 후 이전에 만든 toohello 이벤트 허브를 푸시할는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="7196e-199">Hello 응용 프로그램을 실행 하기 전에 hello Twitter 키 hello 이벤트 허브 연결 문자열 등의 정보를 특정 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="7196e-200">다음과 같은이 방법으로 hello 구성 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="7196e-201">Hello 응용 프로그램을 실행 하 고 hello 응용 프로그램의 UI tooenter hello 키, 비밀 정보 및 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="7196e-202">이 작업을 수행 하는 경우 현재 세션에 대 한 hello 구성 정보를 사용 하지만 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="7196e-203">Hello 응용 프로그램의.config 파일 및 설정 hello 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="7196e-204">이 방법은 hello 구성 정보를 유지 하지만 잠재적으로 중요 한 정보가 일반 텍스트로 컴퓨터에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="7196e-205">hello 다음 절차에서는 두 가지 방법을 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="7196e-206">다운로드 하 고 압축을 hello 확인 [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) hello 필수 구성 요소에 나열 된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="7196e-207">실행 시 (및 hello 현재 세션에 대해서만), tooset hello 값 실행 hello `TwitterWPFClient.exe` 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="7196e-208">Hello 응용 프로그램 메시지를 표시 하면 hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="7196e-209">hello Twitter 소비자 키 (API 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="7196e-210">hello Twitter 사용자 암호 (API Secret)입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="7196e-211">Twitter 액세스 토큰 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="7196e-212">hello Twitter 액세스 토큰 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="7196e-213">이전에 저장 하는 hello 연결 문자열 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="7196e-214">Hello를 제거 하는 hello 연결 문자열을 사용 하면 `EntityPath` 키-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="7196e-215">에 대 한 toodetermine 정서를 원하는 hello Twitter 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![TwitterWpfClient 응용 프로그램 실행 중, 가려진 설정 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="7196e-217">tooset hello 값은 지속적으로, 텍스트 편집기 tooopen hello TwitterWpfClient.exe.config 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="7196e-218">Hello 그런 다음 `<appSettings>` 요소를이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="7196e-219">설정 `oauth_consumer_key` toohello Twitter 소비자 키 (API 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="7196e-220">설정 `oauth_consumer_secret` toohello Twitter 사용자 암호 (API Secret)입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="7196e-221">설정 `oauth_token` toohello Twitter 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="7196e-222">설정 `oauth_token_secret` toohello Twitter 액세스 토큰 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="7196e-223">Hello의 뒷부분에 나오는 `<appSettings>` 요소를이 변경 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7196e-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="7196e-224">설정 `EventHubName` toohello 이벤트 허브 이름 (즉, hello 엔터티 경로 toohello 값).</span><span class="sxs-lookup"><span data-stu-id="7196e-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="7196e-225">설정 `EventHubNameConnectionString` toohello 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="7196e-226">Hello를 제거 하는 hello 연결 문자열을 사용 하면 `EntityPath` 키-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="7196e-227">hello `<appSettings>` 섹션 다음 예제는 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="7196e-228">(이해를 돕고 보안을 위해 일부 줄을 래핑하고 일부 문자는 제거했습니다.)</span><span class="sxs-lookup"><span data-stu-id="7196e-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Hello Twitter 키와 비밀 정보 및 hello 이벤트 허브 연결 문자열 정보를 표시 하는 텍스트 편집기에서 TwitterWpfClient 응용 프로그램 구성 파일](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="7196e-230">Hello 응용 프로그램을 시작 이미 하지 않은 경우 지금 TwitterWpfClient.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="7196e-231">Hello toocollect 소셜 감성 녹색 시작 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="7196e-232">Hello 사용 하 여 트 윗 이벤트 참조 **CreatedAt**, **항목**, 및 **SentimentScore** tooyour 이벤트 허브 전송 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![TwitterWpfClient 응용 프로그램 실행 중, 트윗 목록 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="7196e-234">오류를 보고 트 윗 hello hello 창 하단에 표시 되는 스트림을 표시 되지 않는 경우에 hello 키 및 암호를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="7196e-235">또한 hello 연결 문자열 확인 (hello를 포함 하지 않는지 확인 `EntityPath` 키와 값입니다.)</span><span class="sxs-lookup"><span data-stu-id="7196e-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7196e-236">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="7196e-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="7196e-237">트 윗 이벤트는 Twitter에서 실시간에서 스트리밍, 있습니다 수 설정할 스트림 분석 작업 tooanalyze 이러한 이벤트를 실시간으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="7196e-238">Hello Azure 포털에서에서 클릭 **새로** > **사물 인터넷** > **스트림 분석 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="7196e-239">이름 hello 작업 `socialtwitter-sa-job` 구독, 리소스 그룹 및 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="7196e-240">것이 좋습니다 tooplace hello 작업과 hello 이벤트 허브를 hello에 동일한 지역에 대 한 최상의 성능 지역 간 데이터 tootransfer을 지불 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![새 Stream Analytics 작업 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="7196e-242">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-242">Click **Create**.</span></span>

    <span data-ttu-id="7196e-243">hello 작업은 생성 하 고 hello 포털 작업 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="7196e-244">Hello 작업 입력 지정</span><span class="sxs-lookup"><span data-stu-id="7196e-244">Specify hello job input</span></span>

1. <span data-ttu-id="7196e-245">스트림 분석 작업에서 아래 **작업 토폴로지** hello 작업 블레이드의 hello 중간 클릭 **입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="7196e-246">Hello에 **입력** 블레이드에서 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="7196e-247">**입력된 별칭**: hello 이름 사용 `TwitterStream`합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="7196e-248">다른 이름을 사용하는 경우 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="7196e-249">**원본 형식**: **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="7196e-250">**원본**: **이벤트 허브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="7196e-251">**가져오기 옵션**: **현재 구독의 이벤트 허브 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="7196e-252">**서비스 버스 네임 스페이스**: 이전에 만든 hello 이벤트 허브 네임 스페이스를 선택 (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="7196e-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="7196e-253">**이벤트 허브**: 이전에 만든 선택 hello 이벤트 허브 (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="7196e-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="7196e-254">**이벤트 허브 정책 이름**: 이전에 만든 hello 액세스 정책 (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="7196e-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Streaming Analytics 작업에 대한 새 입력 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="7196e-256">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="7196e-257">Hello 작업 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-257">Specify hello job query</span></span>

<span data-ttu-id="7196e-258">Stream Analytics는 변환을 설명하는 간단하고 선언적인 쿼리 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="7196e-259">hello 언어에 대해 자세히 toolearn 참조 hello [Azure 스트림 분석 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="7196e-260">이 자습서에서는 Twitter 데이터에 대해 여러 쿼리를 작성하고 테스트하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="7196e-261">사용할 수 있습니다 항목 간에 언급 되어 toocompare hello 수는 [연속 창](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello 수가 5 초 마다 항목에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="7196e-262">닫기 hello **입력** 블레이드 च ो.</span><span class="sxs-lookup"><span data-stu-id="7196e-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="7196e-263">Hello 작업 블레이드에서 hello 클릭 **쿼리** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="7196e-264">Azure hello 입력 목록과 hello 작업에 대해 구성 되 고 수 있는 쿼리를 만들 수 있습니다는 출력을 toohello 출력 전송 될 때 hello 입력된 스트림 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="7196e-265">해당 hello TwitterWpfClient 응용 프로그램이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="7196e-266">Hello에 **쿼리** 블레이드에서 hello 점 다음 toohello 클릭 `TwitterStream` 입력 한 다음 선택 **데이터 입력에서 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![메뉴 옵션 toouse 샘플 hello 스트리밍 분석 작업 항목에 대 한 데이터와 데이터 "샘플 입력에서" 선택](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="7196e-268">Tooread hello 입력 스트림을 기간 측면에서 정의 된 샘플 데이터 tooget 양을 지정할 수 있는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="7196e-269">설정 **분** too3 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    !["3 분" 선택 된 입력된 스트림의 hello 샘플링에 대 한 옵션입니다.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="7196e-271">Azure는 3 분 분량의 hello 입력 스트림에서 데이터를 샘플링 하 고 hello 샘플 데이터를 준비 되 면 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="7196e-272">(짧은 시간이 소요됩니다.)</span><span class="sxs-lookup"><span data-stu-id="7196e-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="7196e-273">hello 예제 데이터는 임시로 저장 되었다가 hello 쿼리 창이 열려 있는 동안를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="7196e-274">Hello 쿼리 창을 닫으면 hello 샘플 데이터가 무시 되 있고 toocreate 새 샘플 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="7196e-275">Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="7196e-276">하는 경우 사용 하지 않은 `TwitterStream` hello 입력 별칭에 대 한 hello로 대 한 별칭으로 대체 `TwitterStream` hello 쿼리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="7196e-277">이 쿼리에서 hello를 사용 하 여 **TIMESTAMP BY** 키워드 toospecify hello 임시 계산에서 사용 되는 hello 페이로드 toobe의 타임 스탬프 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="7196e-278">이 필드를 지정 하지 않으면 hello 기간 이동 연산은 이벤트 허브 hello에 각 이벤트 도착 하는 hello 시간을 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="7196e-279">hello "도착 시간 및 응용 프로그램 시간" 섹션에서 자세한 내용을 [스트림 분석 쿼리 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="7196e-280">이 쿼리는 또한 각 창의 hello 끝에 대 한 타임 스탬프 hello를 사용 하 여 액세스 **System.Timestamp** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="7196e-281">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-281">Click **Test**.</span></span> <span data-ttu-id="7196e-282">hello 쿼리 하면 샘플링 hello 데이터에 대해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="7196e-283">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-283">Click **Save**.</span></span> <span data-ttu-id="7196e-284">이 hello 스트리밍 분석 작업의 일부로 hello 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="7196e-285">(Hello 예제 데이터 저장 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="7196e-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="7196e-286">서로 다른 필드를 사용 하 여 hello 스트림에서 실험</span><span class="sxs-lookup"><span data-stu-id="7196e-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="7196e-287">hello 다음 표 hello JSON 스트리밍 데이터의 일부인 hello 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="7196e-288">Hello 쿼리 편집기에서 무료 tooexperiment을 느낍니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="7196e-289">JSON 속성</span><span class="sxs-lookup"><span data-stu-id="7196e-289">JSON property</span></span> | <span data-ttu-id="7196e-290">정의</span><span class="sxs-lookup"><span data-stu-id="7196e-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="7196e-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="7196e-291">CreatedAt</span></span> | <span data-ttu-id="7196e-292">hello 시간 해당 hello 윗 생성</span><span class="sxs-lookup"><span data-stu-id="7196e-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="7196e-293">항목</span><span class="sxs-lookup"><span data-stu-id="7196e-293">Topic</span></span> | <span data-ttu-id="7196e-294">hello hello와 일치 하는 지정 되는 키워드</span><span class="sxs-lookup"><span data-stu-id="7196e-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="7196e-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="7196e-295">SentimentScore</span></span> | <span data-ttu-id="7196e-296">Sentiment140에서 hello 감성 점수</span><span class="sxs-lookup"><span data-stu-id="7196e-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="7196e-297">작성자</span><span class="sxs-lookup"><span data-stu-id="7196e-297">Author</span></span> | <span data-ttu-id="7196e-298">hello 트 윗을 보낼 hello Twitter 핸들</span><span class="sxs-lookup"><span data-stu-id="7196e-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="7196e-299">텍스트</span><span class="sxs-lookup"><span data-stu-id="7196e-299">Text</span></span> | <span data-ttu-id="7196e-300">hello 윗의 전문을 hello</span><span class="sxs-lookup"><span data-stu-id="7196e-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="7196e-301">출력 싱크 만들기</span><span class="sxs-lookup"><span data-stu-id="7196e-301">Create an output sink</span></span>

<span data-ttu-id="7196e-302">이벤트 스트림, 이벤트 허브 입력된 tooingest 이벤트 및 쿼리 tooperform 변환 hello 스트림을 통해 이제 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="7196e-303">hello 마지막 단계는 hello 작업에 대 한 출력 싱크가 toodefine입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="7196e-304">이 자습서에서는 hello 작업 쿼리 tooAzure Blob 저장소에서에서 집계 하는 hello 윗 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="7196e-305">또한 프로그램 결과 tooAzure SQL 데이터베이스, Azure 테이블 저장소에 이벤트 허브를 푸시할 수 있습니다 또는 Power BI 응용 프로그램에 따라 필요한.</span><span class="sxs-lookup"><span data-stu-id="7196e-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="7196e-306">Hello 작업 출력을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-306">Specify hello job output</span></span>

1. <span data-ttu-id="7196e-307">Hello에 **작업 토폴로지** 섹션에서 hello **출력** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="7196e-308">Hello에 **출력** 블레이드에서 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="7196e-309">**출력 별칭**: hello 이름 사용 `TwitterStream-Output`합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="7196e-310">**싱크**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="7196e-311">**가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="7196e-312">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="7196e-312">**Storage account**.</span></span> <span data-ttu-id="7196e-313">**새 저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="7196e-314">**저장소 계정**(두 번째 상자).</span><span class="sxs-lookup"><span data-stu-id="7196e-314">**Storage account** (second box).</span></span> <span data-ttu-id="7196e-315">`YOURNAMEsa`를 입력합니다. 여기서 `YOURNAME`은 사용자 이름 또는 다른 고유 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="7196e-316">hello 이름은 소문자 및 숫자를 사용할 수 및 Azure 전체에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="7196e-317">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="7196e-317">**Container**.</span></span> <span data-ttu-id="7196e-318">`socialtwitter`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="7196e-319">hello 저장소 계정 이름과 컨테이너 이름에 사용 되는 함께 tooprovide 다음과 같이 hello blob 저장소에 대 한 URI는</span><span class="sxs-lookup"><span data-stu-id="7196e-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Stream Analytics 작업에 대한 “새 출력” 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="7196e-321">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-321">Click **Create**.</span></span> 

    <span data-ttu-id="7196e-322">Azure는 hello 저장소 계정을 만들고 키를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="7196e-323">닫기 hello **출력** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="7196e-324">Hello 작업 시작</span><span class="sxs-lookup"><span data-stu-id="7196e-324">Start hello job</span></span>

<span data-ttu-id="7196e-325">작업 입력, 쿼리 및 출력이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="7196e-326">준비 toostart hello 스트림 분석 작업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="7196e-327">해당 hello TwitterWpfClient 응용 프로그램이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="7196e-328">Hello 작업 블레이드에서 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-328">In hello job blade, click **Start**.</span></span>

    ![Hello 스트림 분석 작업 시작](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="7196e-330">Hello에 **시작 작업** 블레이드에서 대 한 **작업 출력 시작 시간**선택, **이제** 클릭 하 고 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Hello 스트림 분석 작업에 대 한 블레이드 "작업을 시작 합니다."](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="7196e-332">Azure 알리는 hello 작업이 시작 되 고으로 표시 되 면 hello 상태 hello 작업 블레이드에서 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![작업 실행 중](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="7196e-334">정서 분석에 대한 출력 보기</span><span class="sxs-lookup"><span data-stu-id="7196e-334">View output for sentiment analysis</span></span>

<span data-ttu-id="7196e-335">작업 실행을 시작 하 고 hello 실시간 Twitter 스트림 처리, 후 감성 분석에 대 한 hello 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="7196e-336">와 같은 도구를 사용할 수 있습니다 [Azure 저장소 탐색기](https://http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction) tooview 작업 실시간으로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="7196e-337">여기에서 사용할 수 있습니다 [Power BI](https://powerbi.com/) tooextend 프로그램 응용 프로그램 tooinclude 사용자 지정된 된 대시보드와 같은 hello hello 스크린 샷 뒤에 표시 된 것 하나:</span><span class="sxs-lookup"><span data-stu-id="7196e-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="7196e-339">다른 쿼리 tooidentify 추세 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="7196e-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="7196e-340">Twitter 감성 toounderstand에서는 다른 쿼리 기반으로 한 [슬라이딩 윈도우](https://msdn.microsoft.com/library/azure/dn835051.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="7196e-341">지정된 된 기간에 언급 되어에 대 한 임계값을 교차 하는 항목에 대 한 보면 tooidentify 추세 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="7196e-342">이 자습서의 hello 목적에 언급 된 20 배 이상 hello 마지막 5 초 하는 항목에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="7196e-343">Hello 작업 블레이드에서 클릭 **중지** toostop hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="7196e-344">Hello에 **작업 토폴로지** 섹션에서 hello **쿼리** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="7196e-345">Hello 쿼리 toohello 다음을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="7196e-346">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-346">Click **Save**.</span></span>

5. <span data-ttu-id="7196e-347">해당 hello TwitterWpfClient 응용 프로그램이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="7196e-348">클릭 **시작** hello 새 쿼리를 사용 하 여 toorestart hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7196e-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="7196e-349">지원 받기</span><span class="sxs-lookup"><span data-stu-id="7196e-349">Get support</span></span>
<span data-ttu-id="7196e-350">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7196e-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7196e-351">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7196e-351">Next steps</span></span>
* [<span data-ttu-id="7196e-352">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="7196e-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7196e-353">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="7196e-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7196e-354">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="7196e-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7196e-355">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="7196e-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7196e-356">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="7196e-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
