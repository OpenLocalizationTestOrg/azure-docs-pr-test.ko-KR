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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>보내는 사용자 컨텍스트 tooenable 사용 환경을 Azure Application Insights

## <a name="tracking-users"></a>사용자 추적

Application Insights toomonitor 수 있으며 특정 제품 사용 도구 집합을 통해 사용자 추적: 
* [사용자, 세션, 이벤트](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [깔때기](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [보존](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* 코호트
* [통합 문서](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

시간이 지남에 따라 어떤 사용자가 수행 하는 순서 tootrack, Application Insights는 각 사용자 또는 세션에 대 한 ID가 필요 합니다. 모든 사용자 지정 이벤트 또는 페이지 보기에 이러한 ID를 포함합니다.
- 사용자, 깔때기, 재방문 주기 및 코호트: 사용자 ID를 포함합니다.
- 세션: 세션 ID를 포함합니다.

앱 hello와 통합 되어 있으면 [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), 사용자 ID를 자동으로 추적 합니다.

## <a name="choosing-user-ids"></a>사용자 ID 선택

사용자 Id 시간에 따라 사용자가 동작 하는 방법을 사용자 세션 tootrack 유지 되어야 합니다. 다양 한 가지 방법으로 유지 hello id.
- 서비스에 이미 있는 사용자의 정의.
- Hello 서비스에 대 한 액세스 tooa 브라우저를 전달할 수 있습니다 hello 브라우저 쿠키 ID와 그 안에 있습니다. hello 쿠키 hello 사용자의 브라우저에서 남아 있는 기간과 같습니다 hello ID에 대 한 지속 됩니다.
- 필요한 경우 각 세션에 새 ID를 사용할 수 있습니다 하지만 사용자에 대 한 hello 결과가 제한 됩니다. 예를 들어 시간이 지남에 따라 사용자의 동작을 변경 하는 방법을 수 toosee 수 없습니다.

hello ID는 Guid 여야 합니다 또는 다른 문자열 충분히 복잡 tooidentify 각 사용자 고유 하 게 합니다. 예를 들어 긴 임의의 수일 수 있습니다.

Hello 사용자에 대 한 개인 식별 정보를 포함 하는 hello ID, 없는 경우 적절 한 값 toosend tooApplication 통찰력으로 사용자 id입니다. 이러한 ID로 보낼 수 있습니다는 [사용자 ID를 인증](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), 하지만 사용 시나리오에 대 한 hello 사용자 ID 요구 사항을 만족 하지 않습니다.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>ASP.NET 앱: ITelemetryInitializer에 사용자 컨텍스트 설정

세부 정보에 설명 된 대로 원격 분석 이니셜라이저 만들기 [여기](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), Context.User.Id hello 및 Context.Session.Id hello 설정 합니다.

Hello 사용자 ID tooan 식별자를 hello 세션 후에 만료 되는이 예제가입니다. 가능하면 세션 간에 유지되는 사용자 ID를 사용합니다.

*C#*

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

## <a name="next-steps"></a>다음 단계
- tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.
- 사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.
    * [사용 현황 개요](app-insights-usage-overview.md)
    * [사용자, 세션 및 이벤트](app-insights-usage-segmentation.md)
    * [깔때기](usage-funnels.md)
    * [보존](app-insights-usage-retention.md)
    * [통합 문서](app-insights-usage-workbooks.md)
