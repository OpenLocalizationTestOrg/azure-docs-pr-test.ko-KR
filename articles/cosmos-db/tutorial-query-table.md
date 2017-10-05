---
title: "Azure Cosmos DB에서 테이블 데이터를 쿼리하는 방법 | Microsoft Docs"
description: "Azure Cosmos DB에서 테이블 데이터를 쿼리하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="57811-104">Azure Cosmos DB: Table API(미리 보기)를 사용하여 테이블 데이터를 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="57811-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="57811-105">Azure Cosmos DB의 [Table API](table-introduction.md)(미리 보기)는 키/값(테이블) 데이터에 대한 OData 및 [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="57811-106">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="57811-107">Table API를 사용한 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="57811-107">Querying data with the Table API</span></span>

<span data-ttu-id="57811-108">이 문서의 쿼리에서는 다음 샘플 `People` 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="57811-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="57811-109">PartitionKey</span></span> | <span data-ttu-id="57811-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="57811-110">RowKey</span></span> | <span data-ttu-id="57811-111">Email</span><span class="sxs-lookup"><span data-stu-id="57811-111">Email</span></span> | <span data-ttu-id="57811-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="57811-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="57811-113">Harp</span><span class="sxs-lookup"><span data-stu-id="57811-113">Harp</span></span> | <span data-ttu-id="57811-114">Walter</span><span class="sxs-lookup"><span data-stu-id="57811-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="57811-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="57811-115">425-555-0101</span></span> |
| <span data-ttu-id="57811-116">Smith</span><span class="sxs-lookup"><span data-stu-id="57811-116">Smith</span></span> | <span data-ttu-id="57811-117">Ben</span><span class="sxs-lookup"><span data-stu-id="57811-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="57811-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="57811-118">425-555-0102</span></span> |
| <span data-ttu-id="57811-119">Smith</span><span class="sxs-lookup"><span data-stu-id="57811-119">Smith</span></span> | <span data-ttu-id="57811-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="57811-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="57811-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="57811-121">425-555-0104</span></span> | 

<span data-ttu-id="57811-122">Azure Cosmos DB는 Azure Table Storage API와 호환되므로 Table API를 사용하여 쿼리하는 방법에 대한 자세한 내용은 [테이블 및 엔터티 쿼리](https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57811-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="57811-123">Azure Cosmos DB에서 제공하는 프리미엄 기능에 대한 자세한 내용은 [Azure Cosmos DB: Table API](table-introduction.md) 및 [.NET에서 Table API를 통해 개발](tutorial-develop-table-dotnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57811-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="57811-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="57811-124">Prerequisites</span></span>

<span data-ttu-id="57811-125">이러한 쿼리가 작동하려면 Azure Cosmos DB 계정이 있어야 하며 컨테이너에 엔터티 데이터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="57811-126">이들 중 하나라도 없는가요?</span><span class="sxs-lookup"><span data-stu-id="57811-126">Don't have any of those?</span></span> <span data-ttu-id="57811-127">그러면 [5분 빠른 시작](https://aka.ms/acdbtnetqs) 또는 [개발자 자습서](https://aka.ms/acdbtabletut)를 수행하여 계정을 만들고 데이터베이스를 채워 놓으세요.</span><span class="sxs-lookup"><span data-stu-id="57811-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="57811-128">PartitionKey 및 RowKey에 대한 쿼리</span><span class="sxs-lookup"><span data-stu-id="57811-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="57811-129">PartitionKey 및 RowKey 속성은 엔터티의 기본 키를 구성하므로 다음과 같은 특수 구문을 사용하여 엔터티를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="57811-130">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="57811-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="57811-131">**결과**</span><span class="sxs-lookup"><span data-stu-id="57811-131">**Results**</span></span>

| <span data-ttu-id="57811-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="57811-132">PartitionKey</span></span> | <span data-ttu-id="57811-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="57811-133">RowKey</span></span> | <span data-ttu-id="57811-134">Email</span><span class="sxs-lookup"><span data-stu-id="57811-134">Email</span></span> | <span data-ttu-id="57811-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="57811-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="57811-136">Harp</span><span class="sxs-lookup"><span data-stu-id="57811-136">Harp</span></span> | <span data-ttu-id="57811-137">Walter</span><span class="sxs-lookup"><span data-stu-id="57811-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="57811-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="57811-138">425-555-0104</span></span> |

<span data-ttu-id="57811-139">또는 다음 섹션과 같이 `$filter` 옵션의 일부로 이러한 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="57811-140">키 속성 이름과 상수 값은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="57811-141">PartitionKey 및 RowKey 속성은 모두 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="57811-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="57811-142">OData 필터를 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="57811-142">Query by using an OData filter</span></span>
<span data-ttu-id="57811-143">필터 문자열을 생성할 때는 다음 규칙에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="57811-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="57811-144">OData 프로토콜 사양에 정의된 논리 연산자를 사용하여 속성과 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="57811-145">동적 값과 속성을 비교할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="57811-146">식의 한 쪽은 상수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="57811-147">속성 이름, 연산자 및 상수 값은 URL로 인코딩된 공백으로 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="57811-148">URL로 인코딩된 공백은 `%20`입니다.</span><span class="sxs-lookup"><span data-stu-id="57811-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="57811-149">필터 문자열의 모든 부분은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="57811-150">상수 값은 유효한 결과를 반환하는 필터에 대한 속성과 동일한 데이터 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57811-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="57811-151">속성 형식에 대한 자세한 내용은 [테이블 서비스 데이터 모델 이해](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57811-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="57811-152">다음은 OData `$filter`를 사용하여 PartitionKey 및 Email 속성으로 필터링하는 방법을 보여 주는 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="57811-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="57811-153">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="57811-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="57811-154">다양한 데이터 형식에 대한 필터 식을 생성하는 방법에 대한 자세한 내용은 [테이블 및 엔터티 쿼리](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57811-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="57811-155">**결과**</span><span class="sxs-lookup"><span data-stu-id="57811-155">**Results**</span></span>

| <span data-ttu-id="57811-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="57811-156">PartitionKey</span></span> | <span data-ttu-id="57811-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="57811-157">RowKey</span></span> | <span data-ttu-id="57811-158">Email</span><span class="sxs-lookup"><span data-stu-id="57811-158">Email</span></span> | <span data-ttu-id="57811-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="57811-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="57811-160">Ben</span><span class="sxs-lookup"><span data-stu-id="57811-160">Ben</span></span> |<span data-ttu-id="57811-161">Smith</span><span class="sxs-lookup"><span data-stu-id="57811-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="57811-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="57811-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="57811-163">LINQ를 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="57811-163">Query by using LINQ</span></span> 
<span data-ttu-id="57811-164">해당 OData 쿼리 식으로 변환되는 LINQ를 사용하여 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="57811-165">다음은 .NET SDK를 사용하여 쿼리를 작성하는 방법을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="57811-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="57811-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57811-166">Next steps</span></span>

<span data-ttu-id="57811-167">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57811-168">Table API(미리 보기)를 사용하여 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="57811-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="57811-169">이제 전 세계로 데이터를 배포하는 방법을 알아보려면 다음 자습서로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57811-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57811-170">전 세계로 데이터 배포</span><span class="sxs-lookup"><span data-stu-id="57811-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
