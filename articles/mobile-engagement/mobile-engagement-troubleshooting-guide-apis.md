---
title: "Mobile Engagement 문제 해결 가이드-aaaAzure Api"
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
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="4217a-103">API 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="4217a-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="4217a-104">hello 다음은 hello Api 통해 관리자가 Azure Mobile Engagement 상호 작용 하는 방법에 발생할 수 있는 관련 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-104">hello following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via hello APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="4217a-105">구문 문제</span><span class="sxs-lookup"><span data-stu-id="4217a-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="4217a-106">문제</span><span class="sxs-lookup"><span data-stu-id="4217a-106">Issue</span></span>
* <span data-ttu-id="4217a-107">Hello API (또는 예기치 않은 동작이)를 사용 하 여 구문 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-107">Syntax Errors using hello API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="4217a-108">원인</span><span class="sxs-lookup"><span data-stu-id="4217a-108">Causes</span></span>
* <span data-ttu-id="4217a-109">구문 문제</span><span class="sxs-lookup"><span data-stu-id="4217a-109">Syntax issues:</span></span>
  * <span data-ttu-id="4217a-110">있는지 toocheck hello hello 특정 API 사용 하는의 구문을 확인 하십시오 옵션 hello tooconfirm를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-110">Make sure toocheck hello Syntax of hello specific API you are using tooconfirm that hello option is available.</span></span>
  * <span data-ttu-id="4217a-111">API 사용 된 일반적인 문제에 tooconfuse hello Reach API 이며 hello 푸시 API (대부분의 작업 푸시 API hello 대신 hello Reach API로 수행 해야) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-111">A common issue with API usage is tooconfuse hello Reach API and hello Push API (most tasks should be performed with hello Reach API instead of hello Push API).</span></span> 
  * <span data-ttu-id="4217a-112">SDK 통합 및 API 사용 관련 된 일반적인 문제도 tooconfuse hello SDK 키 이며 hello API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-112">Another common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>
  * <span data-ttu-id="4217a-113">Toohello Api를 연결 하는 스크립트에는 toosend 데이터가 필요할 매 10 분 또는 hello 연결 (특히, 데이터에 대 한 수신 대기 하는 모니터 API 스크립트에서 공통) 시간 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-113">Scripts that connect toohello APIs need toosend data at least every 10 minutes or hello connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="4217a-114">tooprevent 제한 시간, 있어야 스크립트 보내기 XMPP ping 모든 10 분 tookeep hello 세션 hello 서버와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-114">tooprevent timeouts, have your script send an XMPP ping every 10 minutes tookeep hello session alive with hello server.</span></span>

### <a name="see-also"></a><span data-ttu-id="4217a-115">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4217a-115">See also</span></span>
* <span data-ttu-id="4217a-116">[API 설명서][Link 4]</span><span class="sxs-lookup"><span data-stu-id="4217a-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="4217a-117">XMPP 프로토콜 정보</span><span class="sxs-lookup"><span data-stu-id="4217a-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a><span data-ttu-id="4217a-118">없습니다 toouse hello API tooperform hello hello Azure Mobile Engagement UI에서에서 사용할 수 있는 동일한 작업</span><span class="sxs-lookup"><span data-stu-id="4217a-118">Unable toouse hello API tooperform hello same action available in hello Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="4217a-119">문제</span><span class="sxs-lookup"><span data-stu-id="4217a-119">Issue</span></span>
* <span data-ttu-id="4217a-120">Azure Mobile Engagement UI hello에서 작동 하지 않는 hello에서 작동 하는 작업 관련 Azure Mobile Engagement API입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-120">An action that works from hello Azure Mobile Engagement UI doesn't work from hello related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="4217a-121">원인</span><span class="sxs-lookup"><span data-stu-id="4217a-121">Causes</span></span>
* <span data-ttu-id="4217a-122">SDK hello hello와 Azure Mobile Engagement의이 기능을 통합 올바르게 한 hello Azure Mobile Engagement UI에서에서 동일한 작업 표시를 수행할 수 있음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-122">Confirming that you can perform hello same action from hello Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with hello SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="4217a-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4217a-123">See also</span></span>
* <span data-ttu-id="4217a-124">[UI 설명서][Link 1]</span><span class="sxs-lookup"><span data-stu-id="4217a-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="4217a-125">오류 메시지</span><span class="sxs-lookup"><span data-stu-id="4217a-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="4217a-126">문제</span><span class="sxs-lookup"><span data-stu-id="4217a-126">Issue</span></span>
* <span data-ttu-id="4217a-127">런타임 시 또는 로그에 표시 하는 hello API를 사용 하는 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-127">Error codes using hello API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="4217a-128">원인</span><span class="sxs-lookup"><span data-stu-id="4217a-128">Causes</span></span>
* <span data-ttu-id="4217a-129">아래에는 참조 및 임시 문제 해결에 사용할 수 있도록 일반적인 API 상태 코드 번호의 통합 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a><span data-ttu-id="4217a-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4217a-130">See also</span></span>
* <span data-ttu-id="4217a-131">[API 설명서 - 각 특정 API에 대한 상세 오류 정보][Link 4]</span><span class="sxs-lookup"><span data-stu-id="4217a-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="4217a-132">자동 오류</span><span class="sxs-lookup"><span data-stu-id="4217a-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="4217a-133">문제</span><span class="sxs-lookup"><span data-stu-id="4217a-133">Issue</span></span>
* <span data-ttu-id="4217a-134">API 작업이 실패하고 런타임이나 로그에 오류 메시지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="4217a-135">원인</span><span class="sxs-lookup"><span data-stu-id="4217a-135">Causes</span></span>
* <span data-ttu-id="4217a-136">Azure Mobile Engagement UI 제대로 통합 되지 않지만 hello API에서에서 자동으로 실패 합니다 경우 따라서 프로그램인 hello 항목 수 없게 됩니다 맞으면 tootest hello hello UI toosee에서 동일한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-136">Many items will be disabled in hello Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from hello API, so remember tootest hello same functionality from hello UI toosee if it works.</span></span>
* <span data-ttu-id="4217a-137">Azure Mobile Engagement 및 toouse, 필요 toobe 사용 하기 전에 hello SDK 사용 하 여 앱에 별도 단계로 개별적으로 통합 하려고 하는 Azure Mobile Engagement의 여러 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4217a-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting toouse, need toobe individually integrated into your app with hello SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="4217a-138">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4217a-138">See also</span></span>
* <span data-ttu-id="4217a-139">[문제 해결 가이드 - SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="4217a-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

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

