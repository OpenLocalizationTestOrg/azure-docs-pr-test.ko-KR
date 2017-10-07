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
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 PolyBase를 사용하여 데이터 로드
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [데이터 팩터리](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

이 자습서에서는 어떻게 AzCopy 및 PolyBase를 사용 하 여 SQL 데이터 웨어하우스로 tooload 데이터입니다. 자습서를 마치면 다음과 같은 방법을 알게 됩니다.

* AzCopy toocopy 데이터 tooAzure blob 저장소를 사용 하 여
* 데이터베이스 개체 toodefine hello 데이터 만들기
* T-SQL 쿼리 tooload hello 데이터를 실행 합니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>필수 조건
이 자습서를 통해 toostep, 해야

* SQL 데이터 웨어하우스 데이터베이스
* 표준 로컬 중복 저장소(표준-LRS), 표준 지역 중복 저장소(표준-GRS) 또는 표준 읽기 액세스 지역 중복 저장소(표준-RAGRS) 유형의 Azure 저장소 계정
* AzCopy 명령줄 유틸리티. 다운로드 및 설치 hello [AzCopy의 최신 버전] [ latest version of AzCopy] hello Microsoft Azure 저장소 도구를 함께 설치 합니다.
  
    ![Azure 저장소 도구](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>1 단계: 추가 샘플 데이터 tooAzure blob 저장소
주문 tooload 데이터에서 필요 tooput 몇 가지 샘플 데이터를 Azure blob 저장소로 합니다. 이 단계에서는 Azure Blob 저장소를 샘플 데이터로 채웁니다. 나중에 사용 합니다 PolyBase tooload이 예제 데이터를 SQL 데이터 웨어하우스 데이터베이스에.

### <a name="a-prepare-a-sample-text-file"></a>A. 샘플 텍스트 파일 준비
tooprepare 샘플 텍스트 파일:

1. 메모장 및 복사 hello 줄의 데이터를 새 파일에 다음을 엽니다. %Temp%\DimDate2.txt이 tooyour 로컬 임시 디렉터리를 저장 합니다.

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

### <a name="b-find-your-blob-service-endpoint"></a>B. Blob 서비스 끝점 찾기
toofind blob 서비스 끝점:

1. Hello Azure 포털에서에서 선택 **찾아보기** > **저장소 계정은**합니다.
2. 원하는 toouse hello 저장소 계정을 클릭 합니다.
3. Hello 저장소 계정 블레이드에서 Blob를 클릭 합니다.
   
    ![BLOB 클릭](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. 나중을 위해 Blob 서비스 끝점 URL을 저장합니다.
   
    ![Blob 서비스 끝점](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Azure 저장소 키 찾기
toofind Azure 저장소 키:

1. Hello Azure 포털에서에서 선택 **찾아보기** > **저장소 계정은**합니다.
2. 원하는 toouse hello 저장소 계정을 클릭 합니다.
3. **모든 설정** > **선택키**를 선택합니다.
4. Hello 복사 상자 toocopy 액세스 키 toohello 클립보드 중 하나를 클릭 합니다.
   
    ![Azure 저장소 키 복사](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Hello 샘플 파일 tooAzure blob 저장소를 복사 합니다.
toocopy 데이터 tooAzure blob 저장소:

1. 명령 프롬프트를 열고 디렉터리 toohello AzCopy 설치 디렉터리를 변경 합니다. 이 명령은 64 비트 Windows 클라이언트에서 toohello 기본 설치 디렉터리를 변경합니다.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. 다음 명령은 tooupload hello 파일 hello를 실행 합니다. <blob service endpoint URL>에 Blob service 끝점 URL을 지정하고 <azure_storage_account_key>에 Azure Storage 계정 키를 지정합니다.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

참고 항목 [hello AzCopy 명령줄 유틸리티 시작][Getting Started with hello AzCopy Command-Line Utility]합니다.

### <a name="e-explore-your-blob-storage-container"></a>E. Blob 저장소 컨테이너 탐색
tooblob 저장소에 업로드 한 toosee hello 파일:

1. Tooyour Blob 서비스 블레이드를 돌아갑니다.
2. 컨테이너에서 **datacontainer**를 두 번 클릭합니다.
3. tooexplore hello 경로 tooyour 데이터 hello 폴더를 클릭 합니다. **datedimension** 업로드 된 파일을 볼 수 있습니다 **DimDate2.txt**합니다.
4. tooview 속성 클릭 **DimDate2.txt**합니다.
5. Note hello Blob 속성 블레이드에서 수 다운로드 하거나 있는 hello 파일을 삭제 합니다.
   
    ![Azure 저장소 Blob 보기](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>2 단계: hello 샘플 데이터에 대 한 외부 테이블 만들기
이 섹션에서는 hello 예제 데이터를 정의 하는 외부 테이블을 만듭니다.

PolyBase는 Azure blob 저장소에 외부 테이블 tooaccess 데이터를 사용합니다. SQL 데이터 웨어하우스 내에서 hello 데이터 저장 되지 않으므로 이후 PolyBase 데이터베이스 범위 자격 증명을 사용 하 여 인증 toohello 외부 데이터를 처리 합니다.

이 단계에서는 hello 예제 이러한 Transact SQL 문 toocreate 외부 테이블을 사용합니다.

* [마스터 키 (Transact SQL) 만들기] [ Create Master Key (Transact-SQL)] tooencrypt hello 비밀 데이터베이스 범위 자격 증명입니다.
* [데이터베이스 범위 자격 증명 만들기 (Transact SQL)] [ Create Database Scoped Credential (Transact-SQL)] Azure 저장소 계정에 대 한 toospecify 인증 정보입니다.
* [외부 데이터 원본 (Transact SQL) 만들기] [ Create External Data Source (Transact-SQL)] Azure blob 저장소의 toospecify hello 위치입니다.
* [외부 파일 형식 (Transact SQL) 만들기] [ Create External File Format (Transact-SQL)] toospecify hello 데이터 형식입니다.
* [외부 테이블 (Transact SQL) 만들기] [ Create External Table (Transact-SQL)] toospecify hello 테이블 정 및 위치의 hello 데이터입니다.

SQL 데이터 웨어하우스 데이터베이스에 대해 이 쿼리를 실행합니다. Hello Azure blob 저장소에 toohello DimDate2.txt 예제 데이터를 가리키는 hello dbo 스키마에서 DimDate2External 라는 외부 테이블이 만들어집니다.

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


Visual Studio에서 SQL Server 개체 탐색기에서 hello 외부 파일 형식, 외부 데이터 원본 및 hello DimDate2External 테이블을 볼 수 있습니다.

![외부 테이블 보기](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>3단계: SQL 데이터 웨어하우스에 데이터 로드
Hello 외부 테이블을 만든 후 새 테이블로 hello 데이터를 로드 하거나 기존 테이블에 삽입 합니다.

* hello 실행 새 테이블로 tooload hello 데이터 [CREATE TABLE AS SELECT (Transact SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] 문. 새 테이블 hello hello 쿼리에서 명명 된 hello 열이 포함 됩니다. hello 열의 데이터 형식을 hello hello 외부 테이블 정의에 hello 데이터 형식과 일치 됩니다.
* tooload hello 데이터를 기존 테이블에 사용 하 여 hello [삽입... 선택 (Transact SQL)] [ INSERT...SELECT (Transact-SQL)] 문.

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>4단계: 새로 로드한 데이터에 대한 통계 만들기
SQL 데이터 웨어하우스는 통계 자동 만들기 또는 자동 업데이트를 수행하지 않습니다. 따라서 tooachieve 쿼리 성능이 반드시 toocreate 통계 hello 후 각 테이블의 각 열에 먼저 로드 합니다. 것도 중요 한 tooupdate 통계 후 hello 데이터의 주요 부분을 변경 합니다.

이 예제는 hello 새 DimDate2 테이블에 단일 열 통계를 만듭니다.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

toolearn 더 참조 [통계][Statistics]합니다.  

## <a name="next-steps"></a>다음 단계
Hello 참조 [PolyBase 가이드] [ PolyBase guide] 대 한 자세한 내용은 PolyBase를 사용 하는 솔루션을 개발할 때 알고 있어야 합니다.

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
