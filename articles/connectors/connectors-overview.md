---
title: "논리 앱 커넥터의 aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a><span data-ttu-id="57210-103">논리 앱에서 커넥터 사용</span><span class="sxs-lookup"><span data-stu-id="57210-103">Using connectors in a logic app</span></span>
<span data-ttu-id="57210-104">커넥터는 서비스, 프로토콜 및 플랫폼 간에 빠르게 액세스 tooevents, 데이터 및 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-104">Connectors provide quick access tooevents, data, and actions across services, protocols, and platforms.</span></span>  <span data-ttu-id="57210-105">커넥터를 지 원하는 논리 앱의 전체 목록은 hello 수 [´ ֿ ´](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-105">hello full list of connectors that Logic Apps supports can [be found here](apis-list.md).</span></span>  <span data-ttu-id="57210-106">커넥터는 트리거 또는 논리 앱에서 작업으로 사용할 수 있습니다 및 구성 해야 할 수 있습니다 *연결* toouse (예: tooaccess 계정 또는 사용자 대신 post는 Twitter 권한 부여) 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-106">Connectors can be used as a trigger or an action in a logic app, and may require a configured *connection* toouse (for example: authorizing a Twitter account tooaccess or post on your behalf).</span></span>

## <a name="basics"></a><span data-ttu-id="57210-107">기본 사항</span><span class="sxs-lookup"><span data-stu-id="57210-107">Basics</span></span>
<span data-ttu-id="57210-108">Dynamics, Azure, Salesforce와 같은 다른 서비스와 논리 앱 toointegrate의 일환으로 액세스할 수는 호스팅된 서비스에 따르면 커넥터는 [많은](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-108">Connectors are hosted services you can access as part of a logic app toointegrate with other services like Dynamics, Azure, Salesforce, [and more](apis-list.md).</span></span>  <span data-ttu-id="57210-109">이러한 커넥터는 Microsoft에서 배포 및 관리하므로, 규모, 처리량 및 보안이 관리되는 통합 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-109">They are deployed and managed by Microsoft, so you can build your integration workflows with scale, throughput, and security taken care of.</span></span>  <span data-ttu-id="57210-110">검색 및 커넥터 작업을 선택 하 여 커넥터 tooa 논리 앱을 추가 하거나 아래에서 트리거할 수 있습니다 **표시 Microsoft 관리 되는 Api**합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-110">You can add a connector tooa logic app by searching and selecting a connector action or trigger under **Show Microsoft managed APIs**.</span></span>

![트리거를 선택하기 위한 작업 메뉴][1]

<span data-ttu-id="57210-112">각 커넥터 동작이 나 트리거 속성 tooconfigure 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-112">Each connector action or trigger will have its set of properties tooconfigure.</span></span>  <span data-ttu-id="57210-113">작업에 대 한 hello 정보 단추 toolearn에서을 클릭 하거나 해당 설명서를 참조할 수 있습니다 [자세한 toolearn](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-113">You can click on hello info buttons toolearn more about action, or reference its documentation [toolearn more](apis-list.md).</span></span>

<span data-ttu-id="57210-114">서비스 또는 하지 않은 API 아직 커넥터와 toointegrate 원하는 논리 앱을 통해 확장할 수도 있습니다는 [사용자 지정 커넥터](../logic-apps/logic-apps-create-api-app.md) 또는 HTTP와 같은 프로토콜을 통해 toohello 서비스 직접 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-114">If you want toointegrate with a service or API that isn't yet a connector, you can also extend logic apps through a [custom connector](../logic-apps/logic-apps-create-api-app.md) or just call directly toohello service over a protocol like HTTP.</span></span>

## <a name="triggers"></a><span data-ttu-id="57210-115">트리거</span><span class="sxs-lookup"><span data-stu-id="57210-115">Triggers</span></span>
<span data-ttu-id="57210-116">일부 연결선은 트리거, 즉 해당 커넥터에서 이벤트는 논리 앱을 실행 하 고 hello 트리거의 일부로 모든 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-116">Some connectors have a trigger, which means an event from that connector will fire a logic app and pass in any data as part of hello trigger.</span></span>  <span data-ttu-id="57210-117">트리거는 항상 hello 논리 앱의 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="57210-117">A trigger is always hello first step in a logic app.</span></span>  <span data-ttu-id="57210-118">인기 있는 트리거에는 다음과 같은 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57210-118">Popular triggers include operations like:</span></span>

* <span data-ttu-id="57210-119">되풀이 - 1시간마다 실행</span><span class="sxs-lookup"><span data-stu-id="57210-119">Recurrence - run every hour</span></span>
* <span data-ttu-id="57210-120">HTTP 요청을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="57210-120">When an HTTP request is received</span></span>
* <span data-ttu-id="57210-121">Tooa 큐는 항목을 추가 하는 경우</span><span class="sxs-lookup"><span data-stu-id="57210-121">When an item is added tooa queue</span></span>
* <span data-ttu-id="57210-122">전자 메일이 수신될 때</span><span class="sxs-lookup"><span data-stu-id="57210-122">When an email is received</span></span>

<span data-ttu-id="57210-123">일부 트리거는 이벤트 알림 toohello 논리 앱을 통해 수행 되며 얼마나 자주 hello 논리 앱 확인 합니다 (위쪽 tooevery 15 초) 이벤트에 대 한 hello 서비스에 구성 된 되풀이 간격 할 다른 인스턴트 hello를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57210-123">Some triggers will fire hello instant an event happens through a notification toohello logic app, and others will need a recurrence interval configured on how often hello logic app will check hello service for an event (up tooevery 15 seconds).</span></span>  

<span data-ttu-id="57210-124">이벤트가 수신 되 면 hello 논리 앱을 실행 하면 발생 하 고 hello 워크플로에서 hello 작업 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57210-124">Once an event is received, hello logic app run will fire and hello actions in hello workflow will start.</span></span>  <span data-ttu-id="57210-125">Hello에서 모든 데이터가 hello 워크플로 전체에서 트리거할 수 tooaccess 수도 있습니다 ('에서 새 윗' 예제 hello에 대 한 트리거는 hello 트 윗에 전달할 hello 실행).</span><span class="sxs-lookup"><span data-stu-id="57210-125">You will also be able tooaccess any data from hello trigger throughout hello workflow (for example hello 'On a new tweet' trigger will pass hello tweet into hello run).</span></span>

## <a name="actions"></a><span data-ttu-id="57210-126">작업</span><span class="sxs-lookup"><span data-stu-id="57210-126">Actions</span></span>
<span data-ttu-id="57210-127">대부분의 커넥터에는 hello 워크플로의 일부로 실행 될 수 있는 하나 이상의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-127">Most connectors have one or many actions that can be executed as part of hello workflow.</span></span>  <span data-ttu-id="57210-128">작업은 hello 실행 한 후 발생 하는 단계는 트리거에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-128">Actions are any steps that happen after hello run has fired from a trigger.</span></span>  <span data-ttu-id="57210-129">동작 tooadd 클릭 hello **새 단계** 단추와 검색에 대 한 hello toouse 원하는 연결선입니다.</span><span class="sxs-lookup"><span data-stu-id="57210-129">tooadd an action click hello **New Step** button and search for hello connector you want toouse.</span></span>  <span data-ttu-id="57210-130">선택 하면 (및 모든를 구성한 후 [연결](#connections) 필요할 수 있습니다) 구성할 수 있습니다 hello 동작 카드 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57210-130">Once selected (and after configuring any [connections](#connections) that may be required) you will see hello action card you can configure.</span></span>  <span data-ttu-id="57210-131">출력에 대 한 hello 토큰 중 하나를 클릭 하 여 이전 단계에서 데이터를 선택 하거나 필요에 따라 다른 구성에 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-131">You can select data from previous steps by clicking on any of hello tokens for outputs, or enter in any other configuration as needed.</span></span>

![커넥터 작업 구성][2]

## <a name="connections"></a><span data-ttu-id="57210-133">연결</span><span class="sxs-lookup"><span data-stu-id="57210-133">Connections</span></span>
<span data-ttu-id="57210-134">대부분의 커넥터 필요 tooconfigure는 *연결* hello 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-134">Most connectors require you tooconfigure a *connection* before you can use hello connector.</span></span>  <span data-ttu-id="57210-135">A *연결* 모든 로그인 또는 연결 구성이 tooaccess hello 커넥터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-135">A *connection* is any login or connection configuration needed tooaccess hello connector.</span></span>  <span data-ttu-id="57210-136">OAuth를 사용 하 여, 연결 하는 커넥터에 대 한 (예: Office 365, Salesforce, 또는 GitHub) 액세스 토큰 암호화 끌어다 비밀 Azure 저장소에 안전 하 게 저장할 수 있는 hello 서비스에 로그인을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-136">For connectors that use OAuth, create a connection means signing into hello service (like Office 365, Salesforce, or GitHub) where your access token can be encrypted and securely stored in an Azure secret store.</span></span>  <span data-ttu-id="57210-137">다른 커넥터(예: FTP 및 SQL)에는 서버 주소, 사용자 이름 및 암호와 같은 구성을 포함하는 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-137">Other connectors (like FTP and SQL) require a connection that contains configuration like server address, username, and password.</span></span>  <span data-ttu-id="57210-138">이러한 연결 구성 세부 정보 또한 암호화된 후 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="57210-138">These connection configuration details are also encrypted and securely stored.</span></span>  <span data-ttu-id="57210-139">연결이 허용 됩니다 수 tooaccess hello 서비스에 대 한 상태로 hello 서비스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-139">Connections will be able tooaccess hello service for as long as hello service allows.</span></span>  <span data-ttu-id="57210-140">Azure Active Directory OAuth 연결 (예: Office 365, Dynamics)에 대 한 toorefresh hello 액세스 토큰을 무기한 계속 수 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-140">For Azure Active Directory OAuth connections (like Office 365 and Dynamics) we can continue toorefresh hello access token indefinitely.</span></span>  <span data-ttu-id="57210-141">다른 서비스는 토큰을 새로 고치지 않고 사용할 수 있는 기간이 한정되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-141">Other services may put limits on how long we can use a token without it being refreshed.</span></span>  <span data-ttu-id="57210-142">일반적으로 암호 변경과 같은 특정 작업을 수행하면 모든 액세스 토큰이 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="57210-142">In general certain actions like changing a password will invalidate all access tokens.</span></span>  

<span data-ttu-id="57210-143">Azure에서 **찾아보기**를 클릭하고 **API 연결**을 선택하여 연결을 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57210-143">Connections can be viewed and managed in Azure by clicking **Browse** and selecting **API Connections**.</span></span>  <span data-ttu-id="57210-144">Hello API 연결 리소스에서에서 있습니다 수 보기, 편집, 업데이트 또는 다시 만든 모든 연결을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="57210-144">From hello API Connections resource you can view, edit, update, or re-authorize any connections you have created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57210-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57210-145">Next Steps</span></span>
* [<span data-ttu-id="57210-146">첫 번째 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="57210-146">Create your first logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="57210-147">논리 앱의 일반 용도 및 예제에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="57210-147">Learn common uses and examples of logic apps</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="57210-148">엔터프라이즈 통합 트리거 및 작업 시작</span><span class="sxs-lookup"><span data-stu-id="57210-148">Get started with enterprise integration triggers and actions</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
