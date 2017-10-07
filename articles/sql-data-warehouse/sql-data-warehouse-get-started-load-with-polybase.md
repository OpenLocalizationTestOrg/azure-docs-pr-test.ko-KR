---
title: "SQL 데이터 웨어하우스 자습서에서 aaaPolyBase | Microsoft Docs"
description: "PolyBase 무엇 인지 알아보고 방법과 toouse 데이터 웨어하우징 시나리오에 대 한 것입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="d310d-103">SQL 데이터 웨어하우스에서 PolyBase를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="d310d-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d310d-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="d310d-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="d310d-105">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="d310d-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="d310d-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d310d-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="d310d-107">BCP</span><span class="sxs-lookup"><span data-stu-id="d310d-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="d310d-108">이 자습서에서는 어떻게 AzCopy 및 PolyBase를 사용 하 여 SQL 데이터 웨어하우스로 tooload 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="d310d-109">자습서를 마치면 다음과 같은 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="d310d-110">AzCopy toocopy 데이터 tooAzure blob 저장소를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d310d-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="d310d-111">데이터베이스 개체 toodefine hello 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="d310d-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="d310d-112">T-SQL 쿼리 tooload hello 데이터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d310d-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d310d-113">Prerequisites</span></span>
<span data-ttu-id="d310d-114">이 자습서를 통해 toostep, 해야</span><span class="sxs-lookup"><span data-stu-id="d310d-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="d310d-115">SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d310d-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="d310d-116">표준 로컬 중복 저장소(표준-LRS), 표준 지역 중복 저장소(표준-GRS) 또는 표준 읽기 액세스 지역 중복 저장소(표준-RAGRS) 유형의 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="d310d-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="d310d-117">AzCopy 명령줄 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="d310d-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="d310d-118">다운로드 및 설치 hello [AzCopy의 최신 버전] [ latest version of AzCopy] hello Microsoft Azure 저장소 도구를 함께 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Azure 저장소 도구](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="d310d-120">1 단계: 추가 샘플 데이터 tooAzure blob 저장소</span><span class="sxs-lookup"><span data-stu-id="d310d-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="d310d-121">주문 tooload 데이터에서 필요 tooput 몇 가지 샘플 데이터를 Azure blob 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="d310d-122">이 단계에서는 Azure Blob 저장소를 샘플 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="d310d-123">나중에 사용 합니다 PolyBase tooload이 예제 데이터를 SQL 데이터 웨어하우스 데이터베이스에.</span><span class="sxs-lookup"><span data-stu-id="d310d-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="d310d-124">A.</span><span class="sxs-lookup"><span data-stu-id="d310d-124">A.</span></span> <span data-ttu-id="d310d-125">샘플 텍스트 파일 준비</span><span class="sxs-lookup"><span data-stu-id="d310d-125">Prepare a sample text file</span></span>
<span data-ttu-id="d310d-126">tooprepare 샘플 텍스트 파일:</span><span class="sxs-lookup"><span data-stu-id="d310d-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="d310d-127">메모장 및 복사 hello 줄의 데이터를 새 파일에 다음을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="d310d-128">%Temp%\DimDate2.txt이 tooyour 로컬 임시 디렉터리를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="d310d-129">B.</span><span class="sxs-lookup"><span data-stu-id="d310d-129">B.</span></span> <span data-ttu-id="d310d-130">Blob 서비스 끝점 찾기</span><span class="sxs-lookup"><span data-stu-id="d310d-130">Find your blob service endpoint</span></span>
<span data-ttu-id="d310d-131">toofind blob 서비스 끝점:</span><span class="sxs-lookup"><span data-stu-id="d310d-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="d310d-132">Hello Azure 포털에서에서 선택 **찾아보기** > **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d310d-133">원하는 toouse hello 저장소 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="d310d-134">Hello 저장소 계정 블레이드에서 Blob를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-134">In hello Storage account blade, click Blobs</span></span>
   
    ![BLOB 클릭](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="d310d-136">나중을 위해 Blob 서비스 끝점 URL을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Blob 서비스 끝점](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="d310d-138">C.</span><span class="sxs-lookup"><span data-stu-id="d310d-138">C.</span></span> <span data-ttu-id="d310d-139">Azure 저장소 키 찾기</span><span class="sxs-lookup"><span data-stu-id="d310d-139">Find your Azure storage key</span></span>
<span data-ttu-id="d310d-140">toofind Azure 저장소 키:</span><span class="sxs-lookup"><span data-stu-id="d310d-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="d310d-141">Hello Azure 포털에서에서 선택 **찾아보기** > **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d310d-142">원하는 toouse hello 저장소 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="d310d-143">**모든 설정** > **선택키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="d310d-144">Hello 복사 상자 toocopy 액세스 키 toohello 클립보드 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Azure 저장소 키 복사](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="d310d-146">D.</span><span class="sxs-lookup"><span data-stu-id="d310d-146">D.</span></span> <span data-ttu-id="d310d-147">Hello 샘플 파일 tooAzure blob 저장소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="d310d-148">toocopy 데이터 tooAzure blob 저장소:</span><span class="sxs-lookup"><span data-stu-id="d310d-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="d310d-149">명령 프롬프트를 열고 디렉터리 toohello AzCopy 설치 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="d310d-150">이 명령은 64 비트 Windows 클라이언트에서 toohello 기본 설치 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="d310d-151">다음 명령은 tooupload hello 파일 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="d310d-152"><blob service endpoint URL>에 Blob service 끝점 URL을 지정하고 <azure_storage_account_key>에 Azure Storage 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="d310d-153">참고 항목 [hello AzCopy 명령줄 유틸리티 시작][Getting Started with hello AzCopy Command-Line Utility]합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="d310d-154">E.</span><span class="sxs-lookup"><span data-stu-id="d310d-154">E.</span></span> <span data-ttu-id="d310d-155">Blob 저장소 컨테이너 탐색</span><span class="sxs-lookup"><span data-stu-id="d310d-155">Explore your blob storage container</span></span>
<span data-ttu-id="d310d-156">tooblob 저장소에 업로드 한 toosee hello 파일:</span><span class="sxs-lookup"><span data-stu-id="d310d-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="d310d-157">Tooyour Blob 서비스 블레이드를 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="d310d-158">컨테이너에서 **datacontainer**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="d310d-159">tooexplore hello 경로 tooyour 데이터 hello 폴더를 클릭 합니다. **datedimension** 업로드 된 파일을 볼 수 있습니다 **DimDate2.txt**합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="d310d-160">tooview 속성 클릭 **DimDate2.txt**합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="d310d-161">Note hello Blob 속성 블레이드에서 수 다운로드 하거나 있는 hello 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Azure 저장소 Blob 보기](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="d310d-163">2 단계: hello 샘플 데이터에 대 한 외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="d310d-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="d310d-164">이 섹션에서는 hello 예제 데이터를 정의 하는 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="d310d-165">PolyBase는 Azure blob 저장소에 외부 테이블 tooaccess 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="d310d-166">SQL 데이터 웨어하우스 내에서 hello 데이터 저장 되지 않으므로 이후 PolyBase 데이터베이스 범위 자격 증명을 사용 하 여 인증 toohello 외부 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="d310d-167">이 단계에서는 hello 예제 이러한 Transact SQL 문 toocreate 외부 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="d310d-168">[마스터 키 (Transact SQL) 만들기] [ Create Master Key (Transact-SQL)] tooencrypt hello 비밀 데이터베이스 범위 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="d310d-169">[데이터베이스 범위 자격 증명 만들기 (Transact SQL)] [ Create Database Scoped Credential (Transact-SQL)] Azure 저장소 계정에 대 한 toospecify 인증 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="d310d-170">[외부 데이터 원본 (Transact SQL) 만들기] [ Create External Data Source (Transact-SQL)] Azure blob 저장소의 toospecify hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="d310d-171">[외부 파일 형식 (Transact SQL) 만들기] [ Create External File Format (Transact-SQL)] toospecify hello 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="d310d-172">[외부 테이블 (Transact SQL) 만들기] [ Create External Table (Transact-SQL)] toospecify hello 테이블 정 및 위치의 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="d310d-173">SQL 데이터 웨어하우스 데이터베이스에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="d310d-174">Hello Azure blob 저장소에 toohello DimDate2.txt 예제 데이터를 가리키는 hello dbo 스키마에서 DimDate2External 라는 외부 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="d310d-175">Visual Studio에서 SQL Server 개체 탐색기에서 hello 외부 파일 형식, 외부 데이터 원본 및 hello DimDate2External 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![외부 테이블 보기](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="d310d-177">3단계: SQL 데이터 웨어하우스에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="d310d-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="d310d-178">Hello 외부 테이블을 만든 후 새 테이블로 hello 데이터를 로드 하거나 기존 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="d310d-179">hello 실행 새 테이블로 tooload hello 데이터 [CREATE TABLE AS SELECT (Transact SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] 문.</span><span class="sxs-lookup"><span data-stu-id="d310d-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="d310d-180">새 테이블 hello hello 쿼리에서 명명 된 hello 열이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="d310d-181">hello 열의 데이터 형식을 hello hello 외부 테이블 정의에 hello 데이터 형식과 일치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="d310d-182">tooload hello 데이터를 기존 테이블에 사용 하 여 hello [삽입... 선택 (Transact SQL)] [ INSERT...SELECT (Transact-SQL)] 문.</span><span class="sxs-lookup"><span data-stu-id="d310d-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="d310d-183">4단계: 새로 로드한 데이터에 대한 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="d310d-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="d310d-184">SQL 데이터 웨어하우스는 통계 자동 만들기 또는 자동 업데이트를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="d310d-185">따라서 tooachieve 쿼리 성능이 반드시 toocreate 통계 hello 후 각 테이블의 각 열에 먼저 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="d310d-186">것도 중요 한 tooupdate 통계 후 hello 데이터의 주요 부분을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="d310d-187">이 예제는 hello 새 DimDate2 테이블에 단일 열 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="d310d-188">toolearn 더 참조 [통계][Statistics]합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d310d-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d310d-189">Next steps</span></span>
<span data-ttu-id="d310d-190">Hello 참조 [PolyBase 가이드] [ PolyBase guide] 대 한 자세한 내용은 PolyBase를 사용 하는 솔루션을 개발할 때 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d310d-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
