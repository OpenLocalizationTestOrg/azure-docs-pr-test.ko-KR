---
title: "Azure Cosmos DB DocumentDB API에 대 한 쿼리 aaaSQL | Microsoft Docs"
description: "Azure Cosmos DB에 대한 SQL 구문, 데이터베이스 개념 및 SQL 쿼리를 알아봅니다. SQL은 Azure Cosmos DB에서 JSON 쿼리 언어로 사용될 수 있습니다."
keywords: "sql 구문, sql 쿼리, 여러 SQL 쿼리, json 쿼리 언어, 데이터베이스 개념 및 sql 쿼리, 집계 함수"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리
Microsoft Azure Cosmos DB는 JSON 쿼리 언어인 SQL(구조적 쿼리 언어)을 사용한 문서 쿼리를 지원합니다. Cosmos DB는 스키마가 없습니다. 해당 약정 toohello JSON 데이터 모델 hello 데이터베이스 엔진 내에서 직접을 통해 명시적 스키마 나 보조 인덱스를 만들어 사용 하지 않고도 자동 JSON 문서를 인덱싱 수를 제공 합니다. 

Cosmos DB에 대 한 hello 쿼리 언어를 디자인 하는 동안 두 가지 목표를가지고 했습니다.

* 새로운 JSON 쿼리 언어를 한계 대신 SQL toosupport를 싶었기 합니다. SQL은 hello 가장 친숙 하 고 인기 있는 쿼리 언어 중 하나입니다. Cosmos DB SQL은 JSON 문서에 대한 풍부한 쿼리를 위한 공식 프로그래밍 모델을 제공합니다.
* JSON 문서 데이터베이스로 JavaScript hello 데이터베이스 엔진에서 직접 실행할 수 있는 싶었기 toouse JavaScript 프로그래밍 모델 hello 기반으로 쿼리 언어에 대 한 합니다. DocumentDB API SQL hello 작성과 JavaScript의 형식 시스템, 식 평가, 및 함수 호출 합니다. 따라서 관계형 프로젝션, JSON 문서에 대한 계층적 탐색, 자체 조인, 공간 쿼리, JavaScript로만 작성된 UDF(사용자 정의 함수) 호출 등을 위한 일반 프로그래밍 모델을 제공합니다. 

이러한 기능 hello 응용 프로그램과 hello 데이터베이스 간의 주요 tooreducing hello 마찰 있고 있는 개발자 생산성에 대 한 중요 한 것으로 생각 합니다.

다음 비디오에서는 Aravind Ramachandran Cosmos DB의 쿼리 기능에 표시 하는 hello를 시청 하 여 및 방문 하 여 시작 하는 것이 좋습니다 우리의 [Query Playground](http://www.documentdb.com/sql/demo), 고 수 있는 Cosmos DB 사용해에 대 한 SQL 쿼리를 실행 합니다. 이 데이터 집합입니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

그런 다음 반환 된 몇 가지 간단한 JSON 문서 및 SQL 명령 안내 하는 SQL 쿼리 자습서 시작 위치 toothis 문서.

## <a id="GettingStarted"></a>Cosmos DB의 SQL 명령 시작하기
toosee Cosmos DB SQL에서 보겠습니다 몇 가지 간단한 JSON 문서로 시작 하 고 작업을 몇 가지 간단한 쿼리를 안내 합니다. 두 가족에 대한 다음 두 개의 JSON 문서를 고려해 보세요. Cosmos DB에서는 필요 하지 않습니다 toocreate 모든 스키마 또는 보조 인덱스 명시적으로 합니다. 쿼리할 및 단순히 tooinsert hello JSON 문서 tooa Cosmos DB 컬렉션을 필요 합니다. 간단한 JSON 가지 주소 및 등록 정보 hello Andersen 제품군, hello 부모, 자식 (및의 애완 동물)에 대해 설명 합니다. hello 문서 문자열, 숫자, 부울, 배열 및 중첩 된 속성에 있습니다. 

**문서**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

다음은 한 가지 미묘한 차이점이 있는 두 번째 문서입니다. `givenName` 및 `familyName`이 `firstName` 및 `lastName` 대신 사용됩니다.

**문서**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

이제 몇 가지 쿼리 시도 하세요.이 데이터 toounderstand에 대 한 hello 중 일부의 핵심 요소 DocumentDB API SQL 합니다. Hello 다음 hello id 필드와 일치 하는 반환 hello 문서를 쿼리 하는 예를 들어 `AndersenFamily`합니다. 이기 때문에 `SELECT *`, hello 쿼리의 hello 출력은 JSON 문서를 완료 하는 hello:

**쿼리**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


이제 hello 경우를 JSON 출력을 다른 모양에 tooreformat hello이 필요한 경우를 살펴보겠습니다. 이 쿼리 hello 주소 도시 이름과 같은 이름을 hello hello 상태로 때 두 개의 선택 된 필드 이름 및 도시와 함께 프로젝트 새 JSON 개체입니다. 이 경우 "NY, NY"가 일치합니다.

**쿼리**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**결과**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


hello 다음 쿼리 id와 일치 하는 hello 제품군의 자식 항목의 모든 hello 지정 된 이름을 반환 `WakefieldFamily` 거주 hello 도시별으로 정렬 합니다.

**쿼리**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**결과**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


주목할 만한 몇 가지 hello Cosmos DB 쿼리 언어를 통해 지금까지 살펴본 hello 예제에서는 toodraw 주의 tooa 하려는:  

* DocumentDB API SQL은 JSON 값에 대해 작동하므로 행과 열 대신 트리 모양의 엔터티를 다룹니다. Hello 언어를 임의 깊이에 hello 트리의 toonodes를 같은 참조할 수 있습니다 따라서 `Node1.Node2.Node3…..Nodem`, 비슷한 toorelational SQL 참조 toohello 두 파트 참조의 `<table>.<column>`합니다.   
* hello 구조적 쿼리 언어 작동 하는 스키마가 지정 되지 않은 데이터. 따라서 시스템 요구 사항 toobe 바인딩 종류를 동적으로 hello 합니다. hello 같은 식 향상 시킬 다른 문서에서 여러 유형의 합니다. hello 쿼리 결과의 유효한 JSON 값이 있지만 고정된 스키마의 toobe 보장할 수 없습니다.  
* Cosmos DB는 엄격한 JSON 문서만 지원합니다. 즉 hello 형식 시스템 및 식에는 JSON 형식에만 제한 toodeal 됩니다. Toohello 참조 [JSON 사양](http://www.json.org/) 내용을 확인 합니다.  
* Cosmos DB 컬렉션은 JSON 문서의 스키마 없는 컨테이너입니다. 데이터 엔터티 컬렉션의 문서 및 내에서에서 hello 관계 제약 아니라에 의해 기본 키 및 외래 키 관계에 암시적으로 캡처됩니다. 이 문서의 뒷부분에서 설명 하는 hello 문서 간 조인 측면에서 살펴볼 중요 한 부분입니다.

## <a id="Indexing"></a> Cosmos DB 인덱싱
Hello DocumentDB API SQL 구문에 들어가기 전에 hello Cosmos db에서 디자인 인덱싱 살펴볼 됩니다. 

hello 데이터베이스 인덱스의 목적은 다양 한 폼 및 최소 리소스 사용 (예: CPU 및 입/출력)를 사용 하 여 셰이프 tooserve 쿼리 좋은 처리량과 낮은 대기 시간을 제공 하는 중입니다. 종종 hello 다양 한 hello 올바른 인덱스는 데이터베이스를 쿼리 하기 위한 많은 계획과 실험 필요 합니다. 이 방법을 사용 하는 경우 여기서 hello 데이터 tooa 엄격한 스키마 준수 하지 않음 고 신속 하 게 진화 함에 따라 스키마가 지정 되지 않은 데이터베이스에 대 한 합니다. 

따라서 hello Cosmos DB 인덱싱 하위 시스템의으로 설계 했으므로 때 다음과 같은 목표가 hello를 설정 합니다.

* 스키마를 요구 하지 않고 문서를 인덱싱할: hello 인덱싱 하위 시스템 스키마 정보를 필요로 하지 않거나 hello 문서 스키마에 대 한 모든 있다고 가정 합니다. 
* 효율적이 고 풍부한 관계형 및 계층적, 쿼리에 대 한 지원: hello 인덱스 언어를 지 원하는 hello Cosmos DB 쿼리를 효율적으로 관계형 및 계층적 프로젝션에 대 한 지원을 포함 합니다.
* 쓰기 지속적인된 볼륨 사항이 발생 하더라도 일관 된 쿼리에 대 한 지원: 쓰기 처리량 워크 로드에 일관 된 쿼리로 hello 인덱스가에서 업데이트 되기 효율적으로, 증분 및 온라인 쓰기 지속적인된 볼륨의 hello 면 합니다. hello 일치 인덱스 업데이트는 hello 일관성 수준 hello 구성 된 사용자 hello 문서 서비스에서 중요 한 tooserve hello 쿼리입니다.
* 다중 테 넌 트에 대 한 지원: 테 넌 트 간에 리소스 관리를 위한 hello 예약 기반 모델 들어 인덱스 업데이트는 hello 예산 복제본 당 할당 된 시스템 리소스 (CPU, 메모리 및 입/출력 작업 / 초) 내에서 수행 됩니다. 
* 저장소 효율성: 비용 효율성에 대 한 hello 디스크에 저장소 오버 헤드가 hello 인덱스의는 경계 및 예측 가능 합니다. 이 Cosmos DB를 사용 하면 hello 개발자 toomake 비용 기반 관계 인덱스 오버 헤드가 관계 toohello 쿼리 성능이 매우 중요 합니다.  

Toohello 참조 [Azure Cosmos DB 샘플](https://github.com/Azure/azure-documentdb-net) tooconfigure 컬렉션에 대 한 인덱싱 정책을 hello 하는 방법을 보여 주는 샘플에 대 한 MSDN에 있습니다. Hello Azure Cosmos DB SQL 구문의 hello 세부 정보를 이제 가져올 보겠습니다.

## <a id="Basics"></a>Azure Cosmos DB SQL 쿼리의 기본 사항
ANSI-SQL 표준에 따라 모든 쿼리는 SELECT 절과 선택적 FROM 및 WHERE 절로 구성됩니다. 일반적으로 각 쿼리에 대 한 hello 소스 hello FROM 절에 열거 됩니다. 그런 다음 hello JSON 문서의 하위 집합 WHERE 절 hello 소스 tooretrieve에 적용 되는 hello에서 필터링. Hello SELECT 절을 사용 하는 마지막으로, tooproject hello 요청한 hello에 대 한 JSON 값 목록을 선택 합니다.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>FROM 절
hello `FROM <from_specification>` hello 소스 필터링 되거나 hello 쿼리의 뒷부분에 나오는 프로젝션 하지 않는 한 절은 선택 사항입니다. 이 절의 hello 목적은 toospecify hello 데이터 소스는 hello 시 쿼리 작동 해야 합니다. 일반적으로 hello 전체 컬렉션은 hello 소스 하지만 하나 hello 컬렉션의 하위 집합을 대신 지정할 수 있습니다. 

쿼리 같은 `SELECT * FROM Families` hello 전체 제품군 컬렉션 위에 있는 tooenumerate hello 소스 임을 나타냅니다. 특수 식별자 루트 hello 컬렉션 이름을 사용 하는 대신 사용 되는 toorepresent hello 컬렉션 수 있습니다. hello 다음 목록은 쿼리당 적용 하는 hello 규칙.

* hello 컬렉션 별칭을 같은 수 `SELECT f.id FROM Families AS f` 또는 단순히 `SELECT f.id FROM Families f`합니다. 여기 `f` hello 해당 `Families`합니다. `AS`선택적 키워드 tooalias hello 식별자가입니다.
* 한 번 별칭 hello 원본 소스를 바인딩할 수 없습니다. 예를 들어 `SELECT Families.id FROM Families f` hello 식별자 "제품군"는 더 이상 확인할 수 없습니다 이므로 구문상 유효 하지 않습니다.
* Toobe 참조 해야 하는 모든 속성을 정규화 되어야 합니다. 엄격한 스키마 준수 hello 없는 경우,이 적용된 tooavoid 모호한 모든 바인딩. 따라서 `SELECT id FROM Families f` hello 속성 이후 구문이 올바르지 않습니다 `id` 바인딩되어 있지 않습니다.

### <a name="subdocuments"></a>하위 문서
hello 소스 감소 tooa 작은 하위 집합을 될 수도 있습니다. 예를 들어, 각 문서에 하위 트리만 tooenumerating hello subroot 될 수 hello 소스 hello 다음 예제와 같이:

**쿼리**

    SELECT * 
    FROM Families.children

**결과**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

위 예제는 hello 배열을 hello 소스로으로 사용 되지만 개체 사용할 수도 hello 다음 예제에에서 표시 된 항목은 hello 소스로: 유효한 모든 JSON 값 (하지 정의 되지 않음) hello 원본에서 찾을 수 있는의 hello 결과에 포함 될 것으로 간주 됩니다 hello 쿼리입니다. 일부 모음에 있지 않은 경우는 `address.state` 값 hello 쿼리 결과에서 제외 됩니다.

**쿼리**

    SELECT * 
    FROM Families.address.state

**결과**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>WHERE 절
WHERE 절 hello (**`WHERE <filter_condition>`**)은 선택 사항입니다. Hello 원본에서 제공 하는 hello JSON 문서 hello 결과의 일부분으로 포함 순서 toobe에서 충족 해야 하는 hello 조건을 지정 합니다. JSON 문서 여야 hello 지정 조건 너무 "true" toobe hello 결과 대 한 것으로 간주 합니다. 순서 toodetermine hello 절대 가장 작은 하위 집합에 hello 결과의 일부가 될 수 있는 소스 문서의 hello 인덱스 레이어에서 절을 사용 하는 번호입니다. 

hello 다음 쿼리를 요청 값이 인 name 속성을 포함 하는 문서 `AndersenFamily`합니다. Name 속성을 맺지 않은 다른 문서 hello 값이 일치 하지 않으면 또는 `AndersenFamily` 제외 됩니다. 

**쿼리**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


hello 앞의 예제는 간단한 같음 쿼리를 보여 주었습니다. DocumentDB API SQL은 다양한 스칼라 식도 지원합니다. 가장 일반적으로 사용 하는 hello은 단항 및 이항 식입니다. 유효한 식 hello 원본 JSON 개체에서 속성 참조 됩니다. 

이항 연산자 뒤 hello는 현재 지원 하 고 hello 다음 예제와 같이 쿼리에서 사용할 수 있습니다:  

<table>
<tr>
<td>산술</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>비트</td>    
<td>|, &, ^, <<, >>, >>>(0 채우기 오른쪽 시프트)</td>
</tr>
<tr>
<td>논리</td>
<td>AND, OR, NOT</td>
</tr>
<tr>
<td>비교</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>문자열</td>    
<td>||(연결)</td>
</tr>
</table>  


이항 연산자를 사용한 몇 가지 쿼리를 살펴보겠습니다.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


hello 단항 연산자 +,-, ~ 에서도 지원 됩니다 하지 넣고 hello 다음 예제와 같이 쿼리를 사용할 수 있습니다.

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



또한 toobinary 및 단항 연산자 속성 참조 허용 됩니다. 예를 들어 `SELECT * FROM Families f WHERE f.isRegistered` 반환 hello hello 속성을 포함 하는 JSON 문서 `isRegistered` 된 hello 속성의 값이 같으면 toohello JSON `true` 값입니다. 다른 값 (false, null, 정의 되지 않음, `<number>`, `<string>`, `<object>`, `<array>`등) hello 결과에서 제외 되 고 toohello 소스 문서를 안내 합니다. 

### <a name="equality-and-comparison-operators"></a>같음 및 비교 연산자
hello 다음 표에 나와 같음 비교의 hello 결과 DocumentDB API SQL 임의의 JSON 형식 간의 있습니다.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Op</strong>
         </td>
         <td valign="top">
            <strong>Undefined</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>Boolean</strong>
         </td>
         <td valign="top">
            <strong>Number</strong>
         </td>
         <td valign="top">
            <strong>String</strong>
         </td>
         <td valign="top">
            <strong>Object</strong>
         </td>
         <td valign="top">
            <strong>Array</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Undefined<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Boolean<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Number<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>String<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Object<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Array<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

와 같은 다른 비교 연산자에 대 한 >, > =,! =, < 및 < =, hello 다음 규칙이 적용 됩니다.   

* 형식 비교 결과가 Undefined입니다.
* 두 개체 또는 두 배열 간 비교 결과가 Undefined입니다.   

Hello 필터에 hello 스칼라 식의 hello 결과 정의 되어 있지 hello는 해당 문서는에 포함 되지 hello 결과 이후 Undefined 너무 "true"와 동등 논리적으로 하지 않습니다.

### <a name="between-keyword"></a>BETWEEN 키워드
ANSI SQL에서와 같은 값의 범위에 대 한 hello BETWEEN 키워드 tooexpress 쿼리를 사용할 수도 있습니다. 문자열이나 숫자에 BETWEEN을 사용할 수 있습니다.

예를 들어이 쿼리는 모든 패밀리 문서는 hello 첫 번째 자식 등급이 1-5 (둘 다 포함) 사이입니다를 반환 합니다. 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

와 달리 ANSI SQL에서 사용할 수도 있습니다 hello BETWEEN 절 hello 다음 예제에서에서와 같은 hello FROM 절에 합니다.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

더 빠른 쿼리 실행 시간에 대 한 모든 숫자 속성/경로 hello BETWEEN 절에 필터링 된 범위 인덱스 유형을 사용 하는 인덱싱 정책을 toocreate를 기억 합니다. 

hello는 주요 차이점이 BETWEEN DocumentDB API 및 ANSI SQL을 사용 하 여 혼합 형식의 속성에 대 한 범위 쿼리를 표현할 수 있습니다-예를 들어 "1 등급" (5)는 숫자 여야 할 수도 있습니다 일부 문서 및 다른 사용자 ("grade4")의 문자열입니다. 이러한 경우와 같은 JavaScript에서 "undefined"에서 두 개의 서로 다른 형식 결과 hello 문서 간의 비교를 건너뜁니다.

### <a name="logical-and-or-and-not-operators"></a>논리(AND, OR 및 NOT) 연산자
논리 연산자는 부울 값에 작동합니다. 이러한 연산자에 대 한 hello 논리적 진리 테이블은 다음 표에서 hello에 표시 됩니다.

| 또는 | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Undefined |
| Undefined |True |Undefined |Undefined |

| AND | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |False |Undefined |
| False |False |False |False |
| Undefined |Undefined |False |Undefined |

| NOT |  |
| --- | --- |
| True |False |
| False |True |
| Undefined |Undefined |

### <a name="in-keyword"></a>IN 키워드
hello IN 키워드는 지정된 된 값 목록에 있는 값이 일치 하는지 여부를 사용 하는 toocheck 수 있습니다. 예를 들어이 쿼리는 hello id가 "WakefieldFamily" 또는 "AndersenFamily" 중 패밀리 문서를 모두 반환 합니다. 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

이 예에서는 모든 문서 hello 상태는 지정 된 hello의 반환 값입니다.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>3항(?) 및 병합(??) 연산자
hello 삼항과 Coalesce 연산자에 사용 되는 toobuild 조건식, 프로그래밍 언어 C# 및 JavaScript와 같은 비슷한 toopopular 수 있습니다. 

고객이 hello에 새 JSON 속성을 생성 하는 경우에 hello (?) 삼항 연산자 매우 유용할 수 있습니다. 예를 들어 이제 작성할 수 있습니다 쿼리 tooclassify hello 클래스 수준 초급/중간/고급 아래와 같이 같은 사람이 읽을 수 있는 형식으로.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

아래 hello 쿼리에서 hello 호출 toohello 연산자와 같은 중첩할 수 있습니다.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

으로 다른 쿼리 연산자와 hello hello 조건식에 참조 된 속성에서에서 누락 된 경우 모든 문서 또는 hello 형식을 비교 하 고 서로 다른 경우 다음 해당 문서 제외 됩니다 hello 쿼리 결과에 있습니다.

hello Coalesce (?) 연산자 될 수 있습니다 (규칙 하위 속성이 있는지 hello에 대 한 tooefficiently 검사 사용 효율적으로 확인할 수 있습니다. 이 연산자는 반구조적 데이터나 혼합 형식의 데이터에 대해 쿼리할 때 유용합니다. 예를 들어이 쿼리 없으면 hello "lastName" 있는 경우 또는 "surname" hello 존재 하지입니다.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>따옴표 붙은 속성 접근자
Hello 따옴표 붙은 속성 연산자를 사용 하 여 속성에 액세스할 수도 있습니다 `[]`합니다. 예를 들어 `SELECT c.grade` and `SELECT c["grade"]` 와 동일합니다. 이 구문은 tooescape SQL 키워드 또는 예약 된 단어인 이름이 tooshare hello 또는 공백, 특수 문자를 포함 하는 속성을 사용 해야 하는 경우에 유용 합니다.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>SELECT 절
hello SELECT 절 (**`SELECT <select_list>`**) 필수 이며 ANSI SQL의와 동일 하 게 hello 쿼리에서 값은 검색을 지정 합니다. hello 소스 문서를 기반으로 필터링 된 hello 하위 집합 hello JSON 값을 검색 하 고 새 JSON 개체가 생성 되 면 붙여 전달 하는 각 입력에 대해 지정 된이 있는 hello 프로젝션 단계에 전달 됩니다. 

다음 예제는 hello 일반적인 선택 쿼리를 보여 줍니다. 

**쿼리**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>중첩 속성
다음 예제는 hello, 두 개의 중첩된 속성 프로젝션은 우리 `f.address.state` 및 `f.address.city`합니다.

**쿼리**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


또한 프로젝션 hello 다음 예제와 같이 JSON 식을 지원 합니다.

**쿼리**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


hello 역할에 살펴보겠습니다 `$1` 여기 합니다. hello `SELECT` 절 toocreate JSON 개체 하며으로 시작 하는 암시적 인수가 변수 이름을 사용 하 여 없는 키를 제공 하므로 `$1`합니다. 예를 들어 이 쿼리는 `$1` 및 `$2` 레이블이 지정된 두 개의 암시적 인수 변수를 반환합니다.

**쿼리**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>별칭 지정
이제 hello 위의 예에서는 명시적 앨리어싱 사용한 값을 확장 해 보겠습니다. 마찬가지로 연결 하기 위해 사용 하는 hello 키워드입니다. 프로젝션 hello 두 번째 값으로 하는 동안 표시 된 것 처럼 선택 사항이 기는 `NameInfo`합니다. 

쿼리에서 hello 사용 하 여 두 개의 속성 경우 동일한 이름 별칭 이어야 합니다. 하나 또는 둘 다의 hello 속성을 프로젝션 하는 hello에 구분 되는 사용 되는 toorename 결과입니다.

**쿼리**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>스칼라 식
또한 tooproperty 참조, hello SELECT 절에 상수, 산술 식, 논리 식 등과 같은 스칼라 식도 지원 합니다. 예를 들어 다음은 단순한 "Hello World" 쿼리입니다.

**쿼리**

    SELECT "Hello World"

**결과**

    [{
      "$1": "Hello World"
    }]


다음은 스칼라 식을 사용하는 보다 복잡한 예제입니다.

**쿼리**

    SELECT ((2 + 11 % 7)-2)/3    

**결과**

    [{
      "$1": 1.33333
    }]


다음 예제는 hello, hello 스칼라 식의 hello 결과는 부울입니다.

**쿼리**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**결과**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>개체 및 배열 만들기
DocumentDB API SQL의 다른 주요 기능은 배열/개체 만들기입니다. Hello 이전 예제에서는 새 JSON 개체를 만들었다고 note 합니다. 마찬가지로, 다음 예제는 hello와 같이 배열을 생성할 수도 하나:

**쿼리**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**결과**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>VALUE 키워드
hello **값** 키워드 방법을 tooreturn JSON 값을 제공 합니다. 예를 들어 hello 쿼리 아래에 표시 된 반환 hello 스칼라 `"Hello World"` 대신 `{$1: "Hello World"}`합니다.

**쿼리**

    SELECT VALUE "Hello World"

**결과**

    [
      "Hello World"
    ]


hello 다음 쿼리는 반환 hello 없이 hello JSON 값 `"address"` hello 결과에 레이블.

**쿼리**

    SELECT VALUE f.address
    FROM Families f    

**결과**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

hello 다음 예에서는 확장이 tooshow 어떻게 tooreturn JSON primitive 값 (hello JSON 트리의 hello 리프 수준). 

**쿼리**

    SELECT VALUE f.address.state
    FROM Families f    

**결과**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>* 연산자
hello 특수 연산자 (*)는 지원 되는 tooproject hello 문서-됩니다. 을 사용 하는 hello만 필드를 프로젝션 이어야 합니다. `SELECT * FROM Families f`와 같은 쿼리는 유효하지만 `SELECT VALUE * FROM Families f ` 및 `SELECT *, f.id FROM Families f `와 같은 쿼리는 유효하지 않습니다.

**쿼리**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**결과**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>TOP 연산자
hello TOP 키워드 수 toolimit hello 수가 쿼리에서 값을 사용 합니다. Hello 결과 집합은 정렬 된 값의 제한 된 toohello 첫 번째 N 번호 TOP와 hello ORDER BY 절과 함께에서 사용할 경우 그렇지 않으면 정의 되지 않은 순서로 hello 결과의 첫 번째 N 수를 반환합니다. 모범 사례로, SELECT 문에서 항상는 ORDER BY 절과 함께 사용 hello TOP 절. 이 hello 유일한 방법은 toopredictably TOP의 영향을 받는 행을 나타냅니다. 

**쿼리**

    SELECT TOP 1 * 
    FROM Families f 

**결과**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

위에 나와 있는 것처럼 상수 값 또는 매개 변수가 있는 쿼리를 사용하는 변수 값과 함께 TOP를 사용할 수 있습니다. 자세한 내용은 아래의 매개 변수가 있는 쿼리를 참조하세요.

### <a id="Aggregates"></a>집계 함수
또한 hello에 대 한 집계를 수행 `SELECT` 절. 집계 함수는 값 집합에서 계산을 수행하고 단일 값을 반환합니다. 예를 들어 hello 다음 쿼리 hello의 개수를 반환 hello 컬렉션 내에서 패밀리 문서입니다.

**쿼리**

    SELECT COUNT(1) 
    FROM Families f 

**결과**

    [{
        "$1": 2
    }]

반환할 수도 있습니다 hello hello의 스칼라 값 집계 hello를 사용 하 여 `VALUE` 키워드입니다. 예를 들어 hello 다음 쿼리 hello의 개수를 반환 값을 단일 숫자로:

**쿼리**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**결과**

    [ 2 ]

필터와 함께 조합하여 집계를 수행할 수도 있습니다. 예를 들어 hello 다음 쿼리 hello에서에서 개수를 반환 hello 주소를 사용 하 여 문서의 hello 워싱턴 주의 합니다.

**쿼리**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**결과**

    [ 1 ]

hello 다음 표에 지원 되는 집계 함수 목록은 hello DocumentDB API에 있습니다. `SUM` 및 `AVG`는 숫자 값에 대해 수행되는 반면 `COUNT`, `MIN` 및 `MAX`는 숫자, 문자열, 부울 및 null에 대해 수행될 수 있습니다. 

| 사용 현황 | 설명 |
|-------|-------------|
| 개수 | 반환 hello hello 식의 항목 수입니다. |
| 합계   | 반환 hello hello 식에서 모든 hello 값의 합계입니다. |
| 최소   | 반환 hello hello 식의 최소값입니다. |
| 최대   | 반환 hello hello 식의 최대값입니다. |
| 평균   | 반환 hello hello hello 식 값의 평균입니다. |

배열 반복 hello 결과 집계를 수행할 수도 있습니다. 자세한 내용은 [쿼리에서 배열 반복](#Iteration)을 참조하세요.

> [!NOTE]
> Azure 포털의 쿼리 탐색기 hello를 사용 하 여, 집계 쿼리를 반환할 수 있습니다 부분적으로 hello 참고 쿼리 페이지를 통해 결과 집계 합니다. hello Sdk는 모든 페이지에 걸쳐 단일 누적 값을 생성합니다. 
> 
> .NET SDK 1.12.0,.NET Core SDK 1.1.0, 또는 Java SDK 1.9.5 필요한 코드를 사용 하 여 tooperform 집계 쿼리를 위해 이상.    
>

## <a id="OrderByClause"></a>ORDER BY 절
ANSI-SQL에서와 마찬가지로 쿼리하는 동안 선택적 Order By 절을 포함할 수 있습니다. hello 절은 선택적 ASC/DESC 인수 toospecify hello 순서는 결과 검색에 포함할 수 있습니다.

예를 들어 여기에 hello 상주 도시 이름 순서 대로 패밀리를 검색 하는 쿼리입니다.

**쿼리**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**결과**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

및의 순서를 나타내는 숫자 hello epoch 시간, 즉, 경과 시간 1970 년 1 월 1 일 이후 (초)에서으로 저장 된 만든 날짜, 패밀리를 검색 하는 쿼리 다음과 같습니다.

**쿼리**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**결과**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>고급 데이터베이스 개념 및 SQL 쿼리

### <a id="Iteration"></a>반복
새 구문을 hello를 통해 추가 된 **IN** JSON 배열을 반복 하는 DocumentDB API SQL tooprovide 지원의 키워드입니다. hello FROM 소스 반복에 대 한 지원을 제공합니다. 다음 예제는 hello로 시작 하겠습니다.

**쿼리**

    SELECT * 
    FROM Families.children

**결과**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

이제 hello 컬렉션에 대 한 자식 반복을 수행 하는 다른 쿼리를 살펴 보겠습니다. Note hello 차이 hello 출력 배열입니다. 이 예제에서는 분할 `children` 단일 배열로 hello 결과 평면화 하 고 있습니다.  

**쿼리**

    SELECT * 
    FROM c IN Families.children

**결과**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

이 수 추가로 hello 다음 예제와 같이 hello 배열의 각 개별 항목에 사용 되는 toofilter:

**쿼리**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**결과**  

    [{
      "givenName": "Lisa"
    }]

배열 반복 hello 결과 대해 집계를 수행할 수도 있습니다. 예를 들어 hello 다음 쿼리 수를 계산 hello 모든 패밀리 자식의 합니다.

**쿼리**

    SELECT COUNT(child) 
    FROM child IN Families.children

**결과**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>조인
관계형 데이터베이스 테이블에서 hello 필요 toojoin이 중요 합니다. hello 논리 배치한 toodesigning 정규화 된 스키마입니다. 반대 toothis, DocumentDB API 문서 스키마가 없는 hello 정규화 되지 않은 데이터 모델을 처리합니다. 이 hello 논리적으로 동일 "자체 조인을" a.

hello hello 언어를 지원 하는 구문은 < from_source1 > 조인 < from_source2 > 조인 중... JOIN <from_sourceN>입니다. 대체로 이 구문은 **N** 튜플(**N**개 값이 포함된 튜플) 집합을 반환합니다. 각 튜플은 해당 집합에 모든 컬렉션 별칭을 반복하여 생성된 값을 포함합니다. 즉,이 전체 집합의 교차곱 hello hello 조인에 참여 하는 합니다.

hello 다음 예제에서는 작동 방식을 보여 hello JOIN 절. 다음 예제는 hello, hello 결과 hello 각 문서 원본과 빈 집합의 교차곱은 비어 있으므로 비어 있습니다.

**쿼리**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**결과**  

    [{
    }]


다음 예제는 hello, hello 조인은 hello 문서 루트 사이의 hello `children` subroot 합니다. 두 JSON 개체 간의 교차곱입니다. hello 자식 배열에 있는 단일 루트를 다루는 때문에 자식 배열 임을 hello 팩트 hello 조인에에서 유효 하지 않습니다. 따라서 hello 결과 hello hello 배열이 포함 된 각 문서의 교차곱 생성 문서가 정확히 하나만 있으므로 두 개의 결과 포함 합니다.

**쿼리**

    SELECT f.id
    FROM Families f
    JOIN f.children

**결과**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


다음 예제는 hello에 더 많은 기본 조인을 보여 줍니다.

**쿼리**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**결과**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



hello 먼저 toonote는 해당 hello `from_source` 의 hello **조인** 절은 반복기입니다. 따라서 hello 흐름이 경우에 다음과 같습니다.  

* 각 자식 요소를 확장 **c** hello 배열에 있습니다.
* Hello 문서의 hello 루트를 가진 교차곱 적용 **f** 각 자식 요소가 **c** hello 첫 번째 단계에서 결합 된입니다.
* 마지막으로, 프로젝트 hello 루트 개체 **f** 속성만 이름을 지정 합니다. 

첫 번째 문서 hello (`AndersenFamily`) hello 결과 집합에는 단일 개체 해당 toothis 문서에만 포함 되므로 자식 요소가 하나만 포함 합니다. 두 번째 문서 hello (`WakefieldFamily`) 두 명의 자식이 포함 되어 있습니다. 따라서 hello 교차곱 개체를 생성 별도 각 자식 해당 toothis 문서에 대해 하나씩 두 개의 개체를 그 결과로 각 자식에 대 한 합니다. 이러한 두 문서 필드는 hello 루트 hello 교차곱에서 기대 하는 것 처럼 동일 합니다.

hello hello 조인의 실제 유틸리티이 고, 그렇지 않은 셰이프에 hello 교차곱 tooform 튜플을 어려운 tooproject 합니다. 또한 아래 hello 예제에서 보이는 것 처럼를 필터링 할 수 있는 튜플의 hello 조합 수 있는 hello overall hello 튜플에 의해 충족 하는 조건을 지정 했습니다.

**쿼리**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**결과**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



이 예제는 hello 예제에서는 앞의 기본 확장 및 이중 조인을 수행 합니다. 따라서 hello 교차곱으로 볼 수 있습니다 다음 의사 코드 hello:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily`에는 애완 동물 한 마리를 키우는 자식 한 명이 있습니다. 따라서 hello 교차곱을 생성 한 행 (1\*1\*1)이이 제품군에서. 그러나 WakefieldFamily에는 자녀 두 명이 있지만 그 중에 "Jesse"만 애완 동물을 두 마리 키우고 있습니다. 따라서 hello 교차곱 생성 1\*1\*이 제품군에서 행을 2 = 2입니다.

Hello 다음 예제에서는 필터를 추가로에 없을 `pet`합니다. 이 hello 애완 동물 이름 "그림자" 하지 않은 모든 hello 튜플을 제외 됩니다. म 수 toobuild 튜플로 배열, hello 튜플의 hello 요소에 대 한 필터를 hello 요소 조합을 프로젝트를 확인 합니다. 

**쿼리**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**결과**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>JavaScript 통합
Azure Cosmos DB 저장된 프로시저 및 트리거를 기준으로 hello 컬렉션에 직접 JavaScript 기반 응용 프로그램 논리를 실행 하기 위한 프로그래밍 모델을 제공 합니다. 이 경우 다음 두 가지 기능을 모두 사용할 수 있습니다.

* 기능 toodo 고성능 트랜잭션 CRUD 작업 및 hello 데이터베이스 엔진 내에서 직접 JavaScript 런타임 hello 긴밀 한 통합으로 인해 컬렉션의 문서에 대해 쿼리 합니다. 
* 데이터베이스 트랜잭션을 사용하여 제어 흐름, 변수 범위 지정 및 예외 처리 기본 형식의 할당과 통합을 기본적으로 모델링할 수 있습니다. JavaScript 통합에 대 한 Azure Cosmos DB 지원에 대 한 자세한 내용은 toohello JavaScript 서버 쪽 프로그래밍 기능 설명서를 참조 하십시오.

### <a id="UserDefinedFunctions"></a>UDF(사용자 정의 함수)
이 문서에 이미 정의 된 hello 형식과, 함께 DocumentDB API SQL 지원에 대 한 사용자 정의 함수 (UDF)를 제공 합니다. 특히, 스칼라 Udf는 hello 개발자 0 개 이상의 인수를 전달 하 고 단일 인수 결과 다시 반환할 수 있는 지원 됩니다. 이러한 각 인수가 유효한 JSON 값인지 확인됩니다.  

DocumentDB API SQL 구문이 hello는 이러한 사용자 정의 함수를 사용 하 여 toosupport 사용자 지정 응용 프로그램 논리를 확장 합니다. UDF를 DocumentDB API에 등록한 다음 SQL 쿼리의 일부로 참조할 수 있습니다. 사실, Udf는 exquisitely hello 설계 toobe 쿼리에 의해 호출 됩니다. 배치한 toothis 선택으로 Udf 하지 않은 액세스 toohello 컨텍스트 개체는 hello 다른 JavaScript 형식 (예: 저장된 프로시저 및 트리거)에 있어야 합니다. 쿼리는 읽기 전용으로 실행되므로 주 복제본 또는 보조 복제본에서 실행될 수 있습니다. 따라서 Udf 다른 JavaScript 종류와 달리 보조 복제본에서 설계 된 toorun 않습니다.

다음은 hello Cosmos DB 데이터베이스 문서 컬렉션에서 특히에 UDF 수 등록 하는 방법의 예입니다.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

hello 앞의 예제는 UDF를 만듭니다 이름이 `REGEX_MATCH`합니다. 두 개의 JSON 문자열 값을 허용 `input` 및 `pattern` 및 JavaScript의 string.match() 함수를 사용 하는 hello 첫 번째 일치 항목이 hello 패턴에 지정 된 두 번째 hello 되는지 확인 합니다.

이제 이 UDF를 프로젝트의 쿼리에 사용할 수 있습니다. Udf는 hello 대/소문자 구분 접두사 "udf"으로 한정 되어야 합니다. UDF를 한정해야 합니다. 

> [!NOTE]
> 이전 too3/17/2015 Cosmos DB 지원 hello "udf." 없는 UDF 호출 UDF 호출을 지원했습니다. 이 호출 패턴은 더 이상 사용되지 않습니다.  
> 
> 

**쿼리**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**결과**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

hello 아래 예에서는 또한 hello "udf."으로 정규화와 같이 hello UDF 필터 내 사용할 수도 있습니다. 있습니다.

**쿼리**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**결과**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


기본적으로 UDF는 유효한 스칼라 식이며 프로젝션과 필터 둘 다에 사용될 수 있습니다. 

tooexpand Udf의 hello 전원으로 살펴보겠습니다 또 다른 예로 조건부 논리로:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


다음은 연습 hello UDF는 예입니다.

**쿼리**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**결과**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


위의 예제 사례 hello, 대로 Udf JavaScript 언어의 hello 전원와 통합 hello DocumentDB API SQL tooprovide는 풍부한 프로그래밍 가능한 인터페이스 toodo 복잡 한 절차, 조건부 논리 사용 하 여 hello 내장된 JavaScript 런타임 기능입니다.

DocumentDB API SQL 인수를 제공 hello toohello Udf hello 소스에 있는 각 문서에 대 한 hello의 현재 단계 (WHERE 절 또는 SELECT 절) 처리 hello UDF에 있습니다. hello 결과에 통합 됩니다 전반적인 실행 파이프라인을 원활 하 게 hello 합니다. 참조 된 tooby hello UDF 매개 변수에서 사용할 수 없는 JSON 값 hello hello 매개 변수 한 것으로 간주 하는 hello 속성 정의 되지 않은 및 따라서 hello UDF 호출 전적으로 건너뜁니다. 마찬가지로 hello UDF의 hello 결과 정의 되지 않은 경우 hello 결과에 되지 포함 됩니다. 

요약 하자면, Udf는 hello 쿼리의 일부로 유용한 도구 toodo 복잡 한 비즈니스 논리를 사용 합니다.

### <a name="operator-evaluation"></a>연산자 평가
Cosmos DB JSON 데이터베이스는 hello 전문화 하 여 JavaScript 연산자와 해당 평가 의미 체계가 parallels를 그립니다. Cosmos DB JSON 지원 측면에서 toopreserve JavaScript 의미 체계를 시도 하는 동안 일부 인스턴스에서 hello 작업 평가 다르면 합니다.

DocumentDB API sql에서 달리 기존의 SQL hello 유형의 값 종종 알 수 없는 데이터베이스에서 hello 값을 검색할 때까지 합니다. 쿼리를 실행할 순서 tooefficiently에서, 대부분의 hello 연산자 엄격한 형식 요구 사항. 

DocumentDB API SQL은 JavaScript와 달리 암시적 변환을 수행하지 않습니다. 예를 들어 `SELECT * FROM Person p WHERE p.Age = 21`과 같은 쿼리는 Age 속성을 포함하고 값이 21인 문서에 일치됩니다. Age 속성이 문자열 "21" 또는 "021", "21.0", "0021", "00021" 등의 다른 무한 변형과 일치하는 다른 문서는 일치되지 않습니다. 이 hello 문자열에 값이 암시적으로 캐스팅할 toonumbers JavaScript toohello 반대로 (예: 연산자에 기반한: = =) 합니다. 이 선택 항목은 DocumentDB API SQL의 효율적인 인덱스 매핑에 중요합니다. 

## <a name="parameterized-sql-queries"></a>매개 변수가 있는 SQL 쿼리
Cosmos DB는 @ 표기법 친숙 한 hello로 표현 된 매개 변수가 있는 쿼리를 지원 합니다. 매개 변수가 있는 SQL은 사용자 입력의 강력한 처리 및 이스케이프를 제공하여 SQL 주입을 통해 데이터가 실수로 노출되는 것을 방지합니다. 

예를 들어 성 및 주소 상태를 매개 변수로 사용하는 쿼리를 작성한 다음 사용자 입력에 따라 다양한 성 및 주소 상태 값에 대해 실행할 수 있습니다.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

이 요청 보낼 수와 같은 매개 변수가 있는 JSON 쿼리로 DB tooCosmos 아래에 표시 합니다.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

hello 인수 tooTOP 설정할 수 있습니다 같은 매개 변수가 있는 쿼리를 사용 하 여 아래에 표시 합니다.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

매개 변수 값은 유효한 모든 JSON(문자열, 숫자, 부울, null, 짝수 배열 또는 중첩된 JSON)일 수 있습니다. 또한 Cosmos DB는 스키마가 없으므로 모든 형식에 대해 매개 변수의 유효성이 검사되지 않습니다.

## <a id="BuiltinFunctions"></a>기본 제공 함수
Cosmos DB는 일반적인 작업을 위해 많은 기본 제공 함수도 지원하며, UDF(사용자 정의 함수)처럼 쿼리 내에서 이러한 함수를 사용할 수 있습니다.

| 함수 그룹          | 작업                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| 수치 연산 함수  | ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN 및 TAN |
| 형식 검사 함수 | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED 및 IS_PRIMITIVE                                                           |
| 문자열 함수        | CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING 및 UPPER       |
| 배열 함수         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH 및 ARRAY_SLICE                                                                                         |
| 공간 함수       | ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID 및 ST_ISVALIDDETAILED                                                                           | 

Toobe 빠르게 toorun 등 것 처럼 hello 해당 기본 제공 함수를 사용 해야 사용자 정의 함수 (UDF) 기본 제공 함수를 지금 사용할 수 있는, 현재 사용 중인 경우 효율적으로 합니다. 

### <a name="mathematical-functions"></a>수치 연산 함수
인수로 제공 되 고 숫자 값을 반환 하는 입력된 값에 따라 계산을 수행 하는 hello 각 수치 연산 함수입니다. 다음은 지원되는 기본 제공 수치 연산 함수 표입니다.


| 사용 현황 | 설명 |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS(num_expr)](#bk_abs) | Hello 절대 (양수)의 값을 반환 hello 지정 된 숫자 식입니다. |
| [CEILING(num_expr)](#bk_ceiling) | Hello, 보다 큰 가장 작은 정수 값 또는 같음, hello 특정된 숫자 식을 반환 합니다. |
| [FLOOR(num_expr)](#bk_floor) | 작은 hello 가장 큰 정수를 반환 toohello 같거나 지정 된 숫자 식입니다. |
| [EXP(num_expr)](#bk_exp) | Hello의 반환 hello 지 수를 지정 된 숫자 식입니다. |
| [LOG(num_expr [,base])](#bk_log) | 반환 hello 자연 로그의 hello 지정한 숫자 식 또는 hello를 사용 하 여 hello 로그 지정 자료 |
| [LOG10(num_expr)](#bk_log10) | Hello 상용 로그 눈금 간격의 값을 반환 hello 지정 된 숫자 식입니다. |
| [ROUND(num_expr)](#bk_round) | 숫자 값을 반올림된 toohello 가장 가까운 정수 값을 반환합니다. |
| [TRUNC(num_expr)](#bk_trunc) | 숫자 값, 잘린된 toohello 가장 가까운 정수 값을 반환합니다. |
| [SQRT(num_expr)](#bk_sqrt) | Hello의 반환 hello 제곱근을 지정 된 숫자 식입니다. |
| [SQUARE(num_expr)](#bk_square) | 반환 hello hello의 제곱를 지정 된 숫자 식입니다. |
| [POWER(num_expr, num_expr)](#bk_power) | 반환 hello 전원 hello의 지정 된 숫자 식 toohello 값 지정 합니다. |
| [SIGN(num_expr)](#bk_sign) | Hello 반환 hello 기호 값 (-1, 0, 1)이 숫자 식을 지정 합니다. |
| [ACOS(num_expr)](#bk_acos) | 반환 hello 각도 라디안 코사인이 hello 지정 된 숫자 식입니다. 아크코사인이 라고도합니다. |
| [ASIN(num_expr)](#bk_asin) | 사인이 hello 라디안 단위로 반환 hello 각도 숫자 식 지정. 아크사인이라고도 합니다. |
| [ATAN(num_expr)](#bk_atan) | 반환 hello 각도 라디안의 탄젠트는 hello 지정 된 숫자 식입니다. 아크탄젠트라고도 합니다. |
| [ATN2(num_expr)](#bk_atn2) | 반환 hello hello 양의 x 축 (y, x) hello 시작 toohello 지점부터 hello 광선 사이의 라디안 단위의 각도, 여기서 x와 y는 hello의 hello 값 지정한 두 float 식입니다. |
| [COS(num_expr)](#bk_cos) | 반환 hello hello의 삼각 코사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다. |
| [COT(num_expr)](#bk_cot) | 반환 hello hello의 삼각 코탄젠트 각도 라디안에서으로 지정 된, hello에 지정 된 숫자 식입니다. |
| [DEGREES(num_expr)](#bk_degrees) | 반환 hello 해당 각도에서 라디안에서으로 지정 된 각도의 단위입니다. |
| [PI()](#bk_pi) | 반환 hello PI의 상수 값입니다. |
| [RADIANS(num_expr)](#bk_radians) | 숫자 식을 단위로 입력하면 라디안을 반환합니다. |
| [SIN(num_expr)](#bk_sin) | 반환 hello hello의 삼각 사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다. |
| [TAN(num_expr)](#bk_tan) | Hello에 hello 입력된 식의 반환 hello 탄젠트 값을 지정 된 식입니다. |

예를 들어 hello 다음과 같은 쿼리 실행할 수 있습니다.

**쿼리**

    SELECT VALUE ABS(-4)

**결과**

    [4]

Cosmos DB 비교 함수 tooANSI SQL 간의 주요 차이점 hello는 스키마 없음 및 혼합 스키마 데이터와 잘 설계 된 toowork 이들이 합니다. 예를 들어 여기서 hello 크기 속성이 없거나에 문서가 있는 경우 숫자가 아닌 값에 "알 수 없음"와 같은 다음 오류를 반환 하는 대신, hello 문서를 건너뜁니다.

### <a name="type-checking-functions"></a>형식 검사 함수
hello 형식 검사 함수는 toocheck hello 유형의 SQL 쿼리 내에서 식 허용 합니다. 형식 검사 함수 수 변수 또는 알 수 없는 경우 hello 신속 하 게 toodetermine hello 유형의 문서 내에서 속성을 사용 합니다. 다음은 지원되는 기본 제공 형식 검사 함수 표입니다.

<table>
<tr>
  <td><strong>사용 현황</strong></td>
  <td><strong>설명</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Hello 유형의 hello 값 배열 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Hello 값의 hello 형식이 부울 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Hello 유형의 hello 값이 null 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Hello 유형의 hello 값이 숫자 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Hello 유형의 hello 값은 JSON 개체 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Hello 유형의 hello 값 문자열 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>경우 hello 속성 값이 할당에 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Hello 유형의 hello 값 문자열, 숫자, 부울 또는 null 인지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>

</table>

이러한 함수를 사용 하 여 hello 다음과 같은 쿼리를 실행할 수 있습니다.

**쿼리**

    SELECT VALUE IS_NUMBER(-4)

**결과**

    [true]

### <a name="string-functions"></a>문자열 함수
hello 다음 스칼라 함수는 문자열 입력된 값에 대 한 작업을 수행 하 고 문자열, 숫자 또는 부울 값을 반환 합니다. 기본 제공 문자열 함수의 테이블은 다음과 같습니다.

| 사용 현황 | 설명 |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |지정 된 문자열 식의 hello 문자의 hello 수를 반환 합니다. |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |않은 hello 두 개 이상의 문자열 값을 연결한 결과인 문자열을 반환 합니다. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |문자열 식의 일부를 반환합니다. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다. |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다. |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |첫 번째 문자열 식 hello hello를 두 번째로 포함 되는지 여부를 나타내는 부울 값을 반환 합니다. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Hello hello 문자열을 찾을 수 없는 경우 시작 hello hello hello 첫 번째 지정 된 문자열 식 또는-1 내에서 두 번째 문자열 식의 첫 번째 발생 위치를 반환 합니다. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |반환 문자열의 왼쪽된 부분을 지정 하는 hello로 hello 문자 수입니다. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Hello로 반환 hello 오른쪽 부분 문자열의 문자 수를 지정 합니다. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |선행 공백을 제거한 후에 문자열 식을 반환합니다. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |후행 공백을 잘라낸 후에 문자열 식을 반환합니다. |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |대문자 데이터 toolowercase 변환한 후 문자열 식을 반환 합니다. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |소문자 데이터 toouppercase 변환한 후 문자열 식을 반환 합니다. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |문자열 값을 지정한 횟수 만큼 반복합니다. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Hello는 문자열 값의 역순을 반환합니다. |

이러한 함수를 사용 하 여 hello 다음과 같은 쿼리를 실행할 수 있습니다. 예를 들어 다음과 같이 대문자로 hello 제품군 이름을 반환할 수 있습니다.

**쿼리**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**결과**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

또는 이 예제와 같이 문자열을 연결합니다.

**쿼리**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**결과**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


문자열 함수 사용할 수도 있습니다 hello에 절 toofilter 결과 hello 다음 예제에서에서와 같이 하는 위치:

**쿼리**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**결과**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>배열 함수
다음 스칼라 함수 hello는 배열 입력된 값 및 반환 숫자, 부울 또는 배열 값에 대 한 작업을 수행 합니다. 기본 제공 배열 함수의 테이블은 다음과 같습니다.

| 사용 현황 | 설명 |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |배열 식을 지정 하는 hello 요소의 hello 수를 반환 합니다. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |hello가 두 개 이상의 배열 값을 연결한 결과인 배열을 반환 합니다. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |값을 지정 하는 hello hello 배열에 포함 되는지 여부를 나타내는 부울 값을 반환 합니다. 전체 또는 일부 경우 hello 일치는 지정할 수 있습니다. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |배열 식의 일부를 반환합니다. |

배열 함수에는 JSON 내에서 사용 되는 toomanipulate 배열 형식일 수 있습니다. 예를 들어 여기에 "로빈 Wakefield" hello 부모 항목 중 하나가 모든 문서를 반환 하는 쿼리입니다. 

**쿼리**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**결과**

    [{
      "id": "WakefieldFamily"
    }]

Hello 배열 내에서 일치 하는 요소에 대 한 부분 일부분을 지정할 수 있습니다. hello 다음 쿼리에서 찾습니다 hello로 모든 부모 `givenName` 의 `Robin`합니다.

**쿼리**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**결과**

    [{
      "id": "WakefieldFamily"
    }]


패밀리당 자녀 수가 tooget hello ARRAY_LENGTH를 사용 하는 또 다른 예는 다음과 같습니다.

**쿼리**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**결과**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>공간 함수
Cosmos DB hello Open Geospatial Consortium (OGC) 기본 제공 함수를 쿼리 하는 지리 공간에 대 한 다음을 지원 합니다. 

<table>
<tr>
  <td><strong>사용 현황</strong></td>
  <td><strong>설명</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>두 hello GeoJSON 지점, 다각형 또는 LineString 식 사이의 hello 거리를 반환합니다.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Hello 첫 번째 GeoJSON 개체 (점, 다각형, 또는 LineString) hello 두 번째 GeoJSON 개체 (점, 다각형, 또는 LineString) 이내 인지 여부를 나타내는 부울 식을 반환 합니다.</td>
</tr>
<tr>
  <td>ST_INTERSECTS(spatial_expr, spatial_expr)</td>
  <td>Hello 지정 된 두 GeoJSON 개체 (점, 다각형, 또는 LineString) 교차 하는지 여부를 나타내는 부울 식을 반환 합니다.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Hello GeoJSON 지점, 다각형 또는 LineString 식이 유효한 경우이 지정 되었는지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Hello GeoJSON 지점, 다각형 또는 LineString 식이 지정 된 경우 부울 값을 포함 하는 JSON 값은 유효 하 고, 잘못 된 경우에 문자열 값으로 이유 hello 또한 반환 합니다.</td>
</tr>
</table>

공간 함수에는 공간 데이터에 대 한 사용된 tooperform 근접 쿼리 수 있습니다. 예를 들어 여기에 모든 제품군에 설명 하의 hello 30 km 내에서 지정 된 위치 사용 하는 hello ST_DISTANCE 기본 제공 함수를 반환 하는 쿼리입니다. 

**쿼리**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**결과**

    [{
      "id": "WakefieldFamily"
    }]

Cosmos DB의 지리 공간 지원에 대한 자세한 내용은 [Azure Cosmos DB에서 지리 공간 데이터 작업](geospatial.md)을 참조하세요. Cosmos DB에 대 한 SQL 구문 hello 및 공간 함수를 래핑합니다. 이제 어떻게 작동 hello 구문을 사용 하 여 상호 작용 하는 방법 및 쿼리 LINQ 살펴본 지금까지에 대해 살펴보겠습니다.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ는 개체 스트림에 대한 쿼리로 계산을 표현하는 .NET 프로그래밍 모델입니다. Cosmos DB JSON 및.NET 개체 사이의 변환은 촉진 하 여 LINQ 통한 클라이언트 쪽 라이브러리 toointerface를 제공 하 고 LINQ의 하위 집합에서의 매핑 tooCosmos DB 쿼리를 쿼리 합니다. 

아래 hello 그림 Cosmos DB를 사용 하 여 LINQ 쿼리를 지 원하는 hello 아키텍처를 보여 줍니다.  Cosmos DB 클라이언트 hello를 사용 하 여 개발자가 만들 수는 **IQueryable** 개체 쿼리 hello Cosmos DB 쿼리 공급자, 직접 그러면 Cosmos DB 쿼리로 hello LINQ 쿼리를 변환 합니다. hello 쿼리 toohello Cosmos DB 서버 tooretrieve 결과 집합을 JSON 형식으로 전달 됩니다. hello 스트림으로 hello 클라이언트 쪽에서.NET 개체의 역직렬화 된 결과 반환 합니다.

![DocumentDB API를 사용한 LINQ 쿼리를 지원하는 아키텍처 - SQL 구문, JSON 쿼리 언어, 데이터베이스 개념 및 SQL 쿼리][1]

### <a name="net-and-json-mapping"></a>.NET 및 JSON 매핑
.NET 개체와 JSON 문서 간의 hello 매핑은 자연-각 데이터 멤버 필드 매핑된 tooa JSON 개체, 여기서는 hello 필드 이름이 hello 개체의 "키" 일부 toohello 매핑되고 hello "value" 부분은 hello 개체의 매핑된 재귀적으로 toohello 값 부분입니다. 다음 예제는 hello는 것이 좋습니다: 아래 표시 된 대로 만든 hello 제품군 개체는 매핑된 toohello JSON 문서입니다. 및 그 반대로 hello JSON 문서는 매핑된 백 tooa.NET 개체입니다.

**C# 클래스**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>LINQ tooSQL 변환
LINQ 쿼리에서 최상의 노력 매핑 Cosmos DB SQL 쿼리를 수행 하는 hello Cosmos DB 쿼리 공급자 합니다. Hello 설명 뒤, hello 판독기에 LINQ에 대 한 기본 지식이 가정 합니다.

첫째, hello 형식 시스템에 대 한 모든 JSON 기본 형식 – 숫자 형식, 부울, 문자열 및 null 지원합니다. 이러한 JSON 형식만 지원됩니다. 스칼라 식은 다음 hello 지원 됩니다.

* 상수 값-hello 쿼리가 평가 되는 hello 시 hello 기본 데이터 형식의 상수 값이 포함 됩니다.
* 속성/배열 인덱스 식 – 이러한 식 toohello 속성을 개체 또는 배열 요소를 참조 하십시오.
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable
* 산술 식 - 숫자 및 부울 값에 대한 일반 산술 식을 포함합니다. Hello 전체 목록을 보려면 toohello SQL specification을 참조 하십시오.
  
     2 * family.children[0].grade;    x + y;
* 문자열 비교 식-여기에 문자열 값 toosome 상수 문자열 값을 비교 합니다.  
  
     mother.familyName == "Smith";    child.givenName == s; //s is a string variable
* 개체/배열 만들기 식 - 복합 값 형식 또는 무명 형식의 개체나 이러한 개체의 배열을 반환합니다. 해당 값을 중첩할 수 있습니다.
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields              
     new int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>지원되는 LINQ 연산자 목록
다음은 hello DocumentDB.NET SDK에 포함 된 hello LINQ 공급자에서 지원 되는 LINQ 연산자의 목록입니다.

* **선택**: 프로젝션 toohello SQL 개체 생성을 포함 하 여 선택 변환
* **여기서**: 필터 toohello SQL WHERE 및 간의 변환을 지원 & &, | | 및! toohello SQL 연산자
* **SelectMany**: 배열 toohello SQL JOIN 절을 해제할 수 있습니다. 배열 요소에 대해 사용 되는 toochain/중첩 식은 toofilter 수 있습니다.
* **OrderBy 및 OrderByDescending**: tooORDER BY 오름차순/내림차순으로 변환
* 집계를 위한 **Count**, **Sum**, **Min**, **Max** 및 **Average** 연산자와 해당 비동기 동급 연산자 **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** 및 **AverageAsync**
* **CompareTo**: toorange 비교로 변환 합니다. .NET에서 비교 불가능하므로 문자열에 대해 일반적으로 사용됩니다.
* **라인**: toohello SQL TOP 쿼리 결과 제한 하기 위한 변환
* **수치 연산 함수**:에서 변환만 지원 합니다. NET의 Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, 로그, Log10, Pow, 라운드, Sign, Sin, Sqrt, Tan, toohello 동등한 SQL 기본 제공 함수를 자릅니다.
* **문자열 함수**:에서 변환만 지원 합니다. NET의 Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, 역방향, TrimEnd, StartsWith, SubString, ToUpper toohello 동등한 SQL 기본 제공 함수입니다.
* **배열 함수**:에서 변환만 지원 합니다. NET의 Concat, Contains 및 Count toohello 동등한 SQL 기본 제공 함수입니다.
* **지리 공간 확장 함수**: IsValid, 내에서 거리 스텁 메서드에서 변환만 지원 및 IsValidDetailed toohello 동등한 SQL 기본 제공 함수입니다.
* **사용자 정의 함수 확장 함수**: hello에서 지 원하는 변환 스텁 메서드 UserDefinedFunctionProvider.Invoke toohello 해당 사용자 정의 함수입니다.
* **기타**: hello의 번역 coalesce 지원 하 고 조건부 연산자입니다. Contains tooString를 가져올 수 있습니다. CONTAINS, ARRAY_CONTAINS, 또는 컨텍스트에 따라 SQL hello 합니다.

### <a name="sql-query-operators"></a>SQL 쿼리 연산자
다음은 일부 hello LINQ 표준 쿼리 연산자 변환 되는 방법을 tooCosmos DB 쿼리를 보여 주는 몇 가지 예입니다.

#### <a name="select-operator"></a>Select 연산자
hello 구문은 `input.Select(x => f(x))`여기서 `f` 스칼라 식입니다.

**LINQ 람다 식**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**LINQ 람다 식**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**LINQ 람다 식**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>SelectMany 연산자
hello 구문은 `input.SelectMany(x => f(x))`여기서 `f` 컬렉션 형식을 반환 하는 스칼라 식입니다.

**LINQ 람다 식**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Where 연산자
hello 구문은 `input.Where(x => f(x))`여기서 `f` 부울 값을 반환 하는 스칼라 식입니다.

**LINQ 람다 식**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**LINQ 람다 식**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>복합 SQL 쿼리
hello 연산자 위에 구성 된 tooform 더 강력한 쿼리가 될 수 있습니다. Cosmos DB 중첩된 컬렉션을 지 원하는 이후 hello 컴퍼지션 수 연결 하거나 중첩 합니다.

#### <a name="concatenation"></a>연결
hello 구문은 `input(.|.SelectMany())(.Select()|.Where())*`합니다. 연결된 쿼리는 선택적 `SelectMany` 쿼리로 시작하며 그 뒤에 여러 `Select` 또는 `Where` 연산자가 올 수 있습니다.

**LINQ 람다 식**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**LINQ 람다 식**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**LINQ 람다 식**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**LINQ 람다 식**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>중첩
hello 구문은 `input.SelectMany(x=>x.Q())` 여기서 Q는는 `Select`, `SelectMany`, 또는 `Where` 연산자입니다.

중첩 쿼리에서 hello 내부 쿼리에 적용 된 tooeach 요소 hello 외부 컬렉션입니다. 중요 한 기능은 hello 내부 쿼리 하는 hello와 같은 외부 컬렉션에 있는 hello 요소의 toohello 필드를 참조할 수 있습니다 하나 자체 조인 합니다.

**LINQ 람다 식**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**LINQ 람다 식**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**LINQ 람다 식**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>SQL 쿼리 실행
Cosmos DB는 HTTP/HTTPS 요청을 수행할 수 있는 임의의 언어로 호출할 수 있는 REST API를 통해 리소스를 노출합니다. 또한 Cosmos DB는 .NET, Node.js, JavaScript, Python 등 많이 사용되는 여러 언어를 위한 프로그래밍 라이브러리를 제공합니다. hello REST API 및 hello 모든 다양 한 라이브러리를 통해 SQL 쿼리를 지원 합니다. .NET SDK hello LINQ tooSQL 또한 쿼리를 지원 합니다.

예제에서는 보여 방법을 다음 hello toocreate 쿼리 및 Cosmos DB 데이터베이스 계정에 대해 제출 합니다.

### <a id="RestAPI"></a>REST API
Cosmos DB는 HTTP를 통해 개방형 RESTful 프로그래밍 모델을 제공합니다. Azure 구독을 사용하여 데이터베이스 계정을 프로비전할 수 있습니다. hello Cosmos DB 리소스 모델 되는 논리적이 고 안정적인 URI를 사용 하 여에 접근할 수 있으며 각 데이터베이스 계정 내 리소스의 집합으로 구성 됩니다. 리소스 집합은 참조 tooas이이 문서에 피드. 데이터베이스 계정은 각각 여러 컬렉션을 포함하는 데이터베이스 집합으로 구성되고, 각 컬렉션에는 문서, UDF 및 기타 리소스 유형이 포함됩니다.

hello 기본 상호 작용 모델 이러한 리소스와은 hello HTTP 동사를 통해 GET, PUT, POST 및 DELETE의 표준 해석을 사용 합니다. 새 리소스를 만들기 위한, 저장된 프로시저 실행을 위한 또는 Cosmos DB 쿼리 실행에 대 한 hello POST 동사가 사용 됩니다. 쿼리는 항상 파생 작업이 없는 읽기 전용 작업입니다.

hello 다음 예제에서는 지금까지 검토 했으므로 hello 두 예제 문서를 포함 하는 컬렉션에 대 한 DocumentDB API 쿼리에 대 한 POST hello 쿼리는 간단한 필터를 hello JSON name 속성에 증가 시킵니다. Hello hello 사용 `x-ms-documentdb-isquery` 및 콘텐츠-유형: `application/query+json` 작업 hello 헤더 toodenote는 쿼리입니다.

**요청**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**결과**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


두 번째 예에서는 hello hello 조인에서 여러 결과 반환 하는 보다 복잡 한 쿼리를 보여 줍니다.

**요청**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**결과**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


쿼리 결과의 결과 단일 페이지에 들어갈 수 없는 경우 hello REST API를 통해 hello 연속 토큰도 반환 `x-ms-continuation-token` 응답 헤더입니다. 클라이언트는 후속 결과에 hello 헤더를 포함 하 여 결과 페이지를 매기 수 있습니다. hello를 통해 hello 페이지당 결과 수를 제어할 수도 있습니다 `x-ms-max-item-count` 번호 헤더입니다. 지정 된 쿼리에 hello와 같은 집계 함수 있으면 `COUNT`, hello 쿼리 페이지 hello 결과 페이지를 통해 부분적으로 집계 된 값을 반환 합니다. hello 클라이언트는 이러한 결과 tooproduce hello 최종 결과, 예를 들어 두 번째 수준의 집계를 수행 해야, hello 개수 hello 개별 페이지 tooreturn hello 총 개수에 반환 된 합계입니다.

쿼리를 사용 하 여 hello에 대 한 toomanage hello 데이터 일관성 정책을 `x-ms-consistency-level` 같은 REST API에 대 한 모든 요청 헤더입니다. 세션 일관성을 위해 그는 필요한 tooalso 에코 hello 최신 `x-ms-session-token` hello 쿼리 요청에 쿠키 헤더입니다. hello 쿼리 된 컬렉션의 인덱싱 정책을 영향을 줄 수 쿼리 결과의 hello 일관성. Hello 기본 인덱싱 정책 설정, 사용 하 여 컬렉션에 대 한 hello 인덱스는 항상 최신 hello 문서 목차, 쿼리 결과 데이터에 대해 선택한 hello 일관성 일치 합니다. 인덱싱 정책을 hello 상대적으로 느 tooLazy 이면 쿼리는 유효 하지 않은 결과 반환할 수 있습니다. 자세한 내용은 [Azure Cosmos DB 일관성 수준][consistency-levels]을 참조하세요.

Hello 컬렉션에 인덱싱 정책을 구성 하는 hello hello 지정 된 쿼리를 지원 하지 않는 경우 400 "잘못 된 요청" hello Azure Cosmos DB 서버에 반환 합니다. 해시(같음) 조회에 구성된 경로 및 인덱싱에서 명시적으로 제외된 경로의 범위 쿼리에 대해 반환됩니다. hello `x-ms-documentdb-query-enable-scan` 헤더 인덱스를 사용할 수 없는 경우 지정 된 tooallow hello 쿼리 tooperform 검색 될 수 있습니다.

설정 하 여 쿼리 실행에 자세한 메트릭을 가져올 수 `x-ms-documentdb-populatequerymetrics` 헤더 너무`True`합니다. 자세한 내용은 [Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리 메트릭](documentdb-sql-query-metrics.md)을 참조하세요.

### <a id="DotNetSdk"></a>C#(.NET) SDK
LINQ와 SQL 모두 hello.NET SDK 지원 쿼리 합니다. hello 다음 예제에서는이 문서의 앞부분에서 tooperform hello 간단한 필터 쿼리 도입 하는 방법

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


이 샘플은 각 문서 내에서 두 속성이 같은지 비교하고 익명 프로젝션을 사용합니다. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


hello 다음 샘플에서는 LINQ SelectMany 통해 명시 된 조인 보여 줍니다.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



.NET 클라이언트 hello 위와 같이 hello foreach 블록의 쿼리 결과의 모든 hello 페이지를 자동으로 반복 합니다. hello REST API 섹션에에서 추가 된 옵션에 사용할 수도 있습니다. hello 쿼리 hello hello를 사용 하 여.NET SDK `FeedOptions` 및 `FeedResponse` hello CreateDocumentQuery 메서드의에서 클래스. hello를 사용 하 여 hello 페이지 수를 제어할 수 있습니다 `MaxItemCount` 설정 합니다. 

만들어 페이징을 명시적으로 제어할 수 있습니다 `IDocumentQueryable` hello를 사용 하 여 `IQueryable` 참조 하 여 다음 개체는` ResponseContinuationToken` 값 전달 하는 것으로 다시 `RequestContinuationToken` 에서 `FeedOptions`합니다. `EnableScanInQuery`인덱싱 정책을 구성 하는 hello에서 hello 쿼리를 지원할 수 없는 경우에 집합 tooenable 검색이 될 수 있습니다. 분할 된 컬렉션에 대 한 사용할 수 있습니다 `PartitionKey` toorun hello 쿼리는 단일에 대해 (하지만 Cosmos DB을 자동으로 추출이 hello 쿼리 텍스트에서)를 분할 하 고 `EnableCrossPartitionQuery` toobe 필요할 수 있는 toorun 쿼리를 여러 파티션에 대해 실행 합니다. 

너무 참조[Azure Cosmos DB.NET 샘플](https://github.com/Azure/azure-documentdb-net) 쿼리를 포함 하는 추가 예제입니다. 

### <a id="JavaScriptServerSideApi"></a>JavaScript 서버 쪽 API
Cosmos DB 저장된 프로시저 및 트리거를 사용 하 여 hello 컬렉션에 직접 JavaScript 기반 응용 프로그램 논리를 실행 하기 위한 프로그래밍 모델을 제공 합니다. 컬렉션 수준에서 등록 하는 hello JavaScript 논리 데이터베이스 작업의 컬렉션을 제공 하는 hello hello 문서에 대 한 hello 작업에 발급할 수 있습니다. 해당 작업은 앰비언트 ACID 트랜잭션에 래핑됩니다.

hello 다음 예제에서는 JavaScript 서버 API hello toomake에서 toouse hello queryDocuments에서 쿼리 하는 방법을 내부 저장 프로시저와 트리거의 합니다.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>참조
1. [소개 tooAzure Cosmos DB][introduction]
2. [Azure Cosmos DB SQL 사양](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Azure Cosmos DB .NET 샘플](https://github.com/Azure/azure-documentdb-net)
4. [Azure Cosmos DB 일관성 수준][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Javascript 사양 [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. 대형 데이터베이스에 대한 쿼리 평가 기술 [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994
11. Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.
13. G. Graefe. 쿼리 최적화에 대 한 hello 단계적 프레임 워크입니다. IEEE 데이터 Eng. Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md