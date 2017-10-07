---
title: "SQL 데이터 웨어하우스로 aaaUse bcp tooload 데이터 | Microsoft Docs"
description: "Bcp 무엇 인지 알아보고 방법과 toouse 데이터 웨어하우징 시나리오에 대 한 것입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>bcp를 사용하여 데이터 로드
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [데이터 팩터리](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[bcp] [ bcp]**  는 SQL Server, 데이터 파일 및 SQL 데이터 웨어하우스 간에 toocopy 데이터를 허용 하는 명령줄 대량 로드 유틸리티입니다. Bcp tooimport 많은 수의 행으로 SQL 데이터 웨어하우스 테이블이 나 tooexport 테이블의 데이터를 SQL Server 데이터 파일에 사용 합니다. Hello queryout 옵션을 사용 경우를 제외 하 고 bcp TRANSACT-SQL 지식 없이 필요 합니다.

bcp는 빠르고 쉬운 방법을 toomove 소량의 데이터 집합 및 SQL 데이터 웨어하우스 데이터베이스 외부로입니다. hello tooload/추출 bcp 통해 권장는 데이터의 정확한 간격에 따라 달라 집니다 연결 toohello Azure 데이터 센터 네트워크에 있습니다.  일반적으로 차원 테이블은 bcp를 통해 쉽게 로드 및 추출할 수 있으나, 대용량 데이터를 로드 또는 추출할 때는 bcp가 권장되지 않습니다.   Polybase는 hello 권장 도구를 로드 하 고 SQL 데이터 웨어하우스의 hello 방대한 병렬 처리 아키텍처를 활용 하 여 작업을 더 효율적으로 많은 양의 데이터를 추출 합니다.

bcp를 사용하면 다음과 같은 작업을 수행할 수 있습니다.

* SQL 데이터 웨어하우스에서 간단한 명령줄 유틸리티 tooload 데이터를 사용 합니다.
* SQL 데이터 웨어하우스에서 간단한 명령줄 유틸리티 tooextract 데이터를 사용 합니다.

이 자습서는 다음에 대한 방법을 보여 줍니다.

* 명령에 hello bcp를 사용 하 여 테이블로 데이터 가져오기
* 테이블 데 hello bcp 명령 출력에서 데이터 내보내기

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>필수 조건
이 자습서를 통해 toostep를 해야합니다.

* SQL 데이터 웨어하우스 데이터베이스
* hello bcp 명령줄 유틸리티 설치
* hello SQLCMD 명령줄 유틸리티 설치

> [!NOTE]
> Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>SQL 데이터 웨어하우스로 데이터 로드
이 자습서에서는 Azure SQL 데이터 웨어하우스의 테이블을 만들 및 hello 테이블로 데이터를 가져올 됩니다.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>1단계: Azure SQL 데이터 웨어하우스에서 테이블 만들기
명령 프롬프트에서 sqlcmd toorun hello 쿼리 toocreate 테이블 인스턴스에서 다음을 사용 합니다.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> 참조 [테이블 개요] [ Table Overview] 또는 [CREATE TABLE 구문을] [ CREATE TABLE syntax] SQL 데이터 웨어하우스 및 hello에서 테이블을 만드는 방법에 대 한 자세한 내용은  hello WITH 절에서 사용할 수 있는 옵션입니다.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>2단계: 원본 데이터 파일 만들기
새 텍스트 파일에 줄의 데이터로 다음 메모장 및 복사 hello 열고이 파일 tooyour 로컬 임시 디렉터리 C:\Temp\DimDate2.txt를 저장 합니다.

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

> [!NOTE]
> 중요 한 tooremember는 해당 bcp.exe hello u t F-8 파일 인코딩을 지원 하지 않습니다. bcp.exe 사용 시 파일에 ASCII 파일 또는 UTF-16 인코딩 파일을 사용하세요.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>3 단계: 연결 및 hello 데이터 가져오기
Bcp를 사용 하 여 연결 하 한 다음 적절 하 게 교체 hello 값 명령에는 hello를 사용 하 여 hello 데이터를 가져올 수 있습니다.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Hello hello 다음 sqlcmd를 사용 하 여 쿼리를 실행 하 여 로드 된 데이터를 확인할 수 있습니다.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Hello 다음 결과 반환 해야 합니다.

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>4단계: 새로 로드한 데이터에 대한 통계 만들기
Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다. 순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 통계 hello 첫 번째 로드 한 후 모든 테이블의 모든 열에 만들 수 또는 hello 데이터에서 발생 된 모든 주요 부분을 변경 합니다. 통계에 대 한 자세한 내용은 참조 hello [통계] [ Statistics] hello 개발 그룹 항목의 항목입니다. 다음은이 예에서 테이블 hello에 대 한 toocreate 통계 로드 하는 방법의 간단한 예

Hello CREATE STATISTICS 문을 sqlcmd 프롬프트에서 다음을 실행 합니다.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 데이터 내보내기
이 자습서에서는 SQL 데이터 웨어하우스의 테이블에서 데이터 파일이 만들어집니다. Tooa 새로운 데이터 파일 DimDate2_export.txt 라는 위에서 만든 hello 데이터를 내보냅니다.

### <a name="step-1-export-hello-data"></a>1 단계: hello 데이터 내보내기
Hello bcp 유틸리티를 사용 하 여 연결을 다음 적절 하 게 교체 hello 값 명령에는 hello를 사용 하 여 데이터를 내보낼 수 있습니다.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Hello 새 파일을 열어 데이터 올바르게 내보낸 hello를 확인할 수 있습니다. hello 파일의에서 데이터를 hello 아래 hello 텍스트를 일치 해야 합니다.

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

> [!NOTE]
> 분산된 시스템에서는 toohello 이기 때문 hello 데이터 순서가 않을 SQL 데이터 웨어하우스 데이터베이스에 걸쳐 hello 동일 합니다. 두 번째 방법은 toouse hello **queryout** bcp toowrite 쿼리의 추출 대신 함수 hello 전체 테이블을 내보냅니다.
> 
> 

## <a name="next-steps"></a>다음 단계
로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.
더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
