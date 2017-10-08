---
title: "SQL 데이터베이스에 대 한 링 버퍼 코드 aaaXEvent | Microsoft Docs"
description: "Azure SQL 데이터베이스의 hello 링 버퍼 대상 사용 하 여 쉽게 만들고 빠른 만들어지는 Transact SQL 코드 예제를 제공 합니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>SQL Database의 확장 이벤트에 대한 링 버퍼 대상 코드

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

원하는 hello 쉬운 신속 하 게 toocapture 및 보고서에 대 한 정보는 확장된 이벤트 테스트 하는 동안에 대 한 전체 코드 샘플입니다. 확장된 이벤트 데이터에 대 한 쉬운 대상 hello는 hello [링 버퍼 대상](http://msdn.microsoft.com/library/ff878182.aspx)합니다.

이 항목에서는 다음을 수행하는 Transact-SQL 코드 샘플을 제공합니다.

1. 와 데이터 toodemonstrate 있는 테이블을 만듭니다.
2. 기존 확장 이벤트에 대한 세션 즉, **sqlserver.sql_statement_starting**을 만듭니다.
   
   * hello 이벤트는 특정 업데이트 문자열을 포함 하는 제한 된 tooSQL 문은: **'업데이트 tabEmployee % %'와 같은 문을**합니다.
   * Hello 이벤트 tooa 형식이 링 버퍼 대상의 toosend hello 출력 즉 선택 **package0.ring_buffer**합니다.
3. Hello 이벤트 세션을 시작합니다.
4. 몇 가지 간단한 SQL UPDATE 문을 실행합니다.
5. SQL SELECT 문을 tooretrieve 이벤트 출력을 hello 링 버퍼에서에서 발급합니다.
   
   * **sys.dm_xe_database_session_targets** 및 다른 DMV(동적 관리 뷰)가 조인됩니다.
6. Hello 이벤트 세션을 중지합니다.
7. 삭제 합니다. 해당 리소스를 링 버퍼 대상, toorelease hello 합니다.
8. Hello 이벤트 세션 및 hello 데모 테이블을 삭제합니다.

## <a name="prerequisites"></a>필수 조건

* Azure 계정 및 구독 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* 테이블을 만들 수 있는 데이터베이스.
  
  * 또는 몇 분 이내에 [**AdventureWorksLT** 데모 데이터베이스를 만들](sql-database-get-started.md) 수 있습니다.
* SQL Server Management Studio(ssms.exe)(이상적으로 최신 월별 업데이트 버전). 
  Hello 최신 ssms.exe에서 다운로드할 수 있습니다.
  
  * [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)항목
  * [직접 링크 toohello 다운로드 합니다.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>코드 샘플

매우 사소한 수정 hello 링 버퍼 및 다음 코드 샘플 수에서 실행할 수 Azure SQL 데이터베이스 또는 Microsoft SQL Server. hello 차이가 5 단계에서에서 hello FROM 절에 사용 되는 일부 동적 관리 뷰 (Dmv)의 hello 이름에 ' 만족할' hello 노드의 hello 존재 합니다. 예:

* sys.dm_xe**_database**_session_targets
* sys.dm_xe_session_targets

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a>링 버퍼 콘텐츠

Ssms.exe toorun hello 코드 샘플을 사용 했습니다.

tooview hello 결과 클릭 hello 셀 hello 열 머리글 아래에서 **target_data_XML**합니다.

Hello 결과 창에 hello 열 머리글 아래에서 hello 셀 클릭 한 다음 **target_data_XML**합니다. 다른 파일 탭은 hello에 hello 결과 셀의 내용을 표시 된, XML로 ssms.exe에서 만든 하는이를이 클릭 합니다.

hello 출력 hello 블록 뒤에 표시 됩니다. 길어 보이지만 두 개의 **<event>** 요소뿐입니다.

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a>링 버퍼에서 보유한 리소스 해제

링 버퍼를 완료 하는 경우 제거 하 고 실행 하는 해당 리소스를 해제 수는 **ALTER** hello 다음과 같은:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


이벤트 세션의 hello 정의 업데이트는 되지만 삭제 되지 않습니다. 나중에 hello 링 버퍼 tooyour 이벤트 세션의 다른 인스턴스를 추가할 수 있습니다.

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>자세한 정보

Azure SQL 데이터베이스에서 확장된 이벤트에 대 한 hello 기본 항목은입니다.

* [SQL Database의 확장 이벤트 고려 사항](sql-database-xevent-db-diff-from-svr.md): Microsoft SQL Server와 Azure SQL Database 간에 다른 확장 이벤트의 일부 측면을 비교합니다.

확장된 이벤트에 대 한 다른 코드 샘플 항목에 링크를 따라 hello에서 제공 됩니다. 그러나 모든 샘플 toosee 체크 정기적으로 hello 샘플 Microsoft SQL Server와 Azure SQL 데이터베이스를 대상으로 하는지 여부를. 그런 다음 약간의 변경이 필요한 toorun hello 샘플 지 여부를 결정할 수 있습니다.

* Azure SQL Database에 대한 코드 샘플: [SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
