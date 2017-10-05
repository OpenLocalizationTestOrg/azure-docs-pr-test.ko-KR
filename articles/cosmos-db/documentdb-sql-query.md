---
title: "Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리 | Microsoft Docs"
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
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="fce67-105">Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="fce67-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="fce67-106">Microsoft Azure Cosmos DB는 JSON 쿼리 언어인 SQL(구조적 쿼리 언어)을 사용한 문서 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="fce67-107">Cosmos DB는 스키마가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="fce67-108">DocumentDB는 데이터베이스 엔진 내에 직접 JSON 데이터 모델을 커밋하므로 명시적 스키마나 보조 인덱스 생성을 요구하지 않고 JSON 문서의 자동 인덱싱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="fce67-109">Cosmos DB용 쿼리 언어를 설계할 때 다음 두 가지 목표를 고려했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="fce67-110">새 JSON 쿼리 언어를 고안하는 대신 SQL 언어를 지원하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="fce67-111">SQL은 가장 익숙하고 많이 사용하는 쿼리 언어 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="fce67-112">Cosmos DB SQL은 JSON 문서에 대한 풍부한 쿼리를 위한 공식 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="fce67-113">데이터베이스 엔진에서 직접 JavaScript를 실행할 수 있는 JSON 문서 데이터베이스로서, JavaScript의 프로그래밍 모델을 쿼리 언어의 기초로 사용하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="fce67-114">DocumentDB API SQL은 JavaScript의 형식 시스템, 식 평가 및 함수 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="fce67-115">따라서 관계형 프로젝션, JSON 문서에 대한 계층적 탐색, 자체 조인, 공간 쿼리, JavaScript로만 작성된 UDF(사용자 정의 함수) 호출 등을 위한 일반 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="fce67-116">이러한 기능은 응용 프로그램과 데이터베이스 간의 충돌을 줄이는 데 도움이 되며 개발자 생산성에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="fce67-117">먼저 Aravind Ramachandran이 Cosmos DB의 쿼리 기능을 보여 주는 다음 동영상을 보고, Cosmos DB를 사용해 보고 데이터 집합에 대해 SQL 쿼리를 실행하는 [쿼리 실습](http://www.documentdb.com/sql/demo)을 방문하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="fce67-118">그런 다음 이 문서로 돌아와 SQL 쿼리 자습서로 몇 가지 단순한 JSON 문서 및 SQL 명령을 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="fce67-119"><a id="GettingStarted"></a>Cosmos DB의 SQL 명령 시작하기</span><span class="sxs-lookup"><span data-stu-id="fce67-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="fce67-120">Cosmos DB SQL의 작동 방식을 확인하기 위해 몇 개의 간단한 JSON 문서로 시작해서 몇 가지 단순한 쿼리를 연습해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="fce67-121">두 가족에 대한 다음 두 개의 JSON 문서를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="fce67-122">Cosmos DB를 사용하면 스키마나 보조 인덱스를 명시적으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="fce67-123">Cosmos DB 컬렉션에 JSON 문서를 삽입한 후 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="fce67-124">다음은 Andersen 가족, 부모, 자녀(및 애완 동물), 주소 및 등록 정보에 대한 단순한 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="fce67-125">이 문서에는 문자열, 숫자, 부울, 배열 및 중첩 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="fce67-126">**문서**</span><span class="sxs-lookup"><span data-stu-id="fce67-126">**Document**</span></span>  

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

<span data-ttu-id="fce67-127">다음은 한 가지 미묘한 차이점이 있는 두 번째 문서입니다. `givenName` 및 `familyName`이 `firstName` 및 `lastName` 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="fce67-128">**문서**</span><span class="sxs-lookup"><span data-stu-id="fce67-128">**Document**</span></span>  

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

<span data-ttu-id="fce67-129">이제 DocumentDB API SQL의 몇 가지 주요 측면을 이해하기 위해 이 데이터에 대해 몇 가지 쿼리를 시도해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="fce67-130">예를 들어 다음 쿼리는 ID 필드가 `AndersenFamily`와 일치하는 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="fce67-131">쿼리가 `SELECT *`이므로 쿼리의 출력은 전체 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="fce67-132">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-133">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-133">**Results**</span></span>

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


<span data-ttu-id="fce67-134">이제 JSON 출력을 다른 형식으로 변경해야 하는 경우를 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="fce67-135">이 쿼리는 주소의 구/군/시 이름이 시/도와 같은 경우 두 개의 선택한 필드인 이름 및 구/군/시와 함께 새 JSON 개체를 프로젝션합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="fce67-136">이 경우 "NY, NY"가 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="fce67-137">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="fce67-138">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="fce67-139">다음 쿼리는 ID가 거주 도시의 순서로 정렬한 `WakefieldFamily` 와 일치하는 가족의 자녀 이름을 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="fce67-140">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="fce67-141">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="fce67-142">지금까지 확인한 예제를 통해 Cosmos DB 쿼리 언어의 몇 가지 중요한 측면을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="fce67-143">DocumentDB API SQL은 JSON 값에 대해 작동하므로 행과 열 대신 트리 모양의 엔터티를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="fce67-144">따라서 이 언어를 사용하면 임의 깊이의 트리 노드를 참조할 수 있습니다(예: `Node1.Node2.Node3…..Nodem`). 이는 `<table>.<column>`의 두 부분을 참조하는 관계형 SQL과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="fce67-145">구조적 쿼리 언어는 스키마 없는 데이터로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="fce67-146">따라서 형식 시스템을 동적으로 바인딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="fce67-147">문서에 따라 동일한 식이 다른 형식을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="fce67-148">쿼리 결과는 유효한 JSON 값이지만 고정 스키마가 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="fce67-149">Cosmos DB는 엄격한 JSON 문서만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="fce67-150">즉, 형식 시스템과 식이 JSON 형식만 처리하도록 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="fce67-151">자세한 내용은 [JSON 사양](http://www.json.org/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="fce67-152">Cosmos DB 컬렉션은 JSON 문서의 스키마 없는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="fce67-153">컬렉션의 문서 내 및 문서 간 데이터 엔터티의 관계는 기본 키 및 외래 키 관계가 아니라 포함을 통해 암시적으로 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="fce67-154">이것은 이 문서의 뒷부분에서 설명하는 문서 내 조인과 관련해서 주의할 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="fce67-155"><a id="Indexing"></a> Cosmos DB 인덱싱</span><span class="sxs-lookup"><span data-stu-id="fce67-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="fce67-156">DocumentDB API SQL 구문을 시작하기 전에 Cosmos DB의 인덱싱 설계를 살펴보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="fce67-157">데이터베이스 인덱스의 목적은 우수한 처리량과 짧은 대기 시간을 제공하는 동시에 다양한 형태와 모양의 쿼리를 최소 리소스 사용(예: CPU, 입출력)으로 처리하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="fce67-158">데이터베이스 쿼리에 올바른 인덱스를 선택하려면 대체로 많은 계획과 실험이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="fce67-159">이 접근 방법은 데이터가 엄격한 스키마를 준수하지 않고 빠르게 발전하는 스키마 없는 데이터베이스에 문제를 제기합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="fce67-160">따라서 Cosmos DB 인덱싱 하위 시스템을 설계할 때 다음 목표를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="fce67-161">스키마가 필요 없는 문서 인덱싱: 인덱싱 하위 시스템에 스키마 정보가 필요 없거나 문서 스키마에 대한 가정을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="fce67-162">효율적이고 풍부한 계층적 관계형 쿼리 지원: 인덱스는 계층적 관계형 프로젝션 지원을 포함하여 Cosmos DB 쿼리 언어를 효율적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="fce67-163">지속적인 쓰기 볼륨에서도 일관성 있는 쿼리 지원: 일관성 있는 쿼리와 더불어 높은 쓰기 처리량 워크로드를 위해 지속적인 쓰기 볼륨에서도 인덱스가 온라인에서 효율적으로 증분 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="fce67-164">일관성 있는 인덱스 업데이트는 사용자가 문서 서비스를 구성한 일관성 수준으로 쿼리를 처리하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="fce67-165">다중 테넌트 지원: 테넌트의 리소스 거버넌스를 위한 예약 기반 모델을 고려하여 복제본당 할당된 시스템 리소스(CPU, 메모리, 초당 입출력 작업 수) 예산 내에서 인덱스 업데이트가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="fce67-166">저장소 효율성: 비용 효율성을 위해 인덱스의 디스크에 있는 저장소 오버헤드가 제한되고 예측 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="fce67-167">이 목표는 Cosmos DB를 사용할 경우 개발자가 비용을 기반으로 인덱스 오버헤드와 쿼리 성능 간을 절충할 수 있기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="fce67-168">컬렉션에 대한 인덱싱 정책을 구성하는 방법을 보여 주는 샘플은 MSDN에서 [Azure Cosmos DB 샘플](https://github.com/Azure/azure-documentdb-net)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="fce67-169">이제 Azure Cosmos DB SQL 구문의 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="fce67-170"><a id="Basics"></a>Azure Cosmos DB SQL 쿼리의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="fce67-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="fce67-171">ANSI-SQL 표준에 따라 모든 쿼리는 SELECT 절과 선택적 FROM 및 WHERE 절로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="fce67-172">일반적으로 각 쿼리에 대해 FROM 절의 소스가 열거됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="fce67-173">그런 다음 WHERE 절의 필터를 소스에 적용하여 JSON 문서의 하위 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="fce67-174">마지막으로, SELECT 절을 사용하여 선택 목록에서 요청된 JSON 값을 프로젝션합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="fce67-175"><a id="FromClause"></a>FROM 절</span><span class="sxs-lookup"><span data-stu-id="fce67-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="fce67-176">쿼리의 뒷부분에서 소스를 필터링/프로젝션하지 않을 경우 `FROM <from_specification>` 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="fce67-177">이 절의 목적은 쿼리가 작동해야 하는 데이터 원본을 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="fce67-178">일반적으로 전체 컬렉션이 소스이지만 컬렉션의 하위 집합을 대신 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="fce67-179">`SELECT * FROM Families` 와 유사한 쿼리는 전체 Families 컬렉션이 열거할 소스임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="fce67-180">컬렉션 이름을 사용하는 대신 특수 식별자 ROOT를 사용하여 컬렉션을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="fce67-181">다음 목록은 쿼리 단위로 적용되는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="fce67-182">컬렉션을 별칭으로 `SELECT f.id FROM Families AS f` 또는 간단히 `SELECT f.id FROM Families f`로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="fce67-183">여기서 `f`는 `Families`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="fce67-184">`AS` 는 식별자를 별칭으로 지정하는 선택적 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="fce67-185">별칭으로 지정한 후에는 원본 소스를 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="fce67-186">예를 들어 `SELECT Families.id FROM Families f` 는 "Families" 식별자를 더 이상 예약할 수 없으므로 구문이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="fce67-187">참조해야 하는 모든 속성을 정규화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="fce67-188">엄격한 스키마 준수가 없을 경우 모호한 바인딩을 방지하기 위해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="fce67-189">따라서 `SELECT id FROM Families f`는 `id` 속성이 바인딩되지 않았으므로 구문이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="fce67-190">하위 문서</span><span class="sxs-lookup"><span data-stu-id="fce67-190">Subdocuments</span></span>
<span data-ttu-id="fce67-191">소스를 더 작은 하위 집합으로 줄일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="fce67-192">예를 들어 각 문서에서 하위 트리만을 열거하려는 경우 다음 예제에서처럼 하위 루트가 원본이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="fce67-193">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="fce67-194">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-194">**Results**</span></span>  

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

<span data-ttu-id="fce67-195">위 예제에서는 배열을 원본으로 사용했지만 다음 예제에 나온 대로 개체를 원본으로 사용할 수도 있습니다. 원본에 있는 유효한 모든 JSON 값(undefined 제외)이 쿼리 결과에 포함되기 위해 고려됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="fce67-196">일부 가족에 `address.state` 값이 없는 경우 쿼리 결과에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="fce67-197">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="fce67-198">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="fce67-199"><a id="WhereClause"></a>WHERE 절</span><span class="sxs-lookup"><span data-stu-id="fce67-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="fce67-200">WHERE 절(**`WHERE <filter_condition>`**)은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="fce67-201">소스에서 제공하는 JSON 문서가 결과의 일부로 포함되기 위해 충족해야 하는 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="fce67-202">JSON 문서가 결과에 고려되려면 지정된 조건이 "true"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="fce67-203">WHERE 절은 결과에 포함될 수 있는 소스 문서의 가장 작은 절대 하위 집합을 결정하기 위해 인덱스 계층에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="fce67-204">다음 쿼리는 이름 속성을 포함하고 속성 값이 `AndersenFamily`인 문서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="fce67-205">이름 속성이 없거나 값이 `AndersenFamily` 와 일치하지 않는 다른 문서는 모두 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="fce67-206">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-207">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="fce67-208">앞의 예제는 단순한 같음 쿼리를 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="fce67-209">DocumentDB API SQL은 다양한 스칼라 식도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="fce67-210">가장 일반적으로 사용되는 식은 이항 및 단항 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="fce67-211">소스 JSON 개체의 속성 참조도 유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="fce67-212">현재 지원되며 다음 예제와 같이 쿼리에 사용할 수 있는 이항 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="fce67-213">산술</span><span class="sxs-lookup"><span data-stu-id="fce67-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="fce67-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="fce67-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fce67-215">비트</span><span class="sxs-lookup"><span data-stu-id="fce67-215">Bitwise</span></span></td>    
<td><span data-ttu-id="fce67-216">|, &, ^, <<, >>, >>>(0 채우기 오른쪽 시프트)</span><span class="sxs-lookup"><span data-stu-id="fce67-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fce67-217">논리</span><span class="sxs-lookup"><span data-stu-id="fce67-217">Logical</span></span></td>
<td><span data-ttu-id="fce67-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="fce67-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fce67-219">비교</span><span class="sxs-lookup"><span data-stu-id="fce67-219">Comparison</span></span></td>    
<td><span data-ttu-id="fce67-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="fce67-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fce67-221">문자열</span><span class="sxs-lookup"><span data-stu-id="fce67-221">String</span></span></td>    
<td><span data-ttu-id="fce67-222">||(연결)</span><span class="sxs-lookup"><span data-stu-id="fce67-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="fce67-223">이항 연산자를 사용한 몇 가지 쿼리를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="fce67-224">단항 연산자 +,-, ~ 및 NOT도 지원되며 다음 예제에 표시된 대로 쿼리 내부에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="fce67-225">이항 및 단항 연산자뿐 아니라 속성 참조도 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="fce67-226">예를 들어 `SELECT * FROM Families f WHERE f.isRegistered`는 `isRegistered` 속성을 포함하고 속성 값이 JSON `true` 값과 같은 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="fce67-227">다른 값(false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>` 등)이면 소스 문서가 결과에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="fce67-228">같음 및 비교 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-228">Equality and comparison operators</span></span>
<span data-ttu-id="fce67-229">다음 표에서는 DocumentDB API SQL에서 두 JSON 형식 간의 같음 비교 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-233">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-234">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-235">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fce67-237">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fce67-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-254">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fce67-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-262">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fce67-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-270">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fce67-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fce67-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fce67-286">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fce67-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fce67-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fce67-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fce67-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="fce67-294">다른 비교 연산자(예: >, >=, !=, < 및 <=)의 경우</span><span class="sxs-lookup"><span data-stu-id="fce67-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="fce67-295">형식 비교 결과가 Undefined입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="fce67-296">두 개체 또는 두 배열 간 비교 결과가 Undefined입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="fce67-297">필터의 스칼라 식 결과가 Undefined인 경우 Undefined는 논리적으로 "true"가 아니므로 해당 문서가 결과에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="fce67-298">BETWEEN 키워드</span><span class="sxs-lookup"><span data-stu-id="fce67-298">BETWEEN keyword</span></span>
<span data-ttu-id="fce67-299">또한 ANSI SQL에서처럼 값의 범위에 대한 쿼리를 표현하는 BETWEEN 키워드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="fce67-300">문자열이나 숫자에 BETWEEN을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="fce67-301">예를 들어 이 쿼리는 첫 번째 자식의 등급이 1-5(모두 포함)인 가족 문서를 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="fce67-302">ANSI-SQL과 달리, 다음 예제처럼 BETWEEN 절을 FROM 절에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="fce67-303">쿼리 실행 시간을 단축하려면 BETWEEN 절에서 필터링되는 모든 숫자 속성/경로에 대해 범위 인덱스 형식을 사용하는 인덱싱 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="fce67-304">DocumentDB API와 ANSI SQL에서 BETWEEN을 사용하는 경우의 주요 차이점은 혼합 형식의 속성에 대해 범위 쿼리를 실행할 수 있다는 점입니다. 예를 들어 일부 문서에서는 "등급"이 숫자(5)이고 다른 문서에서는 문자열("grade4")일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="fce67-305">이러한 경우 JavaScript에서처럼 다른 두 형식 간 비교는 "undefined"가 되고 문서는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="fce67-306">논리(AND, OR 및 NOT) 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="fce67-307">논리 연산자는 부울 값에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="fce67-308">다음 표에는 이 연산자의 논리적 진위 표가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="fce67-309">또는</span><span class="sxs-lookup"><span data-stu-id="fce67-309">OR</span></span> | <span data-ttu-id="fce67-310">True</span><span class="sxs-lookup"><span data-stu-id="fce67-310">True</span></span> | <span data-ttu-id="fce67-311">False</span><span class="sxs-lookup"><span data-stu-id="fce67-311">False</span></span> | <span data-ttu-id="fce67-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fce67-313">True</span><span class="sxs-lookup"><span data-stu-id="fce67-313">True</span></span> |<span data-ttu-id="fce67-314">True</span><span class="sxs-lookup"><span data-stu-id="fce67-314">True</span></span> |<span data-ttu-id="fce67-315">True</span><span class="sxs-lookup"><span data-stu-id="fce67-315">True</span></span> |<span data-ttu-id="fce67-316">True</span><span class="sxs-lookup"><span data-stu-id="fce67-316">True</span></span> |
| <span data-ttu-id="fce67-317">False</span><span class="sxs-lookup"><span data-stu-id="fce67-317">False</span></span> |<span data-ttu-id="fce67-318">True</span><span class="sxs-lookup"><span data-stu-id="fce67-318">True</span></span> |<span data-ttu-id="fce67-319">False</span><span class="sxs-lookup"><span data-stu-id="fce67-319">False</span></span> |<span data-ttu-id="fce67-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-320">Undefined</span></span> |
| <span data-ttu-id="fce67-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-321">Undefined</span></span> |<span data-ttu-id="fce67-322">True</span><span class="sxs-lookup"><span data-stu-id="fce67-322">True</span></span> |<span data-ttu-id="fce67-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-323">Undefined</span></span> |<span data-ttu-id="fce67-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-324">Undefined</span></span> |

| <span data-ttu-id="fce67-325">AND</span><span class="sxs-lookup"><span data-stu-id="fce67-325">AND</span></span> | <span data-ttu-id="fce67-326">True</span><span class="sxs-lookup"><span data-stu-id="fce67-326">True</span></span> | <span data-ttu-id="fce67-327">False</span><span class="sxs-lookup"><span data-stu-id="fce67-327">False</span></span> | <span data-ttu-id="fce67-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fce67-329">True</span><span class="sxs-lookup"><span data-stu-id="fce67-329">True</span></span> |<span data-ttu-id="fce67-330">True</span><span class="sxs-lookup"><span data-stu-id="fce67-330">True</span></span> |<span data-ttu-id="fce67-331">False</span><span class="sxs-lookup"><span data-stu-id="fce67-331">False</span></span> |<span data-ttu-id="fce67-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-332">Undefined</span></span> |
| <span data-ttu-id="fce67-333">False</span><span class="sxs-lookup"><span data-stu-id="fce67-333">False</span></span> |<span data-ttu-id="fce67-334">False</span><span class="sxs-lookup"><span data-stu-id="fce67-334">False</span></span> |<span data-ttu-id="fce67-335">False</span><span class="sxs-lookup"><span data-stu-id="fce67-335">False</span></span> |<span data-ttu-id="fce67-336">False</span><span class="sxs-lookup"><span data-stu-id="fce67-336">False</span></span> |
| <span data-ttu-id="fce67-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-337">Undefined</span></span> |<span data-ttu-id="fce67-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-338">Undefined</span></span> |<span data-ttu-id="fce67-339">False</span><span class="sxs-lookup"><span data-stu-id="fce67-339">False</span></span> |<span data-ttu-id="fce67-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-340">Undefined</span></span> |

| <span data-ttu-id="fce67-341">NOT</span><span class="sxs-lookup"><span data-stu-id="fce67-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="fce67-342">True</span><span class="sxs-lookup"><span data-stu-id="fce67-342">True</span></span> |<span data-ttu-id="fce67-343">False</span><span class="sxs-lookup"><span data-stu-id="fce67-343">False</span></span> |
| <span data-ttu-id="fce67-344">False</span><span class="sxs-lookup"><span data-stu-id="fce67-344">False</span></span> |<span data-ttu-id="fce67-345">True</span><span class="sxs-lookup"><span data-stu-id="fce67-345">True</span></span> |
| <span data-ttu-id="fce67-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-346">Undefined</span></span> |<span data-ttu-id="fce67-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="fce67-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="fce67-348">IN 키워드</span><span class="sxs-lookup"><span data-stu-id="fce67-348">IN keyword</span></span>
<span data-ttu-id="fce67-349">IN 키워드는 지정된 값이 목록에 있는 값과 일치하는지를 확인하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="fce67-350">예를 들어 이 쿼리는 id가 "WakefieldFamily" 또는 "AndersenFamily" 중 하나인 가족 문서를 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="fce67-351">이 예는 상태가 지정된 값인 모든 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="fce67-352">3항(?) 및 병합(??) 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="fce67-353">3항 및 병합 연산자를 사용하여 널리 사용되는 프로그래밍 언어(예: C# 및 JavaScript)와 유사하게 조건식을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="fce67-354">3항(?) 연산자는 새로운 JSON 속성을 즉시 생성할 때 매우 간편하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="fce67-355">예를 들어 쿼리를 작성하여 아래에 표시된 대로 Beginner/Intermediate/Advanced와 같이 사람이 읽을 수 있는 형식으로 클래스 수준을 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="fce67-356">또한 아래 쿼리에서처럼 연산자에 대한 호출을 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="fce67-357">다른 쿼리 연산자에서처럼 조건식에서 참조된 속성이 문서에서 누락된 경우 또는 비교할 형식이 다른 경우 해당 문서가 쿼리 결과에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="fce67-358">병합(??) 연산자를 사용하면 문서에서 속성의 존재(정의됨)를</span><span class="sxs-lookup"><span data-stu-id="fce67-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="fce67-359">효율적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-359">is defined) in a document.</span></span> <span data-ttu-id="fce67-360">이 연산자는 반구조적 데이터나 혼합 형식의 데이터에 대해 쿼리할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="fce67-361">예를 들어 이 쿼리는 "lastName"(있는 경우) 또는 "surname"(없는 경우)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="fce67-362"><a id="EscapingReservedKeywords"></a>따옴표 붙은 속성 접근자</span><span class="sxs-lookup"><span data-stu-id="fce67-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="fce67-363">따옴표 붙은 속성 연산자 `[]`를 사용하여 속성에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="fce67-364">예를 들어 `SELECT c.grade` and `SELECT c["grade"]` 와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="fce67-365">이 구문은 공백, 특수 문자가 포함되어 있거나 SQL 키워드 또는 예약어와 동일한 이름을 공유하는 속성을 이스케이프해야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="fce67-366"><a id="SelectClause"></a>SELECT 절</span><span class="sxs-lookup"><span data-stu-id="fce67-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="fce67-367">SELECT 절(**`SELECT <select_list>`**)은 필수이며 ANSI-SQL과 같이 쿼리에서 검색할 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="fce67-368">소스 문서에서 필터링된 하위 집합이 프로젝션 단계로 전달되며, 여기서 전달된 각 입력에 대해 지정한 JSON 값이 검색되고 새 JSON 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="fce67-369">다음 예제에서는 일반적인 SELECT 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="fce67-370">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-371">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="fce67-372">중첩 속성</span><span class="sxs-lookup"><span data-stu-id="fce67-372">Nested properties</span></span>
<span data-ttu-id="fce67-373">다음 예제에서는 두 개의 중첩된 속성 `f.address.state` and `f.address.city`와 일치하는 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="fce67-374">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-375">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="fce67-376">다음 예제와 같이 프로젝션은 JSON 식도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="fce67-377">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-378">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="fce67-379">여기서 `$1` 의 역할을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="fce67-380">`SELECT` 절은 JSON 개체를 만들어야 하며 키가 제공되지 않았으므로 `$1`로 시작하는 암시적 인수 변수 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="fce67-381">예를 들어 이 쿼리는 `$1` 및 `$2` 레이블이 지정된 두 개의 암시적 인수 변수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="fce67-382">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-383">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="fce67-384">별칭 지정</span><span class="sxs-lookup"><span data-stu-id="fce67-384">Aliasing</span></span>
<span data-ttu-id="fce67-385">이제 값의 별칭을 명시적으로 지정하여 위 예제를 확장하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="fce67-386">AS는 별칭 지정에 사용되는 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="fce67-387">두 번째 값을 `NameInfo`로 프로젝션하는 동안 표시되므로 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="fce67-388">쿼리에 동일한 이름을 가진 두 개의 속성이 있을 경우 프로젝션된 결과에서 구분되도록 별칭 지정을 사용하여 속성 중 하나 또는 둘 다의 이름을 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="fce67-389">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-390">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="fce67-391">스칼라 식</span><span class="sxs-lookup"><span data-stu-id="fce67-391">Scalar expressions</span></span>
<span data-ttu-id="fce67-392">속성 참조뿐 아니라 SELECT 절은 상수, 산술 식, 논리 식 등의 스칼라 식도 지원합니다. 예를 들어 다음은 단순한 "Hello World" 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="fce67-393">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="fce67-394">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="fce67-395">다음은 스칼라 식을 사용하는 보다 복잡한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="fce67-396">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="fce67-397">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="fce67-398">다음 예제에서 스칼라 식의 결과는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="fce67-399">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="fce67-400">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="fce67-401">개체 및 배열 만들기</span><span class="sxs-lookup"><span data-stu-id="fce67-401">Object and array creation</span></span>
<span data-ttu-id="fce67-402">DocumentDB API SQL의 다른 주요 기능은 배열/개체 만들기입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="fce67-403">앞의 예제에서는 새 JSON 개체를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="fce67-404">마찬가지로 아래 예제에 표시된 대로 배열을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="fce67-405">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="fce67-406">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-406">**Results**</span></span>  

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

### <span data-ttu-id="fce67-407"><a id="ValueKeyword"></a>VALUE 키워드</span><span class="sxs-lookup"><span data-stu-id="fce67-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="fce67-408">**VALUE** 키워드는 JSON 값을 반환하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="fce67-409">예를 들어 아래 표시된 쿼리는 `{$1: "Hello World"}` 대신 스칼라 `"Hello World"`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="fce67-410">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="fce67-411">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="fce67-412">다음 쿼리는 `"address"` 레이블이 없는 JSON 값을 결과에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="fce67-413">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="fce67-414">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-414">**Results**</span></span>  

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

<span data-ttu-id="fce67-415">다음 예제에서는 이 코드를 확장하여 JSON 기본 값(JSON 트리 리프 수준)을 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="fce67-416">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="fce67-417">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="fce67-418">* 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-418">* Operator</span></span>
<span data-ttu-id="fce67-419">문서를 있는 그대로 프로젝션하는 특수 연산자(*)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="fce67-420">사용할 경우 프로젝션되는 유일한 필드여야</span><span class="sxs-lookup"><span data-stu-id="fce67-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="fce67-421">`SELECT * FROM Families f`와 같은 쿼리는 유효하지만 `SELECT VALUE * FROM Families f ` 및 `SELECT *, f.id FROM Families f `와 같은 쿼리는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="fce67-422">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fce67-423">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-423">**Results**</span></span>

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

### <span data-ttu-id="fce67-424"><a id="TopKeyword"></a>TOP 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="fce67-425">쿼리에서 값의 수를 제한하는 데 TOP 키워드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="fce67-426">TOP를 ORDER BY 절과 함께 사용하면 결과 집합이 정렬된 값의 처음 N개로 제한되고 그렇지 않은 경우 정의되지 않은 순서의 처음 N개 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="fce67-427">SELECT 문에서는 항상 TOP 절과 함께 ORDER BY 절을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="fce67-428">TOP의 영향을 받는 행을 예측 가능하게 나타내는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="fce67-429">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="fce67-430">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-430">**Results**</span></span>

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

<span data-ttu-id="fce67-431">위에 나와 있는 것처럼 상수 값 또는 매개 변수가 있는 쿼리를 사용하는 변수 값과 함께 TOP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="fce67-432">자세한 내용은 아래의 매개 변수가 있는 쿼리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="fce67-433"><a id="Aggregates"></a>집계 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="fce67-434">`SELECT` 절에서 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="fce67-435">집계 함수는 값 집합에서 계산을 수행하고 단일 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="fce67-436">예를 들어 다음 쿼리는 컬렉션 내에서 가족 문서의 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="fce67-437">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="fce67-438">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="fce67-439">`VALUE` 키워드를 사용하여 집계의 스칼라 값을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="fce67-440">예를 들어 다음 쿼리는 단일 숫자로 값의 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="fce67-441">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="fce67-442">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="fce67-443">필터와 함께 조합하여 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="fce67-444">예를 들어 다음 쿼리는 워싱턴 주의 주소로 문서 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="fce67-445">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="fce67-446">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="fce67-447">다음 표에서는 DocumentDB API에서 지원되는 집계 함수 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="fce67-448">`SUM` 및 `AVG`는 숫자 값에 대해 수행되는 반면 `COUNT`, `MIN` 및 `MAX`는 숫자, 문자열, 부울 및 null에 대해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="fce67-449">사용 현황</span><span class="sxs-lookup"><span data-stu-id="fce67-449">Usage</span></span> | <span data-ttu-id="fce67-450">설명</span><span class="sxs-lookup"><span data-stu-id="fce67-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="fce67-451">개수</span><span class="sxs-lookup"><span data-stu-id="fce67-451">COUNT</span></span> | <span data-ttu-id="fce67-452">식에서 항목 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="fce67-453">합계</span><span class="sxs-lookup"><span data-stu-id="fce67-453">SUM</span></span>   | <span data-ttu-id="fce67-454">식에서 모든 값의 합계를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="fce67-455">최소</span><span class="sxs-lookup"><span data-stu-id="fce67-455">MIN</span></span>   | <span data-ttu-id="fce67-456">식에서 최소값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="fce67-457">최대</span><span class="sxs-lookup"><span data-stu-id="fce67-457">MAX</span></span>   | <span data-ttu-id="fce67-458">식에서 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="fce67-459">평균</span><span class="sxs-lookup"><span data-stu-id="fce67-459">AVG</span></span>   | <span data-ttu-id="fce67-460">식에서 평균값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="fce67-461">배열 반복의 결과에 대해 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="fce67-462">자세한 내용은 [쿼리에서 배열 반복](#Iteration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="fce67-463">Azure Portal의 쿼리 탐색기를 사용하는 경우 집계 쿼리는 쿼리 페이지에 대해 부분적으로 집계된 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="fce67-464">SDK는 모든 페이지에 걸쳐 단일 누적 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="fce67-465">코드를 사용하여 집계 쿼리를 수행하기 위해 .NET SDK 1.12.0, .NET Core SDK 1.1.0 또는 Java SDK 1.9.5 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="fce67-466"><a id="OrderByClause"></a>ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="fce67-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="fce67-467">ANSI-SQL에서와 마찬가지로 쿼리하는 동안 선택적 Order By 절을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="fce67-468">절은 선택적 ASC/DESC 인수를 포함하여 결과를 검색해야 하는 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="fce67-469">예를 들어 상주하는 도시의 이름 순으로 가족을 검색하는 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="fce67-470">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="fce67-471">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-471">**Results**</span></span>

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

<span data-ttu-id="fce67-472">다음은 Epoch 시간, 즉 1970년 1월 1일부터 경과된 시간(초 단위)을 나타내는 숫자로 저장된 만든 날짜 순으로 가족을 검색하는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="fce67-473">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="fce67-474">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-474">**Results**</span></span>

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

## <span data-ttu-id="fce67-475"><a id="Advanced"></a>고급 데이터베이스 개념 및 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="fce67-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="fce67-476"><a id="Iteration"></a>반복</span><span class="sxs-lookup"><span data-stu-id="fce67-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="fce67-477">JSON 배열 반복을 지원하기 위해 DocumentDB API SQL의 **IN** 키워드를 통해 새 구문을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="fce67-478">FROM 소스에서 반복 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="fce67-479">다음 예제로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-479">Let's start with the following example:</span></span>

<span data-ttu-id="fce67-480">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="fce67-481">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-481">**Results**</span></span>  

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

<span data-ttu-id="fce67-482">이제 컬렉션의 자식을 반복하는 다른 쿼리를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="fce67-483">출력 배열의 차이점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-483">Note the difference in the output array.</span></span> <span data-ttu-id="fce67-484">이 예제에서는 `children` 을 분할하고 결과를 단일 배열로 평면화합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="fce67-485">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="fce67-486">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-486">**Results**</span></span>  

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

<span data-ttu-id="fce67-487">이 예제를 사용하여 다음 예제에 나온 대로 배열의 각 개별 항목을 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="fce67-488">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="fce67-489">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="fce67-490">배열 반복의 결과에 대해 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="fce67-491">예를 들어 다음 쿼리는 모든 가족 간의 자식 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="fce67-492">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="fce67-493">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="fce67-494"><a id="Joins"></a>조인</span><span class="sxs-lookup"><span data-stu-id="fce67-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="fce67-495">관계형 데이터베이스에서는 테이블 간 조인 요구가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="fce67-496">이는 정규화된 스키마 설계의 필연적인 논리적 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="fce67-497">이와 반대로 DocumentDB API는 스키마 없는 문서의 비정규화된 데이터 모델을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="fce67-498">이는 논리적으로 "자체 조인"과 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="fce67-499">언어가 지원하는 구문은 <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="fce67-500">대체로 이 구문은 **N** 튜플(**N**개 값이 포함된 튜플) 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="fce67-501">각 튜플은 해당 집합에 모든 컬렉션 별칭을 반복하여 생성된 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="fce67-502">즉, 조인에 참여하는 집합의 전체 교차곱입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="fce67-503">다음 예제는 JOIN 절의 작동 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="fce67-504">다음 예제에서는 소스의 각 문서와 빈 집합의 교차곱이 비어 있으므로 결과가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="fce67-505">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="fce67-506">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="fce67-507">다음 예제에서는 문서 루트와 `children` 하위 루트 간의 조인이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="fce67-508">두 JSON 개체 간의 교차곱입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="fce67-509">자식 배열인 단일 루트를 다루기 때문에 자식이 배열이라는 사실은 JOIN에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="fce67-510">따라서 각 문서와 배열의 교차곱에서 정확히 한 개의 문서만 생성하므로 결과에 두 개의 결과만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="fce67-511">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="fce67-512">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="fce67-513">다음 예제에서는 보다 기본적인 조인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="fce67-514">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="fce67-515">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-515">**Results**</span></span>

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



<span data-ttu-id="fce67-516">확인할 첫 번째 사항은 **JOIN** 절의 `from_source`가 반복기라는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="fce67-517">따라서 이 경우의 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="fce67-518">배열의 각 자식 요소 **c** 를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="fce67-519">문서 루트 **f**와 첫 번째 단계에서 평면화된 각 자식 요소 **c**의 교차곱을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="fce67-520">마지막으로, 루트 개체 **f** 의 이름 속성만 프로젝션합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="fce67-521">첫 번째 문서(`AndersenFamily`)에는 하나의 자식 요소만 포함되어 있으므로 이 문서에 해당하는 단일 개체만 결과 집합에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="fce67-522">두 번째 문서(`WakefieldFamily`)에는 두 개의 자식이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="fce67-523">따라서 교차곱을 통해 각 자식에 대한 개별 개체가 생성되므로 이 문서에 해당하는 각 자식에 하나씩, 두 개의 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="fce67-524">교차곱에서 예상한 대로 두 문서의 루트 필드는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="fce67-525">JOIN의 진정한 유용성은 다른 방식으로 프로젝션하기 어려운 모양의 교차곱에서 튜플을 형성할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="fce67-526">또한 아래 예제와 같이 사용자가 전체 튜플에서 충족되는 조건을 선택할 수 있도록 튜플 조합을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="fce67-527">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="fce67-528">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-528">**Results**</span></span>

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



<span data-ttu-id="fce67-529">이 예제는 이전 예제의 일반 확장이며 이중 조인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="fce67-530">따라서 교차곱을 다음 의사 코드로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

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

<span data-ttu-id="fce67-531">`AndersenFamily`에는 애완 동물 한 마리를 키우는 자식 한 명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="fce67-532">따라서 이 가족의 교차곱은 하나의 행(1\*1\*1)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="fce67-533">그러나 WakefieldFamily에는 자녀 두 명이 있지만 그 중에 "Jesse"만 애완 동물을</span><span class="sxs-lookup"><span data-stu-id="fce67-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="fce67-534">두 마리 키우고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-534">Jesse has two pets though.</span></span> <span data-ttu-id="fce67-535">따라서 이 가족의 교차곱은 1\*1\*2 = 2개의 행을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="fce67-536">다음 예제에서는 `pet`에 대한 추가 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="fce67-537">이 필터는 애완 동물 이름이 "Shadow"가 아닌 튜플을 모두 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="fce67-538">배열에서 튜플을 작성하고, 튜플 요소를 필터링한 다음 요소 조합을 프로젝션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="fce67-539">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="fce67-540">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="fce67-541"><a id="JavaScriptIntegration"></a>JavaScript 통합</span><span class="sxs-lookup"><span data-stu-id="fce67-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="fce67-542">Azure Cosmos DB는 저장 프로시저 및 트리거 측면에서 컬렉션에 대해 직접 JavaScript 기반 응용 프로그램 논리를 실행하기 위한 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="fce67-543">이 경우 다음 두 가지 기능을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-543">This allows for both:</span></span>

* <span data-ttu-id="fce67-544">데이터베이스 엔진 내에 직접 JavaScript 런타임이 전체 통합되므로 컬렉션의 문서에 대해 고성능 트랜잭션 CRUD 작업 및 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="fce67-545">데이터베이스 트랜잭션을 사용하여 제어 흐름, 변수 범위 지정 및 예외 처리 기본 형식의 할당과 통합을 기본적으로 모델링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="fce67-546">Azure Cosmos DB의 JavaScript 통합 지원에 대한 자세한 내용은 JavaScript 서버 쪽 프로그래밍 기능 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="fce67-547"><a id="UserDefinedFunctions"></a>UDF(사용자 정의 함수)</span><span class="sxs-lookup"><span data-stu-id="fce67-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="fce67-548">이 문서에 이미 정의되어 있는 형식과 더불어 DocumentDB API SQL은 UDF(사용자 정의 함수)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="fce67-549">특히 개발자가 0개 또는 많은 인수를 전달하고 단일 인수 결과를 반환할 수 있는 스칼라 UDF가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="fce67-550">이러한 각 인수가 유효한 JSON 값인지 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="fce67-551">이러한 사용자 정의 함수를 사용한 사용자 지정 응용 프로그램 논리를 지원하기 위해 DocumentDB API SQL 구문이 확장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="fce67-552">UDF를 DocumentDB API에 등록한 다음 SQL 쿼리의 일부로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="fce67-553">실제로 UDF는 쿼리에서 호출되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="fce67-554">이 선택의 필연적인 결과로 UDF는 다른 JavaScript 형식(저장 프로시저 및 트리거)과 달리 컨텍스트 개체에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="fce67-555">쿼리는 읽기 전용으로 실행되므로 주 복제본 또는 보조 복제본에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="fce67-556">따라서 UDF는 다른 JavaScript 형식과 달리 보조 복제본에서 실행되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="fce67-557">다음은 Cosmos DB 데이터베이스의 문서 컬렉션 아래에 UDF를 등록할 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="fce67-558">위 예제에서는 이름이 `REGEX_MATCH`인 UDF를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="fce67-559">두 JSON 문자열 값 `input` and `pattern` 을 받아들이고 JavaScript의 string.match() 함수를 사용하여 첫 번째 값이 두 번째 값에 지정된 패턴과 일치하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="fce67-560">이제 이 UDF를 프로젝트의 쿼리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="fce67-561">쿼리 내에서 호출하는 경우 대/소문자를 구분하는 접두사 "udf."를 사용하여</span><span class="sxs-lookup"><span data-stu-id="fce67-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="fce67-562">UDF를 한정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="fce67-563">2015년 3월 17일 이전에는 Cosmos DB가 SELECT REGEX_MATCH()와 같이 "udf." 접두사가 없는</span><span class="sxs-lookup"><span data-stu-id="fce67-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="fce67-564">UDF 호출을 지원했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="fce67-565">이 호출 패턴은 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="fce67-566">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="fce67-567">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="fce67-568">아래 예제와 같이 "udf." 접두사로 한정된 UDF를 필터 내부에 사용할 수도</span><span class="sxs-lookup"><span data-stu-id="fce67-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="fce67-569">있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-569">prefix:</span></span>

<span data-ttu-id="fce67-570">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="fce67-571">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="fce67-572">기본적으로 UDF는 유효한 스칼라 식이며 프로젝션과 필터 둘 다에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="fce67-573">UDF 기능을 확장하기 위해 조건부 논리가 포함된 다른 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="fce67-574">다음은 UDF를 실행하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="fce67-575">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="fce67-576">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-576">**Results**</span></span>

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


<span data-ttu-id="fce67-577">앞의 예제에서 소개한 대로 UDF는 JavaScript 언어 기능과 DocumentDB API SQL을 통합하여 내장된 JavaScript 런타임 기능을 통해 복잡한 절차적 조건부 논리를 수행하는 풍부한 프로그래밍 가능 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="fce67-578">DocumentDB API SQL은 현재 UDF 처리 단계(WHERE 절 또는 SELECT 절)에 있는 각 원본 문서에 대한 인수를 UDF에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="fce67-579">결과는 전체 실행 파이프라인에 매끄럽게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="fce67-580">UDF 매개 변수가 참조하는 속성을 JSON 값에 사용할 수 없는 경우 매개 변수가 undefined로 간주되므로 전체 UDF 호출을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="fce67-581">마찬가지로, UDF 결과가 undefined이면 결과에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="fce67-582">요약하면 UDF는 쿼리의 일부로 복잡한 비즈니스 논리를 수행하는 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="fce67-583">연산자 평가</span><span class="sxs-lookup"><span data-stu-id="fce67-583">Operator evaluation</span></span>
<span data-ttu-id="fce67-584">Cosmos DB는 JSON 데이터베이스이므로 JavaScript 연산자 및 평가 의미 체계와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="fce67-585">Cosmos DB는 JSON 지원 측면에서 JavaScript 의미 체계를 유지하려고 하지만 연산 평가가 다른 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="fce67-586">DocumentDB API SQL에서는 기존 SQL과 달리 데이터베이스에서 값이 검색될 때까지 값의 형식을 알 수 없는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="fce67-587">쿼리를 효율적으로 실행하기 위해 대부분의 연산자에 강력한 형식 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="fce67-588">DocumentDB API SQL은 JavaScript와 달리 암시적 변환을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="fce67-589">예를 들어 `SELECT * FROM Person p WHERE p.Age = 21`과 같은 쿼리는 Age 속성을 포함하고 값이 21인 문서에 일치됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="fce67-590">Age 속성이 문자열 "21" 또는 "021", "21.0", "0021", "00021" 등의 다른 무한 변형과 일치하는 다른 문서는 일치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="fce67-591">이는 문자열 값이 암시적으로 숫자로 캐스팅되는 JavaScript와 대조됩니다(연산자 기준, 예: ==)</span><span class="sxs-lookup"><span data-stu-id="fce67-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="fce67-592">이 선택 항목은 DocumentDB API SQL의 효율적인 인덱스 매핑에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="fce67-593">매개 변수가 있는 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="fce67-593">Parameterized SQL queries</span></span>
<span data-ttu-id="fce67-594">Cosmos DB는 익숙한 @ 표기법으로 표현된 매개 변수가 있는 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="fce67-595">매개 변수가 있는 SQL은 사용자 입력의 강력한 처리 및 이스케이프를 제공하여 SQL 주입을 통해 데이터가 실수로 노출되는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="fce67-596">예를 들어 성 및 주소 상태를 매개 변수로 사용하는 쿼리를 작성한 다음 사용자 입력에 따라 다양한 성 및 주소 상태 값에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="fce67-597">그런 다음 아래와 같이 이 요청을 매개 변수가 있는 JSON 쿼리로 Cosmos DB에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="fce67-598">아래와 같이 매개 변수가 있는 쿼리를 사용하여 TOP에 대한 인수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="fce67-599">매개 변수 값은 유효한 모든 JSON(문자열, 숫자, 부울, null, 짝수 배열 또는 중첩된 JSON)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="fce67-600">또한 Cosmos DB는 스키마가 없으므로 모든 형식에 대해 매개 변수의 유효성이 검사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="fce67-601"><a id="BuiltinFunctions"></a>기본 제공 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="fce67-602">Cosmos DB는 일반적인 작업을 위해 많은 기본 제공 함수도 지원하며, UDF(사용자 정의 함수)처럼 쿼리 내에서 이러한 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="fce67-603">함수 그룹</span><span class="sxs-lookup"><span data-stu-id="fce67-603">Function group</span></span>          | <span data-ttu-id="fce67-604">작업</span><span class="sxs-lookup"><span data-stu-id="fce67-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fce67-605">수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-605">Mathematical functions</span></span>  | <span data-ttu-id="fce67-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN 및 TAN</span><span class="sxs-lookup"><span data-stu-id="fce67-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="fce67-607">형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-607">Type checking functions</span></span> | <span data-ttu-id="fce67-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED 및 IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="fce67-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="fce67-609">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-609">String functions</span></span>        | <span data-ttu-id="fce67-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING 및 UPPER</span><span class="sxs-lookup"><span data-stu-id="fce67-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="fce67-611">배열 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-611">Array functions</span></span>         | <span data-ttu-id="fce67-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH 및 ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="fce67-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="fce67-613">공간 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-613">Spatial functions</span></span>       | <span data-ttu-id="fce67-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID 및 ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="fce67-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="fce67-615">현재 기본 제공 함수가 제공되는 UDF(사용자 정의 함수)를 사용 중인 경우 더 빨리 실행되고 더 효율적이므로 해당하는 기본 제공 함수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="fce67-616">수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-616">Mathematical functions</span></span>
<span data-ttu-id="fce67-617">수치 연산 함수는 각각 인수로 제공된 입력 값에 따라 계산을 수행하고 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="fce67-618">다음은 지원되는 기본 제공 수치 연산 함수 표입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="fce67-619">사용 현황</span><span class="sxs-lookup"><span data-stu-id="fce67-619">Usage</span></span> | <span data-ttu-id="fce67-620">설명</span><span class="sxs-lookup"><span data-stu-id="fce67-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fce67-621">[[ABS(num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="fce67-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="fce67-622">지정한 숫자 식의 절대(양수) 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-623">CEILING(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="fce67-624">지정한 숫자 식보다 크거나 같은 가장 작은 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-625">FLOOR(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="fce67-626">지정한 숫자 식보다 작거나 같은 가장 큰 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-627">EXP(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="fce67-628">지정한 숫자 식의 지수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="fce67-629">[LOG(num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="fce67-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="fce67-630">지정한 숫자 식의 자연 로그 또는 지정한 밑을 사용하는 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="fce67-631">LOG10(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="fce67-632">지정한 숫자 식의 상용 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-633">ROUND(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="fce67-634">가장 가까운 정수 값으로 반올림한 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="fce67-635">TRUNC(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="fce67-636">가장 가까운 정수 값으로 버린 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="fce67-637">SQRT(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="fce67-638">지정한 숫자 식의 제곱근을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-639">SQUARE(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="fce67-640">지정한 숫자 식의 거듭제곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-641">POWER(num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="fce67-642">지정한 값까지 지정한 숫자 식의 거듭제곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="fce67-643">SIGN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="fce67-644">지정한 숫자 식의 부호 값(-1, 0, 1)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-645">ACOS(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="fce67-646">코사인 값이 지정된 숫자 식인 라디안에서 각도를 반환합니다. 아크코사인이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="fce67-647">ASIN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="fce67-648">사인 값이 지정된 숫자 식인 라디안에서 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="fce67-649">아크사인이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="fce67-650">ATAN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="fce67-651">탄젠트 값이 지정된 숫자 식인 라디안에서 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="fce67-652">아크탄젠트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="fce67-653">ATN2(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="fce67-654">x와 y가 두 지정된 float 식의 값인 양의 x축과 원점부터 (y, x) 지점의 선 사이의 라디안에서 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="fce67-655">COS(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="fce67-656">지정된 식의 라디안에서 지정된 각도의 삼각 코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="fce67-657">COT(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="fce67-658">지정된 숫자 식의 라디안에서 지정된 각도의 삼각 코탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="fce67-659">DEGREES(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="fce67-660">라디안에서 지정된 각도로 해당하는 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="fce67-661">PI()</span><span class="sxs-lookup"><span data-stu-id="fce67-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="fce67-662">PI의 상수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="fce67-663">RADIANS(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="fce67-664">숫자 식을 단위로 입력하면 라디안을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="fce67-665">SIN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="fce67-666">지정된 식의 라디안에서 지정된 각도의 삼각 사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="fce67-667">TAN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="fce67-668">지정된 식에서 입력 식의 탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="fce67-669">예를 들어 이제 다음과 같은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="fce67-670">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="fce67-671">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-671">**Results**</span></span>

    [4]

<span data-ttu-id="fce67-672">Cosmos DB 함수와 ANSI SQL 간의 주요 차이점은 스키마가 없는 데이터 및 혼합된 스키마 데이터에서 잘 작동하도록 설계되었다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="fce67-673">예를 들어 Size 속성이 없거나 "unknown"과 같은 숫자가 아닌 값을 가진 문서가 있는 경우 오류를 반환하는 대신 문서를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="fce67-674">형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-674">Type checking functions</span></span>
<span data-ttu-id="fce67-675">형식 검사 함수를 통해 SQL 쿼리 내에서 식의 형식을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="fce67-676">형식 검사 함수를 사용하여 변수이거나 알 수 없는 경우 문서 내의 속성 형식을 즉시 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="fce67-677">다음은 지원되는 기본 제공 형식 검사 함수 표입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="fce67-678"><strong>사용 현황</strong></span><span class="sxs-lookup"><span data-stu-id="fce67-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="fce67-679"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="fce67-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-681">값의 형식이 배열인지 여부를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-683">값의 형식이 부울인지 여부를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-685">값의 형식이 null인지 여부를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-687">값의 형식이 숫자인지 여부를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-689">값의 형식이 JSON 개체인지 여부를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-691">값의 형식이 문자열인지 여부를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-693">속성이 값을 할당할지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fce67-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="fce67-695">문자열, 숫자, 부울 또는 null 값의 형식인지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="fce67-696">이러한 함수를 사용하여 이제 다음과 같은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="fce67-697">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="fce67-698">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="fce67-699">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-699">String functions</span></span>
<span data-ttu-id="fce67-700">다음 스칼라 함수는 문자열 입력 값에 대해 작업을 수행하고 문자열, 숫자 또는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="fce67-701">기본 제공 문자열 함수의 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="fce67-702">사용 현황</span><span class="sxs-lookup"><span data-stu-id="fce67-702">Usage</span></span> | <span data-ttu-id="fce67-703">설명</span><span class="sxs-lookup"><span data-stu-id="fce67-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fce67-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="fce67-705">지정한 문자열 식의 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="fce67-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="fce67-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="fce67-707">둘 이상의 문자열 값을 연결한 결과인 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="fce67-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="fce67-709">문자열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="fce67-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="fce67-711">첫 번째 문자열 식이 두 번째로 끝나지를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="fce67-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="fce67-713">첫 번째 문자열 식이 두 번째로 끝나지를 나타내는 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="fce67-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="fce67-715">첫 번째 문자열 식이 두 번째를 포함하는지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="fce67-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="fce67-717">지정된 첫 번째 문자열 식 내의 두 번째 문자열 식에서 첫 번째로 나타나는 시작 위치를 반환하거나 문자열을 찾을 수 없는 경우 -1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="fce67-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="fce67-719">지정된 수의 문자로 문자열의 왼쪽 부분을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="fce67-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="fce67-721">지정된 수의 문자로 문자열의 오른쪽 부분을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="fce67-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="fce67-723">선행 공백을 제거한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="fce67-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="fce67-725">후행 공백을 잘라낸 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="fce67-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="fce67-727">대문자 데이터를 소문자로 변환한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="fce67-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="fce67-729">소문자 데이터를 대문자로 변환한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="fce67-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="fce67-731">지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="fce67-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="fce67-733">문자열 값을 지정한 횟수 만큼 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="fce67-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="fce67-735">문자열 값의 순서와 반대로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="fce67-736">이제 이러한 함수를 사용하여 다음과 같은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="fce67-737">예를 들어 다음과 같이 대문자로 제품군 이름을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="fce67-738">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="fce67-739">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="fce67-740">또는 이 예제와 같이 문자열을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="fce67-741">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="fce67-742">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="fce67-743">또한 다음 예제와 같이 결과를 필터링하려면 WHERE 절에 문자열 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="fce67-744">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="fce67-745">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="fce67-746">배열 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-746">Array functions</span></span>
<span data-ttu-id="fce67-747">다음 스칼라 함수는 배열 입력 값에 대해 작업을 수행하고 숫자, 부울, 또는 배열 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="fce67-748">기본 제공 배열 함수의 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="fce67-749">사용 현황</span><span class="sxs-lookup"><span data-stu-id="fce67-749">Usage</span></span> | <span data-ttu-id="fce67-750">설명</span><span class="sxs-lookup"><span data-stu-id="fce67-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fce67-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="fce67-752">지정된 배열 식의 요소 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="fce67-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="fce67-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="fce67-754">둘 이상의 배열 값을 연결한 결과인 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="fce67-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="fce67-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="fce67-756">지정된 값이 배열에 포함되는지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="fce67-757">전체 또는 부분 일치 항목인지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="fce67-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="fce67-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="fce67-759">배열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="fce67-760">배열 함수는 JSON 내 배열을 조작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="fce67-761">예를 들어 다음은 부모 중 한 사람이 "Robin Wakefield"인 모든 문서를 반환하는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="fce67-762">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="fce67-763">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="fce67-764">배열 내의 요소와 일치하는 부분 조각을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="fce67-765">다음 쿼리는 `givenName`이 `Robin`인 모든 부모를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="fce67-766">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="fce67-767">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="fce67-768">제품군 당 자녀 수를 가져오는 ARRAY_LENGTH를 사용하는 다른 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="fce67-769">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="fce67-770">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="fce67-771">공간 함수</span><span class="sxs-lookup"><span data-stu-id="fce67-771">Spatial functions</span></span>
<span data-ttu-id="fce67-772">Cosmos DB는 지리 공간 쿼리를 위해 다음과 같은 OGC(Open Geospatial Consortium) 기본 제공 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="fce67-773"><strong>사용 현황</strong></span><span class="sxs-lookup"><span data-stu-id="fce67-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="fce67-774"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="fce67-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="fce67-776">두 GeoJSON Point, Polygon 또는 LineString 식 사이의 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="fce67-778">첫 번째 GeoJSON 개체(Point, Polygon 또는 LineString)가 두 번째 GeoJSON 개체(Point, Polygon 또는 LineString) 내에 있는지를 나타내는 부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-779">ST_INTERSECTS(spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="fce67-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="fce67-780">지정한 두 GeoJSON 개체(Point, Polygon 또는 LineString)가 교차하는지 여부를 나타내는 부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="fce67-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="fce67-782">지정된 GeoJSON Point, Polygon 또는 LineString 식이 유효한지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fce67-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="fce67-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="fce67-784">지정된 GeoJSON Point, Polygon 또는 LineString 식이 유효한 경우 부울 값을 포함하는 JSON 값을 반환하고, 잘못된 경우 추가로 그 이유를 문자열 값으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="fce67-785">공간 함수를 사용하여 공간 데이터에 대한 근접 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="fce67-786">예를 들어 ST_DISTANCE 기본 제공 함수를 사용하여 지정된 위치에서 30km 이내에 있는 모든 제품군 문서를 반환하는 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="fce67-787">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="fce67-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="fce67-788">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="fce67-789">Cosmos DB의 지리 공간 지원에 대한 자세한 내용은 [Azure Cosmos DB에서 지리 공간 데이터 작업](geospatial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="fce67-790">공간 함수 및 Cosmos DB에 대한 SQL 구문을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="fce67-791">이제 지금까지 나타난 LINQ 쿼리 작동 방법 및 구문 조작 방법을 살펴봤습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="fce67-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="fce67-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="fce67-793">LINQ는 개체 스트림에 대한 쿼리로 계산을 표현하는 .NET 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="fce67-794">Cosmos DB는 JSON 및 .NET 개체 간의 변환과 LINQ 쿼리 하위 집합에서 Cosmos DB 쿼리로의 매핑을 용이하게 하여 LINQ와 인터페이스할 클라이언트 쪽 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="fce67-795">아래 그림은 Cosmos DB를 사용한 LINQ 쿼리를 지원하는 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="fce67-796">개발자는 Cosmos DB 클라이언트를 사용하여 Cosmos DB 쿼리 공급자를 직접 쿼리하는 **IQueryable** 개체를 만들 수 있습니다. 그런 후에 쿼리 공급자가 LINQ 쿼리를 Cosmos DB 쿼리로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="fce67-797">그런 다음 JSON 형식으로 결과 집합을 검색하기 위해 쿼리가 Cosmos DB 서버로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="fce67-798">반환된 결과는 클라이언트 쪽에서 .NET 개체 스트림으로 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![DocumentDB API를 사용한 LINQ 쿼리를 지원하는 아키텍처 - SQL 구문, JSON 쿼리 언어, 데이터베이스 개념 및 SQL 쿼리][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="fce67-800">.NET 및 JSON 매핑</span><span class="sxs-lookup"><span data-stu-id="fce67-800">.NET and JSON mapping</span></span>
<span data-ttu-id="fce67-801">.NET 개체와 JSON 문서 간의 매핑은 기본적으로 수행됩니다. 각 데이터 멤버 필드가 JSON 개체에 매핑됩니다. 여기서 필드 이름은 개체의 "키" 부분에 매핑되고 "값" 부분은 개체의 값 부분에 재귀적으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="fce67-802">다음 예제를 고려해 보세요. 만들어진 Family 개체는 아래와 같이 JSON 문서에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="fce67-803">반대로 JSON 문서는 다시 .NET 개체에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="fce67-804">**C# 클래스**</span><span class="sxs-lookup"><span data-stu-id="fce67-804">**C# Class**</span></span>

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


<span data-ttu-id="fce67-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="fce67-805">**JSON**</span></span>  

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



### <a name="linq-to-sql-translation"></a><span data-ttu-id="fce67-806">LINQ to SQL 변환</span><span class="sxs-lookup"><span data-stu-id="fce67-806">LINQ to SQL translation</span></span>
<span data-ttu-id="fce67-807">Cosmos DB 쿼리 공급자는 LINQ 쿼리에서 Cosmos DB SQL 쿼리로 매핑하기 위해 최대한 노력합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="fce67-808">다음 설명에서는 사용자가 LINQ의 기본 사항을 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="fce67-809">먼저 형식 시스템에 대해 모든 JSON 기본 형식(숫자 형식, 부울, 문자열 및 null)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="fce67-810">이러한 JSON 형식만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-810">Only these JSON types are supported.</span></span> <span data-ttu-id="fce67-811">다음 스칼라 식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="fce67-812">상수 값 – 쿼리가 평가될 때 기본 데이터 형식의 상수 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="fce67-813">속성/배열 인덱스 식 – 이러한 식은 개체 또는 배열 요소의 속성을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="fce67-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span><span class="sxs-lookup"><span data-stu-id="fce67-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="fce67-815">산술 식 - 숫자 및 부울 값에 대한 일반 산술 식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="fce67-816">전체 목록은 SQL 사양을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="fce67-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="fce67-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="fce67-818">문자열 비교 식 - 문자열 값과 상수 문자열 값 비교를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="fce67-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span><span class="sxs-lookup"><span data-stu-id="fce67-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="fce67-820">개체/배열 만들기 식 - 복합 값 형식 또는 무명 형식의 개체나 이러한 개체의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="fce67-821">해당 값을 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-821">These values can be nested.</span></span>
  
     <span data-ttu-id="fce67-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span><span class="sxs-lookup"><span data-stu-id="fce67-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="fce67-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="fce67-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="fce67-824"><a id="SupportedLinqOperators"></a>지원되는 LINQ 연산자 목록</span><span class="sxs-lookup"><span data-stu-id="fce67-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="fce67-825">다음은 DocumentDB .NET SDK에 포함된 LINQ 공급자에서 지원되는 LINQ 연산자의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="fce67-826">**Select**: 프로젝션이 개체 생성을 포함하는 SQL SELECT로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="fce67-827">**Where**: 필터가 SQL WHERE로 변환하고 && , || 및 !</span><span class="sxs-lookup"><span data-stu-id="fce67-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="fce67-828">간의 SQL 연산자로 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-828">to the SQL operators</span></span>
* <span data-ttu-id="fce67-829">**SelectMany**: SQL JOIN 절에 대한 배열 해제를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="fce67-830">배열 요소를 필터링하는 데 체인/중첩 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="fce67-831">**OrderBy 및 OrderByDescending**: ORDER BY 오름차순/내림차순으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="fce67-832">집계를 위한 **Count**, **Sum**, **Min**, **Max** 및 **Average** 연산자와 해당 비동기 동급 연산자 **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** 및 **AverageAsync**</span><span class="sxs-lookup"><span data-stu-id="fce67-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="fce67-833">**CompareTo**: 범위 비교로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="fce67-834">.NET에서 비교 불가능하므로 문자열에 대해 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="fce67-835">**Take**: 쿼리에서 결과를 제한하기 위해 SQL TOP으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="fce67-836">**수치 연산 함수**: NET의 Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate를 해당하는 SQL 기본 제공 함수로의 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fce67-837">**문자열 함수**: .NET의 Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper를 해당하는 SQL 기본 제공 함수로의 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fce67-838">**배열 함수**: .NET의 oncat, Contains 및 Count를 해당하는 SQL 기본 제공 함수로의 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fce67-839">**지리 공간 확장 함수**: 스텁 메서드 Distance, Within, IsValid 및 IsValidDetailed에서 해당하는 SQL 기본 제공 함수로의 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fce67-840">**사용자 정의 함수 확장 함수**: 스텁 메서드 UserDefinedFunctionProvider.Invoke에서 해당하는 사용자 정의 함수로의 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="fce67-841">**기타**: coalesce 및 조건부 연산자의 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="fce67-842">컨텍스트에 따라 Contains는 문자열 CONTAINS, ARRAY_CONTAINS 또는 SQL IN으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="fce67-843">SQL 쿼리 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-843">SQL query operators</span></span>
<span data-ttu-id="fce67-844">다음은 표준 LINQ 쿼리 연산자 중 일부가 Cosmos DB 쿼리로 변환되는 방식을 보여 주는 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="fce67-845">Select 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-845">Select Operator</span></span>
<span data-ttu-id="fce67-846">구문은 `input.Select(x => f(x))`입니다. 여기서 `f`는 스칼라 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="fce67-847">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="fce67-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="fce67-849">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="fce67-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="fce67-851">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="fce67-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="fce67-853">SelectMany 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-853">SelectMany operator</span></span>
<span data-ttu-id="fce67-854">구문은 `input.SelectMany(x => f(x))`입니다. 여기서 `f`는 컬렉션 형식을 반환하는 스칼라 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="fce67-855">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="fce67-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="fce67-857">Where 연산자</span><span class="sxs-lookup"><span data-stu-id="fce67-857">Where operator</span></span>
<span data-ttu-id="fce67-858">구문은 `input.Where(x => f(x))`입니다. 여기서 `f`는 부울 값을 반환하는 스칼라 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="fce67-859">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="fce67-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="fce67-861">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="fce67-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="fce67-863">복합 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="fce67-863">Composite SQL queries</span></span>
<span data-ttu-id="fce67-864">위 연산자를 구성하여 보다 강력한 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="fce67-865">Cosmos DB는 중첩된 컬렉션을 지원하므로 해당 컴퍼지션을 연결하거나 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="fce67-866">연결</span><span class="sxs-lookup"><span data-stu-id="fce67-866">Concatenation</span></span>
<span data-ttu-id="fce67-867">구문은 `input(.|.SelectMany())(.Select()|.Where())*`입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="fce67-868">연결된 쿼리는 선택적 `SelectMany` 쿼리로 시작하며 그 뒤에 여러 `Select` 또는 `Where` 연산자가 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="fce67-869">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="fce67-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="fce67-871">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="fce67-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="fce67-873">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="fce67-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="fce67-875">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="fce67-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="fce67-877">중첩</span><span class="sxs-lookup"><span data-stu-id="fce67-877">Nesting</span></span>
<span data-ttu-id="fce67-878">구문은 `input.SelectMany(x=>x.Q())`입니다. 여기서 Q는 `Select`, `SelectMany` 또는 `Where` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="fce67-879">중첩 쿼리에서는 외부 컬렉션의 각 요소에 내부 쿼리가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="fce67-880">한 가지 중요한 기능은 자체 조인처럼 내부 쿼리가 외부 컬렉션의 요소 필드를 참조할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="fce67-881">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="fce67-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="fce67-883">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="fce67-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="fce67-885">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="fce67-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="fce67-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fce67-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="fce67-887"><a id="ExecutingSqlQueries"></a>SQL 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="fce67-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="fce67-888">Cosmos DB는 HTTP/HTTPS 요청을 수행할 수 있는 임의의 언어로 호출할 수 있는 REST API를 통해 리소스를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="fce67-889">또한 Cosmos DB는 .NET, Node.js, JavaScript, Python 등 많이 사용되는 여러 언어를 위한 프로그래밍 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="fce67-890">REST API 및 다양한 라이브러리가 모두 SQL을 통한 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="fce67-891">.NET SDK는 SQL뿐 아니라 LINQ 쿼리도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="fce67-892">다음 예제에서는 쿼리를 만들고 Cosmos DB 데이터베이스 계정에 대해 제출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="fce67-893"><a id="RestAPI"></a>REST API</span><span class="sxs-lookup"><span data-stu-id="fce67-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="fce67-894">Cosmos DB는 HTTP를 통해 개방형 RESTful 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="fce67-895">Azure 구독을 사용하여 데이터베이스 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="fce67-896">Cosmos DB 리소스 모델은 단일 데이터베이스 계정 아래에 있으며 각각 논리적이고 안정적인 URI를 사용하여 주소를 지정할 수 있는 리소스 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="fce67-897">이 문서에서는 리소스 집합을 피드라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="fce67-898">데이터베이스 계정은 각각 여러 컬렉션을 포함하는 데이터베이스 집합으로 구성되고, 각 컬렉션에는 문서, UDF 및 기타 리소스 유형이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="fce67-899">이러한 리소스를 사용한 기본 조작 모델은 HTTP 동사인 GET, PUT, POST 및 DELETE와 표준 해석을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="fce67-900">POST 동사는 새 리소스를 만들거나 저장 프로시저를 실행하거나 Cosmos DB 쿼리를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="fce67-901">쿼리는 항상 파생 작업이 없는 읽기 전용 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="fce67-902">다음 예제에서는 지금까지 검토한 두 개의 샘플 문서가 포함된 컬렉션에 대한 DocumentDB API 쿼리의 POST를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="fce67-903">이 쿼리는 JSON 이름 속성에 단순한 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="fce67-904">`x-ms-documentdb-isquery` 및 Content-Type: `application/query+json` 헤더를 사용하여 작업이 쿼리임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="fce67-905">**요청**</span><span class="sxs-lookup"><span data-stu-id="fce67-905">**Request**</span></span>

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


<span data-ttu-id="fce67-906">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-906">**Results**</span></span>

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


<span data-ttu-id="fce67-907">두 번째 예제에서는 조인의 여러 결과를 반환하는 보다 복잡한 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="fce67-908">**요청**</span><span class="sxs-lookup"><span data-stu-id="fce67-908">**Request**</span></span>

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


<span data-ttu-id="fce67-909">**결과**</span><span class="sxs-lookup"><span data-stu-id="fce67-909">**Results**</span></span>

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


<span data-ttu-id="fce67-910">쿼리 결과가 단일 결과 페이지에 모두 들어가지 않는 경우 REST API에서 `x-ms-continuation-token` 응답 헤더를 통해 연속 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="fce67-911">클라이언트는 후속 결과에 헤더를 포함하여 결과에 페이지를 매길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="fce67-912">`x-ms-max-item-count` 숫자 헤더를 통해 페이지당 결과 수를 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="fce67-913">지정된 쿼리에 `COUNT`와 같은 집계 함수가 있는 경우 쿼리 페이지는 결과 페이지에 대해 부분적으로 집계된 값을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="fce67-914">클라이언트는 최종 결과(예: 총 개수를 반환하는 개별 페이지에서 반환된 개수에 대한 합계)를 생성하는 이러한 결과에 대해 두 번째 수준 집계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="fce67-915">쿼리에 대한 데이터 일관성 정책을 관리하려면 모든 REST API 요청처럼 `x-ms-consistency-level` 헤더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="fce67-916">세션 일관성을 사용하려면 쿼리 요청에 최신 `x-ms-session-token` 쿠키 헤더도 에코해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="fce67-917">쿼리된 컬렉션의 인덱싱 정책이 쿼리 결과의 일관성에 영향을 줄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="fce67-918">컬렉션에 기본 인덱싱 정책 설정을 사용할 경우 인덱스가 항상 문서 콘텐츠로 최신 상태를 유지하며 쿼리 결과가 데이터에 대해 선택한 일관성과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="fce67-919">인덱싱 정책을 지연으로 완화하면 쿼리에서 오래된 결과가 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="fce67-920">자세한 내용은 [Azure Cosmos DB 일관성 수준][consistency-levels]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="fce67-921">컬렉션에 구성된 인덱싱 정책이 지정된 쿼리를 지원할 수 없는 경우 Azure Cosmos DB 서버에서 400 "잘못된 요청"이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="fce67-922">해시(같음) 조회에 구성된 경로 및 인덱싱에서 명시적으로 제외된 경로의 범위 쿼리에 대해 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="fce67-923">인덱스를 사용할 수 없는 경우 쿼리에서 스캔을 수행할 수 있도록 `x-ms-documentdb-query-enable-scan` 헤더를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="fce67-924">`x-ms-documentdb-populatequerymetrics` 헤더를 `True`로 설정하여 쿼리 실행에 대한 자세한 메트릭을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="fce67-925">자세한 내용은 [Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리 메트릭](documentdb-sql-query-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="fce67-926"><a id="DotNetSdk"></a>C#(.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="fce67-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="fce67-927">.NET SDK는 LINQ 및 SQL 쿼리를 둘 다 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="fce67-928">다음 예제에서는 이 문서의 앞부분에서 소개한 단순한 필터 쿼리를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="fce67-929">이 샘플은 각 문서 내에서 두 속성이 같은지 비교하고 익명 프로젝션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="fce67-930">다음 샘플은 LINQ SelectMany를 통해 표현된 조인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="fce67-931">.NET 클라이언트는 위에 표시된 대로 foreach 블록에서 쿼리 결과의 모든 페이지를 자동으로 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="fce67-932">REST API 섹션에서 소개한 쿼리 옵션은 CreateDocumentQuery 메서드의 `FeedOptions` and `FeedResponse` 클래스를 통해 .NET SDK에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="fce67-933">페이지 수는 `MaxItemCount` 설정을 사용하여 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="fce67-934">또한 `IQueryable` 개체를 사용하여 `IDocumentQueryable`을 만든 다음 ` ResponseContinuationToken` 값을 읽고 `FeedOptions`에서 다시 `RequestContinuationToken`으로 전달하여 페이징을 명시적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="fce67-935">`EnableScanInQuery` 를 설정하여 구성된 인덱싱 정책이 쿼리를 지원할 수 없는 경우 스캔을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="fce67-936">분할된 컬렉션의 경우 `PartitionKey`을 사용하여 단일 파티션에 대해 쿼리를 실행할 수 있고(Cosmos DB가 쿼리 텍스트에서 이를 자동으로 추출할 수 있음) `EnableCrossPartitionQuery`를 사용하여 여러 파티션에 대해 실행되어야 하는 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="fce67-937">쿼리가 포함된 추가 샘플은 [Azure Cosmos DB .NET 샘플](https://github.com/Azure/azure-documentdb-net)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fce67-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="fce67-938"><a id="JavaScriptServerSideApi"></a>JavaScript 서버 쪽 API</span><span class="sxs-lookup"><span data-stu-id="fce67-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="fce67-939">Cosmos DB는 저장 프로시저 및 트리거를 사용하여 컬렉션에 대해 직접 JavaScript 기반 응용 프로그램 논리를 실행하기 위한 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="fce67-940">그런 다음 컬렉션 수준에서 등록된 JavaScript 논리가 지정된 컬렉션의 문서에 대해 데이터베이스 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="fce67-941">해당 작업은 앰비언트 ACID 트랜잭션에 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="fce67-942">다음 예제에서는 JavaScript 서버 API에서 queryDocuments를 사용하여 저장 프로시저와 트리거 내부에서 쿼리를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce67-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

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

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="fce67-943"><a id="References"></a>참조</span><span class="sxs-lookup"><span data-stu-id="fce67-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="fce67-944">[Azure Cosmos DB 소개][introduction]</span><span class="sxs-lookup"><span data-stu-id="fce67-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="fce67-945">Azure Cosmos DB SQL 사양</span><span class="sxs-lookup"><span data-stu-id="fce67-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="fce67-946">Azure Cosmos DB .NET 샘플</span><span class="sxs-lookup"><span data-stu-id="fce67-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="fce67-947">[Azure Cosmos DB 일관성 수준][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="fce67-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="fce67-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="fce67-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="fce67-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="fce67-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="fce67-950">Javascript 사양 [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="fce67-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="fce67-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="fce67-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="fce67-952">대형 데이터베이스에 대한 쿼리 평가 기술 [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="fce67-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="fce67-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="fce67-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="fce67-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="fce67-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="fce67-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="fce67-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="fce67-956">G.</span><span class="sxs-lookup"><span data-stu-id="fce67-956">G.</span></span> <span data-ttu-id="fce67-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="fce67-957">Graefe.</span></span> <span data-ttu-id="fce67-958">The Cascades framework for query optimization.</span><span class="sxs-lookup"><span data-stu-id="fce67-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="fce67-959">IEEE 데이터 Eng.</span><span class="sxs-lookup"><span data-stu-id="fce67-959">IEEE Data Eng.</span></span> <span data-ttu-id="fce67-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="fce67-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md