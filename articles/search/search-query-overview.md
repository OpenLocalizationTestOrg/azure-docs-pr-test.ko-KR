---
title: "Azure 검색 인덱스 aaaQuery | Microsoft Docs"
description: "Azure 검색에서 검색 쿼리를 작성 하 고 검색 매개 변수 toofilter 및 정렬 검색 결과 사용 합니다."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Azure 검색 인덱스 쿼리
> [!div class="op_single_selector"]
> * [개요](search-query-overview.md)
> * [포털](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST (영문)](search-query-rest-api.md)
> 
> 

검색 요청 tooAzure 검색을 제출할 때 응용 프로그램의 hello 검색 상자에 입력 하는 hello 실제 단어와 함께 지정할 수 있는 매개 변수는 여러 가지가 있습니다. 이 쿼리 매개 변수 허용 tooachieve hello의 일부 하위 수준 제어 [전체 텍스트 검색 환경](search-lucene-query-architecture.md)합니다.

다음은 Azure 검색의 hello 쿼리 매개 변수를 사용 하는 일반적인를 간략하게 설명 하는 목록입니다. 쿼리 매개 변수 및 해당 명령의 동작은 전체 검사에 대 한 참조 하십시오 hello 세부 hello에 대 한 페이지 [REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) 및 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary)합니다.

## <a name="types-of-queries"></a>쿼리 유형
Azure 검색은 많은 옵션 toocreate 매우 강력한 쿼리를 제공합니다. hello 2 주 쿼리를 사용 하 여 유형은 `search` 및 `filter`합니다. A `search` 쿼리는 모든 페이지에서 하나 이상의 단어로 검색 *검색 가능한* 인덱스의 필드 및 toowork Bing 이나 Google 같은 검색 엔진 예상 hello 방식으로 작동 합니다. `filter` 쿼리는 인덱스의 *필터링 가능한* 모든 필드에 걸쳐 부울 식을 계산합니다. 와 달리 `search` 쿼리, `filter` 쿼리 문자열 필드에 대 한 대/소문자 구분은 의미 하는 필드의 정확한 내용을 hello와 일치 합니다.

검색 및 필터를 함께 또는 별도로 사용할 수 있습니다. Hello 필터는 함께 사용할 경우 첫 번째 toohello 전체 인덱스를 적용 하 고 hello 검색은 hello 필터 hello 결과에서 수행 하는 다음 합니다. 따라서 필터는 hello 하는 설명서의 검색 쿼리 요구 tooprocess hello를 줄여 주므로 유용한 방법은 tooimprove 쿼리 성능을 수 있습니다.

필터 식에 대 한 hello 구문을 hello의 하위 집합인 [OData 필터 언어](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)합니다. 검색 쿼리에 대 한 hello 중 하나를 사용할 수 있습니다 [간단한 구문을](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) 또는 hello [Lucene 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) 아래 설명 하는 합니다.

### <a name="simple-query-syntax"></a>단순 쿼리 구문
hello [단순 쿼리 구문을](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) 는 Azure 검색에 사용 된 hello 기본 쿼리 언어입니다. 일반적인 검색 연산자 hello AND, OR, NOT, 구, 접미사 및 우선 순위가 연산자를 포함 하 여 hello 단순 쿼리 구문을 지원 합니다.

### <a name="lucene-query-syntax"></a>Lucene 쿼리 구문
hello [Lucene 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) toouse hello 널리 채택 하 고의 일환으로 개발 표현이 가능한 쿼리 언어로 있습니다 [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html)합니다.

이 쿼리 구문을 사용 하면 tooeasily 달성 기능을 수행 하는 hello: [필드 범위 쿼리에](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [퍼지 검색](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [근접 검색](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ 부스트 용어](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [정규식 검색](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [와일드 카드 검색](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [구문 기초](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), 및 [사용 하는 쿼리 부울 연산자](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean)합니다.

## <a name="ordering-results"></a>결과 정렬
검색 쿼리에 대 한 결과 받을 때 Azure 검색 역할 특정 필드의 값으로 정렬 하는 hello 결과 요청할 수 있습니다. 기본적으로 Azure 검색 hello에서 파생 된 각 문서의 검색 점수 순위에 따라 hello 검색 결과 정렬 [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)합니다.

Azure 검색 tooreturn hello 검색 점수 이외의 값으로 정렬 된 결과 원하는 경우에 hello을 사용할 수 있습니다 `orderby` 매개 변수를 검색 합니다. Hello hello 값을 지정할 수 있습니다 `orderby` 매개 변수 tooinclude 필드 이름을 지정 하 고 toohello 호출 [ `geo.distance()` 함수](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) 지리 공간 값에 대 한 합니다. 각 식은 올 수 있습니다 `asc` tooindicate 결과 오름차순으로 요청 된 및 `desc` tooindicate 결과 내림차순 요청 됩니다. hello 기본 순위 오름차순입니다.

## <a name="paging"></a>페이징
Azure 검색 쉽게 tooimplement를 사용 하면 검색 결과의 페이징 합니다. Hello를 사용 하 여 `top` 및 `skip` 매개 변수를 있습니다 좋은 검색 UI 사례를 사용 하는 쉽게 관리할 수 있는, 순서가 지정 된 하위 집합에서 tooreceive hello 총 검색 결과 집합을 허용 하는 검색 요청 원활 하 게 실행할 수 있습니다. 이러한 더 작은 하위 집합 결과 받을 때 hello 총 검색 결과 집합에 hello 문서 수를 받을 수도 있습니다.

Hello 문서에서 검색 결과 페이징 하는 방법에 대 한 자세히 알아볼 수 있습니다 [toopage 검색 Azure 검색의 결과 어떻게](search-pagination-page-layout.md)합니다.

## <a name="hit-highlighting"></a>적중 항목 강조 표시
Azure 검색에서는 hello 검색 쿼리와 일치 하는 검색 결과의 정확한 부분 hello 강조 쉬워진 hello를 사용 하 여 `highlight`, `highlightPreTag`, 및 `highlightPostTag` 매개 변수입니다. 지정할 수 있습니다 *검색 가능한* 필드 지정 문자열 태그 tooappend toohello 시작 하 고 hello의 끝 일치 하는 텍스트는 Azure 검색 정확한 hello 반환 뿐만 아니라 강조가 일치 하는 텍스트에 있어야 합니다.

## <a name="try-out-query-syntax"></a>쿼리 구문 사용

hello 가장 좋은 방법은 toounderstand 구문 차이점 쿼리를 제출 하 고 결과 검토 하는 것입니다.

+ 사용 하 여 [탐색기 검색](search-explorer.md) hello Azure 포털의에서. 배포 하 여 [hello 샘플 인덱스](search-get-started-portal.md), hello 포털에서 도구를 사용 하는 시간 (분)의 hello 인덱스를 쿼리할 수 있습니다.

+ 사용 하 여 [Fiddler](search-fiddler.md) 또는 Chrome 우체부 toosubmit 쿼리 tooan 인덱스 tooyour 검색 서비스를 업로드 합니다. 두 도구 모두 REST 호출 tooan HTTP 끝점을 지원 합니다. 
