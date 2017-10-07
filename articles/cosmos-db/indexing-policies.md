---
title: "aaaAzure Cosmos DB 인덱싱 정책 | Microsoft Docs"
description: "Azure Cosmos DB에서 인덱싱의 작동 방식을 파악하고 어떻게 tooconfigure 및 변경 hello 자동 인덱싱 및 성능 향상에 대 한 인덱싱 정책에 알아봅니다."
keywords: "인덱싱 작동 방식, 자동 인덱싱, 데이터베이스 인덱싱"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Azure Cosmos DB는 데이터를 어떻게 인덱싱하나요?

기본적으로 모든 Azure Cosmos DB 데이터가 인덱싱됩니다. 많은 고객은 Azure Cosmos DB toolet 인덱싱의 모든 측면을 자동으로 처리 만족 하지만, Azure Cosmos DB도에서는 지정할 수 있으므로 사용자 지정 및 **인덱싱 정책** 를 만드는 동안 컬렉션에 대 한 합니다. 디자인 하 고, 스키마 유연성을 유지 하면서 hello 인덱스의 hello 모양을 사용자 지정할 수 있으므로 Azure Cosmos DB에서 인덱싱 정책은 보다 유연 하 고 다른 데이터베이스 플랫폼에서 제공 하는 보조 인덱스 보다 강력 합니다. toolearn 인덱싱의 작동 원리 Azure Cosmos DB에서 이해 해야 인덱싱 정책을 관리 함으로써 인덱스 저장소 오버 헤드가, 쓰기 및 쿼리 처리량 및 쿼리 일관성 간 세분화 된 균형 만들 수 있습니다.  

이 문서에서 인덱싱 정책을 Azure Cosmos DB를 자세히 검토를 수행, 인덱싱 정책을 사용자 지정 hello 하는 방법에 대 한 연결 장점과 단점을 이해 합니다. 

이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.

* Hello 속성 tooinclude 재정의 하거나 인덱싱에서 제외할 수 있습니다 어떻게 합니까?
* 최종 업데이트에 대 한 hello 인덱스를 구성 하려면 어떻게 해야 합니까?
* 인덱싱 tooperform Order By 또는 범위 쿼리를 구성 하려면 어떻게 해야 합니까?
* 변경 내용 tooa 컬렉션의 인덱싱 정책을 어떻게 해야 합니까?
* 저장소 및 다른 인덱싱 정책의 성능을 어떻게 비교하나요?

## <a id="CustomizingIndexingPolicy"></a>Hello 인덱싱 정책 컬렉션의 사용자 지정
개발자는 hello Azure Cosmos DB 컬렉션에 기본 인덱싱 정책을 재정의 하 고 hello 다음 측면을 구성 하 여 hello 척도로 상대적 저장소, 쓰기/쿼리 성능 및 쿼리 일관성을 사용자 지정할 수 있습니다.

* **문서 및 인덱스까지/로부터의 경로 포함/제외**. 개발자는 특정 문서 toobe 삽입 하거나 바꾸는 toohello 컬렉션 hello 시 hello 인덱스에 포함 또는 제외를 선택할 수 있습니다. 개발자가 tooinclude 선택 하거나 라고도 함 특정 JSON 속성을 제외할 수도 있습니다. 경로 (와일드 카드 패턴 포함) toobe 인덱스에 포함 된 문서 간에 인덱싱됩니다.
* **다양한 인덱스 유형 구성**. 각 hello 포함 경로 대 한 개발자 hello 유형의 인덱스의 데이터와 예상된 쿼리 작업 및 hello 숫자가/문자열 "precision" 각 경로 대 한 기반으로 컬렉션에 대해 필요한 지정할 수도 있습니다.
* **인덱스 업데이트 모드 구성**. Azure Cosmos DB 지원 hello 인덱싱 Azure Cosmos DB 컬렉션에 대 한 정책을 통해 구성할 수 있는 세 가지 인덱싱 모드: 일관성이 Lazy 및 없음입니다. 

코드 조각에 나와 있는.NET 방법을 따르는 hello tooset hello 컬렉션을 만드는 동안 사용자 지정 인덱싱 정책 합니다. 여기 hello 최대 전체 자릿수에 대 한 문자열 및 숫자 범위 인덱스를 사용 하 여 hello 정책을 설정합니다. 이 정책을 통해 문자열에 대한 Order By 쿼리를 실행할 수 있습니다.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> 인덱싱 정책에 대 한 JSON 스키마 hello 2015-06-03 toosupport 범위 인덱스 문자열에 대 한 REST API 버전의 hello 릴리스로 변경 되었습니다. .NET SDK 1.2.0 및 Java, Python 및 Node.js Sdk 1.1.0 hello 새 정책 스키마를 지원합니다. 이전 Sdk hello REST API 버전 2015-04-08을 사용 하 고 인덱싱 정책의 hello 이전 스키마를 지원 합니다.
> 
> 기본적으로 Azure Cosmos DB는 해시 인덱스를 사용하여 문서 내의 모든 문자열 속성을 일관되게 인덱싱하고, 범위 인덱스를 사용하여 숫자 속성을 인덱싱합니다.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Hello 포털을 사용 하 여 hello 인덱싱 정책을 사용자 지정

Hello 인덱싱 hello Azure 포털을 사용 하 여 컬렉션의 정책을 변경할 수 있습니다. 열기 hello Azure 포털의에서 Azure Cosmos DB 계정 컬렉션 선택 하 고, hello 왼쪽된 탐색 메뉴에서에서 **설정**, 클릭 하 고 **인덱싱 정책**합니다. Hello에 **인덱싱 정책** 블레이드에서 인덱싱 정책 변경 하 고 클릭 **확인** toosave 변경 내용을 합니다. 

### <a id="indexing-modes"></a>데이터베이스 인덱싱 모드
Azure Cosmos DB 세 가지 인덱싱 모드 hello 인덱싱 – Azure Cosmos DB 컬렉션에 대 한 정책을 통해 구성할 수 있는 일관성, Lazy 및 없음 지원 합니다.

**일관 된**: 지정 된 Azure Cosmos DB 컬렉션 수행 hello 쿼리 읽기 지점 (즉, 강력한 제한-부실, hello에 대 한 지정 된 대로 동일한 일관성 수준 hello Azure Cosmos DB 컬렉션의 정책 "일관성"을 지정 하는 경우 세션 최종 또는). hello 인덱스가 hello 문서 업데이트 (예:: insert, replace, update 및 delete Azure Cosmos DB 컬렉션의 문서)의 일부로 동기적으로 업데이트 됩니다.  일치 하는 인덱스가 쓰기 처리량의 가능한 축소의 hello 비용에 일관 된 쿼리를 지원합니다. 이 축소 인덱싱된 toobe 해야 하는 hello 고유 경로의 기능과 "일관성 수준" hello는입니다. 일관성 인덱싱 모드는 "신속하게 쿼리를 즉시 쓰기" 워크로드를 위해 설계되었습니다.

**지연**: tooallow 최대 문서 수집 처리량 Azure Cosmos DB 컬렉션 지연 일관성으로 구성할 수 있습니다; 의미 쿼리는 결국 일치 합니다. hello 인덱스는 Azure Cosmos DB 컬렉션이 때 정지 된, 즉 hello 컬렉션 처리 용량 사용률이 tooserve 사용자 요청 없을 때 비동기적으로 업데이트 됩니다. 아무런 제약 없이 문서 수집을 필요로 하는 "지금 수집, 나중에 쿼리" 워크로드의 경우, "지연" 인덱싱 모드가 적합할 수 있습니다.

**없음**: 인덱스 모드가 "없음"으로 표시되는 컬렉션에는 연관된 인덱스가 없습니다. 이 모드는 Azure Cosmos DB를 키-값 저장소로 이용하고 해당 ID 속성에 의해서만 문서에 액세스하는 경우에 흔히 사용됩니다. 

> [!NOTE]
> 인덱싱 정책을 "None"으로 구성 hello hello 부작용의 모든 기존 인덱스를 삭제 하는 중에 있습니다. 액세스 패턴이 "Id" 및/또는 "자체 링크"만을 필요로 하면 이를 사용합니다.
> 
> 

샘플 표시 방법을 다음 hello hello.NET SDK를 사용 하 여 모든 문서 삽입 작업에서 일관 된 자동 인덱싱을와 Azure Cosmos DB 컬렉션을 만듭니다.

다음 표에서 hello hello 일관성을 hello 인덱싱 모드 (Consistent 및 Lazy) hello 컬렉션과 hello 일관성 수준이 hello 쿼리 요청에 대해 지정 된 구성에 따라 쿼리를 보여 줍니다. 이 모든 인터페이스-REST API Sdk를 사용 하 여 만든 tooqueries를 적용 하거나 내에서 저장 프로시저와 트리거의 합니다. 

|일관성|인덱싱 모드: 일관성|인덱싱 모드: 지연|
|---|---|---|
|강력|강력|최종|
|제한된 부실|제한된 부실|최종|
|세션|세션|최종|
|최종|최종|최종|

Azure Cosmos DB는 없음 인덱싱 모드를 사용할 경우 컬렉션에 대해 실행된 쿼리에 대해 오류를 반환합니다. 명시적 hello 통해 검색으로 계속 쿼리를 실행할 수 `x-ms-documentdb-enable-scan` 헤더 hello REST API 또는 hello에 `EnableScanInQuery` .NET SDK hello 옵션 사용 하 여 요청 합니다. ORDER BY와 같은 일부 쿼리 기능은 `EnableScanInQuery`을(를) 사용한 검색으로 지원되지 않습니다.

hello 다음 표에 나와 hello 인덱싱 모드 (Consistent, Lazy, 및 없음)에 따라 쿼리에 hello 일관성 EnableScanInQuery 지정 된 경우.

|일관성|인덱싱 모드: 일관성|인덱싱 모드: 지연|인덱싱 모드: 없음|
|---|---|---|---|
|강력|강력|최종|강력|
|제한된 부실|제한된 부실|최종|제한된 부실|
|세션|세션|최종|세션|
|최종|최종|최종|최종|

코드 샘플 표시 방법을 따르는 hello hello.NET SDK를 사용 하 여 문서에 대 한 모든 삽입에는 일치 인덱스를 가진 Azure Cosmos DB 컬렉션을 만듭니다.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>인덱스 경로
Azure Cosmos DB 트리로의 JSON 문서와 hello 인덱스를 모델링 하 고 hello 트리 내에서 경로 대 한 tootune toopolicies 있습니다. 문서 내에서 인덱싱에 포함하거나 인덱싱에서 제외할 경로를 선택할 수 있습니다. Hello 쿼리 패턴이 미리 확인 된 경우 시나리오의 더 낮은 인덱스 저장소 및 쓰기 성능을 제공할 수 있습니다.

Hello 루트 (/)로 시작 하 고 hello를 일반적으로 끝나야 하는 인덱스 경로? hello 접두사에 대 한 여러 가능한 값이 있는지를 나타내는 와일드 카드 연산자입니다. 예를 들어 tooserve SELECT * 제품군 F WHERE F.familyName FROM에서 = "Andersen" /familyName/에 대 한 인덱스 경로 포함 해야? hello 컬렉션의 인덱스 정책.

인덱스 경로 hello 사용할 수도 * hello 접두사에서 재귀적으로 경로 대 한 와일드 카드 연산자 toospecify hello 동작 합니다. 예를 들어/페이로드 / * 사용된 tooexclude 인덱싱에서 hello 페이로드 속성 아래에 있는 모든 될 하 수 있습니다.

다음은 hello 인덱스 경로 지정 하기 위한 일반적인 패턴입니다.

| Path                | 설명/사용 사례                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | 컬렉션의 기본 경로입니다. 재귀 toowhole 문서 트리에 적용 합니다.                                                                                                                                                                                                                                   |
| /prop/?             | Hello 다음과 같은 쿼리 tooserve 데 필요한 인덱스 경로 (Hash 또는 Range 형식 사용 각각):<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /prop/*             | Hello 지정 된 레이블 아래의 모든 경로 대 한 인덱스 경로입니다. 작동 하는 쿼리를 수행 하는 hello<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | 인덱스 경로 tooserve 반복 및 JOIN 쿼리 ["a", "b", "c"]와 같은 스칼라 배열에 대해 필요합니다.<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | Tooserve 반복 데 필요한 인덱스 경로 개체의 배열에 대 한 조인 쿼리 같은 [{subprop: "a"}, {subprop: "b"}].<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | Tooserve 쿼리 데 필요한 인덱스 경로 (Hash 또는 Range 형식 사용 각각):<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> 사용자 지정 인덱스 경로 설정 하는 동안 필요한 toospecify hello 기본 hello 특수 한 경로 가리키는 hello 전체 문서 트리에 대 한 인덱싱 규칙은 "/ *"입니다. 
> 
> 

hello 다음 예제에서는 구성 범위는 인덱스를 가진 특정 경로 및 20 바이트는 사용자 지정 전체 자릿수 값:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>인덱스 데이터 형식, 종류 및 전체 자릿수
이전 지나온 어떻게 했으므로 toospecify 경로 살펴보겠습니다 tooconfigure의 경로 대 한 인덱싱 정책을 hello hello 옵션에 사용할 수 있습니다. 모든 경로에 대해 하나 이상의 인덱싱 정의를 지정할 수 있습니다.

* 데이터 형식: **문자열**, **숫자**, **점**, **다각형** 또는 **LineString**(경로별로 데이터 형식당 하나만 포함할 수 있음)
* 인덱스 종류: **해시**(같음 쿼리), **범위**(같음, 범위 또는 Order By 쿼리) 또는 **공간**(공간 쿼리) 
* 정밀도: 해시 인덱스에 대 한 달라 문자열 및 숫자 이며 기본값은 모두에 대해 1 too8에서 3으로 합니다. 범위 인덱스의 경우 이 값은 -1(최대 전체 자릿수)일 수 있으며 문자열 또는 숫자 값에 대해 1-100(최대 전체 자릿수) 범위일 수 있습니다.

#### <a name="index-kind"></a>인덱스 종류
Azure Cosmos DB는 모든 경로에 대해 해시 및 범위 인덱스 종류를 지원합니다(문자열, 숫자 또는 둘 다로 구성할 수 있음).

* **해시** 는 효율적인 같음 및 JOIN 쿼리를 지원합니다. 대부분의 사용 사례에 대 한 해시 인덱스에는 3 바이트의 hello 기본값 보다 더 높은 정밀도 필요 하지 않습니다. 데이터 형식은 문자열 또는 숫자일 수 있습니다.
* **범위**는 효율적인 같음 쿼리, 범위 쿼리(>, <, >=, <=, != 사용) 및 Order By 쿼리를 지원합니다. 또한 Order By 쿼리에는 기본적으로 최대 인덱스 전체 자릿수(-1)가 필요합니다. 데이터 형식은 문자열 또는 숫자일 수 있습니다.

또한 azure Cosmos DB hello 점, 다각형, 또는 LineString 데이터 형식에 대해 지정할 수 있는 모든 경로 대 한 hello 공간 인덱스 종류를 지원 합니다. hello hello 지정된 경로에 길어야와 같은 유효한 GeoJSON 조각 `{"type": "Point", "coordinates": [0.0, 10.0]}`합니다.

* **공간** 은 효율적인 공간(이내 및 거리) 쿼리를 지원합니다. 데이터 형식은 점, 다각형 또는 LineString일 수 있습니다.

> [!NOTE]
> Azure Cosmos DB는 점, 다각형 및 LineStrings의 자동 인덱싱을 지원합니다.
> 
> 

다음은 지원 되는 hello 인덱스 종류와 tooserve 사용된 될 수는 쿼리의 예입니다.

| 인덱스 종류 | 설명/사용 사례                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 해시       | Hash over/prop/? (또는 /) 수 사용된 tooserve hello 다음과 같은 사용 될 쿼리 효율적으로:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Hash over /props/[]/? (또는 / 또는/props /) 수 사용된 tooserve hello 다음과 같은 사용 될 쿼리 효율적으로:<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| 범위      | /prop/? (또는 /) 수 사용된 tooserve hello 다음과 같은 사용 될 쿼리 효율적으로:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| 공간     | /prop/? (또는 /) 수 사용된 tooserve hello 다음과 같은 사용 될 쿼리 효율적으로:<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --with indexing on points enabled<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --with indexing on polygons enabled              |

기본적으로 쿼리 연산자를와 같은 범위에 대 한 오류가 반환 됩니다 > = (모든 자릿수) 범위 인덱스가 있을 경우 필요한 tooserve hello 쿼리는 검색 되는 순서 toosignal에 있습니다. 범위 쿼리에 hello REST API에에서 hello x-ms-documentdb-enable-검색 헤더 또는 hello.NET SDK를 사용 하 여 hello EnableScanInQuery 요청 하는 옵션을 사용 하 여 범위 인덱스 없이 수행할 수 있습니다. Azure Cosmos DB에 대 한 인덱스 toofilter hello를 사용할 수 있는 hello 쿼리에 다른 필터가 있는 경우 오류가 반환 됩니다.

hello 공간 쿼리에 대 한 동일한 규칙이 적용 됩니다. 기본적으로 공간 인덱스가 없으면 hello 인덱스에서 제공 될 수 있는 다른 필터가 없는 경우 공간 쿼리에 대 한 오류가 반환 됩니다. x-ms-documentdb-enable-scan/EnableScanInQuery를 사용하여 스캔으로 수행할 수 있습니다.

#### <a name="index-precision"></a>인덱스 전체 자릿수
인덱스 전체 자릿수를 사용하면 인덱스 저장소 오버헤드와 쿼리 성능 간에 적절한 균형을 유지할 수 있습니다. 숫자-1 ("최대")의 hello 기본 정밀도 구성을 사용 하는 것이 좋습니다. 숫자 JSON의 8 바이트와 되므로 해당 tooa 구성 8 바이트입니다. 일부 범위 맵 toohello 내에서 동일한 값을 의미 항목을 인덱스 1-7 같은 전체 자릿수에 대 한 낮은 값을 선택 합니다. 따라서 인덱스 저장소 공간이 줄어듭니다 하지만 쿼리 실행 tooprocess 더 많은 문서 및 결과적으로, 즉, 더 많은 처리량을 사용 요청 단위입니다.

인덱스 전체 자릿수 구성은 문자열 범위와 함께 사용할 때 실질적으로 더 유용합니다. 문자열 길이 일 수 이후 hello 인덱스 자릿수 hello 선택 문자열 범위 쿼리 및 필요한 인덱스 저장소 공간의 영향 hello 크기 hello 성능을 달라질 수 있습니다. 문자열 범위 인덱스는 1-100 또는 -1("최대값")로 구성할 수 있습니다. 문자열 속성에 대 한 tooperform Order By 쿼리를 원하는 경우 hello 해당 경로 대 한-1의 전체 자릿수를 지정 해야 합니다.

공간 인덱스는 항상 (점, LineStrings, 및 다각형)의 모든 형식에 대 한 hello 기본 인덱스 정밀도 사용 및 대체할 수 없습니다. 

다음 예제는 hello tooincrease hello 정밀도 범위에 대 한 hello.NET SDK를 사용 하 여 컬렉션의 인덱스는 방법을 보여 줍니다. 

**사용자 지정 인덱스 전체 자릿수로 컬렉션 만들기**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Azure Cosmos DB 쿼리에 Order By 사용 하지만 hello hello 최대 전체 자릿수를 사용 하 여 쿼리 경로 대 한 범위 인덱스가 없는 경우 오류가 반환 됩니다. 
> 
> 

마찬가지로 경로는 인덱싱에서 완전히 제외될 수 있습니다. 다음 예제에서는 hello 방법을 tooexclude hello의 전체 섹션에 설명 (규칙 하위 보여 줍니다. 하위 트리) hello를 사용 하 여 인덱싱에서 "*" 와일드 카드입니다.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>인덱싱 옵트인 및 옵트아웃
사용할지 hello 컬렉션 tooautomatically 인덱스 모든 문서를 선택할 수 있습니다. 기본적으로 모든 문서가 자동 인덱싱되지 tooturn를 선택할 수 있습니다 하지만 해제 합니다. 인덱싱을 해제하면 자체 링크를 통해서나 ID를 사용한 쿼리로만 문서에 액세스할 수 있습니다.

자동 인덱싱을 사용 해제 되어 특정 문서 toohello 인덱스만 여전히 선택적으로 추가할 수 있습니다. 반대로 자동 인덱싱을 유지 수 있으며 특정 문서 tooexclude를 선택할 수 있습니다. 인덱싱 구성을 설정/해제는 쿼리할 toobe 필요한 문서에 하위 집합만 있는 경우에 유용 합니다.

예를 들어 hello 다음 샘플에서는 어떻게 hello를 사용 하 여 명시적 문서 tooinclude [DocumentDB API.NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) 및 hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) 속성입니다.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>컬렉션의 hello 인덱싱 정책을 수정
Azure Cosmos DB hello 즉석에서 컬렉션의 toomake 변경 toohello 인덱싱 정책을 허용 합니다. 인덱싱 Azure Cosmos DB 컬렉션에 정책 변경 hello 경로 인덱싱할 수, 해당 정밀도으로 hello 인덱스 자체의 hello 일관성 모델을 포함 하 여 hello 인덱스의 hello 셰이프에서 tooa 변경이 될 수 있습니다. 따라서 인덱싱 정책 변경 새를 변환 하는 hello 이전 인덱스를 효과적으로 필요 합니다. 

**온라인 인덱스 변환**

![인덱싱 작동 방식 – Azure Cosmos DB 온라인 인덱스 변환](./media/indexing-policies/index-transformations.png)

인덱스 변환 온라인으로 hello 이전 정책에 따라 인덱싱된 hello 문서 hello 새 정책에 따라 효율적으로 변환 된 내용이 **hello 쓰기 가용성 또는 hello 프로 비전 된 처리량에 영향을 주지 않고** 의 hello 컬렉션입니다. 읽기의 일관성 hello 및 쓰기 Sdk hello REST API를 사용 하 여 만든 작업 또는에서 저장된 프로시저 및 트리거 내에서 영향을 받지 않는 인덱스 변환 중입니다. 이 있다는 것을 의미 있는 성능 저하 또는 가동 중지 시간 tooyour 앱 인덱싱 정책을 변경 하는 경우.

그러나 인덱스 변환이 진행 된 hello 시간 동안 쿼리는 결국 hello 인덱싱 모드 구성 (Consistent 또는 Lazy)에 관계 없이 일관성 있는 합니다. 그러면도 tooqueries 모든 인터페이스-REST API, Sdk, 적용 되 고 내에서 저장 프로시저와 트리거의 합니다. 마찬가지로 Lazy 인덱싱을와 인덱스 변환 비동기적으로 백그라운드에서 수행 됩니다 hello hello 복제본을 사용할 수 있는 예비 리소스 hello를 사용 하 여 지정된 된 복제본에 대 한 합니다. 

인덱스 변환 만들어집니다 **situ에** (위치)에서, 즉 Azure Cosmos DB 유지 관리 하지 않습니다 hello 인덱스와 스왑 hello 이전 인덱스 아웃 새 hello로의 두 복사본입니다. 즉, 추가 디스크 공간이 없는 필요하지 않거나 인덱스 변환을 수행하는 동안 컬렉션에서 사용할 수 있음을 의미합니다.

인덱싱 정책을 변경 하는 경우 어떻게 hello 변경은 hello 이전 인덱스 toohello 새 하나에 따라 달라 집니다 hello 보다 다른와 같은 값 포함/제외 경로, 인덱스 종류 및 전체 자릿수가 하므로 더 모드 구성 인덱싱 hello에서에서 적용 된 toomove입니다. 이전 정책과 새 정책 모두가 일관성 인덱싱을 사용하는 경우, Azure Cosmos DB는 온라인 인덱스 변환을 수행합니다. Hello 변환 진행 중인 동안 다른 인덱싱 정책 변경 일관 된 인덱싱 모드를 적용할 수 없습니다.

그러나 tooLazy 실행할 수 없거나 진행 중인으로 변환 하는 동안 인덱싱 모드를 이동할 수 있습니다. 

* TooLazy 이동 하면 hello 인덱스 정책 변경 내용이 유효 즉시 하 고 Azure Cosmos DB hello 인덱스를 비동기적으로 다시 시작 합니다. 
* TooNone 이동 하면 다음 hello 인덱스를 삭제 효과적인 즉시 합니다. 이동 하려는 toocancel 진행 중인 경우 tooNone 유용 합니다. 변환 및 다른 인덱싱 정책을 사용 하 여 새로 시작 합니다. 

새 hello를 사용 하 여 한 인덱싱 정책 변경 시작과 수 hello.NET SDK를 사용 하는 경우 **ReplaceDocumentCollectionAsync** hello를 사용 하 여 hello 인덱스 변환의 메서드 및 추적 hello 백분율 진행률  **IndexTransformationProgress** 에서 response 속성을 **ReadDocumentCollectionAsync** 호출 합니다. 다른 Sdk 및 REST API hello 인덱싱 정책을 변경 하기 위한 해당 속성과 메서드를 지원 합니다.

다음은 어떻게 toomodify 컬렉션의 인덱싱 정책을 일관 된 인덱싱 모드 tooLazy에서 보여 주는 코드 조각입니다.

**일관 된 tooLazy에서 인덱싱 정책을 수정합니다**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


다음과 같은 예를 들어 호출 ReadDocumentCollectionAsync 하 여 인덱스 변환의 hello 진행률을 확인할 수 있습니다.

**인덱스 변환의 진행률 추적**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

인덱싱 모드 없음 toohello를 이동 하 여 컬렉션에 대 한 hello 인덱스를 삭제할 수 있습니다. 이 원하는 toocancel 진행 중인 변환 하 고 새를 즉시 시작 하는 경우 작동 하는 유용한 도구를 수 있습니다.

**컬렉션에 대 한 hello 인덱스를 삭제 하는 중**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

가 변경 하는 경우 인덱싱 정책 tooyour Azure Cosmos DB 컬렉션? hello 다음은 hello 가장 일반적인 사용 사례입니다.

* 정상 작동 하는 동안 일관 된 결과 제공 하지만 대체 toolazy 대량 데이터 가져오기 중 인덱싱
* 현재 Azure Cosmos DB 컬렉션, 예를 들어,에서 새 인덱싱 기능을 사용 하 여 hello 공간 인덱스 종류 필요 또는 Order By를 쿼리 하는 지리 공간 처럼 start/hello 문자열이 범위 인덱스 종류 범위 쿼리 문자열
* 인덱스 선택 hello 속성 toobe 전달 하 고 시간이 지남에 따라 변경
* 사용 되는 저장소를 줄이거나 인덱싱 정밀도 tooimprove 쿼리 성능 튜닝

> [!NOTE]
> 인덱싱 정책을 toomodify 버전이 필요한 ReplaceDocumentCollectionAsync를 사용 하 여 >의 hello.NET SDK 1.3.0 =
> 
> 인덱스 변환 toocomplete에 성공적으로 확인 해야 hello 컬렉션에 사용할 수 있는 충분 한 사용 가능한 저장 공간이 있는지 합니다. 저장소 할당량에 도달 하는 hello 컬렉션 hello 인덱스 변환 중단 됩니다. 저장소 공간을 사용할 수 있게 되면 예를 들어 일부 문서를 삭제하는 경우 인덱스 변환은 자동으로 다시 시작됩니다 
> 
> 

## <a name="performance-tuning"></a>성능 튜닝
DocumentDB Api hello hello 인덱스 저장소에 사용 되는 모든 작업에 대해 hello 처리량 비용 (요청 단위)와 같은 성능 메트릭에 대 한 정보를 제공 합니다. 이 정보 다양 한 인덱싱 정책을 사용 하는 toocompare 수 및 성능 조정에 대 한 합니다.

toocheck hello 저장 용량 할당량 및 사용 하 여 컬렉션의 hello 컬렉션 리소스에 대해 HEAD 또는 GET 요청을 실행 하 고 hello x-ms--할당량을 요청 및 hello ms 요청 사용 x 헤더를 검사 합니다. .NET SDK hello에 hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) 및 [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) 속성에 [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) 이러한 해당 값이 포함 .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


각 쓰기 작업에 대해 인덱싱을 toomeasure hello 오버 헤드 (만들기, 업데이트 또는 삭제), hello ms 요청 무료 x 헤더를 검사 (또는 해당 하는 hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) 속성 [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) hello.NET SDK에에서) 이러한 작업을 사용한 요청 단위 toomeasure hello 수 있습니다.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>변경 내용 toohello 인덱싱 정책 지정
인덱싱 정책에 대 한 hello 스키마 변경으로 인 한 REST api 버전 2015-06-03 2015 년 7 월 7 일에 도입 되었습니다. hello SDK 버전의 hello 해당 클래스는 새로운 구현을 toomatch hello 스키마를 갖습니다. 

hello JSON 사양에에서 따라 변경 하는 hello 구현 되었습니다.

* 정책 인덱싱이 문자열에 대한 범위 인덱스 지원
* 각 경로는 각 데이터 형식에 하나씩 여러 인덱스 정의가 존재
* 인덱싱 정확도가 숫자의 경우 1-8, 문자열의 경우 1-100 및 -1(최대 전체 자릿수) 지원
* 경로 세그먼트 큰따옴표 tooescape 각 경로 필요 하지 않습니다. 예를 들어 /”title”/? 대신 /title/?에 대한 경로를 추가할 수 있습니다.
* "모든 경로" 나타내는 hello 루트 경로으로 나타낼 수 / * (또한 너무 /)

버전 1.1.0로 작성 된 사용자 지정 인덱싱 정책을 사용 하 여 컬렉션을 프로 비전 하는 코드가 있는 경우 hello.NET SDK를 toochange 해야 응용 프로그램 코드가 toohandle 순서 toomove tooSDK 버전 1.2.0에서에서 이러한 변경 합니다. 인덱싱 정책을 구성 하는 코드가 있는 하지 않거나 이전 SDK 버전을 사용 하 여 toocontinue를 계획 하는 경우 없습니다 변경이 필요 합니다.

실용적인 비교에 대 한 하나의 예에서는 사용자 지정 인덱싱 정책을 사용 하 여 작성 hello REST API 버전 2015-06-03 뿐 아니라 이전 버전 2015-04-08 hello 다음과 같습니다.

**이전 인덱싱 정책 JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**현재 인덱싱 정책 JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>다음 단계
아래에 인덱스 정책 관리 샘플 및 toolearn를 Azure Cosmos DB의 쿼리 언어에 대 한 자세한 hello 링크를 따르십시오.

1. [DocumentDB API .NET 인덱스 관리 코드 샘플](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [DocumentDB API REST 컬렉션 작업](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [SQL을 사용한 쿼리](documentdb-sql-query.md)

