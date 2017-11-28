---
title: "CSV에서 aaaLoad 데이터 파일을 Azure SQL 데이터베이스로 (bcp) | Microsoft Docs"
description: "작은 데이터 크기에 대 한 Azure SQL 데이터베이스에 bcp tooimport 데이터를 사용합니다."
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="9f845-103">CSV에서 Azure SQL Database(플랫 파일)로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9f845-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="9f845-104">Azure SQL 데이터베이스로 hello bcp 명령줄 유틸리티 tooimport 데이터 CSV 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f845-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9f845-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="9f845-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9f845-106">Prerequisites</span></span>
<span data-ttu-id="9f845-107">이 문서의 단계를 toocomplete hello 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="9f845-108">Azure SQL 데이터베이스 논리 서버 및 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="9f845-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="9f845-109">hello bcp 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="9f845-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="9f845-110">hello sqlcmd 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="9f845-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="9f845-111">Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="9f845-112">ASCII 또는 UTF-16 형식 데이터</span><span class="sxs-lookup"><span data-stu-id="9f845-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="9f845-113">이 자습서에서는 사용자 고유의 데이터로 시도 하는 경우 데이터 toouse hello ASCII 또는 utf-16 인코딩 bcp u t F-8을 지원 하지 않으므로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="9f845-114">1. 대상 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="9f845-114">1. Create a destination table</span></span>
<span data-ttu-id="9f845-115">SQL 데이터베이스의 hello 대상 테이블로 테이블을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="9f845-116">hello 테이블의 hello 열에는 데이터 파일의 각 행에 toohello 데이터 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="9f845-117">toocreate 테이블을 명령 프롬프트를 열고 sqlcmd.exe toorun hello 다음 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="9f845-118">2. 원본 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9f845-118">2. Create a source data file</span></span>
<span data-ttu-id="9f845-119">새 텍스트 파일에 줄의 데이터로 다음 메모장 및 복사 hello 열고이 파일 tooyour 로컬 임시 디렉터리 C:\Temp\DimDate2.txt를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="9f845-120">이 데이터는 ASCII 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="9f845-121">(선택 사항) tooexport SQL Server 데이터베이스에서 사용자 고유의 데이터는 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="9f845-122">TableName, ServerName, DatabaseName, Username 및 Password를 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="9f845-123">3. Hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9f845-123">3. Load hello data</span></span>
<span data-ttu-id="9f845-124">tooload hello 데이터 명령 프롬프트를 열고 다음 명령을, hello 값을 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호에 대 한 사용자의 정보로 대체 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="9f845-125">이 명령은 tooverify hello 데이터가 제대로 로드 사용</span><span class="sxs-lookup"><span data-stu-id="9f845-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="9f845-126">hello 결과 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-126">hello results should look like this:</span></span>

| <span data-ttu-id="9f845-127">DateId</span><span class="sxs-lookup"><span data-stu-id="9f845-127">DateId</span></span> | <span data-ttu-id="9f845-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="9f845-128">CalendarQuarter</span></span> | <span data-ttu-id="9f845-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="9f845-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f845-130">20150101</span><span class="sxs-lookup"><span data-stu-id="9f845-130">20150101</span></span> |<span data-ttu-id="9f845-131">1</span><span class="sxs-lookup"><span data-stu-id="9f845-131">1</span></span> |<span data-ttu-id="9f845-132">3</span><span class="sxs-lookup"><span data-stu-id="9f845-132">3</span></span> |
| <span data-ttu-id="9f845-133">20150201</span><span class="sxs-lookup"><span data-stu-id="9f845-133">20150201</span></span> |<span data-ttu-id="9f845-134">1</span><span class="sxs-lookup"><span data-stu-id="9f845-134">1</span></span> |<span data-ttu-id="9f845-135">3</span><span class="sxs-lookup"><span data-stu-id="9f845-135">3</span></span> |
| <span data-ttu-id="9f845-136">20150301</span><span class="sxs-lookup"><span data-stu-id="9f845-136">20150301</span></span> |<span data-ttu-id="9f845-137">1</span><span class="sxs-lookup"><span data-stu-id="9f845-137">1</span></span> |<span data-ttu-id="9f845-138">3</span><span class="sxs-lookup"><span data-stu-id="9f845-138">3</span></span> |
| <span data-ttu-id="9f845-139">20150401</span><span class="sxs-lookup"><span data-stu-id="9f845-139">20150401</span></span> |<span data-ttu-id="9f845-140">2</span><span class="sxs-lookup"><span data-stu-id="9f845-140">2</span></span> |<span data-ttu-id="9f845-141">4</span><span class="sxs-lookup"><span data-stu-id="9f845-141">4</span></span> |
| <span data-ttu-id="9f845-142">20150501</span><span class="sxs-lookup"><span data-stu-id="9f845-142">20150501</span></span> |<span data-ttu-id="9f845-143">2</span><span class="sxs-lookup"><span data-stu-id="9f845-143">2</span></span> |<span data-ttu-id="9f845-144">4</span><span class="sxs-lookup"><span data-stu-id="9f845-144">4</span></span> |
| <span data-ttu-id="9f845-145">20150601</span><span class="sxs-lookup"><span data-stu-id="9f845-145">20150601</span></span> |<span data-ttu-id="9f845-146">2</span><span class="sxs-lookup"><span data-stu-id="9f845-146">2</span></span> |<span data-ttu-id="9f845-147">4</span><span class="sxs-lookup"><span data-stu-id="9f845-147">4</span></span> |
| <span data-ttu-id="9f845-148">20150701</span><span class="sxs-lookup"><span data-stu-id="9f845-148">20150701</span></span> |<span data-ttu-id="9f845-149">3</span><span class="sxs-lookup"><span data-stu-id="9f845-149">3</span></span> |<span data-ttu-id="9f845-150">1</span><span class="sxs-lookup"><span data-stu-id="9f845-150">1</span></span> |
| <span data-ttu-id="9f845-151">20150801</span><span class="sxs-lookup"><span data-stu-id="9f845-151">20150801</span></span> |<span data-ttu-id="9f845-152">3</span><span class="sxs-lookup"><span data-stu-id="9f845-152">3</span></span> |<span data-ttu-id="9f845-153">1</span><span class="sxs-lookup"><span data-stu-id="9f845-153">1</span></span> |
| <span data-ttu-id="9f845-154">20150801</span><span class="sxs-lookup"><span data-stu-id="9f845-154">20150801</span></span> |<span data-ttu-id="9f845-155">3</span><span class="sxs-lookup"><span data-stu-id="9f845-155">3</span></span> |<span data-ttu-id="9f845-156">1</span><span class="sxs-lookup"><span data-stu-id="9f845-156">1</span></span> |
| <span data-ttu-id="9f845-157">20151001</span><span class="sxs-lookup"><span data-stu-id="9f845-157">20151001</span></span> |<span data-ttu-id="9f845-158">4</span><span class="sxs-lookup"><span data-stu-id="9f845-158">4</span></span> |<span data-ttu-id="9f845-159">2</span><span class="sxs-lookup"><span data-stu-id="9f845-159">2</span></span> |
| <span data-ttu-id="9f845-160">20151101</span><span class="sxs-lookup"><span data-stu-id="9f845-160">20151101</span></span> |<span data-ttu-id="9f845-161">4</span><span class="sxs-lookup"><span data-stu-id="9f845-161">4</span></span> |<span data-ttu-id="9f845-162">2</span><span class="sxs-lookup"><span data-stu-id="9f845-162">2</span></span> |
| <span data-ttu-id="9f845-163">20151201</span><span class="sxs-lookup"><span data-stu-id="9f845-163">20151201</span></span> |<span data-ttu-id="9f845-164">4</span><span class="sxs-lookup"><span data-stu-id="9f845-164">4</span></span> |<span data-ttu-id="9f845-165">2</span><span class="sxs-lookup"><span data-stu-id="9f845-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f845-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f845-166">Next steps</span></span>
<span data-ttu-id="9f845-167">SQL Server 데이터베이스 toomigrate 참조 [SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f845-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
