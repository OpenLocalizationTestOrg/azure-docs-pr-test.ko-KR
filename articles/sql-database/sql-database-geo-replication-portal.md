---
title: "Azure Portal: SQL Database 지역에서 복제 | Microsoft Docs"
description: "Azure Portal에서 Azure SQL 데이터베이스에 대한 지역에서 복제 구성 및 장애 조치(Failover) 시작"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="6c811-103">Azure Portal에서 Azure SQL 데이터베이스에 대한 활성 지역 복제 구성 및 장애 조치(Failover) 시작</span><span class="sxs-lookup"><span data-stu-id="6c811-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="6c811-104">이 문서에서는 [Azure Portal](http://portal.azure.com)을 사용하여 SQL Database에 대한 활성 지역 복제를 구성하고 장애 조치(Failover)를 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="6c811-105">Azure 포털에서 장애 조치를 시작하려면 [Azure SQL 데이터베이스에 대해 계획 또는 계획되지 않은 장애 조치(Failover) 시작](sql-database-geo-replication-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c811-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="6c811-106">Azure Portal을 사용하여 활성 지역 복제를 구성하려면 다음 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="6c811-107">Azure SQL Database: 다른 지역으로 복제하려는 주 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="6c811-108">활성 지역 복제는 동일한 구독에 있는 데이터베이스 간에 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="6c811-109">보조 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="6c811-109">Add a secondary database</span></span>
<span data-ttu-id="6c811-110">다음 단계에서는 지역에서 복제 파트너 관계에 새 보조 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="6c811-111">보조 데이터베이스를 추가하려면 구독 소유자 또는 공동 소유자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="6c811-112">보조 데이터베이스는 주 데이터베이스와 동일한 이름을 포함하며 기본적으로 동일한 수준의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="6c811-113">보조 데이터베이스는 단일 데이터베이스 또는 탄력적 풀에 있는 데이터베이스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="6c811-114">자세한 내용은 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c811-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="6c811-115">보조가 만들어지고 시드된 후 데이터는 주 데이터베이스에서 새로운 보조 데이터베이스로 복제되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="6c811-116">파트너 데이터베이스가 이미 있는 경우(예: 이전 지역에서 복제 관계를 종료한 결과) 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="6c811-117">[Azure Portal](http://portal.azure.com)에서 지역에서 복제를 위해 설치하려는 데이터베이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="6c811-118">SQL Database 페이지에서 **지역에서 복제**를 선택하고 보조 데이터베이스를 만들 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="6c811-119">주 데이터베이스를 호스트하는 지역과 다른 지역을 선택할 수 있지만 [쌍을 이루는 지역](../best-practices-availability-paired-regions.md)이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![지역에서 복제 구성](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="6c811-121">보조 데이터베이스를 위한 서버 및 가격 책정 계층을 선택하거나 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![보조 구성](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="6c811-123">필요에 따라 탄력적 풀에 보조 데이터베이스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="6c811-124">풀에서 보조 데이터베이스를 만들려면 **탄력적 풀**을 클릭하고 대상 서버에서 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="6c811-125">대상 서버에 풀이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="6c811-126">이 워크플로는 풀을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="6c811-127">**만들기** 를 클릭하여 보조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="6c811-128">보조 데이터베이스가 만들어지고 시드 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![보조 구성](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="6c811-130">시드 프로세스가 완료되면 보조 데이터베이스가 해당 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![시드 완료](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="6c811-132">장애 조치(Failover) 시작</span><span class="sxs-lookup"><span data-stu-id="6c811-132">Initiate a failover</span></span>

<span data-ttu-id="6c811-133">보조 데이터베이스가 주 데이터베이스가 되도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="6c811-134">[Azure Portal](http://portal.azure.com)에서 지역에서 복제 파트너 관계에 있는 주 데이터베이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="6c811-135">SQL Database 블레이드에서 **모든 설정** > **지역에서 복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="6c811-136">**보조** 목록에서 새로운 주 데이터베이스가 될 데이터베이스를 선택하고 **장애 조치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![장애 조치](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="6c811-138">장애 조치를 시작하려면 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="6c811-139">이 명령은 보조 데이터베이스를 주 역할로 즉시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="6c811-140">역할이 전환되는 동안 두 데이터베이스를 모두 사용할 수 없는 (0-25초의 순서로) 짧은 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="6c811-141">주 데이터베이스에 여러 개의 보조 데이터베이스가 있는 경우 이 명령을 사용하면 새로운 주 데이터베이스에 연결할 다른 보조 데이터베이스가 자동으로 다시 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="6c811-142">전체 작업은 정상적인 상황에서 완료하는데 1분 미만이 걸려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="6c811-143">이 명령은 가동 중지 시에 데이터베이스의 빠른 복구를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="6c811-144">데이터 동기화 없이 장애 조치(Failover)를 트리거합니다(강제 장애 조치).</span><span class="sxs-lookup"><span data-stu-id="6c811-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="6c811-145">주 데이터베이스가 온라인이고 명령이 실행될 때 트랜잭션을 커밋하면 일부 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="6c811-146">보조 데이터베이스 제거</span><span class="sxs-lookup"><span data-stu-id="6c811-146">Remove secondary database</span></span>
<span data-ttu-id="6c811-147">이 작업은 보조 데이터베이스에 대한 복제를 영구적으로 종료하고 보조의 역할을 일반적인 읽기-쓰기 데이터베이스로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="6c811-148">보조 데이터베이스에 대한 연결이 끊어진 경우 명령이 성공하지만 연결이 복원된 후에야 보조는 읽기-쓰기가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="6c811-149">[Azure Portal](http://portal.azure.com)에서 지역에서 복제 파트너 관계에 있는 주 데이터베이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="6c811-150">SQL Database 페이지에서 **지역에서 복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="6c811-151">**보조** 목록에서 지역에서 복제 파트너 관계에서 제거할 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="6c811-152">**복제 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-152">Click **Stop Replication**.</span></span>
   
    ![보조 제거](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="6c811-154">확인 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-154">A confirmation window opens.</span></span> <span data-ttu-id="6c811-155">지역에서 복제 파트너 관계에서 데이터베이스를 제거하려면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c811-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="6c811-156">(복제에 포함되지 않는 읽기-쓰기 데이터베이스로 설정)</span><span class="sxs-lookup"><span data-stu-id="6c811-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c811-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c811-157">Next steps</span></span>
* <span data-ttu-id="6c811-158">활성 지역 복제에 대한 자세한 내용은 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c811-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="6c811-159">비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c811-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

