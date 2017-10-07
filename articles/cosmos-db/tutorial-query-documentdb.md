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
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="d1264-104">Azure Cosmos DB: 어떻게 SQL을 사용 하 여 tooquery?</span><span class="sxs-lookup"><span data-stu-id="d1264-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="d1264-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) 지원 SQL을 사용 하 여 문서를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="d1264-106">이 문서에서는 샘플 문서 및 두 가지 샘플 SQL 쿼리와 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="d1264-107">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d1264-108">SQL을 사용한 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="d1264-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="d1264-109">샘플 문서</span><span class="sxs-lookup"><span data-stu-id="d1264-109">Sample document</span></span>

<span data-ttu-id="d1264-110">이 문서의 hello SQL 쿼리는 다음 샘플 문서 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-110">hello SQL queries in this article use hello following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="d1264-111">SQL 쿼리를 실행할 수 있는 위치</span><span class="sxs-lookup"><span data-stu-id="d1264-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="d1264-112">Hello hello 통해 Azure 포털에에서 있는 데이터 탐색기 hello를 사용 하 여 쿼리를 실행할 수 있습니다 [REST API와 Sdk](documentdb-sdk-dotnet.md), 및에 hello [Query playground](https://www.documentdb.com/sql/demo), 기존 샘플 데이터 집합에서 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="d1264-113">SQL 쿼리에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1264-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="d1264-114">SQL 쿼리 및 SQL 구문</span><span class="sxs-lookup"><span data-stu-id="d1264-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="d1264-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d1264-115">Prerequisites</span></span>

<span data-ttu-id="d1264-116">이 자습서에서는 Azure Cosmos DB 계정과 컬렉션이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="d1264-117">이들 중 하나라도 없는가요?</span><span class="sxs-lookup"><span data-stu-id="d1264-117">Don't have any of those?</span></span> <span data-ttu-id="d1264-118">전체 hello [5 분 퀵 스타트](create-mongodb-nodejs.md) 또는 hello [개발자 자습서](tutorial-develop-mongodb.md) toocreate 계정과 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="d1264-119">예제 쿼리 1</span><span class="sxs-lookup"><span data-stu-id="d1264-119">Example query 1</span></span>

<span data-ttu-id="d1264-120">매개 변수로 받아 hello 샘플 패밀리 문서 위의 다음 SQL 쿼리에서 반환 hello 문서 hello id 필드와 일치 하는 `WakefieldFamily`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="d1264-121">이기 때문에 `SELECT *` 문, hello 쿼리의 hello 출력은 JSON 문서를 완료 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="d1264-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="d1264-122">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="d1264-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="d1264-123">**결과**</span><span class="sxs-lookup"><span data-stu-id="d1264-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="d1264-124">예제 쿼리 2</span><span class="sxs-lookup"><span data-stu-id="d1264-124">Example query 2</span></span>

<span data-ttu-id="d1264-125">hello 다음 쿼리 id와 일치 하는 hello 제품군의 자식 항목의 모든 hello 지정 된 이름을 반환 `WakefieldFamily` 해당 등급으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="d1264-126">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="d1264-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="d1264-127">**결과**</span><span class="sxs-lookup"><span data-stu-id="d1264-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="d1264-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1264-128">Next steps</span></span>

<span data-ttu-id="d1264-129">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="d1264-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d1264-130">방법에 대해 배웠습니다 tooquery SQL을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d1264-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="d1264-131">이제 진행할 수 있습니다 다음 자습서 toolearn toohello 어떻게 toodistribute 데이터 전체적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1264-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1264-132">전 세계로 데이터 배포</span><span class="sxs-lookup"><span data-stu-id="d1264-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

