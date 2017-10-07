---
title: "SQL 데이터베이스의 aaaExtended 이벤트 | Microsoft Docs"
description: "Azure SQL Database의 확장 이벤트(XEvent)와 Microsoft SQL Server의 이벤트 세션 간 차이점에 대해 설명합니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a>SQL Database의 확장 이벤트
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

이 방법을 hello Azure SQL 데이터베이스의 확장된 이벤트에는 Microsoft SQL Server에 비해 약간 다른 tooextended 이벤트 설명 합니다.

- SQL 데이터베이스 V12 얻은 hello 확장된 이벤트 기능 hello에 두 번째 달력 2015의 절반입니다.
- SQL Server는 2008년 이후 확장 이벤트를 추가해 왔습니다.
- SQL 데이터베이스에서 확장된 이벤트의 hello 기능 집합은 강력한 SQL Server에서 hello 기능 하위 집합입니다.

*XEvents*는 블로그 및 기타 비공식 위치에서 '확장 이벤트'를 가리키는 비공식적 별명입니다.

Azure SQL Database 및 Microsoft SQL Server용 확장 이벤트에 대한 추가 정보는 다음에 제공됩니다.

- [빠른 시작: SQL Server의 확장 이벤트](http://msdn.microsoft.com/library/mt733217.aspx)
- [확장 이벤트](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>필수 조건

이 항목은 다음에 대한 어느 정도의 지식이 있는 것으로 가정합니다.

- [Azure SQL Database 서비스](https://azure.microsoft.com/services/sql-database/).
- Microsoft SQL Server의 [Extended events](http://msdn.microsoft.com/library/bb630282.aspx).

- 확장된 이벤트에 대 한 설명서의 hello 대량 tooboth SQL Server 및 SQL 데이터베이스에 적용합니다.

Hello hello로 이벤트 파일을 선택할 때 다음 항목 이전 노출 toohello 유용 [대상](#AzureXEventsTargets):

- [Azure Storage 서비스](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [Azure PowerShell을 사용 하 여 Azure 저장소와](../storage/common/storage-powershell-guide-full.md) -PowerShell 및 hello Azure 저장소 서비스에 대 한 포괄적인 정보를 제공 합니다.

## <a name="code-samples"></a>코드 샘플

관련 항목에서 두 가지 코드 샘플을 제공합니다.


- [SQL Database의 확장 이벤트에 대한 링 버퍼 대상 코드](sql-database-xevent-code-ring-buffer.md)
    - 짧고 간단한 Transact-SQL 스크립트.
    - 링 버퍼 대상을 사용 하 여 완료 되 면 alter 놓기를 실행 하 여 해당 리소스를 해제 해야 하는 hello 코드 샘플 항목의 내용을 강조 `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` 문. 나중에 `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`(으)로 링 버퍼의 다른 인스턴스를 추가할 수 있습니다.


- [SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드](sql-database-xevent-code-event-file.md)
    - 1 단계에는 PowerShell toocreate Azure 저장소 컨테이너입니다.
    - 단계 2는 hello Azure 저장소 컨테이너를 사용 하는 TRANSACT-SQL입니다.

## <a name="transact-sql-differences"></a>Transact-SQL 차이점


- Hello를 실행 하는 동안 [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) hello를 사용 하 여 SQL Server 명령을 **ON SERVER** 절. Hello를 사용 하면 SQL 데이터베이스에서 하지만 **ON DATABASE** 절 대신 합니다.


- hello **ON DATABASE** toohello 절에도 적용 됩니다 [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) 및 [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) TRANSACT-SQL 명령입니다.


- 가장 좋은 방법은 tooinclude hello 이벤트 세션 옵션의 **STARTUP_STATE = ON** 에 프로그램 **CREATE EVENT SESSION** 또는 **ALTER EVENT SESSION** 문.
    - hello **= ON** 값 tooa 장애 조치 인해 hello 논리적 데이터베이스의 재구성 후 자동 다시 시작을 지원 합니다.

## <a name="new-catalog-views"></a>새 카탈로그 뷰

hello 확장된 이벤트에서 지 원하는 기능 여러 [카탈로그 뷰](http://msdn.microsoft.com/library/ms174365.aspx)합니다. 카탈로그 뷰에 대해 알려줄 *메타 데이터 또는 정의* hello 현재 데이터베이스의 사용자가 만든 이벤트 세션의 합니다. hello 뷰는 활성 이벤트 세션의 인스턴스에 대 한 정보를 반환 하지 않습니다.

| 카탈로그 뷰의<br/>이름 | 설명 |
|:--- |:--- |
| **sys.database_event_session_actions** |이벤트 세션의 각 이벤트에 있는 각 작업에 대한 행을 반환합니다. |
| **sys.database_event_session_events** |이벤트 세션의 각 이벤트에 대한 행을 반환합니다. |
| **sys.database_event_session_fields** |이벤트 및 대상에 명시적으로 설정된 사용자 지정 가능한 각 열에 대한 행을 반환합니다. |
| **sys.database_event_session_targets** |이벤트 세션의 각 이벤트 대상에 대한 행을 반환합니다. |
| **sys.database_event_sessions** |Hello SQL 데이터베이스 데이터베이스의 각 이벤트 세션에 대 한 행을 반환합니다. |

Microsoft SQL Server에서 유사한 카탈로그 뷰의 이름에는 *.database\_*가 아닌 *.server\_*가 포함됩니다. 같은 hello 이름 패턴은 **sys.server_event_%**합니다.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>새로운 [DMV](http://msdn.microsoft.com/library/ms188754.aspx)

Azure SQL Database에는 확장 이벤트를 지원하는 [DMV(동적 관리 뷰)](http://msdn.microsoft.com/library/bb677293.aspx) 가 있습니다. DMV를 통해 *활성* 이벤트 세션을 확인할 수 있습니다.

| DMV의 이름 | 설명 |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |이벤트 세션 작업에 대한 정보를 반환합니다. |
| **sys.dm_xe_database_session_events** |세션 이벤트에 대한 정보를 반환합니다. |
| **sys.dm_xe_database_session_object_columns** |바인딩된 tooa 세션 개체에 대 한 hello 구성 값을 표시 합니다. |
| **sys.dm_xe_database_session_targets** |세션 작업에 대한 정보를 반환합니다. |
| **sys.dm_xe_database_sessions** |범위가 지정 된 toohello 현재 데이터베이스는 각 이벤트 세션에 대 한 행을 반환 합니다. |

Microsoft SQL Server에서 유사한 카탈로그 뷰 hello 없이 이름은  *\_데이터베이스* 같은 hello의 부분 이름:

- **sys.dm_xe_sessions**, 이름 대신<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>일반적인 tooboth Dmv
확장된 이벤트에는 일반적인 tooboth Azure SQL 데이터베이스는 추가 Dmv 및 Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Hello 사용 가능한 확장된 이벤트, 동작 및 대상 찾기

단순한 SQL을 실행할 수 있습니다 **선택** tooobtain hello 사용 가능한 이벤트, 동작 및 대상의 목록입니다.

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>SQL Database 이벤트 세션의 대상

SQL Database에서 이벤트 세션의 결과를 캡처할 수 있는 대상은 다음과 같습니다.

- [링 버퍼 대상](http://msdn.microsoft.com/library/ff878182.aspx) - 이벤트 데이터를 메모리에 잠시 보관합니다.
- [이벤트 카운터 대상](http://msdn.microsoft.com/library/ff878025.aspx) - 확장 이벤트 세션 동안 발생하는 모든 이벤트의 수를 계산합니다.
- [이벤트 파일 대상을](http://msdn.microsoft.com/library/ff878115.aspx) -쓰기 전체 버퍼 tooan Azure 저장소 컨테이너입니다.

hello [이벤트 추적에 대 한 ETW (Windows)](http://msdn.microsoft.com/library/ms751538.aspx) API는 SQL 데이터베이스에서 확장된 이벤트에 사용할 수 없습니다.

## <a name="restrictions"></a>제한

SQL 데이터베이스의 hello 클라우드 환경 befitting 보안 관련 차이점 몇 가지가 있습니다.

- 확장된 이벤트는 hello 단일 테 넌 트 격리 모델에 기초로 합니다. 한 데이터베이스의 이벤트 세션은 다른 데이터베이스의 데이터 또는 이벤트에 액세스할 수 없습니다.
- 실행할 수 없는 **CREATE EVENT SESSION** hello의 hello 컨텍스트에서 문을 **마스터** 데이터베이스입니다.

## <a name="permission-model"></a>권한 모델

있어야 **제어** 데이터베이스 tooissue hello에 대 한 권한이 **CREATE EVENT SESSION** 문. hello 데이터베이스 소유자 (dbo)에 **제어** 권한.

### <a name="storage-container-authorizations"></a>저장소 컨테이너 권한

hello SAS 토큰을 지정 해야 Azure 저장소 컨테이너에 대 한 생성 **rwl** hello 사용 권한에 대 한 합니다. hello **rwl** hello 다음 권한을 제공 하는 값:

- 읽기
- 쓰기
- 나열

## <a name="performance-considerations"></a>성능 고려 사항

확장된 이벤트를 많이 사용 빈도가 높은 메모리는 hello에 대 한 정상 보다 누적 될 수 있는 시나리오 전반적인 시스템입니다. 따라서 hello Azure SQL 데이터베이스 시스템 동적으로 설정 하 고 조정 hello 이벤트 세션에 의해 누적 될 수 있는 활성 메모리 양 제한 합니다. 다양 한 요인 hello 동적 계산으로 이동합니다.

메모리 최대 한도가 적용되었다는 오류 메시지가 표시될 경우 다음과 같은 방법으로 해결할 수 있습니다.

- 실행하는 동시 이벤트 세션 수를 줄입니다.
- 통해 프로그램 **만들기** 및 **ALTER** 이벤트 세션에 대 한 문을 hello hello에서 지정 하는 메모리 양을 줄일 **최대\_메모리** 절.

### <a name="network-latency"></a>네트워크 대기 시간

hello **이벤트 파일** 대상 네트워크 대기 시간 또는 저장소 blob 데이터 tooAzure 유지 하는 동안 오류가 발생할 수 있습니다. SQL 데이터베이스의 다른 이벤트 hello 네트워크 통신 toocomplete를 기다리는 동안 지연 될 수 있습니다. 이 지연으로 인해 워크로드가 느려질 수 있습니다.

- toomitigate이이 성능 위험, hello를 설정 하지 마십시오 **EVENT_RETENTION_MODE** 옵션**NO_EVENT_LOSS** 에서 이벤트 세션 정의 합니다.

## <a name="related-links"></a>관련 링크

- [Azure Storage와 함께 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md)
- [Azure Storage Cmdlet](http://msdn.microsoft.com/library/dn806401.aspx)
- [Azure PowerShell을 사용 하 여 Azure 저장소와](../storage/common/storage-powershell-guide-full.md) -PowerShell 및 hello Azure 저장소 서비스에 대 한 포괄적인 정보를 제공 합니다.
- [어떻게 toouse.NET에서 Blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL(Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREATE EVENT SESSION(Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Microsoft SQL Server의 확장 이벤트에 대한 Jonathan Kehayias의 블로그](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Azure hello *서비스 업데이트* 웹 페이지에서 SQL 데이터베이스 매개 변수 tooAzure 좁혀집니다.
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


확장된 이벤트에 대 한 다른 코드 샘플 항목에 링크를 따라 hello에서 제공 됩니다. 그러나 모든 샘플 toosee 체크 정기적으로 hello 샘플 Microsoft SQL Server와 Azure SQL 데이터베이스를 대상으로 하는지 여부를. 그런 다음 약간의 변경이 필요한 toorun hello 샘플 지 여부를 결정할 수 있습니다.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
