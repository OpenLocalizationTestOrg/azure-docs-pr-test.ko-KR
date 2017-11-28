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
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="7d8a9-103">SQL Database의 확장 이벤트</span><span class="sxs-lookup"><span data-stu-id="7d8a9-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="7d8a9-104">이 방법을 hello Azure SQL 데이터베이스의 확장된 이벤트에는 Microsoft SQL Server에 비해 약간 다른 tooextended 이벤트 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="7d8a9-105">SQL 데이터베이스 V12 얻은 hello 확장된 이벤트 기능 hello에 두 번째 달력 2015의 절반입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="7d8a9-106">SQL Server는 2008년 이후 확장 이벤트를 추가해 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="7d8a9-107">SQL 데이터베이스에서 확장된 이벤트의 hello 기능 집합은 강력한 SQL Server에서 hello 기능 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="7d8a9-108">*XEvents*는 블로그 및 기타 비공식 위치에서 '확장 이벤트'를 가리키는 비공식적 별명입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="7d8a9-109">Azure SQL Database 및 Microsoft SQL Server용 확장 이벤트에 대한 추가 정보는 다음에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="7d8a9-110">빠른 시작: SQL Server의 확장 이벤트</span><span class="sxs-lookup"><span data-stu-id="7d8a9-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="7d8a9-111">확장 이벤트</span><span class="sxs-lookup"><span data-stu-id="7d8a9-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="7d8a9-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7d8a9-112">Prerequisites</span></span>

<span data-ttu-id="7d8a9-113">이 항목은 다음에 대한 어느 정도의 지식이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="7d8a9-114">[Azure SQL Database 서비스](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="7d8a9-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="7d8a9-115">Microsoft SQL Server의 [Extended events](http://msdn.microsoft.com/library/bb630282.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d8a9-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="7d8a9-116">확장된 이벤트에 대 한 설명서의 hello 대량 tooboth SQL Server 및 SQL 데이터베이스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="7d8a9-117">Hello hello로 이벤트 파일을 선택할 때 다음 항목 이전 노출 toohello 유용 [대상](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="7d8a9-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="7d8a9-118">Azure Storage 서비스</span><span class="sxs-lookup"><span data-stu-id="7d8a9-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="7d8a9-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d8a9-119">PowerShell</span></span>
    - <span data-ttu-id="7d8a9-120">[Azure PowerShell을 사용 하 여 Azure 저장소와](../storage/common/storage-powershell-guide-full.md) -PowerShell 및 hello Azure 저장소 서비스에 대 한 포괄적인 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="7d8a9-121">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="7d8a9-121">Code samples</span></span>

<span data-ttu-id="7d8a9-122">관련 항목에서 두 가지 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="7d8a9-123">SQL Database의 확장 이벤트에 대한 링 버퍼 대상 코드</span><span class="sxs-lookup"><span data-stu-id="7d8a9-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="7d8a9-124">짧고 간단한 Transact-SQL 스크립트.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="7d8a9-125">링 버퍼 대상을 사용 하 여 완료 되 면 alter 놓기를 실행 하 여 해당 리소스를 해제 해야 하는 hello 코드 샘플 항목의 내용을 강조 `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` 문.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="7d8a9-126">나중에 `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`(으)로 링 버퍼의 다른 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="7d8a9-127">SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드</span><span class="sxs-lookup"><span data-stu-id="7d8a9-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="7d8a9-128">1 단계에는 PowerShell toocreate Azure 저장소 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="7d8a9-129">단계 2는 hello Azure 저장소 컨테이너를 사용 하는 TRANSACT-SQL입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="7d8a9-130">Transact-SQL 차이점</span><span class="sxs-lookup"><span data-stu-id="7d8a9-130">Transact-SQL differences</span></span>


- <span data-ttu-id="7d8a9-131">Hello를 실행 하는 동안 [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) hello를 사용 하 여 SQL Server 명령을 **ON SERVER** 절.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="7d8a9-132">Hello를 사용 하면 SQL 데이터베이스에서 하지만 **ON DATABASE** 절 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="7d8a9-133">hello **ON DATABASE** toohello 절에도 적용 됩니다 [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) 및 [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) TRANSACT-SQL 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="7d8a9-134">가장 좋은 방법은 tooinclude hello 이벤트 세션 옵션의 **STARTUP_STATE = ON** 에 프로그램 **CREATE EVENT SESSION** 또는 **ALTER EVENT SESSION** 문.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="7d8a9-135">hello **= ON** 값 tooa 장애 조치 인해 hello 논리적 데이터베이스의 재구성 후 자동 다시 시작을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="7d8a9-136">새 카탈로그 뷰</span><span class="sxs-lookup"><span data-stu-id="7d8a9-136">New catalog views</span></span>

<span data-ttu-id="7d8a9-137">hello 확장된 이벤트에서 지 원하는 기능 여러 [카탈로그 뷰](http://msdn.microsoft.com/library/ms174365.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="7d8a9-138">카탈로그 뷰에 대해 알려줄 *메타 데이터 또는 정의* hello 현재 데이터베이스의 사용자가 만든 이벤트 세션의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="7d8a9-139">hello 뷰는 활성 이벤트 세션의 인스턴스에 대 한 정보를 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="7d8a9-140">카탈로그 뷰의</span><span class="sxs-lookup"><span data-stu-id="7d8a9-140">Name of</span></span><br/><span data-ttu-id="7d8a9-141">이름</span><span class="sxs-lookup"><span data-stu-id="7d8a9-141">catalog view</span></span> | <span data-ttu-id="7d8a9-142">설명</span><span class="sxs-lookup"><span data-stu-id="7d8a9-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7d8a9-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="7d8a9-144">이벤트 세션의 각 이벤트에 있는 각 작업에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="7d8a9-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="7d8a9-146">이벤트 세션의 각 이벤트에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="7d8a9-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="7d8a9-148">이벤트 및 대상에 명시적으로 설정된 사용자 지정 가능한 각 열에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="7d8a9-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="7d8a9-150">이벤트 세션의 각 이벤트 대상에 대한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="7d8a9-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="7d8a9-152">Hello SQL 데이터베이스 데이터베이스의 각 이벤트 세션에 대 한 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="7d8a9-153">Microsoft SQL Server에서 유사한 카탈로그 뷰의 이름에는 *.database\_*가 아닌 *.server\_*가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="7d8a9-154">같은 hello 이름 패턴은 **sys.server_event_%**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="7d8a9-155">새로운 [DMV](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="7d8a9-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="7d8a9-156">Azure SQL Database에는 확장 이벤트를 지원하는 [DMV(동적 관리 뷰)](http://msdn.microsoft.com/library/bb677293.aspx) 가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="7d8a9-157">DMV를 통해 *활성* 이벤트 세션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="7d8a9-158">DMV의 이름</span><span class="sxs-lookup"><span data-stu-id="7d8a9-158">Name of DMV</span></span> | <span data-ttu-id="7d8a9-159">설명</span><span class="sxs-lookup"><span data-stu-id="7d8a9-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7d8a9-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="7d8a9-161">이벤트 세션 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="7d8a9-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="7d8a9-163">세션 이벤트에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-163">Returns information about session events.</span></span> |
| <span data-ttu-id="7d8a9-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="7d8a9-165">바인딩된 tooa 세션 개체에 대 한 hello 구성 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="7d8a9-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="7d8a9-167">세션 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="7d8a9-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="7d8a9-169">범위가 지정 된 toohello 현재 데이터베이스는 각 이벤트 세션에 대 한 행을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="7d8a9-170">Microsoft SQL Server에서 유사한 카탈로그 뷰 hello 없이 이름은  *\_데이터베이스* 같은 hello의 부분 이름:</span><span class="sxs-lookup"><span data-stu-id="7d8a9-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="7d8a9-171">**sys.dm_xe_sessions**, 이름 대신</span><span class="sxs-lookup"><span data-stu-id="7d8a9-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="7d8a9-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="7d8a9-173">일반적인 tooboth Dmv</span><span class="sxs-lookup"><span data-stu-id="7d8a9-173">DMVs common tooboth</span></span>
<span data-ttu-id="7d8a9-174">확장된 이벤트에는 일반적인 tooboth Azure SQL 데이터베이스는 추가 Dmv 및 Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="7d8a9-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="7d8a9-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="7d8a9-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="7d8a9-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="7d8a9-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="7d8a9-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="7d8a9-179">Hello 사용 가능한 확장된 이벤트, 동작 및 대상 찾기</span><span class="sxs-lookup"><span data-stu-id="7d8a9-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="7d8a9-180">단순한 SQL을 실행할 수 있습니다 **선택** tooobtain hello 사용 가능한 이벤트, 동작 및 대상의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

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


<span data-ttu-id="7d8a9-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="7d8a9-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="7d8a9-182">SQL Database 이벤트 세션의 대상</span><span class="sxs-lookup"><span data-stu-id="7d8a9-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="7d8a9-183">SQL Database에서 이벤트 세션의 결과를 캡처할 수 있는 대상은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="7d8a9-184">[링 버퍼 대상](http://msdn.microsoft.com/library/ff878182.aspx) - 이벤트 데이터를 메모리에 잠시 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="7d8a9-185">[이벤트 카운터 대상](http://msdn.microsoft.com/library/ff878025.aspx) - 확장 이벤트 세션 동안 발생하는 모든 이벤트의 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="7d8a9-186">[이벤트 파일 대상을](http://msdn.microsoft.com/library/ff878115.aspx) -쓰기 전체 버퍼 tooan Azure 저장소 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="7d8a9-187">hello [이벤트 추적에 대 한 ETW (Windows)](http://msdn.microsoft.com/library/ms751538.aspx) API는 SQL 데이터베이스에서 확장된 이벤트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="7d8a9-188">제한</span><span class="sxs-lookup"><span data-stu-id="7d8a9-188">Restrictions</span></span>

<span data-ttu-id="7d8a9-189">SQL 데이터베이스의 hello 클라우드 환경 befitting 보안 관련 차이점 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="7d8a9-190">확장된 이벤트는 hello 단일 테 넌 트 격리 모델에 기초로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="7d8a9-191">한 데이터베이스의 이벤트 세션은 다른 데이터베이스의 데이터 또는 이벤트에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="7d8a9-192">실행할 수 없는 **CREATE EVENT SESSION** hello의 hello 컨텍스트에서 문을 **마스터** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="7d8a9-193">권한 모델</span><span class="sxs-lookup"><span data-stu-id="7d8a9-193">Permission model</span></span>

<span data-ttu-id="7d8a9-194">있어야 **제어** 데이터베이스 tooissue hello에 대 한 권한이 **CREATE EVENT SESSION** 문.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="7d8a9-195">hello 데이터베이스 소유자 (dbo)에 **제어** 권한.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="7d8a9-196">저장소 컨테이너 권한</span><span class="sxs-lookup"><span data-stu-id="7d8a9-196">Storage container authorizations</span></span>

<span data-ttu-id="7d8a9-197">hello SAS 토큰을 지정 해야 Azure 저장소 컨테이너에 대 한 생성 **rwl** hello 사용 권한에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="7d8a9-198">hello **rwl** hello 다음 권한을 제공 하는 값:</span><span class="sxs-lookup"><span data-stu-id="7d8a9-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="7d8a9-199">읽기</span><span class="sxs-lookup"><span data-stu-id="7d8a9-199">Read</span></span>
- <span data-ttu-id="7d8a9-200">쓰기</span><span class="sxs-lookup"><span data-stu-id="7d8a9-200">Write</span></span>
- <span data-ttu-id="7d8a9-201">나열</span><span class="sxs-lookup"><span data-stu-id="7d8a9-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="7d8a9-202">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7d8a9-202">Performance considerations</span></span>

<span data-ttu-id="7d8a9-203">확장된 이벤트를 많이 사용 빈도가 높은 메모리는 hello에 대 한 정상 보다 누적 될 수 있는 시나리오 전반적인 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="7d8a9-204">따라서 hello Azure SQL 데이터베이스 시스템 동적으로 설정 하 고 조정 hello 이벤트 세션에 의해 누적 될 수 있는 활성 메모리 양 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="7d8a9-205">다양 한 요인 hello 동적 계산으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="7d8a9-206">메모리 최대 한도가 적용되었다는 오류 메시지가 표시될 경우 다음과 같은 방법으로 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="7d8a9-207">실행하는 동시 이벤트 세션 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="7d8a9-208">통해 프로그램 **만들기** 및 **ALTER** 이벤트 세션에 대 한 문을 hello hello에서 지정 하는 메모리 양을 줄일 **최대\_메모리** 절.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="7d8a9-209">네트워크 대기 시간</span><span class="sxs-lookup"><span data-stu-id="7d8a9-209">Network latency</span></span>

<span data-ttu-id="7d8a9-210">hello **이벤트 파일** 대상 네트워크 대기 시간 또는 저장소 blob 데이터 tooAzure 유지 하는 동안 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="7d8a9-211">SQL 데이터베이스의 다른 이벤트 hello 네트워크 통신 toocomplete를 기다리는 동안 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="7d8a9-212">이 지연으로 인해 워크로드가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="7d8a9-213">toomitigate이이 성능 위험, hello를 설정 하지 마십시오 **EVENT_RETENTION_MODE** 옵션**NO_EVENT_LOSS** 에서 이벤트 세션 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="7d8a9-214">관련 링크</span><span class="sxs-lookup"><span data-stu-id="7d8a9-214">Related links</span></span>

- <span data-ttu-id="7d8a9-215">[Azure Storage와 함께 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="7d8a9-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="7d8a9-216">Azure Storage Cmdlet</span><span class="sxs-lookup"><span data-stu-id="7d8a9-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="7d8a9-217">[Azure PowerShell을 사용 하 여 Azure 저장소와](../storage/common/storage-powershell-guide-full.md) -PowerShell 및 hello Azure 저장소 서비스에 대 한 포괄적인 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="7d8a9-218">어떻게 toouse.NET에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="7d8a9-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="7d8a9-219">CREATE CREDENTIAL(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="7d8a9-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="7d8a9-220">CREATE EVENT SESSION(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="7d8a9-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="7d8a9-221">Microsoft SQL Server의 확장 이벤트에 대한 Jonathan Kehayias의 블로그</span><span class="sxs-lookup"><span data-stu-id="7d8a9-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="7d8a9-222">Azure hello *서비스 업데이트* 웹 페이지에서 SQL 데이터베이스 매개 변수 tooAzure 좁혀집니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="7d8a9-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="7d8a9-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="7d8a9-224">확장된 이벤트에 대 한 다른 코드 샘플 항목에 링크를 따라 hello에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="7d8a9-225">그러나 모든 샘플 toosee 체크 정기적으로 hello 샘플 Microsoft SQL Server와 Azure SQL 데이터베이스를 대상으로 하는지 여부를.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="7d8a9-226">그런 다음 약간의 변경이 필요한 toorun hello 샘플 지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8a9-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
