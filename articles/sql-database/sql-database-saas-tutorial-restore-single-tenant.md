---
title: "다중 테 넌 트 응용 프로그램에서 Azure SQL 데이터베이스 aaaRestore | Microsoft Docs"
description: "단일 toorestore SQL 테 넌 트에서 방법에 대해 알아봅니다 데이터를 실수로 삭제 한 후 데이터베이스"
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a><span data-ttu-id="f7d38-104">Wingtip SaaS 테넌트 SQL Database 복원</span><span class="sxs-lookup"><span data-stu-id="f7d38-104">Restore a Wingtip SaaS tenants SQL database</span></span>

<span data-ttu-id="f7d38-105">각 테 넌 트는 자체 데이터베이스에 있는 테 넌 당 데이터베이스 모델을 사용 하 여 hello Wingtip SaaS 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-105">hello Wingtip SaaS app is built using a database-per-tenant model, where each tenant has their own database.</span></span> <span data-ttu-id="f7d38-106">이 모델의 hello 이점 중 하나는 쉽게 toorestore 다른 테 넌 트에 영향을 주지 않고 격리에 단일 테 넌 트의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-106">One of hello benefits of this model is that it is easy toorestore a single tenant’s data in isolation without impacting other tenants.</span></span>

<span data-ttu-id="f7d38-107">이 자습서에서는 다음 두 가지 데이터 복구 패턴에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-107">In this tutorial you learn two data recovery patterns:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="f7d38-108">병렬 데이터베이스에 데이터베이스 복원(병렬)</span><span class="sxs-lookup"><span data-stu-id="f7d38-108">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="f7d38-109">원래 위치에 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="f7d38-109">Restore a database in place</span></span>


|||
|:--|:--|
| <span data-ttu-id="f7d38-110">**병렬 데이터베이스에 시간 내에 테 넌 트 tooa 이전 지점 복원**</span><span class="sxs-lookup"><span data-stu-id="f7d38-110">**Restore tenant tooa prior point in time, into a parallel database**</span></span> | <span data-ttu-id="f7d38-111">검토, 감사, 규정 준수에 대 한 hello 테 넌 트 별로이 패턴을 사용할 수 있습니다, 그리고 등 hello 원본 데이터베이스에 온라인 상태이 고 변경 되지 않은 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-111">This pattern can be used by hello tenant for review, auditing, compliance, etc. hello original database remains online and unchanged.</span></span> |
| <span data-ttu-id="f7d38-112">**원래 위치에 테넌트 복원**</span><span class="sxs-lookup"><span data-stu-id="f7d38-112">**Restore tenant in-place**</span></span> | <span data-ttu-id="f7d38-113">이 방법은 일반적으로 사용 되는 테 넌 트 tooa 이전 지점 toorecover 테 넌 트 데이터를 실수로 삭제 한 후 시간 내에입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-113">This pattern is typically used toorecover a tenant tooa prior point in time, after a tenant accidentally deletes data.</span></span> <span data-ttu-id="f7d38-114">hello 원본 데이터베이스는 오프 라인으로 전환 하 고 hello 복원 된 데이터베이스 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-114">hello original database is taken offline, and replaced with hello restored database.</span></span> |
|||

<span data-ttu-id="f7d38-115">toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-115">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="f7d38-116">hello Wingtip SaaS 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-116">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="f7d38-117">5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="f7d38-117">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="f7d38-118">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-118">Azure PowerShell is installed.</span></span> <span data-ttu-id="f7d38-119">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7d38-119">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a><span data-ttu-id="f7d38-120">소개 toohello SaaS 테 넌 트 복원 패턴</span><span class="sxs-lookup"><span data-stu-id="f7d38-120">Introduction toohello SaaS tenant restore pattern</span></span>

<span data-ttu-id="f7d38-121">Hello 테 넌 트에 대 한 복원 패턴, 개별 테 넌 트의 데이터를 복원 하기 위한 두 가지 간단한 패턴.</span><span class="sxs-lookup"><span data-stu-id="f7d38-121">For hello tenant restore pattern, there are two simple patterns for restoring an individual tenant's data.</span></span> <span data-ttu-id="f7d38-122">테넌트 데이터베이스가 서로 격리되어 있기 때문에 하나의 테넌트를 복원해도 다른 테넌트의 데이터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-122">Because tenant databases are isolated from each other, restoring one tenant has no impact on any other tenant's data.</span></span>

<span data-ttu-id="f7d38-123">Hello 첫 번째 패턴에서는 데이터가 있는 새 데이터베이스로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-123">In hello first pattern, data is restored into a new database.</span></span> <span data-ttu-id="f7d38-124">hello 테 넌 트 프로덕션 데이터와 함께 access toothis 데이터베이스를 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-124">hello tenant is then given access toothis database alongside their production data.</span></span> <span data-ttu-id="f7d38-125">이 패턴을 사용 하면 테 넌 트 관리자 tooreview 복원 hello 데이터 및 잠재적으로 사용 하 여 tooselectively 현재 데이터 값을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-125">This pattern allows a tenant admin tooreview hello restored data and potentially use it tooselectively overwrite current data values.</span></span> <span data-ttu-id="f7d38-126">가 toohello SaaS 응용 프로그램 디자이너 toodetermine 얼마나 정교한 hello 데이터 복구 옵션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-126">It's up toohello SaaS app designer toodetermine just how sophisticated hello data recovery options should be.</span></span> <span data-ttu-id="f7d38-127">단순히 hello의 상태로 지정 된 시점으로 데이터를 수 tooreview 되 고 일부 시나리오에서는 필요한 모든 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-127">Simply being able tooreview data in hello state it was in at a given point in time may be all that is required in some scenarios.</span></span> <span data-ttu-id="f7d38-128">Hello 데이터베이스를 사용 하는 경우 [지리적 복제](sql-database-geo-replication-overview.md), hello 원래 데이터베이스에 복원 하는 hello 복사본에서 hello 필요한 데이터를 복사 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-128">If hello database uses [geo-replication](sql-database-geo-replication-overview.md), we recommend copying hello required data from hello restored copy into hello original database.</span></span> <span data-ttu-id="f7d38-129">데이터베이스를 복원 하는 hello와 hello 원래 데이터베이스를 대체 하는 경우 tooreconfigure 필요 하 고 지리적 복제를 다시 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-129">If you replace hello original database with hello restored database, you need tooreconfigure and resynchronize geo-replication.</span></span>

<span data-ttu-id="f7d38-130">이 경우 해당 hello 테 넌 트 손실 되거나 데이터 손상 되었다는 가정, 두 번째 패턴에서는 hello hello 테 넌 트의 프로덕션 데이터베이스를 복원 tooa 이전 지정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-130">In hello second pattern, which assumes that hello tenant has suffered a loss or corruption of data, hello tenant’s production database is restored tooa prior point in time.</span></span> <span data-ttu-id="f7d38-131">Hello 복원 시 위치 패턴이에 hello 테 넌 트는 동안 오프 라인 짧은 시간에 대 한 hello 데이터베이스가 복원 되 고 다시 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-131">In hello restore in place pattern, hello tenant is taken offline for a brief time while hello database is restored and brought back online.</span></span> <span data-ttu-id="f7d38-132">hello 원본 데이터베이스는 삭제 되지만 여전히에서 복원할 수 있습니다 toogo 백 tooan 해야 할 경우에 이전 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-132">hello original database is deleted, but can still be restored from if you need toogo back tooan even earlier point in time.</span></span> <span data-ttu-id="f7d38-133">Hello 데이터베이스 이름 바꾸기 데이터 보안과 관련 없는 추가적인 이점도 제공 하지만이 패턴의 변형에, 삭제 하는 대신 hello 데이터베이스 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-133">A variation of this pattern could rename hello database instead of deleting it, although renaming hello database offers no additional advantage in terms of data security.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="f7d38-134">Hello Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="f7d38-134">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="f7d38-135">hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-135">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="f7d38-136">[Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-136">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="simulate-a-tenant-accidentally-deleting-data"></a><span data-ttu-id="f7d38-137">실수로 데이터를 삭제하는 테넌트 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="f7d38-137">Simulate a tenant accidentally deleting data</span></span>

<span data-ttu-id="f7d38-138">toodemonstrate 이러한 복구 시나리오에 필요한 너무*실수로* hello 테 넌 트 데이터베이스 중 하나에 일부 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-138">toodemonstrate these recovery scenarios, we need too*accidentally* delete some data in one of hello tenant databases.</span></span> <span data-ttu-id="f7d38-139">모든 레코드를 삭제 하려면 동안 hello 데모 toonot 다음 단계 집합 hello 참조 무결성 위반을 통해 차단 될!</span><span class="sxs-lookup"><span data-stu-id="f7d38-139">While you can delete any record, hello next step sets up hello demo toonot get blocked by referential integrity violations!</span></span> <span data-ttu-id="f7d38-140">또한 일부 티켓 구매 데이터를 사용할 수 있습니다 hello의 뒷부분에 나오는 추가 *Wingtip SaaS 분석 자습서*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-140">It also adds some ticket purchase data you can use later in hello *Wingtip SaaS Analytics tutorials*.</span></span>

<span data-ttu-id="f7d38-141">Hello 티켓 생성기 스크립트를 실행 하 고 추가 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-141">Run hello ticket generator script and create additional data.</span></span> <span data-ttu-id="f7d38-142">의도적으로 hello 티켓 생성기는 각 테 넌 트 마지막 이벤트에 대 한 티켓을 구매 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-142">hello ticket generator intentionally does not purchase tickets for each tenants last event.</span></span>

1. <span data-ttu-id="f7d38-143">열기... \\학습 모듈\\유틸리티\\*데모 TicketGenerator.ps1* hello에 *PowerShell ISE*</span><span class="sxs-lookup"><span data-stu-id="f7d38-143">Open ...\\Learning Modules\\Utilities\\*Demo-TicketGenerator.ps1* in hello *PowerShell ISE*</span></span>
1. <span data-ttu-id="f7d38-144">키를 눌러 **F5** toorun 스크립트 hello 및 고객을 생성 및 티켓 판매 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-144">Press **F5** toorun hello script and generate customers and ticket sales data.</span></span>


### <a name="open-hello-events-app-tooreview-hello-current-events"></a><span data-ttu-id="f7d38-145">Hello 이벤트 응용 프로그램 tooreview hello 현재 이벤트를 열려면</span><span class="sxs-lookup"><span data-stu-id="f7d38-145">Open hello Events app tooreview hello current events</span></span>

1. <span data-ttu-id="f7d38-146">열기 hello *이벤트 허브* (http://events.wtp.&lt; 사용자&gt;. trafficmanager.net)를 클릭 하 고 **Contoso 함께 Hall**:</span><span class="sxs-lookup"><span data-stu-id="f7d38-146">Open hello *Events Hub* (http://events.wtp.&lt;user&gt;.trafficmanager.net) and click **Contoso Concert Hall**:</span></span>

   ![Events Hub](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. <span data-ttu-id="f7d38-148">Hello 이벤트 목록을 스크롤하여 hello 목록에서 hello 마지막 이벤트 확인:</span><span class="sxs-lookup"><span data-stu-id="f7d38-148">Scroll hello list of events and make a note of hello last event in hello list:</span></span>

   ![마지막 이벤트](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a><span data-ttu-id="f7d38-150">Hello 데모 시나리오 tooaccidentally delete hello 마지막 이벤트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-150">Run hello demo scenario tooaccidentally delete hello last event</span></span>

1. <span data-ttu-id="f7d38-151">열기... \\학습 모듈\\비즈니스 연속성 및 재해 복구\\RestoreTenant\\*데모 RestoreTenant.ps1* hello에 *PowerShell ISE*, 다음 값 집합 hello 및:</span><span class="sxs-lookup"><span data-stu-id="f7d38-151">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\*Demo-RestoreTenant.ps1* in hello *PowerShell ISE*, and set hello following value:</span></span>
   * <span data-ttu-id="f7d38-152">**$DemoScenario** = **1**너무 설정,**1** -티켓 판매량이 없는 이벤트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-152">**$DemoScenario** = **1**, Set too**1** - Delete events with no ticket sales.</span></span>
1. <span data-ttu-id="f7d38-153">키를 눌러 **F5** toorun 스크립트 hello 및 hello 마지막 이벤트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-153">Press **F5** toorun hello script and delete hello last event.</span></span> <span data-ttu-id="f7d38-154">확인 메시지와 비슷한 toohello 다음을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-154">You should see a confirmation message similar toohello following:</span></span>

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. <span data-ttu-id="f7d38-155">hello Contoso 이벤트 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-155">hello Contoso events page opens.</span></span> <span data-ttu-id="f7d38-156">아래로 스크롤하여 hello 이벤트는 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-156">Scroll down and verify hello event is gone.</span></span> <span data-ttu-id="f7d38-157">Hello 이벤트 hello 목록에 여전히 있는 경우 새로 고침을 클릭 하 고이 삭제 되 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-157">If hello event is still in hello list, click refresh and verify it is gone.</span></span>

   ![마지막 이벤트](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a><span data-ttu-id="f7d38-159">Hello 프로덕션 데이터베이스와 동시에 테 넌 트 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-159">Restore a tenant database in parallel with hello production database</span></span>

<span data-ttu-id="f7d38-160">이 연습 hello Contoso 함께 Hall 데이터베이스 tooa 지정 시간 hello 이벤트가 삭제 되기 전에 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-160">This exercise restores hello Contoso Concert Hall database tooa point in time before hello event was deleted.</span></span> <span data-ttu-id="f7d38-161">Hello 이벤트 hello 이전 단계에서 삭제 된 후 toorecover을 삭제 하는 hello 데이터를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f7d38-161">After hello event is deleted in hello previous steps, you want toorecover and see hello deleted data.</span></span> <span data-ttu-id="f7d38-162">Toorestore 프로덕션 데이터베이스를 삭제 하는 hello 레코드와 필요는 없지만 비즈니스 사유로 toorecover hello 이전 데이터베이스 tooaccess hello 이전 데이터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-162">You don't need toorestore your production database with hello deleted record, but you need toorecover hello old database tooaccess hello old data for other business reasons.</span></span>

 <span data-ttu-id="f7d38-163">hello *복원 TenantInParallel.ps1* 스크립트 병렬 테 넌 트 데이터베이스 만들고, 병렬 카탈로그 항목을 모두 라는 *ContosoConcertHall\_이전*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-163">hello *Restore-TenantInParallel.ps1* script creates a parallel tenant database, and a parallel catalog entry both named *ContosoConcertHall\_old*.</span></span> <span data-ttu-id="f7d38-164">이 복원 패턴은 사소한 데이터 손실로부터의 복구 또는 복구 시나리오에 대한 규정 준수 및 감사에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-164">This pattern of restore is best suited for recovering from a minor data loss or for compliance and auditing recovery scenarios.</span></span> <span data-ttu-id="f7d38-165">권장 접근법을 사용 중인 경우 hello 이기도 [지리적 복제](sql-database-geo-replication-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-165">It is also hello recommended approach when you are using [geo-replication](sql-database-geo-replication-overview.md).</span></span>

1. <span data-ttu-id="f7d38-166">전체 hello [실수로 데이터를 삭제 하는 사용자를 시뮬레이트합니다](#simulate-a-tenant-accidentally-deleting-data) 섹션.</span><span class="sxs-lookup"><span data-stu-id="f7d38-166">Complete hello [simulate a user accidentally deleting data](#simulate-a-tenant-accidentally-deleting-data) section.</span></span>
1. <span data-ttu-id="f7d38-167">열기... \\학습 모듈\\비즈니스 연속성 및 재해 복구\\RestoreTenant\\_데모 RestoreTenant.ps1_ hello에 *PowerShell ISE*.</span><span class="sxs-lookup"><span data-stu-id="f7d38-167">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\_Demo-RestoreTenant.ps1_ in hello *PowerShell ISE*.</span></span>
1. <span data-ttu-id="f7d38-168">설정 **$DemoScenario** = **2**, 너무 설정**2** 너무*병렬로 복원 테 넌 트*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-168">Set **$DemoScenario** = **2**, Set this too**2** too*Restore tenant in parallel*.</span></span>
1. <span data-ttu-id="f7d38-169">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-169">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="f7d38-170">hello 스크립트는 hello 테 넌 트 데이터베이스 (tooa 병렬 데이터베이스) tooa 지점 hello 이전 단원의 hello 이벤트를 삭제 하기 전에 시간으로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-170">hello script restores hello tenant database (tooa parallel database) tooa point in time before you deleted hello event in hello previous section.</span></span> <span data-ttu-id="f7d38-171">두 번째 데이터베이스를 만들고,이 데이터베이스에 존재 하며 hello에서 hello 데이터베이스 toohello 카탈로그를 추가 하는 기존 카탈로그 메타 데이터를 제거 *ContosoConcertHall\_이전* 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-171">It creates a second database, removes any existing catalog metadata that exists in this database, and adds hello database toohello catalog under hello *ContosoConcertHall\_old* entry.</span></span>

<span data-ttu-id="f7d38-172">hello 데모 스크립트 브라우저에서 hello 이벤트 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-172">hello demo script opens hello events page in your browser.</span></span> <span data-ttu-id="f7d38-173">Hello URL에서 참고: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` hello 복원 된 데이터베이스의에서 데이터를 보여 주는이 위치 *_old* toohello 이름이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-173">Note from hello URL: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` that this is showing data from hello restored database where *_old* is added toohello name.</span></span>

<span data-ttu-id="f7d38-174">스크롤 hello에에서 나열 된 이벤트 hello 브라우저 tooconfirm hello 이벤트 hello 이전 섹션에서 삭제 하는 복원 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-174">Scroll hello events listed in hello browser tooconfirm that hello event deleted in hello previous section has been restored.</span></span>

<span data-ttu-id="f7d38-175">추가 테 넌 트를 고유 이벤트 앱 toobrowse 티켓와 같이 드문 상황이 toobe 어떻게에 제공 하는 데 사용 tooeasily 아니라 테 넌 트 액세스 toorestored 데이터가 hello 복원 패턴을 보여 줍니다.은 해당 노출을 복원 hello 테 넌 트를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-175">Note that exposing hello restored tenant as an additional tenant, with its own Events app toobrowse tickets, is unlikely toobe how you would provide a tenant access toorestored data, but serves tooeasily illustrate hello restore pattern.</span></span>

<span data-ttu-id="f7d38-176">실제로 정의된 기간 동안 복원된 이 데이터베이스만 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-176">In reality, you would probably only retain this restored database for a defined period.</span></span> <span data-ttu-id="f7d38-177">Hello를 호출 하 여 완료 된 후 복원 하는 hello 테 넌 트 항목을 삭제할 수 *제거 RestoredTenant.ps1* 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-177">You can delete hello restored tenant entry once you are finished by calling hello *Remove-RestoredTenant.ps1* script.</span></span>

1. <span data-ttu-id="f7d38-178">설정 **$DemoScenario** 너무**4** tooselect hello *복원 제거 테 넌 트* 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-178">Set **$DemoScenario** too**4** tooselect hello *remove restored tenant* scenario.</span></span>
1. <span data-ttu-id="f7d38-179">**F5** **키를 사용하여** **실행합니다**.</span><span class="sxs-lookup"><span data-stu-id="f7d38-179">**Execute** **using** **F5**</span></span>
1. <span data-ttu-id="f7d38-180">hello *ContosoConcertHall\_이전* 항목은 이제 hello 카탈로그에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-180">hello *ContosoConcertHall\_old* entry is now deleted from hello catalog.</span></span> <span data-ttu-id="f7d38-181">계속 진행 하 고 브라우저에서이 테 넌이 트에 대 한 hello 이벤트 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-181">Go ahead and close hello events page for this tenant in your browser.</span></span>


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a><span data-ttu-id="f7d38-182">테 넌 트 원위치에서 hello 기존 테 넌 트 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-182">Restore a tenant in place, replacing hello existing tenant database</span></span>

<span data-ttu-id="f7d38-183">이 연습 hello Contoso 함께 Hall 테 넌 트 tooa 지점 시간 hello 이벤트가 삭제 되기 전에 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-183">This exercise restores hello Contoso Concert Hall tenant tooa point in time before hello event was deleted.</span></span> <span data-ttu-id="f7d38-184">hello *복원 TenantInPlace* 삭제 hello 원래 데이터베이스 및 스크립트 hello 현재 테 넌 트 데이터베이스 tooa 새 데이터베이스 시간 내에 tooa 이전 시점을 가리키는 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-184">hello *Restore-TenantInPlace* script restores hello current tenant database tooa new database pointing tooa previous point in time, and deletes hello original database.</span></span> <span data-ttu-id="f7d38-185">이 패턴의 복원 tooaccommodate 갖기 테 넌 트 hello 많은 양의 데이터가 손실 될 수 있으므로 심각한 데이터 손상 으로부터 복구에 대 한 가장 잘 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-185">This pattern of restore is best suited for recovering from serious data corruption as there may be significant data loss that hello tenant would have tooaccommodate.</span></span>

1. <span data-ttu-id="f7d38-186">PowerShell ISE에서 **Demo-RestoreTenant.ps1** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-186">Open **Demo-RestoreTenant.ps1** file in PowerShell ISE</span></span>
1. <span data-ttu-id="f7d38-187">설정 **$DemoScenario** 너무**5** tooselect hello *전체 시나리오에서 테 넌 트 복원*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-187">Set **$DemoScenario** too**5** tooselect hello *restore tenant in place scenario*.</span></span>
1. <span data-ttu-id="f7d38-188">**F5** 키를 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-188">Execute using **F5**.</span></span>

<span data-ttu-id="f7d38-189">hello 스크립트 hello 테 넌 트 데이터베이스 tooa 지점 hello 이벤트가 삭제 되기 전에 5 분을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-189">hello script restores hello tenant database tooa point five minutes before hello event was deleted.</span></span> <span data-ttu-id="f7d38-190">이렇게 하기 첫 번째 라인 hello Contoso 함께 Hall 더 이상 없으면 하므로 오프 라인으로 테 넌 트 toohello 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-190">It does this by first taking hello Contoso Concert Hall tenant offline so there are no further updates toohello data.</span></span> <span data-ttu-id="f7d38-191">그런 다음 병렬 데이터베이스 hello 복원 지점에서 복원 하 여 만든를 명명 된 타임 스탬프를 갖는 tooensure hello 데이터베이스 이름을 hello 기존 테 넌 트 데이터베이스 이름을와 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-191">Then, a parallel database is created by restoring from hello restore point and named with a timestamp tooensure hello database name does not conflict with hello existing tenant database name.</span></span> <span data-ttu-id="f7d38-192">다음으로 이전 테 넌 트 데이터베이스 hello 삭제 되 고, hello 복원 된 데이터베이스는 이름이 바뀐된 toohello 원래 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-192">Next, hello old tenant database is deleted, and hello restored database is renamed toohello original database name.</span></span> <span data-ttu-id="f7d38-193">마지막으로, Contoso 함께 Hall 온라인 tooallow hello 응용 프로그램 액세스 복원 toohello 데이터베이스를 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-193">Finally, Contoso Concert Hall is brought online tooallow hello app access toohello restored database.</span></span>

<span data-ttu-id="f7d38-194">Hello 데이터베이스 tooa 지정 hello 이벤트가 삭제 되기 전에 시간으로 복원 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-194">You successfully restored hello database tooa point in time before hello event was deleted.</span></span> <span data-ttu-id="f7d38-195">이벤트 페이지가 열리면 hello, 확인 하므로 hello 마지막 이벤트 복원 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-195">hello Events page opens, so confirm hello last event has been restored.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7d38-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7d38-196">Next steps</span></span>

<span data-ttu-id="f7d38-197">이 자습서에서는 다음을 수행하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f7d38-197">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="f7d38-198">병렬 데이터베이스에 데이터베이스 복원(병렬)</span><span class="sxs-lookup"><span data-stu-id="f7d38-198">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="f7d38-199">원래 위치에 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="f7d38-199">Restore a database in place</span></span>

[<span data-ttu-id="f7d38-200">테넌트 데이터베이스 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="f7d38-200">Manage tenant database schema</span></span>](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a><span data-ttu-id="f7d38-201">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f7d38-201">Additional resources</span></span>

* <span data-ttu-id="f7d38-202">추가 [hello Wingtip SaaS 응용 프로그램을 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="f7d38-202">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="f7d38-203">Azure SQL 데이터베이스의 비즈니스 연속성 개요</span><span class="sxs-lookup"><span data-stu-id="f7d38-203">Overview of business continuity with Azure SQL Database</span></span>](sql-database-business-continuity.md)
* [<span data-ttu-id="f7d38-204">SQL Database 백업에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f7d38-204">Learn about SQL Database backups</span></span>](sql-database-automated-backups.md)
