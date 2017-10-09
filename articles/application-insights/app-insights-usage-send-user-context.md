---
title: "aaaSending 사용자 컨텍스트 tooenable 사용 환경을 Azure Application Insights | Microsoft Docs"
description: "Application Insights에서 각각에 고유하고 영구적인 ID 문자열을 할당한 후 사용자가 서비스를 통해 이동하는 방식을 추적합니다."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="654d5-103">보내는 사용자 컨텍스트 tooenable 사용 환경을 Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="654d5-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="654d5-104">사용자 추적</span><span class="sxs-lookup"><span data-stu-id="654d5-104">Tracking users</span></span>

<span data-ttu-id="654d5-105">Application Insights toomonitor 수 있으며 특정 제품 사용 도구 집합을 통해 사용자 추적:</span><span class="sxs-lookup"><span data-stu-id="654d5-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="654d5-106">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="654d5-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="654d5-107">깔때기</span><span class="sxs-lookup"><span data-stu-id="654d5-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="654d5-108">보존</span><span class="sxs-lookup"><span data-stu-id="654d5-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="654d5-109">코호트</span><span class="sxs-lookup"><span data-stu-id="654d5-109">Cohorts</span></span>
* [<span data-ttu-id="654d5-110">통합 문서</span><span class="sxs-lookup"><span data-stu-id="654d5-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="654d5-111">시간이 지남에 따라 어떤 사용자가 수행 하는 순서 tootrack, Application Insights는 각 사용자 또는 세션에 대 한 ID가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="654d5-112">모든 사용자 지정 이벤트 또는 페이지 보기에 이러한 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="654d5-113">사용자, 깔때기, 재방문 주기 및 코호트: 사용자 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="654d5-114">세션: 세션 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="654d5-115">앱 hello와 통합 되어 있으면 [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), 사용자 ID를 자동으로 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="654d5-116">사용자 ID 선택</span><span class="sxs-lookup"><span data-stu-id="654d5-116">Choosing user IDs</span></span>

<span data-ttu-id="654d5-117">사용자 Id 시간에 따라 사용자가 동작 하는 방법을 사용자 세션 tootrack 유지 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="654d5-118">다양 한 가지 방법으로 유지 hello id.</span><span class="sxs-lookup"><span data-stu-id="654d5-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="654d5-119">서비스에 이미 있는 사용자의 정의.</span><span class="sxs-lookup"><span data-stu-id="654d5-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="654d5-120">Hello 서비스에 대 한 액세스 tooa 브라우저를 전달할 수 있습니다 hello 브라우저 쿠키 ID와 그 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="654d5-121">hello 쿠키 hello 사용자의 브라우저에서 남아 있는 기간과 같습니다 hello ID에 대 한 지속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="654d5-122">필요한 경우 각 세션에 새 ID를 사용할 수 있습니다 하지만 사용자에 대 한 hello 결과가 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="654d5-123">예를 들어 시간이 지남에 따라 사용자의 동작을 변경 하는 방법을 수 toosee 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="654d5-124">hello ID는 Guid 여야 합니다 또는 다른 문자열 충분히 복잡 tooidentify 각 사용자 고유 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="654d5-125">예를 들어 긴 임의의 수일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="654d5-126">Hello 사용자에 대 한 개인 식별 정보를 포함 하는 hello ID, 없는 경우 적절 한 값 toosend tooApplication 통찰력으로 사용자 id입니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="654d5-127">이러한 ID로 보낼 수 있습니다는 [사용자 ID를 인증](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), 하지만 사용 시나리오에 대 한 hello 사용자 ID 요구 사항을 만족 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="654d5-128">ASP.NET 앱: ITelemetryInitializer에 사용자 컨텍스트 설정</span><span class="sxs-lookup"><span data-stu-id="654d5-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="654d5-129">세부 정보에 설명 된 대로 원격 분석 이니셜라이저 만들기 [여기](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), Context.User.Id hello 및 Context.Session.Id hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="654d5-130">Hello 사용자 ID tooan 식별자를 hello 세션 후에 만료 되는이 예제가입니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="654d5-131">가능하면 세션 간에 유지되는 사용자 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="654d5-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="654d5-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="654d5-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="654d5-133">Next steps</span></span>
- <span data-ttu-id="654d5-134">tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.</span><span class="sxs-lookup"><span data-stu-id="654d5-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="654d5-135">사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.</span><span class="sxs-lookup"><span data-stu-id="654d5-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="654d5-136">사용 현황 개요</span><span class="sxs-lookup"><span data-stu-id="654d5-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="654d5-137">사용자, 세션 및 이벤트</span><span class="sxs-lookup"><span data-stu-id="654d5-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="654d5-138">깔때기</span><span class="sxs-lookup"><span data-stu-id="654d5-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="654d5-139">보존</span><span class="sxs-lookup"><span data-stu-id="654d5-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="654d5-140">통합 문서</span><span class="sxs-lookup"><span data-stu-id="654d5-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
