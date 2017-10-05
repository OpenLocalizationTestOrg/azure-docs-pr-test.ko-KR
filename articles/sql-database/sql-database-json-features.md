---
title: "Azure SQL Database JSON 기능 | Microsoft Docs"
description: "Azure SQL 데이터베이스에서는 JSON(JavaScript Object Notation) 표기법으로 데이터 구문 분석, 쿼리 및 서식 지정을 수행할 수 있습니다."
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
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="11b2d-103">Azure SQL 데이터베이스의 JSON 기능 시작</span><span class="sxs-lookup"><span data-stu-id="11b2d-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="11b2d-104">Azure SQL 데이터베이스를 사용하면 [JSON](http://www.json.org/) (JavaScript Object Notation) 형식으로 표현된 데이터를 구문 분석 및 쿼리하고 관계형 데이터를 JSON 텍스트로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="11b2d-105">JSON은 최신 웹 및 모바일 응용 프로그램에서 데이터를 교환하는 데 사용되는 일반적인 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="11b2d-106">또한 JSON은 로그 파일 또는 NoSQL 데이터베이스(예: [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/))에 반구조화된 데이터를 저장하는 데도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="11b2d-107">많은 REST 웹 서비스는 JSON 텍스트로 형식이 지정된 결과를 반환하거나 JSON으로 형식이 지정된 데이터를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="11b2d-108">대부분의 Azure 서비스(예: [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/) 및 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/))에는 JSON을 반환하거나 사용하는 REST 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="11b2d-109">Azure SQL 데이터베이스를 사용하여 JSON 데이터를 쉽게 사용하고 데이터베이스를 최신 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="11b2d-110">개요</span><span class="sxs-lookup"><span data-stu-id="11b2d-110">Overview</span></span>
<span data-ttu-id="11b2d-111">Azure SQL 데이터베이스는 JSON 데이터를 사용하기 위한 다음과 같은 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![JSON 함수](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="11b2d-113">JSON 텍스트가 있는 경우 JSON에서 데이터를 추출하거나 기본 제공 함수 [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx) 및 [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx)을 사용하여 JSON 형식이 제대로 지정되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="11b2d-114">[JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) 함수를 사용하면 JSON 텍스트 내의 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="11b2d-115">고급 쿼리 및 분석을 위해 [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) 함수는 JSON 개체의 배열을 행 집합을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="11b2d-116">모든 SQL 쿼리는 반환된 결과 집합에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="11b2d-117">마지막으로 관계형 테이블에 저장된 데이터의 형식을 JSON 텍스트로 지정할 수 있는 [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) 절이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="11b2d-118">관계형 데이터 형식을 JSON으로 지정</span><span class="sxs-lookup"><span data-stu-id="11b2d-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="11b2d-119">데이터베이스 계층에서 데이터를 가져오고 JSON 형식으로 응답을 제공하는 웹 서비스 또는 JSON으로 형식이 지정된 데이터를 수락하는 클라이언트 쪽 JavaScript 프레임워크나 라이브러리가 있는 경우 SQL 쿼리에서 직접 데이터베이스 콘텐츠 형식을 JSON으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="11b2d-120">Azure SQL 데이터베이스의 결과 형식을 JSON으로 지정하는 응용 프로그램 코드를 작성하거나, 테이블 형식 쿼리 결과를 변환한 다음 개체를 JSON 형식으로 직렬화하는 JSON 직렬화 라이브러리를 더 이상 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="11b2d-121">대신, FOR JSON 절을 사용하여 Azure SQL 데이터베이스에서 SQL 쿼리 결과의 형식을 JSON으로 지정한 후 응용 프로그램에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="11b2d-122">다음 예제에서 Sales.Customer 테이블의 행은 FOR JSON 절을 사용하여 JSON으로 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="11b2d-123">FOR JSON PATH 절은 쿼리의 결과 형식을 JSON 텍스트로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="11b2d-124">열 이름은 키로 사용되지만 셀 값은 JSON 값으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="11b2d-125">각 행이 별도의 JSON 개체로 형식이 지정될 경우 결과 집합은 JSON 배열로 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="11b2d-126">PATH는 열 별칭에 점 표기법을 사용하여 JSON 결과의 출력 형식을 사용자 지정할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="11b2d-127">다음 쿼리는 출력 JSON 형식에서 "CustomerName" 키의 이름을 변경하고 전화번호 및 팩스 번호를 "Contact" 하위 개체에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="11b2d-128">이 쿼리의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="11b2d-129">이 예제에서는 [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) 옵션을 지정하여 배열 대신 단일 JSON 개체를 반환했습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="11b2d-130">쿼리 결과로 단일 개체를 반환하는지 알고 있다면 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="11b2d-131">FOR JSON 절의 주 값은 중첩된 JSON 개체 또는 배열로 형식이 지정된 데이터베이스에서 복잡한 계층적 데이터를 반환할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="11b2d-132">다음 예제에서는 Customer에 속하는 Orders를 Orders의 중첩 배열로 포함하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="11b2d-133">Customer 데이터를 가져온 다음 관련 Orders 목록을 인출하는 별도의 쿼리를 전송하는 대신, 다음 샘플 출력에 표시된 대로 단일 쿼리로 필요한 모든 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="11b2d-134">JSON 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="11b2d-134">Working with JSON data</span></span>
<span data-ttu-id="11b2d-135">엄격하게 구조화된 데이터가 없거나, 복잡한 하위 개체, 배열 또는 계층적 데이터가 있거나, 시간이 지나면서 데이터 구조가 변화할 경우 JSON 형식을 사용하면 복잡한 데이터 구조를 나타내는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="11b2d-136">JSON은 Azure SQL 데이터베이스에서 다른 문자열 형식처럼 사용할 수 있는 텍스트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="11b2d-137">JSON 데이터를 표준 NVARCHAR로 전송하거나 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="11b2d-138">이 예제에서 사용되는 JSON 데이터는 NVARCHAR(MAX) 형식을 사용하여 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="11b2d-139">JSON을 이 테이블에 삽입하거나, 다음 예제와 같이 표준 Transact-SQL 구문을 사용하여 저장 프로시저의 인수로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="11b2d-140">Azure SQL 데이터베이스의 문자열 데이터를 사용하는 모든 클라이언트 쪽 언어 또는 라이브러리에서도 JSON 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="11b2d-141">JSON은 메모리 최적화 테이블 또는 시스템 버전 테이블같이 NVARCHAR 형식을 지원하는 모든 테이블에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="11b2d-142">JSON을 사용할 경우 클라이언트 쪽 코드 또는 데이터베이스 계층에 어떤 제약도 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="11b2d-143">JSON 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="11b2d-143">Querying JSON data</span></span>
<span data-ttu-id="11b2d-144">Azure SQL 테이블에 저장된 JSON으로 형식이 지정된 데이터가 있는 경우 JSON 함수를 통해 SQL 쿼리에서 이 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="11b2d-145">Azure SQL 데이터베이스에서 사용할 수 있는 JSON 함수는 JSON으로 형식이 지정된 데이터를 다른 SQL 데이터 형식처럼 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="11b2d-146">JSON 텍스트에서 쉽게 값을 추출하고 쿼리에서 JSON 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="11b2d-147">JSON_VALUE 함수는 데이터 열에 저장된 JSON 텍스트의 값을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="11b2d-148">이 함수는 JavaScript와 비슷한 경로를 사용하여 추출할 JSON 텍스트의 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="11b2d-149">추출된 값은 SQL 쿼리의 모든 부분에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="11b2d-150">JSON_QUERY 함수는 JSON_VALUE와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="11b2d-151">JSON_VALUE와 달리 이 함수는 JSON 텍스트에 배치된 배열 또는 개체와 같은 복잡한 하위 개체를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="11b2d-152">JSON_MODIFY 함수를 사용하여 이전 값을 덮어쓰는 새 값뿐만 아니라 업데이트해야 하는 JSON 텍스트의 값 경로를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="11b2d-153">이러한 방식으로 전체 구조를 다시 구문 분석하지 않고 JSON 텍스트를 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="11b2d-154">JSON은 표준 텍스트로 저장되므로 텍스트 열에 저장된 값의 형식이 올바를 것으로 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="11b2d-155">JSON 열에 저장된 텍스트는 표준 Azure SQL 데이터베이스 check 제약 조건 및 ISJSON 함수를 사용하여 올바르게 형식이 지정되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="11b2d-156">입력 텍스트가 JSON으로 올바르게 형식이 지정되면 ISJSON 함수는 값 1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="11b2d-157">JSON 열이 삽입되거나 업데이트될 때마다 이 제약 조건은 새 텍스트 값이 잘못된 형식의 JSON이 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="11b2d-158">JSON을 테이블 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="11b2d-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="11b2d-159">Azure SQL 데이터베이스에서는 JSON 컬렉션을 테이블 형식으로 변환하고 JSON 데이터를 로드 또는 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="11b2d-160">OPENJSON은 JSON 텍스트를 구문 분석하고, JSON 개체의 배열을 찾고, 배열의 요소를 반복하고, 배열의 각 요소에 대한 출력 결과에 하나의 행을 반환하는 테이블 값 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![JSON 테이블 형식](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="11b2d-162">위의 예에서 열려야 하는 JSON 배열을 찾을 위치($.Orders 경로), 결과로 반환해야 하는 열 및 셀로 반환될 JSON 값을 찾을 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="11b2d-163">@orders 변수의 JSON 배열을 행 집합으로 변환하거나 이 결과 집합을 분석하거나, 행을 표준 테이블에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="11b2d-164">JSON 배열로 형식이 지정되고 저장 프로시저에 대한 매개 변수로 제공되는 주문 컬렉션은 구문 분석된 후 Orders 테이블에 삽입될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11b2d-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11b2d-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11b2d-165">Next steps</span></span>
<span data-ttu-id="11b2d-166">JSON을 응용 프로그램에 통합하는 방법을 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11b2d-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="11b2d-167">TechNet 블로그</span><span class="sxs-lookup"><span data-stu-id="11b2d-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="11b2d-168">MSDN 설명서</span><span class="sxs-lookup"><span data-stu-id="11b2d-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="11b2d-169">Channel 9 비디오</span><span class="sxs-lookup"><span data-stu-id="11b2d-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="11b2d-170">JSON을 응용 프로그램에 통합하는 다양한 시나리오에 대해 알아보려면 이 [Channel 9 비디오](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)에서 데모를 참조하거나 [JSON 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)에서 사용 사례와 일치하는 시나리오 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="11b2d-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

