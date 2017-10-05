---
title: "Azure Data Factory 복사 작업에서 저장 프로시저 호출 | Microsoft Docs"
description: "Azure SQL Database 또는 Azure Data Factory 복사 작업의 SQL Server에서 저장 프로시저를 호출하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="dd8ce-103">Azure Data Factory의 복사 작업에서 저장 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="dd8ce-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="dd8ce-104">[SQL Server](data-factory-sqlserver-connector.md) 또는 [Azure SQL Database](data-factory-azure-sql-connector.md)로 데이터를 복사할 때 복사 작업에 저장 프로시저를 호출할 **SqlSink**를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="dd8ce-105">대상 테이블에 데이터를 삽입하기 전에 추가 처리(열 병합, 값 검색, 여러 테이블에 삽입 등)를 수행하는 저장 프로시저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="dd8ce-106">이 기능은 [테이블 값 매개 변수](https://msdn.microsoft.com/library/bb675163.aspx)을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="dd8ce-107">다음 샘플에서는 Data Factory 파이프라인(복사 작업)에서 SQL Server Database의 저장 프로시저를 호출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="dd8ce-108">출력 데이터 집합 JSON</span><span class="sxs-lookup"><span data-stu-id="dd8ce-108">Output dataset JSON</span></span>
<span data-ttu-id="dd8ce-109">출력 데이터 집합 JSON에서 **형식**을 **SqlServerTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="dd8ce-110">Azure SQL Database에 사용하기 위해 이 항목을 **AzureSqlTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="dd8ce-111">**tableName** 속성 값은 저장 프로시저의 첫 번째 매개 변수 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="dd8ce-112">복사 작업 JSON의 SqlSink 섹션</span><span class="sxs-lookup"><span data-stu-id="dd8ce-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="dd8ce-113">복사 작업 JSON의 **SqlSink** 섹션을 다음과 같이 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="dd8ce-114">데이터를 싱크/대상 데이터베이스에 삽입하는 동안 저장 프로시저를 호출하려면 **SqlWriterStoredProcedureName** 및 **SqlWriterTableType** 속성 모두에 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="dd8ce-115">이러한 속성에 대한 설명은 [SQL Server 커넥터 문서의 SqlSink 섹션](data-factory-sqlserver-connector.md#sqlsink)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="dd8ce-116">저장 프로시저 정의</span><span class="sxs-lookup"><span data-stu-id="dd8ce-116">Stored procedure definition</span></span> 
<span data-ttu-id="dd8ce-117">데이터베이스에서 **SqlWriterStoredProcedureName**과 동일한 이름으로 저장 프로시저를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="dd8ce-118">저장 프로시저는 원본 데이터 저장소의 입력 데이터를 처리하고 데이터를 대상 데이터베이스의 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="dd8ce-119">저장 프로시저의 첫 번째 매개 변수 이름은 데이터 집합 JSON(Marketing)에 정의된 tableName과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="dd8ce-120">테이블 유형 정의</span><span class="sxs-lookup"><span data-stu-id="dd8ce-120">Table type definition</span></span>
<span data-ttu-id="dd8ce-121">데이터베이스에서 **SqlWriterTableType**과 동일한 이름으로 테이블 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="dd8ce-122">테이블 형식의 스키마는 입력 데이터 집합의 스키마와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="dd8ce-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd8ce-123">Next steps</span></span>
<span data-ttu-id="dd8ce-124">완전한 JSON 예제에 대한 다음 커넥터 문서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="dd8ce-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="dd8ce-125">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="dd8ce-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="dd8ce-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dd8ce-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
