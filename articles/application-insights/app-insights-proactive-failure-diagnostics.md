---
title: "Application Insights에서 오류 변칙 검색-aaaSmart | Microsoft Docs"
description: "실패 한 요청 tooyour 웹 앱의 속도가 hello toounusual 변경 내용을 알려 하 고 진단 분석을 제공 합니다. 구성이 필요하지 않습니다."
services: application-insights
documentationcenter: 
author: yorac
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: bwren
ms.openlocfilehash: dfd178ca9546294be91f27b0c1b846d519539b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---failure-anomalies"></a>스마트 감지 - 실패
[Application Insights](app-insights-overview.md) 자동으로 웹 앱 환경을 hello 실패 한 요청 비율의 비정상적인 증가 면 거의 실시간으로 표시 합니다. HTTP 요청 또는 실패로 보고 되는 종속성 호출의 hello 속도의 비정상적인 증가를 검색 합니다. 요청의 경우 실패한 요청은 일반적으로 응답 코드 400 이상입니다. toohelp 심사 하 고 hello 문제를 진단, hello 실패 및 관련된 원격 분석의 hello 특성에 대 한 분석 hello 알림이 제공 됩니다. 추가 진단을 위해 링크 toohello Application Insights 포털도 있습니다. hello 기능 필요 없는 설치 및 구성, 기계 학습을 사용 하 여 알고리즘 toopredict hello 일반 오류 비율입니다.

이 기능은 hello 클라우드 또는 사용자의 서버에서 호스팅된, Java 및 ASP.NET 웹 앱에 대 한 작동 합니다. 요청 원격 분석 또는 종속성 원격 분석을 생성하는 모든 앱에 대해 작동합니다(예를 들어 [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) 또는 [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency)를 호출하는 작업자 역할이 있는 경우).

설정한 후 [프로젝트에 대 한 Application Insights](app-insights-overview.md), 하며 최소 일정량의 원격 분석을 생성 하는 응용 프로그램 제공 스마트 오류 비정상 탐지 24 시간 동안 toolearn hello 하기 전에 응용 프로그램의 일반적인 동작 가 설정 되 고 경고를 보낼 수 있습니다.

샘플 경고는 다음과 같습니다.

![실패에 대한 클러스터 분석을 보여주는 샘플 스마트 감지 경고](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> 기본적으로 이 예제보다 더 짧은 형식의 메일을 받게 됩니다. 하 고 있지만 [스위치 toothis 자세한 형식을](#configure-alerts)합니다.
>
>

여기서 알 수 있는 정보:

* hello 실패율 toonormal 앱 동작을 비교합니다.
* 사용자 수 영향 – 얼마나 tooworry를 확인할 수 있도록 합니다.
* Hello 실패와 관련 된 특성 패턴입니다. 이 예제에는 특정 응답 코드, 요청 이름(작업) 및 앱 버전이 있습니다. 즉시 알려주는 여기서 toostart 코드를 검색 합니다. 다른 가능성으로 특정 브라우저 또는 클라이언트 운영 체제가 있을 수 있습니다.
* hello 예외, 로그 추적 및 종속성이 실패 했습니다 (데이터베이스 또는 다른 외부 구성 요소) hello와 관련 된 toobe 나타나는 오류 특징입니다.
* Application Insights의 hello 원격 분석에 대 한 toorelevant 검색을 직접 연결합니다.

## <a name="benefits-of-smart-detection"></a>스마트 감지의 이점
일반 [메트릭 경고](app-insights-alerts.md) 는 문제일 수 있음을 알려 줍니다. 하지만 스마트 검색이 hello hello 분석 해야 하는 toodo 직접 많이 수행 하면에 대 한 진단 작업을 시작 합니다. 결과 얻는 hello 깔끔하게 패키지 하는 데 도움이 tooget 신속 하 게 hello 문제의 toohello 루트입니다.

## <a name="how-it-works"></a>작동 방법
스마트 검색 응용 프로그램에서 특정 hello 실패율에서 받은 hello 원격 분석을 모니터링 합니다. Hello는 hello에 대 한 요청 수를 계산 하는이 규칙 `Successful request` 속성이 false이 고 어떤 hello에 대 한 호출에 종속성 hello 수 `Successful call` 속성이 false입니다. 기본적으로 요청에 대 한 `Successful request == (resultCode < 400)` (너무 사용자 지정 코드를 작성 한 경우가 아니면[필터](app-insights-api-filtering-sampling.md#filtering) 하거나 사용자 고유의 생성 [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) 호출). 

앱의 성능에는 일반적인 동작의 패턴이 있습니다. 일부 요청 또는 종속성 호출 됩니다; 다른 항목 보다 더 toofailure 및 hello 전반적인 실패율 니다 로드가 증가 합니다. 기계 학습 toofind 이러한 예외를 사용 하는 스마트 검색 합니다.

웹 앱에서 Application Insights로 원격 분석 되 면, 스마트 검색 hello 지난 몇 일 동안 나타나는 hello 패턴과 hello 현재 동작을 비교 합니다. 이전 성능과 비교하여 실패율에 비정상적인 증가가 관찰되면 분석이 트리거됩니다.

분석 트리거되면 hello 서비스 hello 실패 한 요청에 tootry tooidentify hello 오류 특징을 결정 하는 값의 패턴에서 클러스터 분석을 수행 합니다. Hello 위의 예제에서는 특정 결과 코드, 요청 이름, 서버 URL 호스트 및 역할 인스턴스에 대 한 대부분의 오류는 hello 분석을 발견 했습니다. 이와 반대로 hello 클라이언트 운영 체제 속성은 여러 값을 통해 배포 하 고 있으므로 해당 옵션이 나타나지 hello 분석을 발견 했습니다.

이러한 원격 분석 호출 된 서비스에이 계측 찾습니다 hello 분석기와 파악 된, 설정과 관련 된 모든 추적 로그의 예제와 함께 hello 클러스터의 요청 연결 된 종속성 오류가 발생 했으며 요청 수입니다.

폼이 아니라 구성 하지 않으면 hello 분석 결과 tooyou 경고에 전송 됩니다.

Hello 처럼 [수동으로 설정 경고](app-insights-alerts.md), hello 경고의 hello 상태를 검사 하 고 Application Insights 리소스의 hello 경고 블레이드에서 구성할 수 있습니다. 하지만 다른 경고와는 달리를 tooset 필요 하거나 스마트 검색을 구성 하지 않습니다. 원하는 경우 해당 대상 전자 메일 주소를 사용하지 않거나 변경할 수 있습니다.

## <a name="configure-alerts"></a>경고 구성
스마트 검색을 사용 하지 않도록 설정, 변경 hello 전자 메일 받는 사람, webhook을 만들 하거나 자세한 toomore 옵트인 경고 메시지입니다.

Hello 경고 페이지를 엽니다. 오류 잘못 된 부분을 수동으로 설정 하 고 hello 경고 상태에 현재 인지 확인할 수 있는 모든 경고와 함께 포함 되어 있습니다.

![Hello 개요 페이지에서 경고 타일을 클릭 합니다. 또는 메트릭 페이지에서 경고 단추를 클릭합니다.](./media/app-insights-proactive-failure-diagnostics/021.png)

Hello 경고 tooconfigure 클릭 것입니다.

![구성](./media/app-insights-proactive-failure-diagnostics/032.png)

스마트 감지를 비활성화할 수 있지만 삭제할 수 없습니다(또는 다른 스마트 감지를 만들 수 없음).

#### <a name="detailed-alerts"></a>세부 경고
"보다 자세한 진단 가져오기"를 선택 하는 경우 자세한 진단 정보 hello 전자 메일에 포함 됩니다. 경우에 따라 hello 전자 메일의 hello 데이터에서 방금 수 toodiagnose hello 문제가 됩니다.

약간의 위험 보다 자세한 경고 hello을 중요 한 정보를 포함 하므로 예외 및 추적 메시지를 포함 합니다. 그러나 이러한 문제는 코드에서 해당 메시지에 중요한 정보를 허용할 수 있는 경우에만 발생합니다.

## <a name="triaging-and-diagnosing-an-alert"></a>경고 분류 및 진단
경고는 hello 실패 한 요청 비율의 비정상적인 증가 검색 되었음을 나타냅니다. 앱 또는 해당 환경에 문제가 있을 가능성이 있습니다.

요청 및 개수의 영향을 받는 사용자의 백분율 hello에서에서 hello 문제 우선 순위를 결정할 수 있습니다는 합니다. 위의 hello 예제에서 hello 실패율 22.5%의 %1의 보통 속도와 비교, 뭔가 나쁜 것을 나타냅니다. 다른 손 hello, 11만 사용자가 영향을 합니다. 응용 프로그램은 마치를 심각도 수 tooassess 것입니다.

대부분의 경우에서 수 toodiagnose hello 문제 hello 요청 이름, 예외, 제공 된 종속성 오류 및 추적 데이터에서 신속 하 게 됩니다.

몇 가지 다른 단서가 있습니다. 예를 들어 hello 종속성 실패율이 예에서 예외 속도 (89.3%) hello와 같을 hello 됩니다. 이 인해 hello 종속성 실패-where 명확 하 게 알고 제공에서 직접 hello 예외 발생을 toostart 코드를 검색 합니다.

tooinvestigate 또한 각 섹션에 링크는 hello 걸립니다 직선 tooa [검색 페이지](app-insights-diagnostic-search.md) toohello 관련 요청, 예외, 종속성 또는 추적을 필터링 합니다. Hello를 열 수 있습니다 또는 [Azure 포털](https://portal.azure.com)응용 프로그램에 대 한 Application Insights 리소스 toohello 이동한 hello 오류 블레이드를 엽니다.

이 예제에서는 hello '종속성 오류 세부 정보 보기' 링크를 클릭 하 여 hello Application Insights 검색 블레이드를 엽니다. Hello 근본 원인의 예에 있는 hello SQL 문으로 표시: Null 필수 필드에 제공 된 및 hello 저장 작업 중에 유효성 검사를 통과 하지 못했습니다.

![진단 검색](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a>최근 경고 검토

클릭 **스마트 검색** tooget toohello 가장 최근의 경고:

![경고 요약](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-hello-difference-"></a>Hello 차이가 중...
실패에 대한 스마트 감지는 Application Insights의 다른 유사하지만 고유한 기능을 보완합니다.

* [메트릭 경고](app-insights-alerts.md) 는 사용자에 의해 설정되며 CPU 점유율, 요청 속도, 페이지 로드 시간 등과 같은 광범위한 메트릭을 모니터링할 수 있습니다. Toowarn 사용할 수 있습니다 예를 들어 tooadd 더 많은 리소스가 필요 합니다. 오류 예외의 스마트 검색에 실시간으로 방식으로 웹 앱의 실패 한 요청 속도 크게 향상 되 면 근처 비교한 tooweb 응용 프로그램의 설계 중요 한 메트릭 (현재만 실패 한 요청 속도), 작은 범위의 toonotify를 포함 하는 반면, 정상적인 동작입니다.

    스마트 검색 응답 tooprevailing 조건에 해당 임계값을 자동으로 조정합니다.

    스마트 검색이 hello 진단 작업을 시작 합니다.
* [성능 비정상 탐지 스마트](app-insights-proactive-performance-diagnostics.md) 도 사용 하 여 컴퓨터에서 메트릭, intelligence toodiscover 특별 한 패턴 및 사용자가 구성은 필요 하지 않습니다. 하지만 오류 예외의 스마트 검색 달리 hello의 스마트 검색 성능 이상의의 목적은-예를 들어 브라우저의 특정 종류의 특정 페이지 잘못 제공 될 수 있는 프로그램 사용 현황 기관을의 toofind 세그먼트입니다. hello 분석은 매일 수행 되며 결과 있으면 경고 보다 훨씬 덜 긴급 한 가능성이 toobe 있습니다. 반면, 실패 예외에 대 한 hello 분석은 들어오는 원격 분석에서 지속적으로 수행 하 고 알려 분 이내 서버 실패율이 예상 보다 큰 경우.

## <a name="if-you-receive-a-smart-detection-alert"></a>스마트 감지 경고를 받은 경우
*이 경고를 받은 이유는 무엇입니까?*

* 실패 한 요청 속도 비교 toohello hello 기간 앞의 정상적인 기준의 비정상적인 증가 검색 되었습니다. Hello 실패와 관련된 원격 분석의 분석 후를 확인 해야 하는 문제 인지 한다고 생각 합니다.

*문제가 있는 경우 확실 하 게 hello 알림 의미 합니까?*

* 응용 프로그램 중단 또는 성능 저하에 tooalert 시도 하지만 완벽 하 게 이해할 수 hello 의미 체계와 hello 앱 또는 사용자에 미치는 영향을 hello.

*그렇다면, 내 데이터를 확인하고 있습니까?*

* 아니요. hello 서비스는 완전 자동입니다. 만 hello 알림을 받을 수 있습니다. 사용자의 데이터는 [비공개](app-insights-data-retention-privacy.md)입니다.

*Toosubscribe toothis 경고 있습니까?*

* 아니요. 모든 응용 프로그램 요청 원격 분석을 보냅니다는 hello 스마트 검색 경고 규칙을 있습니다.

*구독을 취소 하거나 toomy 동료를 대신 보냅니다 hello 알림을 받을 수 있습니까?*

* 예,에서 경고 규칙 클릭 hello 스마트 검색 규칙 tooconfigure 것입니다. Hello 경고를 사용 하지 않도록 설정 하거나 hello 경고에 대 한 받는 사람을 변경할 수 있습니다.

*Hello 전자 메일을 끊어졌습니다. Hello 포털에서 hello 알림을 어디서 찾을 수 있습니까?*

* Hello에 활동을 기록합니다. Azure에서 응용 프로그램에 대 한 hello Application Insights 리소스를 열고 작업 로그를 선택 합니다.

*일부 hello 경고가 약의 알려진 문제 및 tooreceive를 원하지 않는 해당 합니다.*

* 백로그에 경고 제거가 있습니다.

## <a name="next-steps"></a>다음 단계
이러한 진단 도구를 사용 하면 응용 프로그램에서 hello 원격 분석을 검사할 수 있습니다.

* [메트릭 탐색기](app-insights-metrics-explorer.md)
* [검색 탐색기](app-insights-diagnostic-search.md)
* [분석 - 강력한 쿼리 언어](app-insights-analytics-tour.md)

스마트 감지는 완전히 자동으로 수행됩니다. 하지만 미정 원하는 몇 가지 더 많은 경고를 tooset?

* [수동으로 구성된 메트릭 경고](app-insights-alerts.md)
* [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)
