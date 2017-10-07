---
title: "aaa \"인덱스 (포털-Azure 검색) | \"Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 인덱스를 만듭니다."
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 Azure 검색 인덱스 만들기
> [!div class="op_single_selector"]
> * [개요](search-what-is-an-index.md)
> * [포털](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST (영문)](search-create-index-rest-api.md)
> 
> 

Azure 포털 tooprototype hello 인덱스 기본 제공 디자이너를 사용 하거나 만들는 [검색 인덱스](search-what-is-an-index.md) toorun Azure 검색 서비스에 있습니다. 

## <a name="prerequisites"></a>필수 조건

이 문서에서는 [Azure 구독](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) 및 [Azure Search 서비스](search-create-service-portal.md)를 사용하는 것으로 가정합니다.  

## <a name="find-your-search-service"></a>검색 서비스 찾기
1. Azure 포털 페이지 toohello에 로그인 하 고 hello 검토 [구독에 대 한 서비스 검색](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Azure Search 서비스를 선택합니다.

## <a name="name-hello-index"></a>Hello 인덱스 이름

1. Hello 클릭 **인덱스 추가** hello hello 페이지 위쪽에 hello 명령 모음에서 단추입니다.
2. Azure 검색 인덱스를 명명합니다. 
   * 문자로 시작합니다.
   * 소문자, 숫자 또는 대시(“-”)만 사용합니다.
   * Hello 이름 too60 문자를 제한 합니다.

  hello 인덱스 이름에는 hello Azure 검색 REST API의에서 HTTP 요청을 보내기 위한 및 연결 toohello 인덱스에서 사용 하는 hello 끝점 URL의 일부가 됩니다.

## <a name="define-hello-fields-of-your-index"></a>인덱스의 hello 필드 정의

인덱스 컴퍼지션 포함 한 *필드 컬렉션* index에서 hello 검색 가능한 데이터를 정의 하는 합니다. 보다 구체적으로, 개별적으로 업로드 하는 문서 hello 구조를 지정 합니다. hello Fields 컬렉션에 명명 된 인스턴스 및 인덱스 특성 toodetermine hello 필드를 어떻게 사용할 수 있는 형식의 필수 및 선택 필드가 포함 됩니다.

1. Hello에 **인덱스 추가** 블레이드에서 클릭 **필드 >** tooslide hello 필드 정의 블레이드를 엽니다. 

2. 생성 된 hello 수락 *키* Edm.String 형식의 필드입니다. 기본적으로 hello 필드 이름은 *id* hello 문자열이 충족 한다면 이름을 바꿀 수 있지만 [명명 규칙](https://docs.microsoft.com/rest/api/searchservice/Naming-rules)합니다. 키 필드는 모든 Azure Search 인덱스에 필수이며 문자열이어야 합니다.

3. Toofully을 업로드 하는 hello 문서를 지정 하는 필드를 추가 합니다. 문서를 구성 하는 경우는 *id*, *호텔 이름*, *주소*, *도시*, 및 *지역*를 만들기는 각각에 대 한 hello 인덱스에서 해당 필드입니다. 검토 hello [디자인 지침 아래의 hello 절의](#design) 특성을 설정 하는 데 도움이 필요 합니다.

4. 필요에 따라 필터 식에 내부적으로 사용되는 필드를 추가합니다. Hello 필드의 특성은 검색 작업에서 tooexclude 필드 설정할 수 있습니다.

5. 완료 되 면 클릭 **확인** toosave hello 인덱스를 만듭니다.

## <a name="tips-for-adding-fields"></a>필드 추가를 위한 팁

Hello 포털에서 인덱스를 만들는 키보드 많이 사용 합니다. 이 워크플로에 따라 단계를 최소화합니다.

1. 이름을 입력 하 고 데이터 형식을 설정 하 여 hello 필드 목록을 먼저 작성 합니다.

2. 그런 다음 확인란 사용 하 여 hello 각 특성 toobulk hello 위쪽에 모든 필드에 대 한 hello 설정을 사용 하 고 선택적으로 지울 hello에 대 한 상자 필요 하지 않은 할 필드가 단 몇 합니다. 예를 들어 문자열 필드는 일반적으로 검색할 수 있습니다. 이와 같이 선택할 수 있습니다 **Retrievable** 및 **Searchable** hello tooboth 반환 hello 값 검색 결과에서 필드 뿐만 아니라 hello 필드에 전체 텍스트 검색을 허용 합니다. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>특성 설정을 위한 디자인 지침

언제 든 지 새 필드를 추가할 수 있습니다, 있지만 hello 인덱스의 hello 수명에 대 한 기존 필드 정의 잠깁니다. 이러한 이유로 개발자 단순 인덱스를 만들거나 아이디어를 테스트 하는 드는 포털 페이지 toolook hello를 사용 하 여에 대 한 hello 포털 일반적으로 사용 합니다. 인덱스 디자인에 대 한 자주 반복 쉽게 hello 인덱스를 다시 작성할 수 있도록 코드 기반 접근 방식을 따를 경우 더 효율적입니다.

분석기 및 확인 기 hello 인덱스를 저장 하기 전에 필드와 연결 됩니다. 각 탭된 페이지 tooadd 언어 분석기 또는 확인 기 tooyour 인덱스 정의 통해 있는지 tooclick 수 있습니다.

문자열 필드는 보통 **검색 가능** 및 **조회 가능**으로 표시됩니다.

사용 되는 필드 toonarrow 검색 결과 포함 **Sortable**, **Filterable**, 및 **Facetable**합니다.

필드 특성에 따라 필드가 사용되는 방식(즉, 전체 텍스트 검색, 패싯 탐색, 정렬 작업 등)이 결정됩니다. 다음 표에서 hello 각 특성에 설명 합니다.

|특성|설명|  
|---------------|-----------------|  
|**검색 가능**|전체 텍스트 검색 가능한, 주체 toolexical 분석 인덱싱 중에 단어 분리 등입니다. 검색 가능한 필드 tooa 값이 "sunny day"로 설정 하면 내부적으로 것으로 분할 됩니다 hello 개별 토큰 "sunny"와 "day"입니다. 자세한 내용은 [전체 텍스트 검색 작동 방식](search-lucene-query-architecture.md)을 참조하세요.|  
|**필터링 가능**|**$filter** 쿼리에서 참조됩니다. 형식이 `Edm.String` 또는 `Collection(Edm.String)`인 필터링 가능 필드의 경우 단어 분리가 수행되지 않으므로 정확하게 일치하는 항목만 비교합니다. 예를 들어, 너무 이러한 필드를 설정 하는 경우 "sunny day" `$filter=f eq 'sunny'` 일치 하는 항목을 찾을 수 있지만 `$filter=f eq 'sunny day'` 됩니다. |  
|**정렬 가능**|기본적으로 hello 시스템 설정, 결과 정렬 하지만 정렬 hello 문서에 대 한 필드를 기반으로 구성할 수 있습니다. 형식이 `Collection(Edm.String)`인 필드는 **정렬 가능**으로 설정할 수 없습니다. |  
|**패싯 가능**|일반적으로 카테고리별 적중 횟수가 포함된 검색 결과를 표시하는 데 사용됩니다(예: 특정 도시의 호텔). 형식이 `Edm.GeographyPoint`인 필드에는 이 옵션을 사용할 수 없습니다. **필터링 가능**, **정렬 가능** 또는 **패싯 가능**이고 형식이 `Edm.String`인 필드는 최대 32KB일 수 있습니다. 자세한 내용은 [인덱스 만들기(REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index)를 참조하세요.|  
|**key**|Hello 인덱스 내에서 문서에 대 한 고유 식별자입니다. Hello 키 필드와 정확히 하나의 필드를 선택 해야 하 고 형식의 `Edm.String`합니다.|  
|**조회 가능**|Hello 필드는 검색 결과에 반환 될 수 있는지 여부를 결정 합니다. Toouse 필드를 원하는 경우에 유용 (같은 *이익률*) 필터와 정렬 또는 점수 매기기 메커니즘, 하지만 않으며 원하는 hello 필드 toobe 표시 toohello 최종 사용자가 아닌 합니다. `true` for `key` 로 설정해야 합니다.|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>예제에서는 API 섹션에 사용 되는 hello 호텔 인덱스 만들기

Azure Search API 설명서에는 간단한 *호텔* 인덱스를 제공하는 코드 예제가 들어 있습니다. Hello 스크린샷에서 아래 인덱스 정의 하는 동안 지정 된 hello 프랑스어 언어 분석기를 비롯 한 hello 인덱스 정의 볼 수 있는 hello 포털에서 연습으로 다시 만들 수 있습니다.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>다음 단계

Azure 검색 인덱스를 만든 후 toohello 다음 단계를 이동할 수 있습니다: [hello 인덱스로 검색할 수 있는 데이터를 업로드](search-what-is-data-import.md)합니다.

또는 인덱스를 보다 자세히 살펴볼 수도 있습니다. 또한 toohello Fields 컬렉션 인덱스 지정 분석기, 확인 기, 점수 매기기 프로필 및 CORS 설정 합니다. hello 포털은 제공 탭된 페이지 hello 가장 일반적인 요소를 정의 하기 위한: 필드, 분석기, 및 확인 기입니다. toocreate 또는 다른 요소를 수정, hello REST API 또는.NET SDK를 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목

 [전체 텍스트 검색 작동 방식](search-lucene-query-architecture.md)  
 [Search 서비스 REST API](https://docs.microsoft.com/rest/api/searchservice/) [.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

