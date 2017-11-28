---
title: "Azure Mobile Engagement 문제 해결 가이드 - API"
description: "Azure Mobile Engagement에 대한 문제 해결 가이드 - API"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: a7ae0a83046f2d67b790f672dcd3ae261987357a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="cb122-103">API 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="cb122-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="cb122-104">다음은 관리자가 API를 통해 Azure Mobile Engagement와 상호 작용하는 방법과 관련해서 발생할 수 있는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-104">The following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via the APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="cb122-105">구문 문제</span><span class="sxs-lookup"><span data-stu-id="cb122-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="cb122-106">문제</span><span class="sxs-lookup"><span data-stu-id="cb122-106">Issue</span></span>
* <span data-ttu-id="cb122-107">API 사용 시에 구문 오류가 발생하거나 예기치 않은 동작이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-107">Syntax Errors using the API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="cb122-108">원인</span><span class="sxs-lookup"><span data-stu-id="cb122-108">Causes</span></span>
* <span data-ttu-id="cb122-109">구문 문제</span><span class="sxs-lookup"><span data-stu-id="cb122-109">Syntax issues:</span></span>
  * <span data-ttu-id="cb122-110">사용 중인 특정 API의 구문을 점검하여 옵션이 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-110">Make sure to check the Syntax of the specific API you are using to confirm that the option is available.</span></span>
  * <span data-ttu-id="cb122-111">API 사용 시 일반적으로 발생하는 문제 중 하나는 도달률 API와 푸시 API를 혼동하는 것입니다. 대부분의 작업은 푸시 API가 아닌 도달률 API를 사용하여 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-111">A common issue with API usage is to confuse the Reach API and the Push API (most tasks should be performed with the Reach API instead of the Push API).</span></span> 
  * <span data-ttu-id="cb122-112">SDK 통합 및 API 사용과 관련하여 흔히 발생하는 또 다른 문제는 SDK 키와 API 키를 혼동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-112">Another common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>
  * <span data-ttu-id="cb122-113">API에 연결하는 스크립트는 최소 10분마다 데이터를 보내야 하며, 그렇지 않으면 연결 시간이 초과됩니다. 이러한 현상은 특히 데이터를 수신 대기하는 모니터 API 스크립트에서 일반적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-113">Scripts that connect to the APIs need to send data at least every 10 minutes or the connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="cb122-114">시간 초과를 방지하려면 서버에 대한 세션 연결을 유지하기 위해 스크립트가 10분마다 XMPP ping을 전송하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-114">To prevent timeouts, have your script send an XMPP ping every 10 minutes to keep the session alive with the server.</span></span>

### <a name="see-also"></a><span data-ttu-id="cb122-115">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cb122-115">See also</span></span>
* <span data-ttu-id="cb122-116">[API 설명서][Link 4]</span><span class="sxs-lookup"><span data-stu-id="cb122-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="cb122-117">XMPP 프로토콜 정보</span><span class="sxs-lookup"><span data-stu-id="cb122-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-to-use-the-api-to-perform-the-same-action-available-in-the-azure-mobile-engagement-ui"></a><span data-ttu-id="cb122-118">Azure Mobile Engagement UI에서 수행 가능한 것과 같은 작업을 API를 사용하여 수행할 수 없음</span><span class="sxs-lookup"><span data-stu-id="cb122-118">Unable to use the API to perform the same action available in the Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="cb122-119">문제</span><span class="sxs-lookup"><span data-stu-id="cb122-119">Issue</span></span>
* <span data-ttu-id="cb122-120">Azure Mobile Engagement UI에서 수행할 수 있는 작업을 관련 Azure Mobile Engagement API에서는 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-120">An action that works from the Azure Mobile Engagement UI doesn't work from the related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="cb122-121">원인</span><span class="sxs-lookup"><span data-stu-id="cb122-121">Causes</span></span>
* <span data-ttu-id="cb122-122">Azure Mobile Engagement UI에서 같은 작업을 수행할 수 있으면 Azure Mobile Engagement의 이 기능이 SDK와 올바르게 통합된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-122">Confirming that you can perform the same action from the Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with the SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="cb122-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cb122-123">See also</span></span>
* <span data-ttu-id="cb122-124">[UI 설명서][Link 1]</span><span class="sxs-lookup"><span data-stu-id="cb122-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="cb122-125">오류 메시지</span><span class="sxs-lookup"><span data-stu-id="cb122-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="cb122-126">문제</span><span class="sxs-lookup"><span data-stu-id="cb122-126">Issue</span></span>
* <span data-ttu-id="cb122-127">API 사용 시 런타임에 또는 로그에 오류 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-127">Error codes using the API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="cb122-128">원인</span><span class="sxs-lookup"><span data-stu-id="cb122-128">Causes</span></span>
* <span data-ttu-id="cb122-129">아래에는 참조 및 임시 문제 해결에 사용할 수 있도록 일반적인 API 상태 코드 번호의 통합 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from the current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in the response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). The parameters provided to the API or service are invalid. In this case, the HTTP response will embed more details. Make sure to test for the MIME type of the response as the payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check the AppID and SDK key).
        402        Billing lock. The application is either off its quotas or is currently in a bad billing state.
        403        The application is not enabled or the specific API is disabled for this application.
        403        Unauthorized access to the project or application, invalid access key (the key must match the one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), the suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and the campaign’s property named, manual Push must be set to true.
        403        The email address is already associated to another account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        The email address is not associated with an account. Please create or update the account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying to edit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for the first time.
        409        Name already associated to a different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or the period is too large to be displayed (the server didn’t retrieve the analytics because the user request is for a period that is too large).
        503        Analytics not available yet (the requested information is not computed yet for an application).
        504        The server was not able to handle your request in a reasonable time (if you make multiple calls to an API very quickly, try to make one call at a time and spread the calls out over time).

### <a name="see-also"></a><span data-ttu-id="cb122-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cb122-130">See also</span></span>
* <span data-ttu-id="cb122-131">[API 설명서 - 각 특정 API에 대한 상세 오류 정보][Link 4]</span><span class="sxs-lookup"><span data-stu-id="cb122-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="cb122-132">자동 오류</span><span class="sxs-lookup"><span data-stu-id="cb122-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="cb122-133">문제</span><span class="sxs-lookup"><span data-stu-id="cb122-133">Issue</span></span>
* <span data-ttu-id="cb122-134">API 작업이 실패하고 런타임이나 로그에 오류 메시지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="cb122-135">원인</span><span class="sxs-lookup"><span data-stu-id="cb122-135">Causes</span></span>
* <span data-ttu-id="cb122-136">대부분의 항목은 올바르게 통합되지 않은 경우 Azure Mobile Engagement UI에서 사용되지 않도록 설정되지만 API에서는 자동으로 오류가 발생하므로 UI의 같은 기능을 테스트하여 작동하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-136">Many items will be disabled in the Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from the API, so remember to test the same functionality from the UI to see if it works.</span></span>
* <span data-ttu-id="cb122-137">Azure Mobile Engagement 및 Azure Mobile Engagement에서 사용하려는 대다수의 고급 기능은 별도의 단계를 통해 SDK와 함께 앱에 개별적으로 통합해야 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="cb122-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting to use, need to be individually integrated into your app with the SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="cb122-138">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cb122-138">See also</span></span>
* <span data-ttu-id="cb122-139">[문제 해결 가이드 - SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="cb122-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

