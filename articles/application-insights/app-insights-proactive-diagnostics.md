---
title: "Azure Application Insights에서 검색을 aaaSmart | Microsoft Docs"
description: "Application Insights는 앱 원격 분석의 자동 심층 분석을 수행하여 잠재적 성능 문제에 대해 경고합니다."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Application Insights의 스마트 감지
 스마트 감지는 웹 응용 프로그램에서 잠재적인 성능 문제를 자동으로 경고해 줍니다. 사전 분석할 때 너무 응용 프로그램에서 전송 하는 hello 원격 분석을 수행[Application Insights](app-insights-overview.md)합니다. 실패율이나 클라이언트 또는 서버 성능의 비정상적인 패턴이 갑자기 증가하는 경우 경고가 발생합니다. 이 기능에는 구성이 필요하지 않습니다. 응용 프로그램에서 충분한 원격 분석을 보내는 경우 작동합니다.

스마트 감지 경고와 hello 스마트 검색 블레이드 모두 hello 전자 메일을 받으면에서 액세스할 수 있습니다.

## <a name="review-your-smart-detections"></a>스마트 감지 검토
두 가지 방법으로 자동 관리 검색을 검색할 수 있습니다.

* **전자 메일을 받습니다** . 일반적인 예는 다음과 같습니다.
  
    ![전자 메일 경고](./media/app-insights-proactive-diagnostics/03.png)
  
    Hello 큰 단추가 tooopen hello 포털에서 자세히를 클릭 합니다.
* **hello 스마트 검색 타일** 블레이드 응용 프로그램의 개요에 최근 경고의 수를 보여 줍니다. Hello 타일 toosee 목록이 최신 경고를 클릭 합니다.

![최근 검색 보기](./media/app-insights-proactive-diagnostics/04.png)

경고 toosee 세부 정보를 선택 합니다.

## <a name="what-problems-are-detected"></a>어떤 문제가 검색되나요?
세 가지 종류가 검색됩니다.

* [스마트 감지 - 실패](app-insights-proactive-failure-diagnostics.md). 기계 학습 사용 하 여 tooset hello 예상 비율 앱 부하 및 기타 요소와의 상관 관계에 대 한 실패 한 요청입니다. Hello 실패율 hello 예상된 봉투 (envelope) 외부 되 면 알림을 보냅니다.
* [스마트 감지 - 성능 이상](app-insights-proactive-performance-diagnostics.md). 작업 또는 종속성 기간의 응답 시간은 비교 toohistorical 기준의 속도가 느려지지 또는 응답 시간이 나 페이지 로드 시간 비정상 패턴을 식별 했습니다 알림을 받을 수 있습니다.   
* [스마트 감지 - Azure 클라우드 서비스 문제](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). 앱이 Azure 클라우드 서비스에서 호스트되고 역할 인스턴스에 시작 실패, 빈번한 재활용 또는 런타임 충돌이 있는 경우 경고가 발생합니다.

(각 알림에 hello 도움말 링크 이동 toohello 관련 문서.)

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>다음 단계
이러한 진단 도구를 사용 하면 응용 프로그램에서 hello 원격 분석을 검사할 수 있습니다.

* [메트릭 탐색기](app-insights-metrics-explorer.md)
* [검색 탐색기](app-insights-diagnostic-search.md)
* [분석 - 강력한 쿼리 언어](app-insights-analytics-tour.md)

스마트 감지는 완전 자동입니다. 하지만 미정 원하는 몇 가지 더 많은 경고를 tooset?

* [수동으로 구성된 메트릭 경고](app-insights-alerts.md)
* [가용성 웹 테스트](app-insights-monitor-web-app-availability.md) 

