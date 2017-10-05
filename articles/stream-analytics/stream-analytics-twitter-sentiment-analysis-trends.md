---
title: "Azure Stream Analytics를 사용한 실시간 Twitter 정서 분석 | Microsoft Docs"
description: "실시간 Twitter 정서 분석에 대한 Stream Analytics을 사용하는 방법에 대해 알아봅니다. 이벤트 생성부터 라이브 대시보드의 데이터에 이르는 단계별 지침이 포함되어 있습니다."
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
ms.openlocfilehash: 8de6850964700f5b3f71d144b40af927f2e52d7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="31746-105">Azure Stream Analytics에서 실시간 Twitter 감정 분석</span><span class="sxs-lookup"><span data-stu-id="31746-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="31746-106">실시간 Twitter 이벤트를 Azure Event Hubs로 가져와서 소셜 미디어 분석을 위한 감정 분석 솔루션을 구축하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31746-106">Learn how to build a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="31746-107">그런 다음 Azure Stream Analytics 쿼리를 작성하여 데이터를 분석하고 나중에 사용할 수 있도록 결과를 저장하거나 대시보드 및 [Power BI](https://powerbi.com/)를 사용하여 실시간으로 통찰력 있는 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-107">You can then write an Azure Stream Analytics query to analyze the data and either store the results for later use or use a dashboard and [Power BI](https://powerbi.com/) to provide insights in real time.</span></span>

<span data-ttu-id="31746-108">소셜 미디어 분석 도구는 조직에서 추세 항목을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="31746-109">추세 항목은 소셜 미디어에 많은 게시물을 발생시키는 주제 및 입장입니다.</span><span class="sxs-lookup"><span data-stu-id="31746-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="31746-110">*의견 마이닝*이라는 감정 분석은 소셜 미디어 분석 도구를 사용하여 제품, 아이디어 등에 대한 자세를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools to determine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="31746-111">실시간 Twitter 추세 분석은 분석 도구의 아주 좋은 예입니다. 특정 키워드(해시태그)를 수신 대기하고 피드에 대한 감정 분석을 개발할 수 있는 해시 태그 구독 모델을 사용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="31746-111">Real-time Twitter trend analysis is a great example of an analytics tool, because the hashtag subscription model enables you to listen to specific keywords (hashtags) and develop sentiment analysis of the feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="31746-112">시나리오: 소셜 미디어 실시간 감정 분석</span><span class="sxs-lookup"><span data-stu-id="31746-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="31746-113">뉴스 미디어 웹 사이트를 보유하는 기업은 독자와 직접적으로 관련이 있는 사이트 콘텐츠를 부각시켜 경쟁 우위를 확보하는 데 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant to its readers.</span></span> <span data-ttu-id="31746-114">이러한 기업은 Twitter 데이터에 대해 실시간으로 감정을 분석하여 독자와 관련된 항목에 대한 소셜 미디어 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-114">The company uses social media analysis on topics that are relevant to readers by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="31746-115">Twitter에서 실시간으로 추세를 분석할 토픽을 식별하기 위해 기업에서는 주요 토픽에 대한 트윗 볼륨 및 감정에 대한 실시간 분석이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-115">To identify trending topics in real time on Twitter, the company needs real-time analytics about the tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="31746-116">즉, 이 소셜 미디어 피드를 기반으로 하는 감정 분석 엔진이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-116">In other words, the need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31746-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31746-117">Prerequisites</span></span>
<span data-ttu-id="31746-118">이 자습서에서는 Twitter에 연결하고 특정 해시태그(설정 가능)가 있는 트윗을 찾는 클라이언트 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-118">In this tutorial, you use a client application that connects to Twitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="31746-119">응용 프로그램을 실행하고 Azure Streaming Analytics를 사용하여 트윗을 분석하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-119">In order to run the application and analyze the tweets using Azure Streaming Analytics, you must have the following:</span></span>

* <span data-ttu-id="31746-120">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="31746-120">An Azure subscription</span></span>
* <span data-ttu-id="31746-121">Twitter 계정</span><span class="sxs-lookup"><span data-stu-id="31746-121">A Twitter account</span></span> 
* <span data-ttu-id="31746-122">Twitter 응용 프로그램 및 해당 응용 프로그램에 대한 [OAuth 액세스 토큰](https://dev.twitter.com/oauth/overview/application-owner-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="31746-122">A Twitter application, and the [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="31746-123">나중에 Twitter 응용 프로그램을 만드는 방법에 대한 대략적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-123">We provide high-level instructions for how to create a Twitter application later.</span></span>
* <span data-ttu-id="31746-124">Twitter 피드를 읽어 오는 TwitterWPFClient 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="31746-124">The TwitterWPFClient application, which reads the Twitter feed.</span></span> <span data-ttu-id="31746-125">이 응용 프로그램을 가져오려면 GitHub에서 [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) 파일을 다운로드한 후 컴퓨터의 폴더로 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="31746-125">To get this application, download the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip the package into a folder on your computer.</span></span> <span data-ttu-id="31746-126">소스 코드를 확인하고 디버거에서 응용 프로그램을 실행하려면 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)에서 소스 코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-126">If you want to see the source code and run the application in a debugger, you can get the source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="31746-127">Streaming Analytics 입력을 위한 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="31746-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="31746-128">응용 프로그램 예제에서 이벤트를 생성하여 Azure Event Hub에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-128">The sample application generates events and pushes them to an Azure event hub.</span></span> <span data-ttu-id="31746-129">Azure Event Hubs는 Stream Analytics을 위해 이벤트를 수집하는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="31746-129">Azure event hubs are the preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="31746-130">자세한 내용은 [Azure Event Hubs 설명서](../event-hubs/event-hubs-what-is-event-hubs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31746-130">For more information, see the [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="31746-131">이벤트 허브 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="31746-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="31746-132">이 절차에서는 이벤트 허브 네임스페이스를 먼저 만든 후 이벤트 허브를 해당 네임스페이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-132">In this procedure, you first create an event hub namespace, and then you add an event hub to that namespace.</span></span> <span data-ttu-id="31746-133">이벤트 허브 네임스페이스는 관련된 이벤트 버스 인스턴스를 논리적으로 그룹화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-133">Event hub namespaces are used to logically group related event bus instances.</span></span> 

1. <span data-ttu-id="31746-134">Azure Portal에 로그인하고 **새로 만들기** > **사물 인터넷** > **이벤트 허브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-134">Log  in to the Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="31746-135">**네임스페이스 만들기** 블레이드에서 네임스페이스 이름을 입력합니다(예: `<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="31746-135">In the **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="31746-136">네임스페이스에 어떤 이름이든 사용할 수 있지만 이름은 URL에 대해 유효해야 하며 Azure 전체에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-136">You can use any name for the namespace, but the name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="31746-137">구독을 선택하고 리소스 그룹을 만들거나 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![이벤트 허브 네임스페이스 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="31746-139">네임스페이스에서 배포를 완료했으면 Azure 리소스 목록에서 이벤트 허브 네임스페이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-139">When the namespace has finished deploying, find the event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="31746-140">새 네임스페이스를 클릭하고 네임스페이스 블레이드에서 **+&nbsp;이벤트 허브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-140">Click the new namespace, and in the namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="31746-141">새 이벤트 허브를 만들기 위한 이벤트 허브 추가 단추</span><span class="sxs-lookup"><span data-stu-id="31746-141">The Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="31746-142">새 이벤트 허브 이름을 `socialtwitter-eh`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-142">Name the new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="31746-143">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-143">You can use a different name.</span></span> <span data-ttu-id="31746-144">이 경우 나중에 이름이 필요하기 때문에 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="31746-144">If you do, make a note of it, because you need the name later.</span></span> <span data-ttu-id="31746-145">이벤트 허브에 다른 옵션을 설정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-145">You don't need to set any other options for the event hub.</span></span>

    ![새 이벤트 허브를 만들기 위한 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="31746-147">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-147">Click **Create**.</span></span>


### <a name="grant-access-to-the-event-hub"></a><span data-ttu-id="31746-148">이벤트 허브에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="31746-148">Grant access to the event hub</span></span>

<span data-ttu-id="31746-149">프로세스에서 이벤트 허브로 데이터를 보낼 수 있으려면 이벤트 허브에 적절한 액세스 권한을 허용하는 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-149">Before a process can send data to an event hub, the event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="31746-150">액세스 정책은 권한 부여 정보를 포함하는 연결 문자열을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-150">The access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="31746-151">이벤트 네임스페이스 블레이드에서 **이벤트 허브**를 클릭하고 새 이벤트 허브의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-151">In the event namespace blade, click **Event Hubs** and then click the name of your new event hub.</span></span>

2.  <span data-ttu-id="31746-152">이벤트 허브 블레이드에서 **공유 액세스 정책**을 클릭한 후 **+&nbsp;추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-152">In the event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="31746-153">이벤트 허브 네임스페이스가 아니라 이벤트 허브로 작업하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-153">Make sure you're working with the event hub, not the event hub namespace.</span></span>

3.  <span data-ttu-id="31746-154">**클레임**에 대해 `socialtwitter-access`라는 이름의 정책을 추가하고 **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![새 이벤트 허브 액세스 정책을 만들기 위한 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="31746-156">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-156">Click **Create**.</span></span>

5.  <span data-ttu-id="31746-157">정책이 배포되었으면 공유 액세스 정책 목록에서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-157">After the policy has been deployed, click it in the list of shared access policies.</span></span>

6.  <span data-ttu-id="31746-158">**CONNECTION STRING-PRIMARY KEY**로 레이블이 지정된 상자를 찾고 연결 문자열 옆의 복사 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-158">Find the box labeled **CONNECTION STRING-PRIMARY KEY** and click the copy button next to the connection string.</span></span> 
    
    ![액세스 정책에서 기본 연결 문자열 키 복사](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="31746-160">연결 문자열을 텍스트 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-160">Paste the connection string into a text editor.</span></span> <span data-ttu-id="31746-161">다음 섹션에서 몇 가지 편집을 수행한 후 이 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-161">You need this connection string for the next section, after you make some small edits to it.</span></span>

    <span data-ttu-id="31746-162">연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-162">The connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="31746-163">연결 문자열에는 세미콜론으로 구분된 여러 키-값 쌍이 포함되어 있습니다(`Endpoint`, `SharedAccessKeyName`, `SharedAccessKey` 및 `EntityPath`).</span><span class="sxs-lookup"><span data-stu-id="31746-163">Notice that the connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="31746-164">보안을 위해 예제에 있는 연결 문자열의 일부가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-164">For security, parts of the connection string in the example have been removed.</span></span>

8.  <span data-ttu-id="31746-165">텍스트 편집기에서 연결 문자열의 `EntityPath` 쌍을 제거합니다(앞에 나오는 세미콜론을 반드시 제거).</span><span class="sxs-lookup"><span data-stu-id="31746-165">In the text editor, remove the `EntityPath` pair from the connection string (don't forget to remove the semicolon that precedes it).</span></span> <span data-ttu-id="31746-166">작업을 완료한 후 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-166">When you're done, the connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-the-twitter-client-application"></a><span data-ttu-id="31746-167">Twitter 클라이언트 응용 프로그램 구성 및 시작</span><span class="sxs-lookup"><span data-stu-id="31746-167">Configure and start the Twitter client application</span></span>
<span data-ttu-id="31746-168">클라이언트 응용 프로그램이 Twitter에서 트윗 이벤트를 직접 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="31746-168">The client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="31746-169">이렇게 하려면 Twitter Streaming API를 호출할 수 있는 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-169">In order to do so, it needs permission to call the Twitter Streaming APIs.</span></span> <span data-ttu-id="31746-170">해당 사용 권한을 구성하려면 고유한 자격 증명(예: OAuth 토큰)을 생성하는 응용 프로그램을 Twitter에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31746-170">To configure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="31746-171">그런 다음 API를 호출할 때 이러한 자격 증명을 사용하도록 클라이언트 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-171">You can then configure the client application to use these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="31746-172">Twitter 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="31746-172">Create a Twitter application</span></span>
<span data-ttu-id="31746-173">이 자습서에 사용할 수 있는 Twitter 응용 프로그램이 아직 없는 경우 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="31746-174">Twitter 계정이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="31746-175">Twitter에서 응용 프로그램을 만들고 키, 비밀 및 토큰을 가져오는 정확한 프로세스는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-175">The exact process in Twitter for creating an application and getting the keys, secrets, and token might change.</span></span> <span data-ttu-id="31746-176">이러한 지침이 Twitter 사이트에 표시되는 내용과 일치하지 않으면 Twitter 개발자 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31746-176">If these instructions don't match what you see on the Twitter site, refer to the Twitter developer documentation.</span></span>

1. <span data-ttu-id="31746-177">[Twitter 응용 프로그램 관리 페이지](https://apps.twitter.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-177">Go to the [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="31746-178">새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31746-178">Create a new application.</span></span> 

    * <span data-ttu-id="31746-179">웹 사이트 URL에 대한 유효한 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-179">For the website URL, specify a valid URL.</span></span> <span data-ttu-id="31746-180">라이브 사이트일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-180">It does not have to be a live site.</span></span> <span data-ttu-id="31746-181">(`localhost`만 지정할 수는 없음)</span><span class="sxs-lookup"><span data-stu-id="31746-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="31746-182">콜백 필드는 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="31746-182">Leave the callback field blank.</span></span> <span data-ttu-id="31746-183">이 자습서에 사용할 클라이언트 응용 프로그램에는 콜백이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-183">The client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Twitter에서 응용 프로그램 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="31746-185">필요에 따라 응용 프로그램 권한을 읽기 전용으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-185">Optionally, change the application's permissions to read-only.</span></span>

4. <span data-ttu-id="31746-186">응용 프로그램이 만들어지면 **키 및 액세스 토큰** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-186">When the application is created, go to the **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="31746-187">액세스 토큰 및 액세스 토큰 암호를 생성하는 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-187">Click the button to generate an access token and access token secret.</span></span>

<span data-ttu-id="31746-188">다음 절차에 필요하기 때문에 이 정보를 보관해 두세요.</span><span class="sxs-lookup"><span data-stu-id="31746-188">Keep this information handy, because you will need it in the next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="31746-189">Twitter 응용 프로그램에 대한 키 및 비밀은 Twitter 계정에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-189">The keys and secrets for the Twitter application provide access to your Twitter account.</span></span> <span data-ttu-id="31746-190">이 정보는 Twitter 암호처럼 중요하게 취급합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-190">Treat this information as sensitive, the same as you do your Twitter password.</span></span> <span data-ttu-id="31746-191">예를 들어 이 정보를 다른 사람에게 제공하는 응용 프로그램에 포함하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="31746-191">For example, don't embed this information in an application that you give to others.</span></span> 


### <a name="configure-the-client-application"></a><span data-ttu-id="31746-192">클라이언트 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="31746-192">Configure the client application</span></span>
<span data-ttu-id="31746-193">Microsoft에서는 특정 항목 집합에 대한 트윗 이벤트를 수집하기 위해 [Twitter의 스트리밍 API](https://dev.twitter.com/streaming/overview)를 사용하여 Twitter 데이터에 연결하는 클라이언트 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-193">We've created a client application that connects to Twitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) to collect tweet events about a specific set of topics.</span></span> <span data-ttu-id="31746-194">응용 프로그램에서는 각 트윗에 다음 감정을 할당하는 [Sentiment140](http://help.sentiment140.com/) 오픈 소스 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-194">The application uses the [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns the following sentiment value to each tweet:</span></span>

* <span data-ttu-id="31746-195">0 = 부정적</span><span class="sxs-lookup"><span data-stu-id="31746-195">0 = negative</span></span>
* <span data-ttu-id="31746-196">2 = 중립</span><span class="sxs-lookup"><span data-stu-id="31746-196">2 = neutral</span></span>
* <span data-ttu-id="31746-197">4 = 긍정적</span><span class="sxs-lookup"><span data-stu-id="31746-197">4 = positive</span></span>

<span data-ttu-id="31746-198">트윗 이벤트에 감정 값이 할당된 후에는 이전에 만든 이벤트 허브에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-198">After the tweet events have been assigned a sentiment value, they are pushed to the event hub that you created earlier.</span></span>

<span data-ttu-id="31746-199">응용 프로그램이 실행되기 전에 Twitter 키 및 이벤트 허브 연결 문자열과 같은 사용자의 특정 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-199">Before the application runs, it requires certain information from you, like the Twitter keys and the event hub connection string.</span></span> <span data-ttu-id="31746-200">다음과 같은 방법으로 구성 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-200">You can provide the configuration information in these ways:</span></span>

* <span data-ttu-id="31746-201">응용 프로그램을 실행한 다음 응용 프로그램의 UI를 사용하여 키, 비밀 및 연결 문자열을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-201">Run the application, and then use the application's UI to enter the keys, secrets, and connection string.</span></span> <span data-ttu-id="31746-202">이 작업을 수행하는 경우 현재 세션에 대한 구성 정보가 사용되지만 저장되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-202">If you do this, the configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="31746-203">응용 프로그램의 .config 파일을 편집하고 여기서 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-203">Edit the application's .config file and set the values there.</span></span> <span data-ttu-id="31746-204">이 방법은 구성 정보를 유지하지만 잠재적으로 중요한 정보는 컴퓨터에 일반 텍스트에 저장됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-204">This approach persists the configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="31746-205">다음 절차에서는 두 가지 방법을 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-205">The following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="31746-206">필수 조건에 나와 있는 것처럼 [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) 응용 프로그램을 다운로드하여 압축을 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-206">Make sure you've downloaded and unzipped the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in the prerequisites.</span></span>

2. <span data-ttu-id="31746-207">실행시간(현재 세션에 대해서만)에 값을 설정하려면 `TwitterWPFClient.exe` 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-207">To set the values at run time (and only for the current session), run the `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="31746-208">응용 프로그램에 메시지가 표시되면 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-208">When the application prompts you, enter the following values:</span></span>

    * <span data-ttu-id="31746-209">Twitter 사용자 키(API 키)</span><span class="sxs-lookup"><span data-stu-id="31746-209">The Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="31746-210">Twitter 사용자 암호(API 암호)</span><span class="sxs-lookup"><span data-stu-id="31746-210">The Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="31746-211">Twitter 액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="31746-211">The Twitter Access Token.</span></span>
    * <span data-ttu-id="31746-212">Twitter 액세스 토큰 암호</span><span class="sxs-lookup"><span data-stu-id="31746-212">The Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="31746-213">이전에 저장한 연결 문자열 정보.</span><span class="sxs-lookup"><span data-stu-id="31746-213">The connection string information that you saved earlier.</span></span> <span data-ttu-id="31746-214">`EntityPath` 키-값 쌍을 제거한 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-214">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="31746-215">감정을 확인하려는 Twitter 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="31746-215">The Twitter keywords that you want to determine sentiment for.</span></span>

   ![TwitterWpfClient 응용 프로그램 실행 중, 가려진 설정 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="31746-217">값을 영구적으로 설정하려면 텍스트 편집기를 사용하여 TwitterWpfClient.exe.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31746-217">To set the values persistently, use a text editor to open the TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="31746-218">그런 다음 `<appSettings>` 요소에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-218">Then in the `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="31746-219">`oauth_consumer_key`를 Twitter 사용자 키(API 키)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-219">Set `oauth_consumer_key` to the Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="31746-220">`oauth_consumer_secret`을 Twitter 사용자 암호(API 암호)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-220">Set `oauth_consumer_secret` to the Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="31746-221">`oauth_token`을 Twitter 액세스 토큰으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-221">Set `oauth_token` to the Twitter Access Token.</span></span>
    * <span data-ttu-id="31746-222">`oauth_token_secret`을 Twitter 액세스 토큰 암호로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-222">Set `oauth_token_secret` to the Twitter Access Token Secret.</span></span>

    <span data-ttu-id="31746-223">뒷부분의 `<appSettings>` 요소에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-223">Later in the `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="31746-224">`EventHubName`을 이벤트 허브 이름으로 설정합니다(즉, 엔터티 경로 값).</span><span class="sxs-lookup"><span data-stu-id="31746-224">Set `EventHubName` to the event hub name (that is, to the value of the entity path).</span></span>
    * <span data-ttu-id="31746-225">`EventHubNameConnectionString`을 연결 문자열로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-225">Set `EventHubNameConnectionString` to the connection string.</span></span> <span data-ttu-id="31746-226">`EntityPath` 키-값 쌍을 제거한 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-226">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="31746-227">`<appSettings>` 섹션은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-227">The `<appSettings>` section looks like the following example.</span></span> <span data-ttu-id="31746-228">(이해를 돕고 보안을 위해 일부 줄을 래핑하고 일부 문자는 제거했습니다.)</span><span class="sxs-lookup"><span data-stu-id="31746-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![텍스트 편집기에서 TwitterWpfClient 응용 프로그램 구성 파일, Twitter 키 및 비밀, 이벤트 허브 연결 문자열 정보 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="31746-230">응용 프로그램을 아직 시작하지 않은 경우 지금 TwitterWpfClient.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-230">If you didn't already start the application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="31746-231">녹색 시작 단추를 선택하여 소셜 정서를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-231">Click the green start button to collect social sentiment.</span></span> <span data-ttu-id="31746-232">**CreatedAt**, **Topic** 및 **SentimentScore** 값이 이벤트 허브로 전송 중인 트윗 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-232">You see Tweet events with the **CreatedAt**, **Topic**, and **SentimentScore** values being sent to your event hub.</span></span>

    ![TwitterWpfClient 응용 프로그램 실행 중, 트윗 목록 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="31746-234">오류가 표시되고 창 하단에 트윗 스트림이 표시되지 않으면 키 및 비밀을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-234">If you see errors, and you don't see a stream of tweets displayed in the lower part of the window, double-check the keys and secrets.</span></span> <span data-ttu-id="31746-235">또한 연결 문자열을 확인합니다(`EntityPath` 키 및 값이 포함되지 않는지 확인).</span><span class="sxs-lookup"><span data-stu-id="31746-235">Also check the connection string (make sure that it does not include the `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="31746-236">스트림 분석 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="31746-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="31746-237">이제 Twitter에서 실시간으로 트윗 이벤트가 스트리밍되며 이러한 이벤트를 실시간으로 분석하도록 Stream Analytics 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job to analyze these events in real time.</span></span>

1. <span data-ttu-id="31746-238">Azure Portal에서 **새로 만들기** > **사물 인터넷** > **Stream Analytics 작업**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-238">In the Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="31746-239">작업 이름을 `socialtwitter-sa-job`으로 지정하고 구독, 리소스 그룹 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-239">Name the job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="31746-240">최상의 성능을 위해 동일한 지역에 작업 및 이벤트 허브를 배치하는 것이 좋으며 지역 간에 데이터를 전송하는 데 비용을 지불하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-240">It's a good idea to place the job and the event hub in the same region for best performance and so that you don't pay to transfer data between regions.</span></span>

    ![새 Stream Analytics 작업 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="31746-242">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-242">Click **Create**.</span></span>

    <span data-ttu-id="31746-243">작업이 만들어지고 포털에 작업 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-243">The job is created and the portal displays job details.</span></span>


## <a name="specify-the-job-input"></a><span data-ttu-id="31746-244">작업 입력 지정</span><span class="sxs-lookup"><span data-stu-id="31746-244">Specify the job input</span></span>

1. <span data-ttu-id="31746-245">Stream Analytics 작업에서 작업 블레이드의 중간에 있는 **작업 토폴로지** 아래에서 **입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-245">In your Stream Analytics job, under **Job Topology** in the middle of the job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="31746-246">**입력** 블레이드에서 **+&nbsp;추가**를 클릭한 후 블레이드를 다음 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="31746-246">In the **Inputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="31746-247">**입력 별칭**: 이름으로 `TwitterStream`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-247">**Input alias**: Use the name `TwitterStream`.</span></span> <span data-ttu-id="31746-248">다른 이름을 사용하는 경우 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="31746-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="31746-249">**원본 형식**: **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="31746-250">**원본**: **이벤트 허브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="31746-251">**가져오기 옵션**: **현재 구독의 이벤트 허브 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="31746-252">**서비스 버스 네임스페이스**: 이전에 만든 이벤트 허브 네임스페이스를 선택합니다(`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="31746-252">**Service bus namespace**: Select the event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="31746-253">**이벤트 허브**: 이전에 만든 이벤트 허브를 선택합니다(`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="31746-253">**Event hub**: Select the event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="31746-254">**이벤트 허브 정책 이름**: 앞부분에서 만든 액세스 정책을 선택합니다(`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="31746-254">**Event hub policy name**: Select the access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Streaming Analytics 작업에 대한 새 입력 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="31746-256">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-256">Click **Create**.</span></span>


## <a name="specify-the-job-query"></a><span data-ttu-id="31746-257">작업 쿼리 지정</span><span class="sxs-lookup"><span data-stu-id="31746-257">Specify the job query</span></span>

<span data-ttu-id="31746-258">Stream Analytics는 변환을 설명하는 간단하고 선언적인 쿼리 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="31746-259">이 언어에 대한 자세한 내용은 [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31746-259">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="31746-260">이 자습서에서는 Twitter 데이터에 대해 여러 쿼리를 작성하고 테스트하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="31746-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="31746-261">항목 간의 멘션 수를 비교하기 위해 [연속 창](https://msdn.microsoft.com/library/azure/dn835055.aspx)을 활용하여 5초마다 항목별 멘션 수를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-261">To compare the number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) to get the count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="31746-262">없는 경우 **입력** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-262">Close the **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="31746-263">작업 블레이드에서 **쿼리** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-263">In the job blade, click the **Query** box.</span></span> <span data-ttu-id="31746-264">Azure에서는 작업에 대해 구성된 입력 및 출력을 나열하고 데이터가 출력으로 전송됨에 따라 사용자가 입력 스트림을 변환하는 쿼리를 작성할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-264">Azure lists the inputs and outputs that are configured for the job, and lets you create a query that lets you transform the input stream as it is sent to the output.</span></span>

3. <span data-ttu-id="31746-265">TwitterWpfClient 응용 프로그램이 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-265">Make sure that the TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="31746-266">**쿼리** 블레이드에서 `TwitterStream` 입력 옆에 있는 점을 클릭한 후 **입력의 샘플 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-266">In the **Query** blade, click the dots next to the `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Streaming Analytics 작업 항목에 대해 샘플 데이터를 사용하는 메뉴 옵션, “입력의 샘플 데이터” 선택됨](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="31746-268">그러면 입력 스트림을 읽는 시간에 따라 정의된, 가져올 샘플 데이터의 양을 지정할 수 있는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="31746-268">This opens a blade that lets you specify how much sample data to get, defined in terms of how long to read the input stream.</span></span>

4. <span data-ttu-id="31746-269">**분**을 3으로 설정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-269">Set **Minutes** to 3 and then click **OK**.</span></span> 
    
    ![입력 스트림을 샘플링하는 옵션, “3분” 선택됨](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="31746-271">Azure에서는 입력 스트림의 3분 분량의 데이터를 샘플링하고 샘플 데이터가 준비되면 이를 사용자에게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="31746-271">Azure samples 3 minutes' worth of data from the input stream and notifies you when the sample data is ready.</span></span> <span data-ttu-id="31746-272">(짧은 시간이 소요됩니다.)</span><span class="sxs-lookup"><span data-stu-id="31746-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="31746-273">샘플 데이터는 임시로 저장되었다가 쿼리 창이 열려 있는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-273">The sample data is stored temporarily and is available while you have the query window open.</span></span> <span data-ttu-id="31746-274">쿼리 창을 닫으면 샘플 데이터가 무시되고 새로운 샘플 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-274">If you close the query window, the sample data is discarded, and you have to create a new set of sample data.</span></span> 

5. <span data-ttu-id="31746-275">코드 편집기에서 쿼리를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-275">Change the query in the code editor to the following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="31746-276">입력에 대한 별칭으로 `TwitterStream`을 사용하지 않은 경우 쿼리에서 `TwitterStream`에 대한 별칭을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-276">If didn't use `TwitterStream` as the alias for the input, substitute your alias for `TwitterStream` in the query.</span></span>  

    <span data-ttu-id="31746-277">이 쿼리에서는 **TIMESTAMP BY** 키워드를 사용하여 임시 계산에서 사용할 페이로드에 타임스탬프 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-277">This query uses the **TIMESTAMP BY** keyword to specify a timestamp field in the payload to be used in the temporal computation.</span></span> <span data-ttu-id="31746-278">이 필드를 지정하지 않으면 각 이벤트가 이벤트 허브에 도착한 시간을 사용하여 창 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-278">If this field isn't specified, the windowing operation is performed by using the time that each event arrived at the event hub.</span></span> <span data-ttu-id="31746-279">자세한 내용은 [Stream Analytics 쿼리 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)에서 “도착 시간과 응용 프로그램 시간” 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31746-279">Learn more in the "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="31746-280">또한 이 쿼리는 **System.Timestamp** 속성을 사용하여 각 창 끝부분의 타임스탬프에도 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-280">This query also accesses a timestamp for the end of each window by using the **System.Timestamp** property.</span></span>

5. <span data-ttu-id="31746-281">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-281">Click **Test**.</span></span> <span data-ttu-id="31746-282">샘플링된 데이터에 대해 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-282">The query runs against the data that you sampled.</span></span>
    
6. <span data-ttu-id="31746-283">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-283">Click **Save**.</span></span> <span data-ttu-id="31746-284">그러면 Streaming Analytics 작업의 일부로 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-284">This saves the query as part of the Streaming Analytics job.</span></span> <span data-ttu-id="31746-285">(샘플 데이터를 저장하지 않음)</span><span class="sxs-lookup"><span data-stu-id="31746-285">(It doesn't save the sample data.)</span></span>


## <a name="experiment-using-different-fields-from-the-stream"></a><span data-ttu-id="31746-286">스트림에서 서로 다른 필드를 사용하여 실험</span><span class="sxs-lookup"><span data-stu-id="31746-286">Experiment using different fields from the stream</span></span> 

<span data-ttu-id="31746-287">다음 표는 JSON 스트리밍 데이터의 일부인 필드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-287">The following table lists the fields that are part of the JSON streaming data.</span></span> <span data-ttu-id="31746-288">쿼리 편집기에서 마음껏 테스트하세요.</span><span class="sxs-lookup"><span data-stu-id="31746-288">Feel free to experiment in the query editor.</span></span>

|<span data-ttu-id="31746-289">JSON 속성</span><span class="sxs-lookup"><span data-stu-id="31746-289">JSON property</span></span> | <span data-ttu-id="31746-290">정의</span><span class="sxs-lookup"><span data-stu-id="31746-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="31746-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="31746-291">CreatedAt</span></span> | <span data-ttu-id="31746-292">트윗을 만든 시간</span><span class="sxs-lookup"><span data-stu-id="31746-292">The time that the tweet was created</span></span>|
|<span data-ttu-id="31746-293">항목</span><span class="sxs-lookup"><span data-stu-id="31746-293">Topic</span></span> | <span data-ttu-id="31746-294">지정된 키워드와 일치하는 항목</span><span class="sxs-lookup"><span data-stu-id="31746-294">The topic that matches the specified keyword</span></span>|
|<span data-ttu-id="31746-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="31746-295">SentimentScore</span></span> | <span data-ttu-id="31746-296">Sentiment140의 관심도</span><span class="sxs-lookup"><span data-stu-id="31746-296">The sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="31746-297">작성자</span><span class="sxs-lookup"><span data-stu-id="31746-297">Author</span></span> | <span data-ttu-id="31746-298">트윗을 보낸 Twitter 핸들</span><span class="sxs-lookup"><span data-stu-id="31746-298">The Twitter handle that sent the tweet</span></span>|
|<span data-ttu-id="31746-299">텍스트</span><span class="sxs-lookup"><span data-stu-id="31746-299">Text</span></span> | <span data-ttu-id="31746-300">트윗의 전체 본문</span><span class="sxs-lookup"><span data-stu-id="31746-300">The full body of the tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="31746-301">출력 싱크 만들기</span><span class="sxs-lookup"><span data-stu-id="31746-301">Create an output sink</span></span>

<span data-ttu-id="31746-302">이제 이벤트 스트림, 이벤트를 수집할 이벤트 허브 입력 및 스트림 변환을 수행할 쿼리를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-302">You have now defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream.</span></span> <span data-ttu-id="31746-303">마지막 단계는 작업에 대한 출력 싱크를 정의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31746-303">The last step is to define an output sink for the job.</span></span>  

<span data-ttu-id="31746-304">이 자습서에서는 작업 쿼리에서 집계된 트윗 이벤트를 Azure Blob Storage에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-304">In this tutorial, you write the aggregated tweet events from the job query to Azure Blob storage.</span></span>  <span data-ttu-id="31746-305">또한 특정 응용 프로그램 요구 사항에 따라 Azure SQL Database, Azure Table Storage, Event Hubs 또는 Power BI에 결과를 푸시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-305">You can also push your results to Azure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-the-job-output"></a><span data-ttu-id="31746-306">작업 출력 지정</span><span class="sxs-lookup"><span data-stu-id="31746-306">Specify the job output</span></span>

1. <span data-ttu-id="31746-307">**작업 토폴로지** 섹션에서 **출력** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-307">In the **Job Topology** section, click the **Output** box.</span></span> 

2. <span data-ttu-id="31746-308">**출력** 블레이드에서 **+&nbsp;추가**를 클릭한 후 블레이드를 다음 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="31746-308">In the **Outputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="31746-309">**출력 별칭**: 이름으로 `TwitterStream-Output`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-309">**Output alias**: Use the name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="31746-310">**싱크**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="31746-311">**가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="31746-312">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="31746-312">**Storage account**.</span></span> <span data-ttu-id="31746-313">**새 저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="31746-314">**저장소 계정**(두 번째 상자).</span><span class="sxs-lookup"><span data-stu-id="31746-314">**Storage account** (second box).</span></span> <span data-ttu-id="31746-315">`YOURNAMEsa`를 입력합니다. 여기서 `YOURNAME`은 사용자 이름 또는 다른 고유 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31746-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="31746-316">이름으로 소문자 및 숫자만 사용할 수 있으며 Azure 전체에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-316">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="31746-317">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="31746-317">**Container**.</span></span> <span data-ttu-id="31746-318">`socialtwitter`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="31746-319">저장소 계정 이름 및 컨테이너 이름을 다음과 같이 함께 사용하여 Blob Storage에 대한 URI를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-319">The storage account name and container name are used together to provide a URI for the blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Stream Analytics 작업에 대한 “새 출력” 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="31746-321">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-321">Click **Create**.</span></span> 

    <span data-ttu-id="31746-322">Azure에서 저장소 계정을 만들고 키를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-322">Azure creates the storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="31746-323">**출력** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-323">Close the **Outputs** blade.</span></span> 


## <a name="start-the-job"></a><span data-ttu-id="31746-324">작업 시작</span><span class="sxs-lookup"><span data-stu-id="31746-324">Start the job</span></span>

<span data-ttu-id="31746-325">작업 입력, 쿼리 및 출력이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="31746-326">Stream Analytics 작업을 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-326">You are ready to start the Stream Analytics job.</span></span>

1. <span data-ttu-id="31746-327">TwitterWpfClient 응용 프로그램이 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-327">Make sure that the TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="31746-328">작업 블레이드에서 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-328">In the job blade, click **Start**.</span></span>

    ![Stream Analytic 작업 시작](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="31746-330">**작업 시작** 블레이드에서 **작업 출력 시작 시간**으로 **지금**을 선택한 후 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-330">In the **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Stream Analytics 작업에 대한 “작업 시작” 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="31746-332">Azure에서 사용자에게 작업이 시작된 때를 알려주고 작업 블레이드에 상태가 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31746-332">Azure notifies you when the job has started, and in the job blade, the status is displayed as **Running**.</span></span>

    ![작업 실행 중](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="31746-334">정서 분석에 대한 출력 보기</span><span class="sxs-lookup"><span data-stu-id="31746-334">View output for sentiment analysis</span></span>

<span data-ttu-id="31746-335">작업이 실시간 Twitter 스트림을 실행 및 처리하면 감정 분석에 대한 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-335">After your job has started running and is processing the real-time Twitter stream, you can view the output for sentiment analysis.</span></span>

<span data-ttu-id="31746-336">[Azure Storage 탐색기](https://http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)와 같은 도구를 사용하여 작업 출력을 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) to view your job output in real time.</span></span> <span data-ttu-id="31746-337">여기에서 [Power BI](https://powerbi.com/)를 사용하여 다음 스크린샷과 같은 사용자 지정된 대시보드를 포함하도록 응용 프로그램을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31746-337">From here, you can use [Power BI](https://powerbi.com/) to extend your application to include a customized dashboard like the one shown in the following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-to-identify-trending-topics"></a><span data-ttu-id="31746-339">추세 항목을 확인하는 다른 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="31746-339">Create another query to identify trending topics</span></span>

<span data-ttu-id="31746-340">Twitter 감정을 이해하는 데 사용할 수 있는 다른 쿼리는 [슬라이딩 윈도우](https://msdn.microsoft.com/library/azure/dn835051.aspx)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-340">Another query you can use to understand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="31746-341">인기 항목을 식별하기 위해 지정된 기간 동안 멘션의 임계값을 초과한 항목을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31746-341">To identify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="31746-342">이 자습서에서는 마지막 5초 이내에 20번 넘게 멘션된 항목을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-342">For the purposes of this tutorial, you check for topics that are mentioned more than 20 times in the last 5 seconds.</span></span>

1. <span data-ttu-id="31746-343">작업 블레이드에서 **중지**를 클릭하여 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-343">In the job blade, click **Stop** to stop the job.</span></span> 

2. <span data-ttu-id="31746-344">**작업 토폴로지** 섹션에서 **쿼리** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-344">In the **Job Topology** section, click the **Query** box.</span></span> 

3. <span data-ttu-id="31746-345">쿼리를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-345">Change the query to the following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="31746-346">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-346">Click **Save**.</span></span>

5. <span data-ttu-id="31746-347">TwitterWpfClient 응용 프로그램이 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-347">Make sure that the TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="31746-348">**시작**을 클릭하여 새 쿼리로 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="31746-348">Click **Start** to restart the job using the new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="31746-349">지원 받기</span><span class="sxs-lookup"><span data-stu-id="31746-349">Get support</span></span>
<span data-ttu-id="31746-350">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31746-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31746-351">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31746-351">Next steps</span></span>
* [<span data-ttu-id="31746-352">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="31746-352">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="31746-353">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="31746-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="31746-354">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="31746-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="31746-355">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="31746-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="31746-356">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="31746-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
