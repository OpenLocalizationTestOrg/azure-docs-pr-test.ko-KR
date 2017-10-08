---
title: "Azure 검색의 aaaHow toomodel 복잡 한 데이터 형식 | Microsoft Docs"
description: "일반 행 집합 및 컬렉션 데이터 형식을 사용하여 Azure Search 인덱스에서 중첩된 데이터 또는 계층적 데이터 구조를 모델링할 수 있습니다."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Azure 검색의 toomodel 복잡 한 데이터 형식을 하는 방법
외부 데이터 집합 사용 toopopulate Azure 검색 인덱스 연결 된 해제 되지 않도록 깔끔하게 테이블 형식의 행 집합을 계층적 또는 중첩 된 하위 구조체 경우도 있습니다. 이러한 구조의 예에는 한 고객에 대한 여러 위치와 전화 번호, 단일 SKU에 대한 여러 색과 크기, 한 권의 책에 대한 여러 저자 등이 포함될 수 있습니다. 모델링 용어에 표시 될 수 있습니다 이러한 구조 참조 tooas *복잡 한 데이터 형식을*, *복합 데이터 형식*, *복합 데이터 형식*, 또는 *집계 데이터 형식*, 몇 가지 tooname 합니다.

Azure 검색에서는 복잡 한 데이터 형식은 기본적으로 지원 되지 않습니다 되지만 hello 구조를 평면화 하 고 사용 하 여 다음의 2 단계 프로세스를 포함 하는 검증 된 문제를 해결 한 **컬렉션** 데이터 형식 tooreconstitute hello 내부 구조입니다. 이 문서에서 설명 하는 hello 기법 다음 허용 hello 콘텐츠 toobe 검색 결과, 패싯, 필터링 및 정렬 합니다.

## <a name="example-of-a-complex-data-structure"></a>복합 데이터 구조의 예
일반적으로, 문제의 hello 데이터에는 Azure Cosmos DB와 같은 NoSQL 저장소에 있는 항목 또는 JSON 또는 XML 문서 집합으로 저장 됩니다. 구조적으로 hello 챌린지 toobe 검색 하 고 필터링 해야 하는 여러 개의 자식 항목이 하는 것과 형태소 분석 합니다.  Hello 해결 방법을 설명 하는 시작 점으로 hello 예를 들어 연락처의 집합을 나열 하는 JSON 문서에 다음을 수행 합니다.

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Hello 필드 라는 'id', 'name' 및 '회사' 쉽게 매핑할 수 있는 Azure 검색 인덱스 내에서 필드로 일대일, hello '위치' 필드 위치,으로 위치 Id 위치 설명 세트의 배열을 포함 합니다. Azure 검색에서 지 원하는 데이터 형식에 없는 있다고 가정이 항목이 필요한 다른 방식으로 toomodel Azure 검색에서 합니다. 

> [!NOTE]
> 이 기술은에 설명 되어 Kirk Evans 하 여 블로그 게시물을 [Azure 검색 DocumentDB 인덱싱](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), "flattening hello data" 라는 필드가 있는 그에 따라 기법을 보여 주는 `locationsID` 및 `locationsDescription` 모두 [컬렉션](https://msdn.microsoft.com/library/azure/dn798938.aspx) (또는 문자열의 배열)입니다.   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>1 부: hello 배열 개별 필드로 결합
이 데이터 집합을 제공 하는 Azure 검색 인덱스 toocreate hello 중첩된 구조에 대 한 개별 필드를 만들: `locationsID` 및 `locationsDescription` 의 데이터 형식과 [컬렉션](https://msdn.microsoft.com/library/azure/dn798938.aspx) (또는 문자열의 배열)입니다. 이러한 필드에 hello에 '1' 및 '2' hello 값 인덱스는 `locationsID` John Smith 및 hello 값 '3' & '4' hello에 대 한 필드 `locationsID` Jen Campbell에 대 한 필드입니다.  

Azure Search의 데이터는 다음과 같습니다. 

![샘플 데이터, 2행](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>2 부: hello 인덱스 정의의 컬렉션 필드를 추가 합니다.
Hello 인덱스 스키마에 hello 필드 정의는 비슷한 예는 toothis 보일 수 있습니다.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>검색 동작의 유효성을 검사 하 고 필요에 따라 hello 인덱스 확장
만든된 hello 인덱스 및 hello 로드 된 데이터 라고 가정할 경우 hello 데이터 집합에 대 한 hello 솔루션 tooverify 검색 쿼리 실행을 테스트할 수 있습니다. 각 **컬렉션** 필드는 **검색 가능**해야 하고, **필터링 가능**해야 하며 **패싯 가능**해야 합니다. 같은 쿼리 toorun 수 있어야 합니다.

* ' Adventureworks 본사 ' hello에서 근무 하는 모든 사용자를 찾습니다.
* ' 홈 오피스 '에서 작업 하는 사람의 hello 개수를 가져옵니다.  
* ' 홈 오피스 '에서 작업 하는 hello 인력, 각 위치에 hello 인원 수와 함께 작동 하는 다른 어떤 사무실을 보여 줍니다.  

이 기술은 떨어져 있는 대체 하는 것은 toodo 결합으로 hello 위치 id hello 위치 설명 하는 검색을 식별할 때. 예:

* Home Office가 있고 위치 ID가 4인 사용자를 모두 찾습니다.  

이 다음과 같이 hello 원본 콘텐츠를 기억 하는 경우:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

그러나 이제 별도 필드로 hello 데이터 구분 했습니다, 있는지 hello Campbell Jen에 대 한 홈 오피스 너무 관련 된 것 이면 알 수 없습니다`locationsID 3` 또는 `locationsID 4`합니다.  

이 경우 toohandle hello 데이터 모두를 하나의 컬렉션으로 결합 하는 hello 인덱스의 다른 필드를 정의 합니다.  이 예에서는이 필드 라고 합니다 `locationsCombined` hello 콘텐츠를 구분할 म 및는 `||` 생각 하는 모든 구분 기호 문자 콘텐츠에 대 한 고유한 것을 선택할 수는 있지만 합니다. 예: 

![샘플 데이터, 구분 기호가 있는 2행](./media/search-howto-complex-data-types/sample-data-2.png)

이 `locationsCombined` 필드를 사용하여 다음과 같이 더 많은 쿼리를 사용할 수도 있습니다.

* ‘Home Office’에서 근무하며 위치 ID가 ‘4’인 사용자 수를 표시합니다.  
* ‘Home Office’에서 근무하며 위치 ID가 ‘4’인 사용자를 검색합니다. 

## <a name="limitations"></a>제한 사항
이 기술은 여러 시나리오에서 유용하지만 모든 경우에 적용되지는 않습니다.  예:

1. 복잡 한 데이터 형식에는 정적 필드 집합이 없는 되었으며 방법은 toomap 없는 경우 모든 hello 가능한 tooa 단일 필드를 입력 합니다. 
2. Hello Azure 검색 인덱스에서 업데이트 toobe 정확히 필요한 몇 가지 추가 작업 toodetermine 필요 중첩 hello 개체 업데이트

## <a name="sample-code"></a>샘플 코드
예 설정 방법에 tooindex 복잡 한 JSON 데이터를 Azure 검색에 파악 하 고이이 데이터 집합을 통해 다양 한 쿼리를 수행할 [GitHub 리포지토리](https://github.com/liamca/AzureSearchComplexTypes)합니다.

## <a name="next-step"></a>다음 단계
[복잡 한 데이터 형식에 대 한 기본 지원에 대 한 투표](https://feedback.azure.com/forums/263029-azure-search) hello Azure 검색 UserVoice 페이지 및 추가 입력을 제공할 싶다는 의사를 us tooconsider 기능 구현에 대 한 합니다. 에 Twitter에서 직접 toome 또한 교류할 수 @liamca합니다.

