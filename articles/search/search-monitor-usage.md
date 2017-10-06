---
title: "aaaMonitor 사용량 및 Azure 검색 서비스의 통계 | Microsoft Docs"
description: "Microsoft Azure에서 호스팅되는 검색 서비스인 Azure 검색에 대해 리소스 소비 및 인덱스 크기를 추적합니다."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Azure Search 서비스 모니터링

Azure Search는 검색 서비스의 사용량 및 성능을 추적하기 위한 다양한 리소스를 제공합니다. 제공 toometrics, 로그, 인덱스 통계 및 Power BI에서 확장 된 모니터링 기능에 액세스 합니다. 이 문서에는 어떻게 tooenable hello 다른 모니터링 전략 및 toointerpret 결과 데이터를 hello 하는 방법을 설명 합니다.

## <a name="azure-search-metrics"></a>Azure Search 메트릭
메트릭은 거의 실시간으로 검색 서비스에 대한 고급 정보를 제공하며, 추가 설치 없이 모든 서비스에 사용할 수 있습니다. Too30 일 구성에 대 한 서비스의 hello 성능을 추적할 수 있습니다.

Azure Search는 다음 세 가지 메트릭에 대한 데이터를 수집합니다.

* 대기 시간 검색: 시간 hello 검색 서비스 필요한 tooprocess 분 단위로 집계 쿼리를 검색 합니다.
* QPS(초당 검색 쿼리 수): 초당 수신된 검색 쿼리 수를 1분마다 집계합니다.
* 제한된 검색 쿼리 백분율: 제한된 검색 쿼리의 비율을 1분마다 집계합니다.

![QPS 활동의 스크린 샷][1]

### <a name="set-up-alerts"></a>경고 설정
Hello 메트릭 세부 정보 페이지에서 구성할 수 있습니다 경고 tootrigger 전자 메일 알림을 또는 자동화 된 작업 메트릭 정의 된 임계값을 초과할 때.

메트릭에 대 한 자세한 내용은 hello Azure 모니터의 전체 설명서를 확인 합니다.  

## <a name="how-tootrack-resource-usage"></a>어떻게 tootrack 리소스 사용
인덱스 및 문서 크기의 hello 증가 추적 사전 서비스에 설정 된 hello 위쪽 제한에 도달 하기 전에 용량을 조정 수 있습니다. Hello 포털 또는 프로그래밍 방식으로 hello REST API를 사용 하 여이 수행할 수 있습니다.

### <a name="using-hello-portal"></a>Hello 포털을 사용 하 여

toomonitor 자원 배정 현황 hello에 hello 개수 및 서비스에 대 한 통계를 보려면 [포털](https://portal.azure.com)합니다.

1. Toohello 로그인 [포털](https://portal.azure.com)합니다.
2. Azure 검색 서비스의 hello 서비스 대시보드를 엽니다. Hello 서비스에 대 한 타일 hello 홈 페이지에서 확인할 수 있습니다 또는 toohello 서비스 JumpBar hello에 찾아보기에서 찾아볼 수 있습니다.

hello 사용 섹션에는 사용 가능한 리소스의 어떤 부분에서에서 현재 사용 중인를 알려 주는 미터 포함 되어 있습니다. 인덱스, 문서, 저장소에 대한 서비스당 제한에 대한 정보는 [서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.

  ![사용량 타일][2]

> [!NOTE]
> 또한 위의 스크린 샷에서 hello hello 무료 서비스에 대 한 복제 데이터베이스의 최대 및 개이고, 각각 분할 호스트 3 인덱스, 10, 000 문서 또는 데이터의 50 MB 수가 중 하나에 먼저 나타납니다. 기본 또는 표준 계층에서 만든 서비스는 훨씬 더 큰 서비스 제한이 있습니다. 계층 선택에 대한 자세한 내용은 [계층 또는 SKU 선택](search-sku-tier.md)을 참조하세요.
>
>

### <a name="using-hello-rest-api"></a>Hello REST API를 사용 하 여
Hello Azure 검색 REST API와.NET SDK hello tooservice 메트릭에 프로그래밍 방식 액세스를 제공합니다.  사용 중인 경우 [인덱서](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload Azure Cosmos DB 나 Azure SQL 데이터베이스에서 인덱스를 추가 API는 필요한 사용 가능한 tooget hello 번호입니다.

* [인덱스 통계 가져오기](/rest/api/searchservice/get-index-statistics)
* [문서 수 계산](/rest/api/searchservice/count-documents)
* [인덱서 상태 가져오기](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Tooexport 기록 하는 방법 및 메트릭

Hello 앞 섹션에서에서 설명 하는 hello 메트릭에 대 한 서비스 및 hello 원시 데이터에 대 한 hello 작업 로그를 내보낼 수 있습니다. 작업 로그를 알려 줍니다 hello 서비스를 사용 하 고 데이터가 Power BI에서 사용 될 수 있습니다 어떻게 tooa 저장소 계정에 복사 합니다. Azure Search는 이 목적을 위해 모니터링 Power BI 콘텐츠 팩을 제공합니다.


### <a name="enabling-monitoring"></a>모니터링 사용
Hello에 Azure 검색 서비스를 열고 [Azure 포털](http://portal.azure.com) hello 모니터링 사용 옵션 아래에서 합니다.

Hello 데이터 선택 tooexport 원하는: 로그, 메트릭 중 하나 또는 둘 다 합니다. Tooa 저장소 계정을 복사, tooan 이벤트 허브 송신 하 하거나 tooLog 분석을 내보낼 수 있습니다.

![어떻게 tooenable hello 포털에서 모니터링][3]

hello 설명서를 참조 하는 hello Azure CLI 또는 PowerShell을 사용 하 여 tooenable [여기](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs)합니다.

### <a name="logs-and-metrics-schemas"></a>로그 및 메트릭 스키마
Hello 데이터가 상태가 복사한 tooa 저장소 계정, hello 데이터 서식이 JSON 및 해당 위치에 두 개의 컨테이너:

* insights-logs-operationlogs: 검색 트래픽 로그인 경우
* insights-metrics-pt1m: 메트릭인 경우

시간 및 컨테이너당 하나의 Blob가 있습니다.

경로 예: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>로그 스키마
hello 로그 blob은 검색 서비스 트래픽 로그를 포함 합니다.
각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.
각 blob에 레코드가 hello 동안 발생 한 모든 hello 작업에서 같은 시간입니다.

| 이름 | 형식 | 예 | 참고 사항 |
| --- | --- | --- | --- |
| 실시간 |datetime |"2015-12-07T00:00:43.6872559Z" |Hello 작업의 타임 스탬프 |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |ResourceId |
| operationName |string |"Query.Search" |hello 작업의 hello 이름 |
| operationVersion |string |"2015-02-28" |사용 되는 hello api 버전 |
| 카테고리 |string |"OperationLogs" |constant |
| resultType |string |"Success" |가능한 값: Success 또는 Failure |
| resultSignature |int |200 |HTTP 결과 코드 |
| durationMS |int |50 |밀리초에서 hello 작업 기간 |
| properties |object |다음 표에서 hello를 참조 하십시오. |데이터별 작업을 포함하는 개체 |

**속성 스키마**
| 이름 | 형식 | 예 | 참고 사항 |
| --- | --- | --- | --- |
| 설명 |string |"GET /indexes('content')/docs" |hello 작업의 끝점 |
| 쿼리 |string |"?search=AzureSearch&$count=true&api-version=2015-02-28" |hello 쿼리 매개 변수 |
| 문서 |int |42 |처리된 문서 수 |
| IndexName |string |"testindex" |Hello 작업과 연결 된 hello 인덱스의 이름 |

#### <a name="metrics-schema"></a>메트릭 스키마
| 이름 | 형식 | 예 | 참고 사항 |
| --- | --- | --- | --- |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |리소스 ID |
| metricName |string |"Latency" |hello 메트릭의 hello 이름 |
| 실시간 |datetime |"2015-12-07T00:00:43.6872559Z" |hello 작업의 타임 스탬프 |
| average |int |64 |hello hello 메트릭 시간 간격의 hello 원시 샘플의 평균 값 |
| minimum |int |37 |hello hello 메트릭 시간 간격의 hello 원시 샘플의 최소 값 |
| maximum |int |78 |hello 최대값 hello 메트릭 시간 간격에 있는 hello 원시 샘플 |
| total |int |258 |hello 메트릭 시간 간격에 있는 hello 원시 샘플 hello 합계 값 |
| count |int |4 |toogenerate hello 메트릭을 사용 하는 hello 원시 샘플 수 |
| timegrain |string |"PT1M" |ISO 8601에서 hello 메트릭의 hello 시간 세분화 |

모든 메트릭은 1 분 간격으로 보고됩니다. 각 메트릭은 분당 최소, 최대 및 평균 값을 표시합니다.

Hello SearchQueriesPerSecond 메트릭에 대 한 최소값은 해당 1 분 동안 등록 된 초당 검색 쿼리에 대 한 hello 가장 낮은 값입니다. hello 마찬가지 toohello 최 댓 값입니다. 평균는 hello 전체 분에서 hello 집계 합니다.
1 분 동안이 시나리오에 대해 고려: 1 초는 hello SearchQueriesPerSecond에 대 한 최대 높은 부하의 뒤에는 평균 부하의 58 초과 마지막 1 초 하나의 쿼리를 사용 하는 최소 hello 합니다.

ThrottledSearchQueriesPercentage에 대 한 최소값, 최대값, 평균 및 합계를 모두 hello 같은 값: hello hello 1 분 동안 검색 쿼리의 총 수에서 제한 된 검색 쿼리의 비율입니다.

## <a name="analyzing-your-data-with-power-bi"></a>Power BI를 사용하여 데이터 분석

사용 하는 것이 좋습니다 [Power BI](https://powerbi.microsoft.com) tooexplore 데이터를 시각화 하 고 있습니다. 쉽게 tooyour Azure 저장소 계정을 연결 하 고 신속 하 게 데이터 분석을 시작할 수 있습니다.

Azure 검색에서는 [Power BI 콘텐츠 팩](https://app.powerbi.com/getdata/services/azure-search) toomonitor를 허용 하 고 미리 정의 된 차트 및 테이블 검색 트래픽 이해 합니다. 자동으로 tooyour 데이터를 연결 하 고 검색 서비스에 대 한 시각적 통찰력을 제공 하는 Power BI 보고서의 집합을 포함 합니다. 자세한 내용은 참조 hello [콘텐츠 팩 도움말 페이지](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/)합니다.

![Azure Search에 대한 Power BI 대시보드][4]

## <a name="next-steps"></a>다음 단계
검토 [복제본과 파티션 크기를 조정](search-limits-quotas-capacity.md) toobalance는 파티션 및 복제본 기존 서비스에 대 한 할당을 hello 하는 방법에 대 한 지침입니다.

서비스 관리에 대한 자세한 내용은 [Microsoft Azure에서 검색 서비스 관리](search-manage.md) 또는 튜닝 지침은 [성능 및 최적화](search-performance-optimization.md)를 방문하십시오.

놀라운 보고서 만들기에 대해 자세히 알아보세요. 자세한 내용은 [Power BI Desktop 시작](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)을 참조하세요.

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
