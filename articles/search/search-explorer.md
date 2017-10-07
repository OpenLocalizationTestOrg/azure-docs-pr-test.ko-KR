---
title: "aaa \"는 인덱스 (포털-Azure 검색) 쿼리하여 | \"Microsoft Docs"
description: "Hello Azure 포털의 검색 탐색기에서 검색 쿼리를 실행 합니다."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>검색 탐색기를 사용 하 여 hello Azure 포털에서에서 Azure 검색 인덱스를 쿼리 합니다.
> [!div class="op_single_selector"]
> * [개요](search-query-overview.md)
> * [포털](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST (영문)](search-query-rest-api.md)
> 
> 

이 문서에서는 어떻게 tooquery Azure 검색 인덱스를 사용 하 여 **탐색기 검색** hello Azure 포털의에서. 서비스에서 검색 탐색기 toosubmit 전체 또는 단순 Lucene 쿼리 문자열 tooany 기존 인덱스를 사용할 수 있습니다.

## <a name="open-hello-service-dashboard"></a>열기 hello 서비스 대시보드
1. 클릭 **모든 리소스** hello hello의 왼쪽에 hello 점프 막대 [Azure 포털](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)합니다.
2. Azure Search 서비스를 선택합니다.

## <a name="select-an-index"></a>인덱스 선택

선택 hello 인덱스 toosearch hello에서 원하는 **인덱스** 바둑판식으로 배열입니다.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Search Explorer 열기

Hello 탐색기 검색 타일 tooslide 열기 hello 검색 표시줄을 클릭 하 고 결과 창.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>검색 시작

Hello 검색 탐색기를 사용 하는 경우 지정할 수 있습니다 [쿼리 매개 변수](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello 쿼리 합니다.

1. **쿼리 문자열**에서 쿼리를 입력한 다음 **검색** 키를 누릅니다. 

   hello 쿼리 문자열은 자동으로 구문 분석 hello 적절 한 요청으로 URL toosubmit hello Azure 검색 REST API에 대 한 HTTP 요청입니다.   
   
   모든 유효한 전체 또는 단순 Lucene 쿼리 구문을 toocreate hello 요청을 사용할 수 있습니다. hello `*` 문자는 임의의 순서로 모든 문서를 반환 하는 해당 tooan 비어 있거나 지정 되지 않은 검색 합니다.

2. **결과**, 쿼리 결과 원시 JSON으로 표시 됩니다. 동일한 toohello 페이로드 반환 프로그래밍 방식으로 요청을 실행 하는 경우에 HTTP 응답 본문입니다.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>다음 단계

다음 리소스는 hello 추가 쿼리 구문 정보 및 예제를 제공 합니다.

 + [단순 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Lucene 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Lucene 쿼리 구문 예제](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData 필터 식 구문](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 