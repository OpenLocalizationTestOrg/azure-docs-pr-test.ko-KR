---
title: "Azure 검색 aaaWhat | Microsoft Docs"
description: "Azure 검색은 완벽하게 관리되는 호스트된 클라우드 검색 서비스입니다. 이 기능 개요에 대해 자세히 알아보세요."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>Azure 검색이란?
Azure Search는 개발자에게 웹, 모바일 및 엔터프라이즈 응용 프로그램에 대한 풍부한 검색 환경을 추가하기 위한 API 및 도구를 제공하는 SaaS(Search-as-a-Service) 클라우드 솔루션입니다.

간단한 통해 기능이 노출 됩니다 [REST API](/rest/api/searchservice/) 또는 [.NET SDK](search-howto-dotnet-sdk.md) 검색 기술의 hello 내재 된 복잡성을 마스크입니다. 또한 tooAPIs hello Azure 포털 관리 및 프로토타입 지원을 제공합니다. 인프라 및 가용성은 Microsoft에서 관리합니다.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>기능 요약

| Category | 기능 |
|----------|----------|
|전체 텍스트 검색 및 텍스트 분석 | [**전체 텍스트 검색**](search-lucene-query-architecture.md)은 대부분의 검색 기반 앱에서 기본적으로 사용되는 검색 방식입니다. 쿼리는 다음과 같은 지원되는 구문을 사용하여 작성할 수 있습니다. <br/><br/>[**간단한 쿼리 구문**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)은 논리 연산자, 구 검색 연산자, 후위 연산자, 선행 연산자를 제공합니다.<br/><br/>[**Lucene 쿼리 구문**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)은 모든 간단한 쿼리 지원과 유사 항목 쿼리, 근접 검색, 용어 상승 및 정규식을 제공합니다.| 
| 데이터 통합 | Azure Search 인덱스는 JSON 데이터 구조로 제출되기만 하면 모든 원본의 데이터를 수용합니다. <br/><br/> 필요에 따라 Azure에서 지원 되는 데이터 원본의 경우 사용할 수 있습니다 [ **인덱서** ](search-indexer-overview.md) tooautomatically 크롤링 [Azure SQL 데이터베이스](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [Azure Cosmos DB](search-howto-index-documentdb.md), 또는 [Azure Blob 저장소](search-howto-indexing-azure-blob-storage.md) toosync 검색 인덱스의 주 데이터 저장소를 사용 하 여 콘텐츠입니다. Azure Blob 인덱서는 Microsoft Office, PDF 및 HTML 문서를 비롯한 [주요 파일 형식 인덱싱](search-howto-indexing-azure-blob-storage.md)을 위해 *문서 크래킹*을 수행할 수 있습니다. |
| 검색 분석 | [**사용자 지정 어휘 분석기**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search)는 표기 일치 및 정규식을 사용하는 복잡한 검색 쿼리에 사용할 수 있습니다. |
| 언어 지원 | [**언어 분석기** ](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene, 뿐만 아니라 Microsoft의 자연어 프로세서 toointelligently 핸들 언어별 linguistics 56 서로 다른 언어에서에서 사용할 수 있는 동사 시제, 성별, 등 불규칙 한 복수로 명사 (예를 들어 ' 마우스' 및 'mice'), 단어 취소 그래야만, 단어 분리 (언어에 대 한 공백 없이) 등입니다. |
| 지리적 검색 | Azure Search는 지리적 위치를 지능적으로 처리하고, 필터링하고, 표시합니다. 사용자가 tooexplore 데이터 hello 근접 한 검색 결과 tooa 실제 위치를 기반으로 합니다. [이 비디오를 시청](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) 또는 [이 샘플을 검토](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn 더 합니다. |
| 사용자 환경 기능 | [**검색 제안**](https://docs.microsoft.com/rest/api/searchservice/suggesters)은 검색 창의 자동 완성 쿼리에 사용할 수 있습니다. 사용자가 검색어 일부를 입력하면 인덱스의 실제 문서가 제안됩니다. <br/><br/>[**패싯 탐색**](https://docs.microsoft.com/azure/search/search-faceted-navigation)은 단일 쿼리 매개 변수를 통해 사용하도록 설정됩니다. Azure 검색 스스로 학습할된 (예를 들어 toofilter 카탈로그로 항목 필터링 가격 범위 또는 브랜드)에 대 한 hello 코드 숨김 범주 목록으로 사용할 수 있습니다 하는 패싯 탐색 구조를 반환 합니다. <br/><br/> [**필터** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 응용 프로그램의 UI 사용 하는 tooincorporate 패싯 탐색 수, 쿼리 구문이 개선 하 고, 사용자 또는 개발자가 지정한 조건에 따라 필터입니다. Hello OData 구문을 사용 하 여 필터를 만듭니다.<br/><br/> [**방문 횟수 강조** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) 검색 결과에 키워드와 일치 하는 시각적 형식 atting tooa 적용 됩니다. 강조 표시된 조각을 반환할 필드를 선택할 수 있습니다.<br/><br/>[**정렬** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello 인덱스 스키마를 통해 여러 개의 필드에 제공 하 고 단일 검색 매개 변수가 있는 쿼리 단계에서 다음 설정/해제 합니다.<br/><br/> [**페이징** ](search-pagination-page-layout.md) 검색 결과 제한 하는 것이 검색 결과 통해 Azure 검색에서 제공 하는 조정 된 솔루션이 hello 컨트롤과 간단 합니다.  
| 관련성 | [**간단한 점수 매기기**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index)는 Azure Search의 주요 이점입니다. 점수 매기기 프로필을 사용 하는 toomodel 관련성은 hello에 있는 값의 함수에 자체 설명입니다. 예를 들어 신제품이 할 수 있습니다 또는 hello 검색 결과에서 더 높은 제품 tooappear 할인 된 가격으로 합니다. 또한 따로 추적하고 저장한 고객 검색 기본 설정에 따라 개인화된 점수에 태그를 사용하여 점수 매기기 프로필을 만들 수도 있습니다. |
| 모니터링 및 보고 | [**검색 트래픽 분석** ](search-traffic-analytics.md) hello 검색 상자에 입력 하는 사용자 로부터 수집 하 고 분석 된 toounlock 이해 됩니다. <br/><br/>필요한 추가 구성 없이 포털 페이지에서 초당 쿼리 수, 대기 시간 및 제한에 대한 메트릭이 캡처되고 보고됩니다. 인덱스 및 문서 수를 쉽게 모니터링할 수 있으므로 필요에 따라 용량을 조정할 수 있습니다. 자세한 내용은 [서비스 관리](search-manage.md)를 참조하세요. |
| 프로토타입 및 검사용 도구 | Hello hello 포털에서 사용할 수 있습니다 [ **데이터 가져오기 마법사** ](search-import-data-portal.md) tooconfigure 인덱서 인덱스는 인덱스를 디자이너 toostand 및 [ **탐색기 검색** ](search-explorer.md) tootest 쿼리하고 점수 매기기 프로필을 구체화 합니다. 또한 모든 인덱스 tooview 스키마를 열 수 있습니다. |
| 인프라 | hello **항상 사용 가능한 플랫폼** 매우 신뢰할 수 있는 검색 서비스 환경을 보장 합니다. 규모를 적절하게 조정하면 [Azure 검색은 99.9%의 SLA를 제공](https://azure.microsoft.com/support/legal/sla/search/v1_0/)합니다.<br/><br/> **완벽하게 관리 및 확장되는** 종합 솔루션인 Azure Search는 인프라 관리가 전혀 필요 없습니다. 서비스는 더 많은 문서 저장, 더 높은 쿼리 부하 또는 둘 다에서 두 차원 toohandle 확장 하 여 맞춤형된 tooyour 요구를 수 있습니다.

## <a name="how-it-works"></a>작동 방법
### <a name="step-1-provision-service"></a>1단계: 서비스 프로비전
Hello에 Azure 검색 서비스를 회전 시킬 수 있습니다 [Azure 포털](https://portal.azure.com/) 또는 hello 통해 [Azure 리소스 관리 API](/rest/api/searchmanagement/)합니다. 다른 구독자와 공유 hello 무료 서비스 중 하나를 선택할 수 있습니다 또는 [유료 계층](https://azure.microsoft.com/pricing/details/search/) 하는 서비스에 의해 사용 되는 리소스를 집중 합니다. 유료 계층의 경우 다음 2가지 차원에서 서비스를 확장할 수 있습니다. 

- 복제본 toogrow 용량 toohandle 많은 쿼리 로드를 추가 합니다.   
- 더 많은 문서에 대 한 파티션을 toogrow 저장소를 추가 합니다. 

문서 저장소 및 쿼리 처리량을 별도로 처리하여 프로덕션 요구에 따라 리소스 관리를 조정할 수 있습니다.

### <a name="step-2-create-index"></a>2단계: 인덱스 만들기
검색 가능한 콘텐츠를 업로드하려면 먼저 Azure Search 인덱스를 정의해야 합니다. 인덱스는 데이터가 보관된 데이터베이스 테이블과 비슷하며 검색 쿼리를 수용할 수 있습니다. Hello 인덱스 스키마 toomap tooreflect hello 구조를 정의 하려는 toosearch, 데이터베이스의 유사한 toofields hello 문서입니다.

Hello Azure에서에서 스키마를 만들 수 있습니다 프로그래밍 방식으로 사용 하거나 포털 hello [.NET SDK](search-howto-dotnet-sdk.md) 또는 [REST API](/rest/api/searchservice/)합니다.

### <a name="step-3-index-data"></a>3단계: 인덱스 데이터
인덱스를 정의한 후에 준비 tooupload 콘텐츠를 수 있습니다. 밀어넣기 또는 끌어오기 모델을 사용할 수 있습니다.

hello 끌어오기 모델 외부 데이터 원본에서 데이터를 검색합니다. 이 방식은 데이터에 연결, 데이터 읽기 및 데이터 직렬화 등의 데이터 수집 측면을 능률화하고 자동화하는 *인덱서*를 통해 지원됩니다. [인덱서](/rest/api/searchservice/Indexer-operations)는 Azure Cosmos DB, Azure SQL Database, Azure Blob Storage 및 Azure VM에 호스트된 SQL Server에서 사용할 수 있습니다. 필요 시 또는 예약된 데이터 새로 고침을 위해 인덱서를 구성할 수 있습니다.

hello 밀어 넣기 모델 hello SDK 또는 업데이트 된 문서 tooan 인덱스를 보내는 데 사용 되는 REST Api를 통해 제공 됩니다. Hello JSON 형식을 사용 하 여 거의 모든 데이터 집합에서 데이터를 푸시할 수 있습니다. 참조 [추가, 업데이트 또는 삭제에 설명](/rest/api/searchservice/addupdate-or-delete-documents) 또는 [toouse.NET SDK hello 하는 방법)](search-howto-dotnet-sdk.md) 데이터 로드에 대 한 지침입니다.

### <a name="step-4-search"></a>4단계: 검색
수는 인덱스를 채울 후 [검색 쿼리를 실행할](/rest/api/searchservice/Search-Documents) 단순 HTTP를 사용 하 여 tooyour 서비스 끝점에서 REST API 또는.NET SDK hello 요청 합니다.

## <a name="how-it-compares"></a>비교 결과

고객은 [Azure Search의 전체 텍스트 검색](search-lucene-query-architecture.md)이 데이터베이스 제품의 [전체 텍스트 검색](https://en.wikipedia.org/wiki/Full_text_search)과 어떻게 다른지 종종 질문합니다. 이 응답은 Azure 검색 언어 기능 풍부 하 고 Lucene 쿼리, 음성 또는 기타 특수 입력에 대 한 사용자 지정 분석기 Lucene와 Microsoft에서 언어 분석기와 hello 기능 toomerge 데이터를 지원 하 여 보다 유연한 않는다는 여러 원본 hello에서 색인을 검색 합니다. 

다른 굴곡 지점 검색 솔루션 hello 전체 검색 경험을 해결 됩니다. 예를 들어 결과의 사용자 지정 점수 매기기, 자기 주도형 필터링을 위한 패싯 탐색, 적중 항목 강조 표시 및 자동 완성 쿼리 추천 단어 등의 기능이 필요할 수 있습니다. 

쿼리 활동을 모니터링 및 이해하기 위한 도구도 검색 솔루션을 결정할 때 중요하게 고려될 수 있습니다. 예를 들어 Azure Search는 클릭률, 상위 검색, 클릭 없는 검색 등의 메트릭에 대해 [트래픽 분석 검색](search-traffic-analytics.md)을 지원합니다. 본인이 나 가능성이 toofind 여기서 검색은 추가 기능 제품에서는 이러한 기능입니다.

리소스 사용률도 고려됩니다. 자연어 검색은 종종 계산 집약적입니다. 검색 작업 tooAzure 검색의 오프 로드 된 트랜잭션 처리에 대 한 방식으로 toopreserve 컴퓨터 리소스로 고객의 일부입니다. 구체화 검색을 통해 눈금 toomatch 쿼리 볼륨을 쉽게 조정할 수 있습니다.

전용 검색 toogo 결정 하면 클라우드 서비스 또는 온-프레미스 서버 사이 다음 결정이입니다. 클라우드 서비스는 hello 선택 하려는 경우는 [오버 헤드가 최소로 유지 및 유지 관리와 배율로 조정 가능한 턴키 솔루션](#cloud-service-advantage)합니다.

Hello 클라우드 패러다임이 내에서 여러 공급자 hello 기능 toohandle 모호성 검색 입력에 대 한 특정 수준의 전체 텍스트 검색, 지리적 검색와 비교할 수 기준 기능을 제공합니다. 일반적으로는 [특별히 기능](#feature-drilldown), hello 쉽고 Api, 도구 및 hello 가장 적합 한 것을 결정 하는 관리의 전반적인 단순성 또는 합니다.

클라우드 공급자 중에서 Azure Search는 정보 검색 및 콘텐츠 탐색 작업을 주로 검색 기능에 의존하는 앱을 위한 Azure의 콘텐츠 저장소 및 데이터베이스에 대한 전체 텍스트 검색 워크로드에 가장 강력합니다. 주요 장점은 다음과 같습니다.

+ Hello 인덱싱 계층에서의 azure 데이터 통합 (크롤러에)
+ 중앙 관리를 위한 Azure Portal
+ Azure 규모, 안정성 및 세계 수준의 가용성
+ 56개 언어로 안정적인 전체 텍스트 검색을 수행하기 위한 분석기를 사용한 언어 및 사용자 지정 분석
+ [코어 기능 일반적인 toosearch 중심 앱](#feature-drilldown): 점수 매기기, 패싯, 제안, 동의어, 지리적 검색, 등입니다.

> [!Note]
> toobe 명확 하 고 비 Azure 데이터 원본 완벽 하 게 지원 하지만 인덱서 보다는 코드를 더 많이 사용 푸시 방법을 고려 합니다. Api를 사용 하 여 JSON 문서 컬렉션 tooan Azure 검색 인덱스를 파이프할 수 있습니다.

고객 간에 이러한 수 tooleverage hello 광범위 한 Azure 검색의 기능 온라인 카탈로그, 기간 업무 프로그램과 문서 검색 응용 프로그램에 포함 합니다.

## <a name="rest-api--net-sdk"></a>REST API | .Net SDK

Hello 포털에서 많은 작업을 수행할 수 있습니다, 하는 동안 기존 응용 프로그램에 검색 기능 toointegrate 알아보려는 개발자를 위한 Azure 검색이 됩니다. hello 프로그래밍 인터페이스에 따라 제공 됩니다.

|플랫폼 |설명 |
|-----|------------|
|[REST (영문)](/rest/api/searchservice/) | 모든 프로그래밍 플랫폼 및 언어(Xamarin, Java 및 JavaScript 포함)에서 지원하는 HTTP 명령|
|[.NET SDK](search-howto-dotnet-sdk.md) | .NET 래퍼 hello REST API에 대 한 C#에서 효율적인 코딩을 제공 하 고 대상으로 다른 관리 코드 언어 hello.NET Framework |

## <a name="free-trial"></a>무료 평가판
Azure 구독자 수 [hello 무료 계층에 있는 서비스를 프로 비전](search-create-service-portal.md)합니다.

구독자가 아닌 경우 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)할 수 있습니다. 유료 Azure 서비스를 사용해볼 수 있는 크레딧이 제공됩니다. Hello 계정을 유지 하 고 사용 하 여 수 사용 하는 후 [Azure 서비스를 자유](https://azure.microsoft.com/free/)합니다. 명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드 청구 되지 됩니다.

또는 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있음: MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다. 

## <a name="how-tooget-started"></a>Tooget 시작 하는 방법

1. Hello에 서비스를 만들 [무료 계층](search-create-service-portal.md)합니다.

2. 하나 이상의 자습서를 따라 hello 단계별로 실행 합니다. 

  + [어떻게 toouse hello.NET SDK](search-howto-dotnet-sdk.md) hello 주 관리 코드의 단계를 보여 줍니다.  
  + [Hello REST API 시작](https://github.com/Azure-Samples/search-rest-api-getting-started) 동일 표시 hello REST API를 사용 하 여 단계를 제공 하는 hello 합니다.  
  + [Hello 포털에서 첫 번째 인덱스를 만들](search-get-started-portal.md) hello 포털의 기본 제공 인덱싱 및 프로토타입 기능을 보여 줍니다.   

검색 엔진은이 hello 일반적인 드라이버의 hello 웹 및 회사 데이터 저장소 모두에서 모바일 앱에서 정보를 검색 합니다. Azure 검색 대규모 상용 웹 사이트의 검색 환경을 비슷한 toothose을 만들기 위한 도구를 제공 합니다.

프로그램 관리자인 Liam Cavanagh가 제공하는 이 9분짜리 비디오에서 검색 엔진을 통합할 때 앱이 얻는 이점을 알아보세요. 짧은 데모에 Azure Serach의 핵심 기능과 일반적인 워크플로가 제시됩니다. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ 0-3분 구간에서는 주요 기능 및 사용 사례가 나옵니다.
+ 3-4분 구간에서는 서비스 프로비전을 다룹니다. 
+ 4-6 분 동안 데이터 가져오기 마법사 사용 toocreate hello 부동산 기본 제공 데이터 집합을 사용 하 여 인덱스를 설명 합니다.
+ 6-9분 구간에서는 검색 탐색기 및 다양한 쿼리를 다룹니다.


