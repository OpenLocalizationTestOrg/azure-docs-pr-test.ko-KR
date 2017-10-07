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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="6940b-104">Azure Cosmos DB: 어떻게 MongoDB에 대 한 API와 tooquery?</span><span class="sxs-lookup"><span data-stu-id="6940b-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="6940b-105">hello Azure Cosmos DB [MongoDB에 대 한 API](mongodb-introduction.md) 지원 [MongoDB 셸 쿼리](https://docs.mongodb.com/manual/tutorial/query-documents/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="6940b-106">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6940b-107">MongoDB를 사용한 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="6940b-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="6940b-108">샘플 문서</span><span class="sxs-lookup"><span data-stu-id="6940b-108">Sample document</span></span>

<span data-ttu-id="6940b-109">이 문서의 hello 쿼리 샘플 문서 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="6940b-110"><a id="examplequery1"></a>예제 쿼리 1</span><span class="sxs-lookup"><span data-stu-id="6940b-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="6940b-111">Hello 샘플 패밀리 문서 위의 들어 hello 다음 쿼리 hello id 필드와 일치 하는 hello 문서가 반환 `WakefieldFamily`합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="6940b-112">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="6940b-113">**결과**</span><span class="sxs-lookup"><span data-stu-id="6940b-113">**Results**</span></span>

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

## <span data-ttu-id="6940b-114"><a id="examplequery2"></a>예제 쿼리 2</span><span class="sxs-lookup"><span data-stu-id="6940b-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="6940b-115">다음 쿼리 hello hello 제품군의 hello 자식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="6940b-116">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="6940b-117">**결과**</span><span class="sxs-lookup"><span data-stu-id="6940b-117">**Results**</span></span>

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


## <span data-ttu-id="6940b-118"><a id="examplequery3"></a>예제 쿼리 3</span><span class="sxs-lookup"><span data-stu-id="6940b-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="6940b-119">hello 다음 쿼리는 등록 된 모든 hello 패밀리를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="6940b-120">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="6940b-121">**결과** 문서가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="6940b-122"><a id="examplequery4"></a>예제 쿼리 4</span><span class="sxs-lookup"><span data-stu-id="6940b-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="6940b-123">hello 다음 쿼리는 등록 되지 않은 모든 hello 패밀리를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="6940b-124">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="6940b-125">**결과**</span><span class="sxs-lookup"><span data-stu-id="6940b-125">**Results**</span></span>

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
<span data-ttu-id="6940b-126">}</span><span class="sxs-lookup"><span data-stu-id="6940b-126">}</span></span>

## <span data-ttu-id="6940b-127"><a id="examplequery5"></a>예제 쿼리 5</span><span class="sxs-lookup"><span data-stu-id="6940b-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="6940b-128">hello 다음 쿼리는 모든 등록 된 hello 제품군 및 상태는 NY 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="6940b-129">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="6940b-130">**결과**</span><span class="sxs-lookup"><span data-stu-id="6940b-130">**Results**</span></span>

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
<span data-ttu-id="6940b-131">}</span><span class="sxs-lookup"><span data-stu-id="6940b-131">}</span></span>


## <span data-ttu-id="6940b-132"><a id="examplequery6"></a>예제 쿼리 6</span><span class="sxs-lookup"><span data-stu-id="6940b-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="6940b-133">hello 다음 쿼리 자식 등급 8에 있는 모든 hello 패밀리를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="6940b-134">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="6940b-135">**결과**</span><span class="sxs-lookup"><span data-stu-id="6940b-135">**Results**</span></span>

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
<span data-ttu-id="6940b-136">}</span><span class="sxs-lookup"><span data-stu-id="6940b-136">}</span></span>

## <span data-ttu-id="6940b-137"><a id="examplequery7"></a>예제 쿼리 7</span><span class="sxs-lookup"><span data-stu-id="6940b-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="6940b-138">hello 다음 쿼리의 자식 배열 크기는 3 모든 hello 패밀리를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="6940b-139">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="6940b-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="6940b-140">**결과**</span><span class="sxs-lookup"><span data-stu-id="6940b-140">**Results**</span></span>

<span data-ttu-id="6940b-141">2명 이상의 자식이 있는 가족이 없기 때문에 결과가 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="6940b-142">매개 변수 2는 경우에이 쿼리는 성공 하 고 hello 전체 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6940b-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6940b-143">Next steps</span></span>

<span data-ttu-id="6940b-144">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="6940b-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6940b-145">방법에 대해 배웠습니다 tooquery MongoDB를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6940b-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="6940b-146">이제 진행할 수 있습니다 다음 자습서 toolearn toohello 어떻게 toodistribute 데이터 전체적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6940b-147">전 세계로 데이터 배포</span><span class="sxs-lookup"><span data-stu-id="6940b-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

