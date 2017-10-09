---
title: "aaaAzure 검색 성능 및 최적화 고려 사항 | Microsoft Docs"
description: "Azure 검색 성능 조정 및 최적의 크기 조정 구성"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Azure 검색 성능 및 최적화 고려 사항
효율적인 검색 환경에는 많은 모바일 앱을 위해 키 toosuccess 및 웹 응용 프로그램은 합니다. 부동산에서 tooused 자동차 시장 tooonline 카탈로그, 빠른 검색 및 관련 결과 영향을 줍니다 hello 사용자 환경 개선 합니다. 이 문서는 의도 한 toohelp 방법을 사용 하는 고급 시나리오를 위해 특별히 Azure 검색을 최대한 활용 tooget hello 정교한 확장성, 다국어 지원을 또는 사용자 지정 순위에 대 한 요구 사항에 대 한 유용한 정보를 검색 합니다.  또한 이 문서는 내부 구성을 간략하게 설명하고 실제 고객 앱에서 효과적으로 작동하는 접근 방법을 소개합니다.

## <a name="performance-and-scale-tuning-for-search-services"></a>검색 서비스의 성능 및 규모 확장
모든 사용 되는 toosearch 엔진 등 Bing 및 Google 및 hello 높은 성능 제공 하는입니다.  따라서 고객이 검색 기능이 지원되는 웹 또는 모바일 응용 프로그램을 사용할 때도 비슷한 성능 특성을 기대할 것입니다.  검색 성능을 최적화 하는 경우는 쿼리에서 toocomplete 및 반환 결과 hello 시간은 대기 시간에 toofocus hello 최상의 방법 중 하나입니다.  검색 대기 시간을 최적화하는 경우 다음 작업이 중요합니다.

1. 선택 대상 대기 시간 (또는 제한 시간) 일반적인 검색 요청 toocomplete를 수행 해야 합니다.
2. 페이지를 만들고 이러한 지연 속도가 사실적인 데이터 집합 toomeasure 사용 하 여 검색 서비스에 대 한 실제 작업을 테스트 합니다.
3. Queries / sec (QPS) 수가 적으므로 시작 하며 tooincrease hello 번호 hello 쿼리 대기 시간 hello 이하가 대상 대기 시간을 정의할 때까지 hello 테스트에서 실행을 계속 합니다.  이 사용량에서 응용 프로그램까지 확장 되면서 눈금에 대 한 계획 하는 중요 한 벤치 마크 toohelp입니다.
4. 가능하면 HTTP 연결을 다시 사용합니다.  Hello Azure 검색.NET SDK를 사용 하는 경우 즉, 인스턴스를 다시 사용 해야 하거나 [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) 인스턴스를 사용 하는 경우 REST API hello, 단일 한 HttpClient를 다시 사용 해야 합니다.

이 만드는 동안 작업 부하 테스트를 염두에서 tookeep Azure 검색의 몇 가지 특성:

1. Toopush 너무 많은 검색 쿼리가 한 번에, Azure 검색 서비스에서 사용할 수 있는 hello 리소스를 가득 채워 됩니다는 불가능 합니다.  이 경우 HTTP 503 응답 코드가 표시됩니다.  이러한 이유로 이므로 대기 시간 비율의 검색 요청 toosee hello 차이의 다양 한 범위와 관련 된 최상의 toostart 더 많은 검색 요청을 추가 합니다.
2. 전반적인 성능 hello 검색에 영향을 줍니다 콘텐츠 tooAzure의 업로드 및의 대기 시간 hello Azure 검색 서비스입니다.  사용자가 검색을 수행 하는 동안 toosend 데이터를 원하는 경우 중요 한 tootake이이 작업을 테스트에는 계정입니다.
3. 모든 검색 쿼리를 수행 합니다 hello에 동일한 성능 수준입니다.  예를 들어 문서 조회 또는 검색 제안은 패싯과 필터를 상당히 많이 사용하는 쿼리보다 더 빠르게 작동합니다.  것이 가장 좋은 tootake hello toosee에 예상 되는 다양 한 쿼리 테스트를 작성할 때 고려 합니다.  
4. 검색 요청의 변형에 중요 합니다. 동일한 검색 요청을 hello를 지속적으로 실행 되 면 때문에 데이터의 캐시는 시작 toomake 성능을 더 잘 보다 것 보다 서로 다른 쿼리를 통해 설정할 수 있습니다.

> [!NOTE]
> [Visual Studio 부하 테스트](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) 수 있으므로 tooexecute HTTP 요청 Azure 검색에 대 한 쿼리를 실행 하는 데 필요한 만큼 테스트 하 고 요청 병렬화 할 수 있도록 하는 프로그램 벤치 마크 실제로 좋은 방법 tooperform 됩니다.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>높은 쿼리 속도 및 제한된 요청에 따라 Azure 검색 확장
너무 많은 제한 된 요청을 받고 하거나 대상 대기 시간 사용률 증가 된 쿼리 부하를 초과할 때 두 가지 방법 중 하나로 toodecrease 대기 시간 비율을 확인할 수 있습니다.

1. **증가 복제본:** 복제본 hello에 대 한 Azure 검색 tooload 잔액 요청 복사본을 여러 개 허용 데이터의 복사본과 같습니다.  모든 부하 분산 및 Azure 검색에서 복제본에 데이터의 복제 관리, 언제 든 지 서비스에 할당 된 복제본의 hello 수를 변경할 수 있습니다.  표준 검색 서비스의 too12 복제 데이터베이스 및 복제본 기본 검색 서비스의 3 개를 할당할 수 있습니다. 복제본 수 조정 hello에서 [Azure 포털](search-create-service-portal.md) 또는 [PowerShell](search-manage-powershell.md)합니다.
2. **검색 계층 증가:** Azure Search에는 [여러 계층](https://azure.microsoft.com/pricing/details/search/) 이 포함되어 있으며 이러한 각 계층은 다른 수준의 성능을 제공합니다.  경우에 따라 복제본은 최대값을 초과 하는 경우에 해당 hello 계층에 있는 충분할 만큼 짧은 대기 시간 비율을 제공할 수 없는 너무 많은 쿼리를 할 수 있습니다.  이 경우 많은 수의 문서 및 매우 높은 쿼리 워크 로드의 시나리오에 대해 가장 적합 hello Azure 검색 S3 계층 같은 hello 더 높은 검색 계층 중 하나를 활용 하 여 tooconsider를 수도 있습니다.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>느린 개별 쿼리에 맞게 Azure 검색 속도 조정
단일 쿼리에 toocomplete 너무 길어 라인으로 전환 이유 지연 속도가 느려질 수 있습니다 하는 다른 이유가입니다.  이 경우 복제본을 추가해도 대기 시간 속도가 향상되지 않습니다.  이러한 경우에 다음 두 가지 옵션을 사용할 수 있습니다.

1. **파티션 증가** 파티션은 추가 리소스로 데이터를 분할하는 메커니즘입니다.  이러한 이유로 두 번째 파티션을 추가하면 데이터가 둘로 분할됩니다.  세 번째 파티션을 추가하면 인덱스가 셋으로 분할됩니다.  이 경우에 따라 처리 속도가 느린 쿼리 수행 되는 더 빠르게 계산의 toohello 병렬화 인해 hello 효과 있습니다.  선택도가 낮은 쿼리를 포함하는 쿼리에서 이 병렬 처리가 매우 잘 작동한다는 몇 가지 예가 있습니다.  여러 문서와 일치 하는 쿼리 구성이 되거나 tooprovide 다 수의 문서를 통해 계산 패싯 필요한 경우.  되므로 계산이 많이 필요한 tooscore hello 관련성의 hello 문서나 toocount hello 수의 문서, 추가 파티션을 tooprovide 추가 계산 수를 추가 합니다.  
   
   표준 검색 서비스에 대 한 파티션 12 개까지 및 hello 기본 검색 서비스에서 1 파티션 수 있습니다.  파티션 수 조정 hello에서 [Azure 포털](search-create-service-portal.md) 또는 [PowerShell](search-manage-powershell.md)합니다.
2. **제한 높은 카디널리티 필드:** 카디널리티가 높은 필드 facetable 또는 많은 고유 값이 고 결과적으로, 맡습니다 리소스를 많이 toocompute 결과 필터링 가능한 필드 구성 됩니다.   예를 들어 제품 ID 또는 설명 필드 facetable/필터링 가능으로 설정이 만들 카디널리티가 높은 대부분의 문서 toodocument에서 hello 값은 고유 하므로 합니다. 가능 하면 hello 카디널리티가 높은 필드 수를 제한 합니다.
3. **계층을 검색 하는 증가:** Azure 검색 계층을 다른 방식으로 tooimprove 느린 쿼리 성능을 수 tooa 높은 위로 이동 합니다.  또한 각 상위 계층은 더 빠른 CPU와 더 많은 메모리를 제공하므로 쿼리 성능에 긍정적인 영향을 줄 수 있습니다.

## <a name="scaling-for-availability"></a>가용성에 따른 크기 조정
복제본은 쿼리 대기 시간을 줄이는 데 도움이 될 뿐만 아니라 고가용성도 가능하게 합니다.  단일 복제본과 소프트웨어를 업데이트 한 후 또는 발생 하는 다른 유지 관리 이벤트에 대 한 tooserver 재부팅 인해 주기적인 작동 중지가 예상 해야 합니다.  결과적으로, 것이 중요 한 tooconsider 응용 프로그램 검색 (쿼리)의 고가용성이 필요한 쓰기 (인덱싱 이벤트) 뿐 아니라.  Azure 검색은 모든 SLA 옵션 특성에 따라 hello로 유료 검색 버전 hello를 제공 합니다.

* 읽기 전용 작업(쿼리)의 고가용성을 위한 복제본 2개
* 읽기/쓰기 작업(쿼리 및 인덱싱)의 고가용성을 위한 복제본 3개 이상

이 대 한 자세한 내용은 hello를 방문 하세요 [Azure 검색 서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/search/v1_0/)합니다.

복제본은 복제본을 여러 개 있는 데이터의 복사본 Azure 검색 toodo 컴퓨터 재부팅을 허용 하 고 유지 관리를 허용 하는 동안 한 번에 하나의 복제본에 대 한 쿼리 toocontinue toobe에 대해 실행 되는 다른 복제 hello 합니다.  이러한 이유로, 또한 tooconsider이 작동 중단이 시간 이제 toobe hello 데이터의 작은 한 복사본에 대해 실행 하는 hello 쿼리가 영향을 줄 수는 어떻게 해야 합니다.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>지리적으로 분산된 워크로드 조정 및 지리적 중복 제공
지리적으로 분산 작업에 대 한 Azure 검색 서비스를 호스팅할 hello 데이터 센터 멀리 떨어져 있는 사용자에 게 지연 속도가 있는지 알 수 있습니다.  이러한 이유로 것이 중요 한 toohave 근접 toothese 사용자 더 가깝기 때문에 있는 지역에서 여러 검색 서비스입니다.  Azure 검색 Azure 검색 인덱스 지역 복제의 자동화 된 지역에서 현재 제공 하지 않습니다 되지만 일부의 기술을 사용할 수 있는 프로세스 간단한 tooimplement이를 확인 하 고 관리할 수 있는 합니다. Hello 개요는 다음 몇 개 섹션.

hello 검색 서비스의 지리적으로 분산 집합이 ´ ֲ 2 toohave 또는 사용자 수는 두 개 이상의 지역에서 사용할 수 있는 더 많은 인덱스 toohello Azure 검색 서비스이 예제와 같이 hello 가장 짧은 대기 시간을 제공 하는 라우팅:

   ![지역별 서비스 크로스탭][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>여러 Azure 검색 서비스에서 데이터를 동기화 상태로 유지
사용 하 여 구성 된 동기화 분산된 검색 서비스를 유지 하는 데에 두 가지가 hello [Azure 검색 인덱서](search-indexer-overview.md) 또는 푸시 API 환영 (tooas hello 라고도 [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Azure 검색 인덱서
Hello Azure 검색 인덱서를 사용 하는 경우 Azure SQL DB 또는 Azure Cosmos DB와 같은 중앙 데이터 저장소에서 데이터 변경 내용을 가져오는 이미 있습니다. 새 검색 서비스를 만들 때 하면 단순히 해당 지점 toothis 해당 서비스에 대 한 새 Azure 검색 인덱서를 만들 수도 동일한 데이터 저장소입니다. 이런 방식으로 hello 데이터 저장소에 새 변경 작업으로 수행할 때마다 있게 됩니다 다양 한 인덱서 hello로 인덱싱된 합니다.  

이러한 아키텍처 형태의 예는 다음과 같습니다.

   ![분산 인덱서 및 서비스 조합을 포함하는 단일 데이터 원본][2]

### <a name="push-api"></a>푸시 API
사용 중인 경우 hello Azure 검색 API 푸시 너무[Azure 검색 인덱스에는 콘텐츠 업데이트](https://docs.microsoft.com/rest/api/searchservice/update-index)를 유지할 수 있습니다 다양 한 검색 서비스 동기화 업데이트가 필요한 지 될 때마다 변경 내용을 tooall 검색 서비스에 푸시하여 합니다.  이 경우 중요 한 toomake 있는지 toohandle 하는 경우 업데이트 tooone 검색 서비스가 하나 이상 업데이트할 수 있습니다.

## <a name="leveraging-azure-traffic-manager"></a>Azure 트래픽 관리자 활용
[Azure 트래픽 관리자](../traffic-manager/traffic-manager-overview.md) 있습니다 tooroute 요청 toomultiple 위치 해 웹 사이트를 여러 Azure 검색 서비스에 의해 다음 지원 됩니다.  Hello 트래픽 관리자의 장점 중 하나는 Azure 검색 tooensure를 사용할 수 있는지 조사 하 고 사용자 tooalternate 검색 서비스의 가동 중지 시간 hello 이벤트에 라우트할 수는 있습니다.  또한 Azure 웹 사이트를 통해 검색 요청을 라우팅하는 경우 Azure 트래픽 관리자 있습니다 tooload 분산 되는 경우 hello 웹 사이트를 구성 하지만 Azure 검색 되지 않습니다.  트래픽 관리자를 활용 하 여 어떤 hello 아키텍처의 예를 들면 다음과 같습니다.

   ![지역별 서비스 크로스탭(중앙 트래픽 관리자 포함)][3]

## <a name="monitoring-performance"></a>성능 모니터링
Azure 검색을 통해 서비스의 hello 기능 tooanalyze 및 모니터 hello 성능을 제공 [검색 트래픽 분석 (STA)](search-traffic-analytics.md)합니다. STA를 통해 로그인 할 수 필요에 따라 다음 분석을 위해 처리 하거나 시각화할 수 있는 집계 된 메트릭 tooan Azure 저장소 계정 뿐 아니라 hello 개별 검색 작업 Power BI 합니다.  STA 메트릭을 사용하여, 쿼리의 평균 개수 또는 쿼리 응답 시간과 같은 성능 통계를 검토할 수 있습니다.  또한 hello 작업 로깅이 있습니다 toodrill에 특정 검색 작업의 세부 정보.

STA 해당 Azure 검색 관점에서 중요 한 도구 toounderstand 대기 시간 비율입니다.  기록 hello 쿼리 성능 메트릭에 hello 시간을 기반으로 하므로 toobe (hello 두 번째는 전송 되기 요청한 toowhen)에서 Azure 검색에서 완전히 처리를 사용 하는 쿼리, toouse 수는이 toodetermine hello Azure 검색 서비스에서에서 대기 시간 문제가 되는 경우 외부 서비스, 네트워크 대기 시간에서와 같이 hello 하거나 합니다.  

## <a name="next-steps"></a>다음 단계
가격 책정 계층 및 서비스 제한 각 하나에 대 한 hello에 대 한 자세한 toolearn 참조 [서비스에서 Azure 검색의 제한](search-limits-quotas-capacity.md)합니다.

방문 [용량 계획](search-capacity-planning.md) toolearn 파티션 및 복제본 조합에 대 한 자세한 합니다.

성능 및 toosee 어떻게 tooimplement hello 최적화의 일부 데모가이 문서에서 설명에 자세한 드릴 다운에 대 한 hello 다음 비디오 보기:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
