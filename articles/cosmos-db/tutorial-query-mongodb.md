---
title: "Azure Cosmos DB: DocumentDB API를 사용하여 쿼리하는 방법 | Microsoft Docs"
description: "Azure Cosmos DB의 DocumentDB API를 사용하여 쿼리하는 방법을 알아봅니다."
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
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="ae6f4-104">Azure Cosmos DB: MongoDB API를 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ae6f4-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="ae6f4-105">Azure Cosmos DB [MongoDB API](mongodb-introduction.md)는 [MongoDB 셸 쿼리](https://docs.mongodb.com/manual/tutorial/query-documents/)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="ae6f4-106">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ae6f4-107">MongoDB를 사용한 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="ae6f4-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="ae6f4-108">샘플 문서</span><span class="sxs-lookup"><span data-stu-id="ae6f4-108">Sample document</span></span>

<span data-ttu-id="ae6f4-109">이 문서의 쿼리에서는 다음 샘플 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="ae6f4-110"><a id="examplequery1"></a>예제 쿼리 1</span><span class="sxs-lookup"><span data-stu-id="ae6f4-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="ae6f4-111">위의 샘플 가족 문서를 고려해 볼 때 다음 쿼리에서는 ID 필드가 `WakefieldFamily`와 일치하는 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="ae6f4-112">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="ae6f4-113">**결과**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-113">**Results**</span></span>

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

## <span data-ttu-id="ae6f4-114"><a id="examplequery2"></a>예제 쿼리 2</span><span class="sxs-lookup"><span data-stu-id="ae6f4-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="ae6f4-115">다음 쿼리에서는 가족의 모든 자식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="ae6f4-116">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="ae6f4-117">**결과**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-117">**Results**</span></span>

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


## <span data-ttu-id="ae6f4-118"><a id="examplequery3"></a>예제 쿼리 3</span><span class="sxs-lookup"><span data-stu-id="ae6f4-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="ae6f4-119">다음 쿼리에서는 등록된 모든 가족을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="ae6f4-120">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="ae6f4-121">**결과** 문서가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="ae6f4-122"><a id="examplequery4"></a>예제 쿼리 4</span><span class="sxs-lookup"><span data-stu-id="ae6f4-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="ae6f4-123">다음 쿼리에서는 등록되지 않은 모든 가족을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="ae6f4-124">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="ae6f4-125">**결과**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-125">**Results**</span></span>

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
<span data-ttu-id="ae6f4-126">}</span><span class="sxs-lookup"><span data-stu-id="ae6f4-126">}</span></span>

## <span data-ttu-id="ae6f4-127"><a id="examplequery5"></a>예제 쿼리 5</span><span class="sxs-lookup"><span data-stu-id="ae6f4-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="ae6f4-128">다음 쿼리에서는 등록되지 않은 모든 가족을 반환하고 거주 지역(state)은 NY입니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="ae6f4-129">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="ae6f4-130">**결과**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-130">**Results**</span></span>

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
<span data-ttu-id="ae6f4-131">}</span><span class="sxs-lookup"><span data-stu-id="ae6f4-131">}</span></span>


## <span data-ttu-id="ae6f4-132"><a id="examplequery6"></a>예제 쿼리 6</span><span class="sxs-lookup"><span data-stu-id="ae6f4-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="ae6f4-133">다음 쿼리에서는 자식(children)의 학년(grade)이 8인 모든 가족을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="ae6f4-134">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="ae6f4-135">**결과**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-135">**Results**</span></span>

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
<span data-ttu-id="ae6f4-136">}</span><span class="sxs-lookup"><span data-stu-id="ae6f4-136">}</span></span>

## <span data-ttu-id="ae6f4-137"><a id="examplequery7"></a>예제 쿼리 7</span><span class="sxs-lookup"><span data-stu-id="ae6f4-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="ae6f4-138">다음 쿼리에서는 children 배열의 크기가 3인 모든 가족을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="ae6f4-139">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="ae6f4-140">**결과**</span><span class="sxs-lookup"><span data-stu-id="ae6f4-140">**Results**</span></span>

<span data-ttu-id="ae6f4-141">2명 이상의 자식이 있는 가족이 없기 때문에 결과가 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="ae6f4-142">매개 변수가 2일 때만 이 쿼리가 성공하여 전체 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae6f4-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae6f4-143">Next steps</span></span>

<span data-ttu-id="ae6f4-144">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae6f4-145">MongoDB를 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ae6f4-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="ae6f4-146">이제 전 세계로 데이터를 배포하는 방법을 알아보려면 다음 자습서로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae6f4-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae6f4-147">전 세계로 데이터 배포</span><span class="sxs-lookup"><span data-stu-id="ae6f4-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

