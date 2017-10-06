---
title: "aaaGet Azure Application Insights에서 추가 정보 | Microsoft Docs"
description: "Application insights 시작 후에 여기은 요약 hello 기능을 탐색할 수 있습니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>Application Insights의 추가 원격 분석
구성한 후 [Application Insights tooyour ASP.NET 코드를 추가](app-insights-asp-net.md), 가지 tooget 할 수 있는 몇 가지 더 많은 원격 분석에도 합니다. 

| 동작 | 결과|
|---|---|
|(IIS 서버) 각 서버 컴퓨터에 [상태 모니터를 설치](http://go.microsoft.com/fwlink/?LinkId=506648)합니다.<br/>(Azure 웹 앱) Hello Azure 제어판에서 hello 웹 앱에 대 한 hello Application Insights 블레이드를 엽니다.| [**성능 카운터**](app-insights-performance-counters.md)<br/>[**예외** ](app-insights-asp-net-exceptions.md) - 자세한 스택 추적<br/>[**종속성**](app-insights-asp-net-dependencies.md)|
|[Hello JavaScript 조각 tooyour 웹 페이지 추가](app-insights-javascript.md)|[성능 페이지](app-insights-web-track-usage.md), 브라우저 예외, AJAX 성능. 클라이언트쪽 사용자 지정 원격 분석.|
|[가용성 웹 테스트 만들기](app-insights-monitor-web-app-availability.md)|사이트를 사용할 수 없게 되면 알림 수신|
|MSBuild에서 [Ensure buildinfo.config](https://msdn.microsoft.com/library/dn449058.aspx) 생성|[annotationsin 메트릭 차트 작성](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/)
|[사용자 지정 이벤트 및 메트릭 작성](app-insights-api-custom-events-metrics.md)|비즈니스 이벤트 및 메트릭의 수를 계산하고, 자세한 사용 현황을 추적하는 등의 작업을 수행합니다.|
|[라이브 사이트 프로파일링](https://aka.ms/AIProfilerPreview)|라이브 웹앱의 자세한 함수 타이밍|






