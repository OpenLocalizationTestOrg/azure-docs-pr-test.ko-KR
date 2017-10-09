---
제목: aaa "Azure Cosmos DB DocumentDB API: SQL 구문을 | Microsoft Docs "설명: hello Azure Cosmos DB DocumentDB API SQL 쿼리 언어에 대 한 설명서를 참조 합니다.
서비스: cosmos db 작성자: mimig1 관리자: jhubbard 편집기: mimig documentationcenter: '

ms.assetid: ms.service: cosmos db ms.workload: 데이터 서비스 ms.tgt_pltfrm: na ms.devlang: na ms.topic: 참조 ms.date: 06/13/2017 ms.author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>Azure Cosmos DB DocumentDB API: SQL 구문 참조

명시적 스키마 나 보조 인덱스를 만들 필요 없이 계층적 JSON 문서에 대해 문법와 같은 익숙한 SQL (Structured Query Language)을 사용 하 여 쿼리 문서를 지원 하는 hello Azure Cosmos DB DocumentDB API 합니다. 이 항목에서는 DocumentDB API SQL 쿼리 언어 hello에 대 한 참조 설명서를 제공 합니다.

Hello DocumentDB API SQL 쿼리 언어를 연습에 대 한 참조 [Azure Cosmos DB DocumentDB API에 대 한 SQL 쿼리](documentdb-sql-query.md)합니다.  
  
Toovisit hello 초대 또한 [Query Playground](http://www.documentdb.com/sql/demo) Azure Cosmos DB를 시도 하 고이 데이터 집합에 대해 SQL 쿼리를 실행할 수 있는 합니다.  
  
## <a name="select-query"></a>SELECT 쿼리  
Hello 데이터베이스에서 JSON 문서를 검색합니다. 식 평가, 프로젝션, 필터링 및 조인을 지원합니다.  hello SELECT 문을 설명 하는 데 사용 되는 hello 규칙 hello 구문 규칙 섹션에에서 표로 작성 됩니다.  
  
**구문**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **설명**  
  
 각 절에 대한 자세한 내용은 다음 섹션을 참조하세요.  
  
-   [SELECT 절](#bk_select_query)  
  
-   [FROM 절](#bk_from_clause)  
  
-   [WHERE 절](#bk_where_clause)  
  
-   [ORDER BY 절](#bk_orderby_clause)  
  
위와 같이 hello SELECT 문에서 hello 절 순서를 지정 해야 합니다. Hello 선택 사항인 절 중 하나를 생략할 수 있습니다. 하지만 선택 사항인 절을 사용할 때는 hello 올바른 순서로 표시 되어야 합니다.  
  
**Hello SELECT 문의 논리적 처리 순서**  
  
hello order 절이 처리 됩니다.  

1.  [FROM 절](#bk_from_clause)  
2.  [WHERE 절](#bk_where_clause)  
3.  [ORDER BY 절](#bk_orderby_clause)  
4.  [SELECT 절](#bk_select_query)  

Note이 hello 구문에 나타나는 hello 순서와에서 다릅니다. 처리 된 절에 의해 도입 된 새로운 모든 기호가 표시 되 고 나중에 처리 하는 절에 사용할 수 있도록 hello 순서가 지정 됩니다. 예를 들어 FROM 절에 선언된 별칭은 WHERE 절과 SELECT 절에서 액세스할 수 있습니다.  

**공백 문자 및 주석**  

따옴표 붙은 식별자 또는 따옴표 붙은 문자열의 일부가 아닌 모든 공백 문자는 hello 언어 문법의 일부가 아닌 및 구문 분석에서 무시 됩니다.  

hello 쿼리 언어 같은 T-SQL 스타일 주석을 지원합니다  

-   `-- comment text [newline]` SQL 문  

공백 문자와 주석은 없는 반면 중요 hello 문법에를 사용 하는 tooseparate 토큰 이어야 합니다. 예를 들어 `-1e5`는 단일 숫자 토큰이지만, `: – 1 e5`는 숫자 1과 식별자 e5가 뒤에 나오는 마이너스 토큰입니다.  

##  <a name="bk_select_query"></a> SELECT 절  
위와 같이 hello SELECT 문에서 hello 절 순서를 지정 해야 합니다. Hello 선택 사항인 절 중 하나를 생략할 수 있습니다. 하지만 선택 사항인 절을 사용할 때는 hello 올바른 순서로 표시 되어야 합니다.  

**구문**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **인수**  
  
 `<select_specification>`  
  
 속성 또는 값 toobe hello 결과 대 한 선택 설정 합니다.  
  
 `'*'`  
  
Hello 값을 변경 하지 않고 검색을 지정 합니다. 처리 하는 hello 값은 개체, 경우에 특히 모든 속성이 검색 됩니다.  
  
 `<object_property_list>`  
  
검색 속성 toobe hello 목록을 지정 합니다. 각 반환 된 값을 지정 하는 hello 속성을 가진 개체 됩니다.  
  
`VALUE`  
  
Hello 전체 JSON 개체 대신 hello JSON 값을 검색 하도록 지정 합니다. 이 달리 `<property_list>` 개체에 hello 프로젝션 값을 래핑하지 않습니다.  
  
`<scalar_expression>`  
  
Hello 값 toobe를 나타내는 식을 계산 합니다. 자세한 내용은 [스칼라 식](#bk_scalar_expressions) 섹션을 참조하세요.  
  
**설명**  
  
hello `SELECT *` 구문이 올바른지만 FROM 절 정확히 하나의 별칭 선언 합니다. `SELECT *`는 ID 프로젝션을 제공하며, 이는 프로젝션이 필요하지 않은 경우 유용할 수 있습니다. SELECT *는 FROM 절이 지정되고 단일 입력 원본만 도입된 경우에만 유효합니다.  
  
`SELECT <select_list>`과 `SELECT *`는 "syntactic sugar(구문적 설탕)"이며 다음과 같이 간단한 SELECT 문을 사용하여 표현할 수 있습니다.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     이는 다음과 동등합니다.  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     이는 다음과 동등합니다.  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**참고 항목**  
  
[스칼라 식](#bk_scalar_expressions)  
[SELECT 절](#bk_select_query)  
  
##  <a name="bk_from_clause"></a> FROM 절  
Hello 원본 또는 조인 된 원본을 지정합니다. hello FROM 절은 선택 사항입니다. 지정하지 않으면 FROM 절에서 단일 문서를 제공하는 것처럼 다른 절도 계속 실행됩니다.  
  
**구문**  
  
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
  
**인수**  
  
`<from_source>`  
  
별칭이 있거나 없는 데이터 원본을 지정합니다. 별칭이 지정 되지 않은 경우 hello에서 유추할 수는 `<collection_expression>` 다음 규칙을 사용 하 여:  
  
-   Hello 식이 collection_name이 별명 이면 collection_name이 별명 별칭으로 사용 됩니다.  
  
-   Hello 식이 `<collection_expression>`, property_name을 별칭으로 사용 됩니다. Hello 식이 collection_name이 별명 이면 collection_name이 별명 별칭으로 사용 됩니다.  
  
AS `input_alias`  
  
해당 hello 지정 `input_alias` 집합 hello 기본 컬렉션 식에서 반환 된 값입니다.  
 
`input_alias` IN  
  
해당 hello 지정 `input_alias` hello hello 기본 컬렉션 식에서 반환 된 각 배열의 모든 배열 요소를 반복 하 여 얻은 값 집합을 나타내야 합니다. 배열이 아닌 기본 컬렉션 식에서 반환되는 값은 무시됩니다.  
  
`<collection_expression>`  
  
Hello 컬렉션 식 toobe 사용한 tooretrieve hello 문서를 지정 합니다.  
  
`ROOT`  
  
Hello 기본적으로 현재 연결 된 컬렉션에서 해당 문서를 검색 하도록 지정 합니다.  
  
`collection_name`  
  
문서를 제공 하는 hello 컬렉션에서 검색을 지정 합니다. hello 컬렉션의 hello 이름 hello 컬렉션에 현재 연결의 hello 이름을 일치 해야 합니다.  
  
`input_alias`  
  
Hello에서 해당 문서를 검색 하도록 지정 합니다. 제공 된 hello 별칭으로 정의 된 다른 원본입니다.  
  
`<collection_expression> '.' property_`  
  
Hello에 액세스 하 여 해당 문서를 검색 하도록 지정 `property_name` 속성 또는 array_index 배열 요소에서 검색 하는 모든 문서에 대 한 컬렉션 식을 지정 합니다.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Hello에 액세스 하 여 해당 문서를 검색 하도록 지정 `property_name` 속성 또는 array_index 배열 요소에서 검색 하는 모든 문서에 대 한 컬렉션 식을 지정 합니다.  
  
**설명**  
  
모든 별칭에에서 제공 되었거나 유추 hello `<from_source>(`s) 고유 해야 합니다. hello 구문 `<collection_expression>.`property_name 동일 hello은 `<collection_expression>' ['"property_name"']'`합니다. 그러나 속성 이름에는 식별자가 아닌 문자가 포함 되어 있으면 hello 두 번째 구문을 사용할 수 있습니다.  
  
**누락된 속성, 누락된 배열 요소, 정의되지 않은 값 처리**  
  
컬렉션 식에서 속성이나 배열 요소에 액세스하고 해당 값이 존재하지 않으면 이 값은 무시되고 더 이상 처리되지 않습니다.  
  
**컬렉션 식 컨텍스트 범위 지정**  
  
컬렉션 식은 컬렉션 범위 또는 문서 범위일 수 있습니다.  
  
-   식은 컬렉션 범위입니다는 hello 컬렉션 식의 기본 원본이 ROOT 경우 hello 또는 `collection_name`합니다. 이러한 식은 직접 hello 컬렉션에서 검색 된 문서 집합을 나타내며 다른 컬렉션 식의 hello 처리에 종속 되지 않습니다.  
  
-   식은 문서 범위입니다, hello hello 컬렉션 식의 원본 인지 `input_alias` hello 쿼리 앞부분에 나오는 합니다. 이러한 식은 hello 별칭이 지정 된 컬렉션에 연결 된 toohello 집합에 속한 각 문서의 hello 범위에서 hello 컬렉션 식을 평가 하 여 얻은 문서 집합을을 나타냅니다.  hello 결과 집합에는 각각 hello 문서 집합 기본 hello에 대 한 hello 컬렉션 식을 평가 하 여 얻은 집합의 합집합 됩니다.  
  
**조인**  
  
Hello 현재 릴리스에서 Azure Cosmos DB에는 내부 조인을 지원 합니다. 추가 조인 기능이 곧 출시됩니다.

Hello의 완전 한 교차곱에서 내부 조인 결과 hello 조인에 참여 하 고 설정 합니다. N-방향 조인을 hello 결과 hello 튜플의 각 값 hello 조인에 참여 하 고 설정 하는 hello 별칭에 연결 된 하 고 다른 절에서 해당 별칭을 참조 하 여 액세스할 수 있는 N-요소 튜플의 집합.  
  
hello 조인의 hello 평가 hello 참여 하 고 집합의 hello 컨텍스트 범위에 따라 달라 집니다.  
  
-  컬렉션 집합 A와 컬렉션 범위 집합 B을 조인하면 집합 A와 집합 B에 있는 모든 요소의 교차곱을 만듭니다.
  
-   집합 A와 문서 범위 집합 B를 조인하면 집합 A의 각 문서에 대해 문서 범위 집합 B를 평가하여 얻는 모든 집합의 합집합을 만듭니다.  
  
 Hello 현재 릴리스에서 하나의 컬렉션 범위 식의 최대는 hello 쿼리 프로세서에서 지원 됩니다.  
  
**조인 예제:**  
  
FROM 절 뒤 hello를 살펴보겠습니다.`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 각 원본에서 `input_alias1, input_alias2, …, input_aliasN`을 정의하도록 합니다. 이 FROM 절은 N 튜플(N개 값이 포함된 튜플)의 집합을 반환합니다. 각 튜플은 해당 집합에 모든 컬렉션 별칭을 반복하여 생성된 값을 포함합니다.  
  
*2개 원본이 있는 조인 예제 1:*  
  
- 컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.  
  
- input_alias1을 참조하는 문서 범위로 `<from_source2>`를 지정하고 다음 집합을 나타냅니다.  
  
    `input_alias1 = A,`의 경우 {1, 2}  
  
    `input_alias1 = B,`의 경우 {3}  
  
    `input_alias1 = C,`의 경우 {4, 5}  
  
- FROM 절 hello `<from_source1> JOIN <from_source2>` hello 튜플 뒤에 발생 합니다.  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*3개 원본이 있는 조인 예제 2:*  
  
- 컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.  
  
- `input_alias1`을 참조하는 문서 범위로 `<from_source2>`를 지정하고 다음 집합을 나타냅니다.  
  
    `input_alias1 = A,`의 경우 {1, 2}  
  
    `input_alias1 = B,`의 경우 {3}  
  
    `input_alias1 = C,`의 경우 {4, 5}  
  
- `input_alias2`를 참조하는 문서 범위로 `<from_source3>`을 지정하고 다음 집합을 나타냅니다.  
  
    `input_alias2 = 1,`의 경우 {100, 200}  
  
    `input_alias2 = 3,`의 경우 {300}  
  
- FROM 절 hello `<from_source1> JOIN <from_source2> JOIN <from_source3>` hello 튜플 뒤에 발생 합니다.  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> 다른 값에는 튜플이 `input_alias1`, `input_alias2`, 어떤 hello에 대 한 `<from_source3>` 값을 반환 하지 않았습니다.  
  
*3개 원본이 있는 조인 예제 3:*  
  
- 컬렉션 범위로 <from_source1>을 지정하고 집합 {A, B, C}를 나타냅니다.  
  
- 컬렉션 범위로 `<from_source1>`을 지정하고 집합 {A, B, C}를 나타냅니다.  
  
- input_alias1을 참조하는 문서 범위로 <from_source2>를 지정하고 다음 집합을 나타냅니다.  
  
    `input_alias1 = A,`의 경우 {1, 2}  
  
    `input_alias1 = B,`의 경우 {3}  
  
    `input_alias1 = C,`의 경우 {4, 5}  
  
- Let `<from_source3>` 너무 범위를 지정할`input_alias1` 고 다음 집합:  
  
    `input_alias2 = A,`의 경우 {100, 200}  
  
    `input_alias2 = C,`의 경우 {300}  
  
- FROM 절 hello `<from_source1> JOIN <from_source2> JOIN <from_source3>` hello 튜플 뒤에 발생 합니다.  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)  
  
> [!NOTE]
> 사이의 교차곱 되었습니다 `<from_source2>` 및 `<from_source3>` 둘 다 범위 지정 된 toohello 때문에 동일한 `<from_source1>`합니다.  이로 인해 A 값이 있는 4개(2x2) 튜플, B 값이 있는 0개(1x0) 튜플 및 C 값이 있는 2개(2x1) 튜플을 만들었습니다.  
  
**참고 항목**  
  
 [SELECT 절](#bk_select_query)  
  
##  <a name="bk_where_clause"></a> WHERE 절  
 Hello 쿼리에서 반환 된 hello 문서에 대 한 hello 검색 조건을 지정 합니다.  
  
 **구문**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **인수**  
  
-   `<filter_condition>`  
  
     Hello 조건 toobe hello 문서 toobe 반환에 대해 충족를 지정 합니다.  
  
-   `<scalar_expression>`  
  
     Hello 값 toobe를 나타내는 식을 계산 합니다. Hello 참조 [스칼라 식](#bk_scalar_expressions) 자세한 내용은 섹션.  
  
 **설명**  
  
 Hello에 대 한 순서 대로 문서 toobe 필터 조건은 tootrue 유지 되어야 하며 지정 된 식을 반환 합니다. 부울 값 true hello 조건, 다른 모든 값을 만족 하는 전용: 번호, 배열 또는 개체가 정의 되지 않은, null, false 이면 hello 조건을 만족 하지 것입니다.  
  
##  <a name="bk_orderby_clause"></a> ORDER BY 절  
 Hello 정렬 순서 hello 쿼리에 의해 반환 된 결과를 지정 합니다.  
  
 **구문**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **인수**  
  
-   `<sort_specification>`  
  
     속성 또는 toosort hello 쿼리 결과 설정 된 식을 지정 합니다. 정렬 열은 이름 또는 열 별칭으로 지정할 수 있습니다.  
  
     여러 정렬 열을 지정할 수 있습니다. 열 이름은 고유해야 합니다. hello hello ORDER BY 절에 열 정렬의 hello 시퀀스 hello 조직 hello 정렬 된 결과 집합의 정의합니다. 즉, hello 첫 번째 속성으로 hello 결과 집합이 정렬 된 하 고이 정렬 된 목록이 hello 두 번째 속성으로 정렬 됩니다.  
  
     hello ORDER BY 절에서 참조 하는 hello 열 이름은 정확 하 게 hello FROM 절에 지정 된 테이블에 정의 된 목록 또는 tooa 열을 선택 하는 열 hello에 tooeither를 일치 해야 합니다.  
  
-   `<sort_expression>`  
  
     toosort hello 쿼리 결과 집합에 단일 속성 또는 식을 지정합니다.  
  
-   `<scalar_expression>`  
  
     Hello 참조 [스칼라 식](#bk_scalar_expressions) 자세한 내용은 섹션.  
  
-   `ASC | DESC`  
  
     Hello 지정 열의 hello 값을 오름차순 또는 내림차순 정렬 해야 함을 지정 합니다. ASC는 hello 가장 작은 값 toohighest 값에서 정렬합니다. 가장 큰 값 toolowest 값에서 DESC 정렬합니다. ASC는 hello 기본 정렬 순서입니다. Null 값은 hello 가능한 가장 작은 값으로 처리 됩니다.  
  
 **설명**  
  
 Hello 쿼리 문법을 지원 하지만 여러 순서 속성으로 계산 된 속성 대해서가 아니라 단일 속성에 대해서만 및 속성 이름에 대해서만 즉, 정렬 hello Azure Cosmos DB 쿼리 런타임의 지원 합니다. 인덱싱 정책을 해당 hello hello 속성 및 지정 된 hello에 대 한 범위 인덱스를 포함 해야 정렬 hello 최대 정밀도로 유형입니다. Toohello 인덱싱 정책 설명서에 대 한 자세한 내용은 참조 하십시오.  
  
##  <a name="bk_scalar_expressions"></a> 스칼라 식  
 스칼라 식이 기호의 조합와 될 수 있는 연산자는 tooobtain 단일 값으로 계산 합니다. 간단한 식은 상수, 속성 참조, 배열 요소 참조, 별칭 참조 또는 함수 호출일 수 있으며, 연산자를 사용하여 복잡한 식으로 결합될 수 있습니다.  
  
 스칼라 식에 포함될 수 있는 값에 대한 자세한 내용은 [상수](#bk_constants) 섹션을 참조하세요.  
  
 **구문**  
  
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
  
 **인수**  
  
-   `<constant>`  
  
     상수 값을 나타냅니다. 자세한 내용은 [상수](#bk_constants) 섹션을 참조하세요.  
  
-   `input_alias`  
  
     Hello에 정의 된 값을 나타내는 `input_alias` hello에 도입 된 `FROM` 절.  
    이 값은 절대로 toonot 수 **정의 되지 않은** –**정의 되지 않은** hello 입력의 값에 건너뜁니다.  
  
-   `<scalar_expression>.property_name`  
  
     개체의 hello 속성의 값을 나타냅니다. Hello 속성이 없습니다 또는, 개체가 값에서 속성을 참조할 경우 hello 식이 너무**정의 되지 않은** 값입니다.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     이름의 hello 속성의 값을 나타내는 `property_name` 또는 인덱스가 포함 된 배열 요소 `array_index` 개체/배열입니다. Hello 속성/배열 인덱스가 없거나 hello 속성/배열 인덱스가 개체/배열이 값에서 참조 될 경우 hello 식 tooundefined 값을 계산 합니다.  
  
-   `unary_operator <scalar_expression>`  
  
     단일 값을 적용 된 tooa 연산자를 나타냅니다. 자세한 내용은 [연산자](#bk_operators) 섹션을 참조하세요.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     연산자를 적용 된 tootwo 값을 나타냅니다. 자세한 내용은 [연산자](#bk_operators) 섹션을 참조하세요.  
  
-   `<scalar_function_expression>`  
  
     함수 호출의 결과로 정의되는 값을 나타냅니다.  
  
-   `udf_scalar_function`  
  
     스칼라 함수를 정의 하는 hello 사용자의 이름.  
  
-   `builtin_scalar_function`  
  
     Hello 기본 제공 스칼라 함수의 이름입니다.  
  
-   `<create_object_expression>`  
  
     지정된 속성 및 해당 값이 포함된 새 개체를 만들어서 얻는 값을 나타냅니다.  
  
-   `<create_array_expression>`  
  
     요소로 지정된 값이 포함된 새 배열을 만들어서 얻는 값을 나타냅니다.  
  
-   `parameter_name`  
  
     Hello 지정 된 매개 변수 이름의 값을 나타냅니다. 매개 변수 이름은 hello 첫 번째 문자로 @을 하나가 있어야 합니다.  
  
 **설명**  
  
 기본 제공 또는 사용자 정의 스칼라 함수를 호출할 때 모든 인수가 정의되어야 합니다. Hello 인수가 정의 되지 않은 경우 hello 함수를 호출 하지는 및 hello 결과 정의 되지 않습니다.  
  
 개체를 만들 때 정의 되지 않은 값이 할당 된 모든 속성은 건너뛰고 hello 만든 개체에에서 포함 되지 않습니다.  
  
 모든 요소 값 배열을 만들 할당 된 경우 **정의 되지 않은** 값 건너뛰고 hello 만든 개체에 포함 되지 않습니다. 이렇게 하면 다음 정의 hello 요소 tootake 대신 방식으로 해당 만든 hello 배열 됩니다에 건너뛴 인덱스가 있습니다.  
  
##  <a name="bk_operators"></a> 연산자  
 이 섹션에는 지원 hello 연산자에 설명 합니다. 각 연산자는 하나의 범주 할당된 tooexactly 될 수 있습니다.  
  
 **undefined** 값 처리 입력 값 형식 요구 사항 및 일치하지 않는 형식의 값 처리에 대한 자세한 내용은 아래의 **연산자 범주** 표를 참조하세요.  
  
 **연산자 범주**  
  
|**범주**|**세부 정보**|  
|-|-|  
|**산술**|연산자는 입력은 toobe 번호입니다. 출력도 숫자입니다. Hello 입력 중 하나라도 **정의 되지 않은** 번호 다음 hello 결과 외의 다른 형식이 아니거나 **정의 되지 않은**합니다.|  
|**비트**|연산자는 입력은 toobe 32 비트 부호 있는 정수 숫자입니다. 출력도 부호 있는 32비트 정수입니다.<br /><br /> 정수가 아닌 값은 끝수를 자릅니다. 양수 값은 끝수 내림되고, 음수 값은 끝수 올림됩니다.<br /><br /> 2의 보수 표기법의 마지막 32 비트를 수행 하 여 hello 32 비트 정수 범위 밖에 있는 모든 값 변환 됩니다.<br /><br /> Hello 입력 중 하나라도 **정의 되지 않은** 이거나 숫자 이외의 형식인 경우 hello 결과 **정의 되지 않은**합니다.<br /><br /> **참고:** 동작 위에 hello JavaScript 비트 연산자 동작과 호환 됩니다.|  
|**논리**|연산자는 입력은 toobe은 부울입니다. 출력도 부울입니다.<br />Hello 입력 중 하나라도 **정의 되지 않은** 이거나 부울 이외의 형식인 hello 결과가 경우 **정의 되지 않은**합니다.|  
|**비교**|연산자는 입력은 toohave hello 동일 입력 하 고 정의 되지 않은 수 없습니다. 출력은 부울입니다.<br /><br /> Hello 입력 중 하나라도 **정의 되지 않은** 하거나 다른 형식을 사용 했으므로 hello 입력 한 다음 hello 결과 **정의 되지 않은**합니다.<br /><br /> 값 순서 지정에 대한 자세한 내용은 **비교 연산자의 값 순서 지정** 표를 참조하세요.|  
|**string**|연산자는 입력은 toobe 문자열입니다. 출력도 문자열입니다.<br />Hello 입력 중 하나라도 **정의 되지 않은** hello 다음 문자열 결과 외의 다른 형식이 아니거나 **정의 되지 않은**합니다.|  
  
 **단항 연산자:**  
  
|**Name**|**연산자**|**세부 정보**|  
|-|-|-|  
|**산술**|+<br /><br /> -|Hello 숫자 값을 반환 합니다.<br /><br /> 비트 부정입니다. 음수 값을 반환합니다.|  
|**비트**|~|보수입니다. 숫자 값의 보수를 반환합니다.|  
|**논리**|**다음이 아님**|부정입니다. 부정 부울 값을 반환합니다.|  
  
 **이항 연산자:**  
  
|**Name**|**연산자**|**세부 정보**|  
|-|-|-|  
|**산술**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|더하기<br /><br /> 빼기<br /><br /> 곱하기<br /><br /> 나누기<br /><br /> Modulo 연산|  
|**비트**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|비트 OR<br /><br /> 비트 AND<br /><br /> 비트 XOR<br /><br /> 왼쪽 시프트<br /><br /> 오른쪽 시프트<br /><br /> 0 채우기 오른쪽 시프트|  
|**논리**|**및**<br /><br /> **또는**|논리 결합입니다. 두 인수가 **true**이면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.<br /><br /> 논리 결합입니다. 두 인수가 **true**이면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.|  
|**비교**|**=**<br /><br /> **!=, <>**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|같음 - 두 인수가 같으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.<br /><br /> 같지 않음 - 인수가 같지 않으면 **true**를 반환하고, 그렇지 않으면 **false**를 반환합니다.<br /><br /> 큼 - 반환 **true** 첫 번째 인수가 두 번째 식 hello 보다 큰 경우 반환 **false** 그렇지 않은 경우.<br /><br /> 크거나 같음 - 반환 **true** 첫 번째 인수 보다 크면 또는 toohello 두 번째 식과 일치 하는 경우 반환 **false** 그렇지 않은 경우.<br /><br /> 작음 - 반환 **true** 첫 번째 인수 hello 두 번째 식 보다 작은 경우 반환 **false** 그렇지 않은 경우.<br /><br /> 작거나 같음 - 반환 **true** 첫 번째 인수 보다 작거나 같은 경우 toohello의 두 번째 하나 반환 **false** 그렇지 않은 경우.<br /><br /> 병합 - Hello 첫 번째 인수가 반환 hello 두 번째 인수는 **정의 되지 않은** 값입니다.|  
|**String**|**&#124;&#124;**|연결 - 두 인수의 연결을 반환합니다.|  
  
 **삼항 연산자:**  
  
|삼항 연산자|?|반환 너무 hello 첫 번째 인수를 평가 하는 경우 두 번째 인수를 hello**true**; 그렇지 않으면 hello 세 번째 인수를 반환 합니다.|  
|-|-|-|  
  
 **비교 연산자의 값 순서 지정**  
  
|**형식**|**값 순서**|  
|-|-|  
|**Undefined**|비교할 수 없음|  
|**Null**|단일 값: **null**|  
|**Number**|자연수입니다.<br /><br /> Negative Infinity(음의 무한대) 값은 다른 Number 값보다 작습니다.<br /><br /> Positive Infinity(양의 무한대) 값은 다른 Number 값보다 큽니다. **NaN** 값은 비교할 수 없습니다. **NaN**과 비교하면 **undefined** 값이 됩니다.|  
|**String**|사전순 정렬|  
|**Array**|순서를 지정하지 않지만 동등하게 지정합니다.|  
|**Object**|순서를 지정하지 않지만 동등하게 지정합니다.|  
  
 **설명**  
  
 Azure Cosmos DB hello 유형의 값 종종 알 수 없는 실제로 hello 데이터베이스에서 검색 될 때까지 합니다. 순서 toosupport 효율적인 쿼리 실행, 대부분의 hello 연산자에는 엄격한 형식 요구 사항이 있습니다. 또한 연산자 자체는 암시적 변환을 수행하지 않습니다.  
  
 즉, 쿼리 등의: 선택 * FROM ROOT r WHERE r.Age = 21 보존 기간 같은 toohello 숫자 21 속성을 사용 하 여 문서를 반환 합니다. 속성 사용 기간 같은 toohello 문자열 "21" 또는 hello 문자열 "0021" 문서와 일치 하지 것입니다 "21" hello 식으로 = 21 tooundefined 평가 합니다. 이 통해 효율적으로 인덱스를 사용 하기 때문에 특정 값의 hello 조회 (예: 숫자 21) 불특정 개수의 잠재적인 일치 항목 (예: 숫자 21 또는 문자열 "21", "021", "21.0" …)에 대 한 검색 보다 빠릅니다. 이는 JavaScript에서 다른 형식의 값에 대해 연산자를 평가하는 방식과 다릅니다.  
  
 **배열 및 개체 같음 및 비교**  
  
 범위 연산자(>, >=, <, <=)를 사용하여 배열 또는 개체 값을 비교하면 배열 또는 개체 값에 정의된 순서가 없으므로 결과가 정의되지 않습니다. 그러나 같음/같지 않음 연산자(=, !=, <>)를 사용할 수 있으며, 이 경우 값이 구조적으로 비교됩니다.  
  
 두 배열의 요소 수가 같고 일치하는 위치의 요소도 같은 경우 배열은 같습니다. 배열 비교 hello 결과가 정의 되지 않음된, 임의 요소 쌍의 비교 결과가 같은 경우 정의 되지 않습니다.  
  
 두 개체에 동일한 속성이 정의되어 있고 일치하는 속성의 값도 같은 경우 개체는 같습니다. 개체 비교 hello 결과가 정의 되지 않은 속성 값 쌍의 비교 결과가 같은 경우 정의 되지 않습니다.  
  
##  <a name="bk_constants"></a> 상수  
 리터럴 또는 스칼라 값이라고도 하는 상수는 특정 데이터 값을 나타내는 기호입니다. 상수의 형식은 hello 나타내는 hello 값의 hello 데이터 형식에 따라 달라 집니다.  
  
 **지원되는 스칼라 데이터 형식:**  
  
|**형식**|**값 순서**|  
|-|-|  
|**Undefined**|단일 값: **undefined**|  
|**Null**|단일 값: **null**|  
|**Boolean**|값: **false**, **true**.|  
|**Number**|IEEE 754 표준의 두 자리 부동 소수점 숫자입니다.|  
|**String**|0개 이상의 유니코드 문자 시퀀스입니다. 문자열은 작은따옴표 또는 큰 따옴표로 묶어야 합니다.|  
|**Array**|0개 이상의 요소 시퀀스입니다. 각 요소는 Undefined를 제외한 모든 스칼라 데이터 형식의 값일 수 있습니다.|  
|**Object**|순서가 지정되지 않은 0개 이상의 이름/값 쌍의 집합입니다. 이름은 유니코드 문자열이며, 값은 **Undefined**를 제외한 모든 스칼라 데이터 형식이 될 수 있습니다.|  
  
 **구문**  
  
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
  
 **인수**  
  
1.  `<undefined_constant>; undefined`  
  
     Undefined 형식의 undefined 값을 나타냅니다.  
  
2.  `<null_constant>; null`  
  
     **Null** 형식의 **null** 값을 나타냅니다.  
  
3.  `<boolean_constant>`  
  
     Boolean 형식의 상수를 나타냅니다.  
  
4.  `false`  
  
     Boolean 형식의 **false** 값을 나타냅니다.  
  
5.  `true`  
  
     Boolean 형식의 **true** 값을 나타냅니다.  
  
6.  `<number_constant>`  
  
     상수를 나타냅니다.  
  
7.  `decimal_literal`  
  
     10진 리터럴은 10진수 표기법 또는 과학적 표기법을 사용하여 표현되는 숫자입니다.  
  
8.  `hexadecimal_literal`  
  
     16진 리터럴은 '0x' 접두사 다음에 하나 이상의 16진수가 나오는 숫자입니다.  
  
9. `<string_constant>`  
  
     String 형식의 상수를 나타냅니다.  
  
10. `string _literal`  
  
     문자열 리터럴은 연속적인 0이상의 유니코드 문자 또는 이스케이프 시퀀스로 표현되는 유니코드 문자열입니다. 문자열 리터럴은 작은따옴표(아포스트로피: ') 또는 큰따옴표(따옴표: ")로 묶어야 합니다.  
  
 허용되는 이스케이프 시퀀스는 다음과 같습니다.  
  
|**이스케이프 시퀀스**|**설명**|**유니코드 문자**|  
|-|-|-|  
|\\'|아포스트로피(')|U+0027|  
|\\"|따옴표(")|U+0022|  
|\\\|백슬래시(\\)|U+005C|  
|\\/|슬래시(/)|U+002F|  
|\b|백스페이스|U+0008|  
|\f|폼 피드|U+000C|  
|\n|줄 바꿈|U+000A|  
|\r|캐리지 리턴|U+000D|  
|\t|탭|U+0009|  
|\uXXXX|4자리 16진수로 정의된 유니코드 문자|U+XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a> 쿼리 성능 지침  
 대형 컬렉션에 대해 효율적으로 실행 하는 쿼리 toobe에서 하나 이상의 인덱스를 통해 제공 될 수 있는 필터를 사용 해야 합니다.  
  
 다음 필터는 hello 인덱스 검색에 것으로 간주 됩니다.  
  
-   문서 경로 식 및 상수와 함께 같음 연산자(=)를 사용합니다.  
  
-   문서 경로 식 및 상수와 함께 범위 연산자(<, \<=, >, >=)를 사용합니다.  
  
-   문서 경로 식에는 참조 하는 hello 데이터베이스 컬렉션에서 hello 문서의 상수 경로 식별 하는 모든 식을 나타냅니다.  
  
 **문서 경로 식**  
  
 문서 경로 식은 데이터베이스 수집 문서에서 제공하는 문서를 통해 속성 또는 배열 인덱서의 경로를 평가하는 식입니다. Hello 데이터베이스 컬렉션에서 hello 문서 내에서 직접 필터에서 참조 하는 값의 사용된 tooidentify hello 위치 경로일 수 있습니다.  
  
 문서 경로 식으로 간주 하는 식 toobe에 대 한 다음과 같은 것을 수행 해야 합니다.  
  
1.  참조 hello 컬렉션 루트 직접입니다.  
  
2.  일부 문서 경로 식의 속성 또는 상수 배열 인덱서를 참조합니다.  
  
3.  일부 문서 경로 식을 나타내는 별칭을 참조합니다.  
  
     **구문 규칙**  
  
     다음 표에서 hello hello DocumentDB API 쿼리 언어 참조에 hello 사용 되는 규칙 toodescribe 구문에 설명 합니다.  
  
    |**규칙**|**용도**|  
    |-|-|    
    |대문자|대/소문자를 구분하지 않는 키워드|  
    |소문자|대/소문자를 구분하는 키워드|  
    |\<nonterminal>|비단말(nonterminal)이며, 개별적으로 정의됩니다.|  
    |\<nonterminal> ::=|Hello 비터미널의 구문 정의입니다.|  
    |other_terminal|단말(토큰)이며, 단어로 자세히 설명됩니다.|  
    |identifier|식별자입니다. 허용되는 문자: a-z, A-Z, 0-9. 첫 번째 문자는 숫자가 아니어야 합니다.|  
    |"문자열"|따옴표가 붙은 문자열이며, 유효한 문자열이 모두 허용됩니다. string_literal에 대한 설명을 참조합니다.|  
    |'기호'|Hello 구문의 일부인 리터럴 기호입니다.|  
    |&#124; (세로줄)|구문 항목에 대한 대안이며, 지정 된 hello 항목 중 하나만 사용할 수 있습니다.|  
    |[ ] /(대괄호)|대괄호는 하나 이상의 선택 항목을 묶습니다.|  
    |[ ,...n ]|Hello 항목 앞에 n 번 반복된 될 수 나타냅니다. hello 항목은 쉼표로 구분 됩니다.|  
    |[ ...n ]|Hello 항목 앞에 n 번 반복된 될 수 나타냅니다. hello 항목은 공백으로 구분 됩니다.|  
  
##  <a name="bk_built_in_functions"></a> 기본 제공 함수  
 Azure Cosmos DB는 많은 기본 제공 SQL 함수를 제공합니다. 기본 제공 함수의 hello 범주는 다음과 같습니다.  
  
|함수|설명|  
|--------------|-----------------|  
|[수치 연산 함수](#bk_mathematical_functions)|일반적으로 인수로 제공 되 고 숫자 값을 반환 하는 입력된 값에 따라 계산을 수행 하는 hello 각 수치 연산 함수입니다.|  
|[형식 검사 함수](#bk_type_checking_functions)|hello 형식 검사 함수는 toocheck hello 유형의 SQL 쿼리 내에서 식 허용 합니다.|  
|[문자열 함수](#bk_string_functions)|hello 문자열 함수는 문자열 입력된 값에 대 한 작업을 수행 하 고 문자열, 숫자 또는 부울 값을 반환 합니다.|  
|[배열 함수](#bk_array_functions)|hello 배열 함수는 배열 입력된 값 및 숫자 반환에 대 한 작업이, 부울 또는 배열 값을 수행합니다.|  
|[공간 함수](#bk_spatial_functions)|hello 공간 함수는 값을 입력된 공간 개체에 대 한 작업을 수행 하 고 숫자 또는 부울 값을 반환 합니다.|  
  
###  <a name="bk_mathematical_functions"></a> 수치 연산 함수  
 hello 다음 함수는 계산을 수행할 일반적으로 인수로 제공 되 고 숫자 값을 반환 하는 입력된 값에 따라 합니다.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[CEILING](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[각도](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[로그](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[전원](#bk_power)|  
|[라디안](#bk_radians)|[반올림](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[정사각형](#bk_square)|[로그인](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a> ABS  
 Hello 절대 (양수)의 값을 반환 hello 지정 된 숫자 식입니다.  
  
 **구문**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 세 개의 다른 숫자에서 hello ABS 함수를 사용 하는 hello 결과  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> ACOS  
 반환 hello 각도 라디안 코사인이 hello 지정 된 숫자 식입니다. 아크코사인이 라고도합니다.  
  
 **구문**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 hello-1의 ACOS 합니다.  
  
```  
SELECT ACOS(-1)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> ASIN  
 사인이 hello 라디안 단위로 반환 hello 각도 숫자 식 지정. 아크사인이라고도 합니다.  
  
 **구문**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 hello-1의 ASIN 합니다.  
  
```  
SELECT ASIN(-1)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> ATAN  
 반환 hello 각도 라디안의 탄젠트는 hello 지정 된 숫자 식입니다. 아크탄젠트라고도 합니다.  
  
 **구문**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예제에서는 반환 hello hello의 ATAN hello 값을 지정 합니다.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> ATN2  
 라디안에서으로 표현 hello 아크 탄젠트 y / x의 hello 주요 값을 반환 합니다.  
  
 **구문**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 계산 지정 hello에 대 한 hello ATN2 x 및 y 구성 요소입니다.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> CEILING  
 Hello, 보다 큰 가장 작은 정수 값 또는 같음, hello 특정된 숫자 식을 반환 합니다.  
  
 **구문**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 사용 하 여 0 값에 CEILING 함수 hello 및 hello 다음 예에서는 양수, 음수 이면를 보여 줍니다.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> COS  
 반환 hello hello의 삼각 코사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.  
  
 **구문**  
  
```  
COS(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예에서는 hello 지정 된 각도의 hello COS hello를 계산 합니다.  
  
```  
SELECT COS(14.78)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> COT  
 반환 hello hello의 삼각 코탄젠트 각도 라디안에서으로 지정 된, hello에 지정 된 숫자 식입니다.  
  
 **구문**  
  
```  
COT(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예에서는 hello hello hello 지정 된 각도의 COT를 계산 합니다.  
  
```  
SELECT COT(124.1332)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> DEGREES  
 반환 hello 해당 각도에서 라디안에서으로 지정 된 각도의 단위입니다.  
  
 **구문**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 hello 개수의 반환도 PI/2 라디안 각도로 합니다.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> FLOOR  
 작은 hello 가장 큰 정수를 반환 toohello 같거나 지정 된 숫자 식입니다.  
  
 **구문**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 0 값으로 FLOOR 함수 hello 및 hello 다음 예에서는 양수, 음수 이면를 보여 줍니다.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> EXP  
 Hello의 hello 지 수 값 반환을 지정 된 숫자 식입니다.  
  
 **구문**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **설명**  
  
 hello 상수 **e** (2.718281 …)는 자연 로그의 기본 hello 합니다.  
  
 hello 숫자의 지 수는 hello 상수 **e** hello 숫자의 거듭제곱 toohello 발생 합니다. 예를 들어 EXP(1.0) = e^1.0 = 2.71828182845905이며, EXP(10) = e^10 = 22026.4657948067입니다.  
  
 자체 hello 번호 hello 숫자의 자연 로그 hello의 지 수: 즉, EXP (LOG (n)) = n입니다. Hello hello 숫자의 지 수 자연 로그는 자체 hello 번호: LOG (EXP (n)) = n입니다.  
  
 **예**  
  
 hello 다음 예제에서는 변수를 선언 하 고 hello hello 지정한 변수 (10)의 지 수 값을 반환 합니다.  
  
```  
SELECT EXP(10)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 hello 다음 예제에서는 값을 반환 hello 지 수 20의 자연 로그 hello 및 hello의 hello 자연 로그 20의 지 수입니다. 이러한 함수는 역함수 서로 hello 부동 소수점 수학 두 경우 모두 20는 반올림 된 반환 값 때문에입니다.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> LOG  
 Hello의 반환 hello 자연 로그를 지정 된 숫자 식입니다.  
  
 **구문**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
-   `base`  
  
     Hello hello 로그에 대 한 기본 설정 하는 선택적인 숫자 인수입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **설명**  
  
 Log ()는 기본적으로 hello 자연 로그를 반환합니다. Hello 선택적인 base 매개 변수를 사용 하 여 hello 로그 tooanother 값의 기수로 서 hello를 변경할 수 있습니다.  
  
 hello 자연 로그는 hello 로그 toohello 기본 **e**여기서 **e** 는 무리 상수 약 too2.718281828 됩니다.  
  
 hello hello 숫자의 지 수 자연 로그는 자체 hello 번호: LOG (EXP (n)) = n입니다. 자체 hello 번호 hello 숫자의 자연 로그 hello의 지 수: 즉, EXP (LOG (n)) = n입니다.  
  
 **예**  
  
 hello 다음 예제에서는 변수를 선언 하 고 hello 지정한 변수 (10)의 hello 로그 값을 반환 합니다.  
  
```  
SELECT LOG(10)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 hello 다음 예제에서는 계산 숫자의 지 수 hello에 대 한 로그 hello 합니다.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> LOG10  
 Hello의 반환 hello 밑이 10 인 로그를 지정 된 숫자 식입니다.  
  
 **구문**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **설명**  
  
 hello LOG10 및 POWER 함수는 역함수 관련된 tooone 다른 합니다. 예를 들어 10 ^ LOG10(n) = n입니다.  
  
 **예**  
  
 hello 다음 예제에서는 변수를 선언 하 고 hello 지정한 변수 (100)의 hello LOG10 값을 반환 합니다.  
  
```  
SELECT LOG10(100)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> PI  
 반환 hello PI의 상수 값입니다.  
  
 **구문**  
  
```  
PI ()  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예제에서는 PI의 hello 값을 반환 하는 번호입니다.  
  
```  
SELECT PI()  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> POWER  
 반환 값의 지정 된 hello hello 식 toohello 지정 된 거듭제곱 합니다.  
  
 **구문**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
-   `y`  
  
     Hello 전원 toowhich tooraise은 `numeric_expression`합니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예제는 hello 숫자 toohello 거듭제곱 3 (hello hello 숫자의 세제곱) 발생 하는 방법을 보여 줍니다.  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> RADIANS  
 숫자 식을 단위로 입력하면 라디안을 반환합니다.  
  
 **구문**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 몇 개의 각도 입력으로 사용 하 고 해당 라디안 값을 반환 합니다.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> ROUND  
 숫자 값을 반올림된 toohello 가장 가까운 정수 값을 반환합니다.  
  
 **구문**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반올림 양수와 음수 toohello 정수 가장 가까운 다음 hello 합니다.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> SIGN  
 반환 hello 양수 (+ 1), 영 (0) 또는 지정 된 숫자 식의 hello 음수 (-1) 기호입니다.  
  
 **구문**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 숫자의 hello SIGN 값에서에서 반환-2 too2 합니다.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> SIN  
 반환 hello hello의 삼각 사인 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.  
  
 **구문**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예에서는 hello hello 지정 된 각도의 SIN hello를 계산 합니다.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> SQRT  
 Hello의 반환 hello 제곱근 숫자 값을 지정 합니다.  
  
 **구문**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 hello 숫자 1-3의 제곱근입니다.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> SQUARE  
 Hello의 제곱 반환 hello 숫자 값을 지정 합니다.  
  
 **구문**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 hello 숫자 1-3 제곱 합니다.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> TAN  
 Hello의 반환 hello 탄젠트 각도 라디안에서으로 지정 된, hello에 지정 된 식입니다.  
  
 **구문**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 hello의 탄젠트를 계산 PI () / 2입니다.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a> TRUNC  
 숫자 값, 잘린된 toohello 가장 가까운 정수 값을 반환합니다.  
  
 **구문**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **인수**  
  
-   `numeric_expression`  
  
     숫자 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예제는 hello를 양수와 음수 toohello 가장 가까운 정수 값을 다음 hello를 자릅니다.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a> 형식 검사 함수  
 hello 다음 함수는 지원 형식 입력된 값에 대해 검사 하 고 각각 부울 값을 반환 합니다.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a> IS_ARRAY  
 배열 hello hello 유형의 식을 지정 된 경우를 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_ARRAY 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a> IS_BOOL  
 지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 부울을 반환 합니다.  
  
 **구문**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello에서는 IS_BOOL 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a> IS_DEFINED  
 경우 hello 속성 값이 할당에 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello hello 내에 속성이 있는지에 대 한 예제 검사를 수행 하는 hello JSON 문서를 지정 합니다. "a"가 존재 하지만 "b"가 없으므로 hello은 두 번째 false를 반환 하는 이후 hello은 먼저 true를 반환 합니다.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a> IS_NULL  
 지정 된 식 hello hello 유형의 경우를 나타내는 부울 값이 null을 반환 합니다.  
  
 **구문**  
  
```  
IS_NULL(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_NULL 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a> IS_NUMBER  
 Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 숫자를 반환 합니다.  
  
 **구문**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_NULL 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a> IS_OBJECT  
 지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 JSON 개체를 반환 합니다.  
  
 **구문**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello IS_OBJECT 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a> IS_PRIMITIVE  
 Hello의 hello 형식이 지정 되는 기본 식을 나타내는 부울 값을 반환 합니다 (문자열, 부울, 숫자 또는 null).  
  
 **구문**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello에서는 IS_PRIMITIVE 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> IS_STRING  
 Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 문자열로 반환 합니다.  
  
 **구문**  
  
```  
IS_STRING(<expression>)  
```  
  
 **인수**  
  
-   `expression`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 개체의 JSON 부울, 숫자, 문자열, null, 개체, 배열 및 정의 되지 않은 형식을 hello에서는 IS_STRING 함수를 사용 하 여  
  
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
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> 문자열 함수  
 hello 다음 스칼라 함수는 문자열 입력된 값에 대 한 작업을 수행 하 고 문자열, 숫자 또는 부울 값을 반환 합니다.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[CONTAINS](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[왼쪽](#bk_left)|[LENGTH](#bk_length)|  
|[낮은](#bk_lower)|[LTRIM](#bk_ltrim)|[바꾸기](#bk_replace)|  
|[복제](#bk_replicate)|[역방향](#bk_reverse)|[오른쪽](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[하위 문자열](#bk_substring)|  
|[위](#bk_upper)|||  
  
####  <a name="bk_concat"></a> CONCAT  
 않은 hello 두 개 이상의 문자열 값을 연결한 결과인 문자열을 반환 합니다.  
  
 **구문**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 다음 예에서는 hello의 hello 연결 문자열을 반환 하는 hello에 지정 된 값입니다.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> CONTAINS  
 첫 번째 문자열 식 hello hello를 두 번째로 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 "abc" "ab"를 포함 하 고 "d"를 포함 합니다.  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> ENDSWITH  
 끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 hello "abc"는 "b" 및 "bc"로 끝납니다.  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a> INDEX_OF  
 Hello hello 문자열을 찾을 수 없는 경우 시작 hello hello hello 첫 번째 지정 된 문자열 식 또는-1 내에서 두 번째 문자열 식의 첫 번째 발생 위치를 반환 합니다.  
  
 **구문**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예에서는 인덱스를 반환 hello "abc" 내의 다양 한 부분입니다.  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> LEFT  
 반환 문자열의 왼쪽된 부분을 지정 하는 hello로 hello 문자 수입니다.  
  
 **구문**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
-   `num_expr`  
  
     유효한 숫자 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 다양 한 길이 값에 대해 "abc"의 왼쪽 hello 합니다.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> LENGTH  
 Hello의 문자 수를 반환 합니다 hello 지정 된 문자열 식입니다.  
  
 **구문**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 문자열의 길이 hello 합니다.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> LOWER  
 대문자 데이터 toolowercase 변환한 후 문자열 식을 반환 합니다.  
  
 **구문**  
  
```  
LOWER(<str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 하위 쿼리에서 toouse 합니다.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> LTRIM  
 선행 공백을 제거한 후에 문자열 식을 반환합니다.  
  
 **구문**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 쿼리에서 LTRIM toouse 합니다.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> REPLACE  
 지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다.  
  
 **구문**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 다음 예제는 hello toouse 쿼리에서 대체 하는 방법을 보여 줍니다.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> REPLICATE  
 문자열 값을 지정한 횟수 만큼 반복합니다.  
  
 **구문**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
-   `num_expr`  
  
     유효한 숫자 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 다음 예제는 hello toouse 쿼리에서 복제 하는 방법을 보여 줍니다.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> REVERSE  
 Hello는 문자열 값의 역순을 반환합니다.  
  
 **구문**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 다음 예제는 hello toouse 쿼리에서 REVERSE 하는 방법을 보여 줍니다.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> RIGHT  
 Hello로 반환 hello 오른쪽 부분 문자열의 문자 수를 지정 합니다.  
  
 **구문**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
-   `num_expr`  
  
     유효한 숫자 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 hello 오른쪽 부분을 반환 "abc"의 다양 한 길이 값에 대 한 합니다.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> RTRIM  
 후행 공백을 제거한 후에 문자열 식을 반환합니다.  
  
 **구문**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 쿼리에서 RTRIM toouse 합니다.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> STARTSWITH  
 시작 하는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 검사 경우 hello 문자열 "abc"는 다음 예제에서는 "b"로 시작와 "a"입니다.  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> SUBSTRING  
 Hello에서 시작 하는 문자열 식의 반환 일부 문자 0부터 시작 위치를 지정 하 고 길이 또는 hello 문자열의 끝 toohello toohello 지정을 계속 합니다.  
  
 **구문**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
-   `num_expr`  
  
     유효한 숫자 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 다음 예제에서는 반환 hello 부분 문자열 "abc"의 1 1 자 길이 대 한부터 시작 합니다.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a> UPPER  
 소문자 데이터 toouppercase 변환한 후 문자열 식을 반환 합니다.  
  
 **구문**  
  
```  
UPPER(<str_expr>)  
```  
  
 **인수**  
  
-   `str_expr`  
  
     유효한 문자열 식입니다.  
  
 **반환 형식**  
  
 문자열 식을 반환합니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 toouse 위 쿼리에서  
  
```  
SELECT UPPER("Abc")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> 배열 함수  
 다음 스칼라 함수 hello는 배열 입력된 값 및 반환 숫자, 부울 또는 배열 값에 대 한 작업 수행  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a> ARRAY_CONCAT  
 hello가 두 개 이상의 배열 값을 연결한 결과인 배열을 반환 합니다.  
  
 **구문**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **인수**  
  
-   `arr_expr`  
  
     유효한 배열 식입니다.  
  
 **반환 형식**  
  
 배열 식을 반환합니다.  
  
 **예**  
  
 다음 예에서는 두 개의 tooconcatenate 배열은 방법을 hello 합니다.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a> ARRAY_CONTAINS  
 값을 지정 하는 hello hello 배열에 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **인수**  
  
-   `arr_expr`  
  
     유효한 배열 식입니다.  
  
-   `expr`  
  
     유효한 식입니다.  
  
 **반환 형식**  
  
 부울 값을 반환합니다.  
  
 **예**  
  
 다음 예제에서는 어떻게 hello toocheck ARRAY_CONTAINS를 사용 하 여 배열의 멤버 자격에 대 한 합니다.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a> ARRAY_LENGTH  
 배열 식을 지정 하는 hello 요소의 hello 수를 반환 합니다.  
  
 **구문**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **인수**  
  
-   `arr_expr`  
  
     유효한 배열 식입니다.  
  
 **반환 형식**  
  
 숫자 식을 반환합니다.  
  
 **예**  
  
 다음 예제에서는 어떻게 tooget hello ARRAY_LENGTH를 사용 하 여 배열 길이 hello 합니다.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a> ARRAY_SLICE  
 배열 식의 일부를 반환합니다.
  
 **구문**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **인수**  
  
-   `arr_expr`  
  
     유효한 배열 식입니다.  
  
-   `num_expr`  
  
     유효한 숫자 식입니다.  
  
 **반환 형식**  
  
 부울 값을 반환합니다.  
  
 **예**  
  
 다음 예제에서는 어떻게 hello tooget ARRAY_SLICE를 사용 하 여 배열에 포함 합니다.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> 공간 함수  
 hello 다음 스칼라 함수는 공간 개체의 입력된 값에 대 한 작업을 수행 하 고 숫자 또는 부울 값을 반환 합니다.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> ST_DISTANCE  
 두 hello GeoJSON 지점, 다각형 또는 LineString 식 사이의 hello 거리를 반환합니다.  
  
 **구문**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **인수**  
  
-   `spatial_expr`  
  
     유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.  
  
 **반환 형식**  
  
 Hello 거리를 포함 하는 숫자 식을 반환 합니다. 이 hello 기본 참조 시스템에 대 한 미터 단위로 표현 됩니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 tooreturn의 hello 30 km 내에 있는 모든 패밀리 문서 hello ST_DISTANCE 기본 제공 함수를 사용 하 여 위치를 지정 합니다. 에서도 확인할 수 있습니다.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> ST_WITHIN  
 Hello 첫 번째 인수에 지정 된 hello GeoJSON 개체 (점, 다각형, 또는 LineString) hello GeoJSON (점, 다각형, 또는 LineString) 내에서 hello 두 번째 인수에는 표시 하는 부울 식을 반환 합니다.  
  
 **구문**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **인수**  
  
-   `spatial_expr`  
  
     유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.  
 
-   `spatial_expr`  
  
     유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.  
  
 **반환 형식**  
  
 부울 값을 반환합니다.  
  
 **예**  
  
 다음 예제는 hello 방법을 toofind 모든 제품군에 설명 ST_WITHIN를 사용 하 여 다각형 내의 보여 줍니다.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a> ST_INTERSECTS  
 Hello 첫 번째 인수에 지정 된 hello GeoJSON 개체 (점, 다각형, 또는 LineString) hello GeoJSON (점, 다각형, 또는 LineString) hello 두 번째 인수에 교차 하는지 여부를 나타내는 부울 식을 반환 합니다.  
  
 **구문**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **인수**  
  
-   `spatial_expr`  
  
     유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.  
 
-   `spatial_expr`  
  
     유효한 GeoJSON Point, Polygon 또는 LineString 개체 식입니다.  
  
 **반환 형식**  
  
 부울 값을 반환합니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 toofind 다각형 지정한 hello와 교차 하는 모든 영역입니다.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> ST_ISVALID  
 Hello GeoJSON 지점, 다각형 또는 LineString 식이 유효한 경우이 지정 되었는지 여부를 나타내는 부울 값을 반환 합니다.  
  
 **구문**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **인수**  
  
-   `spatial_expr`  
  
     유효한 GeoJSON Point, Polygon 또는 LineString 식입니다.  
  
 **반환 형식**  
  
 부울 식을 반환합니다.  
  
 **예**  
  
 hello 방법을 예제와 다음 toocheck 요소가 있는 경우 ST_VALID를 사용 하 여 유효 합니다.  
  
 예를 들어이 요소에 hello 유효한 [-90, 90] 값의 범위에 있지 않은 위도 값, 이므로 false를 반환 하는 쿼리를 hello 합니다.  
  
 다각형에 대 한 hello 사양에서는 hello 마지막 좌표 쌍 제공 수 있어야 GeoJSON hello 동일 hello 첫 번째 toocreate로 닫힌된 셰이프. 다각형 내의 점을 시계 반대 방향 순서로 지정해야 합니다. 시계 방향으로 순서에 지정 된 다각형 hello hello 영역 내에서 역을 수를 나타냅니다.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED  
 Hello GeoJSON 지점, 다각형 또는 LineString 식이 지정 된 경우 부울 값을 포함 하는 JSON 값은 유효 하 고, 잘못 된 경우에 문자열 값으로 이유 hello 또한 반환 합니다.  
  
 **구문**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **인수**  
  
-   `spatial_expr`  
  
     유효한 GeoJSON 꼭짓점 또는 다각형 식입니다.  
  
 **반환 형식**  
  
 Hello 지정 GeoJSON 지점 또는 다각형 식은 유효 하며 유효 하지 않은 경우에 문자열 값으로 이유 hello 또한 경우 부울 값을 포함 하는 JSON 값을 반환 합니다.  
  
 **예**  
  
 다음 예제에서는 어떻게 hello ST_ISVALIDDETAILED를 사용 하 여 세부 정보와) (함께 toocheck 유효 합니다.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Hello 결과 집합은 다음과 같습니다.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>다음 단계  
 [Azure Cosmos DB에 대한 SQL 구문 및 SQL 쿼리](documentdb-sql-query.md)   
 [Azure Cosmos DB 설명서](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
