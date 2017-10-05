---
title: "Logic Apps 커넥터 개요 | Microsoft Docs"
description: "논리 앱에서 사용할 수 있는 커넥터의 개요"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: 9cbb258ae9e32549669623e6824dd9b18fa1f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-connectors-in-a-logic-app"></a><span data-ttu-id="4f83e-103">논리 앱에서 커넥터 사용</span><span class="sxs-lookup"><span data-stu-id="4f83e-103">Using connectors in a logic app</span></span>
<span data-ttu-id="4f83e-104">커넥터는 서비스, 프로토콜 및 플랫폼에 걸쳐 이벤트, 데이터 및 작업에 빠르게 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-104">Connectors provide quick access to events, data, and actions across services, protocols, and platforms.</span></span>  <span data-ttu-id="4f83e-105">논리 앱이 지원하는 커넥터의 전체 목록은 [여기에서 찾을 수 있습니다](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4f83e-105">The full list of connectors that Logic Apps supports can [be found here](apis-list.md).</span></span>  <span data-ttu-id="4f83e-106">커넥터는 논리 앱에서 트리거 또는 작업으로 사용할 수 있으며 사용하기 위해 구성된 *연결* 이 필요합니다(예: 사용자 대신 액세스하거나 게시할 수 있는 권한을 Twitter 계정에 부여).</span><span class="sxs-lookup"><span data-stu-id="4f83e-106">Connectors can be used as a trigger or an action in a logic app, and may require a configured *connection* to use (for example: authorizing a Twitter account to access or post on your behalf).</span></span>

## <a name="basics"></a><span data-ttu-id="4f83e-107">기본 사항</span><span class="sxs-lookup"><span data-stu-id="4f83e-107">Basics</span></span>
<span data-ttu-id="4f83e-108">커넥터는 Dynamics, Azure, Salesforce, [등](apis-list.md)의 다른 서비스와 통합하기 위해 논리 앱의 일부로 액세스할 수 있는 호스트된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-108">Connectors are hosted services you can access as part of a logic app to integrate with other services like Dynamics, Azure, Salesforce, [and more](apis-list.md).</span></span>  <span data-ttu-id="4f83e-109">이러한 커넥터는 Microsoft에서 배포 및 관리하므로, 규모, 처리량 및 보안이 관리되는 통합 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-109">They are deployed and managed by Microsoft, so you can build your integration workflows with scale, throughput, and security taken care of.</span></span>  <span data-ttu-id="4f83e-110">**Microsoft 관리 API 표시**에서 커넥터 작업 또는 트리거를 검색하고 선택하여 논리 앱에 커넥터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-110">You can add a connector to a logic app by searching and selecting a connector action or trigger under **Show Microsoft managed APIs**.</span></span>

![트리거를 선택하기 위한 작업 메뉴][1]

<span data-ttu-id="4f83e-112">각 커넥터 작업 또는 트리거에는 구성할 속성 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-112">Each connector action or trigger will have its set of properties to configure.</span></span>  <span data-ttu-id="4f83e-113">정보 단추를 클릭하여 작업에 대해 자세히 알아보거나 해당 설명서에서 [자세한 내용을 확인](apis-list.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-113">You can click on the info buttons to learn more about action, or reference its documentation [to learn more](apis-list.md).</span></span>

<span data-ttu-id="4f83e-114">아직 커넥터가 아닌 서비스 또는 API와 통합하려면 [사용자 지정 커넥터](../logic-apps/logic-apps-create-api-app.md) 를 통해 논리 앱을 확장하거나 HTTP와 같은 프로토콜을 통해 서비스를 직접 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-114">If you want to integrate with a service or API that isn't yet a connector, you can also extend logic apps through a [custom connector](../logic-apps/logic-apps-create-api-app.md) or just call directly to the service over a protocol like HTTP.</span></span>

## <a name="triggers"></a><span data-ttu-id="4f83e-115">트리거</span><span class="sxs-lookup"><span data-stu-id="4f83e-115">Triggers</span></span>
<span data-ttu-id="4f83e-116">일부 커넥터에는 트리거가 있습니다. 이것은 해당 커넥터의 이벤트가 논리 앱을 실행하고 트리거의 일부로 데이터를 전달함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-116">Some connectors have a trigger, which means an event from that connector will fire a logic app and pass in any data as part of the trigger.</span></span>  <span data-ttu-id="4f83e-117">트리거는 항상 논리 앱의 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-117">A trigger is always the first step in a logic app.</span></span>  <span data-ttu-id="4f83e-118">인기 있는 트리거에는 다음과 같은 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-118">Popular triggers include operations like:</span></span>

* <span data-ttu-id="4f83e-119">되풀이 - 1시간마다 실행</span><span class="sxs-lookup"><span data-stu-id="4f83e-119">Recurrence - run every hour</span></span>
* <span data-ttu-id="4f83e-120">HTTP 요청을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="4f83e-120">When an HTTP request is received</span></span>
* <span data-ttu-id="4f83e-121">큐에 항목이 추가될 때</span><span class="sxs-lookup"><span data-stu-id="4f83e-121">When an item is added to a queue</span></span>
* <span data-ttu-id="4f83e-122">전자 메일이 수신될 때</span><span class="sxs-lookup"><span data-stu-id="4f83e-122">When an email is received</span></span>

<span data-ttu-id="4f83e-123">논리 앱에 대한 알림을 통해 이벤트가 발생하는 즉시 실행되는 트리거도 있고, 논리 앱이 서비스에서 이벤트를 확인하는 빈도(최대 15초 간격)에 대한 되풀이 간격이 구성되어야 하는 트리거도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-123">Some triggers will fire the instant an event happens through a notification to the logic app, and others will need a recurrence interval configured on how often the logic app will check the service for an event (up to every 15 seconds).</span></span>  

<span data-ttu-id="4f83e-124">이벤트가 수신되면 논리 앱이 실행되고 워크플로의 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-124">Once an event is received, the logic app run will fire and the actions in the workflow will start.</span></span>  <span data-ttu-id="4f83e-125">워크플로 전체에서 트리거의 데이터에 액세스할 수도 있습니다(예를 들어 '새 트윗' 트리거는 실행에 트윗을 전달함).</span><span class="sxs-lookup"><span data-stu-id="4f83e-125">You will also be able to access any data from the trigger throughout the workflow (for example the 'On a new tweet' trigger will pass the tweet into the run).</span></span>

## <a name="actions"></a><span data-ttu-id="4f83e-126">동작</span><span class="sxs-lookup"><span data-stu-id="4f83e-126">Actions</span></span>
<span data-ttu-id="4f83e-127">대부분의 커넥터에는 워크플로의 일부로 실행할 수 있는 작업이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-127">Most connectors have one or many actions that can be executed as part of the workflow.</span></span>  <span data-ttu-id="4f83e-128">작업은 트리거에서 실행이 발생한 후에 발생하는 모든 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-128">Actions are any steps that happen after the run has fired from a trigger.</span></span>  <span data-ttu-id="4f83e-129">작업을 추가하려면 **새 단계** 단추를 클릭하고 사용하려는 커넥터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-129">To add an action click the **New Step** button and search for the connector you want to use.</span></span>  <span data-ttu-id="4f83e-130">일단 선택하면(필요할 수 있는 모든 [연결](#connections) 을 구성한 후) 구성할 수 있는 작업 카드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-130">Once selected (and after configuring any [connections](#connections) that may be required) you will see the action card you can configure.</span></span>  <span data-ttu-id="4f83e-131">출력을 위해 토큰 중 하나를 클릭하여 이전 단계의 데이터를 선택하거나 필요에 따라 다른 구성을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-131">You can select data from previous steps by clicking on any of the tokens for outputs, or enter in any other configuration as needed.</span></span>

![커넥터 작업 구성][2]

## <a name="connections"></a><span data-ttu-id="4f83e-133">연결</span><span class="sxs-lookup"><span data-stu-id="4f83e-133">Connections</span></span>
<span data-ttu-id="4f83e-134">커넥터를 사용하려면 먼저 *연결* 을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-134">Most connectors require you to configure a *connection* before you can use the connector.</span></span>  <span data-ttu-id="4f83e-135">*연결* 은 커넥터에 액세스하는 데 필요한 모든 로그인 또는 연결 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-135">A *connection* is any login or connection configuration needed to access the connector.</span></span>  <span data-ttu-id="4f83e-136">OAuth를 사용하는 커넥터의 경우 연결을 만드는 것은 액세스 토큰을 암호화한 후 Azure 암호 저장소에 안전하게 저장할 수 있는 서비스(예: Office 365, Salesforce 또는 GitHub)에 로그인하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-136">For connectors that use OAuth, create a connection means signing into the service (like Office 365, Salesforce, or GitHub) where your access token can be encrypted and securely stored in an Azure secret store.</span></span>  <span data-ttu-id="4f83e-137">다른 커넥터(예: FTP 및 SQL)에는 서버 주소, 사용자 이름 및 암호와 같은 구성을 포함하는 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-137">Other connectors (like FTP and SQL) require a connection that contains configuration like server address, username, and password.</span></span>  <span data-ttu-id="4f83e-138">이러한 연결 구성 세부 정보 또한 암호화된 후 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-138">These connection configuration details are also encrypted and securely stored.</span></span>  <span data-ttu-id="4f83e-139">연결은 서비스가 허용하는 한 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-139">Connections will be able to access the service for as long as the service allows.</span></span>  <span data-ttu-id="4f83e-140">Azure Active Directory OAuth 연결(예: Office 365 및 Dynamics)의 경우 액세스 토큰을 무제한으로 계속 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-140">For Azure Active Directory OAuth connections (like Office 365 and Dynamics) we can continue to refresh the access token indefinitely.</span></span>  <span data-ttu-id="4f83e-141">다른 서비스는 토큰을 새로 고치지 않고 사용할 수 있는 기간이 한정되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-141">Other services may put limits on how long we can use a token without it being refreshed.</span></span>  <span data-ttu-id="4f83e-142">일반적으로 암호 변경과 같은 특정 작업을 수행하면 모든 액세스 토큰이 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-142">In general certain actions like changing a password will invalidate all access tokens.</span></span>  

<span data-ttu-id="4f83e-143">Azure에서 **찾아보기**를 클릭하고 **API 연결**을 선택하여 연결을 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-143">Connections can be viewed and managed in Azure by clicking **Browse** and selecting **API Connections**.</span></span>  <span data-ttu-id="4f83e-144">API 연결 리소스에서 만든 연결을 보거나, 편집하거나, 업데이트하거나, 권한을 다시 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f83e-144">From the API Connections resource you can view, edit, update, or re-authorize any connections you have created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f83e-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f83e-145">Next Steps</span></span>
* [<span data-ttu-id="4f83e-146">첫 번째 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="4f83e-146">Create your first logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="4f83e-147">논리 앱의 일반 용도 및 예제에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="4f83e-147">Learn common uses and examples of logic apps</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="4f83e-148">엔터프라이즈 통합 트리거 및 작업 시작</span><span class="sxs-lookup"><span data-stu-id="4f83e-148">Get started with enterprise integration triggers and actions</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
