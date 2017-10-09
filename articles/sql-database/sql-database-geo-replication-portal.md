---
title: "Azure Portal: SQL Database 지역에서 복제 | Microsoft Docs"
description: "Azure SQL 데이터베이스에 대 한 지리적 복제를 hello Azure 포털 및 시작 장애 조치 구성"
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
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="d8cf0-103">Azure SQL 데이터베이스에 대 한 활성 지리적 복제를 hello Azure 포털 및 시작 장애 조치 구성</span><span class="sxs-lookup"><span data-stu-id="d8cf0-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="d8cf0-104">이 문서에서는 어떻게 tooconfigure 활성 지리적 복제 SQL 데이터베이스에 대 한 hello에 [Azure 포털](http://portal.azure.com) 및 tooinitiate 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="d8cf0-105">Azure 포털 hello로 장애 조치 tooinitiate 참조 [hello Azure 포털으로 Azure SQL 데이터베이스에 대 한 계획 되거나 계획 되지 않은 장애 조치의 시작](sql-database-geo-replication-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="d8cf0-106">tooconfigure 활성 지리적 복제 hello Azure 포털을 사용 하 여 리소스를 수행 하는 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="d8cf0-107">Azure SQL 데이터베이스: tooreplicate tooa 서로 다른 지리적 위치 영역을 사용 하지 않겠다고 hello 주 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="d8cf0-108">활성 지리적 복제 데이터베이스 hello에 사이 여야 합니다. 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="d8cf0-109">보조 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="d8cf0-109">Add a secondary database</span></span>
<span data-ttu-id="d8cf0-110">hello 다음 단계를 만듭니다 새로운 보조 데이터베이스는 지리적 복제 파트너 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="d8cf0-111">보조 데이터베이스 tooadd hello 구독 소유자 또는 공동 소유자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="d8cf0-112">hello 보조 데이터베이스 hello hello 주 데이터베이스로 이름과 같은 이름을 가지 며 hello 기본적으로, 동일한 서비스 수준</span><span class="sxs-lookup"><span data-stu-id="d8cf0-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="d8cf0-113">hello 보조 데이터베이스는 단일 데이터베이스나 탄력적 풀의 데이터베이스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="d8cf0-114">자세한 내용은 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="d8cf0-115">보조 hello를 만들고 시드 된 후 데이터 hello 주 데이터베이스 toohello 새 보조 데이터베이스에서 복제를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="d8cf0-116">(예를 들어 이전 지리적 복제 관계를 종료) 결과로 hello 파트너 데이터베이스가 이미 있는 경우 hello 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="d8cf0-117">Hello에 [Azure 포털](http://portal.azure.com), tooset 지리적 복제에 대해 원하는 toohello 데이터베이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="d8cf0-118">Hello SQL 데이터베이스 페이지에서 선택 **지리적 복제**, 한 다음 hello 지역 toocreate hello 보조 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="d8cf0-119">Hello 주 데이터베이스를 호스트 하는 hello 지역 이외의 다른 모든 영역을 선택할 수 있지만 hello 권장 [쌍을 이루는 지역](../best-practices-availability-paired-regions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![지역에서 복제 구성](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="d8cf0-121">선택 하거나 hello 서버와 보조 데이터베이스 hello에 대 한 가격 책정 계층을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![보조 구성](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="d8cf0-123">필요에 따라 보조 데이터베이스 tooan 탄력적 풀을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="d8cf0-124">풀에서 toocreate hello 보조 데이터베이스를 클릭 **탄력적 풀** hello 대상 서버에서 풀을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="d8cf0-125">풀은 hello 대상 서버에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="d8cf0-126">이 워크플로는 풀을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="d8cf0-127">클릭 **만들기** tooadd hello 보조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="d8cf0-128">hello 보조 데이터베이스가 만들어지고 hello 시드 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![보조 구성](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="d8cf0-130">프로세스를 시드 hello 완료 되 면 hello 보조 데이터베이스의 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![시드 완료](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="d8cf0-132">장애 조치(Failover) 시작</span><span class="sxs-lookup"><span data-stu-id="d8cf0-132">Initiate a failover</span></span>

<span data-ttu-id="d8cf0-133">hello 보조 데이터베이스는 주 바뀌면된 toobecome hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="d8cf0-134">Hello에 [Azure 포털](http://portal.azure.com), toohello hello 지리적 복제 파트너 관계의 주 데이터베이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="d8cf0-135">Hello SQL 데이터베이스 블레이드에서 선택 **모든 설정을** > **지리적 복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="d8cf0-136">Hello에 **보조** 목록, 선택 hello 데이터베이스 toobecome 원하는 클릭 하 고 새로운 주 hello **장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![장애 조치](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="d8cf0-138">클릭 **예** toobegin hello 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="d8cf0-139">즉시 hello 명령 hello 주 역할로 hello 보조 데이터베이스를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="d8cf0-140">두 데이터베이스 모두에서 사용할 수 없는 (0 too25 초의 hello 순서) hello 역할이 전환 된 하는 동안 짧은 간격이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="d8cf0-141">Hello 주 데이터베이스에 자동으로 부여 된 여러 보조 데이터베이스, hello 명령 하는 경우 다시 구성 합니다. 다른 보조 복제본 tooconnect toohello 새로운 주를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="d8cf0-142">hello 전체 작업에는 일반적인 환경에서 분 toocomplete 보다 작은 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="d8cf0-143">이 명령은 중단 시 hello 데이터베이스의 빠른 복구를 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="d8cf0-144">데이터 동기화 없이 장애 조치(Failover)를 트리거합니다(강제 장애 조치).</span><span class="sxs-lookup"><span data-stu-id="d8cf0-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="d8cf0-145">경우 hello 기본 온라인 상태이 고 hello 명령이 일부 데이터가 손실 될 때 트랜잭션을 커밋하기 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="d8cf0-146">보조 데이터베이스 제거</span><span class="sxs-lookup"><span data-stu-id="d8cf0-146">Remove secondary database</span></span>
<span data-ttu-id="d8cf0-147">이 작업에는 영구적으로 hello 복제 toohello 보조 데이터베이스를 종료 하 고 변경 내용을 hello hello 보조 tooa 일반 읽기 / 쓰기 데이터베이스의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="d8cf0-148">보조 데이터베이스를 toohello hello 연결 중단 된 경우 hello 명령은 성공 하지만 연결이 복원 된 후에 읽기 / 쓰기 보조있지 않습니다 하 게 될 때까지 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="d8cf0-149">Hello에 [Azure 포털](http://portal.azure.com), toohello hello 지리적 복제 파트너 관계의 주 데이터베이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="d8cf0-150">Hello SQL 데이터베이스 페이지에서 선택 **지리적 복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="d8cf0-151">Hello에 **보조** 목록, tooremove hello 지리적 복제 파트너 관계에서 선택 hello 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="d8cf0-152">**복제 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-152">Click **Stop Replication**.</span></span>
   
    ![보조 제거](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="d8cf0-154">확인 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-154">A confirmation window opens.</span></span> <span data-ttu-id="d8cf0-155">클릭 **예** hello 지리적 복제 파트너 관계에서 tooremove hello 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="d8cf0-156">(설정 tooa 읽기 / 쓰기 데이터베이스 복제의 일부가 아닌.)</span><span class="sxs-lookup"><span data-stu-id="d8cf0-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8cf0-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8cf0-157">Next steps</span></span>
* <span data-ttu-id="d8cf0-158">활성 지리적 복제에 대해 자세히 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="d8cf0-159">비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

