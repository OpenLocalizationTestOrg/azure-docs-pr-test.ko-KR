---
title: "CSV 파일에서 Azure SQL Database로 데이터 로드(bcp) | Microsoft Docs"
description: "작은 데이터 크기의 경우 bcp를 사용하여 Azure SQL 데이터베이스로 데이터를 가져옵니다."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="4a979-103">CSV에서 Azure SQL Database(플랫 파일)로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="4a979-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="4a979-104">bcp 명령줄 유틸리티를 사용하여 CSV 파일에서 Azure SQL 데이터베이스로 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4a979-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4a979-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="4a979-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4a979-106">Prerequisites</span></span>
<span data-ttu-id="4a979-107">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-107">To complete the steps in this article, you need:</span></span>

* <span data-ttu-id="4a979-108">Azure SQL 데이터베이스 논리 서버 및 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4a979-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="4a979-109">설치된 bcp 명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="4a979-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="4a979-110">설치된 sqlcmd 명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="4a979-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="4a979-111">[Microsoft 다운로드 센터][Microsoft Download Center]에서 bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="4a979-112">ASCII 또는 UTF-16 형식 데이터</span><span class="sxs-lookup"><span data-stu-id="4a979-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="4a979-113">사용자의 데이터로 이 자습서를 수행하는 경우에는, bcp가 UTF-8을 지원하지 않으므로, 데이터에 ASCII 또는 UTF-16 인코딩을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="4a979-114">1. 대상 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="4a979-114">1. Create a destination table</span></span>
<span data-ttu-id="4a979-115">SQL Database에서 테이블을 대상 테이블로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="4a979-116">테이블의 열은 데이터 파일의 각 행에 있는 데이터와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="4a979-117">테이블을 만들려면, 명령 프롬프트를 열고 sqlcmd.exe를 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="4a979-118">2. 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="4a979-118">2. Create a source data file</span></span>
<span data-ttu-id="4a979-119">메모장을 열고 다음 데이터 줄을 새 텍스트 파일에 복사한 다음 이 파일을 로컬 임시 디렉터리 C:\Temp\DimDate2.txt에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="4a979-120">이 데이터는 ASCII 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-120">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="4a979-121">(선택 사항) SQL Server 데이터베이스에서 사용자의 데이터를 내보내려면, 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="4a979-122">TableName, ServerName, DatabaseName, Username 및 Password를 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a><span data-ttu-id="4a979-123">3. 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="4a979-123">3. Load the data</span></span>
<span data-ttu-id="4a979-124">데이터를 로드하려면, 명령 프롬프트를 열고 Server Name, Database name, Username 및 Password 값을 사용자의 정보로 바꿔서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="4a979-125">이 명령을 사용하여 데이터가 제대로 로드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-125">Use this command to verify the data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="4a979-126">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a979-126">The results should look like this:</span></span>

| <span data-ttu-id="4a979-127">DateId</span><span class="sxs-lookup"><span data-stu-id="4a979-127">DateId</span></span> | <span data-ttu-id="4a979-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="4a979-128">CalendarQuarter</span></span> | <span data-ttu-id="4a979-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="4a979-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a979-130">20150101</span><span class="sxs-lookup"><span data-stu-id="4a979-130">20150101</span></span> |<span data-ttu-id="4a979-131">1</span><span class="sxs-lookup"><span data-stu-id="4a979-131">1</span></span> |<span data-ttu-id="4a979-132">3</span><span class="sxs-lookup"><span data-stu-id="4a979-132">3</span></span> |
| <span data-ttu-id="4a979-133">20150201</span><span class="sxs-lookup"><span data-stu-id="4a979-133">20150201</span></span> |<span data-ttu-id="4a979-134">1</span><span class="sxs-lookup"><span data-stu-id="4a979-134">1</span></span> |<span data-ttu-id="4a979-135">3</span><span class="sxs-lookup"><span data-stu-id="4a979-135">3</span></span> |
| <span data-ttu-id="4a979-136">20150301</span><span class="sxs-lookup"><span data-stu-id="4a979-136">20150301</span></span> |<span data-ttu-id="4a979-137">1</span><span class="sxs-lookup"><span data-stu-id="4a979-137">1</span></span> |<span data-ttu-id="4a979-138">3</span><span class="sxs-lookup"><span data-stu-id="4a979-138">3</span></span> |
| <span data-ttu-id="4a979-139">20150401</span><span class="sxs-lookup"><span data-stu-id="4a979-139">20150401</span></span> |<span data-ttu-id="4a979-140">2</span><span class="sxs-lookup"><span data-stu-id="4a979-140">2</span></span> |<span data-ttu-id="4a979-141">4</span><span class="sxs-lookup"><span data-stu-id="4a979-141">4</span></span> |
| <span data-ttu-id="4a979-142">20150501</span><span class="sxs-lookup"><span data-stu-id="4a979-142">20150501</span></span> |<span data-ttu-id="4a979-143">2</span><span class="sxs-lookup"><span data-stu-id="4a979-143">2</span></span> |<span data-ttu-id="4a979-144">4</span><span class="sxs-lookup"><span data-stu-id="4a979-144">4</span></span> |
| <span data-ttu-id="4a979-145">20150601</span><span class="sxs-lookup"><span data-stu-id="4a979-145">20150601</span></span> |<span data-ttu-id="4a979-146">2</span><span class="sxs-lookup"><span data-stu-id="4a979-146">2</span></span> |<span data-ttu-id="4a979-147">4</span><span class="sxs-lookup"><span data-stu-id="4a979-147">4</span></span> |
| <span data-ttu-id="4a979-148">20150701</span><span class="sxs-lookup"><span data-stu-id="4a979-148">20150701</span></span> |<span data-ttu-id="4a979-149">3</span><span class="sxs-lookup"><span data-stu-id="4a979-149">3</span></span> |<span data-ttu-id="4a979-150">1</span><span class="sxs-lookup"><span data-stu-id="4a979-150">1</span></span> |
| <span data-ttu-id="4a979-151">20150801</span><span class="sxs-lookup"><span data-stu-id="4a979-151">20150801</span></span> |<span data-ttu-id="4a979-152">3</span><span class="sxs-lookup"><span data-stu-id="4a979-152">3</span></span> |<span data-ttu-id="4a979-153">1</span><span class="sxs-lookup"><span data-stu-id="4a979-153">1</span></span> |
| <span data-ttu-id="4a979-154">20150801</span><span class="sxs-lookup"><span data-stu-id="4a979-154">20150801</span></span> |<span data-ttu-id="4a979-155">3</span><span class="sxs-lookup"><span data-stu-id="4a979-155">3</span></span> |<span data-ttu-id="4a979-156">1</span><span class="sxs-lookup"><span data-stu-id="4a979-156">1</span></span> |
| <span data-ttu-id="4a979-157">20151001</span><span class="sxs-lookup"><span data-stu-id="4a979-157">20151001</span></span> |<span data-ttu-id="4a979-158">4</span><span class="sxs-lookup"><span data-stu-id="4a979-158">4</span></span> |<span data-ttu-id="4a979-159">2</span><span class="sxs-lookup"><span data-stu-id="4a979-159">2</span></span> |
| <span data-ttu-id="4a979-160">20151101</span><span class="sxs-lookup"><span data-stu-id="4a979-160">20151101</span></span> |<span data-ttu-id="4a979-161">4</span><span class="sxs-lookup"><span data-stu-id="4a979-161">4</span></span> |<span data-ttu-id="4a979-162">2</span><span class="sxs-lookup"><span data-stu-id="4a979-162">2</span></span> |
| <span data-ttu-id="4a979-163">20151201</span><span class="sxs-lookup"><span data-stu-id="4a979-163">20151201</span></span> |<span data-ttu-id="4a979-164">4</span><span class="sxs-lookup"><span data-stu-id="4a979-164">4</span></span> |<span data-ttu-id="4a979-165">2</span><span class="sxs-lookup"><span data-stu-id="4a979-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4a979-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a979-166">Next steps</span></span>
<span data-ttu-id="4a979-167">SQL Server 데이터베이스를 마이그레이션하려면 [SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a979-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
