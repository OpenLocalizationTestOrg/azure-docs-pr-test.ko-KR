---
title: "SQL Database에 대한 XEvent 링 버퍼 코드 | Microsoft Docs"
description: "Azure SQL Database에서 링 버퍼 대상을 사용하여 편리하고 빨라진 Transact-SQL 코드 샘플을 제공합니다."
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
ms.openlocfilehash: 6fbefe151901ac3b15d93712422878fc4d6206f1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="a5cf5-103">SQL Database의 확장 이벤트에 대한 링 버퍼 대상 코드</span><span class="sxs-lookup"><span data-stu-id="a5cf5-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="a5cf5-104">테스트 중 확장 이벤트에 대한 정보를 캡처하고 보고하는 가장 쉽고 빠른 방법을 위한 전체 코드 샘플이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-104">You want a complete code sample for the easiest quick way to capture and report information for an extended event during a test.</span></span> <span data-ttu-id="a5cf5-105">확장 이벤트 데이터에 대한 가장 쉬운 대상은 [링 버퍼 대상](http://msdn.microsoft.com/library/ff878182.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-105">The easiest target for extended event data is the [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="a5cf5-106">이 항목에서는 다음을 수행하는 Transact-SQL 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="a5cf5-107">시연하는 데 사용할 데이터를 포함하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-107">Creates a table with data to demonstrate with.</span></span>
2. <span data-ttu-id="a5cf5-108">기존 확장 이벤트에 대한 세션 즉, **sqlserver.sql_statement_starting**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="a5cf5-109">이 이벤트는 특정 업데이트 문자열을 포함하는 SQL 문( **statement LIKE '%UPDATE tabEmployee%'**)으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-109">The event is limited to SQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="a5cf5-110">링 버퍼 유형의 대상 즉, **package0.ring_buffer**로 이벤트 출력을 보내도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-110">Chooses to send the output of the event to a target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="a5cf5-111">이벤트 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-111">Starts the event session.</span></span>
4. <span data-ttu-id="a5cf5-112">몇 가지 간단한 SQL UPDATE 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="a5cf5-113">SQL SELECT 문을 실행하여 링 버퍼에서 이벤트 출력을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-113">Issues a SQL SELECT statement to retrieve event output from the Ring Buffer.</span></span>
   
   * <span data-ttu-id="a5cf5-114">**sys.dm_xe_database_session_targets** 및 다른 DMV(동적 관리 뷰)가 조인됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="a5cf5-115">이벤트 세션을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-115">Stops the event session.</span></span>
7. <span data-ttu-id="a5cf5-116">링 버퍼 대상을 삭제하여 해당 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-116">Drops the Ring Buffer target, to release its resources.</span></span>
8. <span data-ttu-id="a5cf5-117">이벤트 세션 및 데모 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-117">Drops the event session and the demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5cf5-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a5cf5-118">Prerequisites</span></span>

* <span data-ttu-id="a5cf5-119">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="a5cf5-119">An Azure account and subscription.</span></span> <span data-ttu-id="a5cf5-120">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a5cf5-121">테이블을 만들 수 있는 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="a5cf5-122">또는 몇 분 이내에 [**AdventureWorksLT** 데모 데이터베이스를 만들](sql-database-get-started.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="a5cf5-123">SQL Server Management Studio(ssms.exe)(이상적으로 최신 월별 업데이트 버전).</span><span class="sxs-lookup"><span data-stu-id="a5cf5-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="a5cf5-124">다음 위치에서 최신 ssms.exe를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-124">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="a5cf5-125">[SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)항목</span><span class="sxs-lookup"><span data-stu-id="a5cf5-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="a5cf5-126">직접 다운로드 링크</span><span class="sxs-lookup"><span data-stu-id="a5cf5-126">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="a5cf5-127">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="a5cf5-127">Code sample</span></span>

<span data-ttu-id="a5cf5-128">다음 링 버퍼 코드 샘플은 약간만 수정하면 Azure SQL Database 또는 Microsoft SQL Server에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-128">With very minor modification, the following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="a5cf5-129">5단계의 FROM 절에 사용되는 일부 DMV(동적 관리 뷰) 이름에 '_database' 노드가 있다는 점이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-129">The difference is the presence of the node '_database' in the name of some dynamic management views (DMVs), used in the FROM clause in Step 5.</span></span> <span data-ttu-id="a5cf5-130">예:</span><span class="sxs-lookup"><span data-stu-id="a5cf5-130">For example:</span></span>

* <span data-ttu-id="a5cf5-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="a5cf5-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="a5cf5-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="a5cf5-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="a5cf5-133">링 버퍼 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="a5cf5-133">Ring Buffer contents</span></span>

<span data-ttu-id="a5cf5-134">ssms.exe를 사용하여 코드 샘플을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-134">We used ssms.exe to run the code sample.</span></span>

<span data-ttu-id="a5cf5-135">결과를 보기 위해 열 머리글 **target_data_XML** 아래의 셀을 클릭했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-135">To view the results, we clicked the cell under the column header **target_data_XML**.</span></span>

<span data-ttu-id="a5cf5-136">그런 다음 결과 창에서 열 머리글 **target_data_XML** 아래의 셀을 클릭했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-136">Then in the results pane we clicked the cell under the column header **target_data_XML**.</span></span> <span data-ttu-id="a5cf5-137">그러면 결과 셀의 콘텐츠가 XML로 표시된 다른 파일 탭이 ssms.exe에 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-137">This click created another file tab in ssms.exe in which the content of the result cell was displayed, as XML.</span></span>

<span data-ttu-id="a5cf5-138">출력은 다음 블록에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-138">The output is shown in the following block.</span></span> <span data-ttu-id="a5cf5-139">길어 보이지만 두 개의 **<event>** 요소뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="a5cf5-140">링 버퍼에서 보유한 리소스 해제</span><span class="sxs-lookup"><span data-stu-id="a5cf5-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="a5cf5-141">링 버퍼 사용을 마쳤으면 링 버퍼를 제거하고 다음과 같은 **ALTER** 를 실행하여 링 버퍼의 리소스를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like the following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="a5cf5-142">이벤트 세션의 정의는 삭제되지 않고 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-142">The definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="a5cf5-143">나중에 이벤트 세션에 링 버퍼의 다른 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-143">Later you can add another instance of the Ring Buffer to your event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="a5cf5-144">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a5cf5-144">More information</span></span>

<span data-ttu-id="a5cf5-145">Azure SQL Database의 확장 이벤트에 대한 기본 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-145">The primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="a5cf5-146">[SQL Database의 확장 이벤트 고려 사항](sql-database-xevent-db-diff-from-svr.md): Microsoft SQL Server와 Azure SQL Database 간에 다른 확장 이벤트의 일부 측면을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="a5cf5-147">확장 이벤트에 대한 다른 코드 샘플 항목은 다음 링크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-147">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="a5cf5-148">하지만 어느 샘플이든 Azure SQL Database와 Microsoft SQL Server 중 무엇을 대상으로 하는지 늘 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-148">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="a5cf5-149">그런 다음 샘플을 실행하기 위해 약간의 변경이 필요한지 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5cf5-149">Then you can decide whether minor changes are needed to run the sample.</span></span>

* <span data-ttu-id="a5cf5-150">Azure SQL Database에 대한 코드 샘플: [SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="a5cf5-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
