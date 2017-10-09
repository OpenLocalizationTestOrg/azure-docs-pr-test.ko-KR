---
title: "Application Insights Azure 응용 프로그램 데이터 aaaView | Microsoft Docs"
description: "Hello Insights 커넥터 응용 프로그램 솔루션 toodiagnose 성능 문제를 사용 하 여 수 있으며 Application Insights로 모니터링 되는 경우 응용 프로그램으로 수행할 작업을 이해할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>OMS(Operations Management Suite)의 Application Insights 커넥터 솔루션(미리 보기)

![Application Insights 기호](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

응용 프로그램 Insights 커넥터 솔루션 hello를 사용 하면 성능 문제를 진단 하 고 사용자가 수행할 작업을 앱과 함께 모니터링 되는 경우 이해 [Application Insights](../application-insights/app-insights-overview.md)합니다. 뷰 hello Application Insights에서 개발자가 표시 되는 동일한 응용 프로그램 원격 분석은 OMS에서 사용할 수 있습니다. 그러나 OMS와 Application Insights 앱을 통합하는 경우 작업 및 응용 프로그램 데이터가 한 곳에 있게 되므로 응용 프로그램에 대한 가시성이 향상됩니다. 동일한 hello 것 뷰를 사용 하면 응용 프로그램 개발자와 toocollaborate 합니다. hello 일반적인 뷰 hello 시간 toodetect 줄어들고 응용 프로그램과 플랫폼 문제를 해결할 수 있습니다.

Hello 솔루션을 사용 하는 경우에 다음을 수행할 수 있습니다.

- Application Insights 앱이 서로 다른 Azure 구독에 있는 경우에도 모두 한 곳에서 보기
- 응용 프로그램 데이터와 인프라 데이터 연결
- 로그 검색에서 큐브 뷰로 응용 프로그램 데이터 시각화
- Hello OMS 로그 분석 데이터 tooyour Application Insights 앱 및 Azure 포털에서 피벗

## <a name="connected-sources"></a>연결된 소스

다른 대부분 로그 분석 솔루션와 달리 데이터 에이전트에서 응용 프로그램 Insights 커넥터 hello에 대 한 수집 되지 않습니다. Hello 솔루션에서 사용 하는 모든 데이터는 Azure에서 직접 제공 됩니다.

| 연결된 소스 | 지원됨 | 설명 |
| --- | --- | --- |
| [Windows 에이전트](log-analytics-windows-agents.md) | 아니요 | hello 솔루션 Windows 에이전트에서 정보를 수집 하지 않습니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 | hello 솔루션 Linux 에이전트에서 정보를 수집 하지 않습니다. |
| [SCOM 관리 그룹](log-analytics-om-agents.md) | 아니요 | hello 솔루션 연결된 SCOM 관리 그룹의 에이전트에서 정보를 수집 하지 않습니다. |
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | hello 솔루션은 Azure 저장소에서 컬렉션 정보 없습니다. |

## <a name="prerequisites"></a>필수 조건

- 응용 프로그램 Insights 커넥터 정보 tooaccess Azure 구독이 있어야 합니다.
- 구성된 Application Insights 리소스가 하나 이상 있어야 합니다.
- Hello 소유자 또는 참가자의 hello Application Insights 리소스 여야 합니다.

## <a name="configuration"></a>구성

1. Hello에서 hello Azure 웹 앱 분석 솔루션을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. Hello OMS 포털에서 클릭 **설정** &gt; **데이터** &gt; **Application Insights**합니다.
3. **구독 선택**에서 Application Insights 리소스가 포함된 구독을 선택하고 **응용 프로그램 이름**에서 하나 이상의 응용 프로그램을 선택합니다.
4. **Save**를 클릭합니다.

약 30 분 내에 데이터를 사용할 수 있고 Application Insights 바둑판식으로 배열 하는 hello hello 다음 이미지와 같은 데이터로 업데이트:

![Application Insights 타일](./media/log-analytics-app-insights-connector/app-insights-tile.png)

다른 염두에서 tookeep를 가리킵니다.

- Application Insights 앱 tooone OMS 작업 영역에만 연결할 수 있습니다.
- 연결할 수 있습니다 [Standard 또는 Premium Application Insights 리소스](https://azure.microsoft.com/pricing/details/application-insights) tooOMS 로그 분석 합니다. 그러나 로그 분석의 hello 무료 계층을 사용할 수 있습니다.

## <a name="management-packs"></a>관리 팩

이 솔루션은 연결된 관리 그룹에서 관리 팩을 설치하지 않습니다.

## <a name="use-hello-solution"></a>사용 가능한 hello 솔루션

hello 다음 단원에서는 hello Application Insights 대시보드 tooview에 표시 된 hello 블레이드를 사용 하 여 앱에서 데이터와 상호 작용 하는 방법.

### <a name="view-application-insights-connector-information"></a>Application Insights 커넥터 정보 보기

Hello 클릭 **Application Insights** 타일 tooopen hello **Application Insights** 대시보드 toosee hello 블레이드를 수행 합니다.

![Application Insights 대시보드](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Application Insights 대시보드](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

hello 대시보드에 hello 표에 표시 된 hello 블레이드 포함 됩니다. 각 블레이드 hello에 대 한 조건을 블레이드 범위 및 시간 범위를 지정 했는지 일치 too10 항목을 나열 합니다. 클릭할 때 모든 레코드를 반환 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 블레이드 머리글을 클릭할 때 또는 hello 블레이드의 hello 맨 아래에 있습니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **열** | **설명** |
| --- | --- |
| 응용 프로그램 - 응용 프로그램 수 | 응용 프로그램 리소스에서 응용 프로그램 hello 수를 표시합니다. 또한 목록 응용 프로그램 이름을 지정 하 고 각 항목에 대해 hello의 응용 프로그램 레코드 수입니다. 에 대 한 로그 검색 번호 toorun hello를 클릭 합니다.<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  응용 프로그램 이름 toorun 호스트, 원격 분석 유형별로 레코드 및 모든 데이터 형식 (기준 hello 마지막 날) 당 응용 프로그램 레코드를 표시 하는 hello 응용 프로그램에 대 한 로그 검색을 클릭 합니다. |
| 데이터 볼륨 - 데이터를 전송하는 호스트 | 데이터 전송 되는 컴퓨터 호스트의 hello 수를 보여 줍니다. 컴퓨터 호스트 및 각 호스트의 레코드 수도 나열합니다. 에 대 한 로그 검색 번호 toorun hello를 클릭 합니다.<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> 컴퓨터 이름 toorun 호스트, 원격 분석 유형별로 레코드 및 모든 데이터 형식 (기준 hello 마지막 날) 당 응용 프로그램 레코드를 표시 하는 hello 호스트에 대 한 로그 검색을 클릭 합니다. |
| 가용성 - 웹 테스트 결과 | 웹 테스트 결과를 성공 또는 실패로 나타내는 도넛형 차트를 보여 줍니다. 에 대 한 로그 검색 hello 차트 toorun를 클릭 합니다.<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> 결과 hello 전달 하 고 모든 테스트에 대 한 실패 수가 표시 됩니다. 지난 1 분간 hello에 대 한 트래픽이 모든 웹 응용 프로그램을 표시합니다. 응용 프로그램 이름 tooview 실패 한 웹 테스트의 세부 정보를 보여 주는 로그 검색을 클릭 합니다. |
| 서버 요청 – 시간당 요청 | 다양 한 응용 프로그램에 대 한 시간당 서버 요청 hello의 꺾은선형 차트를 보여 줍니다. Hello 차트 toosee hello 상위 3 응용 프로그램에서 시간에는 지점에 대 한 요청을 받고 선 위로 가져갑니다. 또한 hello 선택한 기간에 대 한 요청 및 요청 수가 hello 수신 하는 hello 응용 프로그램의 목록을 보여 줍니다. <br><br>에 대 한 로그 검색 hello 그래프 toorun 클릭 <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> hello의 더 자세한 꺾은선형 차트를 보여 주는 다양 한 응용 프로그램에 대 한 시간당 서버 요청 합니다. <br><br> Hello 목록 toorun에서 응용 프로그램에 대 한 로그 검색 클릭 <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> 응답 코드의 요청, 시간 및 요청 기간 동안 요청에 대 한 차트와 요청의 목록의 목록을 보여 주는 합니다.   |
| 실패 - 시간당 실패한 요청 수 | 시간당 실패한 응용 프로그램 요청 수에 대한 꺾은선형 차트를 보여 줍니다. 시간에서 hello 차트 toosee hello 상위 3 개의 응용 프로그램 요소에 대해 실패 한 요청 된 위로 가져갑니다. 또한 각각에 대해 실패 한 요청 수가 hello 응용 프로그램 목록을 보여 줍니다. 에 대 한 로그 검색 hello 차트 toorun 클릭 <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> 실패 한 응용 프로그램 요청 보다 자세한 꺾은선형 차트를 보여 주는 합니다. <br><br>Hello 목록 toorun에서 항목에 대 한 로그 검색을 클릭 <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> 시간과 요청 기간 및 실패 한 요청 응답 코드의 목록 실패 한 요청 실패 한 요청, 차트에 대 한 표시를 합니다. |
| 예외 – 시간당 예외 | 시간당 예외에 대한 꺾은선형 차트를 보여 줍니다. 시간에서 hello 차트 toosee hello 상위 3 개의 응용 프로그램 예외는 지점에 대 한 포인터로 가리킵니다. 또한 각각에 대 한 예외의 hello 번호로 응용 프로그램 목록을 보여 줍니다. 에 대 한 로그 검색 hello 차트 toorun 클릭 <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> 예외 보다 자세한 링크 차트를 보여 주는 합니다. <br><br>Hello 목록 toorun에서 항목에 대 한 로그 검색을 클릭 <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> 목록이 예외, 시간 및 실패 한 요청을 통해 예외에 대 한 차트 및 예외 형식의 목록을 보여 주는 합니다.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>로그 검색을 사용 하 여 hello Application Insights 원근감을 보려면

Hello 대시보드에 항목을 클릭 하면 검색에 표시 된 Application Insights 큐브 뷰는 표시 됩니다. hello 큐브 뷰 선택 된 hello 원격 분석 유형을 기반 하는 확장 된 시각화를 제공 합니다. 따라서 원격 분석 유형에 따라 시각화 콘텐츠가 변경됩니다.

Hello 응용 프로그램 블레이드에서 아무 곳 이나 클릭 하면 hello 기본 볼 **응용 프로그램** 관점입니다.

![Application Insights 응용 프로그램 큐브 뷰](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

hello 관점 선택한 hello 응용 프로그램의 개요를 표시 합니다.

hello **가용성** 블레이드 웹 테스트 결과 관련 된 실패 한 요청을 볼 수 있는 다른 큐브 뷰로 표시 합니다.

![Application Insights 가용성 큐브 뷰](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

에서 클릭 하면 아무 곳 이나 hello **서버 요청** 또는 **오류** 블레이드, 구성 요소 변경 toogive hello 관점 toorequests 관련 되는 시각화 요소가 있습니다.

![Application Insights 실패 블레이드](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

에서 클릭 하면 아무 곳 이나 hello **예외** 블레이드에 맞는 시각화 표시 tooexceptions 합니다.

![Application Insights 예외 블레이드](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

여부 하나를 클릭 하면 항목에 관계 없이 hello **응용 프로그램 Insights 커넥터** hello 내 대시보드 **검색** Application Insights 데이터 hello 표시를 반환 하는 모든 쿼리 자체를 페이지 응용 프로그램 통찰력 관점입니다. 예를 들어, Application Insights 데이터를 보려는 경우는 **&#42;** 쿼리도 hello 다음 이미지와 같은 hello 큐브 뷰 탭을 보여 줍니다.

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

큐브 뷰 구성 요소는 hello 검색 쿼리에 따라 업데이트 됩니다. 즉, 제공 기능 toosee hello hello 데이터를 모든 검색 필드를 사용 하 여 hello 결과 필터링 할 수 있습니다.

- 모든 응용 프로그램
- 선택된 단일 응용 프로그램
- 응용 프로그램 그룹

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Hello Azure 포털에서에서 피벗 tooan 응용 프로그램

응용 프로그램 Insights 커넥터 블레이드는 선택한 toopivot toohello 디자인 된 tooenable Application Insights 앱 *hello OMS 포털을 사용 하는 경우*합니다. 응용 프로그램을 해결 하는 데 도움이 되는 상위 수준의 모니터링 플랫폼으로 hello 솔루션을 사용할 수 있습니다. 잠재적인 문제를 위해 연결 된 응용 프로그램에 표시 되 면으로 OMS 검색에서 두 드릴 하거나 toohello Application Insights 앱 직접 피벗할 수 있습니다.

toopivot, hello 줄임표를 클릭 (**...** ) 하는 각 줄의 hello 끝에 표시 되 고 선택 **Application Insights에서 열려 있는**합니다.

>[!NOTE]
>**Application Insights에서 열기** hello Azure 포털에서에서 사용할 수 있습니다.

![Application Insights에서 열기](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>샘플 수정 데이터

Application Insights는  *[수정 샘플링](../application-insights/app-insights-sampling.md)*  toohelp 원격 분석 트래픽을 줄일 합니다. Application Insights 앱에서 샘플링을 사용하도록 설정하는 경우 Application Insights 및 OMS 모두에서 저장되는 항목의 수가 감소됩니다. Hello에 데이터 일관성은 유지 하는 동안 **응용 프로그램 Insights 커넥터** 페이지 및 큐브 뷰, 사용자 지정 쿼리에 대 한 샘플링된 한 데이터를 수동으로 해결 해야 합니다.

다음은 로그 검색 쿼리의 샘플링 수정 예입니다.

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

hello **카운트 샘플링** 필드는 모든 항목에 있는 및 표시 hello hello 항목이 나타내는 데이터 요소의 수입니다. Application Insights 앱에 대해 샘플링이 설정된 경우 **Sampled Count**(샘플링된 수)가 1보다 큽니다. toocount hello sum hello와 응용 프로그램에서 생성 하는 항목의 실제 수 **카운트 샘플링** 필드입니다.

샘플링 응용 프로그램에서 생성 하는 항목의 총 수를 hello만 영향을 줍니다. Toocorrect 샘플링 메트릭 필드과 같이 필요 하지 않습니다 **RequestDuration** 또는 **AvailabilityDuration** 해당 필드 표시 항목에 대 한 hello 평균을 표시 합니다.

## <a name="input-data"></a>데이터 입력

hello 솔루션 hello 유형의 원격 분석 데이터를 연결 된 Application Insights 앱에서 다음을 수신 합니다.

- Availability
- 예외
- 요청
- 작업 영역 tooreceive에 대 한 페이지 뷰-보기 페이지, 앱 toocollect 해당 정보를 구성 해야 합니다. 자세한 내용은 [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views)를 참조하세요.
- 사용자 지정 이벤트-작업 영역 tooreceive 사용자 지정 이벤트에 대 한 정보를 구성 해야 앱 toocollect 해당 합니다. 자세한 내용은 [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent)를 참조하세요.

데이터를 사용할 수 있게 되면 Application Insights에서 OMS로 수신됩니다.

## <a name="output-data"></a>출력 데이터

각 형식의 입력 데이터에 대해 *종류*가 *ApplicationInsights*인 레코드가 만들어집니다. ApplicationInsights 레코드 hello 다음 섹션에에서 표시 된 속성을 가져야 합니다.

### <a name="generic-fields"></a>일반 필드

| 속성 | 설명 |
| --- | --- |
| 형식 | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Hello 레코드의 시간 |
| ApplicationId | Hello Application Insights 응용 프로그램의 계측 키 |
| ApplicationName | Hello Application Insights 응용 프로그램의 이름 |
| RoleInstance | 서버 호스트의 ID |
| DeviceType | 클라이언트 장치 |
| ScreenResolution |   |
| Continent | 대륙 hello 요청이 발생 한 위치 |
| 국가 | 국가 hello 요청이 발생 한 위치 |
| Province | Province, 상태 또는 위치 요청을 시작한 hello 로캘 |
| City | 도시 또는 동 hello 요청이 발생 한 위치 |
| isSynthetic | 사용자가 또는 자동화 된 방법으로 hello 요청 생성 되었는지 여부를 나타냅니다. 사용자가 생성한 경우 True, 자동화된 방법인 경우 False입니다. |
| SamplingRate | Hello tooportal 보내집니다 SDK에 의해 생성 된 원격 분석의 비율입니다. 범위는 0.0-100.0입니다. |
| SampledCount | 100/(SamplingRate)입니다. 예를 들어 4 =&gt; 25%입니다. |
| IsAuthenticated | True 또는 False |
| OperationID | 항목 hello hello 포털에서 동일한 작업 ID 관련 항목으로 표시 됩니다. 일반적으로 hello 요청 ID입니다. |
| ParentOperationID | Hello 부모 작업의 ID |
| OperationName |   |
| SessionId | Hello 요청이 작성 된 hello 세션을 식별 하는 GUID toouniquely |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>가용성 관련 필드

| 속성 | 설명 |
| --- | --- |
| TelemetryType | Availability |
| AvailabilityTestName | Hello 웹 테스트의 이름 |
| AvailabilityRunLocation | Http 요청의 지리적 소스 |
| AvailabilityResult | Hello 웹 테스트의 hello 성공 결과를 나타냅니다. |
| AvailabilityMessage | hello 메시지 첨부 toohello 웹 테스트 |
| AvailabilityCount | 100/(샘플링 속도)입니다. 예를 들어 4 =&gt; 25%입니다. |
| DataSizeMetricValue | 1.0 또는 0.0 |
| DataSizeMetricCount | 100/(샘플링 속도)입니다. 예를 들어 4 =&gt; 25%입니다. |
| AvailabilityDuration | Hello 웹 테스트 지속 시간을 밀리초 단위로 시간 |
| AvailabilityDurationCount | 100/(샘플링 속도)입니다. 예를 들어 4 =&gt; 25%입니다. |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | Hello 웹 테스트에 대 한 고유 GUID |
| AvailabilityTimestamp | Hello 가용성 테스트의 정확한 타임 스탬프 |
| AvailabilityDurationMin | 샘플링 된 레코드에 대 한이 필드는 hello 최소 웹 테스트 지속 시간 (밀리초) hello 표시 데이터 요소에 대 한 표시 |
| AvailabilityDurationMax | 샘플링 된 레코드에 대 한이 필드는 hello 최대 웹 테스트 지속 시간 (밀리초) hello 표시 데이터 요소에 대 한 표시 |
| AvailabilityDurationStdDev | 샘플링 된 레코드에 대 한이 필드는 모든 웹 테스트의 기간 (밀리초)을 표시 하는 hello 데이터 요소 간의 hello 표준 편차 표시 |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>예외 관련 필드

| 형식 | ApplicationInsights |
| --- | --- |
| TelemetryType | 예외 |
| ExceptionType | 형식의 hello 예외 |
| ExceptionMethod | hello 예외 hello 메서드 |
| ExceptionAssembly | 어셈블리 버전이 포함 되어 hello 프레임 워크 hello 공개 키 토큰 뿐만 아니라 |
| ExceptionGroup | 형식의 hello 예외 |
| ExceptionHandledAt | Hello 예외를 처리 하는 hello 수준을 나타냅니다. |
| ExceptionCount | 100/(샘플링 속도)입니다. 예를 들어 4 =&gt; 25%입니다. |
| ExceptionMessage | Hello 예외 메시지 |
| ExceptionStack | 전체 스택 hello 예외 |
| ExceptionHasStack | 예외에 스택이 있는 경우 True |



### <a name="request-specific-fields"></a>요청 관련 필드

| 속성 | 설명 |
| --- | --- |
| 형식 | ApplicationInsights |
| TelemetryType | 요청 |
| ResponseCode | HTTP 응답 전송 tooclient |
| RequestSuccess | 성공 또는 실패를 표시합니다. True 또는 False입니다. |
| RequestID | ID toouniquely hello 요청 식별 |
| RequestName | GET/POST + URL 기본 |
| RequestDuration | Hello 요청 기간의 초 단위 시간 |
| URL | 호스트를 포함 하지 않고 hello 요청의 URL |
| 호스트 | 웹 서버 호스트 |
| URLBase | Hello 요청의 전체 URL |
| ApplicationProtocol | Hello 응용 프로그램에서 사용 하는 프로토콜 유형 |
| RequestCount | 100/(샘플링 속도)입니다. 예를 들어 4 =&gt; 25%입니다. |
| RequestDurationCount | 100/(샘플링 속도)입니다. 예를 들어 4 =&gt; 25%입니다. |
| RequestDurationMin | 샘플링 된 레코드에 대 한이 필드는 hello 표시 데이터 요소에 대 한 hello 최소 요청 기간 (밀리초)을 보여줍니다. |
| RequestDurationMax | 샘플링 된 레코드에 대 한이 필드에 표시 hello hello 표시 데이터 요소에 대 한 최대 요청 기간 (밀리초) |
| RequestDurationStdDev | 샘플링 된 레코드에 대 한이 필드는 hello 표시 데이터 요소에 대 한 모든 요청 기간 (밀리초) 간의 hello 표준 편차 표시 |

## <a name="sample-log-searches"></a>샘플 로그 검색

이 솔루션에는 샘플 로그 검색 hello 대시보드에 표시 된 집합이 없습니다. 그러나 hello에 설명이 포함 된 로그 검색 쿼리 예제 확인할 [보기 응용 프로그램 Insights 커넥터 정보](#view-application-insights-connector-information) 섹션.

## <a name="next-steps"></a>다음 단계

- 사용 하 여 [로그 검색](log-analytics-log-searches.md) tooview Application Insights 응용 프로그램에 대 한 정보를 자세히 설명 합니다.
