---
title: "SQL Data Warehouse의 PolyBase 사용을 위한 가이드 | Microsoft Docs"
description: "SQL 데이터 웨어하우스 시나리오에서 PolyBase를 사용하는 방법에 대한 지침 및 권장 사항입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 PolyBase 사용을 위한 가이드
이 가이드는 SQL 데이터 웨어하우스의 PolyBase를 사용하는 방법에 대한 실용적인 정보를 제공합니다.

시작하려면 [PolyBase를 사용하여 데이터 로드][Load data with PolyBase] 자습서를 참조하세요.

## <a name="rotating-storage-keys"></a>저장소 키 회전
때때로 보안을 위해 blob 저장소 액세스 키를 변경하는 것이 좋습니다.

이 작업을 수행하는 가장 세련된 방법은 "키 회전" 라고 하는 프로세스를 따르는 것입니다. Blob 저장소 계정에 두 개의 저장소 키가 있는 것을 알 수 있습니다. 이는 다음을 전환하기 위한 것입니다.

Azure 저장소 계정 키를 회전하는 것은 간단한 3단계 프로세스입니다.

1. 두 번째 저장소 액세스 키를 기반으로 두 번째 데이터베이스 범위가 지정된 자격 증명을 만듭니다.
2. 이 새 자격 증명을 기반으로 두 번째 외부 데이터 원본을 만듭니다.
3. 새 외부 테이블을 끌어 놓고 새 외부 데이터 원본을 가리키는 외부 테이블을 만듭니다.

외부 테이블을 새 외부 데이터 원본으로 모두 마이그레이션한 후에 정리 작업을 수행할 수 있습니다.

1. 첫 번째 외부 데이터 원본을 끌어 놓습니다.
2. 기본 저장소 액세스 키를 기반으로 첫 번째 데이터베이스 범위 자격 증명을 끌어 놓습니다.
3. Azure에 로그인하고 다음 번에 사용할 준비가 된 기본 액세스 키를 다시 생성합니다.

## <a name="query-azure-blob-storage-data"></a>Azure Blob 저장소 데이터 쿼리
외부 테이블에 대한 쿼리는 관계형 테이블인 것처럼 테이블 이름을 사용합니다.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> 외부 테이블에 대한 쿼리가 *"쿼리가 중단되었습니다. 외부 소스에서 읽는 동안 최대 거부 임계값에 도달했습니다."*오류로 인해 실패할 수 있습니다. 이는 외부 데이터에 *더티* 레코드가 포함되어 있음을 나타냅니다. 열의 실제 데이터 형식/개수가 외부 테이블의 열 정의와 일치하지 않거나 데이터가 지정된 외부 파일 형식에 맞지 않는 경우 데이터 레코드가 '더티'로 간주됩니다. 이 문제를 해결하려면 외부 테이블 및 외부 파일 형식 정의가 올바른지, 그리고 외부 데이터가 이러한 정의를 준수하는지 확인합니다. 외부 데이터 레코드의 하위 집합이 더티인 경우 CREATE EXTERNAL TABLE DDL의 거부 옵션을 사용하여 쿼리에 대해 해당 레코드를 거부하도록 선택할 수 있습니다.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Azure Blob 저장소에서 데이터 로드
이 예제에서는 SQL 데이터 웨어하우스 데이터베이스로 Azure blob 저장소에서 데이터를 로드합니다.

직접 데이터를 저장하면 쿼리를 위한 데이터 전송 시간을 제거합니다. Columnstore 인덱스를 사용하여 데이터를 저장하면 최대 10배까지 분석 쿼리를 위한 쿼리 성능을 개선합니다.

이 예제에서는 CREATE TABLE AS SELECT 문을 사용하여 데이터를 로드합니다. 새 테이블은 쿼리에서 명명된 열을 상속합니다. 외부 테이블 정의에서 해당 열의 데이터 형식을 상속합니다.

CREATE TABLE AS SELECT는 SQL 데이터 웨어하우스의 모든 계산 노드에 병렬로 데이터를 로드하는 높은 성능의 Transact-SQL 문입니다.  분석 플랫폼 시스템에는 방대한 병렬 처리(MPP) 엔진을 처음 개발했으며 이제 SQL 데이터 웨어하우스에 포함되었습니다.

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

[CREATE TABLE AS SELECT(Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]를 참조하세요.

## <a name="create-statistics-on-newly-loaded-data"></a>새로 로드한 데이터에 대한 통계 만들기
Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.  쿼리에서 최상의 성능을 얻으려면, 데이터를 처음 로드하거나 데이터에 상당한 변화가 발생한 후에 모든 테이블의 모든 열에서 통계가 만들어지는 것이 중요합니다.  통계에 대한 자세한 설명은 개발 항목 그룹의 [통계][Statistics] 항목을 참조하세요.  다음은 이 예제에 로드한 테이블에 대한 통계를 만드는 방법을 간략히 보여주는 예입니다.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a>Azure Blob 저장소에 데이터 내보내기
이 섹션은 SQL 데이터 웨어하우스에서 Azure Blob 저장소로 데이터를 내보내는 방법을 보여줍니다. 이 예에서는 모든 계산 노드에서 병렬로 데이터를 내보내는 높은 성능의 Transact-SQL 문인 CREATE EXTERNAL TABLE AS SELECT를 사용합니다.

다음 예에서는 dbo.Weblogs 표에서 열 정의 및 데이터를 사용하여 외부 표 Weblogs2014를 만듭니다. 외부 표 정의는 SQL 데이터 웨어하우스에 저장되며 SELECT 문의 결과는 데이터 원본에서 정의한 Blob 컨테이너 아래에 있는 “/archive/log2014/” 디렉터리로 내보내집니다. 데이터는 지정된 텍스트 파일 형식으로 내보냅니다.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>사용자 로드 격리
SQL DW로 데이터를 로드할 수 있는 여러 명의 사용자가 필요한 경우가 있습니다. [CREATE TABLE AS SELECT(Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]는 데이터베이스의 CONTROL 권한이 필요하므로 모든 스키마에 대한 제어 액세스가 있는 여러 명의 사용자가 필요합니다. 이를 제한하기 위해 DENY CONTROL 문을 사용할 수 있습니다.

예: 데이터베이스 스키마, 부서 A에 대한 스키마_A 및 부서 B에 대한 스키마_B를 가정합니다. 데이터베이스 사용자, 사용자_A 및 사용자_B가 부서 A와 B 각각에서 PolyBase 로딩에 대한 사용자가 되도록 합니다. 둘 모두 데이터베이스 CONTROL 권한을 부여 받습니다.
스키마 A와 B의 작성자는 이제 DENY를 사용하여 해당 스키마를 잠급니다.

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 이로 인해 사용자_A 및 사용자_B는 이제 다른 부서의 스키마에서 차단되어야 합니다.
 


## <a name="next-steps"></a>다음 단계
SQL Data Warehouse로 데이터를 이동하는 방법에 대한 자세한 내용은 [데이터 마이그레이션 개요][data migration overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
