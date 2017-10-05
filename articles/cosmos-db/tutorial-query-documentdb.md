---
title: "Azure Cosmos DB에서 SQL을 사용하여 쿼리하는 방법 | Microsoft Docs"
description: "Azure Cosmos DB에서 SQL을 사용하여 DocumentDB 데이터를 쿼리하는 방법을 알아봅니다."
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
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="f5ad7-104">Azure Cosmos DB: SQL을 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5ad7-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="f5ad7-105">Azure Cosmos DB [DocumentDB API](documentdb-introduction.md)는 SQL을 사용하여 문서를 쿼리할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="f5ad7-106">이 문서에서는 샘플 문서 및 두 가지 샘플 SQL 쿼리와 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="f5ad7-107">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f5ad7-108">SQL을 사용한 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="f5ad7-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="f5ad7-109">샘플 문서</span><span class="sxs-lookup"><span data-stu-id="f5ad7-109">Sample document</span></span>

<span data-ttu-id="f5ad7-110">이 문서의 SQL 쿼리에서는 다음과 같은 샘플 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="f5ad7-111">SQL 쿼리를 실행할 수 있는 위치</span><span class="sxs-lookup"><span data-stu-id="f5ad7-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="f5ad7-112">Azure Portal의 [데이터 탐색기]를 사용하여 [REST API 및 SDK](documentdb-sdk-dotnet.md)를 통해 쿼리를 실행할 수 있으며, 기존 샘플 데이터 집합에 대해 쿼리를 실행하는 [쿼리 실습](https://www.documentdb.com/sql/demo)도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="f5ad7-113">SQL 쿼리에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="f5ad7-114">SQL 쿼리 및 SQL 구문</span><span class="sxs-lookup"><span data-stu-id="f5ad7-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="f5ad7-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f5ad7-115">Prerequisites</span></span>

<span data-ttu-id="f5ad7-116">이 자습서에서는 Azure Cosmos DB 계정과 컬렉션이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="f5ad7-117">이들 중 하나라도 없는가요?</span><span class="sxs-lookup"><span data-stu-id="f5ad7-117">Don't have any of those?</span></span> <span data-ttu-id="f5ad7-118">그러면 [5분 퀵 스타트](create-mongodb-nodejs.md) 또는 [개발자 자습서](tutorial-develop-mongodb.md)를 수행하여 계정과 컬렉션을 만들어 놓으세요.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="f5ad7-119">예제 쿼리 1</span><span class="sxs-lookup"><span data-stu-id="f5ad7-119">Example query 1</span></span>

<span data-ttu-id="f5ad7-120">위의 샘플 가족 문서를 고려해 볼 때 다음 SQL 쿼리에서는 ID 필드가 `WakefieldFamily`와 일치하는 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="f5ad7-121">`SELECT *` 문이므로 쿼리 결과는 완전한 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="f5ad7-122">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="f5ad7-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="f5ad7-123">**결과**</span><span class="sxs-lookup"><span data-stu-id="f5ad7-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="f5ad7-124">예제 쿼리 2</span><span class="sxs-lookup"><span data-stu-id="f5ad7-124">Example query 2</span></span>

<span data-ttu-id="f5ad7-125">다음 쿼리에서는 ID가 `WakefieldFamily`와 일치하는 가족의 자식 이름을 학년(grade) 순서로 정렬하여 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="f5ad7-126">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="f5ad7-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="f5ad7-127">**결과**</span><span class="sxs-lookup"><span data-stu-id="f5ad7-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="f5ad7-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5ad7-128">Next steps</span></span>

<span data-ttu-id="f5ad7-129">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5ad7-130">SQL을 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5ad7-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="f5ad7-131">이제 전 세계로 데이터를 배포하는 방법을 알아보려면 다음 자습서로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ad7-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f5ad7-132">전 세계로 데이터 배포</span><span class="sxs-lookup"><span data-stu-id="f5ad7-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

