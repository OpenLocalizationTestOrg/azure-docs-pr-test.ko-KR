---
title: "aaaInvoke 저장 프로시저에서 Azure 데이터 팩터리 복사 작업 | Microsoft Docs"
description: "Azure Data Factory에서 SQL Server 나 Azure SQL 데이터베이스의 저장된 프로시저 tooinvoke 활동을 복사 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="77f38-103">Azure Data Factory의 복사 작업에서 저장 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="77f38-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="77f38-104">데이터를 복사 하는 경우 [SQL Server](data-factory-sqlserver-connector.md) 또는 [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md), hello를 구성할 수 있습니다 **SqlSink** 복사 활동 tooinvoke 저장된 프로시저에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="77f38-105">Toouse hello 저장 프로시저 tooperform toohello 대상 테이블에 데이터를 삽입 하기 전에 (여러 등 공용 테이블에 삽입 값 조회 열 병합) 추가로 처리 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="77f38-106">이 기능은 [테이블 값 매개 변수](https://msdn.microsoft.com/library/bb675163.aspx)을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="77f38-107">다음 예제는 hello 방법을 tooinvoke SQL Server에서 저장된 프로시저에서에서 데이터베이스를 데이터 팩토리 파이프라인 (복사 작업)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="77f38-108">출력 데이터 집합 JSON</span><span class="sxs-lookup"><span data-stu-id="77f38-108">Output dataset JSON</span></span>
<span data-ttu-id="77f38-109">Hello 출력 데이터 집합 JSON 설정 hello **형식** 를: **SqlServerTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="77f38-110">너무 설정**AzureSqlTable** toouse Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="77f38-111">값에 대 한 hello **tableName** 속성 hello hello 저장 프로시저의 첫 번째 매개 변수 이름을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="77f38-112">복사 작업 JSON의 SqlSink 섹션</span><span class="sxs-lookup"><span data-stu-id="77f38-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="77f38-113">Hello 정의 **SqlSink** hello 복사 활동 JSON에서에서 다음과 같은 섹션.</span><span class="sxs-lookup"><span data-stu-id="77f38-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="77f38-114">tooinvoke hello 싱크/대상 데이터베이스에 데이터를 삽입 하는 동안 저장된 프로시저 모두에 대 한 값을 지정 **SqlWriterStoredProcedureName** 및 **SqlWriterTableType** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="77f38-115">이러한 속성의 설명에 대 한 참조 [hello SQL Server 커넥터 문서의 SqlSink 섹션](data-factory-sqlserver-connector.md#sqlsink)합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="77f38-116">저장 프로시저 정의</span><span class="sxs-lookup"><span data-stu-id="77f38-116">Stored procedure definition</span></span> 
<span data-ttu-id="77f38-117">데이터베이스에 이름이 hello로 hello 저장 프로시저를 정의 **SqlWriterStoredProcedureName**합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="77f38-118">hello 저장 프로시저 hello 원본 데이터 저장소에서 입력된 데이터를 처리 하 고 hello 대상 데이터베이스의 테이블로 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="77f38-119">저장된 프로시저의 첫 번째 매개 변수 hello의 hello 이름 hello 데이터 집합 JSON (마케팅)에 정의 된 hello tableName 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="77f38-120">테이블 유형 정의</span><span class="sxs-lookup"><span data-stu-id="77f38-120">Table type definition</span></span>
<span data-ttu-id="77f38-121">데이터베이스에 hello로 이름과 같은 이름을 사용 하는 hello 테이블 형식을 정의 **SqlWriterTableType**합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="77f38-122">hello 테이블 형식의 hello 스키마에는 hello 입력된 데이터 집합의 hello 스키마와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="77f38-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77f38-123">Next steps</span></span>
<span data-ttu-id="77f38-124">커넥터 문서에 대 한 완전 한 JSON 예제를 따르는 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="77f38-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="77f38-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="77f38-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="77f38-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="77f38-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
