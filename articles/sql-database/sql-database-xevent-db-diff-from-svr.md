---
title: "SQL Database의 확장 이벤트| Microsoft Docs"
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
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="87c85-103">SQL Database의 확장 이벤트</span><span class="sxs-lookup"><span data-stu-id="87c85-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="87c85-104">이 항목은 Azure SQL Database의 확장 이벤트 구현과 Mirosoft SQL Server의 확장 이벤트 구현의 작은 차이점에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="87c85-105">SQL Database V12는 2015년 후반기 확장 이벤트 기능을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="87c85-106">SQL Server는 2008년 이후 확장 이벤트를 추가해 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="87c85-107">SQL Database의 확장 이벤트 기능 집합은 SQL Server 기능의 견고한 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="87c85-108">*XEvents*는 블로그 및 기타 비공식 위치에서 '확장 이벤트'를 가리키는 비공식적 별명입니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="87c85-109">Azure SQL Database 및 Microsoft SQL Server용 확장 이벤트에 대한 추가 정보는 다음에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="87c85-110">빠른 시작: SQL Server의 확장 이벤트</span><span class="sxs-lookup"><span data-stu-id="87c85-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="87c85-111">확장 이벤트</span><span class="sxs-lookup"><span data-stu-id="87c85-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="87c85-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="87c85-112">Prerequisites</span></span>

<span data-ttu-id="87c85-113">이 항목은 다음에 대한 어느 정도의 지식이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="87c85-114">[Azure SQL Database 서비스](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="87c85-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="87c85-115">Microsoft SQL Server의 [Extended events](http://msdn.microsoft.com/library/bb630282.aspx).</span><span class="sxs-lookup"><span data-stu-id="87c85-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="87c85-116">이 설명서에서 확장 이벤트에 대한 내용의 많은 부분이 SQL Server와 SQL Database에 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="87c85-117">이벤트 파일을 [대상](#AzureXEventsTargets)으로 선택할 경우 다음 항목에 대한 사전 지식이 있으면 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="87c85-118">Azure Storage 서비스</span><span class="sxs-lookup"><span data-stu-id="87c85-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="87c85-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87c85-119">PowerShell</span></span>
    - <span data-ttu-id="87c85-120">[Azure Storage와 함께 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md) - PowerShell 및 Azure Storage 서비스에 대한 포괄적 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="87c85-121">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="87c85-121">Code samples</span></span>

<span data-ttu-id="87c85-122">관련 항목에서 두 가지 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="87c85-123">SQL Database의 확장 이벤트에 대한 링 버퍼 대상 코드</span><span class="sxs-lookup"><span data-stu-id="87c85-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="87c85-124">짧고 간단한 Transact-SQL 스크립트.</span><span class="sxs-lookup"><span data-stu-id="87c85-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="87c85-125">코드 샘플 항목에서는 링 버퍼 대상을 마칠 때 alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` 문을 실행하여 리소스를 해제해야 함을 강조합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="87c85-126">나중에 `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`(으)로 링 버퍼의 다른 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="87c85-127">SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드</span><span class="sxs-lookup"><span data-stu-id="87c85-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="87c85-128">1단계는 Azure Storage 컨테이너를 만드는 PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="87c85-129">2단계는 Azure Storage 컨테이너를 사용하는 Transact-SQL입니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="87c85-130">Transact-SQL 차이점</span><span class="sxs-lookup"><span data-stu-id="87c85-130">Transact-SQL differences</span></span>


- <span data-ttu-id="87c85-131">SQL Server에서 [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) 명령을 사용하는 경우 **ON SERVER** 절을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="87c85-132">하지만 SQL Database에서는 대신 **ON DATABASE** 절을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="87c85-133">**ON DATABASE** 절은 [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) 및 [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL 명령에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="87c85-134">**CREATE EVENT SESSION** 또는 **ALTER EVENT SESSION** 문에 **STARTUP_STATE = ON**의 이벤트 세션 옵션을 포함하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="87c85-135">**= ON** 값은 장애 조치(failover)로 인해 논리적 데이터베이스를 재구성한 다음 자동 재시작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="87c85-136">새 카탈로그 뷰</span><span class="sxs-lookup"><span data-stu-id="87c85-136">New catalog views</span></span>

<span data-ttu-id="87c85-137">확장 이벤트 기능은 여러 [카탈로그 뷰](http://msdn.microsoft.com/library/ms174365.aspx)에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="87c85-138">카탈로그 뷰를 통해 현재 데이터베이스에서 사용자가 만든 이벤트 세션의 *메타데이터 또는 정의* 를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="87c85-139">뷰는 활성 이벤트 세션의 인스턴스에 대한 정보를 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="87c85-140">카탈로그 뷰의</span><span class="sxs-lookup"><span data-stu-id="87c85-140">Name of</span></span><br/><span data-ttu-id="87c85-141">이름</span><span class="sxs-lookup"><span data-stu-id="87c85-141">catalog view</span></span> | <span data-ttu-id="87c85-142">설명</span><span class="sxs-lookup"><span data-stu-id="87c85-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="87c85-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="87c85-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="87c85-144">이벤트 세션의 각 이벤트에 있는 각 작업에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="87c85-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="87c85-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="87c85-146">이벤트 세션의 각 이벤트에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="87c85-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="87c85-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="87c85-148">이벤트 및 대상에 명시적으로 설정된 사용자 지정 가능한 각 열에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="87c85-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="87c85-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="87c85-150">이벤트 세션의 각 이벤트 대상에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="87c85-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="87c85-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="87c85-152">SQL Database의 각 이벤트 세션에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="87c85-153">Microsoft SQL Server에서 유사한 카탈로그 뷰의 이름에는 *.database\_*가 아닌 *.server\_*가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="87c85-154">이름 패턴은 **sys.server_event_%**와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="87c85-155">새로운 [DMV](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="87c85-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="87c85-156">Azure SQL Database에는 확장 이벤트를 지원하는 [DMV(동적 관리 뷰)](http://msdn.microsoft.com/library/bb677293.aspx) 가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="87c85-157">DMV를 통해 *활성* 이벤트 세션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="87c85-158">DMV의 이름</span><span class="sxs-lookup"><span data-stu-id="87c85-158">Name of DMV</span></span> | <span data-ttu-id="87c85-159">설명</span><span class="sxs-lookup"><span data-stu-id="87c85-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="87c85-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="87c85-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="87c85-161">이벤트 세션 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="87c85-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="87c85-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="87c85-163">세션 이벤트에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-163">Returns information about session events.</span></span> |
| <span data-ttu-id="87c85-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="87c85-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="87c85-165">세션에 바인딩되는 개체에 대한 구성 값을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="87c85-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="87c85-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="87c85-167">세션 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="87c85-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="87c85-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="87c85-169">현재 데이터베이스로 범위가 한정된 각 이벤트 세션에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="87c85-170">Microsoft SQL Server에서 유사한 카탈로그 뷰는 다음과 같이 이름에 *\_database* 부분이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="87c85-171">**sys.dm_xe_sessions**, 이름 대신</span><span class="sxs-lookup"><span data-stu-id="87c85-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="87c85-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="87c85-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="87c85-173">둘 다에 공통적인 DMV</span><span class="sxs-lookup"><span data-stu-id="87c85-173">DMVs common to both</span></span>
<span data-ttu-id="87c85-174">확장 이벤트에는 Azure SQL Database와 Microsoft SQL Server에 공통적인 추가 DMV가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="87c85-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="87c85-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="87c85-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="87c85-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="87c85-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="87c85-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="87c85-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="87c85-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="87c85-179">사용 가능한 확장 이벤트, 동작, 대상 찾기</span><span class="sxs-lookup"><span data-stu-id="87c85-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="87c85-180">간단한 SQL **SELECT** 를 실행하여 사용 가능한 이벤트, 작업, 대상의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

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


<span data-ttu-id="87c85-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="87c85-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="87c85-182">SQL Database 이벤트 세션의 대상</span><span class="sxs-lookup"><span data-stu-id="87c85-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="87c85-183">SQL Database에서 이벤트 세션의 결과를 캡처할 수 있는 대상은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="87c85-184">[링 버퍼 대상](http://msdn.microsoft.com/library/ff878182.aspx) - 이벤트 데이터를 메모리에 잠시 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="87c85-185">[이벤트 카운터 대상](http://msdn.microsoft.com/library/ff878025.aspx) - 확장 이벤트 세션 동안 발생하는 모든 이벤트의 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="87c85-186">[이벤트 파일 대상](http://msdn.microsoft.com/library/ff878115.aspx) - Azure Storage 컨테이너에 전체 버퍼를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="87c85-187">[ETW(Windows 이벤트 추적)](http://msdn.microsoft.com/library/ms751538.aspx) API는 SQL Database의 확장 이벤트에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="87c85-188">제한</span><span class="sxs-lookup"><span data-stu-id="87c85-188">Restrictions</span></span>

<span data-ttu-id="87c85-189">SQL Database의 클라우드 환경에 적합한 몇 가지 보안 관련 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="87c85-190">확장 이벤트는 단일 테넌트 격리 모델에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="87c85-191">한 데이터베이스의 이벤트 세션은 다른 데이터베이스의 데이터 또는 이벤트에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="87c85-192">**마스터** 데이터베이스의 컨텍스트에서 **CREATE EVENT SESSION** 문을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="87c85-193">권한 모델</span><span class="sxs-lookup"><span data-stu-id="87c85-193">Permission model</span></span>

<span data-ttu-id="87c85-194">**CREATE EVENT SESSION** 문을 실행하려면 데이터베이스에 **제어** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="87c85-195">데이터베이스 소유자(dbo)는 **제어** 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="87c85-196">저장소 컨테이너 권한</span><span class="sxs-lookup"><span data-stu-id="87c85-196">Storage container authorizations</span></span>

<span data-ttu-id="87c85-197">Azure Storage 컨테이너에 대해 만드는 SAS 토큰은 권한에 대해 **rwl** 을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="87c85-198">**rwl** 값은 다음과 같은 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="87c85-199">읽기</span><span class="sxs-lookup"><span data-stu-id="87c85-199">Read</span></span>
- <span data-ttu-id="87c85-200">쓰기</span><span class="sxs-lookup"><span data-stu-id="87c85-200">Write</span></span>
- <span data-ttu-id="87c85-201">나열</span><span class="sxs-lookup"><span data-stu-id="87c85-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="87c85-202">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="87c85-202">Performance considerations</span></span>

<span data-ttu-id="87c85-203">확장 이벤트를 집중적으로 사용할 경우 전체 시스템에 안정적인 메모리보다 더 많은 활성 메모리가 누적되는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="87c85-204">따라서 Azure SQL Database 시스템은 이벤트 세션이 누적할 수 있는 활성 메모리의 양에 대한 한도를 동적으로 설정 및 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="87c85-205">많은 요소가 동적 계산에 활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="87c85-206">메모리 최대 한도가 적용되었다는 오류 메시지가 표시될 경우 다음과 같은 방법으로 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="87c85-207">실행하는 동시 이벤트 세션 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="87c85-208">이벤트 세션에 대한 **CREATE** 및 **ALTER** 문을 통해 **MAX\_MEMORY** 절에 지정하는 메모리의 양을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="87c85-209">네트워크 대기 시간</span><span class="sxs-lookup"><span data-stu-id="87c85-209">Network latency</span></span>

<span data-ttu-id="87c85-210">Azure Storage BLOB에 데이터를 유지하는 동안 **이벤트 파일** 대상에서 네트워크 지연 또는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="87c85-211">네트워크 통신이 완료될 때까지 기다리는 동안 SQL Database의 다른 이벤트가 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="87c85-212">이 지연으로 인해 워크로드가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="87c85-213">이러한 성능 위험을 줄이려면 이벤트 세션 정의에서 **EVENT_RETENTION_MODE** 옵션을 **NO_EVENT_LOSS**로 설정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="87c85-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="87c85-214">관련 링크</span><span class="sxs-lookup"><span data-stu-id="87c85-214">Related links</span></span>

- <span data-ttu-id="87c85-215">[Azure Storage와 함께 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="87c85-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="87c85-216">Azure Storage Cmdlet</span><span class="sxs-lookup"><span data-stu-id="87c85-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="87c85-217">[Azure Storage와 함께 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md) - PowerShell 및 Azure Storage 서비스에 대한 포괄적 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="87c85-218">.NET에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="87c85-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="87c85-219">CREATE CREDENTIAL(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="87c85-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="87c85-220">CREATE EVENT SESSION(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="87c85-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="87c85-221">Microsoft SQL Server의 확장 이벤트에 대한 Jonathan Kehayias의 블로그</span><span class="sxs-lookup"><span data-stu-id="87c85-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="87c85-222">Azure SQL Database에 대한 매개 변수로 범위가 좁혀지는 Azure *서비스 업데이트* 웹 페이지</span><span class="sxs-lookup"><span data-stu-id="87c85-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="87c85-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="87c85-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="87c85-224">확장 이벤트에 대한 다른 코드 샘플 항목은 다음 링크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="87c85-225">하지만 어느 샘플이든 Azure SQL Database와 Microsoft SQL Server 중 무엇을 대상으로 하는지 늘 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="87c85-226">그런 다음 샘플을 실행하기 위해 약간의 변경이 필요한지 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c85-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
