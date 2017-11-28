---
title: "Azure Blob에서 Azure 데이터 웨어하우스로 로드 | Microsoft Docs"
description: "PolyBase를 사용하여 Azure blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 로드하는 방법을 알아봅니다. 몇 개의 테이블을 공용 데이터에서 Contoso 소매 데이터 웨어하우스 스키마로 로드합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="6eba4-104">Azure blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 로드합니다(PolyBase).</span><span class="sxs-lookup"><span data-stu-id="6eba4-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6eba4-105">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="6eba4-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="6eba4-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="6eba4-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="6eba4-107">Azure Blob 저장소에서 Azure SQL 데이터 웨어하우스로 데이터 로드하기 위해 PolyBase와 T-SQL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="6eba4-108">간단히 말하자면, 이 자습서는 공용 Azure 저장소 Blob에서 두 테이블을 Contoso 소매 데이터 웨어하우스 스키마로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="6eba4-109">전체 데이터 집합을 로드하려면 Microsoft SQL Server 샘플 리포지토리에서 예제 [전체 Contoso 소매 데이터 웨어하우스 로드하기][Load the full Contoso Retail Data Warehouse]를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="6eba4-110">이 자습서에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="6eba4-111">Azure blob 저장소에서 로드하기 위한 PolyBase 구성</span><span class="sxs-lookup"><span data-stu-id="6eba4-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="6eba4-112">공용 데이터를 데이터베이스에 로드</span><span class="sxs-lookup"><span data-stu-id="6eba4-112">Load public data into your database</span></span>
3. <span data-ttu-id="6eba4-113">로드가 완료 된 후에 최적화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6eba4-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6eba4-114">Before you begin</span></span>
<span data-ttu-id="6eba4-115">이 자습서를 실행하려면 SQL 데이터 웨어하우스 데이터베이스를 이미 가지고 있는 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="6eba4-116">계정이 아직 없다면 [SQL Data Warehouse 만들기][Create a SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eba4-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="6eba4-117">1. 데이터 원본 구성</span><span class="sxs-lookup"><span data-stu-id="6eba4-117">1. Configure the data source</span></span>
<span data-ttu-id="6eba4-118">PolyBase는 T-SQL 외부 개체를 사용하여 외부 데이터의 위치와 특성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="6eba4-119">외부 개체의 정의는 SQL 데이터 웨어하우스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="6eba4-120">데이터 자체는 외부에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="6eba4-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="6eba4-121">1.1.</span></span> <span data-ttu-id="6eba4-122">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="6eba4-122">Create a credential</span></span>
<span data-ttu-id="6eba4-123">**이 단계를 건너뜁니다** .</span><span class="sxs-lookup"><span data-stu-id="6eba4-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="6eba4-124">공용 데이터는 누구나 액세스할 수 있으므로 보안 액세스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="6eba4-125">**이 단계를 건너뛰지 마십시오** .</span><span class="sxs-lookup"><span data-stu-id="6eba4-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="6eba4-126">자격 증명을 통해 액세스하려면 다음 스크립트를 사용해 데이터베이스 범위 자격 증명을 생성하고 데이터 원본의 위치를 정의할 때 이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="6eba4-127">2단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="6eba4-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="6eba4-128">1.2.</span></span> <span data-ttu-id="6eba4-129">외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="6eba4-129">Create the external data source</span></span>
<span data-ttu-id="6eba4-130">이 [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] 명령을 사용하여 데이터의 위치와 데이터의 형식을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="6eba4-131">Azure blob 저장소 컨테이너를 공용으로 만들도록 선택하는 경우 데이터가 데이터 센터에서 떠날 때 데이터 소유자로서 귀하에게 데이터 송신 요금이 부과될 것임을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="6eba4-132">2. 데이터 형식 구성</span><span class="sxs-lookup"><span data-stu-id="6eba4-132">2. Configure data format</span></span>
<span data-ttu-id="6eba4-133">데이터는 Azure blob 저장소에 텍스트 파일로 저장되고 각 필드는 구분 기호로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="6eba4-134">이 [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] 명령을 실행하여 텍스트 파일로 된 데이터의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="6eba4-135">Contoso 데이터는 압축되어 있지 않으며 파이프로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-135">The Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-the-external-tables"></a><span data-ttu-id="6eba4-136">3. 외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="6eba4-136">3. Create the external tables</span></span>
<span data-ttu-id="6eba4-137">이제 데이터 원본과 파일 형식을 지정했으니 외부 테이블을 만들 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="6eba4-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="6eba4-138">3.1.</span></span> <span data-ttu-id="6eba4-139">데이터에 대한 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-139">Create a schema for the data.</span></span>
<span data-ttu-id="6eba4-140">데이터베이스에 Contoso 데이터를 저장할 수 있는 위치를 만들려면 스키마를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="6eba4-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="6eba4-141">3.2.</span></span> <span data-ttu-id="6eba4-142">외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-142">Create the external tables.</span></span>
<span data-ttu-id="6eba4-143">DimProduct와 FactOnlineSales 외부 테이블을 만들려면 이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="6eba4-144">여기에서는 열 이름과 데이터 형식을 정의하고 이들을 Azure blob 저장소 파일의 위치와 형식에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="6eba4-145">정의는 SQL 데이터 웨어하우스에 저장되고 데이터는 여전히 Azure 저장소 Blob에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="6eba4-146">**위치** 매개 변수는 Azure Storage Blob의 루트 폴더 아래에 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="6eba4-147">각 테이블은 서로 다른 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-the-data"></a><span data-ttu-id="6eba4-148">4. 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="6eba4-148">4. Load the data</span></span>
<span data-ttu-id="6eba4-149">외부 데이터에 액세스하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-149">There's different ways to access external data.</span></span>  <span data-ttu-id="6eba4-150">외부 테이블에서 직접 쿼리할 수 있고 새 데이터베이스로 데이터를 로드하거나 기존 데이터베이스 테이블에 외부 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="6eba4-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="6eba4-151">4.1.</span></span> <span data-ttu-id="6eba4-152">새 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-152">Create a new schema</span></span>
<span data-ttu-id="6eba4-153">CTAS는 데이터가 포함된 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="6eba4-154">먼저 contoso 데이터에 대한 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="6eba4-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="6eba4-155">4.2.</span></span> <span data-ttu-id="6eba4-156">데이터를 새 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-156">Load the data into new tables</span></span>
<span data-ttu-id="6eba4-157">Azure Blob Storage에서 데이터를 로드하여 데이터베이스 내부의 테이블에 저장하려면 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="6eba4-158">CTAS를 사용하여 로드하면 방금 생성한 강력한 형식의 외부 테이블이 활용됩니다. 새 테이블에 데이터를 로드하려면 테이블당 하나의 [CTAS][CTAS] 문을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6eba4-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="6eba4-159">CTAS는 새 테이블을 만들고 select 문의 결과와 함께 새 테이블을 정보표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="6eba4-160">CTAS는 select 문의 결과에 부합하는 동일한 열과 데이터 형식을 가지도록 새 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="6eba4-161">외부 테이블에서 모든 열을 선택하는 경우 새 테이블은 외부 테이블의 열과 데이터 형식의 복제본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="6eba4-162">이 예제에서는 차원과 해시 분산 테이블로서 팩트 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="6eba4-163">4.3 로드 진행률 추적</span><span class="sxs-lookup"><span data-stu-id="6eba4-163">4.3 Track the load progress</span></span>
<span data-ttu-id="6eba4-164">DMV(동적 관리 뷰)를 사용하여 로드 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="6eba4-165">5. Columnstore 압축을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="6eba4-166">기본적으로 SQL 데이터 웨어하우스는 클러스터형 columnstore 인덱스로 테이블을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="6eba4-167">로드를 완료한 후 데이터 행 일부는 columnstore로 압축되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="6eba4-168">여기에는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="6eba4-169">자세한 내용은 [Columnstore 인덱스 관리][manage columnstore indexes]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eba4-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="6eba4-170">로드 후 쿼리 성능과 columnstore 압축을 최적화하려면 모든 행을 압축하기 위해 columnstore 인덱스를 강제 적용할 테이블을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="6eba4-171">Columnstore 인덱스 유지 관리에 대한 자세한 내용은 [Columnstore 인덱스 관리][manage columnstore indexes] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eba4-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="6eba4-172">6. 통계를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-172">6. Optimize statistics</span></span>
<span data-ttu-id="6eba4-173">로드 직후 단일 열 통계를 만드는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="6eba4-174">통계에 대한 몇 가지 선택 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-174">There are some choices for statistics.</span></span> <span data-ttu-id="6eba4-175">예를 들어 모든 열에 단일 열 통계를 만드는 경우 모든 통계를 다시 작성하는 데 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="6eba4-176">쿼리 조건자에 위치하지 않을 특정 열에 대해 알고 있다면 이들 열에 대한 통계 생성 과정은 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="6eba4-177">단일 열 통계를 모든 테이블의 모든 열에 대해 만들기로 결정한 경우 [통계][statistics] 문서에 저장된 프로시저 코드 샘플 `prc_sqldw_create_stats`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="6eba4-178">다음 예제는 통계를 만들기 위한 좋은 출발점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="6eba4-179">차원 테이블의 각 열과 팩트 테이블의 각 조인 열의 단일 열 통계를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="6eba4-180">이후 언제라도 다른 팩트 테이블 열에 단일 또는 여러 열 통계를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="6eba4-181">목표를 달성했습니다!</span><span class="sxs-lookup"><span data-stu-id="6eba4-181">Achievement unlocked!</span></span>
<span data-ttu-id="6eba4-182">이제 Azure SQL 데이터 웨어하우스에 공용 데이터를 성공적으로 로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="6eba4-183">잘 하셨습니다!</span><span class="sxs-lookup"><span data-stu-id="6eba4-183">Great job!</span></span>

<span data-ttu-id="6eba4-184">다음과 같은 쿼리를 사용하여 테이블 쿼리를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eba4-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="6eba4-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6eba4-185">Next steps</span></span>
<span data-ttu-id="6eba4-186">전체 Contoso 소매 데이터 웨어하우스 데이터를 로드하려면 더 많은 개발 팁(For more development tips)의 스크립트를 사용하고 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eba4-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
