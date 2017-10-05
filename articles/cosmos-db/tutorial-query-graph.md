---
title: "Azure Cosmos DB에서 그래프 데이터를 쿼리하는 방법 | Microsoft Docs"
description: "Azure Cosmos DB에서 그래프 데이터를 쿼리하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="d5529-104">Azure Cosmos DB: Graph API(미리 보기)를 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="d5529-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="d5529-105">Azure Cosmos DB [Graph API](graph-introduction.md)(미리 보기)는 [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="d5529-106">이 문서에서는 샘플 문서와 쿼리를 제공하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="d5529-107">Gremlin에 대해서는 [Gremlin 지원](gremlin-support.md) 문서에서 자세히 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="d5529-108">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d5529-109">Gremlin을 사용한 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="d5529-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5529-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d5529-110">Prerequisites</span></span>

<span data-ttu-id="d5529-111">이러한 쿼리가 작동하려면 Azure Cosmos DB 계정이 있어야 하며 컨테이너에 그래프 데이터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="d5529-112">이들 중 하나라도 없는가요?</span><span class="sxs-lookup"><span data-stu-id="d5529-112">Don't have any of those?</span></span> <span data-ttu-id="d5529-113">그러면 [5분 퀵 스타트](create-graph-dotnet.md) 또는 [개발자 자습서](tutorial-query-graph.md)를 수행하여 계정을 만들고 데이터베이스를 채워 놓으세요.</span><span class="sxs-lookup"><span data-stu-id="d5529-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="d5529-114">[Azure Cosmos DB .NET 그래프 라이브러리](graph-sdk-dotnet.md), [Gremlin 콘솔](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) 또는 즐겨찾는 Gremlin 드라이버를 사용하여 다음 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="d5529-115">그래프의 꼭짓점 계산</span><span class="sxs-lookup"><span data-stu-id="d5529-115">Count vertices in the graph</span></span>

<span data-ttu-id="d5529-116">다음 코드 조각에서는 그래프의 꼭짓점 수를 계산하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="d5529-117">필터</span><span class="sxs-lookup"><span data-stu-id="d5529-117">Filters</span></span>

<span data-ttu-id="d5529-118">Gremlin의 `has` 및 `hasLabel` 단계를 사용하여 필터링을 수행하고, `and`, `or` 및 `not`으로 필터를 결합하여 더 복잡한 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="d5529-119">Azure Cosmos DB는 빠른 쿼리를 위해 꼭짓점과 각도 내의 모든 속성에 대해 스키마 독립적 인덱싱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="d5529-120">프로젝션</span><span class="sxs-lookup"><span data-stu-id="d5529-120">Projection</span></span>

<span data-ttu-id="d5529-121">`values` 단계를 사용하여 쿼리 결과에 특정 속성을 프로젝션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="d5529-122">관련 가장자리 및 꼭짓점 찾기</span><span class="sxs-lookup"><span data-stu-id="d5529-122">Find related edges and vertices</span></span>

<span data-ttu-id="d5529-123">지금까지 모든 데이터베이스에서 작동하는 쿼리 연산자만 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="d5529-124">관련 가장자리와 꼭짓점으로 이동해야 할 때 그래프는 이 순회 작업에 빠르고 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="d5529-125">Thomas의 친구들을 모두 찾아 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="d5529-126">이렇게 하려면 Gremlin의 `outE` 단계를 사용하여 Thomas의 모든 가장자리를 찾은(out-edge) 다음, Gremlin의 `inV` 단계를 사용하여 이러한 가장자리에서 꼭짓점으로 이동합니다(in-vertex).</span><span class="sxs-lookup"><span data-stu-id="d5529-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="d5529-127">다음 쿼리에서는 `outE`과 `inV`를 두 번 호출함으로써 홉을 두 번 수행하여 Thomas의 "친구의 친구"를 모두 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="d5529-128">Gremlin을 사용하여 필터 식을 혼합하고, `loop` 단계를 사용하여 루핑을 수행하고, `choose` 단계를 사용하여 조건부 탐색을 구현하는 등 더욱 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="d5529-129">[Gremlin 지원](gremlin-support.md)에서 수행할 수 있는 작업에 대해 자세히 알아보세요!</span><span class="sxs-lookup"><span data-stu-id="d5529-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5529-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5529-130">Next steps</span></span>

<span data-ttu-id="d5529-131">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5529-132">그래프를 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="d5529-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="d5529-133">이제 전 세계로 데이터를 배포하는 방법을 알아보려면 다음 자습서로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5529-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5529-134">전 세계로 데이터 배포</span><span class="sxs-lookup"><span data-stu-id="d5529-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)