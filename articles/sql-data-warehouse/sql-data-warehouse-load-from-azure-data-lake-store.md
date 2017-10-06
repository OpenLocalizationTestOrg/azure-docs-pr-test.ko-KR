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
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Azure Data Lake Store에서 SQL Data Warehouse로 데이터 로드
이 문서의 제공 SQL 데이터 웨어하우스로 tooload 데이터에서 데이터 레이크 저장소 ADLS (Azure)에 필요한 모든 단계 PolyBase를 사용 하 여 합니다.
Hello 외부 테이블을 사용 하 여 ADLS에 저장 된 hello 데이터에 대해 수 toorun 임시 쿼리를 있는 동안 모범 사례로 권장 hello 데이터 hello SQL 데이터 웨어하우스를 가져오는 합니다.
예상 시간: 10 분 hello 필수 가정 toocomplete가 필요 합니다.
이 자습서에서는 다음 방법에 대해 알아봅니다.

1. Azure 데이터 레이크 저장소에서 개체 tooload를 외부 데이터베이스를 만듭니다.
2. Azure 데이터 레이크 저장소 디렉터리 tooan를 연결 합니다.
3. Azure SQL Data Warehouse에 데이터를 로드합니다.

## <a name="before-you-begin"></a>시작하기 전에
toorun 해야이 자습서에서는:

* 서비스 간 인증에 대 한 azure Active Directory 응용 프로그램 toouse 합니다. toocreate를 따라 [Active directory 인증](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> Hello 클라이언트 ID, 키 및 Active Directory 응용 프로그램 tooconnect tooyour SQL 데이터 웨어하우스에서 Azure 데이터 레이크의 oauth 2.0 토큰 끝점 값 해야합니다. 어떻게 tooget 이러한 값은 위의 hello 링크에 대 한 세부 정보입니다.
>Azure Active Directory 응용 프로그램 등록에 대 한 참고 ' 응용 프로그램 ID' hello를 사용 하 여 hello 클라이언트 ID로

* SQL Server Management Studio 또는 SQL Server Data Tools, SSMS toodownload 참조 연결 및 [쿼리 SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Azure SQL 데이터 웨어하우스 toocreate 하나를 수행: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Azure Data Lake Store, 암호화를 사용하거나 사용하지 않도록 설정합니다. toocreate 하나 수행: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Hello 데이터 소스 구성
PolyBase는 T-SQL 개체 외부 toodefine hello 위치 및 hello 외부 데이터의 특성을 사용합니다. hello 외부 개체 번째 외부에 저장 되는 SQL 데이터 웨어하우스 및 참조 hello 데이터에 저장 됩니다.


###  <a name="create-a-credential"></a>자격 증명 만들기
tooaccess 프로그램 Azure 데이터 레이크 저장소로 데이터베이스 마스터 키 tooencrypt toocreate hello 다음 단계에서 사용 하 여 자격 증명 암호 필요 합니다.
그런 다음 저장 hello 서비스 사용자 자격 증명 AAD에서 설정 하는 데이터베이스 범위 자격 증명을 만듭니다. 경우 Azure 저장소 Blob PolyBase tooconnect tooWindows 사용한, hello 자격 증명을 확인 하는 구문이 서로 다릅니다.
해야 tooconnect tooAzure 데이터 레이크 저장소 **첫 번째** Azure Active Directory 응용 프로그램을 만들려면 액세스 키를 만들고 hello 응용 프로그램 액세스 toohello Azure 데이터 레이크 리소스를 부여 합니다. Instrucitons tooperform 이러한 단계는 있는 [여기](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)합니다.

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


### <a name="create-hello-external-data-source"></a>Hello 외부 데이터 원본 만들기
이 사용 하 여 [외부 데이터 원본 만들기] [ CREATE EXTERNAL DATA SOURCE] hello 데이터 및 데이터 형식을 hello toostore hello 위치 명령입니다.
Azure 포털 hello 및 www.portal.azure.com hello ADL URI를 찾을 수 있습니다.

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



## <a name="configure-data-format"></a>데이터 형식 구성
ADLS tooimport hello 데이터 toospecify hello 외부 파일 형식을 해야합니다. 이 명령에는 데이터 형식에 따른 옵션 toodescribe 합니다.
다음은 파이프로 구분된 텍스트 파일인 자주 사용되는 파일 형식의 예입니다.
[외부 파일 형식 만들기][CREATE EXTERNAL FILE FORMAT]의 전체 목록은 T-SQL 설명서를 참조하세요.

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

## <a name="create-hello-external-tables"></a>Hello 외부 테이블 만들기
이제 사용자가 지정한 데이터 원본 및 파일 형식이 hello 준비 toocreate hello에 대 한 외부 테이블 있는지 합니다. 외부 테이블은 외부 데이터와 상호 작용하는 방식입니다. PolyBase는 재귀 디렉터리 순회 tooread hello 위치 매개 변수에서 지정 된 hello 디렉터리의 모든 하위 디렉터리의 모든 파일을 사용 합니다. 또한, 다음 예제는 hello toocreate 개체 hello 하는 방법을 보여 줍니다. ADLS에 있는 hello 데이터로 toocustomize hello 문을 toowork가 필요 합니다.

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

## <a name="external-table-considerations"></a>외부 테이블 고려 사항
외부 테이블을 작성 하는 것은 간단 하지만 toobe 설명 해야 하는 몇 가지 갖는 합니다.

PolyBase를 사용하는 데이터 로드는 강력한 형식입니다. 즉, 각 데이터 행을 hello 되 고 수집 된 hello 테이블 스키마 정의 충족 해야 합니다.
지정된 된 행에는 hello 스키마 정의와 일치 하지 않습니다, hello 행 hello 부하에서 거부 됩니다.

hello REJECT_TYPE 인데, REJECT_VALUE 옵션을 사용 하면 toodefine 행 수 또는 hello 데이터의 비율 hello 최종 테이블에 존재 해야 합니다.
로드 시 hello 거부 값에 도달 하면 hello 로드가 실패 합니다. 거부 된 행의 가장 일반적인 원인은 hello 스키마 정의가 일치 하지 않습니다.
예를 들어 열 올바르게 지정 되지 int의 hello 스키마 hello 데이터 hello 파일에는 문자열인 경우 모든 행에 tooload를 실패 합니다.

hello 위치 tooread 데이터를 원하는 hello 맨 위에 있는 디렉터리를 지정 합니다.
이 경우 있었던 /DimProduct/ PolyBase 아래의 하위 디렉터리는 hello 하위 디렉터리 내의 모든 hello 데이터를 가져옵니다.

## <a name="load-hello-data"></a>Hello 데이터 로드
Azure 데이터 레이크 저장소의 tooload 데이터 hello를 사용 하 여 [CREATE TABLE AS SELECT (Transact SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] 문. 외부 테이블을 만든는 사용 하 여 hello에서 강력한 형식의 CTAS에는 포함 된 로드 합니다.

CTAS에는 새 테이블을 만들고을 select 문의 hello 결과 함께 채웁니다. CTAS에는 새 테이블 toohave hello 정의의 hello hello 결과 select 문 처럼 동일한 열과 데이터 형식을 hello 합니다. 외부 테이블에서 모든 hello 열을 선택 하는 경우에 hello 새 테이블은 hello 외부 테이블의 hello 열과 데이터 형식을의 복제 합니다.

이 예제에서는 외부 테이블 DimProduct_external에서 DimProduct라는 해시 분산 테이블을 만듭니다.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Columnstore 압축을 최적화합니다.
기본적으로 SQL 데이터 웨어하우스는 hello 테이블을 클러스터형된 columnstore 인덱스로 저장합니다. 로드를 완료 한 후 일부 hello 데이터 행 수 압축 되지 hello columnstore에 합니다.  여기에는 다양한 이유가 있습니다. toolearn 더 참조 [columnstore 인덱스 관리][manage columnstore indexes]합니다.

toooptimize 쿼리 성능 및 columnstore 압축 하 여 로드 한 후 모든 hello 행 hello 테이블 tooforce hello columnstore 인덱스 toocompress를 다시 작성 합니다.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Columnstore 인덱스 유지 관리에 대 한 자세한 내용은 참조 hello [columnstore 인덱스 관리] [ manage columnstore indexes] 문서.

## <a name="optimize-statistics"></a>통계를 최적화합니다.
부하 후 즉시 최상의 toocreate 단일 열 통계에는 다른 합니다. 통계에 대한 몇 가지 선택 사항이 있습니다. 예를 들어 모든 열에 단일 열 통계를 만드는 경우 걸릴 수 있습니다는 오랜 시간이 toorebuild 모든 hello 통계. 특정 열 쿼리 조건자의 toobe 것을 알고 있는 경우 해당 열에 만드는 통계를 건너뛸 수 있습니다.

모든 테이블의 모든 열에 단일 열 통계 toocreate 결정 한 경우에 hello 저장된 프로시저 코드 샘플을 사용할 수 있습니다 `prc_sqldw_create_stats` hello에 [통계] [ statistics] 문서.

다음 예제는 hello은 통계를 만들기 위한 좋은 시작 지점입니다. Hello 팩트 테이블에 각 조인 열 및 hello 차원 테이블의 각 열에 단일 열 통계를 만듭니다. 항상 단일 또는 여러 열 통계 tooother 팩트 테이블 열을 나중에 추가할 수 있습니다.


## <a name="achievement-unlocked"></a>목표를 달성했습니다!
이제 Azure SQL Data Warehouse에 데이터를 성공적으로 로드했습니다. 잘 하셨습니다!

##<a name="next-steps"></a>다음 단계
Hello 첫 번째 단계 toodeveloping SQL 데이터 웨어하우스를 사용 하 여 데이터 웨어하우스 솔루션은 데이터를 로드 합니다. [테이블](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) 및 [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md)에서 개발 리소스를 확인하세요.


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
