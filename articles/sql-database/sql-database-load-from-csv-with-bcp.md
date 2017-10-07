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
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>CSV에서 Azure SQL Database(플랫 파일)로 데이터 로드
Azure SQL 데이터베이스로 hello bcp 명령줄 유틸리티 tooimport 데이터 CSV 파일에서 사용할 수 있습니다.

## <a name="before-you-begin"></a>시작하기 전에
### <a name="prerequisites"></a>필수 조건
이 문서의 단계를 toocomplete hello 사용 해야 합니다.

* Azure SQL 데이터베이스 논리 서버 및 데이터베이스
* hello bcp 명령줄 유틸리티 설치
* hello sqlcmd 명령줄 유틸리티 설치

Hello에서 hello bcp 및 sqlcmd 유틸리티를 다운로드할 수 있습니다 [Microsoft 다운로드 센터][Microsoft Download Center]합니다.

### <a name="data-in-ascii-or-utf-16-format"></a>ASCII 또는 UTF-16 형식 데이터
이 자습서에서는 사용자 고유의 데이터로 시도 하는 경우 데이터 toouse hello ASCII 또는 utf-16 인코딩 bcp u t F-8을 지원 하지 않으므로 필요 합니다. 

## <a name="1-create-a-destination-table"></a>1. 대상 테이블 만들기
SQL 데이터베이스의 hello 대상 테이블로 테이블을 정의 합니다. hello 테이블의 hello 열에는 데이터 파일의 각 행에 toohello 데이터 일치 해야 합니다.

toocreate 테이블을 명령 프롬프트를 열고 sqlcmd.exe toorun hello 다음 명령을 사용 하 여 합니다.

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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Hello 데이터 로드
tooload hello 데이터 명령 프롬프트를 열고 다음 명령을, hello 값을 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호에 대 한 사용자의 정보로 대체 hello를 실행 합니다.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

이 명령은 tooverify hello 데이터가 제대로 로드 사용

```bcp
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

## <a name="next-steps"></a>다음 단계
SQL Server 데이터베이스 toomigrate 참조 [SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다.

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
