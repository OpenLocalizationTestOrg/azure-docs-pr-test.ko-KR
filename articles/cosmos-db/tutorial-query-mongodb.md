---
title: "어떻게 azure Cosmos DB: DocumentDB API hello tooquery를 사용 하 여? | Microsoft Docs"
description: "Cosmos DB Azure 용 hello DocumentDB API로 tooquery에 알아보기"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure Cosmos DB: 어떻게 MongoDB에 대 한 API와 tooquery?

hello Azure Cosmos DB [MongoDB에 대 한 API](mongodb-introduction.md) 지원 [MongoDB 셸 쿼리](https://docs.mongodb.com/manual/tutorial/query-documents/)합니다. 

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * MongoDB를 사용한 데이터 쿼리

## <a name="sample-document"></a>샘플 문서

이 문서의 hello 쿼리 샘플 문서 다음 hello를 사용 합니다.

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
## <a id="examplequery1"></a>예제 쿼리 1 

Hello 샘플 패밀리 문서 위의 들어 hello 다음 쿼리 hello id 필드와 일치 하는 hello 문서가 반환 `WakefieldFamily`합니다.

**쿼리**
    
    db.families.find({ id: “WakefieldFamily”})

**결과**

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
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
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <a id="examplequery2"></a>예제 쿼리 2 

다음 쿼리 hello hello 제품군의 hello 자식을 반환합니다. 

**쿼리**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**결과**

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
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
    ]
    }


## <a id="examplequery3"></a>예제 쿼리 3 

hello 다음 쿼리는 등록 된 모든 hello 패밀리를 반환 합니다. 

**쿼리**
    
    db.families.find( { "isRegistered" : true })
**결과** 문서가 반환 됩니다. 

## <a id="examplequery4"></a>예제 쿼리 4

hello 다음 쿼리는 등록 되지 않은 모든 hello 패밀리를 반환 합니다. 

**쿼리**
    
    db.families.find( { "isRegistered" : false })
**결과**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}

## <a id="examplequery5"></a>예제 쿼리 5

hello 다음 쿼리는 모든 등록 된 hello 제품군 및 상태는 NY 반환 합니다. 

**쿼리**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**결과**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}


## <a id="examplequery6"></a>예제 쿼리 6

hello 다음 쿼리 자식 등급 8에 있는 모든 hello 패밀리를 반환 합니다.

**쿼리**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**결과**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}

## <a id="examplequery7"></a>예제 쿼리 7

hello 다음 쿼리의 자식 배열 크기는 3 모든 hello 패밀리를 반환 합니다.

**쿼리**
  
      db.Family.find( {children: { $size:3} } )

**결과**

2명 이상의 자식이 있는 가족이 없기 때문에 결과가 반환되지 않습니다. 매개 변수 2는 경우에이 쿼리는 성공 하 고 hello 전체 문서를 반환 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * 방법에 대해 배웠습니다 tooquery MongoDB를 사용 하 여 

이제 진행할 수 있습니다 다음 자습서 toolearn toohello 어떻게 toodistribute 데이터 전체적으로 합니다.

> [!div class="nextstepaction"]
> [전 세계로 데이터 배포](tutorial-global-distribution-documentdb.md)

