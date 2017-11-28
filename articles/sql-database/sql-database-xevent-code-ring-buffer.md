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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="f4089-103">SQL Database의 확장 이벤트에 대한 링 버퍼 대상 코드</span><span class="sxs-lookup"><span data-stu-id="f4089-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="f4089-104">원하는 hello 쉬운 신속 하 게 toocapture 및 보고서에 대 한 정보는 확장된 이벤트 테스트 하는 동안에 대 한 전체 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="f4089-105">확장된 이벤트 데이터에 대 한 쉬운 대상 hello는 hello [링 버퍼 대상](http://msdn.microsoft.com/library/ff878182.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="f4089-106">이 항목에서는 다음을 수행하는 Transact-SQL 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="f4089-107">와 데이터 toodemonstrate 있는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="f4089-108">기존 확장 이벤트에 대한 세션 즉, **sqlserver.sql_statement_starting**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="f4089-109">hello 이벤트는 특정 업데이트 문자열을 포함 하는 제한 된 tooSQL 문은: **'업데이트 tabEmployee % %'와 같은 문을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="f4089-110">Hello 이벤트 tooa 형식이 링 버퍼 대상의 toosend hello 출력 즉 선택 **package0.ring_buffer**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="f4089-111">Hello 이벤트 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-111">Starts hello event session.</span></span>
4. <span data-ttu-id="f4089-112">몇 가지 간단한 SQL UPDATE 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="f4089-113">SQL SELECT 문을 tooretrieve 이벤트 출력을 hello 링 버퍼에서에서 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="f4089-114">**sys.dm_xe_database_session_targets** 및 다른 DMV(동적 관리 뷰)가 조인됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="f4089-115">Hello 이벤트 세션을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-115">Stops hello event session.</span></span>
7. <span data-ttu-id="f4089-116">삭제 합니다. 해당 리소스를 링 버퍼 대상, toorelease hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="f4089-117">Hello 이벤트 세션 및 hello 데모 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4089-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4089-118">Prerequisites</span></span>

* <span data-ttu-id="f4089-119">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="f4089-119">An Azure account and subscription.</span></span> <span data-ttu-id="f4089-120">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f4089-121">테이블을 만들 수 있는 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="f4089-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="f4089-122">또는 몇 분 이내에 [**AdventureWorksLT** 데모 데이터베이스를 만들](sql-database-get-started.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="f4089-123">SQL Server Management Studio(ssms.exe)(이상적으로 최신 월별 업데이트 버전).</span><span class="sxs-lookup"><span data-stu-id="f4089-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="f4089-124">Hello 최신 ssms.exe에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="f4089-125">[SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)항목</span><span class="sxs-lookup"><span data-stu-id="f4089-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="f4089-126">직접 링크 toohello 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="f4089-127">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="f4089-127">Code sample</span></span>

<span data-ttu-id="f4089-128">매우 사소한 수정 hello 링 버퍼 및 다음 코드 샘플 수에서 실행할 수 Azure SQL 데이터베이스 또는 Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4089-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="f4089-129">hello 차이가 5 단계에서에서 hello FROM 절에 사용 되는 일부 동적 관리 뷰 (Dmv)의 hello 이름에 ' 만족할' hello 노드의 hello 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="f4089-130">예:</span><span class="sxs-lookup"><span data-stu-id="f4089-130">For example:</span></span>

* <span data-ttu-id="f4089-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="f4089-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="f4089-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="f4089-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="f4089-133">링 버퍼 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="f4089-133">Ring Buffer contents</span></span>

<span data-ttu-id="f4089-134">Ssms.exe toorun hello 코드 샘플을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="f4089-135">tooview hello 결과 클릭 hello 셀 hello 열 머리글 아래에서 **target_data_XML**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="f4089-136">Hello 결과 창에 hello 열 머리글 아래에서 hello 셀 클릭 한 다음 **target_data_XML**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="f4089-137">다른 파일 탭은 hello에 hello 결과 셀의 내용을 표시 된, XML로 ssms.exe에서 만든 하는이를이 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="f4089-138">hello 출력 hello 블록 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="f4089-139">길어 보이지만 두 개의 **<event>** 요소뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="f4089-140">링 버퍼에서 보유한 리소스 해제</span><span class="sxs-lookup"><span data-stu-id="f4089-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="f4089-141">링 버퍼를 완료 하는 경우 제거 하 고 실행 하는 해당 리소스를 해제 수는 **ALTER** hello 다음과 같은:</span><span class="sxs-lookup"><span data-stu-id="f4089-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="f4089-142">이벤트 세션의 hello 정의 업데이트는 되지만 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="f4089-143">나중에 hello 링 버퍼 tooyour 이벤트 세션의 다른 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="f4089-144">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f4089-144">More information</span></span>

<span data-ttu-id="f4089-145">Azure SQL 데이터베이스에서 확장된 이벤트에 대 한 hello 기본 항목은입니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="f4089-146">[SQL Database의 확장 이벤트 고려 사항](sql-database-xevent-db-diff-from-svr.md): Microsoft SQL Server와 Azure SQL Database 간에 다른 확장 이벤트의 일부 측면을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="f4089-147">확장된 이벤트에 대 한 다른 코드 샘플 항목에 링크를 따라 hello에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="f4089-148">그러나 모든 샘플 toosee 체크 정기적으로 hello 샘플 Microsoft SQL Server와 Azure SQL 데이터베이스를 대상으로 하는지 여부를.</span><span class="sxs-lookup"><span data-stu-id="f4089-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="f4089-149">그런 다음 약간의 변경이 필요한 toorun hello 샘플 지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4089-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="f4089-150">Azure SQL Database에 대한 코드 샘플: [SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="f4089-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
