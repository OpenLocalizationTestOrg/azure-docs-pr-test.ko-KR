---
title: "aaaLoad-Azure 데이터 레이크 저장소 tooSQL 데이터 웨어하우스 | Microsoft Docs"
description: "Toouse PolyBase 외부 tooload 데이터 Azure 데이터 레이크 저장소에서 Azure SQL 데이터 웨어하우스 테이블 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="1619c-103">Azure Data Lake Store에서 SQL Data Warehouse로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="1619c-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="1619c-104">이 문서의 제공 SQL 데이터 웨어하우스로 tooload 데이터에서 데이터 레이크 저장소 ADLS (Azure)에 필요한 모든 단계 PolyBase를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="1619c-105">Hello 외부 테이블을 사용 하 여 ADLS에 저장 된 hello 데이터에 대해 수 toorun 임시 쿼리를 있는 동안 모범 사례로 권장 hello 데이터 hello SQL 데이터 웨어하우스를 가져오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="1619c-106">예상 시간: 10 분 hello 필수 가정 toocomplete가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="1619c-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="1619c-108">Azure 데이터 레이크 저장소에서 개체 tooload를 외부 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="1619c-109">Azure 데이터 레이크 저장소 디렉터리 tooan를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="1619c-110">Azure SQL Data Warehouse에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1619c-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1619c-111">Before you begin</span></span>
<span data-ttu-id="1619c-112">toorun 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="1619c-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="1619c-113">서비스 간 인증에 대 한 azure Active Directory 응용 프로그램 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="1619c-114">toocreate를 따라 [Active directory 인증](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="1619c-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="1619c-115">Hello 클라이언트 ID, 키 및 Active Directory 응용 프로그램 tooconnect tooyour SQL 데이터 웨어하우스에서 Azure 데이터 레이크의 oauth 2.0 토큰 끝점 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="1619c-116">어떻게 tooget 이러한 값은 위의 hello 링크에 대 한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="1619c-117">Azure Active Directory 응용 프로그램 등록에 대 한 참고 ' 응용 프로그램 ID' hello를 사용 하 여 hello 클라이언트 ID로</span><span class="sxs-lookup"><span data-stu-id="1619c-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="1619c-118">SQL Server Management Studio 또는 SQL Server Data Tools, SSMS toodownload 참조 연결 및 [쿼리 SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="1619c-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="1619c-119">Azure SQL 데이터 웨어하우스 toocreate 하나를 수행: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="1619c-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="1619c-120">Azure Data Lake Store, 암호화를 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="1619c-121">toocreate 하나 수행: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="1619c-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="1619c-122">Hello 데이터 소스 구성</span><span class="sxs-lookup"><span data-stu-id="1619c-122">Configure hello data source</span></span>
<span data-ttu-id="1619c-123">PolyBase는 T-SQL 개체 외부 toodefine hello 위치 및 hello 외부 데이터의 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="1619c-124">hello 외부 개체 번째 외부에 저장 되는 SQL 데이터 웨어하우스 및 참조 hello 데이터에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="1619c-125">자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="1619c-125">Create a credential</span></span>
<span data-ttu-id="1619c-126">tooaccess 프로그램 Azure 데이터 레이크 저장소로 데이터베이스 마스터 키 tooencrypt toocreate hello 다음 단계에서 사용 하 여 자격 증명 암호 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="1619c-127">그런 다음 저장 hello 서비스 사용자 자격 증명 AAD에서 설정 하는 데이터베이스 범위 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="1619c-128">경우 Azure 저장소 Blob PolyBase tooconnect tooWindows 사용한, hello 자격 증명을 확인 하는 구문이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="1619c-129">해야 tooconnect tooAzure 데이터 레이크 저장소 **첫 번째** Azure Active Directory 응용 프로그램을 만들려면 액세스 키를 만들고 hello 응용 프로그램 액세스 toohello Azure 데이터 레이크 리소스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="1619c-130">Instrucitons tooperform 이러한 단계는 있는 [여기](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
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


### <a name="create-hello-external-data-source"></a><span data-ttu-id="1619c-131">Hello 외부 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="1619c-131">Create hello external data source</span></span>
<span data-ttu-id="1619c-132">이 사용 하 여 [외부 데이터 원본 만들기] [ CREATE EXTERNAL DATA SOURCE] hello 데이터 및 데이터 형식을 hello toostore hello 위치 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="1619c-133">Azure 포털 hello 및 www.portal.azure.com hello ADL URI를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="1619c-134">데이터 형식 구성</span><span class="sxs-lookup"><span data-stu-id="1619c-134">Configure data format</span></span>
<span data-ttu-id="1619c-135">ADLS tooimport hello 데이터 toospecify hello 외부 파일 형식을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="1619c-136">이 명령에는 데이터 형식에 따른 옵션 toodescribe 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="1619c-137">다음은 파이프로 구분된 텍스트 파일인 자주 사용되는 파일 형식의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="1619c-138">[외부 파일 형식 만들기][CREATE EXTERNAL FILE FORMAT]의 전체 목록은 T-SQL 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1619c-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
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

## <a name="create-hello-external-tables"></a><span data-ttu-id="1619c-139">Hello 외부 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1619c-139">Create hello external tables</span></span>
<span data-ttu-id="1619c-140">이제 사용자가 지정한 데이터 원본 및 파일 형식이 hello 준비 toocreate hello에 대 한 외부 테이블 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="1619c-141">외부 테이블은 외부 데이터와 상호 작용하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="1619c-142">PolyBase는 재귀 디렉터리 순회 tooread hello 위치 매개 변수에서 지정 된 hello 디렉터리의 모든 하위 디렉터리의 모든 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="1619c-143">또한, 다음 예제는 hello toocreate 개체 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="1619c-144">ADLS에 있는 hello 데이터로 toocustomize hello 문을 toowork가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

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

## <a name="external-table-considerations"></a><span data-ttu-id="1619c-145">외부 테이블 고려 사항</span><span class="sxs-lookup"><span data-stu-id="1619c-145">External Table Considerations</span></span>
<span data-ttu-id="1619c-146">외부 테이블을 작성 하는 것은 간단 하지만 toobe 설명 해야 하는 몇 가지 갖는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="1619c-147">PolyBase를 사용하는 데이터 로드는 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="1619c-148">즉, 각 데이터 행을 hello 되 고 수집 된 hello 테이블 스키마 정의 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="1619c-149">지정된 된 행에는 hello 스키마 정의와 일치 하지 않습니다, hello 행 hello 부하에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="1619c-150">hello REJECT_TYPE 인데, REJECT_VALUE 옵션을 사용 하면 toodefine 행 수 또는 hello 데이터의 비율 hello 최종 테이블에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="1619c-151">로드 시 hello 거부 값에 도달 하면 hello 로드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="1619c-152">거부 된 행의 가장 일반적인 원인은 hello 스키마 정의가 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="1619c-153">예를 들어 열 올바르게 지정 되지 int의 hello 스키마 hello 데이터 hello 파일에는 문자열인 경우 모든 행에 tooload를 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="1619c-154">hello 위치 tooread 데이터를 원하는 hello 맨 위에 있는 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="1619c-155">이 경우 있었던 /DimProduct/ PolyBase 아래의 하위 디렉터리는 hello 하위 디렉터리 내의 모든 hello 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="1619c-156">Hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="1619c-156">Load hello data</span></span>
<span data-ttu-id="1619c-157">Azure 데이터 레이크 저장소의 tooload 데이터 hello를 사용 하 여 [CREATE TABLE AS SELECT (Transact SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] 문.</span><span class="sxs-lookup"><span data-stu-id="1619c-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="1619c-158">외부 테이블을 만든는 사용 하 여 hello에서 강력한 형식의 CTAS에는 포함 된 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="1619c-159">CTAS에는 새 테이블을 만들고을 select 문의 hello 결과 함께 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="1619c-160">CTAS에는 새 테이블 toohave hello 정의의 hello hello 결과 select 문 처럼 동일한 열과 데이터 형식을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="1619c-161">외부 테이블에서 모든 hello 열을 선택 하는 경우에 hello 새 테이블은 hello 외부 테이블의 hello 열과 데이터 형식을의 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="1619c-162">이 예제에서는 외부 테이블 DimProduct_external에서 DimProduct라는 해시 분산 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="1619c-163">Columnstore 압축을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-163">Optimize columnstore compression</span></span>
<span data-ttu-id="1619c-164">기본적으로 SQL 데이터 웨어하우스는 hello 테이블을 클러스터형된 columnstore 인덱스로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="1619c-165">로드를 완료 한 후 일부 hello 데이터 행 수 압축 되지 hello columnstore에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="1619c-166">여기에는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="1619c-167">toolearn 더 참조 [columnstore 인덱스 관리][manage columnstore indexes]합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="1619c-168">toooptimize 쿼리 성능 및 columnstore 압축 하 여 로드 한 후 모든 hello 행 hello 테이블 tooforce hello columnstore 인덱스 toocompress를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="1619c-169">Columnstore 인덱스 유지 관리에 대 한 자세한 내용은 참조 hello [columnstore 인덱스 관리] [ manage columnstore indexes] 문서.</span><span class="sxs-lookup"><span data-stu-id="1619c-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="1619c-170">통계를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-170">Optimize statistics</span></span>
<span data-ttu-id="1619c-171">부하 후 즉시 최상의 toocreate 단일 열 통계에는 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="1619c-172">통계에 대한 몇 가지 선택 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-172">There are some choices for statistics.</span></span> <span data-ttu-id="1619c-173">예를 들어 모든 열에 단일 열 통계를 만드는 경우 걸릴 수 있습니다는 오랜 시간이 toorebuild 모든 hello 통계.</span><span class="sxs-lookup"><span data-stu-id="1619c-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="1619c-174">특정 열 쿼리 조건자의 toobe 것을 알고 있는 경우 해당 열에 만드는 통계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="1619c-175">모든 테이블의 모든 열에 단일 열 통계 toocreate 결정 한 경우에 hello 저장된 프로시저 코드 샘플을 사용할 수 있습니다 `prc_sqldw_create_stats` hello에 [통계] [ statistics] 문서.</span><span class="sxs-lookup"><span data-stu-id="1619c-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="1619c-176">다음 예제는 hello은 통계를 만들기 위한 좋은 시작 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="1619c-177">Hello 팩트 테이블에 각 조인 열 및 hello 차원 테이블의 각 열에 단일 열 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="1619c-178">항상 단일 또는 여러 열 통계 tooother 팩트 테이블 열을 나중에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="1619c-179">목표를 달성했습니다!</span><span class="sxs-lookup"><span data-stu-id="1619c-179">Achievement unlocked!</span></span>
<span data-ttu-id="1619c-180">이제 Azure SQL Data Warehouse에 데이터를 성공적으로 로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1619c-181">잘 하셨습니다!</span><span class="sxs-lookup"><span data-stu-id="1619c-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="1619c-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1619c-182">Next Steps</span></span>
<span data-ttu-id="1619c-183">Hello 첫 번째 단계 toodeveloping SQL 데이터 웨어하우스를 사용 하 여 데이터 웨어하우스 솔루션은 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1619c-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="1619c-184">[테이블](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) 및 [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md)에서 개발 리소스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="1619c-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
