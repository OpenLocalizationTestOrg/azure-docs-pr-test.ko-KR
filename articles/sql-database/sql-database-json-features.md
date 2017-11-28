---
title: "SQL 데이터베이스 JSON 기능 aaaAzure | Microsoft Docs"
description: "Azure SQL 데이터베이스 tooparse, 쿼리 및 개체 JSON (JavaScript Notation) 표기법의 데이터 형식 지정 하면 있습니다."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="c638a-103">Azure SQL 데이터베이스의 JSON 기능 시작</span><span class="sxs-lookup"><span data-stu-id="c638a-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="c638a-104">Azure SQL 데이터베이스를 사용하면 [JSON](http://www.json.org/) (JavaScript Object Notation) 형식으로 표현된 데이터를 구문 분석 및 쿼리하고 관계형 데이터를 JSON 텍스트로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="c638a-105">JSON은 최신 웹 및 모바일 응용 프로그램에서 데이터를 교환하는 데 사용되는 일반적인 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="c638a-106">또한 JSON은 로그 파일 또는 NoSQL 데이터베이스(예: [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/))에 반구조화된 데이터를 저장하는 데도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="c638a-107">많은 REST 웹 서비스는 JSON 텍스트로 형식이 지정된 결과를 반환하거나 JSON으로 형식이 지정된 데이터를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="c638a-108">대부분의 Azure 서비스(예: [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/) 및 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/))에는 JSON을 반환하거나 사용하는 REST 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="c638a-109">Azure SQL 데이터베이스를 사용하여 JSON 데이터를 쉽게 사용하고 데이터베이스를 최신 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="c638a-110">개요</span><span class="sxs-lookup"><span data-stu-id="c638a-110">Overview</span></span>
<span data-ttu-id="c638a-111">Azure SQL 데이터베이스 hello를 다음 JSON 데이터로 작업 하기 위한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![JSON 함수](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="c638a-113">JSON 텍스트를 설정한 경우에 JSON에서 데이터를 추출 하거나 hello 기본 제공 함수를 사용 하 여 JSON 형식이 제대로 확인 수 있습니다 [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), 및 [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c638a-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="c638a-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) 함수는 JSON 텍스트 내의 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="c638a-115">고급 쿼리 및 분석을 위해 [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) 함수는 JSON 개체의 배열을 행 집합을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="c638a-116">결과 집합을 반환 하는 hello에서 모든 SQL 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="c638a-117">마지막으로 관계형 테이블에 저장된 데이터의 형식을 JSON 텍스트로 지정할 수 있는 [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) 절이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="c638a-118">관계형 데이터 형식을 JSON으로 지정</span><span class="sxs-lookup"><span data-stu-id="c638a-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="c638a-119">웹 서비스는 hello 데이터베이스에서 데이터 계층 및 json에서 응답을 제공 형식으로 또는 JSON으로 서식이 지정 된 클라이언트 쪽 JavaScript 프레임 워크 또는 데이터를 허용 하는 라이브러리를 사용 하도록 설정한 경우 SQL 쿼리에서 직접 데이터베이스 콘텐츠를 JSON으로 서식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="c638a-120">JSON으로 Azure SQL 데이터베이스의 결과 형식을 지정 하는 응용 프로그램 코드를 toowrite 하면 더 이상 일부 JSON serialization 라이브러리 tooconvert 테이블 형식 쿼리 결과 포함 하 고 tooJSON 형식 개체를 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="c638a-121">대신, Azure SQL 데이터베이스에서 JSON으로 JSON 절 tooformat SQL 쿼리 결과 대 한 hello를 사용 하 고 응용 프로그램에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="c638a-122">다음 예제는 hello, hello Sales.Customer 테이블의 행은 JSON으로 hello FOR JSON 절을 사용 하 여 서식이 지정 된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="c638a-123">hello FOR JSON PATH 절 형식을 JSON 텍스트로 hello hello 쿼리 결과 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="c638a-124">Hello 셀 값은 JSON 값으로 생성 되지만 열 이름이 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="c638a-125">hello 결과 집합은 각 행 별도 JSON 개체가 서식이 있는 JSON 배열로 서식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="c638a-126">경로가 나타냅니다 열 별칭의 점 표기법을 사용 하 여 JSON 결과의 hello 출력 형식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="c638a-127">다음 쿼리에서 hello hello 출력 JSON 형식으로 hello "CustomerName" 키의 hello 이름을 변경 하 고 hello "Contact" 하위 개체에 전화 및 팩스 번호:</span><span class="sxs-lookup"><span data-stu-id="c638a-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="c638a-128">hello 출력이 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="c638a-129">이 예제에서는 반환 배열 대신 단일 JSON 개체 hello를 지정 하 여 [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="c638a-130">쿼리 결과로 단일 개체를 반환하는지 알고 있다면 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="c638a-131">hello 주의 hello FOR JSON 절은 중첩 된 JSON 개체 또는 배열 형식으로 지정 하 여 데이터베이스에서 복잡 한 계층적 데이터를 반환할 수 있도록</span><span class="sxs-lookup"><span data-stu-id="c638a-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="c638a-132">다음 예제 tooinclude 정렬 방법을 toohello 고객 주문 중첩 된 배열에 속해 있는 hello:</span><span class="sxs-lookup"><span data-stu-id="c638a-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="c638a-133">Hello 다음 샘플 출력 에서처럼 tooget 고객 데이터를 별도 쿼리 및 toofetch 관련된 주문 목록이, 보내는 대신 단일 쿼리를 사용 하 여 모든 hello 필요한 데이터를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="c638a-134">JSON 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="c638a-134">Working with JSON data</span></span>
<span data-ttu-id="c638a-135">없는 경우 엄격 하 게 구조화 된 데이터를 복잡 한 하위 개체, 배열 또는 계층적 데이터 또는 데이터 구조가 시간이 지남에 따라 발전 하는 경우 hello JSON 형식은 도와 toorepresent 경우 모든 복잡 한 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="c638a-136">JSON은 Azure SQL 데이터베이스에서 다른 문자열 형식처럼 사용할 수 있는 텍스트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="c638a-137">JSON 데이터를 표준 NVARCHAR로 전송하거나 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="c638a-138">이 예에서 사용 된 JSON 데이터 hello hello nvarchar (max) 형식을 사용 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="c638a-139">JSON이이 테이블에 삽입 여부 hello 다음 예제에에서 표시 된 대로 표준 TRANSACT-SQL 구문을 사용 하 여 hello 저장 프로시저의 인수로 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="c638a-140">Azure SQL 데이터베이스의 문자열 데이터를 사용하는 모든 클라이언트 쪽 언어 또는 라이브러리에서도 JSON 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="c638a-141">JSON은 메모리 액세스에 최적화 된 테이블 또는 시스템 버전 테이블 같은 hello NVARCHAR 형식을 지 원하는 모든 테이블에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="c638a-142">JSON은 hello 데이터베이스 계층 또는 hello 클라이언트 측 코드에는 제약 조건을 제공 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="c638a-143">JSON 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="c638a-143">Querying JSON data</span></span>
<span data-ttu-id="c638a-144">Azure SQL 테이블에 저장된 JSON으로 형식이 지정된 데이터가 있는 경우 JSON 함수를 통해 SQL 쿼리에서 이 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="c638a-145">Azure SQL 데이터베이스에서 사용할 수 있는 JSON 함수는 JSON으로 형식이 지정된 데이터를 다른 SQL 데이터 형식처럼 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="c638a-146">쉽게 hello JSON 텍스트에서에서 값을 추출 하 고 JSON 데이터를 사용 하 여 모든 쿼리의 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="c638a-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="c638a-147">JSON_VALUE 함수 hello hello 데이터 열에 저장 된 JSON 텍스트에서 값을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="c638a-148">이 함수는 JSON 텍스트 tooextract에서 JavaScript와 유사한 경로 tooreference 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="c638a-149">SQL 쿼리의 모든 부분에서 추출 된 hello 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="c638a-150">hello JSON_QUERY 함수는 비슷한 tooJSON_VALUE입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="c638a-151">JSON_VALUE와 달리 이 함수는 JSON 텍스트에 배치된 배열 또는 개체와 같은 복잡한 하위 개체를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="c638a-152">hello JSON_MODIFY 함수를 사용 하면 새 값을 이전과 hello 덮어쓰는 비롯 하 여 업데이트 해야 하는 hello JSON 텍스트에 hello 값의 hello 경로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="c638a-153">이러한 방식으로 hello 전체 구조 다시 구문 분석 하지 않고 JSON 텍스트를 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="c638a-154">표준 텍스트, 저장 된 JSON은 이후 텍스트 열에 저장 된 hello 값 올바르게 서식 지정가 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="c638a-155">JSON 열에 저장 된 텍스트 표준 Azure SQL 데이터베이스 check 제약 조건 및 hello ISJSON 함수를 사용 하 여 올바른 형식 인지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="c638a-156">Hello 입력된 텍스트 형식이 제대로 지정 하는 경우 JSON, hello ISJSON 함수 hello 값 1을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="c638a-157">JSON 열이 삽입되거나 업데이트될 때마다 이 제약 조건은 새 텍스트 값이 잘못된 형식의 JSON이 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="c638a-158">JSON을 테이블 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="c638a-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="c638a-159">Azure SQL 데이터베이스에서는 JSON 컬렉션을 테이블 형식으로 변환하고 JSON 데이터를 로드 또는 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="c638a-160">OPENJSON은 JSON 텍스트를 구문 분석 하는 JSON 개체 배열을 찾아서 hello hello 배열 요소를 반복 하 고 hello 배열의 각 요소에 대 한 hello 출력 결과에 하나의 행을 반환 하는 테이블 반환 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON 테이블 형식](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="c638a-162">여기서 toolocate hello hello $ (에서 열 수 있는 JSON 배열 지정할 수 있습니다 위의 hello 예제. 주문 경로),이로 인해 어떤 열 반환 해야 하 고 셀로 toofind hello JSON 값 반환 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="c638a-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="c638a-163">Hello 사용 하 여 JSON 배열의 변환 수 @orders 변수 행 집합으로이 결과 집합을 분석 하거나 표준 테이블에 행을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="c638a-164">JSON 배열로 포맷 하 고 매개 변수 toohello 저장 프로시저를 구문 분석 하 고 hello Orders 테이블에 삽입할 수 있는 그대로 제공 하는 hello 모음 주문입니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c638a-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c638a-165">Next steps</span></span>
<span data-ttu-id="c638a-166">toolearn toointegrate JSON 응용 프로그램에 이러한 리소스를 확인 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="c638a-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="c638a-167">TechNet 블로그</span><span class="sxs-lookup"><span data-stu-id="c638a-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="c638a-168">MSDN 설명서</span><span class="sxs-lookup"><span data-stu-id="c638a-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="c638a-169">Channel 9 비디오</span><span class="sxs-lookup"><span data-stu-id="c638a-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="c638a-170">toolearn JSON 응용 프로그램에 통합 하기 위한 다양 한 시나리오에 대 한 참조이 hello 데모 [Channel 9 비디오](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) 프로그램 사용 사례에 일치 하는 시나리오 찾기 또는 [JSON 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c638a-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

