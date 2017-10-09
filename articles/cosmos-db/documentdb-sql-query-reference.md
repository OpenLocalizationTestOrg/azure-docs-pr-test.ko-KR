---
<span data-ttu-id="93b2b-101">제목: aaa "Azure Cosmos DB DocumentDB API: SQL 구문을 | Microsoft Docs "설명: hello Azure Cosmos DB DocumentDB API SQL 쿼리 언어에 대 한 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="93b2b-102">서비스: cosmos db 작성자: mimig1 관리자: jhubbard 편집기: mimig documentationcenter: '</span><span class="sxs-lookup"><span data-stu-id="93b2b-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="93b2b-103">ms.assetid: ms.service: cosmos db ms.workload: 데이터 서비스 ms.tgt_pltfrm: na ms.devlang: na ms.topic: 참조 ms.date: 06/13/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="93b2b-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="93b2b-104">Azure Cosmos DB DocumentDB API: SQL 구문 참조</span><span class="sxs-lookup"><span data-stu-id="93b2b-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="93b2b-105">명시적 스키마 나 보조 인덱스를 만들 필요 없이 계층적 JSON 문서에 대해 문법와 같은 익숙한 SQL (Structured Query Language)을 사용 하 여 쿼리 문서를 지원 하는 hello Azure Cosmos DB DocumentDB API 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="93b2b-106">이 항목에서는 DocumentDB API SQL 쿼리 언어 hello에 대 한 참조 설명서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="93b2b-107">Hello DocumentDB API SQL 쿼리 언어를 연습에 대 한 참조 [Azure Cosmos DB DocumentDB API에 대 한 SQL 쿼리](documentdb-sql-query.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="93b2b-108">Toovisit hello 초대 또한 [Query Playground](http://www.documentdb.com/sql/demo) Azure Cosmos DB를 시도 하 고이 데이터 집합에 대해 SQL 쿼리를 실행할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="93b2b-109">SELECT 쿼리</span><span class="sxs-lookup"><span data-stu-id="93b2b-109">SELECT query</span></span>  
<span data-ttu-id="93b2b-110">Hello 데이터베이스에서 JSON 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="93b2b-111">식 평가, 프로젝션, 필터링 및 조인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="93b2b-112">hello SELECT 문을 설명 하는 데 사용 되는 hello 규칙 hello 구문 규칙 섹션에에서 표로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="93b2b-113">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="93b2b-114">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-114">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-115">각 절에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="93b2b-116">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="93b2b-117">FROM 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="93b2b-118">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="93b2b-119">ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="93b2b-120">위와 같이 hello SELECT 문에서 hello 절 순서를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="93b2b-121">Hello 선택 사항인 절 중 하나를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="93b2b-122">하지만 선택 사항인 절을 사용할 때는 hello 올바른 순서로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="93b2b-123">**Hello SELECT 문의 논리적 처리 순서**</span><span class="sxs-lookup"><span data-stu-id="93b2b-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="93b2b-124">hello order 절이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="93b2b-125">FROM 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="93b2b-126">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="93b2b-127">ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="93b2b-128">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="93b2b-129">Note이 hello 구문에 나타나는 hello 순서와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="93b2b-130">처리 된 절에 의해 도입 된 새로운 모든 기호가 표시 되 고 나중에 처리 하는 절에 사용할 수 있도록 hello 순서가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="93b2b-131">예를 들어 FROM 절에 선언된 별칭은 WHERE 절과 SELECT 절에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="93b2b-132">**공백 문자 및 주석**</span><span class="sxs-lookup"><span data-stu-id="93b2b-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="93b2b-133">따옴표 붙은 식별자 또는 따옴표 붙은 문자열의 일부가 아닌 모든 공백 문자는 hello 언어 문법의 일부가 아닌 및 구문 분석에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="93b2b-134">hello 쿼리 언어 같은 T-SQL 스타일 주석을 지원합니다</span><span class="sxs-lookup"><span data-stu-id="93b2b-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="93b2b-135">`-- comment text [newline]` SQL 문</span><span class="sxs-lookup"><span data-stu-id="93b2b-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="93b2b-136">공백 문자와 주석은 없는 반면 중요 hello 문법에를 사용 하는 tooseparate 토큰 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="93b2b-137">예를 들어 `-1e5`는 단일 숫자 토큰이지만, `: – 1 e5`는 숫자 1과 식별자 e5가 뒤에 나오는 마이너스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="93b2b-138"><a name="bk_select_query"></a> SELECT 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="93b2b-139">위와 같이 hello SELECT 문에서 hello 절 순서를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="93b2b-140">Hello 선택 사항인 절 중 하나를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="93b2b-141">하지만 선택 사항인 절을 사용할 때는 hello 올바른 순서로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="93b2b-142">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="93b2b-143">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="93b2b-144">속성 또는 값 toobe hello 결과 대 한 선택 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="93b2b-145">Hello 값을 변경 하지 않고 검색을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="93b2b-146">처리 하는 hello 값은 개체, 경우에 특히 모든 속성이 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="93b2b-147">검색 속성 toobe hello 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="93b2b-148">각 반환 된 값을 지정 하는 hello 속성을 가진 개체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="93b2b-149">Hello 전체 JSON 개체 대신 hello JSON 값을 검색 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="93b2b-150">이 달리 `<property_list>` 개체에 hello 프로젝션 값을 래핑하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="93b2b-151">Hello 값 toobe를 나타내는 식을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="93b2b-152">자세한 내용은 [스칼라 식](#bk_scalar_expressions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="93b2b-153">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-153">**Remarks**</span></span>  
  
<span data-ttu-id="93b2b-154">hello `SELECT *` 구문이 올바른지만 FROM 절 정확히 하나의 별칭 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="93b2b-155">`SELECT *`는 ID 프로젝션을 제공하며, 이는 프로젝션이 필요하지 않은 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="93b2b-156">SELECT *는 FROM 절이 지정되고 단일 입력 원본만 도입된 경우에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="93b2b-157">`SELECT <select_list>`과 `SELECT *`는 "syntactic sugar(구문적 설탕)"이며 다음과 같이 간단한 SELECT 문을 사용하여 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="93b2b-158">이는 다음과 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="93b2b-159">이는 다음과 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="93b2b-160">**참고 항목**</span><span class="sxs-lookup"><span data-stu-id="93b2b-160">**See Also**</span></span>  
  
[<span data-ttu-id="93b2b-161">스칼라 식</span><span class="sxs-lookup"><span data-stu-id="93b2b-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="93b2b-162">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="93b2b-163"><a name="bk_from_clause"></a> FROM 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="93b2b-164">Hello 원본 또는 조인 된 원본을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="93b2b-165">hello FROM 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-165">hello FROM clause is optional.</span></span> <span data-ttu-id="93b2b-166">지정하지 않으면 FROM 절에서 단일 문서를 제공하는 것처럼 다른 절도 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="93b2b-167">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="93b2b-168">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="93b2b-169">별칭이 있거나 없는 데이터 원본을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="93b2b-170">별칭이 지정 되지 않은 경우 hello에서 유추할 수는 `<collection_expression>` 다음 규칙을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="93b2b-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="93b2b-171">Hello 식이 collection_name이 별명 이면 collection_name이 별명 별칭으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="93b2b-172">Hello 식이 `<collection_expression>`, property_name을 별칭으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="93b2b-173">Hello 식이 collection_name이 별명 이면 collection_name이 별명 별칭으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="93b2b-174">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="93b2b-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="93b2b-175">해당 hello 지정 `input_alias` 집합 hello 기본 컬렉션 식에서 반환 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="93b2b-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="93b2b-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="93b2b-177">해당 hello 지정 `input_alias` hello hello 기본 컬렉션 식에서 반환 된 각 배열의 모든 배열 요소를 반복 하 여 얻은 값 집합을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="93b2b-178">배열이 아닌 기본 컬렉션 식에서 반환되는 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="93b2b-179">Hello 컬렉션 식 toobe 사용한 tooretrieve hello 문서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="93b2b-180">Hello 기본적으로 현재 연결 된 컬렉션에서 해당 문서를 검색 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="93b2b-181">문서를 제공 하는 hello 컬렉션에서 검색을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="93b2b-182">hello 컬렉션의 hello 이름 hello 컬렉션에 현재 연결의 hello 이름을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="93b2b-183">Hello에서 해당 문서를 검색 하도록 지정 합니다. 제공 된 hello 별칭으로 정의 된 다른 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="93b2b-184">Hello에 액세스 하 여 해당 문서를 검색 하도록 지정 `property_name` 속성 또는 array_index 배열 요소에서 검색 하는 모든 문서에 대 한 컬렉션 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="93b2b-185">Hello에 액세스 하 여 해당 문서를 검색 하도록 지정 `property_name` 속성 또는 array_index 배열 요소에서 검색 하는 모든 문서에 대 한 컬렉션 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="93b2b-186">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-186">**Remarks**</span></span>  
  
<span data-ttu-id="93b2b-187">모든 별칭에에서 제공 되었거나 유추 hello `<from_source>(`s) 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="93b2b-188">hello 구문 `<collection_expression>.`property_name 동일 hello은 `<collection_expression>' ['"property_name"']'`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="93b2b-189">그러나 속성 이름에는 식별자가 아닌 문자가 포함 되어 있으면 hello 두 번째 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="93b2b-190">**누락된 속성, 누락된 배열 요소, 정의되지 않은 값 처리**</span><span class="sxs-lookup"><span data-stu-id="93b2b-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="93b2b-191">컬렉션 식에서 속성이나 배열 요소에 액세스하고 해당 값이 존재하지 않으면 이 값은 무시되고 더 이상 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="93b2b-192">**컬렉션 식 컨텍스트 범위 지정**</span><span class="sxs-lookup"><span data-stu-id="93b2b-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="93b2b-193">컬렉션 식은 컬렉션 범위 또는 문서 범위일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="93b2b-194">식은 컬렉션 범위입니다는 hello 컬렉션 식의 기본 원본이 ROOT 경우 hello 또는 `collection_name`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="93b2b-195">이러한 식은 직접 hello 컬렉션에서 검색 된 문서 집합을 나타내며 다른 컬렉션 식의 hello 처리에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="93b2b-196">식은 문서 범위입니다, hello hello 컬렉션 식의 원본 인지 `input_alias` hello 쿼리 앞부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="93b2b-197">이러한 식은 hello 별칭이 지정 된 컬렉션에 연결 된 toohello 집합에 속한 각 문서의 hello 범위에서 hello 컬렉션 식을 평가 하 여 얻은 문서 집합을을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="93b2b-198">hello 결과 집합에는 각각 hello 문서 집합 기본 hello에 대 한 hello 컬렉션 식을 평가 하 여 얻은 집합의 합집합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="93b2b-199">**조인**</span><span class="sxs-lookup"><span data-stu-id="93b2b-199">**Joins**</span></span>  
  
<span data-ttu-id="93b2b-200">Hello 현재 릴리스에서 Azure Cosmos DB에는 내부 조인을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="93b2b-201">추가 조인 기능이 곧 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="93b2b-202">Hello의 완전 한 교차곱에서 내부 조인 결과 hello 조인에 참여 하 고 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="93b2b-203">N-방향 조인을 hello 결과 hello 튜플의 각 값 hello 조인에 참여 하 고 설정 하는 hello 별칭에 연결 된 하 고 다른 절에서 해당 별칭을 참조 하 여 액세스할 수 있는 N-요소 튜플의 집합.</span><span class="sxs-lookup"><span data-stu-id="93b2b-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="93b2b-204">hello 조인의 hello 평가 hello 참여 하 고 집합의 hello 컨텍스트 범위에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="93b2b-205">컬렉션 집합 A와 컬렉션 범위 집합 B을 조인하면 집합 A와 집합 B에 있는 모든 요소의 교차곱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="93b2b-206">집합 A와 문서 범위 집합 B를 조인하면 집합 A의 각 문서에 대해 문서 범위 집합 B를 평가하여 얻는 모든 집합의 합집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="93b2b-207">Hello 현재 릴리스에서 하나의 컬렉션 범위 식의 최대는 hello 쿼리 프로세서에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="93b2b-208">**조인 예제:**</span><span class="sxs-lookup"><span data-stu-id="93b2b-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="93b2b-209">FROM 절 뒤 hello를 살펴보겠습니다.`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="93b2b-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="93b2b-210">각 원본에서 `input_alias1, input_alias2, …, input_aliasN`을 정의하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="93b2b-211">이 FROM 절은 N 튜플(N개 값이 포함된 튜플)의 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="93b2b-212">각 튜플은 해당 집합에 모든 컬렉션 별칭을 반복하여 생성된 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="93b2b-213">*2개 원본이 있는 조인 예제 1:*</span><span class="sxs-lookup"><span data-stu-id="93b2b-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="93b2b-214">컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="93b2b-215">input_alias1을 참조하는 문서 범위로 `<from_source2>`를 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="93b2b-216">`input_alias1 = A,`의 경우 {1, 2}</span><span class="sxs-lookup"><span data-stu-id="93b2b-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="93b2b-217">`input_alias1 = B,`의 경우 {3}</span><span class="sxs-lookup"><span data-stu-id="93b2b-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="93b2b-218">`input_alias1 = C,`의 경우 {4, 5}</span><span class="sxs-lookup"><span data-stu-id="93b2b-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="93b2b-219">FROM 절 hello `<from_source1> JOIN <from_source2>` hello 튜플 뒤에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="93b2b-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="93b2b-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="93b2b-221">*3개 원본이 있는 조인 예제 2:*</span><span class="sxs-lookup"><span data-stu-id="93b2b-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="93b2b-222">컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="93b2b-223">`input_alias1`을 참조하는 문서 범위로 `<from_source2>`를 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="93b2b-224">`input_alias1 = A,`의 경우 {1, 2}</span><span class="sxs-lookup"><span data-stu-id="93b2b-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="93b2b-225">`input_alias1 = B,`의 경우 {3}</span><span class="sxs-lookup"><span data-stu-id="93b2b-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="93b2b-226">`input_alias1 = C,`의 경우 {4, 5}</span><span class="sxs-lookup"><span data-stu-id="93b2b-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="93b2b-227">`input_alias2`를 참조하는 문서 범위로 `<from_source3>`을 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="93b2b-228">`input_alias2 = 1,`의 경우 {100, 200}</span><span class="sxs-lookup"><span data-stu-id="93b2b-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="93b2b-229">`input_alias2 = 3,`의 경우 {300}</span><span class="sxs-lookup"><span data-stu-id="93b2b-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="93b2b-230">FROM 절 hello `<from_source1> JOIN <from_source2> JOIN <from_source3>` hello 튜플 뒤에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="93b2b-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="93b2b-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="93b2b-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="93b2b-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="93b2b-233">다른 값에는 튜플이 `input_alias1`, `input_alias2`, 어떤 hello에 대 한 `<from_source3>` 값을 반환 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="93b2b-234">*3개 원본이 있는 조인 예제 3:*</span><span class="sxs-lookup"><span data-stu-id="93b2b-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="93b2b-235">컬렉션 범위로 <from_source1>을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="93b2b-236">컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="93b2b-237">input_alias1을 참조하는 문서 범위로 <from_source2>를 지정하고 다음 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="93b2b-238">`input_alias1 = A,`의 경우 {1, 2}</span><span class="sxs-lookup"><span data-stu-id="93b2b-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="93b2b-239">`input_alias1 = B,`의 경우 {3}</span><span class="sxs-lookup"><span data-stu-id="93b2b-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="93b2b-240">`input_alias1 = C,`의 경우 {4, 5}</span><span class="sxs-lookup"><span data-stu-id="93b2b-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="93b2b-241">Let `<from_source3>` 너무 범위를 지정할`input_alias1` 고 다음 집합:</span><span class="sxs-lookup"><span data-stu-id="93b2b-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="93b2b-242">`input_alias2 = A,`의 경우 {100, 200}</span><span class="sxs-lookup"><span data-stu-id="93b2b-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="93b2b-243">`input_alias2 = C,`의 경우 {300}</span><span class="sxs-lookup"><span data-stu-id="93b2b-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="93b2b-244">FROM 절 hello `<from_source1> JOIN <from_source2> JOIN <from_source3>` hello 튜플 뒤에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="93b2b-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="93b2b-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="93b2b-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="93b2b-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="93b2b-247">사이의 교차곱 되었습니다 `<from_source2>` 및 `<from_source3>` 둘 다 범위 지정 된 toohello 때문에 동일한 `<from_source1>`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="93b2b-248">이로 인해 A 값이 있는 4개(2x2) 튜플, B 값이 있는 0개(1x0) 튜플 및 C 값이 있는 2개(2x1) 튜플을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="93b2b-249">**참고 항목**</span><span class="sxs-lookup"><span data-stu-id="93b2b-249">**See also**</span></span>  
  
 [<span data-ttu-id="93b2b-250">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="93b2b-251"><a name="bk_where_clause"></a> WHERE 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="93b2b-252">Hello 쿼리에서 반환 된 hello 문서에 대 한 hello 검색 조건을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="93b2b-253">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="93b2b-254">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="93b2b-255">Hello 조건 toobe hello 문서 toobe 반환에 대해 충족를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="93b2b-256">Hello 값 toobe를 나타내는 식을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="93b2b-257">Hello 참조 [스칼라 식](#bk_scalar_expressions) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="93b2b-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="93b2b-258">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-258">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-259">Hello에 대 한 순서 대로 문서 toobe 필터 조건은 tootrue 유지 되어야 하며 지정 된 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="93b2b-260">부울 값 true hello 조건, 다른 모든 값을 만족 하는 전용: 번호, 배열 또는 개체가 정의 되지 않은, null, false 이면 hello 조건을 만족 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="93b2b-261"><a name="bk_orderby_clause"></a> ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="93b2b-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="93b2b-262">Hello 정렬 순서 hello 쿼리에 의해 반환 된 결과를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="93b2b-263">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="93b2b-264">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="93b2b-265">속성 또는 toosort hello 쿼리 결과 설정 된 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="93b2b-266">정렬 열은 이름 또는 열 별칭으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="93b2b-267">여러 정렬 열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="93b2b-268">열 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-268">Column names must be unique.</span></span> <span data-ttu-id="93b2b-269">hello hello ORDER BY 절에 열 정렬의 hello 시퀀스 hello 조직 hello 정렬 된 결과 집합의 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="93b2b-270">즉, hello 첫 번째 속성으로 hello 결과 집합이 정렬 된 하 고이 정렬 된 목록이 hello 두 번째 속성으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="93b2b-271">hello ORDER BY 절에서 참조 하는 hello 열 이름은 정확 하 게 hello FROM 절에 지정 된 테이블에 정의 된 목록 또는 tooa 열을 선택 하는 열 hello에 tooeither를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="93b2b-272">toosort hello 쿼리 결과 집합에 단일 속성 또는 식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="93b2b-273">Hello 참조 [스칼라 식](#bk_scalar_expressions) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="93b2b-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="93b2b-274">Hello 지정 열의 hello 값을 오름차순 또는 내림차순 정렬 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="93b2b-275">ASC는 hello 가장 작은 값 toohighest 값에서 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="93b2b-276">가장 큰 값 toolowest 값에서 DESC 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="93b2b-277">ASC는 hello 기본 정렬 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-277">ASC is hello default sort order.</span></span> <span data-ttu-id="93b2b-278">Null 값은 hello 가능한 가장 작은 값으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="93b2b-279">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-279">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-280">Hello 쿼리 문법을 지원 하지만 여러 순서 속성으로 계산 된 속성 대해서가 아니라 단일 속성에 대해서만 및 속성 이름에 대해서만 즉, 정렬 hello Azure Cosmos DB 쿼리 런타임의 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="93b2b-281">인덱싱 정책을 해당 hello hello 속성 및 지정 된 hello에 대 한 범위 인덱스를 포함 해야 정렬 hello 최대 정밀도로 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="93b2b-282">Toohello 인덱싱 정책 설명서에 대 한 자세한 내용은 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93b2b-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="93b2b-283"><a name="bk_scalar_expressions"></a> 스칼라 식</span><span class="sxs-lookup"><span data-stu-id="93b2b-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="93b2b-284">스칼라 식이 기호의 조합와 될 수 있는 연산자는 tooobtain 단일 값으로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="93b2b-285">간단한 식은 상수, 속성 참조, 배열 요소 참조, 별칭 참조 또는 함수 호출일 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="93b2b-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="93b2b-286">연산자를 사용하여 복잡한 식으로 결합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="93b2b-287">스칼라 식에 포함될 수 있는 값에 대한 자세한 내용은 [상수](#bk_constants) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="93b2b-288">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="93b2b-289">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="93b2b-290">상수 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-290">Represents a constant value.</span></span> <span data-ttu-id="93b2b-291">자세한 내용은 [상수](#bk_constants) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="93b2b-292">Hello에 정의 된 값을 나타내는 `input_alias` hello에 도입 된 `FROM` 절.</span><span class="sxs-lookup"><span data-stu-id="93b2b-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="93b2b-293">이 값은 절대로 toonot 수 **정의 되지 않은** –**정의 되지 않은** hello 입력의 값에 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="93b2b-294">개체의 hello 속성의 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="93b2b-295">Hello 속성이 없습니다 또는, 개체가 값에서 속성을 참조할 경우 hello 식이 너무**정의 되지 않은** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="93b2b-296">이름의 hello 속성의 값을 나타내는 `property_name` 또는 인덱스가 포함 된 배열 요소 `array_index` 개체/배열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="93b2b-297">Hello 속성/배열 인덱스가 없거나 hello 속성/배열 인덱스가 개체/배열이 값에서 참조 될 경우 hello 식 tooundefined 값을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="93b2b-298">단일 값을 적용 된 tooa 연산자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="93b2b-299">자세한 내용은 [연산자](#bk_operators) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="93b2b-300">연산자를 적용 된 tootwo 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="93b2b-301">자세한 내용은 [연산자](#bk_operators) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="93b2b-302">함수 호출의 결과로 정의되는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="93b2b-303">스칼라 함수를 정의 하는 hello 사용자의 이름.</span><span class="sxs-lookup"><span data-stu-id="93b2b-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="93b2b-304">Hello 기본 제공 스칼라 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="93b2b-305">지정된 속성 및 해당 값이 포함된 새 개체를 만들어서 얻는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="93b2b-306">요소로 지정된 값이 포함된 새 배열을 만들어서 얻는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="93b2b-307">Hello 지정 된 매개 변수 이름의 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="93b2b-308">매개 변수 이름은 hello 첫 번째 문자로 @을 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="93b2b-309">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-309">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-310">기본 제공 또는 사용자 정의 스칼라 함수를 호출할 때 모든 인수가 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="93b2b-311">Hello 인수가 정의 되지 않은 경우 hello 함수를 호출 하지는 및 hello 결과 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="93b2b-312">개체를 만들 때 정의 되지 않은 값이 할당 된 모든 속성은 건너뛰고 hello 만든 개체에에서 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="93b2b-313">모든 요소 값 배열을 만들 할당 된 경우 **정의 되지 않은** 값 건너뛰고 hello 만든 개체에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="93b2b-314">이렇게 하면 다음 정의 hello 요소 tootake 대신 방식으로 해당 만든 hello 배열 됩니다에 건너뛴 인덱스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="93b2b-315"><a name="bk_operators"></a> 연산자</span><span class="sxs-lookup"><span data-stu-id="93b2b-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="93b2b-316">이 섹션에는 지원 hello 연산자에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-316">This section describes hello supported operators.</span></span> <span data-ttu-id="93b2b-317">각 연산자는 하나의 범주 할당된 tooexactly 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="93b2b-318">**undefined** 값 처리 입력 값 형식 요구 사항 및 일치하지 않는 형식의 값 처리에 대한 자세한 내용은 아래의 **연산자 범주** 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="93b2b-319">**연산자 범주**</span><span class="sxs-lookup"><span data-stu-id="93b2b-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="93b2b-320">**범주**</span><span class="sxs-lookup"><span data-stu-id="93b2b-320">**Category**</span></span>|<span data-ttu-id="93b2b-321">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="93b2b-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="93b2b-322">**산술**</span><span class="sxs-lookup"><span data-stu-id="93b2b-322">**arithmetic**</span></span>|<span data-ttu-id="93b2b-323">연산자는 입력은 toobe 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="93b2b-324">출력도 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-324">Output is also a Number.</span></span> <span data-ttu-id="93b2b-325">Hello 입력 중 하나라도 **정의 되지 않은** 번호 다음 hello 결과 외의 다른 형식이 아니거나 **정의 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="93b2b-326">**비트**</span><span class="sxs-lookup"><span data-stu-id="93b2b-326">**bitwise**</span></span>|<span data-ttu-id="93b2b-327">연산자는 입력은 toobe 32 비트 부호 있는 정수 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="93b2b-328">출력도 부호 있는 32비트 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="93b2b-329">정수가 아닌 값은 끝수를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="93b2b-330">양수 값은 끝수 내림되고, 음수 값은 끝수 올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="93b2b-331">2의 보수 표기법의 마지막 32 비트를 수행 하 여 hello 32 비트 정수 범위 밖에 있는 모든 값 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="93b2b-332">Hello 입력 중 하나라도 **정의 되지 않은** 이거나 숫자 이외의 형식인 경우 hello 결과 **정의 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="93b2b-333">**참고:** 동작 위에 hello JavaScript 비트 연산자 동작과 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="93b2b-334">**논리**</span><span class="sxs-lookup"><span data-stu-id="93b2b-334">**logical**</span></span>|<span data-ttu-id="93b2b-335">연산자는 입력은 toobe은 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="93b2b-336">출력도 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="93b2b-337">Hello 입력 중 하나라도 **정의 되지 않은** 이거나 부울 이외의 형식인 hello 결과가 경우 **정의 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="93b2b-338">**비교**</span><span class="sxs-lookup"><span data-stu-id="93b2b-338">**comparison**</span></span>|<span data-ttu-id="93b2b-339">연산자는 입력은 toohave hello 동일 입력 하 고 정의 되지 않은 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="93b2b-340">출력은 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="93b2b-341">Hello 입력 중 하나라도 **정의 되지 않은** 하거나 다른 형식을 사용 했으므로 hello 입력 한 다음 hello 결과 **정의 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="93b2b-342">값 순서 지정에 대한 자세한 내용은 **비교 연산자의 값 순서 지정** 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b2b-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="93b2b-343">**string**</span><span class="sxs-lookup"><span data-stu-id="93b2b-343">**string**</span></span>|<span data-ttu-id="93b2b-344">연산자는 입력은 toobe 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="93b2b-345">출력도 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-345">Output is also a String.</span></span><br /><span data-ttu-id="93b2b-346">Hello 입력 중 하나라도 **정의 되지 않은** hello 다음 문자열 결과 외의 다른 형식이 아니거나 **정의 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="93b2b-347">**단항 연산자:**</span><span class="sxs-lookup"><span data-stu-id="93b2b-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="93b2b-348">**Name**</span><span class="sxs-lookup"><span data-stu-id="93b2b-348">**Name**</span></span>|<span data-ttu-id="93b2b-349">**연산자**</span><span class="sxs-lookup"><span data-stu-id="93b2b-349">**Operator**</span></span>|<span data-ttu-id="93b2b-350">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="93b2b-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="93b2b-351">**산술**</span><span class="sxs-lookup"><span data-stu-id="93b2b-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="93b2b-352">Hello 숫자 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="93b2b-353">비트 부정입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-353">Bitwise negation.</span></span> <span data-ttu-id="93b2b-354">음수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="93b2b-355">**비트**</span><span class="sxs-lookup"><span data-stu-id="93b2b-355">**bitwise**</span></span>|~|<span data-ttu-id="93b2b-356">보수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-356">Ones' complement.</span></span> <span data-ttu-id="93b2b-357">숫자 값의 보수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="93b2b-358">**논리**</span><span class="sxs-lookup"><span data-stu-id="93b2b-358">**Logical**</span></span>|<span data-ttu-id="93b2b-359">**다음이 아님**</span><span class="sxs-lookup"><span data-stu-id="93b2b-359">**NOT**</span></span>|<span data-ttu-id="93b2b-360">부정입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-360">Negation.</span></span> <span data-ttu-id="93b2b-361">부정 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="93b2b-362">**이항 연산자:**</span><span class="sxs-lookup"><span data-stu-id="93b2b-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="93b2b-363">**Name**</span><span class="sxs-lookup"><span data-stu-id="93b2b-363">**Name**</span></span>|<span data-ttu-id="93b2b-364">**연산자**</span><span class="sxs-lookup"><span data-stu-id="93b2b-364">**Operator**</span></span>|<span data-ttu-id="93b2b-365">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="93b2b-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="93b2b-366">**산술**</span><span class="sxs-lookup"><span data-stu-id="93b2b-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="93b2b-367">더하기</span><span class="sxs-lookup"><span data-stu-id="93b2b-367">Addition.</span></span><br /><br /> <span data-ttu-id="93b2b-368">빼기</span><span class="sxs-lookup"><span data-stu-id="93b2b-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="93b2b-369">곱하기</span><span class="sxs-lookup"><span data-stu-id="93b2b-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="93b2b-370">나누기</span><span class="sxs-lookup"><span data-stu-id="93b2b-370">Division.</span></span><br /><br /> <span data-ttu-id="93b2b-371">Modulo 연산</span><span class="sxs-lookup"><span data-stu-id="93b2b-371">Modulation.</span></span>|  
|<span data-ttu-id="93b2b-372">**비트**</span><span class="sxs-lookup"><span data-stu-id="93b2b-372">**bitwise**</span></span>|<span data-ttu-id="93b2b-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="93b2b-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="93b2b-374">비트 OR</span><span class="sxs-lookup"><span data-stu-id="93b2b-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="93b2b-375">비트 AND</span><span class="sxs-lookup"><span data-stu-id="93b2b-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="93b2b-376">비트 XOR</span><span class="sxs-lookup"><span data-stu-id="93b2b-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="93b2b-377">왼쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="93b2b-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="93b2b-378">오른쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="93b2b-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="93b2b-379">0 채우기 오른쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="93b2b-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="93b2b-380">**논리**</span><span class="sxs-lookup"><span data-stu-id="93b2b-380">**logical**</span></span>|<span data-ttu-id="93b2b-381">**및**</span><span class="sxs-lookup"><span data-stu-id="93b2b-381">**AND**</span></span><br /><br /> <span data-ttu-id="93b2b-382">**또는**</span><span class="sxs-lookup"><span data-stu-id="93b2b-382">**OR**</span></span>|<span data-ttu-id="93b2b-383">논리 결합입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-383">Logical conjunction.</span></span> <span data-ttu-id="93b2b-384">두 인수가 **true**이면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-385">논리 결합입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-385">Logical conjunction.</span></span> <span data-ttu-id="93b2b-386">두 인수가 **true**이면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="93b2b-387">**비교**</span><span class="sxs-lookup"><span data-stu-id="93b2b-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="93b2b-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="93b2b-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="93b2b-389">**??**</span><span class="sxs-lookup"><span data-stu-id="93b2b-389">**??**</span></span>|<span data-ttu-id="93b2b-390">같음 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-390">Equals.</span></span> <span data-ttu-id="93b2b-391">두 인수가 같으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-392">같지 않음 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-392">Not equal to.</span></span> <span data-ttu-id="93b2b-393">인수가 같지 않으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-394">큼 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-394">Greater Than.</span></span> <span data-ttu-id="93b2b-395">반환 **true** 첫 번째 인수가 두 번째 식 hello 보다 큰 경우 반환 **false** 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="93b2b-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-396">크거나 같음 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-396">Greater Than or Equal To.</span></span> <span data-ttu-id="93b2b-397">반환 **true** 첫 번째 인수 보다 크면 또는 toohello 두 번째 식과 일치 하는 경우 반환 **false** 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="93b2b-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-398">작음 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-398">Less Than.</span></span> <span data-ttu-id="93b2b-399">반환 **true** 첫 번째 인수 hello 두 번째 식 보다 작은 경우 반환 **false** 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="93b2b-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-400">작거나 같음 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-400">Less Than or Equal To.</span></span> <span data-ttu-id="93b2b-401">반환 **true** 첫 번째 인수 보다 작거나 같은 경우 toohello의 두 번째 하나 반환 **false** 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="93b2b-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="93b2b-402">병합 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-402">Coalesce.</span></span> <span data-ttu-id="93b2b-403">Hello 첫 번째 인수가 반환 hello 두 번째 인수는 **정의 되지 않은** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="93b2b-404">**String**</span><span class="sxs-lookup"><span data-stu-id="93b2b-404">**String**</span></span>|<span data-ttu-id="93b2b-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="93b2b-405">**&#124;&#124;**</span></span>|<span data-ttu-id="93b2b-406">연결 -</span><span class="sxs-lookup"><span data-stu-id="93b2b-406">Concatenation.</span></span> <span data-ttu-id="93b2b-407">두 인수의 연결을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="93b2b-408">**삼항 연산자:**</span><span class="sxs-lookup"><span data-stu-id="93b2b-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="93b2b-409">삼항 연산자</span><span class="sxs-lookup"><span data-stu-id="93b2b-409">Ternary operator</span></span>|<span data-ttu-id="93b2b-410">?</span><span class="sxs-lookup"><span data-stu-id="93b2b-410">?</span></span>|<span data-ttu-id="93b2b-411">반환 너무 hello 첫 번째 인수를 평가 하는 경우 두 번째 인수를 hello**true**; 그렇지 않으면 hello 세 번째 인수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="93b2b-412">**비교 연산자의 값 순서 지정**</span><span class="sxs-lookup"><span data-stu-id="93b2b-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="93b2b-413">**형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-413">**Type**</span></span>|<span data-ttu-id="93b2b-414">**값 순서**</span><span class="sxs-lookup"><span data-stu-id="93b2b-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="93b2b-415">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="93b2b-415">**Undefined**</span></span>|<span data-ttu-id="93b2b-416">비교할 수 없음</span><span class="sxs-lookup"><span data-stu-id="93b2b-416">Not comparable.</span></span>|  
|<span data-ttu-id="93b2b-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="93b2b-417">**Null**</span></span>|<span data-ttu-id="93b2b-418">단일 값: **null**</span><span class="sxs-lookup"><span data-stu-id="93b2b-418">Single value: **null**</span></span>|  
|<span data-ttu-id="93b2b-419">**Number**</span><span class="sxs-lookup"><span data-stu-id="93b2b-419">**Number**</span></span>|<span data-ttu-id="93b2b-420">자연수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="93b2b-421">Negative Infinity(음의 무한대) 값은 다른 Number 값보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="93b2b-422">Positive Infinity(양의 무한대) 값은 다른 Number 값보다 큽니다. **NaN** 값은 비교할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="93b2b-423">**NaN**과 비교하면 **undefined** 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="93b2b-424">**String**</span><span class="sxs-lookup"><span data-stu-id="93b2b-424">**String**</span></span>|<span data-ttu-id="93b2b-425">사전순 정렬</span><span class="sxs-lookup"><span data-stu-id="93b2b-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="93b2b-426">**Array**</span><span class="sxs-lookup"><span data-stu-id="93b2b-426">**Array**</span></span>|<span data-ttu-id="93b2b-427">순서를 지정하지 않지만 동등하게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="93b2b-428">**Object**</span><span class="sxs-lookup"><span data-stu-id="93b2b-428">**Object**</span></span>|<span data-ttu-id="93b2b-429">순서를 지정하지 않지만 동등하게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="93b2b-430">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-430">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-431">Azure Cosmos DB hello 유형의 값 종종 알 수 없는 실제로 hello 데이터베이스에서 검색 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="93b2b-432">순서 toosupport 효율적인 쿼리 실행, 대부분의 hello 연산자에는 엄격한 형식 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="93b2b-433">또한 연산자 자체는 암시적 변환을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="93b2b-434">즉, 쿼리 등의: 선택 * FROM ROOT r WHERE r.Age = 21 보존 기간 같은 toohello 숫자 21 속성을 사용 하 여 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="93b2b-435">속성 사용 기간 같은 toohello 문자열 "21" 또는 hello 문자열 "0021" 문서와 일치 하지 것입니다 "21" hello 식으로 = 21 tooundefined 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="93b2b-436">이 통해 효율적으로 인덱스를 사용 하기 때문에 특정 값의 hello 조회 (예: 숫자 21) 불특정 개수의 잠재적인 일치 항목 (예: 숫자 21 또는 문자열 "21", "021", "21.0" …)에 대 한 검색 보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="93b2b-437">이는 JavaScript에서 다른 형식의 값에 대해 연산자를 평가하는 방식과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="93b2b-438">**배열 및 개체 같음 및 비교**</span><span class="sxs-lookup"><span data-stu-id="93b2b-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="93b2b-439">범위 연산자(>, >=, <, <=)를 사용하여 배열 또는 개체 값을 비교하면 배열 또는 개체 값에 정의된 순서가 없으므로 결과가 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="93b2b-440">그러나 같음/같지 않음 연산자(=, !=, <>)를 사용할 수 있으며, 이 경우 값이 구조적으로 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="93b2b-441">두 배열의 요소 수가 같고 일치하는 위치의 요소도 같은 경우 배열은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="93b2b-442">배열 비교 hello 결과가 정의 되지 않음된, 임의 요소 쌍의 비교 결과가 같은 경우 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="93b2b-443">두 개체에 동일한 속성이 정의되어 있고 일치하는 속성의 값도 같은 경우 개체는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="93b2b-444">개체 비교 hello 결과가 정의 되지 않은 속성 값 쌍의 비교 결과가 같은 경우 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="93b2b-445"><a name="bk_constants"></a> 상수</span><span class="sxs-lookup"><span data-stu-id="93b2b-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="93b2b-446">리터럴 또는 스칼라 값이라고도 하는 상수는 특정 데이터 값을 나타내는 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="93b2b-447">상수의 형식은 hello 나타내는 hello 값의 hello 데이터 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="93b2b-448">**지원되는 스칼라 데이터 형식:**</span><span class="sxs-lookup"><span data-stu-id="93b2b-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="93b2b-449">**형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-449">**Type**</span></span>|<span data-ttu-id="93b2b-450">**값 순서**</span><span class="sxs-lookup"><span data-stu-id="93b2b-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="93b2b-451">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="93b2b-451">**Undefined**</span></span>|<span data-ttu-id="93b2b-452">단일 값: **undefined**</span><span class="sxs-lookup"><span data-stu-id="93b2b-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="93b2b-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="93b2b-453">**Null**</span></span>|<span data-ttu-id="93b2b-454">단일 값: **null**</span><span class="sxs-lookup"><span data-stu-id="93b2b-454">Single value: **null**</span></span>|  
|<span data-ttu-id="93b2b-455">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="93b2b-455">**Boolean**</span></span>|<span data-ttu-id="93b2b-456">값: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="93b2b-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="93b2b-457">**Number**</span><span class="sxs-lookup"><span data-stu-id="93b2b-457">**Number**</span></span>|<span data-ttu-id="93b2b-458">IEEE 754 표준의 두 자리 부동 소수점 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="93b2b-459">**String**</span><span class="sxs-lookup"><span data-stu-id="93b2b-459">**String**</span></span>|<span data-ttu-id="93b2b-460">0개 이상의 유니코드 문자 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="93b2b-461">문자열은 작은따옴표 또는 큰 따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="93b2b-462">**Array**</span><span class="sxs-lookup"><span data-stu-id="93b2b-462">**Array**</span></span>|<span data-ttu-id="93b2b-463">0개 이상의 요소 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="93b2b-464">각 요소는 Undefined를 제외한 모든 스칼라 데이터 형식의 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="93b2b-465">**Object**</span><span class="sxs-lookup"><span data-stu-id="93b2b-465">**Object**</span></span>|<span data-ttu-id="93b2b-466">순서가 지정되지 않은 0개 이상의 이름/값 쌍의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="93b2b-467">이름은 유니코드 문자열이며, 값은 **Undefined**를 제외한 모든 스칼라 데이터 형식이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="93b2b-468">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="93b2b-469">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="93b2b-470">Undefined 형식의 undefined 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="93b2b-471">**Null** 형식의 **null** 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="93b2b-472">Boolean 형식의 상수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="93b2b-473">Boolean 형식의 **false** 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="93b2b-474">Boolean 형식의 **true** 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="93b2b-475">상수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="93b2b-476">10진 리터럴은 10진수 표기법 또는 과학적 표기법을 사용하여 표현되는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="93b2b-477">16진 리터럴은 '0x' 접두사 다음에 하나 이상의 16진수가 나오는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="93b2b-478">String 형식의 상수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="93b2b-479">문자열 리터럴은 연속적인 0이상의 유니코드 문자 또는 이스케이프 시퀀스로 표현되는 유니코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="93b2b-480">문자열 리터럴은 작은따옴표(아포스트로피: ') 또는 큰따옴표(따옴표: ")로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="93b2b-481">허용되는 이스케이프 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="93b2b-482">**이스케이프 시퀀스**</span><span class="sxs-lookup"><span data-stu-id="93b2b-482">**Escape sequence**</span></span>|<span data-ttu-id="93b2b-483">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-483">**Description**</span></span>|<span data-ttu-id="93b2b-484">**유니코드 문자**</span><span class="sxs-lookup"><span data-stu-id="93b2b-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="93b2b-485">\\'</span><span class="sxs-lookup"><span data-stu-id="93b2b-485">\\'</span></span>|<span data-ttu-id="93b2b-486">아포스트로피(')</span><span class="sxs-lookup"><span data-stu-id="93b2b-486">apostrophe (')</span></span>|<span data-ttu-id="93b2b-487">U+0027</span><span class="sxs-lookup"><span data-stu-id="93b2b-487">U+0027</span></span>|  
|<span data-ttu-id="93b2b-488">\\"</span><span class="sxs-lookup"><span data-stu-id="93b2b-488">\\"</span></span>|<span data-ttu-id="93b2b-489">따옴표(")</span><span class="sxs-lookup"><span data-stu-id="93b2b-489">quotation mark (")</span></span>|<span data-ttu-id="93b2b-490">U+0022</span><span class="sxs-lookup"><span data-stu-id="93b2b-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="93b2b-491">백슬래시(\\)</span><span class="sxs-lookup"><span data-stu-id="93b2b-491">reverse solidus (\\)</span></span>|<span data-ttu-id="93b2b-492">U+005C</span><span class="sxs-lookup"><span data-stu-id="93b2b-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="93b2b-493">슬래시(/)</span><span class="sxs-lookup"><span data-stu-id="93b2b-493">solidus (/)</span></span>|<span data-ttu-id="93b2b-494">U+002F</span><span class="sxs-lookup"><span data-stu-id="93b2b-494">U+002F</span></span>|  
|<span data-ttu-id="93b2b-495">\b</span><span class="sxs-lookup"><span data-stu-id="93b2b-495">\b</span></span>|<span data-ttu-id="93b2b-496">백스페이스</span><span class="sxs-lookup"><span data-stu-id="93b2b-496">backspace</span></span>|<span data-ttu-id="93b2b-497">U+0008</span><span class="sxs-lookup"><span data-stu-id="93b2b-497">U+0008</span></span>|  
|<span data-ttu-id="93b2b-498">\f</span><span class="sxs-lookup"><span data-stu-id="93b2b-498">\f</span></span>|<span data-ttu-id="93b2b-499">폼 피드</span><span class="sxs-lookup"><span data-stu-id="93b2b-499">form feed</span></span>|<span data-ttu-id="93b2b-500">U+000C</span><span class="sxs-lookup"><span data-stu-id="93b2b-500">U+000C</span></span>|  
|\n|<span data-ttu-id="93b2b-501">줄 바꿈</span><span class="sxs-lookup"><span data-stu-id="93b2b-501">line feed</span></span>|<span data-ttu-id="93b2b-502">U+000A</span><span class="sxs-lookup"><span data-stu-id="93b2b-502">U+000A</span></span>|  
|<span data-ttu-id="93b2b-503">\r</span><span class="sxs-lookup"><span data-stu-id="93b2b-503">\r</span></span>|<span data-ttu-id="93b2b-504">캐리지 리턴</span><span class="sxs-lookup"><span data-stu-id="93b2b-504">carriage return</span></span>|<span data-ttu-id="93b2b-505">U+000D</span><span class="sxs-lookup"><span data-stu-id="93b2b-505">U+000D</span></span>|  
|<span data-ttu-id="93b2b-506">\t</span><span class="sxs-lookup"><span data-stu-id="93b2b-506">\t</span></span>|<span data-ttu-id="93b2b-507">탭</span><span class="sxs-lookup"><span data-stu-id="93b2b-507">tab</span></span>|<span data-ttu-id="93b2b-508">U+0009</span><span class="sxs-lookup"><span data-stu-id="93b2b-508">U+0009</span></span>|  
|<span data-ttu-id="93b2b-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="93b2b-509">\uXXXX</span></span>|<span data-ttu-id="93b2b-510">4자리 16진수로 정의된 유니코드 문자</span><span class="sxs-lookup"><span data-stu-id="93b2b-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="93b2b-511">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="93b2b-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="93b2b-512"><a name="bk_query_perf_guidelines"></a> 쿼리 성능 지침</span><span class="sxs-lookup"><span data-stu-id="93b2b-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="93b2b-513">대형 컬렉션에 대해 효율적으로 실행 하는 쿼리 toobe에서 하나 이상의 인덱스를 통해 제공 될 수 있는 필터를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="93b2b-514">다음 필터는 hello 인덱스 검색에 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="93b2b-515">문서 경로 식 및 상수와 함께 같음 연산자(=)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="93b2b-516">문서 경로 식 및 상수와 함께 범위 연산자(<, \<=, >, >=)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="93b2b-517">문서 경로 식에는 참조 하는 hello 데이터베이스 컬렉션에서 hello 문서의 상수 경로 식별 하는 모든 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="93b2b-518">**문서 경로 식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="93b2b-519">문서 경로 식은 데이터베이스 수집 문서에서 제공하는 문서를 통해 속성 또는 배열 인덱서의 경로를 평가하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="93b2b-520">Hello 데이터베이스 컬렉션에서 hello 문서 내에서 직접 필터에서 참조 하는 값의 사용된 tooidentify hello 위치 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="93b2b-521">문서 경로 식으로 간주 하는 식 toobe에 대 한 다음과 같은 것을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="93b2b-522">참조 hello 컬렉션 루트 직접입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="93b2b-523">일부 문서 경로 식의 속성 또는 상수 배열 인덱서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="93b2b-524">일부 문서 경로 식을 나타내는 별칭을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="93b2b-525">**구문 규칙**</span><span class="sxs-lookup"><span data-stu-id="93b2b-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="93b2b-526">다음 표에서 hello hello DocumentDB API 쿼리 언어 참조에 hello 사용 되는 규칙 toodescribe 구문에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="93b2b-527">**규칙**</span><span class="sxs-lookup"><span data-stu-id="93b2b-527">**Convention**</span></span>|<span data-ttu-id="93b2b-528">**용도**</span><span class="sxs-lookup"><span data-stu-id="93b2b-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="93b2b-529">대문자</span><span class="sxs-lookup"><span data-stu-id="93b2b-529">UPPERCASE</span></span>|<span data-ttu-id="93b2b-530">대/소문자를 구분하지 않는 키워드</span><span class="sxs-lookup"><span data-stu-id="93b2b-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="93b2b-531">소문자</span><span class="sxs-lookup"><span data-stu-id="93b2b-531">lowercase</span></span>|<span data-ttu-id="93b2b-532">대/소문자를 구분하는 키워드</span><span class="sxs-lookup"><span data-stu-id="93b2b-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="93b2b-533">\<nonterminal></span><span class="sxs-lookup"><span data-stu-id="93b2b-533">\<nonterminal></span></span>|<span data-ttu-id="93b2b-534">비단말(nonterminal)이며, 개별적으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="93b2b-535">\<nonterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="93b2b-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="93b2b-536">Hello 비터미널의 구문 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="93b2b-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="93b2b-537">other_terminal</span></span>|<span data-ttu-id="93b2b-538">단말(토큰)이며, 단어로 자세히 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="93b2b-539">identifier</span><span class="sxs-lookup"><span data-stu-id="93b2b-539">identifier</span></span>|<span data-ttu-id="93b2b-540">식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-540">Identifier.</span></span> <span data-ttu-id="93b2b-541">허용되는 문자: a-z, A-Z, 0-9. 첫 번째 문자는 숫자가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="93b2b-542">"문자열"</span><span class="sxs-lookup"><span data-stu-id="93b2b-542">"string"</span></span>|<span data-ttu-id="93b2b-543">따옴표가 붙은 문자열이며,</span><span class="sxs-lookup"><span data-stu-id="93b2b-543">Quoted string.</span></span> <span data-ttu-id="93b2b-544">유효한 문자열이 모두 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-544">Allows any valid string.</span></span> <span data-ttu-id="93b2b-545">string_literal에 대한 설명을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="93b2b-546">'기호'</span><span class="sxs-lookup"><span data-stu-id="93b2b-546">'symbol'</span></span>|<span data-ttu-id="93b2b-547">Hello 구문의 일부인 리터럴 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="93b2b-548">&#124; (세로줄)</span><span class="sxs-lookup"><span data-stu-id="93b2b-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="93b2b-549">구문 항목에 대한 대안이며,</span><span class="sxs-lookup"><span data-stu-id="93b2b-549">Alternatives for syntax items.</span></span> <span data-ttu-id="93b2b-550">지정 된 hello 항목 중 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="93b2b-551">[ ] /(대괄호)</span><span class="sxs-lookup"><span data-stu-id="93b2b-551">[ ] /(brackets)</span></span>|<span data-ttu-id="93b2b-552">대괄호는 하나 이상의 선택 항목을 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="93b2b-553">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="93b2b-553">[ ,...n ]</span></span>|<span data-ttu-id="93b2b-554">Hello 항목 앞에 n 번 반복된 될 수 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="93b2b-555">hello 항목은 쉼표로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="93b2b-556">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="93b2b-556">[ ...n ]</span></span>|<span data-ttu-id="93b2b-557">Hello 항목 앞에 n 번 반복된 될 수 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="93b2b-558">hello 항목은 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="93b2b-559"><a name="bk_built_in_functions"></a> 기본 제공 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="93b2b-560">Azure Cosmos DB는 많은 기본 제공 SQL 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="93b2b-561">기본 제공 함수의 hello 범주는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="93b2b-562">함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-562">Function</span></span>|<span data-ttu-id="93b2b-563">설명</span><span class="sxs-lookup"><span data-stu-id="93b2b-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="93b2b-564">수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="93b2b-565">일반적으로 인수로 제공 되 고 숫자 값을 반환 하는 입력된 값에 따라 계산을 수행 하는 hello 각 수치 연산 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="93b2b-566">형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="93b2b-567">hello 형식 검사 함수는 toocheck hello 유형의 SQL 쿼리 내에서 식 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="93b2b-568">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="93b2b-569">hello 문자열 함수는 문자열 입력된 값에 대 한 작업을 수행 하 고 문자열, 숫자 또는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="93b2b-570">배열 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="93b2b-571">hello 배열 함수는 배열 입력된 값 및 숫자 반환에 대 한 작업이, 부울 또는 배열 값을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="93b2b-572">공간 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="93b2b-573">hello 공간 함수는 값을 입력된 공간 개체에 대 한 작업을 수행 하 고 숫자 또는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="93b2b-574"><a name="bk_mathematical_functions"></a> 수치 연산 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="93b2b-575">hello 다음 함수는 계산을 수행할 일반적으로 인수로 제공 되 고 숫자 값을 반환 하는 입력된 값에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="93b2b-576">ABS</span><span class="sxs-lookup"><span data-stu-id="93b2b-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="93b2b-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="93b2b-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="93b2b-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="93b2b-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="93b2b-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="93b2b-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="93b2b-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="93b2b-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="93b2b-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="93b2b-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="93b2b-582">COS</span><span class="sxs-lookup"><span data-stu-id="93b2b-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="93b2b-583">COT</span><span class="sxs-lookup"><span data-stu-id="93b2b-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="93b2b-584">각도</span><span class="sxs-lookup"><span data-stu-id="93b2b-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="93b2b-585">EXP</span><span class="sxs-lookup"><span data-stu-id="93b2b-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="93b2b-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="93b2b-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="93b2b-587">로그</span><span class="sxs-lookup"><span data-stu-id="93b2b-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="93b2b-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="93b2b-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="93b2b-589">PI</span><span class="sxs-lookup"><span data-stu-id="93b2b-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="93b2b-590">전원</span><span class="sxs-lookup"><span data-stu-id="93b2b-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="93b2b-591">라디안</span><span class="sxs-lookup"><span data-stu-id="93b2b-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="93b2b-592">반올림</span><span class="sxs-lookup"><span data-stu-id="93b2b-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="93b2b-593">SIN</span><span class="sxs-lookup"><span data-stu-id="93b2b-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="93b2b-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="93b2b-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="93b2b-595">정사각형</span><span class="sxs-lookup"><span data-stu-id="93b2b-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="93b2b-596">로그인</span><span class="sxs-lookup"><span data-stu-id="93b2b-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="93b2b-597">TAN</span><span class="sxs-lookup"><span data-stu-id="93b2b-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="93b2b-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="93b2b-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="93b2b-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="93b2b-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="93b2b-600">Hello 절대 (양수)의 값을 반환 hello 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-601">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-602">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-603">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-604">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-604">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-605">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-606">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-606">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-607">hello 다음 예제에서는 세 개의 다른 숫자에서 hello ABS 함수를 사용 하는 hello 결과</span><span class="sxs-lookup"><span data-stu-id="93b2b-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="93b2b-608">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="93b2b-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="93b2b-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="93b2b-610">반환 hello 각도 라디안 코사인이 hello 지정 된 숫자 식입니다. 아크코사인이 라고도합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="93b2b-611">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-612">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-613">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-614">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-614">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-615">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-616">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-616">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-617">hello 다음 예제에서는 반환 hello-1의 ACOS 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="93b2b-618">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="93b2b-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="93b2b-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="93b2b-620">사인이 hello 라디안 단위로 반환 hello 각도 숫자 식 지정.</span><span class="sxs-lookup"><span data-stu-id="93b2b-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="93b2b-621">아크사인이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="93b2b-622">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-623">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-624">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-625">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-625">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-626">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-627">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-627">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-628">hello 다음 예제에서는 반환 hello-1의 ASIN 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="93b2b-629">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="93b2b-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="93b2b-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="93b2b-631">반환 hello 각도 라디안의 탄젠트는 hello 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="93b2b-632">아크탄젠트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="93b2b-633">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-634">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-635">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-636">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-636">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-637">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-638">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-638">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-639">다음 예제에서는 반환 hello hello의 ATAN hello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="93b2b-640">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="93b2b-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="93b2b-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="93b2b-642">라디안에서으로 표현 hello 아크 탄젠트 y / x의 hello 주요 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="93b2b-643">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-644">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-645">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-646">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-646">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-647">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-648">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-648">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-649">hello 다음 예제에서는 계산 지정 hello에 대 한 hello ATN2 x 및 y 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="93b2b-650">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="93b2b-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="93b2b-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="93b2b-652">Hello, 보다 큰 가장 작은 정수 값 또는 같음, hello 특정된 숫자 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-653">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-654">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-655">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-656">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-656">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-657">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-658">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-658">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-659">사용 하 여 0 값에 CEILING 함수 hello 및 hello 다음 예에서는 양수, 음수 이면를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="93b2b-660">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="93b2b-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="93b2b-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="93b2b-662">반환 hello hello의 삼각 코사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="93b2b-663">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-664">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-665">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-666">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-666">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-667">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-668">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-668">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-669">다음 예에서는 hello 지정 된 각도의 hello COS hello를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="93b2b-670">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="93b2b-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="93b2b-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="93b2b-672">반환 hello hello의 삼각 코탄젠트 각도 라디안에서으로 지정 된, hello에 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-673">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-674">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-675">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-676">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-676">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-677">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-678">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-678">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-679">다음 예에서는 hello hello hello 지정 된 각도의 COT를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="93b2b-680">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="93b2b-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="93b2b-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="93b2b-682">반환 hello 해당 각도에서 라디안에서으로 지정 된 각도의 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="93b2b-683">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-684">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-685">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-686">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-686">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-687">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-688">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-688">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-689">hello 다음 예제에서는 hello 개수의 반환도 PI/2 라디안 각도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="93b2b-690">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="93b2b-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="93b2b-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="93b2b-692">작은 hello 가장 큰 정수를 반환 toohello 같거나 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-693">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-694">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-695">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-696">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-696">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-697">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-698">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-698">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-699">0 값으로 FLOOR 함수 hello 및 hello 다음 예에서는 양수, 음수 이면를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="93b2b-700">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="93b2b-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="93b2b-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="93b2b-702">Hello의 hello 지 수 값 반환을 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-703">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-704">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-705">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-706">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-706">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-707">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-708">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-708">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-709">hello 상수 **e** (2.718281 …)는 자연 로그의 기본 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="93b2b-710">hello 숫자의 지 수는 hello 상수 **e** hello 숫자의 거듭제곱 toohello 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="93b2b-711">예를 들어 EXP(1.0) = e^1.0 = 2.71828182845905이며, EXP(10) = e^10 = 22026.4657948067입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="93b2b-712">자체 hello 번호 hello 숫자의 자연 로그 hello의 지 수: 즉, EXP (LOG (n)) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="93b2b-713">Hello hello 숫자의 지 수 자연 로그는 자체 hello 번호: LOG (EXP (n)) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="93b2b-714">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-714">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-715">hello 다음 예제에서는 변수를 선언 하 고 hello hello 지정한 변수 (10)의 지 수 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="93b2b-716">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="93b2b-717">hello 다음 예제에서는 값을 반환 hello 지 수 20의 자연 로그 hello 및 hello의 hello 자연 로그 20의 지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="93b2b-718">이러한 함수는 역함수 서로 hello 부동 소수점 수학 두 경우 모두 20는 반올림 된 반환 값 때문에입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="93b2b-719">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="93b2b-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="93b2b-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="93b2b-721">Hello의 반환 hello 자연 로그를 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-722">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="93b2b-723">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-724">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="93b2b-725">Hello hello 로그에 대 한 기본 설정 하는 선택적인 숫자 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="93b2b-726">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-726">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-727">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-728">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-728">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-729">Log ()는 기본적으로 hello 자연 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="93b2b-730">Hello 선택적인 base 매개 변수를 사용 하 여 hello 로그 tooanother 값의 기수로 서 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="93b2b-731">hello 자연 로그는 hello 로그 toohello 기본 **e**여기서 **e** 는 무리 상수 약 too2.718281828 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="93b2b-732">hello hello 숫자의 지 수 자연 로그는 자체 hello 번호: LOG (EXP (n)) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="93b2b-733">자체 hello 번호 hello 숫자의 자연 로그 hello의 지 수: 즉, EXP (LOG (n)) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="93b2b-734">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-734">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-735">hello 다음 예제에서는 변수를 선언 하 고 hello 지정한 변수 (10)의 hello 로그 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="93b2b-736">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="93b2b-737">hello 다음 예제에서는 계산 숫자의 지 수 hello에 대 한 로그 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="93b2b-738">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="93b2b-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="93b2b-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="93b2b-740">Hello의 반환 hello 밑이 10 인 로그를 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-741">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-742">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-743">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-744">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-744">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-745">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-746">**설명**</span><span class="sxs-lookup"><span data-stu-id="93b2b-746">**Remarks**</span></span>  
  
 <span data-ttu-id="93b2b-747">hello LOG10 및 POWER 함수는 역함수 관련된 tooone 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="93b2b-748">예를 들어 10 ^ LOG10(n) = n입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="93b2b-749">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-749">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-750">hello 다음 예제에서는 변수를 선언 하 고 hello 지정한 변수 (100)의 hello LOG10 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="93b2b-751">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="93b2b-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="93b2b-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="93b2b-753">반환 hello PI의 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="93b2b-754">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="93b2b-755">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-756">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-757">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-757">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-758">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-759">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-759">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-760">다음 예제에서는 PI의 hello 값을 반환 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="93b2b-761">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="93b2b-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="93b2b-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="93b2b-763">반환 값의 지정 된 hello hello 식 toohello 지정 된 거듭제곱 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="93b2b-764">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="93b2b-765">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-766">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="93b2b-767">Hello 전원 toowhich tooraise은 `numeric_expression`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="93b2b-768">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-768">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-769">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-770">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-770">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-771">다음 예제는 hello 숫자 toohello 거듭제곱 3 (hello hello 숫자의 세제곱) 발생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="93b2b-772">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="93b2b-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="93b2b-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="93b2b-774">숫자 식을 단위로 입력하면 라디안을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="93b2b-775">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-776">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-777">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-778">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-778">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-779">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-780">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-780">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-781">hello 다음 예제에서는 몇 개의 각도 입력으로 사용 하 고 해당 라디안 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="93b2b-782">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="93b2b-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="93b2b-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="93b2b-784">숫자 값을 반올림된 toohello 가장 가까운 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="93b2b-785">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-786">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-787">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-788">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-788">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-789">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-790">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-790">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-791">hello 다음 예제에서는 반올림 양수와 음수 toohello 정수 가장 가까운 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="93b2b-792">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="93b2b-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="93b2b-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="93b2b-794">반환 hello 양수 (+ 1), 영 (0) 또는 지정 된 숫자 식의 hello 음수 (-1) 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-795">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-796">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-797">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-798">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-798">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-799">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-800">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-800">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-801">hello 다음 예제에서는 숫자의 hello SIGN 값에서에서 반환-2 too2 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="93b2b-802">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="93b2b-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="93b2b-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="93b2b-804">반환 hello hello의 삼각 사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="93b2b-805">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-806">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-807">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-808">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-808">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-809">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-810">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-810">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-811">다음 예에서는 hello hello 지정 된 각도의 SIN hello를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="93b2b-812">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="93b2b-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="93b2b-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="93b2b-814">Hello의 반환 hello 제곱근 숫자 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="93b2b-815">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-816">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-817">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-818">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-818">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-819">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-820">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-820">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-821">hello 다음 예제에서는 반환 hello 숫자 1-3의 제곱근입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="93b2b-822">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="93b2b-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="93b2b-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="93b2b-824">Hello의 제곱 반환 hello 숫자 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="93b2b-825">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-826">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-827">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-828">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-828">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-829">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-830">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-830">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-831">hello 다음 예제에서는 반환 hello 숫자 1-3 제곱 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="93b2b-832">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="93b2b-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="93b2b-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="93b2b-834">Hello의 반환 hello 탄젠트 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="93b2b-835">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-836">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-837">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-838">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-838">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-839">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-840">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-840">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-841">hello 다음 예제에서는 hello의 탄젠트를 계산 PI () / 2입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="93b2b-842">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="93b2b-843"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="93b2b-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="93b2b-844">숫자 값, 잘린된 toohello 가장 가까운 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="93b2b-845">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="93b2b-846">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="93b2b-847">숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-848">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-848">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-849">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-850">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-850">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-851">다음 예제는 hello를 양수와 음수 toohello 가장 가까운 정수 값을 다음 hello를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="93b2b-852">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="93b2b-853"><a name="bk_type_checking_functions"></a> 형식 검사 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="93b2b-854">hello 다음 함수는 지원 형식 입력된 값에 대해 검사 하 고 각각 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="93b2b-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="93b2b-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="93b2b-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="93b2b-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="93b2b-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="93b2b-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="93b2b-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="93b2b-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="93b2b-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="93b2b-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="93b2b-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="93b2b-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="93b2b-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="93b2b-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="93b2b-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="93b2b-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="93b2b-863"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="93b2b-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="93b2b-864">배열 hello hello 유형의 식을 지정 된 경우를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="93b2b-865">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="93b2b-866">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-867">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-868">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-868">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-869">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-870">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-870">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-871">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_ARRAY 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-872">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="93b2b-873"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="93b2b-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="93b2b-874">지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 부울을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="93b2b-875">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="93b2b-876">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-877">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-878">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-878">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-879">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-880">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-880">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-881">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello에서는 IS_BOOL 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-882">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="93b2b-883"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="93b2b-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="93b2b-884">경우 hello 속성 값이 할당에 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="93b2b-885">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="93b2b-886">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-887">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-888">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-888">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-889">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-890">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-890">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-891">hello hello 내에 속성이 있는지에 대 한 예제 검사를 수행 하는 hello JSON 문서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="93b2b-892">"a"가 존재 하지만 "b"가 없으므로 hello은 두 번째 false를 반환 하는 이후 hello은 먼저 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="93b2b-893">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="93b2b-894"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="93b2b-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="93b2b-895">지정 된 식 hello hello 유형의 경우를 나타내는 부울 값이 null을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="93b2b-896">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="93b2b-897">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-898">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-899">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-899">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-900">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-901">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-901">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-902">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_NULL 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-903">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="93b2b-904"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="93b2b-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="93b2b-905">Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="93b2b-906">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="93b2b-907">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-908">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-909">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-909">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-910">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-911">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-911">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-912">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_NULL 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-913">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="93b2b-914"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="93b2b-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="93b2b-915">지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 JSON 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="93b2b-916">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="93b2b-917">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-918">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-919">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-919">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-920">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-921">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-921">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-922">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_OBJECT 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-923">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="93b2b-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="93b2b-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="93b2b-925">Hello의 hello 형식이 지정 되는 기본 식을 나타내는 부울 값을 반환 합니다 (문자열, 부울, 숫자 또는 null).</span><span class="sxs-lookup"><span data-stu-id="93b2b-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="93b2b-926">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="93b2b-927">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-928">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-929">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-929">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-930">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-931">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-931">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-932">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello에서는 IS_PRIMITIVE 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-933">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="93b2b-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="93b2b-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="93b2b-935">Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 문자열로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="93b2b-936">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="93b2b-937">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="93b2b-938">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-939">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-939">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-940">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-941">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-941">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-942">hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello에서는 IS_STRING 함수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93b2b-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="93b2b-943">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="93b2b-944"><a name="bk_string_functions"></a> 문자열 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="93b2b-945">hello 다음 스칼라 함수는 문자열 입력된 값에 대 한 작업을 수행 하 고 문자열, 숫자 또는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="93b2b-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="93b2b-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="93b2b-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="93b2b-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="93b2b-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="93b2b-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="93b2b-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="93b2b-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="93b2b-950">왼쪽</span><span class="sxs-lookup"><span data-stu-id="93b2b-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="93b2b-951">LENGTH</span><span class="sxs-lookup"><span data-stu-id="93b2b-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="93b2b-952">낮은</span><span class="sxs-lookup"><span data-stu-id="93b2b-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="93b2b-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="93b2b-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="93b2b-954">바꾸기</span><span class="sxs-lookup"><span data-stu-id="93b2b-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="93b2b-955">복제</span><span class="sxs-lookup"><span data-stu-id="93b2b-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="93b2b-956">역방향</span><span class="sxs-lookup"><span data-stu-id="93b2b-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="93b2b-957">오른쪽</span><span class="sxs-lookup"><span data-stu-id="93b2b-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="93b2b-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="93b2b-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="93b2b-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="93b2b-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="93b2b-960">하위 문자열</span><span class="sxs-lookup"><span data-stu-id="93b2b-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="93b2b-961">위</span><span class="sxs-lookup"><span data-stu-id="93b2b-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="93b2b-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="93b2b-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="93b2b-963">않은 hello 두 개 이상의 문자열 값을 연결한 결과인 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="93b2b-964">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="93b2b-965">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-966">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-967">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-967">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-968">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-969">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-969">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-970">다음 예에서는 hello의 hello 연결 문자열을 반환 하는 hello에 지정 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="93b2b-971">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="93b2b-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="93b2b-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="93b2b-973">첫 번째 문자열 식 hello hello를 두 번째로 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="93b2b-974">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="93b2b-975">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-976">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-977">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-977">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-978">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-979">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-979">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-980">hello 다음 예제에서는 "abc" "ab"를 포함 하 고 "d"를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="93b2b-981">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="93b2b-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="93b2b-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="93b2b-983">끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="93b2b-984">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="93b2b-985">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-986">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-987">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-987">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-988">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-989">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-989">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-990">hello 다음 예제에서는 반환 hello "abc"는 "b" 및 "bc"로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="93b2b-991">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="93b2b-992"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="93b2b-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="93b2b-993">Hello hello 문자열을 찾을 수 없는 경우 시작 hello hello hello 첫 번째 지정 된 문자열 식 또는-1 내에서 두 번째 문자열 식의 첫 번째 발생 위치를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="93b2b-994">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="93b2b-995">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-996">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-997">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-997">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-998">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-999">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-999">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1000">hello 다음 예에서는 인덱스를 반환 hello "abc" 내의 다양 한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="93b2b-1001">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="93b2b-1002"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="93b2b-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="93b2b-1003">반환 문자열의 왼쪽된 부분을 지정 하는 hello로 hello 문자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="93b2b-1004">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="93b2b-1005">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1006">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="93b2b-1007">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-1008">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1009">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1010">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1010">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1011">hello 다음 예제에서는 반환 다양 한 길이 값에 대해 "abc"의 왼쪽 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="93b2b-1012">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="93b2b-1013"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="93b2b-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="93b2b-1014">Hello의 문자 수를 반환 합니다 hello 지정 된 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1015">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1016">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1017">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1018">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1019">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1020">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1020">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1021">hello 다음 예제에서는 반환 문자열의 길이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="93b2b-1022">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="93b2b-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="93b2b-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="93b2b-1024">대문자 데이터 toolowercase 변환한 후 문자열 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="93b2b-1025">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1026">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1027">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1028">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1029">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1030">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1030">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1031">hello 방법을 예제와 다음 하위 쿼리에서 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="93b2b-1032">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="93b2b-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="93b2b-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="93b2b-1034">선행 공백을 제거한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="93b2b-1035">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1036">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1037">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1038">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1039">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1040">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1040">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1041">hello 방법을 예제와 다음 쿼리에서 LTRIM toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="93b2b-1042">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="93b2b-1043"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="93b2b-1044">지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="93b2b-1045">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1046">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1047">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1048">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1049">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1050">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1050">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1051">다음 예제는 hello toouse 쿼리에서 대체 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="93b2b-1052">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="93b2b-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="93b2b-1054">문자열 값을 지정한 횟수 만큼 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="93b2b-1055">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="93b2b-1056">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1057">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="93b2b-1058">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-1059">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1060">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1061">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1061">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1062">다음 예제는 hello toouse 쿼리에서 복제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="93b2b-1063">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="93b2b-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="93b2b-1065">Hello는 문자열 값의 역순을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="93b2b-1066">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1067">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1068">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1069">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1070">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1071">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1071">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1072">다음 예제는 hello toouse 쿼리에서 REVERSE 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="93b2b-1073">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="93b2b-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="93b2b-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="93b2b-1075">Hello로 반환 hello 오른쪽 부분 문자열의 문자 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="93b2b-1076">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="93b2b-1077">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1078">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="93b2b-1079">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-1080">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1081">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1082">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1082">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1083">hello 다음 예제에서는 hello 오른쪽 부분을 반환 "abc"의 다양 한 길이 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="93b2b-1084">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="93b2b-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="93b2b-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="93b2b-1086">후행 공백을 제거한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="93b2b-1087">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1088">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1089">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1090">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1091">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1092">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1092">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1093">hello 방법을 예제와 다음 쿼리에서 RTRIM toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="93b2b-1094">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="93b2b-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="93b2b-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="93b2b-1096">시작 하는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="93b2b-1097">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1098">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1099">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1100">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1101">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-1102">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1102">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1103">hello 검사 경우 hello 문자열 "abc"는 다음 예제에서는 "b"로 시작와 "a"입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="93b2b-1104">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="93b2b-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="93b2b-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="93b2b-1106">Hello에서 시작 하는 문자열 식의 반환 일부 문자 0부터 시작 위치를 지정 하 고 길이 또는 hello 문자열의 끝 toohello toohello 지정을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="93b2b-1107">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="93b2b-1108">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1109">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="93b2b-1110">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-1111">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1112">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1113">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1113">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1114">hello 다음 예제에서는 반환 hello 부분 문자열 "abc"의 1 1 자 길이 대 한부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="93b2b-1115">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="93b2b-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="93b2b-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="93b2b-1117">소문자 데이터 toouppercase 변환한 후 문자열 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="93b2b-1118">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="93b2b-1119">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="93b2b-1120">유효한 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1121">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1122">문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="93b2b-1123">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1123">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1124">hello 방법을 예제와 다음 toouse 위 쿼리에서</span><span class="sxs-lookup"><span data-stu-id="93b2b-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="93b2b-1125">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="93b2b-1126"><a name="bk_array_functions"></a> 배열 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="93b2b-1127">다음 스칼라 함수 hello는 배열 입력된 값 및 반환 숫자, 부울 또는 배열 값에 대 한 작업 수행</span><span class="sxs-lookup"><span data-stu-id="93b2b-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="93b2b-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="93b2b-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="93b2b-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="93b2b-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="93b2b-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="93b2b-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="93b2b-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="93b2b-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="93b2b-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="93b2b-1133">hello가 두 개 이상의 배열 값을 연결한 결과인 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="93b2b-1134">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="93b2b-1135">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="93b2b-1136">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="93b2b-1137">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1138">배열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="93b2b-1139">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1139">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1140">다음 예에서는 두 개의 tooconcatenate 배열은 방법을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="93b2b-1141">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="93b2b-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="93b2b-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="93b2b-1143">값을 지정 하는 hello hello 배열에 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="93b2b-1144">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="93b2b-1145">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="93b2b-1146">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="93b2b-1147">유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="93b2b-1148">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1149">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="93b2b-1150">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1150">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1151">다음 예제에서는 어떻게 hello toocheck ARRAY_CONTAINS를 사용 하 여 배열의 멤버 자격에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="93b2b-1152">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="93b2b-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="93b2b-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="93b2b-1154">배열 식을 지정 하는 hello 요소의 hello 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="93b2b-1155">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="93b2b-1156">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="93b2b-1157">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="93b2b-1158">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1159">숫자 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-1160">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1160">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1161">다음 예제에서는 어떻게 tooget hello ARRAY_LENGTH를 사용 하 여 배열 길이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="93b2b-1162">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="93b2b-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="93b2b-1164">배열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="93b2b-1165">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="93b2b-1166">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="93b2b-1167">유효한 배열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="93b2b-1168">유효한 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="93b2b-1169">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1170">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="93b2b-1171">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1171">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1172">다음 예제에서는 어떻게 hello tooget ARRAY_SLICE를 사용 하 여 배열에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="93b2b-1173">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="93b2b-1174"><a name="bk_spatial_functions"></a> 공간 함수</span><span class="sxs-lookup"><span data-stu-id="93b2b-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="93b2b-1175">hello 다음 스칼라 함수는 공간 개체의 입력된 값에 대 한 작업을 수행 하 고 숫자 또는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="93b2b-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="93b2b-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="93b2b-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="93b2b-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="93b2b-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="93b2b-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="93b2b-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="93b2b-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="93b2b-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="93b2b-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="93b2b-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="93b2b-1182">두 hello GeoJSON 지점, 다각형 또는 LineString 식 사이의 hello 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="93b2b-1183">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="93b2b-1184">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1185">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="93b2b-1186">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1187">Hello 거리를 포함 하는 숫자 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="93b2b-1188">이 hello 기본 참조 시스템에 대 한 미터 단위로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="93b2b-1189">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1189">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1190">hello 방법을 예제와 다음 tooreturn의 hello 30 km 내에 있는 모든 패밀리 문서 hello ST_DISTANCE 기본 제공 함수를 사용 하 여 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="93b2b-1191">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="93b2b-1192">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="93b2b-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="93b2b-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="93b2b-1194">Hello 첫 번째 인수에 지정 된 hello GeoJSON 개체 (점, 다각형, 또는 LineString) hello GeoJSON (점, 다각형, 또는 LineString) 내에서 hello 두 번째 인수에는 표시 하는 부울 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="93b2b-1195">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="93b2b-1196">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1197">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1198">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="93b2b-1199">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1200">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="93b2b-1201">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1201">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1202">다음 예제는 hello 방법을 toofind 모든 제품군에 설명 ST_WITHIN를 사용 하 여 다각형 내의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="93b2b-1203">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="93b2b-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="93b2b-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="93b2b-1205">Hello 첫 번째 인수에 지정 된 hello GeoJSON 개체 (점, 다각형, 또는 LineString) hello GeoJSON (점, 다각형, 또는 LineString) hello 두 번째 인수에 교차 하는지 여부를 나타내는 부울 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="93b2b-1206">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="93b2b-1207">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1208">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1209">유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="93b2b-1210">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1211">부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="93b2b-1212">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1212">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1213">hello 방법을 예제와 다음 toofind 다각형 지정한 hello와 교차 하는 모든 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="93b2b-1214">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="93b2b-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="93b2b-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="93b2b-1216">Hello GeoJSON 지점, 다각형 또는 LineString 식이 유효한 경우이 지정 되었는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="93b2b-1217">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="93b2b-1218">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1219">유효한 GeoJSON Point, Polygon 또는 LineString 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="93b2b-1220">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1221">부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="93b2b-1222">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1222">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1223">hello 방법을 예제와 다음 toocheck 요소가 있는 경우 ST_VALID를 사용 하 여 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="93b2b-1224">예를 들어이 요소에 hello 유효한 [-90, 90] 값의 범위에 있지 않은 위도 값, 이므로 false를 반환 하는 쿼리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="93b2b-1225">다각형에 대 한 hello 사양에서는 hello 마지막 좌표 쌍 제공 수 있어야 GeoJSON hello 동일 hello 첫 번째 toocreate로 닫힌된 셰이프.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="93b2b-1226">다각형 내의 점을 시계 반대 방향 순서로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="93b2b-1227">시계 방향으로 순서에 지정 된 다각형 hello hello 영역 내에서 역을 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="93b2b-1228">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="93b2b-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="93b2b-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="93b2b-1230">Hello GeoJSON 지점, 다각형 또는 LineString 식이 지정 된 경우 부울 값을 포함 하는 JSON 값은 유효 하 고, 잘못 된 경우에 문자열 값으로 이유 hello 또한 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="93b2b-1231">**구문**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="93b2b-1232">**인수**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="93b2b-1233">유효한 GeoJSON 꼭짓점 또는 다각형 식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="93b2b-1234">**반환 형식**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="93b2b-1235">Hello 지정 GeoJSON 지점 또는 다각형 식은 유효 하며 유효 하지 않은 경우에 문자열 값으로 이유 hello 또한 경우 부울 값을 포함 하는 JSON 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="93b2b-1236">**예**</span><span class="sxs-lookup"><span data-stu-id="93b2b-1236">**Examples**</span></span>  
  
 <span data-ttu-id="93b2b-1237">다음 예제에서는 어떻게 hello ST_ISVALIDDETAILED를 사용 하 여 세부 정보와) (함께 toocheck 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="93b2b-1238">Hello 결과 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b2b-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="93b2b-1239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93b2b-1239">Next steps</span></span>  
 <span data-ttu-id="93b2b-1240">[Azure Cosmos DB에 대한 SQL 구문 및 SQL 쿼리](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="93b2b-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="93b2b-1241">Azure Cosmos DB 설명서</span><span class="sxs-lookup"><span data-stu-id="93b2b-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
