---
title: "Azure Application Insights에서 사용 현황 환경을 활성화하도록 사용자 컨텍스트 보내기 | Microsoft Docs"
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
ms.openlocfilehash: 9350029c775643be0dcc679b0f4bb9238b5f8aca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
#  <a name="sending-user-context-to-enable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="010cb-103">Azure Application Insights에서 사용 현황 환경을 활성화하도록 사용자 컨텍스트 보내기</span><span class="sxs-lookup"><span data-stu-id="010cb-103">Sending user context to enable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="010cb-104">사용자 추적</span><span class="sxs-lookup"><span data-stu-id="010cb-104">Tracking users</span></span>

<span data-ttu-id="010cb-105">Application Insights를 사용하면 제품 사용 현황 도구 집합을 통해 사용자를 모니터링하고 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-105">Application Insights enables you to monitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="010cb-106">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="010cb-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="010cb-107">깔때기</span><span class="sxs-lookup"><span data-stu-id="010cb-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="010cb-108">보존</span><span class="sxs-lookup"><span data-stu-id="010cb-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="010cb-109">코호트</span><span class="sxs-lookup"><span data-stu-id="010cb-109">Cohorts</span></span>
* [<span data-ttu-id="010cb-110">통합 문서</span><span class="sxs-lookup"><span data-stu-id="010cb-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="010cb-111">시간이 지남에 따른 사용자 동작을 추적하기 위해 Application Insights에는 각 사용자 또는 세션에 대한 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-111">In order to track what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="010cb-112">모든 사용자 지정 이벤트 또는 페이지 보기에 이러한 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="010cb-113">사용자, 깔때기, 재방문 주기 및 코호트: 사용자 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="010cb-114">세션: 세션 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="010cb-115">앱이 [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page)와 통합된 경우 사용자 ID는 자동으로 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-115">If your app is integrated with the [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="010cb-116">사용자 ID 선택</span><span class="sxs-lookup"><span data-stu-id="010cb-116">Choosing user IDs</span></span>

<span data-ttu-id="010cb-117">사용자 ID는 시간에 따라 사용자가 동작하는 방법을 추적하기 위해 사용자 세션에서 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-117">User IDs should persist across user sessions to track how users behave over time.</span></span> <span data-ttu-id="010cb-118">ID를 유지하기 위한 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-118">There are various approaches for persisting the ID.</span></span>
- <span data-ttu-id="010cb-119">서비스에 이미 있는 사용자의 정의.</span><span class="sxs-lookup"><span data-stu-id="010cb-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="010cb-120">서비스에 브라우저에 대한 액세스가 있는 경우 ID로 브라우저에 쿠키를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-120">If the service has access to a browser, it can pass the browser a cookie with an ID in it.</span></span> <span data-ttu-id="010cb-121">ID는 쿠키가 사용자의 브라우저에 유지되는 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-121">The ID will persist for as long as the cookie remains in the user's browser.</span></span>
- <span data-ttu-id="010cb-122">필요한 경우 각 세션에 새 ID를 사용할 수 있지만 사용자에 대한 결과가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-122">If necessary, you can use a new ID each session, but the results about users will be limited.</span></span> <span data-ttu-id="010cb-123">예를 들어 시간이 지남에 따라 사용자의 동작이 변경하는 방식을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-123">For example, you won't be able to see how a user's behavior changes over time.</span></span>

<span data-ttu-id="010cb-124">ID는 각 사용자를 고유하게 식별하는 데 충분히 복잡한 Guid 또는 다른 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-124">The ID should be a Guid or another string complex enough to identify each user uniquely.</span></span> <span data-ttu-id="010cb-125">예를 들어 긴 임의의 수일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="010cb-126">ID가 사용자에 대한 개인 식별 정보를 포함하는 경우 사용자 ID로 Application Insights에 보낼 적절한 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-126">If the ID contains personally identifying information about the user, it is not an appropriate value to send to Application Insights as a user ID.</span></span> <span data-ttu-id="010cb-127">[인증된 사용자 ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users)로 이러한 ID로 보낼 수 있지만 사용 현황 시나리오에 대한 사용자 ID 요구 사항을 만족하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill the user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="010cb-128">ASP.NET 앱: ITelemetryInitializer에 사용자 컨텍스트 설정</span><span class="sxs-lookup"><span data-stu-id="010cb-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="010cb-129">[여기](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)에서 자세히 설명된 대로 원격 분석 이니셜라이저를 만들고 Context.User.Id 및 Context.Session.Id를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set the Context.User.Id and the Context.Session.Id.</span></span>

<span data-ttu-id="010cb-130">이 예제에서는 세션 후에 만료되는 식별자에 대한 사용자 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-130">This example sets the user ID to an identifier that expires after the session.</span></span> <span data-ttu-id="010cb-131">가능하면 세션 간에 유지되는 사용자 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="010cb-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="010cb-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets the user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on the HttpContext Session.
            // Set the user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set the user id on the Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set the session id on the Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="010cb-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="010cb-133">Next steps</span></span>
- <span data-ttu-id="010cb-134">사용 현황 환경을 활성화하려면 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views) 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-134">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="010cb-135">사용자 지정 이벤트 또는 페이지 보기를 이미 보낸 경우 사용자가 서비스를 사용하는 방법에 대해 알아보려면 사용 현황 도구를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="010cb-135">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    * [<span data-ttu-id="010cb-136">사용 현황 개요</span><span class="sxs-lookup"><span data-stu-id="010cb-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="010cb-137">사용자, 세션 및 이벤트</span><span class="sxs-lookup"><span data-stu-id="010cb-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="010cb-138">깔때기</span><span class="sxs-lookup"><span data-stu-id="010cb-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="010cb-139">보존</span><span class="sxs-lookup"><span data-stu-id="010cb-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="010cb-140">통합 문서</span><span class="sxs-lookup"><span data-stu-id="010cb-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
