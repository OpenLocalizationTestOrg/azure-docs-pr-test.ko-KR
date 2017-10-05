---
title: "Azure Data Factory에서 반복 가능한 복사 | Microsoft Docs"
description: "데이터를 복사하는 조각이 두 번 이상 실행되더라도 중복을 방지하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="1d05f-103">Azure Data Factory에서 반복 가능한 복사</span><span class="sxs-lookup"><span data-stu-id="1d05f-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1d05f-104">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="1d05f-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="1d05f-105">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="1d05f-106">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1d05f-107">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1d05f-108">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="1d05f-109">다음 예제는 Azure SQL에 대한 것이지만, 직사각 데이터 집합을 지원하는 모든 데이터 저장소에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="1d05f-110">데이터 저장소에 대해 소스의 **type** 및 **query** 속성(예: sqlReaderQuery 대신 query)을 조정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="1d05f-111">일반적으로 관계형 저장소에서 읽어올 때는 해당 조각에 대한 데이터만 읽고자 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="1d05f-112">이것은 Azure Data Factory에서 제공하는 WindowStart 및 WindowEnd 시스템 변수를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="1d05f-113">[Azure Data Factory - 함수 및 시스템 변수](data-factory-functions-variables.md) 문서에서 Azure Data Factory의 변수 및 함수 부분을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="1d05f-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="1d05f-114">예:</span><span class="sxs-lookup"><span data-stu-id="1d05f-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="1d05f-115">이 쿼리는 MyTable 테이블에서 조각 기간 범위(WindowEnd-> WindowStart)에 속하는 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="1d05f-116">이 조각을 다시 실행하면 항상 같은 데이터만 읽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="1d05f-117">다른 경우 전체 테이블을 읽고 다음과 같이 sqlReaderQuery를 정의하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="1d05f-118">SqlSink에 반복 가능한 쓰기</span><span class="sxs-lookup"><span data-stu-id="1d05f-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="1d05f-119">다른 데이터 저장소에서 **Azure SQL/SQL Server**로 데이터를 복사할 때 의도치 않은 결과를 방지하려면 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="1d05f-120">Azure SQL/SQL Server 데이터베이스로 데이터를 복사할 때 복사 작업은 기본적으로 싱크 테이블에 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="1d05f-121">예를 들어 두 개의 레코드가 포함된 CSV(쉼표로 구분 된 값) 파일에서 Azure SQL/SQL Server 데이터베이스의 다음 테이블로 데이터를 복사한다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="1d05f-122">조각이 실행되면 두 레코드가 SQL 테이블에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="1d05f-123">원본 파일에서 오류를 발견하고 Down Tube의 수량을 2에서 4로 업데이트했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="1d05f-124">해당 기간의 데이터 조각을 수동으로 다시 실행하면 Azure/SQL Server 데이터베이스에 새 레코드가 두 개 추가된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="1d05f-125">이 예에서는 테이블에 기본 키 제약 조건이 있는 열이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="1d05f-126">이 동작을 방지하려면 다음 두 메커니즘 중 하나를 사용하여 UPSERT 의미 체계를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="1d05f-127">메커니즘 1: sqlWriterCleanupScript 사용</span><span class="sxs-lookup"><span data-stu-id="1d05f-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="1d05f-128">**sqlWriterCleanupScript** 속성을 사용하여 싱크 테이블의 데이터를 정리한 후 조각이 실행되면 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="1d05f-129">조각이 실행되면 SQL 테이블의 조각에 해당하는 데이터를 삭제하는 정리 스크립트가 가장 먼저 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="1d05f-130">그러면 복사 작업에서 데이터를 SQL 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="1d05f-131">조각이 다시 실행되면 필요에 따라 수량이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="1d05f-132">원본 csv에서 Flat Washer 레코드가 제거되었다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="1d05f-133">이제 조각을 다시 실행하면 다음과 같은 결과가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="1d05f-134">복사 작업에서는 정리 스크립트를 실행하여 해당 조각에 대한 데이터를 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="1d05f-135">그런 다음 csv(레코드 하나만 포함)에서 입력을 읽어서 테이블에 삽입했습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="1d05f-136">메커니즘 2: sliceIdentifierColumnName 사용</span><span class="sxs-lookup"><span data-stu-id="1d05f-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1d05f-137">현재 sliceIdentifierColumnName은 Azure SQL Data Warehouse에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="1d05f-138">두 번째 메커니즘은 대상 테이블에 전용 열(sliceIdentifierColumnName)을 만들어서 반복성을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="1d05f-139">이 열은 Azure 데이터 팩터리에서 원본 및 대상을 동기화 상태로 유지하도록 할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="1d05f-140">이 방법은 대상 SQL 테이블 스키마를 유연하게 변경하거나 정의할 수 있을 때 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="1d05f-141">이 열은 반복성을 위해 Azure Data Factory에서 사용되며 Azure Data Factory가 테이블의 어떠한 스키마도 변경하지 않는 프로세스에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="1d05f-142">이 방식을 사용하는 방법:</span><span class="sxs-lookup"><span data-stu-id="1d05f-142">Way to use this approach:</span></span>

1. <span data-ttu-id="1d05f-143">대상 SQL 테이블에서 **이진 형식(32)**으로 열을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="1d05f-144">이 열에는 제약 조건이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-144">There should be no constraints on this column.</span></span> <span data-ttu-id="1d05f-145">이 예에서는 이 열의 이름을 AdfSliceIdentifier라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="1d05f-146">원본 테이블:</span><span class="sxs-lookup"><span data-stu-id="1d05f-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="1d05f-147">대상 테이블:</span><span class="sxs-lookup"><span data-stu-id="1d05f-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="1d05f-148">복사 작업에서 다음과 같이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="1d05f-149">Azure Data Factory는 원본과 대상의 동기화 상태를 유지하기 위해 필요한 대로 이 열을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="1d05f-150">이 열의 값은 이 컨텍스트 외부에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="1d05f-151">메커니즘 1과 마찬가지로, 복사 작업이 대상 SQL 테이블에서 지정된 조각의 데이터를 자동으로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="1d05f-152">그런 다음 원본의 데이터를 대상 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1d05f-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d05f-153">Next steps</span></span>
<span data-ttu-id="1d05f-154">완전한 JSON 예제에 대한 다음 커넥터 문서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="1d05f-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="1d05f-155">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="1d05f-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="1d05f-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1d05f-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="1d05f-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1d05f-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)