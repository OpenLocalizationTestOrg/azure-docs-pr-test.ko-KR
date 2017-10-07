---
title: "Cosmos DB Azure에서에서 SQL로 aaaHow tooquery? | Microsoft Docs"
description: "Sql Azure Cosmos DB에서 DocumentDB 데이터로 tooquery에 알아봅니다"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB: 어떻게 SQL을 사용 하 여 tooquery?

hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) 지원 SQL을 사용 하 여 문서를 쿼리 합니다. 이 문서에서는 샘플 문서 및 두 가지 샘플 SQL 쿼리와 결과를 제공합니다.

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * SQL을 사용한 데이터 쿼리

## <a name="sample-document"></a>샘플 문서

이 문서의 hello SQL 쿼리는 다음 샘플 문서 hello를 사용 합니다.

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
## <a name="where-can-i-run-sql-queries"></a>SQL 쿼리를 실행할 수 있는 위치

Hello hello 통해 Azure 포털에에서 있는 데이터 탐색기 hello를 사용 하 여 쿼리를 실행할 수 있습니다 [REST API와 Sdk](documentdb-sdk-dotnet.md), 및에 hello [Query playground](https://www.documentdb.com/sql/demo), 기존 샘플 데이터 집합에서 쿼리를 실행 합니다.

SQL 쿼리에 대한 자세한 내용은 다음을 참조하세요.
* [SQL 쿼리 및 SQL 구문](documentdb-sql-query.md)

## <a name="prerequisites"></a>필수 조건

이 자습서에서는 Azure Cosmos DB 계정과 컬렉션이 있다고 가정합니다. 이들 중 하나라도 없는가요? 전체 hello [5 분 퀵 스타트](create-mongodb-nodejs.md) 또는 hello [개발자 자습서](tutorial-develop-mongodb.md) toocreate 계정과 컬렉션입니다.

## <a name="example-query-1"></a>예제 쿼리 1

매개 변수로 받아 hello 샘플 패밀리 문서 위의 다음 SQL 쿼리에서 반환 hello 문서 hello id 필드와 일치 하는 `WakefieldFamily`합니다. 이기 때문에 `SELECT *` 문, hello 쿼리의 hello 출력은 JSON 문서를 완료 하는 hello:

**쿼리**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**결과**

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

## <a name="example-query-2"></a>예제 쿼리 2

hello 다음 쿼리 id와 일치 하는 hello 제품군의 자식 항목의 모든 hello 지정 된 이름을 반환 `WakefieldFamily` 해당 등급으로 정렬 합니다.

**쿼리**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**결과**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * 방법에 대해 배웠습니다 tooquery SQL을 사용 하 여  

이제 진행할 수 있습니다 다음 자습서 toolearn toohello 어떻게 toodistribute 데이터 전체적으로 합니다.

> [!div class="nextstepaction"]
> [전 세계로 데이터 배포](tutorial-global-distribution-documentdb.md)

