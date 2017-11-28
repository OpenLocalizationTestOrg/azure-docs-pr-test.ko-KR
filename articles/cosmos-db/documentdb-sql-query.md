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
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="63072-105">Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="63072-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="63072-106">Microsoft Azure Cosmos DB는 JSON 쿼리 언어인 SQL(구조적 쿼리 언어)을 사용한 문서 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="63072-107">Cosmos DB는 스키마가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="63072-108">해당 약정 toohello JSON 데이터 모델 hello 데이터베이스 엔진 내에서 직접을 통해 명시적 스키마 나 보조 인덱스를 만들어 사용 하지 않고도 자동 JSON 문서를 인덱싱 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="63072-109">Cosmos DB에 대 한 hello 쿼리 언어를 디자인 하는 동안 두 가지 목표를가지고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="63072-110">새로운 JSON 쿼리 언어를 한계 대신 SQL toosupport를 싶었기 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="63072-111">SQL은 hello 가장 친숙 하 고 인기 있는 쿼리 언어 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="63072-112">Cosmos DB SQL은 JSON 문서에 대한 풍부한 쿼리를 위한 공식 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="63072-113">JSON 문서 데이터베이스로 JavaScript hello 데이터베이스 엔진에서 직접 실행할 수 있는 싶었기 toouse JavaScript 프로그래밍 모델 hello 기반으로 쿼리 언어에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="63072-114">DocumentDB API SQL hello 작성과 JavaScript의 형식 시스템, 식 평가, 및 함수 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="63072-115">따라서 관계형 프로젝션, JSON 문서에 대한 계층적 탐색, 자체 조인, 공간 쿼리, JavaScript로만 작성된 UDF(사용자 정의 함수) 호출 등을 위한 일반 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="63072-116">이러한 기능 hello 응용 프로그램과 hello 데이터베이스 간의 주요 tooreducing hello 마찰 있고 있는 개발자 생산성에 대 한 중요 한 것으로 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="63072-117">다음 비디오에서는 Aravind Ramachandran Cosmos DB의 쿼리 기능에 표시 하는 hello를 시청 하 여 및 방문 하 여 시작 하는 것이 좋습니다 우리의 [Query Playground](http://www.documentdb.com/sql/demo), 고 수 있는 Cosmos DB 사용해에 대 한 SQL 쿼리를 실행 합니다. 이 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="63072-118">그런 다음 반환 된 몇 가지 간단한 JSON 문서 및 SQL 명령 안내 하는 SQL 쿼리 자습서 시작 위치 toothis 문서.</span><span class="sxs-lookup"><span data-stu-id="63072-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="63072-119"><a id="GettingStarted"></a>Cosmos DB의 SQL 명령 시작하기</span><span class="sxs-lookup"><span data-stu-id="63072-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="63072-120">toosee Cosmos DB SQL에서 보겠습니다 몇 가지 간단한 JSON 문서로 시작 하 고 작업을 몇 가지 간단한 쿼리를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="63072-121">두 가족에 대한 다음 두 개의 JSON 문서를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="63072-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="63072-122">Cosmos DB에서는 필요 하지 않습니다 toocreate 모든 스키마 또는 보조 인덱스 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="63072-123">쿼리할 및 단순히 tooinsert hello JSON 문서 tooa Cosmos DB 컬렉션을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="63072-124">간단한 JSON 가지 주소 및 등록 정보 hello Andersen 제품군, hello 부모, 자식 (및의 애완 동물)에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="63072-125">hello 문서 문자열, 숫자, 부울, 배열 및 중첩 된 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="63072-126">**문서**</span><span class="sxs-lookup"><span data-stu-id="63072-126">**Document**</span></span>  

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

<span data-ttu-id="63072-127">다음은 한 가지 미묘한 차이점이 있는 두 번째 문서입니다. `givenName` 및 `familyName`이 `firstName` 및 `lastName` 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="63072-128">**문서**</span><span class="sxs-lookup"><span data-stu-id="63072-128">**Document**</span></span>  

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

<span data-ttu-id="63072-129">이제 몇 가지 쿼리 시도 하세요.이 데이터 toounderstand에 대 한 hello 중 일부의 핵심 요소 DocumentDB API SQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="63072-130">Hello 다음 hello id 필드와 일치 하는 반환 hello 문서를 쿼리 하는 예를 들어 `AndersenFamily`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="63072-131">이기 때문에 `SELECT *`, hello 쿼리의 hello 출력은 JSON 문서를 완료 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="63072-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="63072-132">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-133">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-133">**Results**</span></span>

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


<span data-ttu-id="63072-134">이제 hello 경우를 JSON 출력을 다른 모양에 tooreformat hello이 필요한 경우를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="63072-135">이 쿼리 hello 주소 도시 이름과 같은 이름을 hello hello 상태로 때 두 개의 선택 된 필드 이름 및 도시와 함께 프로젝트 새 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="63072-136">이 경우 "NY, NY"가 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="63072-137">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="63072-138">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="63072-139">hello 다음 쿼리 id와 일치 하는 hello 제품군의 자식 항목의 모든 hello 지정 된 이름을 반환 `WakefieldFamily` 거주 hello 도시별으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="63072-140">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="63072-141">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="63072-142">주목할 만한 몇 가지 hello Cosmos DB 쿼리 언어를 통해 지금까지 살펴본 hello 예제에서는 toodraw 주의 tooa 하려는:</span><span class="sxs-lookup"><span data-stu-id="63072-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="63072-143">DocumentDB API SQL은 JSON 값에 대해 작동하므로 행과 열 대신 트리 모양의 엔터티를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="63072-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="63072-144">Hello 언어를 임의 깊이에 hello 트리의 toonodes를 같은 참조할 수 있습니다 따라서 `Node1.Node2.Node3…..Nodem`, 비슷한 toorelational SQL 참조 toohello 두 파트 참조의 `<table>.<column>`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="63072-145">hello 구조적 쿼리 언어 작동 하는 스키마가 지정 되지 않은 데이터.</span><span class="sxs-lookup"><span data-stu-id="63072-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="63072-146">따라서 시스템 요구 사항 toobe 바인딩 종류를 동적으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="63072-147">hello 같은 식 향상 시킬 다른 문서에서 여러 유형의 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="63072-148">hello 쿼리 결과의 유효한 JSON 값이 있지만 고정된 스키마의 toobe 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="63072-149">Cosmos DB는 엄격한 JSON 문서만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="63072-150">즉 hello 형식 시스템 및 식에는 JSON 형식에만 제한 toodeal 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="63072-151">Toohello 참조 [JSON 사양](http://www.json.org/) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="63072-152">Cosmos DB 컬렉션은 JSON 문서의 스키마 없는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="63072-153">데이터 엔터티 컬렉션의 문서 및 내에서에서 hello 관계 제약 아니라에 의해 기본 키 및 외래 키 관계에 암시적으로 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="63072-154">이 문서의 뒷부분에서 설명 하는 hello 문서 간 조인 측면에서 살펴볼 중요 한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="63072-155"><a id="Indexing"></a> Cosmos DB 인덱싱</span><span class="sxs-lookup"><span data-stu-id="63072-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="63072-156">Hello DocumentDB API SQL 구문에 들어가기 전에 hello Cosmos db에서 디자인 인덱싱 살펴볼 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="63072-157">hello 데이터베이스 인덱스의 목적은 다양 한 폼 및 최소 리소스 사용 (예: CPU 및 입/출력)를 사용 하 여 셰이프 tooserve 쿼리 좋은 처리량과 낮은 대기 시간을 제공 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="63072-158">종종 hello 다양 한 hello 올바른 인덱스는 데이터베이스를 쿼리 하기 위한 많은 계획과 실험 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="63072-159">이 방법을 사용 하는 경우 여기서 hello 데이터 tooa 엄격한 스키마 준수 하지 않음 고 신속 하 게 진화 함에 따라 스키마가 지정 되지 않은 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="63072-160">따라서 hello Cosmos DB 인덱싱 하위 시스템의으로 설계 했으므로 때 다음과 같은 목표가 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="63072-161">스키마를 요구 하지 않고 문서를 인덱싱할: hello 인덱싱 하위 시스템 스키마 정보를 필요로 하지 않거나 hello 문서 스키마에 대 한 모든 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="63072-162">효율적이 고 풍부한 관계형 및 계층적, 쿼리에 대 한 지원: hello 인덱스 언어를 지 원하는 hello Cosmos DB 쿼리를 효율적으로 관계형 및 계층적 프로젝션에 대 한 지원을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="63072-163">쓰기 지속적인된 볼륨 사항이 발생 하더라도 일관 된 쿼리에 대 한 지원: 쓰기 처리량 워크 로드에 일관 된 쿼리로 hello 인덱스가에서 업데이트 되기 효율적으로, 증분 및 온라인 쓰기 지속적인된 볼륨의 hello 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="63072-164">hello 일치 인덱스 업데이트는 hello 일관성 수준 hello 구성 된 사용자 hello 문서 서비스에서 중요 한 tooserve hello 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="63072-165">다중 테 넌 트에 대 한 지원: 테 넌 트 간에 리소스 관리를 위한 hello 예약 기반 모델 들어 인덱스 업데이트는 hello 예산 복제본 당 할당 된 시스템 리소스 (CPU, 메모리 및 입/출력 작업 / 초) 내에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="63072-166">저장소 효율성: 비용 효율성에 대 한 hello 디스크에 저장소 오버 헤드가 hello 인덱스의는 경계 및 예측 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="63072-167">이 Cosmos DB를 사용 하면 hello 개발자 toomake 비용 기반 관계 인덱스 오버 헤드가 관계 toohello 쿼리 성능이 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="63072-168">Toohello 참조 [Azure Cosmos DB 샘플](https://github.com/Azure/azure-documentdb-net) tooconfigure 컬렉션에 대 한 인덱싱 정책을 hello 하는 방법을 보여 주는 샘플에 대 한 MSDN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="63072-169">Hello Azure Cosmos DB SQL 구문의 hello 세부 정보를 이제 가져올 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="63072-170"><a id="Basics"></a>Azure Cosmos DB SQL 쿼리의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="63072-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="63072-171">ANSI-SQL 표준에 따라 모든 쿼리는 SELECT 절과 선택적 FROM 및 WHERE 절로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="63072-172">일반적으로 각 쿼리에 대 한 hello 소스 hello FROM 절에 열거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="63072-173">그런 다음 hello JSON 문서의 하위 집합 WHERE 절 hello 소스 tooretrieve에 적용 되는 hello에서 필터링.</span><span class="sxs-lookup"><span data-stu-id="63072-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="63072-174">Hello SELECT 절을 사용 하는 마지막으로, tooproject hello 요청한 hello에 대 한 JSON 값 목록을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="63072-175"><a id="FromClause"></a>FROM 절</span><span class="sxs-lookup"><span data-stu-id="63072-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="63072-176">hello `FROM <from_specification>` hello 소스 필터링 되거나 hello 쿼리의 뒷부분에 나오는 프로젝션 하지 않는 한 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="63072-177">이 절의 hello 목적은 toospecify hello 데이터 소스는 hello 시 쿼리 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="63072-178">일반적으로 hello 전체 컬렉션은 hello 소스 하지만 하나 hello 컬렉션의 하위 집합을 대신 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="63072-179">쿼리 같은 `SELECT * FROM Families` hello 전체 제품군 컬렉션 위에 있는 tooenumerate hello 소스 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="63072-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="63072-180">특수 식별자 루트 hello 컬렉션 이름을 사용 하는 대신 사용 되는 toorepresent hello 컬렉션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="63072-181">hello 다음 목록은 쿼리당 적용 하는 hello 규칙.</span><span class="sxs-lookup"><span data-stu-id="63072-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="63072-182">hello 컬렉션 별칭을 같은 수 `SELECT f.id FROM Families AS f` 또는 단순히 `SELECT f.id FROM Families f`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="63072-183">여기 `f` hello 해당 `Families`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="63072-184">`AS`선택적 키워드 tooalias hello 식별자가입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="63072-185">한 번 별칭 hello 원본 소스를 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="63072-186">예를 들어 `SELECT Families.id FROM Families f` hello 식별자 "제품군"는 더 이상 확인할 수 없습니다 이므로 구문상 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="63072-187">Toobe 참조 해야 하는 모든 속성을 정규화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="63072-188">엄격한 스키마 준수 hello 없는 경우,이 적용된 tooavoid 모호한 모든 바인딩.</span><span class="sxs-lookup"><span data-stu-id="63072-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="63072-189">따라서 `SELECT id FROM Families f` hello 속성 이후 구문이 올바르지 않습니다 `id` 바인딩되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="63072-190">하위 문서</span><span class="sxs-lookup"><span data-stu-id="63072-190">Subdocuments</span></span>
<span data-ttu-id="63072-191">hello 소스 감소 tooa 작은 하위 집합을 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="63072-192">예를 들어, 각 문서에 하위 트리만 tooenumerating hello subroot 될 수 hello 소스 hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="63072-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="63072-193">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="63072-194">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-194">**Results**</span></span>  

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

<span data-ttu-id="63072-195">위 예제는 hello 배열을 hello 소스로으로 사용 되지만 개체 사용할 수도 hello 다음 예제에에서 표시 된 항목은 hello 소스로: 유효한 모든 JSON 값 (하지 정의 되지 않음) hello 원본에서 찾을 수 있는의 hello 결과에 포함 될 것으로 간주 됩니다 hello 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="63072-196">일부 모음에 있지 않은 경우는 `address.state` 값 hello 쿼리 결과에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="63072-197">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="63072-198">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="63072-199"><a id="WhereClause"></a>WHERE 절</span><span class="sxs-lookup"><span data-stu-id="63072-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="63072-200">WHERE 절 hello (**`WHERE <filter_condition>`**)은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="63072-201">Hello 원본에서 제공 하는 hello JSON 문서 hello 결과의 일부분으로 포함 순서 toobe에서 충족 해야 하는 hello 조건을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="63072-202">JSON 문서 여야 hello 지정 조건 너무 "true" toobe hello 결과 대 한 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="63072-203">순서 toodetermine hello 절대 가장 작은 하위 집합에 hello 결과의 일부가 될 수 있는 소스 문서의 hello 인덱스 레이어에서 절을 사용 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="63072-204">hello 다음 쿼리를 요청 값이 인 name 속성을 포함 하는 문서 `AndersenFamily`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="63072-205">Name 속성을 맺지 않은 다른 문서 hello 값이 일치 하지 않으면 또는 `AndersenFamily` 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="63072-206">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-207">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="63072-208">hello 앞의 예제는 간단한 같음 쿼리를 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="63072-209">DocumentDB API SQL은 다양한 스칼라 식도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="63072-210">가장 일반적으로 사용 하는 hello은 단항 및 이항 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="63072-211">유효한 식 hello 원본 JSON 개체에서 속성 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="63072-212">이항 연산자 뒤 hello는 현재 지원 하 고 hello 다음 예제와 같이 쿼리에서 사용할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="63072-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="63072-213">산술</span><span class="sxs-lookup"><span data-stu-id="63072-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="63072-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="63072-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="63072-215">비트</span><span class="sxs-lookup"><span data-stu-id="63072-215">Bitwise</span></span></td>    
<td><span data-ttu-id="63072-216">|, &, ^, <<, >>, >>>(0 채우기 오른쪽 시프트)</span><span class="sxs-lookup"><span data-stu-id="63072-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="63072-217">논리</span><span class="sxs-lookup"><span data-stu-id="63072-217">Logical</span></span></td>
<td><span data-ttu-id="63072-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="63072-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="63072-219">비교</span><span class="sxs-lookup"><span data-stu-id="63072-219">Comparison</span></span></td>    
<td><span data-ttu-id="63072-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="63072-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="63072-221">문자열</span><span class="sxs-lookup"><span data-stu-id="63072-221">String</span></span></td>    
<td><span data-ttu-id="63072-222">||(연결)</span><span class="sxs-lookup"><span data-stu-id="63072-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="63072-223">이항 연산자를 사용한 몇 가지 쿼리를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="63072-224">hello 단항 연산자 +,-, ~ 에서도 지원 됩니다 하지 넣고 hello 다음 예제와 같이 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="63072-225">또한 toobinary 및 단항 연산자 속성 참조 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="63072-226">예를 들어 `SELECT * FROM Families f WHERE f.isRegistered` 반환 hello hello 속성을 포함 하는 JSON 문서 `isRegistered` 된 hello 속성의 값이 같으면 toohello JSON `true` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="63072-227">다른 값 (false, null, 정의 되지 않음, `<number>`, `<string>`, `<object>`, `<array>`등) hello 결과에서 제외 되 고 toohello 소스 문서를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="63072-228">같음 및 비교 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-228">Equality and comparison operators</span></span>
<span data-ttu-id="63072-229">hello 다음 표에 나와 같음 비교의 hello 결과 DocumentDB API SQL 임의의 JSON 형식 간의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="63072-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-233">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-234">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-235">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="63072-237">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="63072-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-254">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="63072-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-262">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="63072-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-270">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="63072-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="63072-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="63072-286">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="63072-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="63072-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="63072-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="63072-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="63072-294">와 같은 다른 비교 연산자에 대 한 >, > =,! =, < 및 < =, hello 다음 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="63072-295">형식 비교 결과가 Undefined입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="63072-296">두 개체 또는 두 배열 간 비교 결과가 Undefined입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="63072-297">Hello 필터에 hello 스칼라 식의 hello 결과 정의 되어 있지 hello는 해당 문서는에 포함 되지 hello 결과 이후 Undefined 너무 "true"와 동등 논리적으로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="63072-298">BETWEEN 키워드</span><span class="sxs-lookup"><span data-stu-id="63072-298">BETWEEN keyword</span></span>
<span data-ttu-id="63072-299">ANSI SQL에서와 같은 값의 범위에 대 한 hello BETWEEN 키워드 tooexpress 쿼리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="63072-300">문자열이나 숫자에 BETWEEN을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="63072-301">예를 들어이 쿼리는 모든 패밀리 문서는 hello 첫 번째 자식 등급이 1-5 (둘 다 포함) 사이입니다를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="63072-302">와 달리 ANSI SQL에서 사용할 수도 있습니다 hello BETWEEN 절 hello 다음 예제에서에서와 같은 hello FROM 절에 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="63072-303">더 빠른 쿼리 실행 시간에 대 한 모든 숫자 속성/경로 hello BETWEEN 절에 필터링 된 범위 인덱스 유형을 사용 하는 인덱싱 정책을 toocreate를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="63072-304">hello는 주요 차이점이 BETWEEN DocumentDB API 및 ANSI SQL을 사용 하 여 혼합 형식의 속성에 대 한 범위 쿼리를 표현할 수 있습니다-예를 들어 "1 등급" (5)는 숫자 여야 할 수도 있습니다 일부 문서 및 다른 사용자 ("grade4")의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="63072-305">이러한 경우와 같은 JavaScript에서 "undefined"에서 두 개의 서로 다른 형식 결과 hello 문서 간의 비교를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="63072-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="63072-306">논리(AND, OR 및 NOT) 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="63072-307">논리 연산자는 부울 값에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="63072-308">이러한 연산자에 대 한 hello 논리적 진리 테이블은 다음 표에서 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="63072-309">또는</span><span class="sxs-lookup"><span data-stu-id="63072-309">OR</span></span> | <span data-ttu-id="63072-310">True</span><span class="sxs-lookup"><span data-stu-id="63072-310">True</span></span> | <span data-ttu-id="63072-311">False</span><span class="sxs-lookup"><span data-stu-id="63072-311">False</span></span> | <span data-ttu-id="63072-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="63072-313">True</span><span class="sxs-lookup"><span data-stu-id="63072-313">True</span></span> |<span data-ttu-id="63072-314">True</span><span class="sxs-lookup"><span data-stu-id="63072-314">True</span></span> |<span data-ttu-id="63072-315">True</span><span class="sxs-lookup"><span data-stu-id="63072-315">True</span></span> |<span data-ttu-id="63072-316">True</span><span class="sxs-lookup"><span data-stu-id="63072-316">True</span></span> |
| <span data-ttu-id="63072-317">False</span><span class="sxs-lookup"><span data-stu-id="63072-317">False</span></span> |<span data-ttu-id="63072-318">True</span><span class="sxs-lookup"><span data-stu-id="63072-318">True</span></span> |<span data-ttu-id="63072-319">False</span><span class="sxs-lookup"><span data-stu-id="63072-319">False</span></span> |<span data-ttu-id="63072-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-320">Undefined</span></span> |
| <span data-ttu-id="63072-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-321">Undefined</span></span> |<span data-ttu-id="63072-322">True</span><span class="sxs-lookup"><span data-stu-id="63072-322">True</span></span> |<span data-ttu-id="63072-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-323">Undefined</span></span> |<span data-ttu-id="63072-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-324">Undefined</span></span> |

| <span data-ttu-id="63072-325">AND</span><span class="sxs-lookup"><span data-stu-id="63072-325">AND</span></span> | <span data-ttu-id="63072-326">True</span><span class="sxs-lookup"><span data-stu-id="63072-326">True</span></span> | <span data-ttu-id="63072-327">False</span><span class="sxs-lookup"><span data-stu-id="63072-327">False</span></span> | <span data-ttu-id="63072-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="63072-329">True</span><span class="sxs-lookup"><span data-stu-id="63072-329">True</span></span> |<span data-ttu-id="63072-330">True</span><span class="sxs-lookup"><span data-stu-id="63072-330">True</span></span> |<span data-ttu-id="63072-331">False</span><span class="sxs-lookup"><span data-stu-id="63072-331">False</span></span> |<span data-ttu-id="63072-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-332">Undefined</span></span> |
| <span data-ttu-id="63072-333">False</span><span class="sxs-lookup"><span data-stu-id="63072-333">False</span></span> |<span data-ttu-id="63072-334">False</span><span class="sxs-lookup"><span data-stu-id="63072-334">False</span></span> |<span data-ttu-id="63072-335">False</span><span class="sxs-lookup"><span data-stu-id="63072-335">False</span></span> |<span data-ttu-id="63072-336">False</span><span class="sxs-lookup"><span data-stu-id="63072-336">False</span></span> |
| <span data-ttu-id="63072-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-337">Undefined</span></span> |<span data-ttu-id="63072-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-338">Undefined</span></span> |<span data-ttu-id="63072-339">False</span><span class="sxs-lookup"><span data-stu-id="63072-339">False</span></span> |<span data-ttu-id="63072-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-340">Undefined</span></span> |

| <span data-ttu-id="63072-341">NOT</span><span class="sxs-lookup"><span data-stu-id="63072-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="63072-342">True</span><span class="sxs-lookup"><span data-stu-id="63072-342">True</span></span> |<span data-ttu-id="63072-343">False</span><span class="sxs-lookup"><span data-stu-id="63072-343">False</span></span> |
| <span data-ttu-id="63072-344">False</span><span class="sxs-lookup"><span data-stu-id="63072-344">False</span></span> |<span data-ttu-id="63072-345">True</span><span class="sxs-lookup"><span data-stu-id="63072-345">True</span></span> |
| <span data-ttu-id="63072-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-346">Undefined</span></span> |<span data-ttu-id="63072-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="63072-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="63072-348">IN 키워드</span><span class="sxs-lookup"><span data-stu-id="63072-348">IN keyword</span></span>
<span data-ttu-id="63072-349">hello IN 키워드는 지정된 된 값 목록에 있는 값이 일치 하는지 여부를 사용 하는 toocheck 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="63072-350">예를 들어이 쿼리는 hello id가 "WakefieldFamily" 또는 "AndersenFamily" 중 패밀리 문서를 모두 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="63072-351">이 예에서는 모든 문서 hello 상태는 지정 된 hello의 반환 값입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="63072-352">3항(?) 및 병합(??) 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="63072-353">hello 삼항과 Coalesce 연산자에 사용 되는 toobuild 조건식, 프로그래밍 언어 C# 및 JavaScript와 같은 비슷한 toopopular 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="63072-354">고객이 hello에 새 JSON 속성을 생성 하는 경우에 hello (?) 삼항 연산자 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="63072-355">예를 들어 이제 작성할 수 있습니다 쿼리 tooclassify hello 클래스 수준 초급/중간/고급 아래와 같이 같은 사람이 읽을 수 있는 형식으로.</span><span class="sxs-lookup"><span data-stu-id="63072-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="63072-356">아래 hello 쿼리에서 hello 호출 toohello 연산자와 같은 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="63072-357">으로 다른 쿼리 연산자와 hello hello 조건식에 참조 된 속성에서에서 누락 된 경우 모든 문서 또는 hello 형식을 비교 하 고 서로 다른 경우 다음 해당 문서 제외 됩니다 hello 쿼리 결과에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="63072-358">hello Coalesce (?) 연산자 될 수 있습니다 (규칙 하위 속성이 있는지 hello에 대 한 tooefficiently 검사 사용</span><span class="sxs-lookup"><span data-stu-id="63072-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="63072-359">효율적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-359">is defined) in a document.</span></span> <span data-ttu-id="63072-360">이 연산자는 반구조적 데이터나 혼합 형식의 데이터에 대해 쿼리할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="63072-361">예를 들어이 쿼리 없으면 hello "lastName" 있는 경우 또는 "surname" hello 존재 하지입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="63072-362"><a id="EscapingReservedKeywords"></a>따옴표 붙은 속성 접근자</span><span class="sxs-lookup"><span data-stu-id="63072-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="63072-363">Hello 따옴표 붙은 속성 연산자를 사용 하 여 속성에 액세스할 수도 있습니다 `[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="63072-364">예를 들어 `SELECT c.grade` and `SELECT c["grade"]` 와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="63072-365">이 구문은 tooescape SQL 키워드 또는 예약 된 단어인 이름이 tooshare hello 또는 공백, 특수 문자를 포함 하는 속성을 사용 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="63072-366"><a id="SelectClause"></a>SELECT 절</span><span class="sxs-lookup"><span data-stu-id="63072-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="63072-367">hello SELECT 절 (**`SELECT <select_list>`**) 필수 이며 ANSI SQL의와 동일 하 게 hello 쿼리에서 값은 검색을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="63072-368">hello 소스 문서를 기반으로 필터링 된 hello 하위 집합 hello JSON 값을 검색 하 고 새 JSON 개체가 생성 되 면 붙여 전달 하는 각 입력에 대해 지정 된이 있는 hello 프로젝션 단계에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="63072-369">다음 예제는 hello 일반적인 선택 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63072-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="63072-370">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-371">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="63072-372">중첩 속성</span><span class="sxs-lookup"><span data-stu-id="63072-372">Nested properties</span></span>
<span data-ttu-id="63072-373">다음 예제는 hello, 두 개의 중첩된 속성 프로젝션은 우리 `f.address.state` 및 `f.address.city`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="63072-374">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-375">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="63072-376">또한 프로젝션 hello 다음 예제와 같이 JSON 식을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="63072-377">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-378">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="63072-379">hello 역할에 살펴보겠습니다 `$1` 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="63072-380">hello `SELECT` 절 toocreate JSON 개체 하며으로 시작 하는 암시적 인수가 변수 이름을 사용 하 여 없는 키를 제공 하므로 `$1`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="63072-381">예를 들어 이 쿼리는 `$1` 및 `$2` 레이블이 지정된 두 개의 암시적 인수 변수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="63072-382">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-383">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="63072-384">별칭 지정</span><span class="sxs-lookup"><span data-stu-id="63072-384">Aliasing</span></span>
<span data-ttu-id="63072-385">이제 hello 위의 예에서는 명시적 앨리어싱 사용한 값을 확장 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="63072-386">마찬가지로 연결 하기 위해 사용 하는 hello 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="63072-387">프로젝션 hello 두 번째 값으로 하는 동안 표시 된 것 처럼 선택 사항이 기는 `NameInfo`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="63072-388">쿼리에서 hello 사용 하 여 두 개의 속성 경우 동일한 이름 별칭 이어야 합니다. 하나 또는 둘 다의 hello 속성을 프로젝션 하는 hello에 구분 되는 사용 되는 toorename 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="63072-389">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-390">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="63072-391">스칼라 식</span><span class="sxs-lookup"><span data-stu-id="63072-391">Scalar expressions</span></span>
<span data-ttu-id="63072-392">또한 tooproperty 참조, hello SELECT 절에 상수, 산술 식, 논리 식 등과 같은 스칼라 식도 지원 합니다. 예를 들어 다음은 단순한 "Hello World" 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="63072-393">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="63072-394">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="63072-395">다음은 스칼라 식을 사용하는 보다 복잡한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="63072-396">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="63072-397">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="63072-398">다음 예제는 hello, hello 스칼라 식의 hello 결과는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="63072-399">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="63072-400">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="63072-401">개체 및 배열 만들기</span><span class="sxs-lookup"><span data-stu-id="63072-401">Object and array creation</span></span>
<span data-ttu-id="63072-402">DocumentDB API SQL의 다른 주요 기능은 배열/개체 만들기입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="63072-403">Hello 이전 예제에서는 새 JSON 개체를 만들었다고 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="63072-404">마찬가지로, 다음 예제는 hello와 같이 배열을 생성할 수도 하나:</span><span class="sxs-lookup"><span data-stu-id="63072-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="63072-405">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="63072-406">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-406">**Results**</span></span>  

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

### <span data-ttu-id="63072-407"><a id="ValueKeyword"></a>VALUE 키워드</span><span class="sxs-lookup"><span data-stu-id="63072-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="63072-408">hello **값** 키워드 방법을 tooreturn JSON 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="63072-409">예를 들어 hello 쿼리 아래에 표시 된 반환 hello 스칼라 `"Hello World"` 대신 `{$1: "Hello World"}`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="63072-410">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="63072-411">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="63072-412">hello 다음 쿼리는 반환 hello 없이 hello JSON 값 `"address"` hello 결과에 레이블.</span><span class="sxs-lookup"><span data-stu-id="63072-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="63072-413">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="63072-414">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-414">**Results**</span></span>  

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

<span data-ttu-id="63072-415">hello 다음 예에서는 확장이 tooshow 어떻게 tooreturn JSON primitive 값 (hello JSON 트리의 hello 리프 수준).</span><span class="sxs-lookup"><span data-stu-id="63072-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="63072-416">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="63072-417">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="63072-418">* 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-418">* Operator</span></span>
<span data-ttu-id="63072-419">hello 특수 연산자 (*)는 지원 되는 tooproject hello 문서-됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="63072-420">을 사용 하는 hello만 필드를 프로젝션 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="63072-421">`SELECT * FROM Families f`와 같은 쿼리는 유효하지만 `SELECT VALUE * FROM Families f ` 및 `SELECT *, f.id FROM Families f `와 같은 쿼리는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="63072-422">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="63072-423">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-423">**Results**</span></span>

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

### <span data-ttu-id="63072-424"><a id="TopKeyword"></a>TOP 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="63072-425">hello TOP 키워드 수 toolimit hello 수가 쿼리에서 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="63072-426">Hello 결과 집합은 정렬 된 값의 제한 된 toohello 첫 번째 N 번호 TOP와 hello ORDER BY 절과 함께에서 사용할 경우 그렇지 않으면 정의 되지 않은 순서로 hello 결과의 첫 번째 N 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="63072-427">모범 사례로, SELECT 문에서 항상는 ORDER BY 절과 함께 사용 hello TOP 절.</span><span class="sxs-lookup"><span data-stu-id="63072-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="63072-428">이 hello 유일한 방법은 toopredictably TOP의 영향을 받는 행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="63072-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="63072-429">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="63072-430">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-430">**Results**</span></span>

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

<span data-ttu-id="63072-431">위에 나와 있는 것처럼 상수 값 또는 매개 변수가 있는 쿼리를 사용하는 변수 값과 함께 TOP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="63072-432">자세한 내용은 아래의 매개 변수가 있는 쿼리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63072-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="63072-433"><a id="Aggregates"></a>집계 함수</span><span class="sxs-lookup"><span data-stu-id="63072-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="63072-434">또한 hello에 대 한 집계를 수행 `SELECT` 절.</span><span class="sxs-lookup"><span data-stu-id="63072-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="63072-435">집계 함수는 값 집합에서 계산을 수행하고 단일 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="63072-436">예를 들어 hello 다음 쿼리 hello의 개수를 반환 hello 컬렉션 내에서 패밀리 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="63072-437">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="63072-438">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="63072-439">반환할 수도 있습니다 hello hello의 스칼라 값 집계 hello를 사용 하 여 `VALUE` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="63072-440">예를 들어 hello 다음 쿼리 hello의 개수를 반환 값을 단일 숫자로:</span><span class="sxs-lookup"><span data-stu-id="63072-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="63072-441">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="63072-442">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="63072-443">필터와 함께 조합하여 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="63072-444">예를 들어 hello 다음 쿼리 hello에서에서 개수를 반환 hello 주소를 사용 하 여 문서의 hello 워싱턴 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="63072-445">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="63072-446">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="63072-447">hello 다음 표에 지원 되는 집계 함수 목록은 hello DocumentDB API에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="63072-448">`SUM` 및 `AVG`는 숫자 값에 대해 수행되는 반면 `COUNT`, `MIN` 및 `MAX`는 숫자, 문자열, 부울 및 null에 대해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="63072-449">사용 현황</span><span class="sxs-lookup"><span data-stu-id="63072-449">Usage</span></span> | <span data-ttu-id="63072-450">설명</span><span class="sxs-lookup"><span data-stu-id="63072-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="63072-451">개수</span><span class="sxs-lookup"><span data-stu-id="63072-451">COUNT</span></span> | <span data-ttu-id="63072-452">반환 hello hello 식의 항목 수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="63072-453">합계</span><span class="sxs-lookup"><span data-stu-id="63072-453">SUM</span></span>   | <span data-ttu-id="63072-454">반환 hello hello 식에서 모든 hello 값의 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="63072-455">최소</span><span class="sxs-lookup"><span data-stu-id="63072-455">MIN</span></span>   | <span data-ttu-id="63072-456">반환 hello hello 식의 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="63072-457">최대</span><span class="sxs-lookup"><span data-stu-id="63072-457">MAX</span></span>   | <span data-ttu-id="63072-458">반환 hello hello 식의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="63072-459">평균</span><span class="sxs-lookup"><span data-stu-id="63072-459">AVG</span></span>   | <span data-ttu-id="63072-460">반환 hello hello hello 식 값의 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="63072-461">배열 반복 hello 결과 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="63072-462">자세한 내용은 [쿼리에서 배열 반복](#Iteration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63072-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="63072-463">Azure 포털의 쿼리 탐색기 hello를 사용 하 여, 집계 쿼리를 반환할 수 있습니다 부분적으로 hello 참고 쿼리 페이지를 통해 결과 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="63072-464">hello Sdk는 모든 페이지에 걸쳐 단일 누적 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="63072-465">.NET SDK 1.12.0,.NET Core SDK 1.1.0, 또는 Java SDK 1.9.5 필요한 코드를 사용 하 여 tooperform 집계 쿼리를 위해 이상.</span><span class="sxs-lookup"><span data-stu-id="63072-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="63072-466"><a id="OrderByClause"></a>ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="63072-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="63072-467">ANSI-SQL에서와 마찬가지로 쿼리하는 동안 선택적 Order By 절을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="63072-468">hello 절은 선택적 ASC/DESC 인수 toospecify hello 순서는 결과 검색에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="63072-469">예를 들어 여기에 hello 상주 도시 이름 순서 대로 패밀리를 검색 하는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="63072-470">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="63072-471">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-471">**Results**</span></span>

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

<span data-ttu-id="63072-472">및의 순서를 나타내는 숫자 hello epoch 시간, 즉, 경과 시간 1970 년 1 월 1 일 이후 (초)에서으로 저장 된 만든 날짜, 패밀리를 검색 하는 쿼리 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="63072-473">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="63072-474">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-474">**Results**</span></span>

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

## <span data-ttu-id="63072-475"><a id="Advanced"></a>고급 데이터베이스 개념 및 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="63072-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="63072-476"><a id="Iteration"></a>반복</span><span class="sxs-lookup"><span data-stu-id="63072-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="63072-477">새 구문을 hello를 통해 추가 된 **IN** JSON 배열을 반복 하는 DocumentDB API SQL tooprovide 지원의 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="63072-478">hello FROM 소스 반복에 대 한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="63072-479">다음 예제는 hello로 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-479">Let's start with hello following example:</span></span>

<span data-ttu-id="63072-480">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="63072-481">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-481">**Results**</span></span>  

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

<span data-ttu-id="63072-482">이제 hello 컬렉션에 대 한 자식 반복을 수행 하는 다른 쿼리를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="63072-483">Note hello 차이 hello 출력 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="63072-484">이 예제에서는 분할 `children` 단일 배열로 hello 결과 평면화 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="63072-485">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="63072-486">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-486">**Results**</span></span>  

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

<span data-ttu-id="63072-487">이 수 추가로 hello 다음 예제와 같이 hello 배열의 각 개별 항목에 사용 되는 toofilter:</span><span class="sxs-lookup"><span data-stu-id="63072-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="63072-488">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="63072-489">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="63072-490">배열 반복 hello 결과 대해 집계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="63072-491">예를 들어 hello 다음 쿼리 수를 계산 hello 모든 패밀리 자식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="63072-492">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="63072-493">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="63072-494"><a id="Joins"></a>조인</span><span class="sxs-lookup"><span data-stu-id="63072-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="63072-495">관계형 데이터베이스 테이블에서 hello 필요 toojoin이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="63072-496">hello 논리 배치한 toodesigning 정규화 된 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="63072-497">반대 toothis, DocumentDB API 문서 스키마가 없는 hello 정규화 되지 않은 데이터 모델을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="63072-498">이 hello 논리적으로 동일 "자체 조인을" a.</span><span class="sxs-lookup"><span data-stu-id="63072-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="63072-499">hello hello 언어를 지원 하는 구문은 < from_source1 > 조인 < from_source2 > 조인 중... JOIN <from_sourceN>입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="63072-500">대체로 이 구문은 **N** 튜플(**N**개 값이 포함된 튜플) 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="63072-501">각 튜플은 해당 집합에 모든 컬렉션 별칭을 반복하여 생성된 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="63072-502">즉,이 전체 집합의 교차곱 hello hello 조인에 참여 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="63072-503">hello 다음 예제에서는 작동 방식을 보여 hello JOIN 절.</span><span class="sxs-lookup"><span data-stu-id="63072-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="63072-504">다음 예제는 hello, hello 결과 hello 각 문서 원본과 빈 집합의 교차곱은 비어 있으므로 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="63072-505">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="63072-506">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="63072-507">다음 예제는 hello, hello 조인은 hello 문서 루트 사이의 hello `children` subroot 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="63072-508">두 JSON 개체 간의 교차곱입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="63072-509">hello 자식 배열에 있는 단일 루트를 다루는 때문에 자식 배열 임을 hello 팩트 hello 조인에에서 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="63072-510">따라서 hello 결과 hello hello 배열이 포함 된 각 문서의 교차곱 생성 문서가 정확히 하나만 있으므로 두 개의 결과 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="63072-511">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="63072-512">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="63072-513">다음 예제는 hello에 더 많은 기본 조인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63072-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="63072-514">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="63072-515">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-515">**Results**</span></span>

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



<span data-ttu-id="63072-516">hello 먼저 toonote는 해당 hello `from_source` 의 hello **조인** 절은 반복기입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="63072-517">따라서 hello 흐름이 경우에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="63072-518">각 자식 요소를 확장 **c** hello 배열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="63072-519">Hello 문서의 hello 루트를 가진 교차곱 적용 **f** 각 자식 요소가 **c** hello 첫 번째 단계에서 결합 된입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="63072-520">마지막으로, 프로젝트 hello 루트 개체 **f** 속성만 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="63072-521">첫 번째 문서 hello (`AndersenFamily`) hello 결과 집합에는 단일 개체 해당 toothis 문서에만 포함 되므로 자식 요소가 하나만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="63072-522">두 번째 문서 hello (`WakefieldFamily`) 두 명의 자식이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="63072-523">따라서 hello 교차곱 개체를 생성 별도 각 자식 해당 toothis 문서에 대해 하나씩 두 개의 개체를 그 결과로 각 자식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="63072-524">이러한 두 문서 필드는 hello 루트 hello 교차곱에서 기대 하는 것 처럼 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="63072-525">hello hello 조인의 실제 유틸리티이 고, 그렇지 않은 셰이프에 hello 교차곱 tooform 튜플을 어려운 tooproject 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="63072-526">또한 아래 hello 예제에서 보이는 것 처럼를 필터링 할 수 있는 튜플의 hello 조합 수 있는 hello overall hello 튜플에 의해 충족 하는 조건을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="63072-527">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="63072-528">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-528">**Results**</span></span>

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



<span data-ttu-id="63072-529">이 예제는 hello 예제에서는 앞의 기본 확장 및 이중 조인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="63072-530">따라서 hello 교차곱으로 볼 수 있습니다 다음 의사 코드 hello:</span><span class="sxs-lookup"><span data-stu-id="63072-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

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

<span data-ttu-id="63072-531">`AndersenFamily`에는 애완 동물 한 마리를 키우는 자식 한 명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="63072-532">따라서 hello 교차곱을 생성 한 행 (1\*1\*1)이이 제품군에서.</span><span class="sxs-lookup"><span data-stu-id="63072-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="63072-533">그러나 WakefieldFamily에는 자녀 두 명이 있지만 그 중에 "Jesse"만 애완 동물을</span><span class="sxs-lookup"><span data-stu-id="63072-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="63072-534">두 마리 키우고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-534">Jesse has two pets though.</span></span> <span data-ttu-id="63072-535">따라서 hello 교차곱 생성 1\*1\*이 제품군에서 행을 2 = 2입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="63072-536">Hello 다음 예제에서는 필터를 추가로에 없을 `pet`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="63072-537">이 hello 애완 동물 이름 "그림자" 하지 않은 모든 hello 튜플을 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="63072-538">म 수 toobuild 튜플로 배열, hello 튜플의 hello 요소에 대 한 필터를 hello 요소 조합을 프로젝트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="63072-539">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="63072-540">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="63072-541"><a id="JavaScriptIntegration"></a>JavaScript 통합</span><span class="sxs-lookup"><span data-stu-id="63072-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="63072-542">Azure Cosmos DB 저장된 프로시저 및 트리거를 기준으로 hello 컬렉션에 직접 JavaScript 기반 응용 프로그램 논리를 실행 하기 위한 프로그래밍 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="63072-543">이 경우 다음 두 가지 기능을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-543">This allows for both:</span></span>

* <span data-ttu-id="63072-544">기능 toodo 고성능 트랜잭션 CRUD 작업 및 hello 데이터베이스 엔진 내에서 직접 JavaScript 런타임 hello 긴밀 한 통합으로 인해 컬렉션의 문서에 대해 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="63072-545">데이터베이스 트랜잭션을 사용하여 제어 흐름, 변수 범위 지정 및 예외 처리 기본 형식의 할당과 통합을 기본적으로 모델링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="63072-546">JavaScript 통합에 대 한 Azure Cosmos DB 지원에 대 한 자세한 내용은 toohello JavaScript 서버 쪽 프로그래밍 기능 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="63072-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="63072-547"><a id="UserDefinedFunctions"></a>UDF(사용자 정의 함수)</span><span class="sxs-lookup"><span data-stu-id="63072-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="63072-548">이 문서에 이미 정의 된 hello 형식과, 함께 DocumentDB API SQL 지원에 대 한 사용자 정의 함수 (UDF)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="63072-549">특히, 스칼라 Udf는 hello 개발자 0 개 이상의 인수를 전달 하 고 단일 인수 결과 다시 반환할 수 있는 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="63072-550">이러한 각 인수가 유효한 JSON 값인지 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="63072-551">DocumentDB API SQL 구문이 hello는 이러한 사용자 정의 함수를 사용 하 여 toosupport 사용자 지정 응용 프로그램 논리를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="63072-552">UDF를 DocumentDB API에 등록한 다음 SQL 쿼리의 일부로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="63072-553">사실, Udf는 exquisitely hello 설계 toobe 쿼리에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="63072-554">배치한 toothis 선택으로 Udf 하지 않은 액세스 toohello 컨텍스트 개체는 hello 다른 JavaScript 형식 (예: 저장된 프로시저 및 트리거)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="63072-555">쿼리는 읽기 전용으로 실행되므로 주 복제본 또는 보조 복제본에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="63072-556">따라서 Udf 다른 JavaScript 종류와 달리 보조 복제본에서 설계 된 toorun 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="63072-557">다음은 hello Cosmos DB 데이터베이스 문서 컬렉션에서 특히에 UDF 수 등록 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="63072-558">hello 앞의 예제는 UDF를 만듭니다 이름이 `REGEX_MATCH`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="63072-559">두 개의 JSON 문자열 값을 허용 `input` 및 `pattern` 및 JavaScript의 string.match() 함수를 사용 하는 hello 첫 번째 일치 항목이 hello 패턴에 지정 된 두 번째 hello 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="63072-560">이제 이 UDF를 프로젝트의 쿼리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="63072-561">Udf는 hello 대/소문자 구분 접두사 "udf"으로 한정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="63072-562">UDF를 한정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="63072-563">이전 too3/17/2015 Cosmos DB 지원 hello "udf." 없는 UDF 호출</span><span class="sxs-lookup"><span data-stu-id="63072-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="63072-564">UDF 호출을 지원했습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="63072-565">이 호출 패턴은 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="63072-566">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="63072-567">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="63072-568">hello 아래 예에서는 또한 hello "udf."으로 정규화와 같이 hello UDF 필터 내 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="63072-569">있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-569">prefix:</span></span>

<span data-ttu-id="63072-570">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="63072-571">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="63072-572">기본적으로 UDF는 유효한 스칼라 식이며 프로젝션과 필터 둘 다에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="63072-573">tooexpand Udf의 hello 전원으로 살펴보겠습니다 또 다른 예로 조건부 논리로:</span><span class="sxs-lookup"><span data-stu-id="63072-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="63072-574">다음은 연습 hello UDF는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="63072-575">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="63072-576">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-576">**Results**</span></span>

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


<span data-ttu-id="63072-577">위의 예제 사례 hello, 대로 Udf JavaScript 언어의 hello 전원와 통합 hello DocumentDB API SQL tooprovide는 풍부한 프로그래밍 가능한 인터페이스 toodo 복잡 한 절차, 조건부 논리 사용 하 여 hello 내장된 JavaScript 런타임 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="63072-578">DocumentDB API SQL 인수를 제공 hello toohello Udf hello 소스에 있는 각 문서에 대 한 hello의 현재 단계 (WHERE 절 또는 SELECT 절) 처리 hello UDF에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="63072-579">hello 결과에 통합 됩니다 전반적인 실행 파이프라인을 원활 하 게 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="63072-580">참조 된 tooby hello UDF 매개 변수에서 사용할 수 없는 JSON 값 hello hello 매개 변수 한 것으로 간주 하는 hello 속성 정의 되지 않은 및 따라서 hello UDF 호출 전적으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="63072-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="63072-581">마찬가지로 hello UDF의 hello 결과 정의 되지 않은 경우 hello 결과에 되지 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="63072-582">요약 하자면, Udf는 hello 쿼리의 일부로 유용한 도구 toodo 복잡 한 비즈니스 논리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="63072-583">연산자 평가</span><span class="sxs-lookup"><span data-stu-id="63072-583">Operator evaluation</span></span>
<span data-ttu-id="63072-584">Cosmos DB JSON 데이터베이스는 hello 전문화 하 여 JavaScript 연산자와 해당 평가 의미 체계가 parallels를 그립니다.</span><span class="sxs-lookup"><span data-stu-id="63072-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="63072-585">Cosmos DB JSON 지원 측면에서 toopreserve JavaScript 의미 체계를 시도 하는 동안 일부 인스턴스에서 hello 작업 평가 다르면 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="63072-586">DocumentDB API sql에서 달리 기존의 SQL hello 유형의 값 종종 알 수 없는 데이터베이스에서 hello 값을 검색할 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="63072-587">쿼리를 실행할 순서 tooefficiently에서, 대부분의 hello 연산자 엄격한 형식 요구 사항.</span><span class="sxs-lookup"><span data-stu-id="63072-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="63072-588">DocumentDB API SQL은 JavaScript와 달리 암시적 변환을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="63072-589">예를 들어 `SELECT * FROM Person p WHERE p.Age = 21`과 같은 쿼리는 Age 속성을 포함하고 값이 21인 문서에 일치됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="63072-590">Age 속성이 문자열 "21" 또는 "021", "21.0", "0021", "00021" 등의 다른 무한 변형과 일치하는 다른 문서는 일치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="63072-591">이 hello 문자열에 값이 암시적으로 캐스팅할 toonumbers JavaScript toohello 반대로 (예: 연산자에 기반한: = =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="63072-592">이 선택 항목은 DocumentDB API SQL의 효율적인 인덱스 매핑에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="63072-593">매개 변수가 있는 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="63072-593">Parameterized SQL queries</span></span>
<span data-ttu-id="63072-594">Cosmos DB는 @ 표기법 친숙 한 hello로 표현 된 매개 변수가 있는 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="63072-595">매개 변수가 있는 SQL은 사용자 입력의 강력한 처리 및 이스케이프를 제공하여 SQL 주입을 통해 데이터가 실수로 노출되는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="63072-596">예를 들어 성 및 주소 상태를 매개 변수로 사용하는 쿼리를 작성한 다음 사용자 입력에 따라 다양한 성 및 주소 상태 값에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="63072-597">이 요청 보낼 수와 같은 매개 변수가 있는 JSON 쿼리로 DB tooCosmos 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="63072-598">hello 인수 tooTOP 설정할 수 있습니다 같은 매개 변수가 있는 쿼리를 사용 하 여 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="63072-599">매개 변수 값은 유효한 모든 JSON(문자열, 숫자, 부울, null, 짝수 배열 또는 중첩된 JSON)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="63072-600">또한 Cosmos DB는 스키마가 없으므로 모든 형식에 대해 매개 변수의 유효성이 검사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="63072-601"><a id="BuiltinFunctions"></a>기본 제공 함수</span><span class="sxs-lookup"><span data-stu-id="63072-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="63072-602">Cosmos DB는 일반적인 작업을 위해 많은 기본 제공 함수도 지원하며, UDF(사용자 정의 함수)처럼 쿼리 내에서 이러한 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="63072-603">함수 그룹</span><span class="sxs-lookup"><span data-stu-id="63072-603">Function group</span></span>          | <span data-ttu-id="63072-604">작업</span><span class="sxs-lookup"><span data-stu-id="63072-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="63072-605">수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="63072-605">Mathematical functions</span></span>  | <span data-ttu-id="63072-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN 및 TAN</span><span class="sxs-lookup"><span data-stu-id="63072-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="63072-607">형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="63072-607">Type checking functions</span></span> | <span data-ttu-id="63072-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED 및 IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="63072-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="63072-609">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="63072-609">String functions</span></span>        | <span data-ttu-id="63072-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING 및 UPPER</span><span class="sxs-lookup"><span data-stu-id="63072-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="63072-611">배열 함수</span><span class="sxs-lookup"><span data-stu-id="63072-611">Array functions</span></span>         | <span data-ttu-id="63072-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH 및 ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="63072-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="63072-613">공간 함수</span><span class="sxs-lookup"><span data-stu-id="63072-613">Spatial functions</span></span>       | <span data-ttu-id="63072-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID 및 ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="63072-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="63072-615">Toobe 빠르게 toorun 등 것 처럼 hello 해당 기본 제공 함수를 사용 해야 사용자 정의 함수 (UDF) 기본 제공 함수를 지금 사용할 수 있는, 현재 사용 중인 경우 효율적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="63072-616">수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="63072-616">Mathematical functions</span></span>
<span data-ttu-id="63072-617">인수로 제공 되 고 숫자 값을 반환 하는 입력된 값에 따라 계산을 수행 하는 hello 각 수치 연산 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="63072-618">다음은 지원되는 기본 제공 수치 연산 함수 표입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="63072-619">사용 현황</span><span class="sxs-lookup"><span data-stu-id="63072-619">Usage</span></span> | <span data-ttu-id="63072-620">설명</span><span class="sxs-lookup"><span data-stu-id="63072-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="63072-621">[[ABS(num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="63072-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="63072-622">Hello 절대 (양수)의 값을 반환 hello 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-623">CEILING(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="63072-624">Hello, 보다 큰 가장 작은 정수 값 또는 같음, hello 특정된 숫자 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-625">FLOOR(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="63072-626">작은 hello 가장 큰 정수를 반환 toohello 같거나 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-627">EXP(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="63072-628">Hello의 반환 hello 지 수를 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="63072-629">[LOG(num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="63072-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="63072-630">반환 hello 자연 로그의 hello 지정한 숫자 식 또는 hello를 사용 하 여 hello 로그 지정 자료</span><span class="sxs-lookup"><span data-stu-id="63072-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="63072-631">LOG10(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="63072-632">Hello 상용 로그 눈금 간격의 값을 반환 hello 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-633">ROUND(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="63072-634">숫자 값을 반올림된 toohello 가장 가까운 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="63072-635">TRUNC(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="63072-636">숫자 값, 잘린된 toohello 가장 가까운 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="63072-637">SQRT(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="63072-638">Hello의 반환 hello 제곱근을 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-639">SQUARE(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="63072-640">반환 hello hello의 제곱를 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-641">POWER(num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="63072-642">반환 hello 전원 hello의 지정 된 숫자 식 toohello 값 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="63072-643">SIGN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="63072-644">Hello 반환 hello 기호 값 (-1, 0, 1)이 숫자 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-645">ACOS(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="63072-646">반환 hello 각도 라디안 코사인이 hello 지정 된 숫자 식입니다. 아크코사인이 라고도합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="63072-647">ASIN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="63072-648">사인이 hello 라디안 단위로 반환 hello 각도 숫자 식 지정.</span><span class="sxs-lookup"><span data-stu-id="63072-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="63072-649">아크사인이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="63072-650">ATAN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="63072-651">반환 hello 각도 라디안의 탄젠트는 hello 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="63072-652">아크탄젠트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="63072-653">ATN2(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="63072-654">반환 hello hello 양의 x 축 (y, x) hello 시작 toohello 지점부터 hello 광선 사이의 라디안 단위의 각도, 여기서 x와 y는 hello의 hello 값 지정한 두 float 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="63072-655">COS(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="63072-656">반환 hello hello의 삼각 코사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="63072-657">COT(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="63072-658">반환 hello hello의 삼각 코탄젠트 각도 라디안에서으로 지정 된, hello에 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="63072-659">DEGREES(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="63072-660">반환 hello 해당 각도에서 라디안에서으로 지정 된 각도의 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="63072-661">PI()</span><span class="sxs-lookup"><span data-stu-id="63072-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="63072-662">반환 hello PI의 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="63072-663">RADIANS(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="63072-664">숫자 식을 단위로 입력하면 라디안을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="63072-665">SIN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="63072-666">반환 hello hello의 삼각 사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="63072-667">TAN(num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="63072-668">Hello에 hello 입력된 식의 반환 hello 탄젠트 값을 지정 된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="63072-669">예를 들어 hello 다음과 같은 쿼리 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="63072-670">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="63072-671">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-671">**Results**</span></span>

    [4]

<span data-ttu-id="63072-672">Cosmos DB 비교 함수 tooANSI SQL 간의 주요 차이점 hello는 스키마 없음 및 혼합 스키마 데이터와 잘 설계 된 toowork 이들이 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="63072-673">예를 들어 여기서 hello 크기 속성이 없거나에 문서가 있는 경우 숫자가 아닌 값에 "알 수 없음"와 같은 다음 오류를 반환 하는 대신, hello 문서를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="63072-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="63072-674">형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="63072-674">Type checking functions</span></span>
<span data-ttu-id="63072-675">hello 형식 검사 함수는 toocheck hello 유형의 SQL 쿼리 내에서 식 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="63072-676">형식 검사 함수 수 변수 또는 알 수 없는 경우 hello 신속 하 게 toodetermine hello 유형의 문서 내에서 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="63072-677">다음은 지원되는 기본 제공 형식 검사 함수 표입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="63072-678"><strong>사용 현황</strong></span><span class="sxs-lookup"><span data-stu-id="63072-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="63072-679"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="63072-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-681">Hello 유형의 hello 값 배열 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-683">Hello 값의 hello 형식이 부울 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-685">Hello 유형의 hello 값이 null 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-687">Hello 유형의 hello 값이 숫자 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-689">Hello 유형의 hello 값은 JSON 개체 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-691">Hello 유형의 hello 값 문자열 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-693">경우 hello 속성 값이 할당에 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="63072-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="63072-695">Hello 유형의 hello 값 문자열, 숫자, 부울 또는 null 인지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="63072-696">이러한 함수를 사용 하 여 hello 다음과 같은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="63072-697">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="63072-698">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="63072-699">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="63072-699">String functions</span></span>
<span data-ttu-id="63072-700">hello 다음 스칼라 함수는 문자열 입력된 값에 대 한 작업을 수행 하 고 문자열, 숫자 또는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="63072-701">기본 제공 문자열 함수의 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="63072-702">사용 현황</span><span class="sxs-lookup"><span data-stu-id="63072-702">Usage</span></span> | <span data-ttu-id="63072-703">설명</span><span class="sxs-lookup"><span data-stu-id="63072-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="63072-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="63072-705">지정 된 문자열 식의 hello 문자의 hello 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="63072-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="63072-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="63072-707">않은 hello 두 개 이상의 문자열 값을 연결한 결과인 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="63072-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="63072-709">문자열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="63072-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="63072-711">끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="63072-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="63072-713">끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="63072-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="63072-715">첫 번째 문자열 식 hello hello를 두 번째로 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="63072-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="63072-717">Hello hello 문자열을 찾을 수 없는 경우 시작 hello hello hello 첫 번째 지정 된 문자열 식 또는-1 내에서 두 번째 문자열 식의 첫 번째 발생 위치를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="63072-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="63072-719">반환 문자열의 왼쪽된 부분을 지정 하는 hello로 hello 문자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="63072-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="63072-721">Hello로 반환 hello 오른쪽 부분 문자열의 문자 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="63072-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="63072-723">선행 공백을 제거한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="63072-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="63072-725">후행 공백을 잘라낸 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="63072-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="63072-727">대문자 데이터 toolowercase 변환한 후 문자열 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="63072-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="63072-729">소문자 데이터 toouppercase 변환한 후 문자열 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="63072-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="63072-731">지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63072-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="63072-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="63072-733">문자열 값을 지정한 횟수 만큼 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="63072-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="63072-735">Hello는 문자열 값의 역순을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="63072-736">이러한 함수를 사용 하 여 hello 다음과 같은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="63072-737">예를 들어 다음과 같이 대문자로 hello 제품군 이름을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="63072-738">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="63072-739">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="63072-740">또는 이 예제와 같이 문자열을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="63072-741">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="63072-742">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="63072-743">문자열 함수 사용할 수도 있습니다 hello에 절 toofilter 결과 hello 다음 예제에서에서와 같이 하는 위치:</span><span class="sxs-lookup"><span data-stu-id="63072-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="63072-744">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="63072-745">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="63072-746">배열 함수</span><span class="sxs-lookup"><span data-stu-id="63072-746">Array functions</span></span>
<span data-ttu-id="63072-747">다음 스칼라 함수 hello는 배열 입력된 값 및 반환 숫자, 부울 또는 배열 값에 대 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="63072-748">기본 제공 배열 함수의 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="63072-749">사용 현황</span><span class="sxs-lookup"><span data-stu-id="63072-749">Usage</span></span> | <span data-ttu-id="63072-750">설명</span><span class="sxs-lookup"><span data-stu-id="63072-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="63072-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="63072-752">배열 식을 지정 하는 hello 요소의 hello 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="63072-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="63072-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="63072-754">hello가 두 개 이상의 배열 값을 연결한 결과인 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="63072-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="63072-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="63072-756">값을 지정 하는 hello hello 배열에 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="63072-757">전체 또는 일부 경우 hello 일치는 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="63072-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="63072-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="63072-759">배열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="63072-760">배열 함수에는 JSON 내에서 사용 되는 toomanipulate 배열 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="63072-761">예를 들어 여기에 "로빈 Wakefield" hello 부모 항목 중 하나가 모든 문서를 반환 하는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="63072-762">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="63072-763">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="63072-764">Hello 배열 내에서 일치 하는 요소에 대 한 부분 일부분을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="63072-765">hello 다음 쿼리에서 찾습니다 hello로 모든 부모 `givenName` 의 `Robin`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="63072-766">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="63072-767">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="63072-768">패밀리당 자녀 수가 tooget hello ARRAY_LENGTH를 사용 하는 또 다른 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="63072-769">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="63072-770">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="63072-771">공간 함수</span><span class="sxs-lookup"><span data-stu-id="63072-771">Spatial functions</span></span>
<span data-ttu-id="63072-772">Cosmos DB hello Open Geospatial Consortium (OGC) 기본 제공 함수를 쿼리 하는 지리 공간에 대 한 다음을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="63072-773"><strong>사용 현황</strong></span><span class="sxs-lookup"><span data-stu-id="63072-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="63072-774"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="63072-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="63072-776">두 hello GeoJSON 지점, 다각형 또는 LineString 식 사이의 hello 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="63072-778">Hello 첫 번째 GeoJSON 개체 (점, 다각형, 또는 LineString) hello 두 번째 GeoJSON 개체 (점, 다각형, 또는 LineString) 이내 인지 여부를 나타내는 부울 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-779">ST_INTERSECTS(spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="63072-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="63072-780">Hello 지정 된 두 GeoJSON 개체 (점, 다각형, 또는 LineString) 교차 하는지 여부를 나타내는 부울 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="63072-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="63072-782">Hello GeoJSON 지점, 다각형 또는 LineString 식이 유효한 경우이 지정 되었는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="63072-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="63072-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="63072-784">Hello GeoJSON 지점, 다각형 또는 LineString 식이 지정 된 경우 부울 값을 포함 하는 JSON 값은 유효 하 고, 잘못 된 경우에 문자열 값으로 이유 hello 또한 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="63072-785">공간 함수에는 공간 데이터에 대 한 사용된 tooperform 근접 쿼리 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="63072-786">예를 들어 여기에 모든 제품군에 설명 하의 hello 30 km 내에서 지정 된 위치 사용 하는 hello ST_DISTANCE 기본 제공 함수를 반환 하는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="63072-787">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="63072-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="63072-788">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="63072-789">Cosmos DB의 지리 공간 지원에 대한 자세한 내용은 [Azure Cosmos DB에서 지리 공간 데이터 작업](geospatial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63072-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="63072-790">Cosmos DB에 대 한 SQL 구문 hello 및 공간 함수를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="63072-791">이제 어떻게 작동 hello 구문을 사용 하 여 상호 작용 하는 방법 및 쿼리 LINQ 살펴본 지금까지에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="63072-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="63072-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="63072-793">LINQ는 개체 스트림에 대한 쿼리로 계산을 표현하는 .NET 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="63072-794">Cosmos DB JSON 및.NET 개체 사이의 변환은 촉진 하 여 LINQ 통한 클라이언트 쪽 라이브러리 toointerface를 제공 하 고 LINQ의 하위 집합에서의 매핑 tooCosmos DB 쿼리를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="63072-795">아래 hello 그림 Cosmos DB를 사용 하 여 LINQ 쿼리를 지 원하는 hello 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63072-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="63072-796">Cosmos DB 클라이언트 hello를 사용 하 여 개발자가 만들 수는 **IQueryable** 개체 쿼리 hello Cosmos DB 쿼리 공급자, 직접 그러면 Cosmos DB 쿼리로 hello LINQ 쿼리를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="63072-797">hello 쿼리 toohello Cosmos DB 서버 tooretrieve 결과 집합을 JSON 형식으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="63072-798">hello 스트림으로 hello 클라이언트 쪽에서.NET 개체의 역직렬화 된 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![DocumentDB API를 사용한 LINQ 쿼리를 지원하는 아키텍처 - SQL 구문, JSON 쿼리 언어, 데이터베이스 개념 및 SQL 쿼리][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="63072-800">.NET 및 JSON 매핑</span><span class="sxs-lookup"><span data-stu-id="63072-800">.NET and JSON mapping</span></span>
<span data-ttu-id="63072-801">.NET 개체와 JSON 문서 간의 hello 매핑은 자연-각 데이터 멤버 필드 매핑된 tooa JSON 개체, 여기서는 hello 필드 이름이 hello 개체의 "키" 일부 toohello 매핑되고 hello "value" 부분은 hello 개체의 매핑된 재귀적으로 toohello 값 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="63072-802">다음 예제는 hello는 것이 좋습니다: 아래 표시 된 대로 만든 hello 제품군 개체는 매핑된 toohello JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="63072-803">및 그 반대로 hello JSON 문서는 매핑된 백 tooa.NET 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="63072-804">**C# 클래스**</span><span class="sxs-lookup"><span data-stu-id="63072-804">**C# Class**</span></span>

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


<span data-ttu-id="63072-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="63072-805">**JSON**</span></span>  

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



### <a name="linq-toosql-translation"></a><span data-ttu-id="63072-806">LINQ tooSQL 변환</span><span class="sxs-lookup"><span data-stu-id="63072-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="63072-807">LINQ 쿼리에서 최상의 노력 매핑 Cosmos DB SQL 쿼리를 수행 하는 hello Cosmos DB 쿼리 공급자 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="63072-808">Hello 설명 뒤, hello 판독기에 LINQ에 대 한 기본 지식이 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="63072-809">첫째, hello 형식 시스템에 대 한 모든 JSON 기본 형식 – 숫자 형식, 부울, 문자열 및 null 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="63072-810">이러한 JSON 형식만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-810">Only these JSON types are supported.</span></span> <span data-ttu-id="63072-811">스칼라 식은 다음 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="63072-812">상수 값-hello 쿼리가 평가 되는 hello 시 hello 기본 데이터 형식의 상수 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="63072-813">속성/배열 인덱스 식 – 이러한 식 toohello 속성을 개체 또는 배열 요소를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="63072-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="63072-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span><span class="sxs-lookup"><span data-stu-id="63072-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="63072-815">산술 식 - 숫자 및 부울 값에 대한 일반 산술 식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="63072-816">Hello 전체 목록을 보려면 toohello SQL specification을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="63072-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="63072-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="63072-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="63072-818">문자열 비교 식-여기에 문자열 값 toosome 상수 문자열 값을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="63072-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span><span class="sxs-lookup"><span data-stu-id="63072-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="63072-820">개체/배열 만들기 식 - 복합 값 형식 또는 무명 형식의 개체나 이러한 개체의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="63072-821">해당 값을 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-821">These values can be nested.</span></span>
  
     <span data-ttu-id="63072-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span><span class="sxs-lookup"><span data-stu-id="63072-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="63072-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="63072-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="63072-824"><a id="SupportedLinqOperators"></a>지원되는 LINQ 연산자 목록</span><span class="sxs-lookup"><span data-stu-id="63072-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="63072-825">다음은 hello DocumentDB.NET SDK에 포함 된 hello LINQ 공급자에서 지원 되는 LINQ 연산자의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="63072-826">**선택**: 프로젝션 toohello SQL 개체 생성을 포함 하 여 선택 변환</span><span class="sxs-lookup"><span data-stu-id="63072-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="63072-827">**여기서**: 필터 toohello SQL WHERE 및 간의 변환을 지원 & &, | | 및!</span><span class="sxs-lookup"><span data-stu-id="63072-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="63072-828">toohello SQL 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-828">toohello SQL operators</span></span>
* <span data-ttu-id="63072-829">**SelectMany**: 배열 toohello SQL JOIN 절을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="63072-830">배열 요소에 대해 사용 되는 toochain/중첩 식은 toofilter 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="63072-831">**OrderBy 및 OrderByDescending**: tooORDER BY 오름차순/내림차순으로 변환</span><span class="sxs-lookup"><span data-stu-id="63072-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="63072-832">집계를 위한 **Count**, **Sum**, **Min**, **Max** 및 **Average** 연산자와 해당 비동기 동급 연산자 **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** 및 **AverageAsync**</span><span class="sxs-lookup"><span data-stu-id="63072-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="63072-833">**CompareTo**: toorange 비교로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="63072-834">.NET에서 비교 불가능하므로 문자열에 대해 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="63072-835">**라인**: toohello SQL TOP 쿼리 결과 제한 하기 위한 변환</span><span class="sxs-lookup"><span data-stu-id="63072-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="63072-836">**수치 연산 함수**:에서 변환만 지원 합니다. NET의 Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, 로그, Log10, Pow, 라운드, Sign, Sin, Sqrt, Tan, toohello 동등한 SQL 기본 제공 함수를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="63072-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="63072-837">**문자열 함수**:에서 변환만 지원 합니다. NET의 Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, 역방향, TrimEnd, StartsWith, SubString, ToUpper toohello 동등한 SQL 기본 제공 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="63072-838">**배열 함수**:에서 변환만 지원 합니다. NET의 Concat, Contains 및 Count toohello 동등한 SQL 기본 제공 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="63072-839">**지리 공간 확장 함수**: IsValid, 내에서 거리 스텁 메서드에서 변환만 지원 및 IsValidDetailed toohello 동등한 SQL 기본 제공 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="63072-840">**사용자 정의 함수 확장 함수**: hello에서 지 원하는 변환 스텁 메서드 UserDefinedFunctionProvider.Invoke toohello 해당 사용자 정의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="63072-841">**기타**: hello의 번역 coalesce 지원 하 고 조건부 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="63072-842">Contains tooString를 가져올 수 있습니다. CONTAINS, ARRAY_CONTAINS, 또는 컨텍스트에 따라 SQL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="63072-843">SQL 쿼리 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-843">SQL query operators</span></span>
<span data-ttu-id="63072-844">다음은 일부 hello LINQ 표준 쿼리 연산자 변환 되는 방법을 tooCosmos DB 쿼리를 보여 주는 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="63072-845">Select 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-845">Select Operator</span></span>
<span data-ttu-id="63072-846">hello 구문은 `input.Select(x => f(x))`여기서 `f` 스칼라 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="63072-847">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="63072-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="63072-849">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="63072-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="63072-851">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="63072-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="63072-853">SelectMany 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-853">SelectMany operator</span></span>
<span data-ttu-id="63072-854">hello 구문은 `input.SelectMany(x => f(x))`여기서 `f` 컬렉션 형식을 반환 하는 스칼라 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="63072-855">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="63072-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="63072-857">Where 연산자</span><span class="sxs-lookup"><span data-stu-id="63072-857">Where operator</span></span>
<span data-ttu-id="63072-858">hello 구문은 `input.Where(x => f(x))`여기서 `f` 부울 값을 반환 하는 스칼라 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="63072-859">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="63072-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="63072-861">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="63072-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="63072-863">복합 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="63072-863">Composite SQL queries</span></span>
<span data-ttu-id="63072-864">hello 연산자 위에 구성 된 tooform 더 강력한 쿼리가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="63072-865">Cosmos DB 중첩된 컬렉션을 지 원하는 이후 hello 컴퍼지션 수 연결 하거나 중첩 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="63072-866">연결</span><span class="sxs-lookup"><span data-stu-id="63072-866">Concatenation</span></span>
<span data-ttu-id="63072-867">hello 구문은 `input(.|.SelectMany())(.Select()|.Where())*`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="63072-868">연결된 쿼리는 선택적 `SelectMany` 쿼리로 시작하며 그 뒤에 여러 `Select` 또는 `Where` 연산자가 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="63072-869">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="63072-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="63072-871">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="63072-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="63072-873">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="63072-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="63072-875">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="63072-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="63072-877">중첩</span><span class="sxs-lookup"><span data-stu-id="63072-877">Nesting</span></span>
<span data-ttu-id="63072-878">hello 구문은 `input.SelectMany(x=>x.Q())` 여기서 Q는는 `Select`, `SelectMany`, 또는 `Where` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="63072-879">중첩 쿼리에서 hello 내부 쿼리에 적용 된 tooeach 요소 hello 외부 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="63072-880">중요 한 기능은 hello 내부 쿼리 하는 hello와 같은 외부 컬렉션에 있는 hello 요소의 toohello 필드를 참조할 수 있습니다 하나 자체 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="63072-881">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="63072-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="63072-883">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="63072-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="63072-885">**LINQ 람다 식**</span><span class="sxs-lookup"><span data-stu-id="63072-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="63072-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="63072-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="63072-887"><a id="ExecutingSqlQueries"></a>SQL 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="63072-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="63072-888">Cosmos DB는 HTTP/HTTPS 요청을 수행할 수 있는 임의의 언어로 호출할 수 있는 REST API를 통해 리소스를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="63072-889">또한 Cosmos DB는 .NET, Node.js, JavaScript, Python 등 많이 사용되는 여러 언어를 위한 프로그래밍 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="63072-890">hello REST API 및 hello 모든 다양 한 라이브러리를 통해 SQL 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="63072-891">.NET SDK hello LINQ tooSQL 또한 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="63072-892">예제에서는 보여 방법을 다음 hello toocreate 쿼리 및 Cosmos DB 데이터베이스 계정에 대해 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="63072-893"><a id="RestAPI"></a>REST API</span><span class="sxs-lookup"><span data-stu-id="63072-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="63072-894">Cosmos DB는 HTTP를 통해 개방형 RESTful 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="63072-895">Azure 구독을 사용하여 데이터베이스 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="63072-896">hello Cosmos DB 리소스 모델 되는 논리적이 고 안정적인 URI를 사용 하 여에 접근할 수 있으며 각 데이터베이스 계정 내 리소스의 집합으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="63072-897">리소스 집합은 참조 tooas이이 문서에 피드.</span><span class="sxs-lookup"><span data-stu-id="63072-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="63072-898">데이터베이스 계정은 각각 여러 컬렉션을 포함하는 데이터베이스 집합으로 구성되고, 각 컬렉션에는 문서, UDF 및 기타 리소스 유형이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="63072-899">hello 기본 상호 작용 모델 이러한 리소스와은 hello HTTP 동사를 통해 GET, PUT, POST 및 DELETE의 표준 해석을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="63072-900">새 리소스를 만들기 위한, 저장된 프로시저 실행을 위한 또는 Cosmos DB 쿼리 실행에 대 한 hello POST 동사가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="63072-901">쿼리는 항상 파생 작업이 없는 읽기 전용 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="63072-902">hello 다음 예제에서는 지금까지 검토 했으므로 hello 두 예제 문서를 포함 하는 컬렉션에 대 한 DocumentDB API 쿼리에 대 한 POST</span><span class="sxs-lookup"><span data-stu-id="63072-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="63072-903">hello 쿼리는 간단한 필터를 hello JSON name 속성에 증가 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="63072-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="63072-904">Hello hello 사용 `x-ms-documentdb-isquery` 및 콘텐츠-유형: `application/query+json` 작업 hello 헤더 toodenote는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="63072-905">**요청**</span><span class="sxs-lookup"><span data-stu-id="63072-905">**Request**</span></span>

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


<span data-ttu-id="63072-906">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-906">**Results**</span></span>

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


<span data-ttu-id="63072-907">두 번째 예에서는 hello hello 조인에서 여러 결과 반환 하는 보다 복잡 한 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63072-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="63072-908">**요청**</span><span class="sxs-lookup"><span data-stu-id="63072-908">**Request**</span></span>

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


<span data-ttu-id="63072-909">**결과**</span><span class="sxs-lookup"><span data-stu-id="63072-909">**Results**</span></span>

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


<span data-ttu-id="63072-910">쿼리 결과의 결과 단일 페이지에 들어갈 수 없는 경우 hello REST API를 통해 hello 연속 토큰도 반환 `x-ms-continuation-token` 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="63072-911">클라이언트는 후속 결과에 hello 헤더를 포함 하 여 결과 페이지를 매기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="63072-912">hello를 통해 hello 페이지당 결과 수를 제어할 수도 있습니다 `x-ms-max-item-count` 번호 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="63072-913">지정 된 쿼리에 hello와 같은 집계 함수 있으면 `COUNT`, hello 쿼리 페이지 hello 결과 페이지를 통해 부분적으로 집계 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="63072-914">hello 클라이언트는 이러한 결과 tooproduce hello 최종 결과, 예를 들어 두 번째 수준의 집계를 수행 해야, hello 개수 hello 개별 페이지 tooreturn hello 총 개수에 반환 된 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="63072-915">쿼리를 사용 하 여 hello에 대 한 toomanage hello 데이터 일관성 정책을 `x-ms-consistency-level` 같은 REST API에 대 한 모든 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="63072-916">세션 일관성을 위해 그는 필요한 tooalso 에코 hello 최신 `x-ms-session-token` hello 쿼리 요청에 쿠키 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="63072-917">hello 쿼리 된 컬렉션의 인덱싱 정책을 영향을 줄 수 쿼리 결과의 hello 일관성.</span><span class="sxs-lookup"><span data-stu-id="63072-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="63072-918">Hello 기본 인덱싱 정책 설정, 사용 하 여 컬렉션에 대 한 hello 인덱스는 항상 최신 hello 문서 목차, 쿼리 결과 데이터에 대해 선택한 hello 일관성 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="63072-919">인덱싱 정책을 hello 상대적으로 느 tooLazy 이면 쿼리는 유효 하지 않은 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="63072-920">자세한 내용은 [Azure Cosmos DB 일관성 수준][consistency-levels]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63072-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="63072-921">Hello 컬렉션에 인덱싱 정책을 구성 하는 hello hello 지정 된 쿼리를 지원 하지 않는 경우 400 "잘못 된 요청" hello Azure Cosmos DB 서버에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="63072-922">해시(같음) 조회에 구성된 경로 및 인덱싱에서 명시적으로 제외된 경로의 범위 쿼리에 대해 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="63072-923">hello `x-ms-documentdb-query-enable-scan` 헤더 인덱스를 사용할 수 없는 경우 지정 된 tooallow hello 쿼리 tooperform 검색 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="63072-924">설정 하 여 쿼리 실행에 자세한 메트릭을 가져올 수 `x-ms-documentdb-populatequerymetrics` 헤더 너무`True`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="63072-925">자세한 내용은 [Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리 메트릭](documentdb-sql-query-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63072-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="63072-926"><a id="DotNetSdk"></a>C#(.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="63072-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="63072-927">LINQ와 SQL 모두 hello.NET SDK 지원 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="63072-928">hello 다음 예제에서는이 문서의 앞부분에서 tooperform hello 간단한 필터 쿼리 도입 하는 방법</span><span class="sxs-lookup"><span data-stu-id="63072-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="63072-929">이 샘플은 각 문서 내에서 두 속성이 같은지 비교하고 익명 프로젝션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="63072-930">hello 다음 샘플에서는 LINQ SelectMany 통해 명시 된 조인 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63072-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="63072-931">.NET 클라이언트 hello 위와 같이 hello foreach 블록의 쿼리 결과의 모든 hello 페이지를 자동으로 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="63072-932">hello REST API 섹션에에서 추가 된 옵션에 사용할 수도 있습니다. hello 쿼리 hello hello를 사용 하 여.NET SDK `FeedOptions` 및 `FeedResponse` hello CreateDocumentQuery 메서드의에서 클래스.</span><span class="sxs-lookup"><span data-stu-id="63072-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="63072-933">hello를 사용 하 여 hello 페이지 수를 제어할 수 있습니다 `MaxItemCount` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="63072-934">만들어 페이징을 명시적으로 제어할 수 있습니다 `IDocumentQueryable` hello를 사용 하 여 `IQueryable` 참조 하 여 다음 개체는` ResponseContinuationToken` 값 전달 하는 것으로 다시 `RequestContinuationToken` 에서 `FeedOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="63072-935">`EnableScanInQuery`인덱싱 정책을 구성 하는 hello에서 hello 쿼리를 지원할 수 없는 경우에 집합 tooenable 검색이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="63072-936">분할 된 컬렉션에 대 한 사용할 수 있습니다 `PartitionKey` toorun hello 쿼리는 단일에 대해 (하지만 Cosmos DB을 자동으로 추출이 hello 쿼리 텍스트에서)를 분할 하 고 `EnableCrossPartitionQuery` toobe 필요할 수 있는 toorun 쿼리를 여러 파티션에 대해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="63072-937">너무 참조[Azure Cosmos DB.NET 샘플](https://github.com/Azure/azure-documentdb-net) 쿼리를 포함 하는 추가 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="63072-938"><a id="JavaScriptServerSideApi"></a>JavaScript 서버 쪽 API</span><span class="sxs-lookup"><span data-stu-id="63072-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="63072-939">Cosmos DB 저장된 프로시저 및 트리거를 사용 하 여 hello 컬렉션에 직접 JavaScript 기반 응용 프로그램 논리를 실행 하기 위한 프로그래밍 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="63072-940">컬렉션 수준에서 등록 하는 hello JavaScript 논리 데이터베이스 작업의 컬렉션을 제공 하는 hello hello 문서에 대 한 hello 작업에 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63072-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="63072-941">해당 작업은 앰비언트 ACID 트랜잭션에 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="63072-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="63072-942">hello 다음 예제에서는 JavaScript 서버 API hello toomake에서 toouse hello queryDocuments에서 쿼리 하는 방법을 내부 저장 프로시저와 트리거의 합니다.</span><span class="sxs-lookup"><span data-stu-id="63072-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

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

## <span data-ttu-id="63072-943"><a id="References"></a>참조</span><span class="sxs-lookup"><span data-stu-id="63072-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="63072-944">[소개 tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="63072-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="63072-945">Azure Cosmos DB SQL 사양</span><span class="sxs-lookup"><span data-stu-id="63072-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="63072-946">Azure Cosmos DB .NET 샘플</span><span class="sxs-lookup"><span data-stu-id="63072-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="63072-947">[Azure Cosmos DB 일관성 수준][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="63072-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="63072-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="63072-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="63072-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="63072-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="63072-950">Javascript 사양 [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="63072-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="63072-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="63072-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="63072-952">대형 데이터베이스에 대한 쿼리 평가 기술 [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="63072-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="63072-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="63072-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="63072-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="63072-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="63072-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="63072-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="63072-956">G.</span><span class="sxs-lookup"><span data-stu-id="63072-956">G.</span></span> <span data-ttu-id="63072-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="63072-957">Graefe.</span></span> <span data-ttu-id="63072-958">쿼리 최적화에 대 한 hello 단계적 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="63072-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="63072-959">IEEE 데이터 Eng.</span><span class="sxs-lookup"><span data-stu-id="63072-959">IEEE Data Eng.</span></span> <span data-ttu-id="63072-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="63072-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md