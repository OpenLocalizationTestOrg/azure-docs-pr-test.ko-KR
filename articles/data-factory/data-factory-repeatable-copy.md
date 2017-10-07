---
title: "Azure 데이터 팩터리에서 aaaRepeatable 복사 | Microsoft Docs"
description: "데이터를 복사 하는 조각을 두 번 이상 실행 되는 경우에 tooavoid을 복제 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Azure Data Factory에서 반복 가능한 복사

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.  
 
> [!NOTE]
> hello 다음 샘플은 Azure sql 있지만 사각형 데이터 집합을 지 원하는 해당 tooany 데이터 저장소입니다. Tooadjust hello를 할 수 있습니다 **형식** 원본과 hello의 **쿼리** 속성 (예: sqlReaderQuery 대신 쿼리) hello 데이터를 저장 합니다.   

일반적으로, 관계형 저장소를 읽을 때 tooread hello 데이터만 toothat 분할 영역에 해당 합니다. 따라서 방식으로 toodo Azure Data Factory에서 hello WindowStart 및 WindowEnd 시스템 사용할 수 있는 변수를 사용 하 여 것입니다. Hello 변수와 hello에서 Azure 데이터 팩터리에서 여기 함수에 대 한 읽기 [Azure 데이터 팩터리-함수 및 시스템 변수](data-factory-functions-variables.md) 문서. 예제: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
이 쿼리는 hello MyTable 테이블에서 hello 지속 시간 범위 조각 (WindowStart WindowEnd을->)에 해당 데이터를 읽습니다. 이 조각의 다시 실행 하십시오. 동일한 데이터를 읽는 해당 hello를 확인 항상 합니다. 

경우에 따라 tooread hello에 대 한 전체 테이블을 할 수 있습니다 및 hello sqlReaderQuery를 다음과 같이 정의할 수 있습니다.

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>반복 가능한 쓰기 tooSqlSink
데이터를 너무 복사할 때**Azure SQL/SQL Server** tookeep 반복성 유의 tooavoid에 필요한 다른 데이터 저장소에서 의도 하지 않은 결과입니다. 

데이터 tooAzure SQL/SQL Server 데이터베이스를 복사할 때 hello 복사 활동 기본적으로 데이터 toohello 싱크 테이블을 추가 합니다. 예를 들어에서 복사 하는 데이터는 CSV (쉼표로 구분 된 값) 파일 포함 된 두 개의 레코드 toohello 다음 표에 Azure SQL/SQL Server 데이터베이스에 있습니다. 조각 실행 되 면 hello 두 레코드는 복사한 toohello SQL 테이블 됩니다. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

소스 파일에서 오류를 발견 하 고 2 too4에서 아래로 튜브의 hello 수량을 업데이트 한다고 가정 합니다. 다시 실행 하면 hello 데이터 조각이 해당 기간에 대해 수동으로, tooAzure SQL/SQL Server 데이터베이스를 추가 하는 두 개의 새 레코드를 찾을 수 있습니다. 이 예에서는 primary key 제약 조건을 hello에 없는 hello 테이블의 열 hello 가정 합니다.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid hello 다음 두 가지 메커니즘 중 하나를 사용 하 여 toospecify UPSERT 의미 체계를 필요한이 동작을 합니다.

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>메커니즘 1: sqlWriterCleanupScript 사용
Hello를 사용할 수 있습니다 **sqlWriterCleanupScript** 조각이 실행 될 때 hello 데이터를 삽입 하기 전에 hello 싱크 테이블에서 데이터를 속성 tooclean 합니다. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

조각 실행 되 면 hello 정리 스크립트 toohello 조각 hello SQL 테이블에서 해당 하는 첫 번째 toodelete 데이터 실행 됩니다. hello 복사 작업은 다음 데이터 hello SQL 테이블에 삽입 합니다. Hello 수량이 업데이트는 hello 분할 영역을 다시 실행 하는 경우 원하는 대로 합니다.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Hello 원래 csv에서 hello 플랫 와셔 레코드를 제거 하는 가정 합니다. 그런 다음 hello 조각을 다시 실행 결과 다음 hello을 생성 합니다. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

hello 복사 활동 hello 정리 스크립트 toodelete hello 해당 데이터에 대 한 해당 조각의 실행 했습니다. (다음 레코드를 하나만 포함 됨)는 hello csv에서 hello 입력을 읽은 다음 hello 테이블에 삽입 합니다. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>메커니즘 2: sliceIdentifierColumnName 사용
> [!IMPORTANT]
> 현재 sliceIdentifierColumnName은 Azure SQL Data Warehouse에 지원되지 않습니다. 

두 번째 메커니즘 tooachieve 반복성 hello는 hello 대상 테이블에에서는 전용된 열 (sliceIdentifierColumnName) 것입니다. 이 열은 Azure Data Factory tooensure hello 원본 및 대상 된 상태로 유지 되 동기화에서 사용 됩니다. 이 방법은 더 변경 하거나 hello 대상 SQL 테이블 스키마 정의에 유연성을 제공 하는 경우에 작동 합니다. 

이 열은 반복성을 위해 Azure 데이터 팩터리에서 사용 하 고 hello 프로세스에서 Azure 데이터 팩터리 어떤 스키마도 미치지 않으며 toohello 테이블을 변경 합니다. 방법은 toouse이 방법을이 사용 합니다.

1. 형식의 열을 정의 **이진 (32)** hello 대상 SQL 테이블에에서 있습니다. 이 열에는 제약 조건이 없어야 합니다. 이 예에서는 이 열의 이름을 AdfSliceIdentifier라고 하겠습니다.


    원본 테이블:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    대상 테이블: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. 다음과 같이 hello 복사 활동에서 사용 합니다.
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Azure Data Factory 필요에 따라이 열을 채웁니다 tooensure hello 원본 및 대상 동기화 상태를 유지 합니다. 이 열의 hello 값이이 컨텍스트 외부에서 사용할 수 없습니다. 

비슷한 toomechanism 1, 복사 작업은 자동으로 hello 대상 SQL 테이블에서에서 분할 영역을 제공 하는 hello에 대 한 hello 데이터를 정리 합니다. 그런 다음 toohello 대상 테이블의 원본에서 데이터를 삽입합니다. 

## <a name="next-steps"></a>다음 단계
커넥터 문서에 대 한 완전 한 JSON 예제를 따르는 hello를 검토 합니다. 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)