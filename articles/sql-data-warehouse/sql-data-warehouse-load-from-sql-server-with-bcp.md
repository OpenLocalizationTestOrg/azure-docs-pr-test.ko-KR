---
title: "Azure SQL 데이터 웨어하우스 (bcp)에 SQL Server에서 aaaLoad 데이터 | Microsoft Docs"
description: "작은 데이터 크기에 대 한 Azure SQL 데이터 웨어하우스에 직접 hello 데이터 가져오기 및 SQL Server tooflat 파일에서 bcp tooexport 데이터를 사용 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(플랫 파일)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

작은 데이터 집합에 대 한 hello bcp 명령줄 유틸리티 tooexport 데이터 SQL Server를 사용 하 고 tooAzure SQL 데이터 웨어하우스 직접 로드할 수 있습니다.

이 자습서에서는 bcp를 사용하여:

* 테이블에서 SQL Server에서에서 내보냅니다 hello bcp 명령을 사용 하 여 (또는 간단한 샘플 파일 만들기)
* 플랫 파일 tooSQL 데이터 웨어하우스에서에서 hello 테이블을 가져옵니다.
* Hello 로드 된 데이터에 통계를 만듭니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>시작하기 전에
### <a name="prerequisites"></a>필수 조건
이 자습서를 통해 toostep를 해야합니다.

* SQL 데이터 웨어하우스 데이터베이스
* hello bcp 명령줄 유틸리티 설치
* hello sqlcmd 명령줄 유틸리티 설치

Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.

### <a name="data-in-ascii-or-utf-16-format"></a>ASCII 또는 UTF-16 형식 데이터
이 자습서에서는 사용자 고유의 데이터로 시도 하는 경우 데이터 toouse hello ASCII 또는 utf-16 인코딩 bcp u t F-8을 지원 하지 않으므로 필요 합니다. 

PolyBase는 UTF-8을 지원하지만 아직 UTF-16은 지원하지 않습니다. Polybase toocombine bcp 하려는 경우 시켜야 하 tootransform hello 데이터 tooUTF 8 SQL Server에서 내보낸 후 참고 합니다. 

## <a name="1-create-a-destination-table"></a>1. 대상 테이블 만들기
SQL 데이터 웨어하우스에 hello 부하에 대 한 대상 테이블 hello 될 테이블을 정의 합니다. hello 테이블의 hello 열에는 데이터 파일의 각 행에 toohello 데이터 일치 해야 합니다.

toocreate 테이블을 명령 프롬프트를 열고 sqlcmd.exe toorun hello 다음 명령을 사용 하 여 합니다.

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


## <a name="2-create-a-source-data-file"></a>2. 원본 데이터 파일 만들기
새 텍스트 파일에 줄의 데이터로 다음 메모장 및 복사 hello 열고이 파일 tooyour 로컬 임시 디렉터리 C:\Temp\DimDate2.txt를 저장 합니다. 이 데이터는 ASCII 형식입니다.

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

(선택 사항) tooexport SQL Server 데이터베이스에서 사용자 고유의 데이터는 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다. TableName, ServerName, DatabaseName, Username 및 Password를 사용자의 정보로 바꿉니다.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Hello 데이터 로드
tooload hello 데이터 명령 프롬프트를 열고 다음 명령을, hello 값을 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호에 대 한 사용자의 정보로 대체 hello를 실행 합니다.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

이 명령은 tooverify hello 데이터가 제대로 로드 사용

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

hello 결과 다음과 같이 표시 됩니다.

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

## <a name="4-create-statistics"></a>4. 통계 만들기
SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다. tooget hello 최고의 쿼리 성능을 인지 모든 테이블의 모든 열에 대 한 중요 한 toocreate 통계 hello 첫 번째 로드 한 후 모든 변경이 hello 데이터에서 발생 한 후 합니다. 통계에 대한 자세한 설명은 [통계][Statistics]를 참조하세요. 

Hello 명령 toocreate 통계에 새로 로드 된 테이블에 다음을 실행 합니다.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. SQL 데이터 웨어하우스에서 데이터 내보내기
쉽도록 SQL 데이터 웨어하우스 밖으로 다시 로드 된 hello 데이터를 내보낼 수 있습니다.  hello 명령 tooexport은 SQL Server에서 내보내기 동일 hello 정확 하 게 합니다.

그러나 hello 결과에 차이가 있습니다. Hello 데이터는 데이터를 내보낼 때 SQL 데이터 웨어하우스 내에서 분산 된 위치에 저장 되므로 각 계산 노드가 데이터 toohello 출력 파일을 씁니다. hello hello 출력 파일에는 데이터의 hello 순서가 가능성이 toobe hello hello 입력된 파일에는 데이터의 hello 순서와 다른 경우

### <a name="export-a-table-and-compare-exported-results"></a>테이블을 내보내고 내보낸 결과 비교
toosee hello 내보낸된 데이터를 명령 프롬프트를 열고 고유한 매개 변수를 사용 하 여이 명령을 실행 합니다. 서버 이름에는 논리 SQL Server에 Azure의 hello 이름입니다.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Hello 새 파일을 열어 데이터 올바르게 내보낸 hello를 확인할 수 있습니다. hello 파일의에서 데이터를 hello 아래의 hello 텍스트와 일치 해야 하지만 다른 순서로 정렬 될 가능성이 높습니다.

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

### <a name="export-hello-results-of-a-query"></a>쿼리의 hello 결과 내보내기
Hello를 사용할 수 있습니다 **queryout** bcp tooexport hello 쿼리 결과를 내보내는 hello 전체 테이블 대신의 기능입니다. 

## <a name="next-steps"></a>다음 단계
로드 개요는 [SQL Data Warehouse로 데이터 로드][Load data into SQL Data Warehouse]를 참조하세요.
더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.
SQL Data Warehouse에 테이블을 만드는 방법에 대한 내용은 [테이블 개요][Table Overview] 또는 [CREATE TABLE 구문][CREATE TABLE syntax]을 참조하세요.

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
