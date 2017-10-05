---
title: "Azure Cosmos DB DocumentDB API: SQL 구문 | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API SQL 쿼리 언어에 대한 참조 설명서입니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="dda46-103">Azure Cosmos DB DocumentDB API: SQL 구문 참조</span><span class="sxs-lookup"><span data-stu-id="dda46-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="dda46-104">Azure Cosmos DB DocumentDB API는 명시적 스키마를 요구하거나 보조 인덱스를 만들지 않고 계층적 JSON 문서에 대한 문법과 같은 익숙한 SQL(구조적 쿼리 언어)을 사용하여 문서를 쿼리하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="dda46-105">이 항목에서는 DocumentDB API SQL 쿼리 언어에 대한 참조 설명서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="dda46-106">DocumentDB API SQL 쿼리 언어에 대한 설명은 [Azure Cosmos DB DocumentDB API에 대한 SQL 쿼리](documentdb-sql-query.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="dda46-107">또한 [Query Playground](http://www.documentdb.com/sql/demo)도 방문하여 Azure Cosmos DB를 체험하고 데이터 집합에 대해 SQL 쿼리를 실행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="dda46-108">SELECT 쿼리</span><span class="sxs-lookup"><span data-stu-id="dda46-108">SELECT query</span></span>  
<span data-ttu-id="dda46-109">데이터베이스에서 JSON 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="dda46-110">식 평가, 프로젝션, 필터링 및 조인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="dda46-111">SELECT 문을 설명하는 데 사용되는 규칙은 구문 규칙 섹션에서 표로 작성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="dda46-112">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="dda46-113">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-113">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-114">각 절에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="dda46-115">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="dda46-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="dda46-116">FROM 절</span><span class="sxs-lookup"><span data-stu-id="dda46-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="dda46-117">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="dda46-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="dda46-118">ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="dda46-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="dda46-119">SELECT 문의 절은 위에서 표시한 순서대로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="dda46-120">선택적 절 중 하나는 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="dda46-121">그러나 선택적 절이 사용되면 올바른 순서로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="dda46-122">**SELECT 문의 논리적 처리 순서**</span><span class="sxs-lookup"><span data-stu-id="dda46-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="dda46-123">절이 처리되는 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="dda46-124">FROM 절</span><span class="sxs-lookup"><span data-stu-id="dda46-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="dda46-125">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="dda46-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="dda46-126">ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="dda46-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="dda46-127">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="dda46-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="dda46-128">이 순서는 구문에 표시되는 순서와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="dda46-129">순서를 지정하면 처리된 절에서 도입된 새로운 모든 기호가 표시되고, 나중에 처리되는 절에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="dda46-130">예를 들어 FROM 절에 선언된 별칭은 WHERE 절과 SELECT 절에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="dda46-131">**공백 문자 및 주석**</span><span class="sxs-lookup"><span data-stu-id="dda46-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="dda46-132">따옴표가 붙은 문자열이나 식별자의 일부가 아닌 모든 공백 문자는 언어 문법의 일부가 아니며 구문 분석에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="dda46-133">쿼리 언어는 다음과 같은 T-SQL 스타일 주석을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="dda46-134">`-- comment text [newline]` SQL 문</span><span class="sxs-lookup"><span data-stu-id="dda46-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="dda46-135">공백 문자와 주석은 문법에서 아무런 의미가 없지만 토큰을 분리하는 데 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="dda46-136">예를 들어 `-1e5`는 단일 숫자 토큰이지만, `: – 1 e5`는 숫자 1과 식별자 e5가 뒤에 나오는 마이너스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="dda46-137"><a name="bk_select_query"></a> SELECT 절</span><span class="sxs-lookup"><span data-stu-id="dda46-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="dda46-138">SELECT 문의 절은 위에서 표시한 순서대로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="dda46-139">선택적 절 중 하나는 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="dda46-140">그러나 선택적 절이 사용되면 올바른 순서로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="dda46-141">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="dda46-142">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="dda46-143">결과 집합에 대해 선택되는 속성 또는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="dda46-144">변경하지 않고 값을 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="dda46-145">특히 처리된 값이 개체이면 모든 속성이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="dda46-146">검색할 속성의 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="dda46-147">반환된 각 값은 지정된 속성이 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="dda46-148">완전한 JSON 개체 대신 JSON 값을 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="dda46-149">이것은 `<property_list>`와 달리 개체에 프로젝션된 값을 래핑하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="dda46-150">계산할 값을 나타내는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="dda46-151">자세한 내용은 [스칼라 식](#bk_scalar_expressions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="dda46-152">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-152">**Remarks**</span></span>  
  
<span data-ttu-id="dda46-153">`SELECT *` 구문은 FROM 절에서 정확히 하나의 별칭을 선언한 경우에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="dda46-154">`SELECT *`는 ID 프로젝션을 제공하며, 이는 프로젝션이 필요하지 않은 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="dda46-155">SELECT *는 FROM 절이 지정되고 단일 입력 원본만 도입된 경우에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="dda46-156">`SELECT <select_list>`과 `SELECT *`는 "syntactic sugar(구문적 설탕)"이며 다음과 같이 간단한 SELECT 문을 사용하여 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="dda46-157">이는 다음과 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="dda46-158">이는 다음과 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="dda46-159">**참고 항목**</span><span class="sxs-lookup"><span data-stu-id="dda46-159">**See Also**</span></span>  
  
[<span data-ttu-id="dda46-160">스칼라 식</span><span class="sxs-lookup"><span data-stu-id="dda46-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="dda46-161">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="dda46-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="dda46-162"><a name="bk_from_clause"></a> FROM 절</span><span class="sxs-lookup"><span data-stu-id="dda46-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="dda46-163">원본 또는 조인된 원본을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="dda46-164">FROM 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-164">The FROM clause is optional.</span></span> <span data-ttu-id="dda46-165">지정하지 않으면 FROM 절에서 단일 문서를 제공하는 것처럼 다른 절도 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="dda46-166">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-166">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="dda46-167">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="dda46-168">별칭이 있거나 없는 데이터 원본을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="dda46-169">별칭을 지정하지 않으면 다음 규칙을 사용하여 `<collection_expression>`에서 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="dda46-170">식이 collection_name이면 collection_name이 별칭으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="dda46-171">식이 `<collection_expression>`이면 property_name이 별칭으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="dda46-172">식이 collection_name이면 collection_name이 별칭으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="dda46-173">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="dda46-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="dda46-174">`input_alias`가 기본 컬렉션 식에서 반환되는 값 집합임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="dda46-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="dda46-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="dda46-176">`input_alias`가 기본 컬렉션 식에서 반환되는 각 배열의 모든 배열 요소를 반복하여 얻는 값 집합을 나타내도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="dda46-177">배열이 아닌 기본 컬렉션 식에서 반환되는 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="dda46-178">문서를 검색하는 데 사용할 컬렉션 식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="dda46-179">현재 연결된 기본 컬렉션에서 문서를 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="dda46-180">제공된 컬렉션에서 문서를 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="dda46-181">컬렉션의 이름은 현재 연결된 컬렉션의 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="dda46-182">제공된 별칭으로 정의된 다른 원본에서 문서를 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="dda46-183">지정된 컬렉션 식으로 검색된 모든 문서에 대해 `property_name` 속성 또는 array_index 배열 요소에 액세스하여 문서를 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="dda46-184">지정된 컬렉션 식으로 검색된 모든 문서에 대해 `property_name` 속성 또는 array_index 배열 요소에 액세스하여 문서를 검색하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="dda46-185">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-185">**Remarks**</span></span>  
  
<span data-ttu-id="dda46-186">`<from_source>(`에서 제공되거나 유추되는 모든 별칭은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="dda46-187">`<collection_expression>.`property_name 구문은 `<collection_expression>' ['"property_name"']'`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="dda46-188">그러나 속성 이름에 비식별자 문자가 포함되어 있으면 후자의 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="dda46-189">**누락된 속성, 누락된 배열 요소, 정의되지 않은 값 처리**</span><span class="sxs-lookup"><span data-stu-id="dda46-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="dda46-190">컬렉션 식에서 속성이나 배열 요소에 액세스하고 해당 값이 존재하지 않으면 이 값은 무시되고 더 이상 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="dda46-191">**컬렉션 식 컨텍스트 범위 지정**</span><span class="sxs-lookup"><span data-stu-id="dda46-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="dda46-192">컬렉션 식은 컬렉션 범위 또는 문서 범위일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="dda46-193">컬렉션 식의 기본 원본이 ROOT 또는 `collection_name`이면 식은 컬렉션 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="dda46-194">이러한 식은 컬렉션에서 직접 검색되는 문서 집합을 나타내며 다른 컬렉션 식의 처리에 종속되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="dda46-195">컬렉션 식의 기본 원본이 쿼리의 앞 부분에 도입된 `input_alias`이면 식은 문서 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="dda46-196">이러한 식은 별칭 지정된 컬렉션과 연결된 집합에 속한 각 문서의 범위에서 컬렉션 식을 평가하여 얻는 문서 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="dda46-197">결과 집합은 기본 집합에 있는 각 문서에 대해 컬렉션 식을 평가하여 얻는 집합의 합집합입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="dda46-198">**조인**</span><span class="sxs-lookup"><span data-stu-id="dda46-198">**Joins**</span></span>  
  
<span data-ttu-id="dda46-199">현재 릴리스의 Azure Cosmos DB에서는 내부 조인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="dda46-200">추가 조인 기능이 곧 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="dda46-201">내부 조인은 조인에 참여하는 집합의 완전한 교차곱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="dda46-202">N 방향 조인의 결과는 N 요소 튜플의 집합이며, 여기서 튜플의 각 값은 조인에 참여하는 별칭 지정된 집합과 연결되며 다른 절에서 해당 별칭을 참조하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="dda46-203">조인 평가는 참여하는 집합의 컨텍스트 범위에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="dda46-204">컬렉션 집합 A와 컬렉션 범위 집합 B을 조인하면 집합 A와 집합 B에 있는 모든 요소의 교차곱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="dda46-205">집합 A와 문서 범위 집합 B를 조인하면 집합 A의 각 문서에 대해 문서 범위 집합 B를 평가하여 얻는 모든 집합의 합집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="dda46-206">현재 릴리스의 쿼리 프로세서에서는 컬렉션 범위가 지정된 식 하나만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="dda46-207">**조인 예제:**</span><span class="sxs-lookup"><span data-stu-id="dda46-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="dda46-208">`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>` FROM 절을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="dda46-209">각 원본에서 `input_alias1, input_alias2, …, input_aliasN`을 정의하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="dda46-210">이 FROM 절은 N 튜플(N개 값이 포함된 튜플)의 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="dda46-211">각 튜플은 해당 집합에 모든 컬렉션 별칭을 반복하여 생성된 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="dda46-212">*2개 원본이 있는 조인 예제 1:*</span><span class="sxs-lookup"><span data-stu-id="dda46-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="dda46-213">컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="dda46-214">input_alias1을 참조하는 문서 범위로 `<from_source2>`를 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="dda46-215">`input_alias1 = A,`의 경우 {1, 2}</span><span class="sxs-lookup"><span data-stu-id="dda46-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="dda46-216">`input_alias1 = B,`의 경우 {3}</span><span class="sxs-lookup"><span data-stu-id="dda46-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="dda46-217">`input_alias1 = C,`의 경우 {4, 5}</span><span class="sxs-lookup"><span data-stu-id="dda46-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="dda46-218">`<from_source1> JOIN <from_source2>` FROM 절은 다음과 같은 튜플을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="dda46-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="dda46-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="dda46-220">*3개 원본이 있는 조인 예제 2:*</span><span class="sxs-lookup"><span data-stu-id="dda46-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="dda46-221">컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="dda46-222">`input_alias1`을 참조하는 문서 범위로 `<from_source2>`를 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="dda46-223">`input_alias1 = A,`의 경우 {1, 2}</span><span class="sxs-lookup"><span data-stu-id="dda46-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="dda46-224">`input_alias1 = B,`의 경우 {3}</span><span class="sxs-lookup"><span data-stu-id="dda46-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="dda46-225">`input_alias1 = C,`의 경우 {4, 5}</span><span class="sxs-lookup"><span data-stu-id="dda46-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="dda46-226">`input_alias2`를 참조하는 문서 범위로 `<from_source3>`을 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="dda46-227">`input_alias2 = 1,`의 경우 {100, 200}</span><span class="sxs-lookup"><span data-stu-id="dda46-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="dda46-228">`input_alias2 = 3,`의 경우 {300}</span><span class="sxs-lookup"><span data-stu-id="dda46-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="dda46-229">`<from_source1> JOIN <from_source2> JOIN <from_source3>` FROM 절은 다음과 같은 튜플을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="dda46-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="dda46-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="dda46-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="dda46-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="dda46-232">`input_alias1`, `input_alias2`의 다른 값에 대한 튜플이 없으므로 `<from_source3>`에서 값을 반환하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="dda46-233">*3개 원본이 있는 조인 예제 3:*</span><span class="sxs-lookup"><span data-stu-id="dda46-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="dda46-234">컬렉션 범위로 <from_source1>을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="dda46-235">컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="dda46-236">input_alias1을 참조하는 문서 범위로 <from_source2>를 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="dda46-237">`input_alias1 = A,`의 경우 {1, 2}</span><span class="sxs-lookup"><span data-stu-id="dda46-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="dda46-238">`input_alias1 = B,`의 경우 {3}</span><span class="sxs-lookup"><span data-stu-id="dda46-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="dda46-239">`input_alias1 = C,`의 경우 {4, 5}</span><span class="sxs-lookup"><span data-stu-id="dda46-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="dda46-240">`<from_source3>`을 `input_alias1`로 범위 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="dda46-241">`input_alias2 = A,`의 경우 {100, 200}</span><span class="sxs-lookup"><span data-stu-id="dda46-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="dda46-242">`input_alias2 = C,`의 경우 {300}</span><span class="sxs-lookup"><span data-stu-id="dda46-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="dda46-243">`<from_source1> JOIN <from_source2> JOIN <from_source3>` FROM 절은 다음과 같은 튜플을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="dda46-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="dda46-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="dda46-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="dda46-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="dda46-246">이렇게 하면 `<from_source2>`와 `<from_source3>`의 범위를 모두 동일한 `<from_source1>`로 지정했기 때문에 두 원본의 교차곱을 만들고,</span><span class="sxs-lookup"><span data-stu-id="dda46-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="dda46-247">이로 인해 A 값이 있는 4개(2x2) 튜플, B 값이 있는 0개(1x0) 튜플 및 C 값이 있는 2개(2x1) 튜플을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="dda46-248">**참고 항목**</span><span class="sxs-lookup"><span data-stu-id="dda46-248">**See also**</span></span>  
  
 [<span data-ttu-id="dda46-249">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="dda46-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="dda46-250"><a name="bk_where_clause"></a> WHERE 절</span><span class="sxs-lookup"><span data-stu-id="dda46-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="dda46-251">쿼리에서 반환되는 문서에 대한 검색 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="dda46-252">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="dda46-253">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="dda46-254">반환할 문서에 대해 충족하는 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="dda46-255">계산할 값을 나타내는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="dda46-256">자세한 내용은 [스칼라 식](#bk_scalar_expressions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="dda46-257">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-257">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-258">문서를 반환하려면 필터 조건으로 지정된 식을 true로 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="dda46-259">true 부울 값만 조건을 충족하고, 다른 값(undefined, null, false, 숫자, 배열 또는 개체)은 조건을 충족하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="dda46-260"><a name="bk_orderby_clause"></a> ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="dda46-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="dda46-261">쿼리에서 반환되는 결과의 정렬 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="dda46-262">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="dda46-263">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="dda46-264">쿼리 결과 집합을 정렬할 속성이나 식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="dda46-265">정렬 열은 이름 또는 열 별칭으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="dda46-266">여러 정렬 열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="dda46-267">열 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-267">Column names must be unique.</span></span> <span data-ttu-id="dda46-268">ORDER BY 절의 정렬 열 순서는 정렬되는 결과 집합의 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="dda46-269">즉 결과 집합이 첫 번째 속성으로 정렬된 다음 정렬된 해당 목록이 두 번째 속성으로 정렬되는 등등입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="dda46-270">ORDER BY 절에서 참조되는 열 이름은 선택 목록의 열 이름 또는 FROM 절에 지정된 테이블에 정의된 열 이름과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="dda46-271">쿼리 결과 집합을 정렬할 단일 속성 또는 식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="dda46-272">자세한 내용은 [스칼라 식](#bk_scalar_expressions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="dda46-273">지정된 열의 값을 오름차순 또는 내림차순으로 정렬하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="dda46-274">ASC는 가장 낮은 값에서 가장 높은 값으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="dda46-275">DESC는 가장 높은 값에서 가장 낮은 값으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="dda46-276">ASC가 기본 정렬 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-276">ASC is the default sort order.</span></span> <span data-ttu-id="dda46-277">널 값은 가능한 가장 낮은 값으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="dda46-278">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-278">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-279">쿼리 문법은 속성 기준으로 여러 가지 순서를 지원하지만, Azure Cosmos DB 쿼리 런타임은 단일 속성에 대해서만 정렬을 지원하며, 계산된 속성이 아니라 속성 이름에 대해서만 정렬을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="dda46-280">또한 정렬하기 위해서는 인덱싱 정책에 속성에 대한 범위 인덱스와 지정된 유형이 최대 정밀도로 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="dda46-281">자세한 내용은 인덱싱 정책 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="dda46-282"><a name="bk_scalar_expressions"></a> 스칼라 식</span><span class="sxs-lookup"><span data-stu-id="dda46-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="dda46-283">스칼라 식은 단일 값을 얻기 위해 평가될 수 있는 기호와 연산자의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="dda46-284">간단한 식은 상수, 속성 참조, 배열 요소 참조, 별칭 참조 또는 함수 호출일 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="dda46-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="dda46-285">연산자를 사용하여 복잡한 식으로 결합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="dda46-286">스칼라 식에 포함될 수 있는 값에 대한 자세한 내용은 [상수](#bk_constants) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="dda46-287">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-287">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="dda46-288">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="dda46-289">상수 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-289">Represents a constant value.</span></span> <span data-ttu-id="dda46-290">자세한 내용은 [상수](#bk_constants) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="dda46-291">`FROM` 절에 도입된 `input_alias`에서 정의된 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="dda46-292">이 값은 **undefined**가 되지 않도록 보장되며, 입력에 있는 **undefined** 값은 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="dda46-293">개체의 속성 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="dda46-294">속성이 존재하지 않거나 개체가 아닌 값에서 참조되면 식이 **undefined** 값으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="dda46-295">개체/배열의 `property_name` 이름이 있는 속성 또는 `array_index` 인덱스가 있는 배열 요소의 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="dda46-296">속성/배열 인덱스가 존재하지 않거나 속성/배열이 아닌 값에서 참조되면 식이 undefined 값으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="dda46-297">단일 값에 적용되는 연산자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="dda46-298">자세한 내용은 [연산자](#bk_operators) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="dda46-299">두 값에 적용되는 연산자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="dda46-300">자세한 내용은 [연산자](#bk_operators) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="dda46-301">함수 호출의 결과로 정의되는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="dda46-302">사용자 정의 스칼라 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="dda46-303">기본 제공 스칼라 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="dda46-304">지정된 속성 및 해당 값이 포함된 새 개체를 만들어서 얻는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="dda46-305">요소로 지정된 값이 포함된 새 배열을 만들어서 얻는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="dda46-306">지정된 매개 변수 이름의 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="dda46-307">매개 변수 이름에는 첫 번째 문자로 @가 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="dda46-308">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-308">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-309">기본 제공 또는 사용자 정의 스칼라 함수를 호출할 때 모든 인수가 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="dda46-310">인수 중 하나라도 정의되지 않으면 함수가 호출되지 않고 결과가 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="dda46-311">개체를 만들 때 정의되지 않은 값이 할당된 속성은 건너뛰고 만든 개체에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="dda46-312">배열을 만들 때 **undefined** 값이 할당된 요소 값은 건너뛰고 만든 개체에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="dda46-313">이렇게 하면 건너뛴 인덱스가 만드는 배열에 포함되지 않는 방식으로 다음에 정의된 요소가 해당 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="dda46-314"><a name="bk_operators"></a> 연산자</span><span class="sxs-lookup"><span data-stu-id="dda46-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="dda46-315">이 섹션에서는 지원되는 연산자에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-315">This section describes the supported operators.</span></span> <span data-ttu-id="dda46-316">각 연산자는 정확히 하나의 범주에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="dda46-317">**undefined** 값 처리 입력 값 형식 요구 사항 및 일치하지 않는 형식의 값 처리에 대한 자세한 내용은 아래의 **연산자 범주** 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="dda46-318">**연산자 범주**</span><span class="sxs-lookup"><span data-stu-id="dda46-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="dda46-319">**범주**</span><span class="sxs-lookup"><span data-stu-id="dda46-319">**Category**</span></span>|<span data-ttu-id="dda46-320">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="dda46-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="dda46-321">**산술**</span><span class="sxs-lookup"><span data-stu-id="dda46-321">**arithmetic**</span></span>|<span data-ttu-id="dda46-322">연산자에서 입력은 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="dda46-323">출력도 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-323">Output is also a Number.</span></span> <span data-ttu-id="dda46-324">입력 중 하나가 **undefined**이거나 숫자 이외의 형식이면 결과는 **undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="dda46-325">**비트**</span><span class="sxs-lookup"><span data-stu-id="dda46-325">**bitwise**</span></span>|<span data-ttu-id="dda46-326">연산자에서 입력은 부호 있는 32비트 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="dda46-327">출력도 부호 있는 32비트 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="dda46-328">정수가 아닌 값은 끝수를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="dda46-329">양수 값은 끝수 내림되고, 음수 값은 끝수 올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="dda46-330">32비트 정수 범위를 벗어나는 값은 2의 보수 표기 중 마지막 32비트를 취하여 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="dda46-331">입력 중 하나가 **undefined**이거나 숫자 이외의 형식이면 결과는 **undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="dda46-332">**참고:** 위 동작은 JavaScript 비트 연산자 작동과 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="dda46-333">**논리**</span><span class="sxs-lookup"><span data-stu-id="dda46-333">**logical**</span></span>|<span data-ttu-id="dda46-334">연산자에서 입력은 부울이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="dda46-335">출력도 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="dda46-336">입력 중 하나가 **undefined**이거나 부울 이외의 형식이면 결과는 **undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="dda46-337">**비교**</span><span class="sxs-lookup"><span data-stu-id="dda46-337">**comparison**</span></span>|<span data-ttu-id="dda46-338">연산자에서 입력은 동일한 형식이어야 하며 undefined가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="dda46-339">출력은 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="dda46-340">입력 중 하나가 **undefined**이거나 다른 형식의 입력이면 결과는 **undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="dda46-341">값 순서 지정에 대한 자세한 내용은 **비교 연산자의 값 순서 지정** 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda46-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="dda46-342">**string**</span><span class="sxs-lookup"><span data-stu-id="dda46-342">**string**</span></span>|<span data-ttu-id="dda46-343">연산자에서 입력은 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="dda46-344">출력도 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-344">Output is also a String.</span></span><br /><span data-ttu-id="dda46-345">입력 중 하나가 **undefined**이거나 문자열 이외의 형식이면 결과는 **undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="dda46-346">**단항 연산자:**</span><span class="sxs-lookup"><span data-stu-id="dda46-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="dda46-347">**Name**</span><span class="sxs-lookup"><span data-stu-id="dda46-347">**Name**</span></span>|<span data-ttu-id="dda46-348">**연산자**</span><span class="sxs-lookup"><span data-stu-id="dda46-348">**Operator**</span></span>|<span data-ttu-id="dda46-349">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="dda46-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="dda46-350">**산술**</span><span class="sxs-lookup"><span data-stu-id="dda46-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="dda46-351">숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="dda46-352">비트 부정입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-352">Bitwise negation.</span></span> <span data-ttu-id="dda46-353">음수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="dda46-354">**비트**</span><span class="sxs-lookup"><span data-stu-id="dda46-354">**bitwise**</span></span>|~|<span data-ttu-id="dda46-355">보수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-355">Ones' complement.</span></span> <span data-ttu-id="dda46-356">숫자 값의 보수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="dda46-357">**논리**</span><span class="sxs-lookup"><span data-stu-id="dda46-357">**Logical**</span></span>|<span data-ttu-id="dda46-358">**다음이 아님**</span><span class="sxs-lookup"><span data-stu-id="dda46-358">**NOT**</span></span>|<span data-ttu-id="dda46-359">부정입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-359">Negation.</span></span> <span data-ttu-id="dda46-360">부정 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="dda46-361">**이항 연산자:**</span><span class="sxs-lookup"><span data-stu-id="dda46-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="dda46-362">**Name**</span><span class="sxs-lookup"><span data-stu-id="dda46-362">**Name**</span></span>|<span data-ttu-id="dda46-363">**연산자**</span><span class="sxs-lookup"><span data-stu-id="dda46-363">**Operator**</span></span>|<span data-ttu-id="dda46-364">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="dda46-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="dda46-365">**산술**</span><span class="sxs-lookup"><span data-stu-id="dda46-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="dda46-366">더하기</span><span class="sxs-lookup"><span data-stu-id="dda46-366">Addition.</span></span><br /><br /> <span data-ttu-id="dda46-367">빼기</span><span class="sxs-lookup"><span data-stu-id="dda46-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="dda46-368">곱하기</span><span class="sxs-lookup"><span data-stu-id="dda46-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="dda46-369">나누기</span><span class="sxs-lookup"><span data-stu-id="dda46-369">Division.</span></span><br /><br /> <span data-ttu-id="dda46-370">Modulo 연산</span><span class="sxs-lookup"><span data-stu-id="dda46-370">Modulation.</span></span>|  
|<span data-ttu-id="dda46-371">**비트**</span><span class="sxs-lookup"><span data-stu-id="dda46-371">**bitwise**</span></span>|<span data-ttu-id="dda46-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="dda46-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="dda46-373">비트 OR</span><span class="sxs-lookup"><span data-stu-id="dda46-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="dda46-374">비트 AND</span><span class="sxs-lookup"><span data-stu-id="dda46-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="dda46-375">비트 XOR</span><span class="sxs-lookup"><span data-stu-id="dda46-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="dda46-376">왼쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="dda46-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="dda46-377">오른쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="dda46-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="dda46-378">0 채우기 오른쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="dda46-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="dda46-379">**논리**</span><span class="sxs-lookup"><span data-stu-id="dda46-379">**logical**</span></span>|<span data-ttu-id="dda46-380">**및**</span><span class="sxs-lookup"><span data-stu-id="dda46-380">**AND**</span></span><br /><br /> <span data-ttu-id="dda46-381">**또는**</span><span class="sxs-lookup"><span data-stu-id="dda46-381">**OR**</span></span>|<span data-ttu-id="dda46-382">논리 결합입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-382">Logical conjunction.</span></span> <span data-ttu-id="dda46-383">두 인수가 **true**이면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-384">논리 결합입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-384">Logical conjunction.</span></span> <span data-ttu-id="dda46-385">두 인수가 **true**이면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="dda46-386">**비교**</span><span class="sxs-lookup"><span data-stu-id="dda46-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="dda46-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="dda46-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="dda46-388">**??**</span><span class="sxs-lookup"><span data-stu-id="dda46-388">**??**</span></span>|<span data-ttu-id="dda46-389">같음 -</span><span class="sxs-lookup"><span data-stu-id="dda46-389">Equals.</span></span> <span data-ttu-id="dda46-390">두 인수가 같으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-391">같지 않음 -</span><span class="sxs-lookup"><span data-stu-id="dda46-391">Not equal to.</span></span> <span data-ttu-id="dda46-392">인수가 같지 않으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-393">큼 -</span><span class="sxs-lookup"><span data-stu-id="dda46-393">Greater Than.</span></span> <span data-ttu-id="dda46-394">첫 번째 인수가 두 번째 인수보다 크면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-395">크거나 같음 -</span><span class="sxs-lookup"><span data-stu-id="dda46-395">Greater Than or Equal To.</span></span> <span data-ttu-id="dda46-396">첫 번째 인수가 두 번째 인수보다 크거나 같으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-397">작음 -</span><span class="sxs-lookup"><span data-stu-id="dda46-397">Less Than.</span></span> <span data-ttu-id="dda46-398">첫 번째 인수가 두 번째 인수보다 작으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-399">작거나 같음 -</span><span class="sxs-lookup"><span data-stu-id="dda46-399">Less Than or Equal To.</span></span> <span data-ttu-id="dda46-400">첫 번째 인수가 두 번째 인수보다 작거나 같으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="dda46-401">병합 -</span><span class="sxs-lookup"><span data-stu-id="dda46-401">Coalesce.</span></span> <span data-ttu-id="dda46-402">첫 번째 인수가 **undefined** 값이면 두 번째 인수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="dda46-403">**String**</span><span class="sxs-lookup"><span data-stu-id="dda46-403">**String**</span></span>|<span data-ttu-id="dda46-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="dda46-404">**&#124;&#124;**</span></span>|<span data-ttu-id="dda46-405">연결 -</span><span class="sxs-lookup"><span data-stu-id="dda46-405">Concatenation.</span></span> <span data-ttu-id="dda46-406">두 인수의 연결을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="dda46-407">**삼항 연산자:**</span><span class="sxs-lookup"><span data-stu-id="dda46-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="dda46-408">삼항 연산자</span><span class="sxs-lookup"><span data-stu-id="dda46-408">Ternary operator</span></span>|<span data-ttu-id="dda46-409">?</span><span class="sxs-lookup"><span data-stu-id="dda46-409">?</span></span>|<span data-ttu-id="dda46-410">첫 번째 인수가 **true**로 평가되면 두 번째 인수를 반환하고, 그렇지 않으면 세 번째 인수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="dda46-411">**비교 연산자의 값 순서 지정**</span><span class="sxs-lookup"><span data-stu-id="dda46-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="dda46-412">**형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-412">**Type**</span></span>|<span data-ttu-id="dda46-413">**값 순서**</span><span class="sxs-lookup"><span data-stu-id="dda46-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="dda46-414">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="dda46-414">**Undefined**</span></span>|<span data-ttu-id="dda46-415">비교할 수 없음</span><span class="sxs-lookup"><span data-stu-id="dda46-415">Not comparable.</span></span>|  
|<span data-ttu-id="dda46-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="dda46-416">**Null**</span></span>|<span data-ttu-id="dda46-417">단일 값: **null**</span><span class="sxs-lookup"><span data-stu-id="dda46-417">Single value: **null**</span></span>|  
|<span data-ttu-id="dda46-418">**Number**</span><span class="sxs-lookup"><span data-stu-id="dda46-418">**Number**</span></span>|<span data-ttu-id="dda46-419">자연수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="dda46-420">Negative Infinity(음의 무한대) 값은 다른 Number 값보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="dda46-421">Positive Infinity(양의 무한대) 값은 다른 Number 값보다 큽니다. **NaN** 값은 비교할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="dda46-422">**NaN**과 비교하면 **undefined** 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="dda46-423">**String**</span><span class="sxs-lookup"><span data-stu-id="dda46-423">**String**</span></span>|<span data-ttu-id="dda46-424">사전순 정렬</span><span class="sxs-lookup"><span data-stu-id="dda46-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="dda46-425">**Array**</span><span class="sxs-lookup"><span data-stu-id="dda46-425">**Array**</span></span>|<span data-ttu-id="dda46-426">순서를 지정하지 않지만 동등하게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="dda46-427">**Object**</span><span class="sxs-lookup"><span data-stu-id="dda46-427">**Object**</span></span>|<span data-ttu-id="dda46-428">순서를 지정하지 않지만 동등하게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="dda46-429">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-429">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-430">Azure Cosmos DB에서 값 형식은 실제로 데이터베이스에서 검색될 때까지 알 수 없는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="dda46-431">쿼리의 효율적인 실행을 지원하기 위해 대부분의 연산자에는 엄격한 형식 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="dda46-432">또한 연산자 자체는 암시적 변환을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="dda46-433">즉 SELECT * FROM ROOT r WHERE r.Age = 21과 같은 쿼리는 Age 속성이 21인 문서만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="dda46-434">"21" = 21 식이 undefined로 평가되므로 Age 속성이 "21" 또는 "0021" 문자열과 일치하지 않는 문서는 일치하지 않는 문서가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="dda46-435">이렇게 하면 특정 값(즉, 숫자 21)의 조회가 무한 수의 잠재적 일치 항목(즉, 숫자 21 또는 문자열 "21", "021", "21.0"...)을 검색하는 것보다 빠르기 때문에 인덱스를 더 잘 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="dda46-436">이는 JavaScript에서 다른 형식의 값에 대해 연산자를 평가하는 방식과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="dda46-437">**배열 및 개체 같음 및 비교**</span><span class="sxs-lookup"><span data-stu-id="dda46-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="dda46-438">범위 연산자(>, >=, <, <=)를 사용하여 배열 또는 개체 값을 비교하면 배열 또는 개체 값에 정의된 순서가 없으므로 결과가 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="dda46-439">그러나 같음/같지 않음 연산자(=, !=, <>)를 사용할 수 있으며, 이 경우 값이 구조적으로 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="dda46-440">두 배열의 요소 수가 같고 일치하는 위치의 요소도 같은 경우 배열은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="dda46-441">요소 쌍을 비교할 때 정의되지 않은 결과가 나오는 경우 배열 비교의 결과는 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="dda46-442">두 개체에 동일한 속성이 정의되어 있고 일치하는 속성의 값도 같은 경우 개체는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="dda46-443">속성 값 쌍을 비교할 때 정의되지 않은 결과가 나오는 경우 개체 비교의 결과는 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="dda46-444"><a name="bk_constants"></a> 상수</span><span class="sxs-lookup"><span data-stu-id="dda46-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="dda46-445">리터럴 또는 스칼라 값이라고도 하는 상수는 특정 데이터 값을 나타내는 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="dda46-446">상수의 형식은 나타내는 값의 데이터 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="dda46-447">**지원되는 스칼라 데이터 형식:**</span><span class="sxs-lookup"><span data-stu-id="dda46-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="dda46-448">**형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-448">**Type**</span></span>|<span data-ttu-id="dda46-449">**값 순서**</span><span class="sxs-lookup"><span data-stu-id="dda46-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="dda46-450">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="dda46-450">**Undefined**</span></span>|<span data-ttu-id="dda46-451">단일 값: **undefined**</span><span class="sxs-lookup"><span data-stu-id="dda46-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="dda46-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="dda46-452">**Null**</span></span>|<span data-ttu-id="dda46-453">단일 값: **null**</span><span class="sxs-lookup"><span data-stu-id="dda46-453">Single value: **null**</span></span>|  
|<span data-ttu-id="dda46-454">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="dda46-454">**Boolean**</span></span>|<span data-ttu-id="dda46-455">값: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="dda46-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="dda46-456">**Number**</span><span class="sxs-lookup"><span data-stu-id="dda46-456">**Number**</span></span>|<span data-ttu-id="dda46-457">IEEE 754 표준의 두 자리 부동 소수점 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="dda46-458">**String**</span><span class="sxs-lookup"><span data-stu-id="dda46-458">**String**</span></span>|<span data-ttu-id="dda46-459">0개 이상의 유니코드 문자 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="dda46-460">문자열은 작은따옴표 또는 큰 따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="dda46-461">**Array**</span><span class="sxs-lookup"><span data-stu-id="dda46-461">**Array**</span></span>|<span data-ttu-id="dda46-462">0개 이상의 요소 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="dda46-463">각 요소는 Undefined를 제외한 모든 스칼라 데이터 형식의 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="dda46-464">**Object**</span><span class="sxs-lookup"><span data-stu-id="dda46-464">**Object**</span></span>|<span data-ttu-id="dda46-465">순서가 지정되지 않은 0개 이상의 이름/값 쌍의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="dda46-466">이름은 유니코드 문자열이며, 값은 **Undefined**를 제외한 모든 스칼라 데이터 형식이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="dda46-467">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-467">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="dda46-468">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="dda46-469">Undefined 형식의 undefined 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="dda46-470">**Null** 형식의 **null** 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="dda46-471">Boolean 형식의 상수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="dda46-472">Boolean 형식의 **false** 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="dda46-473">Boolean 형식의 **true** 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="dda46-474">상수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="dda46-475">10진 리터럴은 10진수 표기법 또는 과학적 표기법을 사용하여 표현되는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="dda46-476">16진 리터럴은 '0x' 접두사 다음에 하나 이상의 16진수가 나오는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="dda46-477">String 형식의 상수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="dda46-478">문자열 리터럴은 연속적인 0이상의 유니코드 문자 또는 이스케이프 시퀀스로 표현되는 유니코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="dda46-479">문자열 리터럴은 작은따옴표(아포스트로피: ') 또는 큰따옴표(따옴표: ")로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="dda46-480">허용되는 이스케이프 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="dda46-481">**이스케이프 시퀀스**</span><span class="sxs-lookup"><span data-stu-id="dda46-481">**Escape sequence**</span></span>|<span data-ttu-id="dda46-482">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-482">**Description**</span></span>|<span data-ttu-id="dda46-483">**유니코드 문자**</span><span class="sxs-lookup"><span data-stu-id="dda46-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="dda46-484">\\'</span><span class="sxs-lookup"><span data-stu-id="dda46-484">\\'</span></span>|<span data-ttu-id="dda46-485">아포스트로피(')</span><span class="sxs-lookup"><span data-stu-id="dda46-485">apostrophe (')</span></span>|<span data-ttu-id="dda46-486">U+0027</span><span class="sxs-lookup"><span data-stu-id="dda46-486">U+0027</span></span>|  
|<span data-ttu-id="dda46-487">\\"</span><span class="sxs-lookup"><span data-stu-id="dda46-487">\\"</span></span>|<span data-ttu-id="dda46-488">따옴표(")</span><span class="sxs-lookup"><span data-stu-id="dda46-488">quotation mark (")</span></span>|<span data-ttu-id="dda46-489">U+0022</span><span class="sxs-lookup"><span data-stu-id="dda46-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="dda46-490">백슬래시(\\)</span><span class="sxs-lookup"><span data-stu-id="dda46-490">reverse solidus (\\)</span></span>|<span data-ttu-id="dda46-491">U+005C</span><span class="sxs-lookup"><span data-stu-id="dda46-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="dda46-492">슬래시(/)</span><span class="sxs-lookup"><span data-stu-id="dda46-492">solidus (/)</span></span>|<span data-ttu-id="dda46-493">U+002F</span><span class="sxs-lookup"><span data-stu-id="dda46-493">U+002F</span></span>|  
|<span data-ttu-id="dda46-494">\b</span><span class="sxs-lookup"><span data-stu-id="dda46-494">\b</span></span>|<span data-ttu-id="dda46-495">백스페이스</span><span class="sxs-lookup"><span data-stu-id="dda46-495">backspace</span></span>|<span data-ttu-id="dda46-496">U+0008</span><span class="sxs-lookup"><span data-stu-id="dda46-496">U+0008</span></span>|  
|<span data-ttu-id="dda46-497">\f</span><span class="sxs-lookup"><span data-stu-id="dda46-497">\f</span></span>|<span data-ttu-id="dda46-498">폼 피드</span><span class="sxs-lookup"><span data-stu-id="dda46-498">form feed</span></span>|<span data-ttu-id="dda46-499">U+000C</span><span class="sxs-lookup"><span data-stu-id="dda46-499">U+000C</span></span>|  
|\n|<span data-ttu-id="dda46-500">줄 바꿈</span><span class="sxs-lookup"><span data-stu-id="dda46-500">line feed</span></span>|<span data-ttu-id="dda46-501">U+000A</span><span class="sxs-lookup"><span data-stu-id="dda46-501">U+000A</span></span>|  
|<span data-ttu-id="dda46-502">\r</span><span class="sxs-lookup"><span data-stu-id="dda46-502">\r</span></span>|<span data-ttu-id="dda46-503">캐리지 리턴</span><span class="sxs-lookup"><span data-stu-id="dda46-503">carriage return</span></span>|<span data-ttu-id="dda46-504">U+000D</span><span class="sxs-lookup"><span data-stu-id="dda46-504">U+000D</span></span>|  
|<span data-ttu-id="dda46-505">\t</span><span class="sxs-lookup"><span data-stu-id="dda46-505">\t</span></span>|<span data-ttu-id="dda46-506">탭</span><span class="sxs-lookup"><span data-stu-id="dda46-506">tab</span></span>|<span data-ttu-id="dda46-507">U+0009</span><span class="sxs-lookup"><span data-stu-id="dda46-507">U+0009</span></span>|  
|<span data-ttu-id="dda46-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="dda46-508">\uXXXX</span></span>|<span data-ttu-id="dda46-509">4자리 16진수로 정의된 유니코드 문자</span><span class="sxs-lookup"><span data-stu-id="dda46-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="dda46-510">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="dda46-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="dda46-511"><a name="bk_query_perf_guidelines"></a> 쿼리 성능 지침</span><span class="sxs-lookup"><span data-stu-id="dda46-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="dda46-512">대형 컬렉션에 대해 쿼리를 효율적으로 실행하려면 하나 이상의 인덱스를 통해 제공될 수 있는 필터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="dda46-513">인덱스 조회에 대해 고려되는 필터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="dda46-514">문서 경로 식 및 상수와 함께 같음 연산자(=)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="dda46-515">문서 경로 식 및 상수와 함께 범위 연산자(<, \<=, >, >=)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="dda46-516">문서 경로 식은 참조되는 데이터베이스 컬렉션에서 문서의 상수 경로를 식별하는 모든 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="dda46-517">**문서 경로 식**</span><span class="sxs-lookup"><span data-stu-id="dda46-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="dda46-518">문서 경로 식은 데이터베이스 수집 문서에서 제공하는 문서를 통해 속성 또는 배열 인덱서의 경로를 평가하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="dda46-519">이 경로는 필터에서 직접 참조되는 값의 위치를 데이터베이스 컬렉션의 문서 내에서 식별하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="dda46-520">문서 경로 식으로 간주되는 식의 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="dda46-521">컬렉션 루트를 직접 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="dda46-522">일부 문서 경로 식의 속성 또는 상수 배열 인덱서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="dda46-523">일부 문서 경로 식을 나타내는 별칭을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="dda46-524">**구문 규칙**</span><span class="sxs-lookup"><span data-stu-id="dda46-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="dda46-525">다음 표에서는 DocumentDB API 쿼리 언어 참조의 구문을 설명하는 데 사용되는 규칙을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="dda46-526">**규칙**</span><span class="sxs-lookup"><span data-stu-id="dda46-526">**Convention**</span></span>|<span data-ttu-id="dda46-527">**용도**</span><span class="sxs-lookup"><span data-stu-id="dda46-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="dda46-528">대문자</span><span class="sxs-lookup"><span data-stu-id="dda46-528">UPPERCASE</span></span>|<span data-ttu-id="dda46-529">대/소문자를 구분하지 않는 키워드</span><span class="sxs-lookup"><span data-stu-id="dda46-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="dda46-530">소문자</span><span class="sxs-lookup"><span data-stu-id="dda46-530">lowercase</span></span>|<span data-ttu-id="dda46-531">대/소문자를 구분하는 키워드</span><span class="sxs-lookup"><span data-stu-id="dda46-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="dda46-532">\<nonterminal></span><span class="sxs-lookup"><span data-stu-id="dda46-532">\<nonterminal></span></span>|<span data-ttu-id="dda46-533">비단말(nonterminal)이며, 개별적으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="dda46-534">\<nonterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="dda46-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="dda46-535">비단말의 구문 정의</span><span class="sxs-lookup"><span data-stu-id="dda46-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="dda46-536">other_terminal</span><span class="sxs-lookup"><span data-stu-id="dda46-536">other_terminal</span></span>|<span data-ttu-id="dda46-537">단말(토큰)이며, 단어로 자세히 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="dda46-538">identifier</span><span class="sxs-lookup"><span data-stu-id="dda46-538">identifier</span></span>|<span data-ttu-id="dda46-539">식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-539">Identifier.</span></span> <span data-ttu-id="dda46-540">허용되는 문자: a-z, A-Z, 0-9. 첫 번째 문자는 숫자가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="dda46-541">"문자열"</span><span class="sxs-lookup"><span data-stu-id="dda46-541">"string"</span></span>|<span data-ttu-id="dda46-542">따옴표가 붙은 문자열이며,</span><span class="sxs-lookup"><span data-stu-id="dda46-542">Quoted string.</span></span> <span data-ttu-id="dda46-543">유효한 문자열이 모두 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-543">Allows any valid string.</span></span> <span data-ttu-id="dda46-544">string_literal에 대한 설명을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="dda46-545">'기호'</span><span class="sxs-lookup"><span data-stu-id="dda46-545">'symbol'</span></span>|<span data-ttu-id="dda46-546">구문의 일부인 문자 기호</span><span class="sxs-lookup"><span data-stu-id="dda46-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="dda46-547">&#124; (세로줄)</span><span class="sxs-lookup"><span data-stu-id="dda46-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="dda46-548">구문 항목에 대한 대안이며,</span><span class="sxs-lookup"><span data-stu-id="dda46-548">Alternatives for syntax items.</span></span> <span data-ttu-id="dda46-549">지정된 항목 중 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="dda46-550">[ ] /(대괄호)</span><span class="sxs-lookup"><span data-stu-id="dda46-550">[ ] /(brackets)</span></span>|<span data-ttu-id="dda46-551">대괄호는 하나 이상의 선택 항목을 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="dda46-552">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="dda46-552">[ ,...n ]</span></span>|<span data-ttu-id="dda46-553">앞의 항목이 n번 반복될 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="dda46-554">각 항목은 쉼표로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="dda46-555">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="dda46-555">[ ...n ]</span></span>|<span data-ttu-id="dda46-556">앞의 항목이 n번 반복될 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="dda46-557">각 항목은 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="dda46-558"><a name="bk_built_in_functions"></a> 기본 제공 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="dda46-559">Azure Cosmos DB는 많은 기본 제공 SQL 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="dda46-560">기본 제공 함수의 범주는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="dda46-561">함수</span><span class="sxs-lookup"><span data-stu-id="dda46-561">Function</span></span>|<span data-ttu-id="dda46-562">설명</span><span class="sxs-lookup"><span data-stu-id="dda46-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="dda46-563">수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="dda46-564">수치 연산 함수는 각각 인수로 제공된 입력 값에 따라 계산을 수행하고 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="dda46-565">형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="dda46-566">형식 검사 함수를 통해 SQL 쿼리 내에서 식의 형식을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="dda46-567">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="dda46-568">문자열 함수는 문자열 입력 값에 대한 연산을 수행하고, 문자열, 숫자 또는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="dda46-569">배열 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="dda46-570">배열 함수는 배열 입력 값에 대한 연산을 수행하고, 숫자, 부울, 또는 배열 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="dda46-571">공간 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="dda46-572">공간 함수는 공간 개체 입력 값에 대한 연산을 수행하고, 숫자 또는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="dda46-573"><a name="bk_mathematical_functions"></a> 수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="dda46-574">다음 함수는 각각 인수로 제공된 입력 값에 따라 계산을 수행하고 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="dda46-575">ABS</span><span class="sxs-lookup"><span data-stu-id="dda46-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="dda46-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="dda46-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="dda46-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="dda46-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="dda46-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="dda46-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="dda46-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="dda46-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="dda46-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="dda46-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="dda46-581">COS</span><span class="sxs-lookup"><span data-stu-id="dda46-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="dda46-582">COT</span><span class="sxs-lookup"><span data-stu-id="dda46-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="dda46-583">각도</span><span class="sxs-lookup"><span data-stu-id="dda46-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="dda46-584">EXP</span><span class="sxs-lookup"><span data-stu-id="dda46-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="dda46-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="dda46-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="dda46-586">로그</span><span class="sxs-lookup"><span data-stu-id="dda46-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="dda46-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="dda46-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="dda46-588">PI</span><span class="sxs-lookup"><span data-stu-id="dda46-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="dda46-589">전원</span><span class="sxs-lookup"><span data-stu-id="dda46-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="dda46-590">라디안</span><span class="sxs-lookup"><span data-stu-id="dda46-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="dda46-591">반올림</span><span class="sxs-lookup"><span data-stu-id="dda46-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="dda46-592">SIN</span><span class="sxs-lookup"><span data-stu-id="dda46-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="dda46-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="dda46-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="dda46-594">정사각형</span><span class="sxs-lookup"><span data-stu-id="dda46-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="dda46-595">로그인</span><span class="sxs-lookup"><span data-stu-id="dda46-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="dda46-596">TAN</span><span class="sxs-lookup"><span data-stu-id="dda46-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="dda46-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="dda46-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="dda46-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="dda46-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="dda46-599">지정한 숫자 식의 절대(양수) 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-600">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-601">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-602">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-603">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-603">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-604">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-605">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-605">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-606">다음 예제에서는 세 개의 다른 숫자에 ABS 함수를 사용한 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="dda46-607">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="dda46-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="dda46-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="dda46-609">코사인 값이 지정된 숫자 식인 라디안에서 각도를 반환합니다. 아크코사인이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="dda46-610">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-611">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-612">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-613">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-613">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-614">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-615">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-615">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-616">다음 예제에서는 -1의 ACOS를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="dda46-617">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="dda46-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="dda46-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="dda46-619">사인 값이 지정된 숫자 식인 라디안에서 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="dda46-620">아크사인이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="dda46-621">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-622">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-623">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-624">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-624">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-625">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-626">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-626">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-627">다음 예제에서는 -1의 ASIN을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="dda46-628">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="dda46-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="dda46-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="dda46-630">탄젠트 값이 지정된 숫자 식인 라디안에서 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="dda46-631">아크탄젠트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="dda46-632">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-633">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-634">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-635">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-635">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-636">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-637">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-637">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-638">다음 예제에서는 지정된 값의 ATAN을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="dda46-639">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="dda46-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="dda46-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="dda46-641">y/x에 대한 아크 탄젠트의 주요 값(라디안 단위)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="dda46-642">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-643">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-644">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-645">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-645">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-646">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-647">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-647">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-648">다음 예제에서는 지정된 x 및 y 구성 요소에 대한 ATN2를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="dda46-649">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="dda46-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="dda46-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="dda46-651">지정한 숫자 식보다 크거나 같은 가장 작은 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-652">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-653">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-654">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-655">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-655">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-656">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-657">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-657">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-658">다음 예제에서는 CEILING 함수를 사용하여 양수, 음수 및 0 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="dda46-659">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="dda46-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="dda46-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="dda46-661">지정된 식의 라디안에서 지정된 각도의 삼각 코사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="dda46-662">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-663">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-664">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-665">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-665">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-666">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-667">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-667">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-668">다음 예제에서는 지정된 각도의 COS를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="dda46-669">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="dda46-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="dda46-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="dda46-671">지정된 숫자 식의 라디안에서 지정된 각도의 삼각 코탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-672">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-673">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-674">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-675">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-675">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-676">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-677">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-677">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-678">다음 예제에서는 지정된 각도의 COT를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="dda46-679">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="dda46-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="dda46-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="dda46-681">라디안에서 지정된 각도로 해당하는 각도를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="dda46-682">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-683">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-684">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-685">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-685">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-686">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-687">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-687">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-688">다음 예제에서는 PI/2 라디안 각도의 각도 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="dda46-689">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="dda46-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="dda46-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="dda46-691">지정한 숫자 식보다 작거나 같은 가장 큰 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-692">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-693">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-694">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-695">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-695">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-696">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-697">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-697">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-698">다음 예제에서는 FLOOR 함수를 사용하여 양수, 음수 및 0 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="dda46-699">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="dda46-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="dda46-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="dda46-701">지정된 숫자 식의 지수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-702">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-703">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-704">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-705">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-705">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-706">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-707">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-707">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-708">**e**(2.718281…) 상수는 자연 로그의 밑입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="dda46-709">숫자의 지수는 **e** 상수를 거듭제곱하는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="dda46-710">예를 들어 EXP(1.0) = e^1.0 = 2.71828182845905이며, EXP(10) = e^10 = 22026.4657948067입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="dda46-711">숫자의 자연 로그의 지수는 숫자 자체, 즉 EXP (LOG (n)) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="dda46-712">그리고 숫자의 지수의 자연 로그는 숫자 자체, 즉 LOG (EXP (n)) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="dda46-713">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-713">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-714">다음 예제에서는 변수를 선언하고 지정된 변수 (10)의 지수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="dda46-715">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="dda46-716">다음 예제에서는 20의 자연 로그의 지수 값과 및 20의 지수의 자연 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="dda46-717">이러한 함수는 서로 역함수이므로 두 경우 모두 부동 소수점 수치가 반올림된 반환 값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="dda46-718">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="dda46-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="dda46-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="dda46-720">지정된 숫자 식의 자연 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-721">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="dda46-722">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-723">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="dda46-724">로그의 밑을 설정하는 선택적 숫자 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="dda46-725">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-725">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-726">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-727">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-727">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-728">LOG()는 기본적으로 자연 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="dda46-729">선택적인 base 매개 변수를 사용하여 로그의 밑을 다른 값으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="dda46-730">자연 로그는 **e**를 밑으로 하는 로그입니다. 여기서 **e**는 대략 2.718281828과 같은 무리 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="dda46-731">숫자의 지수의 자연 로그는 숫자 자체, 즉 LOG( EXP( n ) ) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="dda46-732">그리고 숫자의 자연 로그의 지수는 숫자 자체, 즉 EXP( LOG( n ) ) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="dda46-733">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-733">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-734">다음 예제에서는 변수를 선언하고 지정된 변수 (10)의 로그 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="dda46-735">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="dda46-736">다음 예제에서는 숫자의 지수에 대한 LOG를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="dda46-737">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="dda46-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="dda46-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="dda46-739">지정한 숫자 식의 상용 로그(밑 10)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-740">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-741">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-742">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-743">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-743">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-744">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-745">**설명**</span><span class="sxs-lookup"><span data-stu-id="dda46-745">**Remarks**</span></span>  
  
 <span data-ttu-id="dda46-746">LOG10과 POWER 함수는 서로 역의 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="dda46-747">예를 들어 10 ^ LOG10(n) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="dda46-748">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-748">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-749">다음 예제에서는 변수를 선언하고 지정된 변수 (100)의 LOG10 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="dda46-750">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="dda46-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="dda46-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="dda46-752">PI의 상수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="dda46-753">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="dda46-754">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-755">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-756">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-756">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-757">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-758">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-758">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-759">다음 예제에서는 PI의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="dda46-760">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="dda46-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="dda46-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="dda46-762">지정된 식의 값을 지정된 거듭제곱으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="dda46-763">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="dda46-764">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-765">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="dda46-766">`numeric_expression`이 거듭제곱되는 지수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="dda46-767">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-767">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-768">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-769">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-769">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-770">다음 예제에서는 숫자를 3의 지수로 거듭제곱합니다(숫자의 3제곱).</span><span class="sxs-lookup"><span data-stu-id="dda46-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="dda46-771">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="dda46-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="dda46-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="dda46-773">숫자 식을 단위로 입력하면 라디안을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="dda46-774">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-775">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-776">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-777">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-777">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-778">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-779">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-779">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-780">다음 예제에서는 몇 개의 각도를 입력으로 사용하여 해당 라디안 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="dda46-781">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="dda46-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="dda46-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="dda46-783">가장 가까운 정수 값으로 반올림한 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="dda46-784">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-785">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-786">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-787">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-787">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-788">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-789">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-789">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-790">다음 예제에서는 첨부된 양수와 음수를 가장 가까운 정수로 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="dda46-791">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="dda46-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="dda46-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="dda46-793">지정한 숫자 식의 양수(+1), 0(0) 또는 음수(-1) 부호를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-794">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-795">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-796">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-797">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-797">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-798">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-799">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-799">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-800">다음 예제에서는 -2에서 2까지의 숫자의 SIGN 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="dda46-801">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="dda46-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="dda46-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="dda46-803">지정된 식의 라디안에서 지정된 각도의 삼각 사인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="dda46-804">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-805">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-806">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-807">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-807">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-808">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-809">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-809">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-810">다음 예제에서는 지정된 각도의 SIN을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="dda46-811">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="dda46-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="dda46-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="dda46-813">지정된 숫자 값의 제곱근을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="dda46-814">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-815">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-816">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-817">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-817">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-818">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-819">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-819">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-820">다음 예제에서는 숫자 1-3의 제곱근을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="dda46-821">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="dda46-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="dda46-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="dda46-823">지정한 숫자 값의 제곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="dda46-824">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-825">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-826">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-827">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-827">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-828">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-829">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-829">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-830">다음 예제에서는 1에서 3까지의 숫자의 제곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="dda46-831">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="dda46-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="dda46-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="dda46-833">지정된 식에서 지정된 각도(라디안 단위)의 탄젠트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="dda46-834">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-835">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-836">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-837">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-837">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-838">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-839">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-839">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-840">다음 예제에서는 PI()/2의 탄젠트를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="dda46-841">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="dda46-842"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="dda46-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="dda46-843">가장 가까운 정수 값으로 버린 숫자 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="dda46-844">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="dda46-845">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="dda46-846">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-847">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-847">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-848">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-849">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-849">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-850">다음 예제에서는 첨부된 양수와 음수를 가장 가까운 정수 값으로 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="dda46-851">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="dda46-852"><a name="bk_type_checking_functions"></a> 형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="dda46-853">다음 함수는 입력 값에 대한 형식 검사를 지원하며, 각 함수마다 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="dda46-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="dda46-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="dda46-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="dda46-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="dda46-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="dda46-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="dda46-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="dda46-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="dda46-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="dda46-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="dda46-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="dda46-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="dda46-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="dda46-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="dda46-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="dda46-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="dda46-862"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="dda46-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="dda46-863">지정한 식의 형식이 배열인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="dda46-864">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="dda46-865">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-866">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-867">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-867">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-868">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-869">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-869">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-870">다음 예제에서는 IS_ARRAY 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-871">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="dda46-872"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="dda46-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="dda46-873">지정한 식의 형식이 부울인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="dda46-874">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="dda46-875">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-876">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-877">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-877">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-878">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-879">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-879">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-880">다음 예제에서는 IS_BOOL 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-881">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="dda46-882"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="dda46-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="dda46-883">속성이 값을 할당할지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="dda46-884">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="dda46-885">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-886">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-887">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-887">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-888">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-889">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-889">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-890">다음 예제에서는 지정된 JSON 문서 내에 속성이 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="dda46-891">"a"가 있으므로 첫 번째 함수는 true를 반환하지만, "b"가 없으므로 두 번째 함수는 false를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="dda46-892">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="dda46-893"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="dda46-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="dda46-894">지정한 식의 형식이 널인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="dda46-895">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="dda46-896">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-897">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-898">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-898">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-899">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-900">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-900">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-901">다음 예제에서는 IS_NULL 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-902">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="dda46-903"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="dda46-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="dda46-904">지정한 식의 형식이 숫자인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="dda46-905">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="dda46-906">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-907">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-908">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-908">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-909">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-910">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-910">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-911">다음 예제에서는 IS_NULL 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-912">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="dda46-913"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="dda46-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="dda46-914">지정한 식의 형식이 JSON 개체인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="dda46-915">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="dda46-916">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-917">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-918">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-918">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-919">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-920">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-920">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-921">다음 예제에서는 IS_OBJECT 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-922">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="dda46-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="dda46-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="dda46-924">지정한 식의 형식이 기본 형식(문자열, 부울, 숫자 또는 널)인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="dda46-925">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="dda46-926">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-927">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-928">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-928">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-929">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-930">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-930">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-931">다음 예제에서는 IS_PRIMITIVE 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-932">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="dda46-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="dda46-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="dda46-934">지정한 식의 형식이 문자열인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="dda46-935">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="dda46-936">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="dda46-937">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-938">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-938">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-939">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-940">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-940">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-941">다음 예제에서는 IS_STRING 함수를 사용하여 JSON 부울, number, string, null, object, array 및 undefined 형식의 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="dda46-942">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="dda46-943"><a name="bk_string_functions"></a> 문자열 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="dda46-944">다음 스칼라 함수는 문자열 입력 값에 대해 작업을 수행하고 문자열, 숫자 또는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="dda46-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="dda46-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="dda46-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="dda46-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="dda46-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="dda46-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="dda46-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="dda46-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="dda46-949">왼쪽</span><span class="sxs-lookup"><span data-stu-id="dda46-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="dda46-950">LENGTH</span><span class="sxs-lookup"><span data-stu-id="dda46-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="dda46-951">낮은</span><span class="sxs-lookup"><span data-stu-id="dda46-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="dda46-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="dda46-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="dda46-953">바꾸기</span><span class="sxs-lookup"><span data-stu-id="dda46-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="dda46-954">복제</span><span class="sxs-lookup"><span data-stu-id="dda46-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="dda46-955">역방향</span><span class="sxs-lookup"><span data-stu-id="dda46-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="dda46-956">오른쪽</span><span class="sxs-lookup"><span data-stu-id="dda46-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="dda46-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="dda46-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="dda46-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="dda46-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="dda46-959">하위 문자열</span><span class="sxs-lookup"><span data-stu-id="dda46-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="dda46-960">위</span><span class="sxs-lookup"><span data-stu-id="dda46-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="dda46-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="dda46-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="dda46-962">둘 이상의 문자열 값을 연결한 결과인 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="dda46-963">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="dda46-964">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-965">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-966">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-966">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-967">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-968">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-968">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-969">다음 예제에서는 지정된 값의 연결된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="dda46-970">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="dda46-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="dda46-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="dda46-972">첫 번째 문자열 식이 두 번째를 포함하는지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="dda46-973">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="dda46-974">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-975">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-976">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-976">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-977">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-978">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-978">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-979">다음 예제에서는 "abc"에 "ab"와 "d"가 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="dda46-980">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="dda46-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="dda46-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="dda46-982">첫 번째 문자열 식이 두 번째 문자열 식에서 끝나는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="dda46-983">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="dda46-984">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-985">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-986">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-986">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-987">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-988">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-988">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-989">다음 예제에서는 "abc"가 "b"와 "bc"로 끝나는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="dda46-990">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="dda46-991"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="dda46-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="dda46-992">지정된 첫 번째 문자열 식 내의 두 번째 문자열 식에서 첫 번째로 나타나는 시작 위치를 반환하거나 문자열을 찾을 수 없는 경우 -1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="dda46-993">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="dda46-994">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-995">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-996">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-996">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-997">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-998">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-998">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-999">다음 예제에서는 "abc" 안에 다양한 부분 문자열의 인덱스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="dda46-1000">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="dda46-1001"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="dda46-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="dda46-1002">지정된 수의 문자로 문자열의 왼쪽 부분을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="dda46-1003">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="dda46-1004">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1005">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="dda46-1006">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-1007">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1008">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1009">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1009">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1010">다음 예제에서는 다양한 길이 값에 대해 "abc"의 왼쪽 부분을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="dda46-1011">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="dda46-1012"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="dda46-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="dda46-1013">지정한 문자열 식의 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="dda46-1014">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="dda46-1015">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1016">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1017">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1018">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1019">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1019">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1020">다음 예제에서는 문자열의 길이를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="dda46-1021">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="dda46-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="dda46-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="dda46-1023">대문자 데이터를 소문자로 변환한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="dda46-1024">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="dda46-1025">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1026">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1027">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1028">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1029">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1029">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1030">다음 예제에서는 쿼리에서 LOWER를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="dda46-1031">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="dda46-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="dda46-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="dda46-1033">선행 공백을 제거한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="dda46-1034">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="dda46-1035">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1036">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1037">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1038">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1039">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1039">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1040">다음 예제에서는 LTRIM을 쿼리 내에서 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="dda46-1041">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="dda46-1042"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="dda46-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="dda46-1043">지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="dda46-1044">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="dda46-1045">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1046">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1047">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1048">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1049">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1049">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1050">다음 예제에서는 쿼리에서 REPLACE를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="dda46-1051">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="dda46-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="dda46-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="dda46-1053">문자열 값을 지정한 횟수 만큼 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="dda46-1054">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="dda46-1055">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1056">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="dda46-1057">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-1058">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1059">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1060">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1060">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1061">다음 예제에서는 쿼리에서 REPLICATE를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="dda46-1062">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="dda46-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="dda46-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="dda46-1064">문자열 값의 순서와 반대로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="dda46-1065">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="dda46-1066">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1067">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1068">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1069">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1070">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1070">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1071">다음 예제에서는 쿼리에서 REVERSE를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="dda46-1072">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="dda46-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="dda46-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="dda46-1074">지정된 수의 문자로 문자열의 오른쪽 부분을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="dda46-1075">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="dda46-1076">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1077">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="dda46-1078">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-1079">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1080">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1081">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1081">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1082">다음 예제에서는 다양한 길이 값에 대해 "abc"의 오른쪽 부분을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="dda46-1083">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="dda46-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="dda46-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="dda46-1085">후행 공백을 제거한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="dda46-1086">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="dda46-1087">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1088">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1089">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1090">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1091">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1091">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1092">다음 예제에서는 쿼리 내에서 RTRIM을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="dda46-1093">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="dda46-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="dda46-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="dda46-1095">첫 번째 문자열 식이 두 번째 문자열 식에서 시작하는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="dda46-1096">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="dda46-1097">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1098">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1099">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1100">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-1101">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1101">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1102">다음 예제에서는 "abc" 문자열이 "b"와 "a"로 시작하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="dda46-1103">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="dda46-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="dda46-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="dda46-1105">지정한 문자 0 기준 위치에서 시작하여 지정한 길이 또는 문자열의 끝까지에 이르는 문자열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="dda46-1106">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="dda46-1107">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1108">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="dda46-1109">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-1110">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1111">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1112">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1112">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1113">다음 예제에서는 1에서 시작하여 길이가 1인 "abc"의 부분 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="dda46-1114">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="dda46-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="dda46-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="dda46-1116">소문자 데이터를 대문자로 변환한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="dda46-1117">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="dda46-1118">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="dda46-1119">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="dda46-1120">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1121">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="dda46-1122">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1122">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1123">다음 예제에서는 쿼리에서 UPPER를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="dda46-1124">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="dda46-1125"><a name="bk_array_functions"></a> 배열 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="dda46-1126">다음 스칼라 함수는 배열 입력 값에 대한 연산을 수행하고, 숫자, 부울, 또는 배열 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="dda46-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="dda46-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="dda46-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="dda46-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="dda46-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="dda46-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="dda46-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="dda46-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="dda46-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="dda46-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="dda46-1132">둘 이상의 배열 값을 연결한 결과인 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="dda46-1133">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="dda46-1134">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="dda46-1135">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="dda46-1136">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1137">배열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="dda46-1138">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1138">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1139">다음 예제에서는 두 배열을 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="dda46-1140">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="dda46-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="dda46-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="dda46-1142">지정된 값이 배열에 포함되는지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="dda46-1143">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="dda46-1144">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="dda46-1145">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="dda46-1146">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="dda46-1147">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1148">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="dda46-1149">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1149">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1150">다음 예제에서는 ARRAY_CONTAINS를 사용하여 배열의 멤버 자격을 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="dda46-1151">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="dda46-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="dda46-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="dda46-1153">지정된 배열 식의 요소 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="dda46-1154">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="dda46-1155">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="dda46-1156">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="dda46-1157">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1158">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-1159">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1159">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1160">다음 예제에서는 ARRAY_LENGTH를 사용하여 배열의 길이를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="dda46-1161">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="dda46-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="dda46-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="dda46-1163">배열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="dda46-1164">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="dda46-1165">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="dda46-1166">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="dda46-1167">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="dda46-1168">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1169">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="dda46-1170">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1170">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1171">다음 예제에서는 ARRAY_SLICE를 사용하여 배열의 일부를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="dda46-1172">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="dda46-1173"><a name="bk_spatial_functions"></a> 공간 함수</span><span class="sxs-lookup"><span data-stu-id="dda46-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="dda46-1174">다음 스칼라 함수는 공간 개체 입력 값에 대한 연산을 수행하고, 숫자 또는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="dda46-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="dda46-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="dda46-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="dda46-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="dda46-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="dda46-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="dda46-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="dda46-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="dda46-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="dda46-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="dda46-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="dda46-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="dda46-1181">두 GeoJSON Point, Polygon 또는 LineString 식 사이의 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="dda46-1182">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="dda46-1183">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1184">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="dda46-1185">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1186">거리가 포함된 숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="dda46-1187">기본 참조 시스템의 경우 미터 단위로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="dda46-1188">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1188">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1189">다음 예제에서는 ST_DISTANCE 기본 제공 함수를 사용하여 지정된 위치에서 30Km 이내에 있는 모든 패밀리 문서를 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="dda46-1190">등 4가지 유형의 클러스터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="dda46-1191">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="dda46-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="dda46-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="dda46-1193">첫 번째 인수에 지정된 GeoJSON 개체(Point, Polygon 또는 LineString)가 두 번째 인수의 GeoJSON(Point, Polygon 또는 LineString) 내에 있는지 여부를 나타내는 부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="dda46-1194">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="dda46-1195">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1196">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1197">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="dda46-1198">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1199">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="dda46-1200">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1200">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1201">다음 예제에서는 ST_WITHIN을 사용하여 다각형 내의 모든 패밀리 문서를 찾는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="dda46-1202">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="dda46-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="dda46-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="dda46-1204">첫 번째 인수에 지정된 GeoJSON 개체(Point, Polygon 또는 LineString)가 두 번째 인수의 GeoJSON(Point, Polygon 또는 LineString)과 교차하는지 여부를 나타내는 부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="dda46-1205">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="dda46-1206">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1207">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1208">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="dda46-1209">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1210">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="dda46-1211">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1211">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1212">다음 예제에서는 지정된 다각형과 교차하는 모든 영역을 찾는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="dda46-1213">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="dda46-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="dda46-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="dda46-1215">지정된 GeoJSON Point, Polygon 또는 LineString 식이 유효한지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="dda46-1216">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="dda46-1217">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1218">유효한 GeoJSON Point, Polygon 또는 LineString 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="dda46-1219">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1220">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="dda46-1221">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1221">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1222">다음 예제에서는 ST_VALID를 사용하여 꼭짓점이 유효한지 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="dda46-1223">예를 들어 유효 범위[-90, 90]에 없는 위도 값이 이 꼭짓점에 있으므로 쿼리에서 false를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="dda46-1224">다각형의 경우 GeoJSON 사양에서는 닫힌 도형을 만들기 위해 제공된 마지막 좌표 쌍이 첫 번째 것과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="dda46-1225">다각형 내의 점을 시계 반대 방향 순서로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="dda46-1226">시계 방향 순서로 지정된 다각형은 내부 영역의 반전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="dda46-1227">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="dda46-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="dda46-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="dda46-1229">지정된 GeoJSON Point, Polygon 또는 LineString 식이 유효한 경우 부울 값을 포함하는 JSON 값을 반환하고, 잘못된 경우 추가로 그 이유를 문자열 값으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="dda46-1230">**구문**</span><span class="sxs-lookup"><span data-stu-id="dda46-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="dda46-1231">**인수**</span><span class="sxs-lookup"><span data-stu-id="dda46-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="dda46-1232">유효한 GeoJSON 꼭짓점 또는 다각형 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="dda46-1233">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="dda46-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="dda46-1234">지정된 GeoJSON 점 또는 다각형 식이 유효한 경우 부울 값을 포함하는 JSON 값을 반환하고, 잘못된 경우 추가로 그 이유를 문자열 값으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="dda46-1235">**예**</span><span class="sxs-lookup"><span data-stu-id="dda46-1235">**Examples**</span></span>  
  
 <span data-ttu-id="dda46-1236">다음 예제에서는 ST_ISVALIDDETAILED를 사용하여 세부 정보로 유효성을 검사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="dda46-1237">결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda46-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="dda46-1238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dda46-1238">Next steps</span></span>  
 <span data-ttu-id="dda46-1239">[Azure Cosmos DB에 대한 SQL 구문 및 SQL 쿼리](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="dda46-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="dda46-1240">Azure Cosmos DB 설명서</span><span class="sxs-lookup"><span data-stu-id="dda46-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
