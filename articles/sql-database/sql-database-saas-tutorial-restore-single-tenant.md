---
title: "다중 테넌트 앱에서 Azure SQL Database 복원 | Microsoft Docs"
description: "실수로 데이터를 삭제한 후 단일 테넌트 SQL Database를 복원하는 방법에 대해 알아봅니다."
keywords: "sql 데이터베이스 자습서"
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
ms.openlocfilehash: 547851972f13ec69a8f65d01290874ad7d07f192
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a><span data-ttu-id="dc64a-104">Wingtip SaaS 테넌트 SQL Database 복원</span><span class="sxs-lookup"><span data-stu-id="dc64a-104">Restore a Wingtip SaaS tenants SQL database</span></span>

<span data-ttu-id="dc64a-105">Wingtip SaaS 앱은 각 테넌트에 자체 데이터베이스가 있는 테넌트당 데이터베이스 모델을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-105">The Wingtip SaaS app is built using a database-per-tenant model, where each tenant has their own database.</span></span> <span data-ttu-id="dc64a-106">이 모델의 이점 중 하나는 다른 테넌트에 영향을 주지 않으면서 격리된 단일 테넌트의 데이터를 쉽게 복원할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-106">One of the benefits of this model is that it is easy to restore a single tenant’s data in isolation without impacting other tenants.</span></span>

<span data-ttu-id="dc64a-107">이 자습서에서는 다음 두 가지 데이터 복구 패턴에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-107">In this tutorial you learn two data recovery patterns:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="dc64a-108">병렬 데이터베이스에 데이터베이스 복원(병렬)</span><span class="sxs-lookup"><span data-stu-id="dc64a-108">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="dc64a-109">원래 위치에 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="dc64a-109">Restore a database in place</span></span>


|||
|:--|:--|
| <span data-ttu-id="dc64a-110">**병렬 데이터베이스에 이전 시점의 테넌트 복원**</span><span class="sxs-lookup"><span data-stu-id="dc64a-110">**Restore tenant to a prior point in time, into a parallel database**</span></span> | <span data-ttu-id="dc64a-111">이 패턴은 검토, 감사, 준수 등을 위해 테넌트에서 사용할 수 있습니다. 원본 데이터베이스는 온라인 상태에서 변경되지 않은 채 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-111">This pattern can be used by the tenant for review, auditing, compliance, etc. The original database remains online and unchanged.</span></span> |
| <span data-ttu-id="dc64a-112">**원래 위치에 테넌트 복원**</span><span class="sxs-lookup"><span data-stu-id="dc64a-112">**Restore tenant in-place**</span></span> | <span data-ttu-id="dc64a-113">이 패턴은 일반적으로 테넌트에서 실수로 데이터를 삭제한 후 이전 시점으로 테넌트를 복구하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-113">This pattern is typically used to recover a tenant to a prior point in time, after a tenant accidentally deletes data.</span></span> <span data-ttu-id="dc64a-114">원본 데이터베이스는 오프라인 상태가 되고 복원된 데이터베이스로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-114">The original database is taken offline, and replaced with the restored database.</span></span> |
|||

<span data-ttu-id="dc64a-115">이 자습서를 수행하려면 다음 필수 조건이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-115">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="dc64a-116">Wingtip SaaS 앱이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-116">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="dc64a-117">5분 내에 배포하려면 [Wingtip SaaS 응용 프로그램 배포 및 탐색](sql-database-saas-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc64a-117">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="dc64a-118">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-118">Azure PowerShell is installed.</span></span> <span data-ttu-id="dc64a-119">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc64a-119">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

## <a name="introduction-to-the-saas-tenant-restore-pattern"></a><span data-ttu-id="dc64a-120">SaaS 테넌트 복원 패턴 소개</span><span class="sxs-lookup"><span data-stu-id="dc64a-120">Introduction to the SaaS tenant restore pattern</span></span>

<span data-ttu-id="dc64a-121">테넌트 복원 패턴의 경우 개별 테넌트의 데이터를 복원하기 위한 두 가지 간단한 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-121">For the tenant restore pattern, there are two simple patterns for restoring an individual tenant's data.</span></span> <span data-ttu-id="dc64a-122">테넌트 데이터베이스가 서로 격리되어 있기 때문에 하나의 테넌트를 복원해도 다른 테넌트의 데이터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-122">Because tenant databases are isolated from each other, restoring one tenant has no impact on any other tenant's data.</span></span>

<span data-ttu-id="dc64a-123">첫 번째 패턴에서는 데이터가 새 데이터베이스로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-123">In the first pattern, data is restored into a new database.</span></span> <span data-ttu-id="dc64a-124">그런 다음 프로덕션 데이터와 함께 이 데이터베이스에 대한 액세스 권한이 테넌트에 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-124">The tenant is then given access to this database alongside their production data.</span></span> <span data-ttu-id="dc64a-125">이 패턴을 사용하면 테넌트 관리자가 복원된 데이터를 검토하고 현재 데이터 값을 선택적으로 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-125">This pattern allows a tenant admin to review the restored data and potentially use it to selectively overwrite current data values.</span></span> <span data-ttu-id="dc64a-126">데이터 복구 옵션이 얼마나 정교해야 하는지 결정하는 것은 SaaS 앱 디자이너에게 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-126">It's up to the SaaS app designer to determine just how sophisticated the data recovery options should be.</span></span> <span data-ttu-id="dc64a-127">일부 시나리오에서는 특정 시점의 데이터를 검토할 수 있는 것만 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-127">Simply being able to review data in the state it was in at a given point in time may be all that is required in some scenarios.</span></span> <span data-ttu-id="dc64a-128">데이터베이스에서 [지역에서 복제](sql-database-geo-replication-overview.md)를 사용하는 경우 필요한 데이터를 복원된 복사본에서 원본 데이터베이스로 복사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-128">If the database uses [geo-replication](sql-database-geo-replication-overview.md), we recommend copying the required data from the restored copy into the original database.</span></span> <span data-ttu-id="dc64a-129">원본 데이터베이스를 복원된 데이터베이스로 바꾸는 경우 활성 지역 복제를 다시 구성하고 다시 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-129">If you replace the original database with the restored database, you need to reconfigure and resynchronize geo-replication.</span></span>

<span data-ttu-id="dc64a-130">테넌트에서 데이터가 손실되거나 손상되었다고 가정하는 두 번째 패턴에서는 테넌트의 프로덕션 데이터베이스가 이전 시점으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-130">In the second pattern, which assumes that the tenant has suffered a loss or corruption of data, the tenant’s production database is restored to a prior point in time.</span></span> <span data-ttu-id="dc64a-131">원래 위치에 복원 패턴에서는 데이터베이스를 복원하고 다시 온라인 상태로 전환하는 동안 테넌트가 잠시 동안 오프라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-131">In the restore in place pattern, the tenant is taken offline for a brief time while the database is restored and brought back online.</span></span> <span data-ttu-id="dc64a-132">원본 데이터베이스는 삭제되지만 훨씬 이전 시점으로 되돌아가야 하는 경우에도 여전히 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-132">The original database is deleted, but can still be restored from if you need to go back to an even earlier point in time.</span></span> <span data-ttu-id="dc64a-133">이 패턴의 변형은 데이터베이스를 삭제하는 대신 데이터베이스 이름을 바꿀 수 있지만, 데이터베이스 이름을 바꾸는 경우 데이터 보안 측면에서 추가적인 이점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-133">A variation of this pattern could rename the database instead of deleting it, although renaming the database offers no additional advantage in terms of data security.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="dc64a-134">Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="dc64a-134">Get the Wingtip application scripts</span></span>

<span data-ttu-id="dc64a-135">Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-135">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="dc64a-136">[Wingtip SaaS 스크립트를 다운로드하는 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="dc64a-136">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="simulate-a-tenant-accidentally-deleting-data"></a><span data-ttu-id="dc64a-137">실수로 데이터를 삭제하는 테넌트 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="dc64a-137">Simulate a tenant accidentally deleting data</span></span>

<span data-ttu-id="dc64a-138">이러한 복구 시나리오를 실제로 보여 주려면 테넌트 데이터베이스 중 하나에서 일부 데이터를 *실수로* 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-138">To demonstrate these recovery scenarios, we need to *accidentally* delete some data in one of the tenant databases.</span></span> <span data-ttu-id="dc64a-139">레코드를 삭제할 수는 있지만 다음 단계에서 참조 무결성 위반으로 차단되지 않도록 데모를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-139">While you can delete any record, the next step sets up the demo to not get blocked by referential integrity violations!</span></span> <span data-ttu-id="dc64a-140">또한 나중에 *Wingtip SaaS 분석 자습서*에서 사용할 수 있는 몇 가지 티켓 구매 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-140">It also adds some ticket purchase data you can use later in the *Wingtip SaaS Analytics tutorials*.</span></span>

<span data-ttu-id="dc64a-141">티켓 생성기 스크립트를 실행하고 추가 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-141">Run the ticket generator script and create additional data.</span></span> <span data-ttu-id="dc64a-142">티켓 생성기는 의도적으로 각 테넌트의 마지막 이벤트에 대한 티켓을 구매하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-142">The ticket generator intentionally does not purchase tickets for each tenants last event.</span></span>

1. <span data-ttu-id="dc64a-143">*PowerShell ISE*에서 \\Learning Modules\\Utilities\\*Demo-TicketGenerator.ps1*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-143">Open ...\\Learning Modules\\Utilities\\*Demo-TicketGenerator.ps1* in the *PowerShell ISE*</span></span>
1. <span data-ttu-id="dc64a-144">**F5** 키를 눌러 스크립트를 실행하고 고객 및 티켓 판매 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-144">Press **F5** to run the script and generate customers and ticket sales data.</span></span>


### <a name="open-the-events-app-to-review-the-current-events"></a><span data-ttu-id="dc64a-145">Events 앱을 열어 현재 이벤트 검토</span><span class="sxs-lookup"><span data-stu-id="dc64a-145">Open the Events app to review the current events</span></span>

1. <span data-ttu-id="dc64a-146">*Events Hub*(http://events.wtp.&lt;user&gt;.trafficmanager.net)를 열고 **Contoso Concert Hall**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-146">Open the *Events Hub* (http://events.wtp.&lt;user&gt;.trafficmanager.net) and click **Contoso Concert Hall**:</span></span>

   ![Events Hub](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. <span data-ttu-id="dc64a-148">이벤트 목록을 스크롤하고 목록의 마지막 이벤트를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-148">Scroll the list of events and make a note of the last event in the list:</span></span>

   ![마지막 이벤트](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-the-demo-scenario-to-accidentally-delete-the-last-event"></a><span data-ttu-id="dc64a-150">데모 시나리오를 실행하여 실수로 마지막 이벤트 삭제</span><span class="sxs-lookup"><span data-stu-id="dc64a-150">Run the demo scenario to accidentally delete the last event</span></span>

1. <span data-ttu-id="dc64a-151">*PowerShell ISE*에서 \\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\*Demo-RestoreTenant.ps1*을 열고 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-151">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\*Demo-RestoreTenant.ps1* in the *PowerShell ISE*, and set the following value:</span></span>
   * <span data-ttu-id="dc64a-152">**$DemoScenario** = **1** - **1**로 설정하면 티켓 판매가 없는 이벤트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-152">**$DemoScenario** = **1**, Set to **1** - Delete events with no ticket sales.</span></span>
1. <span data-ttu-id="dc64a-153">**F5** 키를 눌러 스크립트를 실행하고 마지막 이벤트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-153">Press **F5** to run the script and delete the last event.</span></span> <span data-ttu-id="dc64a-154">다음과 비슷한 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-154">You should see a confirmation message similar to the following:</span></span>

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. <span data-ttu-id="dc64a-155">Contoso 이벤트 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-155">The Contoso events page opens.</span></span> <span data-ttu-id="dc64a-156">아래로 스크롤하여 해당 이벤트가 삭제되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-156">Scroll down and verify the event is gone.</span></span> <span data-ttu-id="dc64a-157">해당 이벤트가 여전히 목록에 있으면 새로 고침을 클릭하고 삭제되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-157">If the event is still in the list, click refresh and verify it is gone.</span></span>

   ![마지막 이벤트](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-the-production-database"></a><span data-ttu-id="dc64a-159">프로덕션 데이터베이스와 병렬로 테넌트 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="dc64a-159">Restore a tenant database in parallel with the production database</span></span>

<span data-ttu-id="dc64a-160">이 연습에서는 이벤트를 삭제하기 전 특정 시점의 Contoso Concert Hall 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-160">This exercise restores the Contoso Concert Hall database to a point in time before the event was deleted.</span></span> <span data-ttu-id="dc64a-161">이전 단계에서 이벤트를 삭제한 후에 삭제된 데이터를 복구하고 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-161">After the event is deleted in the previous steps, you want to recover and see the deleted data.</span></span> <span data-ttu-id="dc64a-162">삭제된 레코드가 포함된 프로덕션 데이터베이스를 복원할 필요는 없지만, 다른 비즈니스상의 이유로 이전 데이터에 액세스하려면 이전 데이터베이스를 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-162">You don't need to restore your production database with the deleted record, but you need to recover the old database to access the old data for other business reasons.</span></span>

 <span data-ttu-id="dc64a-163">*Restore-TenantInParallel.ps1* 스크립트는 병렬 테넌트 데이터베이스와 병렬 카탈로그 항목을 모두 *ContosoConcertHall\_old*라는 이름으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-163">The *Restore-TenantInParallel.ps1* script creates a parallel tenant database, and a parallel catalog entry both named *ContosoConcertHall\_old*.</span></span> <span data-ttu-id="dc64a-164">이 복원 패턴은 사소한 데이터 손실로부터의 복구 또는 복구 시나리오에 대한 규정 준수 및 감사에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-164">This pattern of restore is best suited for recovering from a minor data loss or for compliance and auditing recovery scenarios.</span></span> <span data-ttu-id="dc64a-165">또한 [지역에서 복제](sql-database-geo-replication-overview.md)를 사용할 때 권장되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-165">It is also the recommended approach when you are using [geo-replication](sql-database-geo-replication-overview.md).</span></span>

1. <span data-ttu-id="dc64a-166">[사용자가 실수로 데이터를 삭제하는 시뮬레이션](#simulate-a-tenant-accidentally-deleting-data) 섹션을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-166">Complete the [simulate a user accidentally deleting data](#simulate-a-tenant-accidentally-deleting-data) section.</span></span>
1. <span data-ttu-id="dc64a-167">*PowerShell ISE*에서 \\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\_Demo-RestoreTenant.ps1_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-167">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\_Demo-RestoreTenant.ps1_ in the *PowerShell ISE*.</span></span>
1. <span data-ttu-id="dc64a-168">**$DemoScenario** = **2**를 설정합니다. **2**로 설정하면 *테넌트를 병렬로 복원합니다*.</span><span class="sxs-lookup"><span data-stu-id="dc64a-168">Set **$DemoScenario** = **2**, Set this to **2** to *Restore tenant in parallel*.</span></span>
1. <span data-ttu-id="dc64a-169">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-169">Press **F5** to run the script.</span></span>

<span data-ttu-id="dc64a-170">스크립트는 이전 섹션에서 이벤트를 삭제하기 전 특정 시점의 테넌트 데이터베이스를 병렬 데이터베이스로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-170">The script restores the tenant database (to a parallel database) to a point in time before you deleted the event in the previous section.</span></span> <span data-ttu-id="dc64a-171">두 번째 데이터베이스를 만들고, 이 데이터베이스에 있는 기존 카탈로그 메타데이터를 제거하며, *ContosoConcertHall\_old* 항목 아래의 카탈로그에 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-171">It creates a second database, removes any existing catalog metadata that exists in this database, and adds the database to the catalog under the *ContosoConcertHall\_old* entry.</span></span>

<span data-ttu-id="dc64a-172">데모 스크립트는 브라우저에서 이벤트 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-172">The demo script opens the events page in your browser.</span></span> <span data-ttu-id="dc64a-173">참고: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` URL에서 복원된 데이터베이스(*_old*가 이름에 추가되어 있음)의 데이터를 보여 주고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-173">Note from the URL: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` that this is showing data from the restored database where *_old* is added to the name.</span></span>

<span data-ttu-id="dc64a-174">브라우저에 나열된 이벤트를 스크롤하여 이전 섹션에서 삭제한 이벤트가 복원되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-174">Scroll the events listed in the browser to confirm that the event deleted in the previous section has been restored.</span></span>

<span data-ttu-id="dc64a-175">복원된 테넌트를 추가 테넌트로 노출하고, 자체 Events 앱으로 티켓을 검색하면 복원된 데이터에 대한 액세스를 테넌트에 제공하는 방법은 아니지만 복원 패턴을 쉽게 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-175">Note that exposing the restored tenant as an additional tenant, with its own Events app to browse tickets, is unlikely to be how you would provide a tenant access to restored data, but serves to easily illustrate the restore pattern.</span></span>

<span data-ttu-id="dc64a-176">실제로 정의된 기간 동안 복원된 이 데이터베이스만 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-176">In reality, you would probably only retain this restored database for a defined period.</span></span> <span data-ttu-id="dc64a-177">*Remove-RestoredTenant.ps1* 스크립트를 호출하여 완료되면 복원된 테넌트 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-177">You can delete the restored tenant entry once you are finished by calling the *Remove-RestoredTenant.ps1* script.</span></span>

1. <span data-ttu-id="dc64a-178">**$DemoScenario**를 **4**로 설정하여 *복원된 테넌트 제거* 시나리오를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-178">Set **$DemoScenario** to **4** to select the *remove restored tenant* scenario.</span></span>
1. <span data-ttu-id="dc64a-179">**F5** **키를 사용하여** **실행합니다**.</span><span class="sxs-lookup"><span data-stu-id="dc64a-179">**Execute** **using** **F5**</span></span>
1. <span data-ttu-id="dc64a-180">이제 카탈로그에서 *ContosoConcertHall\_old* 항목이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-180">The *ContosoConcertHall\_old* entry is now deleted from the catalog.</span></span> <span data-ttu-id="dc64a-181">계속해서 브라우저에서 이 테넌트의 이벤트 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-181">Go ahead and close the events page for this tenant in your browser.</span></span>


## <a name="restore-a-tenant-in-place-replacing-the-existing-tenant-database"></a><span data-ttu-id="dc64a-182">원래 위치에 테넌트 복원 및 기존 테넌트 데이터베이스 대체</span><span class="sxs-lookup"><span data-stu-id="dc64a-182">Restore a tenant in place, replacing the existing tenant database</span></span>

<span data-ttu-id="dc64a-183">이 연습에서는 이벤트를 삭제하기 전 특정 시점의 Contoso Concert Hall 테넌트를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-183">This exercise restores the Contoso Concert Hall tenant to a point in time before the event was deleted.</span></span> <span data-ttu-id="dc64a-184">*Restore-TenantInPlace* 스크립트는 현재 테넌트 데이터베이스를 이전 시점을 가리키는 새 데이터베이스로 복원하고, 원본 데이터베이스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-184">The *Restore-TenantInPlace* script restores the current tenant database to a new database pointing to a previous point in time, and deletes the original database.</span></span> <span data-ttu-id="dc64a-185">이 복원 패턴은 테넌트에서 수용해야 하는 상당한 데이터 손실이 있을 수 있기 때문에 중요한 데이터 손상으로부터 복구하는 데 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-185">This pattern of restore is best suited for recovering from serious data corruption as there may be significant data loss that the tenant would have to accommodate.</span></span>

1. <span data-ttu-id="dc64a-186">PowerShell ISE에서 **Demo-RestoreTenant.ps1** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-186">Open **Demo-RestoreTenant.ps1** file in PowerShell ISE</span></span>
1. <span data-ttu-id="dc64a-187">**$DemoScenario**를 **5**로 설정하여 *원래 위치에 테넌트 복원 시나리오*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-187">Set **$DemoScenario** to **5** to select the *restore tenant in place scenario*.</span></span>
1. <span data-ttu-id="dc64a-188">**F5** 키를 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-188">Execute using **F5**.</span></span>

<span data-ttu-id="dc64a-189">스크립트는 이벤트를 삭제하기 5분 전의 테넌트 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-189">The script restores the tenant database to a point five minutes before the event was deleted.</span></span> <span data-ttu-id="dc64a-190">이렇게 하려면 먼저 Contoso Concert Hall 테넌트를 오프라인으로 전환하여 더 이상 데이터를 업데이트하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-190">It does this by first taking the Contoso Concert Hall tenant offline so there are no further updates to the data.</span></span> <span data-ttu-id="dc64a-191">다음으로, 복원 지점에서 복원하여 병렬 데이터베이스를 만들고, 타임스탬프가 포함된 이름을 지정하여 데이터베이스 이름이 기존 테넌트 데이터베이스 이름과 충돌하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-191">Then, a parallel database is created by restoring from the restore point and named with a timestamp to ensure the database name does not conflict with the existing tenant database name.</span></span> <span data-ttu-id="dc64a-192">다음으로, 이전 테넌트 데이터베이스를 삭제하고, 복원된 데이터베이스 이름을 원본 데이터베이스 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-192">Next, the old tenant database is deleted, and the restored database is renamed to the original database name.</span></span> <span data-ttu-id="dc64a-193">마지막으로, Contoso Concert Hall이 온라인 상태가 되어 응용 프로그램에서 복원된 데이터베이스에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-193">Finally, Contoso Concert Hall is brought online to allow the app access to the restored database.</span></span>

<span data-ttu-id="dc64a-194">이벤트를 삭제하기 전 특정 시점의 데이터베이스를 성공적으로 복원했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-194">You successfully restored the database to a point in time before the event was deleted.</span></span> <span data-ttu-id="dc64a-195">Events 페이지가 열리므로 마지막 이벤트가 복원되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-195">The Events page opens, so confirm the last event has been restored.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dc64a-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc64a-196">Next steps</span></span>

<span data-ttu-id="dc64a-197">이 자습서에서는 다음을 수행하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dc64a-197">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="dc64a-198">병렬 데이터베이스에 데이터베이스 복원(병렬)</span><span class="sxs-lookup"><span data-stu-id="dc64a-198">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="dc64a-199">원래 위치에 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="dc64a-199">Restore a database in place</span></span>

[<span data-ttu-id="dc64a-200">테넌트 데이터베이스 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="dc64a-200">Manage tenant database schema</span></span>](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a><span data-ttu-id="dc64a-201">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="dc64a-201">Additional resources</span></span>

* <span data-ttu-id="dc64a-202">[Wingtip SaaS 응용 프로그램을 기반으로 작성된](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="dc64a-202">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="dc64a-203">Azure SQL 데이터베이스의 비즈니스 연속성 개요</span><span class="sxs-lookup"><span data-stu-id="dc64a-203">Overview of business continuity with Azure SQL Database</span></span>](sql-database-business-continuity.md)
* [<span data-ttu-id="dc64a-204">SQL Database 백업에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="dc64a-204">Learn about SQL Database backups</span></span>](sql-database-automated-backups.md)
