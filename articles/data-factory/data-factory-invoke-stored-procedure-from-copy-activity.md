---
title: "aaaInvoke 저장 프로시저에서 Azure 데이터 팩터리 복사 작업 | Microsoft Docs"
description: "Azure Data Factory에서 SQL Server 나 Azure SQL 데이터베이스의 저장된 프로시저 tooinvoke 활동을 복사 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Azure Data Factory의 복사 작업에서 저장 프로시저 호출
데이터를 복사 하는 경우 [SQL Server](data-factory-sqlserver-connector.md) 또는 [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md), hello를 구성할 수 있습니다 **SqlSink** 복사 활동 tooinvoke 저장된 프로시저에에서 있습니다. Toouse hello 저장 프로시저 tooperform toohello 대상 테이블에 데이터를 삽입 하기 전에 (여러 등 공용 테이블에 삽입 값 조회 열 병합) 추가로 처리 해야 할 수 있습니다. 이 기능은 [테이블 값 매개 변수](https://msdn.microsoft.com/library/bb675163.aspx)을 활용합니다. 

다음 예제는 hello 방법을 tooinvoke SQL Server에서 저장된 프로시저에서에서 데이터베이스를 데이터 팩토리 파이프라인 (복사 작업)를 보여 줍니다.  

## <a name="output-dataset-json"></a>출력 데이터 집합 JSON
Hello 출력 데이터 집합 JSON 설정 hello **형식** 를: **SqlServerTable**합니다. 너무 설정**AzureSqlTable** toouse Azure SQL 데이터베이스입니다. 값에 대 한 hello **tableName** 속성 hello hello 저장 프로시저의 첫 번째 매개 변수 이름을 일치 해야 합니다.  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a>복사 작업 JSON의 SqlSink 섹션
Hello 정의 **SqlSink** hello 복사 활동 JSON에서에서 다음과 같은 섹션. tooinvoke hello 싱크/대상 데이터베이스에 데이터를 삽입 하는 동안 저장된 프로시저 모두에 대 한 값을 지정 **SqlWriterStoredProcedureName** 및 **SqlWriterTableType** 속성입니다. 이러한 속성의 설명에 대 한 참조 [hello SQL Server 커넥터 문서의 SqlSink 섹션](data-factory-sqlserver-connector.md#sqlsink)합니다.

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a>저장 프로시저 정의 
데이터베이스에 이름이 hello로 hello 저장 프로시저를 정의 **SqlWriterStoredProcedureName**합니다. hello 저장 프로시저 hello 원본 데이터 저장소에서 입력된 데이터를 처리 하 고 hello 대상 데이터베이스의 테이블로 데이터를 삽입 합니다. 저장된 프로시저의 첫 번째 매개 변수 hello의 hello 이름 hello 데이터 집합 JSON (마케팅)에 정의 된 hello tableName 일치 해야 합니다.

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>테이블 유형 정의
데이터베이스에 hello로 이름과 같은 이름을 사용 하는 hello 테이블 형식을 정의 **SqlWriterTableType**합니다. hello 테이블 형식의 hello 스키마에는 hello 입력된 데이터 집합의 hello 스키마와 일치 해야 합니다.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>다음 단계
커넥터 문서에 대 한 완전 한 JSON 예제를 따르는 hello를 검토 합니다. 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
