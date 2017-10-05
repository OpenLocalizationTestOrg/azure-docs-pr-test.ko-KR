---
title: "로드 - Azure Data Lake Store에서 SQL Data Warehouse로| Microsoft Docs"
description: "PolyBase 외부 테이블을 사용하여 Azure Data Lake Store에서 Azure SQL Data Warehouse로 데이터를 로드하는 방법에 대해 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: ab951c30aae0d4afdd931e245f25d4645bba1681
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="3865b-103">Azure Data Lake Store에서 SQL Data Warehouse로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="3865b-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="3865b-104">이 문서는 PolyBase를 사용하여 ADLS(Azure Data Lake Store)에서 SQL Data Warehouse로 데이터를 로드하는 데 필요한 모든 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-104">This document gives you all steps you  need to load your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="3865b-105">외부 테이블을 사용하여 ADLS에 저장된 데이터에 대해 임시 쿼리를 실행할 수 있는 동안 모범 사례로 SQL Data Warehouse로 데이터를 가져오는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-105">While you are able to run adhoc queries over the data stored in ADLS using the External Tables, as a best practice we suggest importing the data into the SQL Data Warehouse.</span></span>
<span data-ttu-id="3865b-106">예상 시간: 완료해야 하는 필수 구성 요소를 가지고 있다고 가정하는 10분.</span><span class="sxs-lookup"><span data-stu-id="3865b-106">Time Estimate: 10 minutes assuming you have the prerequisites need to complete.</span></span>
<span data-ttu-id="3865b-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="3865b-108">외부 데이터베이스 개체를 만들어 Azure Data Lake Store에서 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-108">Create External Database objects to load from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="3865b-109">Azure Data Lake Store 디렉터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-109">Connect to an Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="3865b-110">Azure SQL Data Warehouse에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3865b-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="3865b-111">Before you begin</span></span>
<span data-ttu-id="3865b-112">이 자습서를 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-112">To run this tutorial, you need:</span></span>

* <span data-ttu-id="3865b-113">서비스 간 인증에 사용할 Azure Active Directory 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="3865b-113">Azure Active Directory Application to use for Service-to-Service authentication.</span></span> <span data-ttu-id="3865b-114">만들려면 [Active Directory 인증](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-114">To create, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="3865b-115">SQL Data Warehouse에서 Azure Data Lake에 연결하려면 클라이언트 ID, 키 및 Active Directory 응용 프로그램의 OAuth2.0 토큰 끝점 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-115">You need the client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application to connect to your Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="3865b-116">이러한 값을 가져오는 방법에 대한 세부 정보는 위의 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-116">Details for how to get these values are in the link above.</span></span>
><span data-ttu-id="3865b-117">Azure Active Directory 앱 등록의 경우 '응용 프로그램 ID'를 클라이언트 ID로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-117">Note for Azure Active Directory App Registration use the 'Application ID' as the Client ID.</span></span>

* <span data-ttu-id="3865b-118">SQL Server Management Studio 또는 SQL Server Data Tools, SSMS를 다운로드하고 연결하려면 [SSMS 쿼리](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3865b-118">SQL Server Management Studio or SQL Server Data Tools, to download SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="3865b-119">Azure SQL Data Warehouse, 만들려면 https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-119">An Azure SQL Data Warehouse, to create one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="3865b-120">Azure Data Lake Store, 암호화를 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="3865b-121">만들려면 https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-121">To create one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-the-data-source"></a><span data-ttu-id="3865b-122">데이터 원본 구성</span><span class="sxs-lookup"><span data-stu-id="3865b-122">Configure the data source</span></span>
<span data-ttu-id="3865b-123">PolyBase는 T-SQL 외부 개체를 사용하여 외부 데이터의 위치와 특성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-123">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="3865b-124">외부 개체는 SQL Data Warehouse 및 참조에 저장되고 데이터 th는 외부에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-124">The external objects are stored in SQL Data Warehouse and reference the data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="3865b-125">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="3865b-125">Create a credential</span></span>
<span data-ttu-id="3865b-126">Azure Data Lake Store에 액세스하려면 다음 단계에서 사용되는 자격 증명 암호를 암호화하는 데이터베이스 마스터 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-126">To access your Azure Data Lake Store, you will need to create a Database Master Key to encrypt your credential secret used in the next step.</span></span>
<span data-ttu-id="3865b-127">그런 다음 AAD에 서비스 주체 자격 증명 설정을 저장하는 데이터베이스 범위 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-127">You then create a Database scoped credential, which stores the service principal credentials set up in AAD.</span></span> <span data-ttu-id="3865b-128">Miscrosoft Azure Storage Blob에 연결하는 데 PolyBase를 사용한 사용자의 경우 자격 증명 구문은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-128">For those of you who have used PolyBase to connect to Windows Azure Storage Blobs, note that the credential syntax is different.</span></span>
<span data-ttu-id="3865b-129">Azure Data Lake Store에 연결하려면 **먼저** Azure Active Directory 응용 프로그램을 만들고, 액세스 키를 만들고, Azure Data Lake 리소스에 대한 액세스 권한을 응용 프로그램에 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-129">To connect to Azure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant the application access to the Azure Data Lake resource.</span></span> <span data-ttu-id="3865b-130">이러한 단계를 수행하기 위한 지침은 [여기](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-130">Instrucitons to perform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-the-external-data-source"></a><span data-ttu-id="3865b-131">외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="3865b-131">Create the external data source</span></span>
<span data-ttu-id="3865b-132">이 [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] 명령을 사용하여 데이터의 위치와 데이터의 형식을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span>
<span data-ttu-id="3865b-133">Azure Portal 및 www.portal.azure.com에서 ADL URI를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-133">You can find the ADL URI in the Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="3865b-134">데이터 형식 구성</span><span class="sxs-lookup"><span data-stu-id="3865b-134">Configure data format</span></span>
<span data-ttu-id="3865b-135">ADLS에서 데이터를 가져오려면 외부 파일 형식을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-135">To import the data from ADLS, you need to specify the external file format.</span></span> <span data-ttu-id="3865b-136">이 명령에는 데이터를 설명하는 특정 형식 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-136">This command has format-specific options to describe your data.</span></span>
<span data-ttu-id="3865b-137">다음은 파이프로 구분된 텍스트 파일인 자주 사용되는 파일 형식의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="3865b-138">[외부 파일 형식 만들기][CREATE EXTERNAL FILE FORMAT]의 전체 목록은 T-SQL 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3865b-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-the-external-tables"></a><span data-ttu-id="3865b-139">외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="3865b-139">Create the external tables</span></span>
<span data-ttu-id="3865b-140">이제 데이터 원본과 파일 형식을 지정했으니 외부 테이블을 만들 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-140">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> <span data-ttu-id="3865b-141">외부 테이블은 외부 데이터와 상호 작용하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="3865b-142">PolyBase는 재귀 디렉터리 탐색을 사용하여 location 매개 변수에서 지정한 디렉터리의 모든 하위 디렉터리에서 모든 파일을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-142">PolyBase uses recursive directory traversal to read all files in all subdirectories of the directory specified in the location parameter.</span></span> <span data-ttu-id="3865b-143">또한 다음 예제에서는 개체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-143">Also, the following example shows how to create the object.</span></span> <span data-ttu-id="3865b-144">ADLS에 있는 데이터로 작업하려면 문을 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-144">You need to customize the statement to work with the data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="3865b-145">외부 테이블 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3865b-145">External Table Considerations</span></span>
<span data-ttu-id="3865b-146">외부 테이블을 생성하는 것은 쉽지만 논의되어야 하는 몇 가지 미묘한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-146">Creating an external table is easy, but there are some nuances that need to be discussed.</span></span>

<span data-ttu-id="3865b-147">PolyBase를 사용하는 데이터 로드는 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="3865b-148">즉, 수집되는 데이터의 각 행은 테이블 스키마 정의를 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-148">This means that each row of the data being ingested must satisfy the table schema definition.</span></span>
<span data-ttu-id="3865b-149">지정된 행이 스키마 정의와 일치하지 않는 경우 행은 로드에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-149">If a given row does not match the schema definition, the row is rejected from the load.</span></span>

<span data-ttu-id="3865b-150">REJECT_TYPE 및 REJECT_VALUE 옵션을 사용하면 최종 테이블에 있어야 하는 행 수 또는 데이터의 비율을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-150">The REJECT_TYPE and REJECT_VALUE options allow you to define how many rows or what percentage of the data must be present in the final table.</span></span>
<span data-ttu-id="3865b-151">로드 중 거부 값에 도달하는 경우 로드는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-151">During load, if the reject value is reached, the load fails.</span></span> <span data-ttu-id="3865b-152">거부된 행의 가장 일반적인 원인은 스키마 정의 불일치입니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-152">The most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="3865b-153">예를 들어 파일의 데이터가 문자열일 때 열이 int의 스키마로 잘못 지정된 경우 모든 행을 로드하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-153">For example, if a column is incorrectly given the schema of int when the data in the file is a string, every row will fail to load.</span></span>

<span data-ttu-id="3865b-154">위치는 데이터를 읽으려는 맨 위에 있는 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-154">The Location specifies the topmost directory that you want to read data from.</span></span>
<span data-ttu-id="3865b-155">이 경우 /DimProduct/ 아래에 하위 디렉터리가 있으면 PolyBase는 하위 디렉터리 내의 모든 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all the data within the subdirectories.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="3865b-156">데이터 로드</span><span class="sxs-lookup"><span data-stu-id="3865b-156">Load the data</span></span>
<span data-ttu-id="3865b-157">Azure Data Lake Store에서 데이터를 로드하려면 [CREATE TABLE AS SELECT(Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-157">To load data from Azure Data Lake Store use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="3865b-158">CTAS로 로드는 사용자가 만든 강력한 형식의 외부 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-158">Loading with CTAS uses the strongly typed external table you have created.</span></span>

<span data-ttu-id="3865b-159">CTAS는 새 테이블을 만들고 select 문의 결과와 함께 새 테이블을 정보표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="3865b-160">CTAS는 select 문의 결과에 부합하는 동일한 열과 데이터 형식을 가지도록 새 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="3865b-161">외부 테이블에서 모든 열을 선택하는 경우 새 테이블은 외부 테이블의 열과 데이터 형식의 복제본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-161">If you select all the columns from an external table, the new table is a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="3865b-162">이 예제에서는 외부 테이블 DimProduct_external에서 DimProduct라는 해시 분산 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="3865b-163">Columnstore 압축을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-163">Optimize columnstore compression</span></span>
<span data-ttu-id="3865b-164">기본적으로 SQL 데이터 웨어하우스는 클러스터형 columnstore 인덱스로 테이블을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-164">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="3865b-165">로드를 완료한 후 데이터 행 일부는 columnstore로 압축되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-165">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="3865b-166">여기에는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="3865b-167">자세한 내용은 [Columnstore 인덱스 관리][manage columnstore indexes]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3865b-167">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="3865b-168">로드 후 쿼리 성능과 columnstore 압축을 최적화하려면 모든 행을 압축하기 위해 columnstore 인덱스를 강제 적용할 테이블을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-168">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="3865b-169">Columnstore 인덱스 유지 관리에 대한 자세한 내용은 [Columnstore 인덱스 관리][manage columnstore indexes] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3865b-169">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="3865b-170">통계를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-170">Optimize statistics</span></span>
<span data-ttu-id="3865b-171">로드 직후 단일 열 통계를 만드는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-171">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="3865b-172">통계에 대한 몇 가지 선택 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-172">There are some choices for statistics.</span></span> <span data-ttu-id="3865b-173">예를 들어 모든 열에 단일 열 통계를 만드는 경우 모든 통계를 다시 작성하는 데 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-173">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="3865b-174">쿼리 조건자에 위치하지 않을 특정 열에 대해 알고 있다면 이들 열에 대한 통계 생성 과정은 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-174">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="3865b-175">단일 열 통계를 모든 테이블의 모든 열에 대해 만들기로 결정한 경우 [통계][statistics] 문서에 저장된 프로시저 코드 샘플 `prc_sqldw_create_stats`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-175">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="3865b-176">다음 예제는 통계를 만들기 위한 좋은 출발점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-176">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="3865b-177">차원 테이블의 각 열과 팩트 테이블의 각 조인 열의 단일 열 통계를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-177">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="3865b-178">이후 언제라도 다른 팩트 테이블 열에 단일 또는 여러 열 통계를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-178">You can always add single or multi-column statistics to other fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="3865b-179">목표를 달성했습니다!</span><span class="sxs-lookup"><span data-stu-id="3865b-179">Achievement unlocked!</span></span>
<span data-ttu-id="3865b-180">이제 Azure SQL Data Warehouse에 데이터를 성공적으로 로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3865b-181">잘 하셨습니다!</span><span class="sxs-lookup"><span data-stu-id="3865b-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="3865b-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3865b-182">Next Steps</span></span>
<span data-ttu-id="3865b-183">데이터 로드는 SQL Data Warehouse를 사용하여 데이터 웨어하우스 솔루션을 개발하는 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="3865b-183">Loading data is the first step to developing a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="3865b-184">[테이블](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) 및 [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md)에서 개발 리소스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3865b-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
