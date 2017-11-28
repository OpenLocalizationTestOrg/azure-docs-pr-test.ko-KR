---
title: "Azure Portal: SQL Database 탄력적 풀 만들기 및 관리 | Microsoft Docs"
description: "Toouse hello Azure 포털 및 SQL 데이터베이스의 기본 제공 인텔리전스 toomanage, 모니터 및 적정 크기로 확장 가능한 탄력적 풀 toooptimize 데이터베이스 성능 및 비용 관리 방법에 대해 알아봅니다."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="adbab-103">만들기 및 Azure 포털 hello로 탄력적 풀 관리</span><span class="sxs-lookup"><span data-stu-id="adbab-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="adbab-104">이 항목에서는 toocreate 하 고 확장 가능한 관리 [탄력적 풀](sql-database-elastic-pool.md) hello Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="adbab-105">또한 생성 하 고 있는 Azure 탄력적 풀 관리 수 [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello 또는 [C#](sql-database-elastic-pool-manage-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="adbab-106">[Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="adbab-107">탄력적 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="adbab-107">Create an elastic pool</span></span> 

<span data-ttu-id="adbab-108">두 가지 방법으로 탄력적 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="adbab-109">Hello 풀 설치 프로그램을 시작 하 든 hello 서비스에서 권장을 알고 있는 경우 처음부터이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="adbab-110">SQL 데이터베이스에 더 비용 효율적 사용 원격 분석 데이터베이스에 대 한 지난 hello에 근거 하는 경우 탄력적 풀 설치 프로그램을 권장 하는 기본 제공 인텔리전스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="adbab-111">서버에서 여러 풀을 만들 수 있지만 hello에 서로 다른 서버에서 데이터베이스를 추가할 수 없습니다 동일한 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="adbab-112">탄력적 풀은 현재 미리 보기 상태인 인도 서부를 제외한 모든 Azure 지역에서 일반 공급(GA) 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="adbab-113">이 영역에서 탄력적 풀의 GA는 가능한 한 빨리 수행될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="adbab-114">1단계: 탄력적 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="adbab-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="adbab-115">기존 탄력적 풀을 만들어 **서버** hello 포털에서 블레이드는 hello 가장 쉬운 방법은 toomove 기존 데이터베이스를 탄력적 풀으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="adbab-116">검색 하 여 탄력적 풀을 만들 수도 있습니다 **SQL 탄력적인 풀** hello에 **마켓플레이스** 클릭 하거나 **+ 추가** hello에 **SQL 탄력적 풀**블레이드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="adbab-117">워크플로 프로 비전 하는이 풀을 통해 기존 또는 새 서버 수 toospecify 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="adbab-118">Hello에 [Azure 포털](http://portal.azure.com/), 클릭 **더 많은 서비스**  **>**  **SQL server**, 다음 hello를 포함 하는 hello 서버를 클릭 하 고 데이터베이스 tooadd tooan 탄력적 풀에서 사용할 수 있는 권한</span><span class="sxs-lookup"><span data-stu-id="adbab-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="adbab-119">**새 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-119">Click **New pool**.</span></span>

    ![풀 tooa 서버 추가](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="adbab-121">**또는**</span><span class="sxs-lookup"><span data-stu-id="adbab-121">**-OR-**</span></span>

    <span data-ttu-id="adbab-122">표시 될 수 있습니다 있습니다 한다는 메시지가 hello 서버에 대 한 탄력적 풀 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="adbab-123">Hello 메시지 toosee hello 권장 되는 기록 데이터베이스 사용량 원격 분석에 따라 풀을 클릭 한 다음 자세한 내용을 보려면 hello 계층 toosee를 클릭 하 고 hello 풀을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="adbab-124">참조 [풀 권장 사항을 이해](#understand-elastic-pool-recommendations) 이 항목 뒷부분의 hello 권장 사항 생성 되는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="adbab-126">hello **탄력적 풀** 블레이드 표시 되는 풀에 대해 hello 설정을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="adbab-127">클릭 한 경우 **새 풀** hello 가격 책정 계층은 hello 이전 단계에서 **표준** 데이터베이스가 없고 하 고 기본적으로 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="adbab-128">빈 풀을 만들거나 hello 풀으로 해당 서버 toomove에서 기존 데이터베이스의 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="adbab-129">권장된 풀을 만드는 경우 hello 가격 책정 계층, 성능 설정 및 데이터베이스의 목록을 미리 채워져 있습니다, 좋지만 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![탄력적 풀 구성](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="adbab-131">Hello 탄력적 풀에 대 한 이름을 지정 하거나 hello 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="adbab-132">2단계: 가격 책정 계층 선택</span><span class="sxs-lookup"><span data-stu-id="adbab-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="adbab-133">hello 풀의 가격 책정 계층이 결정 hello hello 그룹 및 hello 최대 수 (최대 eDTU) Edtu 및 저장소 (Gb) 사용 가능한 tooeach 데이터베이스의 사용 가능한 toohello elastics 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="adbab-134">자세한 내용은 서비스 계층을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="adbab-135">hello toochange hello 풀에 대 한 가격 책정 계층을 클릭 **가격 책정 계층**, 가격 책정 계층을 하 고 클릭 hello 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adbab-136">Hello 가격 책정 계층을 선택 하 고 클릭 하 여 변경 내용을 적용 한 후 **확인** hello 마지막 단계에서 가격 책정 계층 hello 풀의 수 toochange hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="adbab-137">toochange hello 기존 탄력적 풀의 가격 책정 계층을 hello 원하는 가격 책정 계층에서 탄력적 풀을 만들거나 hello 데이터베이스 toothis 새 풀을 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![가격 책정 계층 선택](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="adbab-139">3 단계: hello 풀 구성</span><span class="sxs-lookup"><span data-stu-id="adbab-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="adbab-140">가격 책정 계층 hello를 설정한 후 데이터베이스, 집합 풀 Edtu 및 저장소 (풀 Gb)를 추가 하 고 hello 풀의 hello min 및 max Edtu elastics hello에 대 한 설정 구성 풀을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="adbab-141">**풀 구성**</span><span class="sxs-lookup"><span data-stu-id="adbab-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="adbab-142">Tooadd toohello 풀에서 사용할 hello 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="adbab-143">Hello 풀을 만드는 동안이 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="adbab-144">Hello 풀이 만들어진 후에 데이터베이스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="adbab-145">tooadd 데이터베이스 클릭 **데이터베이스 추가**, hello 데이터베이스 tooadd를 원하고 hello를 클릭 한 다음 클릭 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![데이터베이스 추가](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="adbab-147">사용 하는 hello 데이터베이스 데이터베이스의 기록 사용 만큼 원격 분석이 충분 경우 hello **예상 eDTU 및 GB 사용량** 그래프 및 hello **실제 eDTU 사용량** 가로 막대형 차트 업데이트 toohelp 구성 확인 의사 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="adbab-148">또한 hello 서비스가 제공할 수 있습니다 권장 메시지 toohelp 풀 hello 적정 크기로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="adbab-149">[동적 권장 사항](#understand-elastic-pool-recommendations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="adbab-150">Hello에 hello 컨트롤을 사용 하 여 **풀 구성** tooexplore 설정 페이지 및 프로그램 풀을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="adbab-151">각 서비스 계층의 제한에 대한 자세한 내용은 [탄력적 풀 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하고 적정한 탄력적 풀의 크기에 대한 자세한 지침은 [탄력적 풀에 대한 가격 및 성능 고려 사항](sql-database-elastic-pool.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="adbab-152">풀 설정에 대한 자세한 내용은 [탄력적 풀 속성](sql-database-elastic-pool.md#database-properties-for-pooled-databases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![탄력적 풀 구성](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="adbab-154">클릭 **선택** hello에 **풀 구성** 설정을 변경한 후 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="adbab-155">클릭 **확인** toocreate hello 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="adbab-156">탄력적 풀 권장 사항 이해</span><span class="sxs-lookup"><span data-stu-id="adbab-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="adbab-157">hello SQL 데이터베이스 서비스는 사용 현황을 평가 하 고 단일 데이터베이스를 사용 하 여 보다 비용 효율성이 되었을 때 하나 이상의 풀은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="adbab-158">각 권장 사항은 hello 풀에 가장 잘 맞는 hello 서버 데이터베이스의 고유 하위 집합으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="adbab-160">hello 풀 권장이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="adbab-161">Hello 풀 (Basic, Standard, Premium 또는 프리미엄 RS)에 대 한 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="adbab-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="adbab-162">적절한 **풀 eDTU** (풀당 최대 eDTU)</span><span class="sxs-lookup"><span data-stu-id="adbab-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="adbab-163">hello **최대 eDTU** 및 **eDTU Min** 데이터베이스당</span><span class="sxs-lookup"><span data-stu-id="adbab-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="adbab-164">hello hello 풀에 대 한 권장된 데이터베이스 목록</span><span class="sxs-lookup"><span data-stu-id="adbab-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adbab-165">hello 서비스 고려 hello 원격 분석의 지난 30 일 동안 풀 권장할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="adbab-166">탄력적 풀에 대 한 대상으로 간주 하는 데이터베이스 toobe에 대 한 일 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="adbab-167">이미 탄력적 풀에 있는 데이터베이스는 탄력적 풀 권장 사항에 대한 후보로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="adbab-168">hello 서비스의 리소스 수요를 평가 및 단일 이동 hello의 비용 효율 데이터베이스 각 서비스 계층에서의 hello 풀에 동일한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="adbab-169">예를 들어 서버의 모든 Standard 데이터베이스는 표준 탄력적 풀에 적합한지 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="adbab-170">즉, hello 서비스 계층 간 권장 사항을 표준 데이터베이스는 프리미엄 풀으로 이동 하는 등을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="adbab-171">데이터베이스 toohello 풀을 추가한 다음 권장 사항은 동적으로 생성 되 hello 선택한 hello 데이터베이스의 기존 사용량 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="adbab-172">이러한 권장 hello eDTU 및 GB 사용 현황 차트에서 고 hello hello 맨 위의 권장 사항 배너에 표시 됩니다 **풀 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="adbab-173">이러한 권장 사항은 의도 한 tooassist 특정 데이터베이스에 대해 최적화 된 탄력적 풀을 만드는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![동적 권장 사항](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="adbab-175">탄력적 풀 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="adbab-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="adbab-176">Azure 포털 toomonitor hello를 사용 하 고 탄력적 풀 및 hello 풀의 hello 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="adbab-177">Hello 포털에서 탄력적 풀과 해당 풀 내의 hello 데이터베이스의 hello 사용률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="adbab-178">변경 내용 집합이 tooyour 탄력적 풀을 확인 하 고 모든 변경 내용을 hello 동일 제출할 수도 있습니다 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="adbab-179">이러한 변경 내용에는 데이터베이스 추가 또는 제거, 탄력적 풀 설정 변경, 데이터베이스 설정 변경이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="adbab-180">다음 그래픽 hello 예제 탄력적 풀을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="adbab-181">hello 보기에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-181">hello view includes:</span></span>

*  <span data-ttu-id="adbab-182">Hello 탄력적 풀과 hello 풀에 포함 된 hello 데이터베이스의 리소스 사용 모니터링에 대 한 차트를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="adbab-183">hello **구성** 풀 단추 toomake toohello 탄력적 풀을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="adbab-184">hello **데이터베이스 만들기** 데이터베이스를 만드는 단추 toohello 현재 탄력적 풀을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="adbab-185">목록의 모든 데이터베이스에 대해 Transact SQL 스크립트를 실행하여 많은 데이터베이스를 관리하는 데 도움이 되는 탄력적 작업</span><span class="sxs-lookup"><span data-stu-id="adbab-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![풀 보기][2]

<span data-ttu-id="adbab-187">해당 리소스 사용률 tooa 특정 풀 toosee를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="adbab-188">기본적으로 hello 풀 지난 1 시간 동안 hello에 대 한 구성된 tooshow 저장소 및 eDTU 사용량은입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="adbab-189">hello 차트에는 다양 한 시간 창에 대해 구성 된 tooshow 가지 다른 메트릭으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="adbab-190">와 탄력적인 풀 toowork를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="adbab-191">**탄력적 풀 모니터링**에는 차트 레이블이 지정된 **리소스 사용률**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="adbab-192">Hello 차트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-192">Click hello chart.</span></span>

    ![탄력적 풀 모니터링][3]

    <span data-ttu-id="adbab-194">hello **메트릭을** 메트릭 hello 지정 된 기간 동안 지정 된 hello에 대 한 자세히 보기를 보여 주는, 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![메트릭 블레이드][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="adbab-196">toocustomize hello 차트 표시</span><span class="sxs-lookup"><span data-stu-id="adbab-196">toocustomize hello chart display</span></span>

<span data-ttu-id="adbab-197">CPU 비율, 데이터 IO 백분율 및 사용 되는 로그 IO 백분율 등 기타 메트릭을 hello 차트 및 hello 메트릭 블레이드 toodisplay 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="adbab-198">Hello 메트릭 블레이드 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-198">On hello metric blade, click **Edit**.</span></span>

    ![편집 클릭][6]

2. <span data-ttu-id="adbab-200">Hello에 **차트 편집** 블레이드에서 (지난 시간을 오늘 또는 지난 주), 시간 범위를 선택 하거나 클릭 **사용자 지정** tooselect 날짜 범위에 속하는 hello 지난 2 주입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="adbab-201">Hello 차트 종류 (가로 막대형 또는 꺾은선형)를 선택 하 고 hello 리소스 toomonitor를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="adbab-202">동일한 hello에 hello 동일한 측정 단위는 hello에 표시 될 수 있는 메트릭 차트에 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="adbab-203">예를 들어 "eDTU percentage"를 선택 하는 경우 선택할 수 있습니다만 기타 메트릭을 (백분율)으로 hello 측정 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![편집 클릭](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="adbab-205">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="adbab-206">탄력적 풀의 데이터베이스 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="adbab-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="adbab-207">문제 발생 가능성에 대한 개별 데이터베이스를 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="adbab-208">**탄력적 데이터베이스 모니터링**에는 다섯 개의 데이터베이스에 대한 메트릭을 표시하는 차트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="adbab-209">기본적으로 hello 차트 표시 hello 상위 5 데이터베이스 hello 풀의 평균 eDTU 사용량 hello에 의해 지난 시간 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="adbab-210">Hello 차트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-210">Click hello chart.</span></span>

    ![탄력적 풀 모니터링][4]

2. <span data-ttu-id="adbab-212">hello **데이터베이스 리소스 사용률** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="adbab-213">Hello 데이터베이스 사용 hello 풀에 대 한 자세히 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="adbab-214">Hello 블레이드의 hello 아래쪽 표에 hello를 사용 하 선택할 수 있습니다 데이터베이스가 hello 풀 toodisplay에 hello 차트 (too5 데이터베이스)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="adbab-215">Hello 메트릭 및 시간 창을 클릭 하 여 hello 차트에 표시를 사용자 지정할 수도 있습니다 **차트 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![데이터베이스 리소스 사용률 블레이드][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="adbab-217">toocustomize hello 보기</span><span class="sxs-lookup"><span data-stu-id="adbab-217">toocustomize hello view</span></span>

1. <span data-ttu-id="adbab-218">Hello에 **리소스 사용률이 데이터베이스** 블레이드에서 클릭 **차트 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![차트 편집 클릭](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="adbab-220">Hello에 **편집** 블레이드에서 차트, 시간 범위 (지난 시간, 지난 24 시간)를 선택 하거나 클릭 **사용자 지정** 지난 2 주 toodisplay hello에 다른 하루 tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![사용자 지정 클릭](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="adbab-222">Hello 클릭 **하 여 데이터베이스를 비교할** 드롭다운 tooselect 다른 메트릭 toouse 데이터베이스를 비교 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="adbab-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Hello 차트 편집](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="adbab-224">tooselect 데이터베이스 toomonitor</span><span class="sxs-lookup"><span data-stu-id="adbab-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="adbab-225">Hello에 hello 데이터베이스 목록에서 **데이터베이스 리소스 사용률** 블레이드에서 hello 페이지 hello 목록을 조회 하거나 데이터베이스의 hello 이름에 입력 하 여 특정 데이터베이스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="adbab-226">Hello 확인란 tooselect hello 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-226">Use hello checkbox tooselect hello database.</span></span>

![데이터베이스 toomonitor 검색][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="adbab-228">경고 tooan 탄력적 풀 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="adbab-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="adbab-229">탄력적 풀 hello 설정 하는 사용 임계값에 도달 하면 전자 메일 문자열 tooURL 끝점 toopeople 또는 경고를 전송 하는 규칙 tooan 탄력적 풀을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="adbab-230">**tooadd 경고 tooany 리소스:**</span><span class="sxs-lookup"><span data-stu-id="adbab-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="adbab-231">Hello 클릭 **리소스 사용률** 차트 tooopen hello **메트릭을** 블레이드에서 클릭 **추가 경고**, hello에 hello 정보 입력 **경고를 추가 규칙** 블레이드 (**리소스** 작업할 때 toobe hello 풀을 자동으로 설정 됩니다).</span><span class="sxs-lookup"><span data-stu-id="adbab-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="adbab-232">입력 **이름** 및 **설명** hello 경고 tooyou 및 hello 받는 사람을 식별 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="adbab-233">선택 된 **메트릭을** tooalert hello 목록에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="adbab-234">동적으로 hello 차트 메트릭 해당 toohelp에 대 한 리소스 사용률 표시 임계값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="adbab-235">**조건**(보다 큼, 보다 작음 등) 및 **임계값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="adbab-236">선택 된 **기간** 메트릭을 hello 시간의 규칙 hello 경고 트리거 하기 전에 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="adbab-237">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-237">Click **OK**.</span></span>

<span data-ttu-id="adbab-238">자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="adbab-239">탄력적 풀로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="adbab-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="adbab-240">기존 풀에서 데이터베이스를 제거하거나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="adbab-241">hello 데이터베이스가 다른 풀 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-241">hello databases can be in other pools.</span></span> <span data-ttu-id="adbab-242">그러나만 추가할 수 있습니다는에 hello 동일 데이터베이스 논리 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="adbab-243">Hello 풀에 대 한 hello 블레이드에서 아래 **탄력적 데이터베이스** 클릭 **풀 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![풀 구성 클릭][1]

2. <span data-ttu-id="adbab-245">Hello에 **풀 구성** 블레이드에서 클릭 **toopool 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![추가 toopool 클릭](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="adbab-247">Hello에 **데이터베이스를 추가할** 블레이드, 선택 hello 데이터베이스 또는 데이터베이스 tooadd toohello 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="adbab-248">그런 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-248">Then click **Select**.</span></span>

    ![데이터베이스 tooadd 선택](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="adbab-250">hello **풀 구성** 블레이드 목록 hello toobe 너무 설정 상태와 함께 추가 하면 선택한 데이터베이스는 이제**보류 중인**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![보류 중인 풀 추가](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="adbab-252">Hello에 **구성 풀 블레이드에서**, 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="adbab-254">탄력적 풀 외부로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="adbab-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="adbab-255">Hello에 **풀 구성** 블레이드, 선택 hello 데이터베이스 또는 데이터베이스 tooremove 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="adbab-257">**풀에서 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-257">Click **Remove from pool**.</span></span>

    ![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="adbab-259">hello **풀 구성** 블레이드 목록 hello 너무 설정 상태가 제거할 toobe 선택한 데이터베이스는 이제**보류 중인**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![데이터베이스 추가 및 제거 미리 보기](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="adbab-261">Hello에 **구성 풀 블레이드에서**, 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="adbab-263">탄력적 풀의 성능 설정 변경</span><span class="sxs-lookup"><span data-stu-id="adbab-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="adbab-264">탄력적 풀의 hello 리소스 사용률을 모니터링 하면서 약간씩 조정 필요한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="adbab-265">아마 hello 풀 hello 성능이 나 저장소 제한 변경을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="adbab-266">Hello 풀에서 toochange hello 데이터베이스 설정을 원하는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="adbab-267">모든 시간 tooget hello 적절 한 성능 및 비용에 hello 풀의 hello 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="adbab-268">자세한 내용은 [탄력적 풀을 사용해야 하는 경우](sql-database-elastic-pool.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="adbab-269">toochange hello Edtu 또는 저장소 풀 및 데이터베이스당 Edtu 당 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="adbab-270">열기 hello **풀 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="adbab-271">아래 **탄력적 풀 설정**, 풀 설정을 하거나 슬라이더 toochange hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![탄력적 풀 리소스 사용률](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="adbab-273">Hello 설정이 변경 되 면 hello 표시 hello hello 변경의 월별 비용을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![탄력적 풀 및 새 월별 비용 업데이트](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="adbab-275">탄력적 풀 작업의 대기 시간</span><span class="sxs-lookup"><span data-stu-id="adbab-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="adbab-276">5 분 이내에 완료 데이터베이스 마다 데이터베이스 또는 최대 Edtu 당 hello 최소 Edtu를 일반적으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="adbab-277">Hello Edtu 풀 당 변경 hello hello 풀의 모든 데이터베이스에 사용 되는 공간의 총 금액에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="adbab-278">변경 시간은 100GB당 평균 90분 이하입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="adbab-279">예를 들어 hello 총 공간에서 사용 하는 경우 hello 풀의 모든 데이터베이스는 200GB, 다음 hello 필요한 hello 풀 eDTU 풀 당 변경에 대 한 대기 시간은 3 시간 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adbab-280">다음 단계</span><span class="sxs-lookup"><span data-stu-id="adbab-280">Next steps</span></span>

- <span data-ttu-id="adbab-281">어떤 탄력적 풀 참조 이면 toounderstand [SQL 데이터베이스 탄력적 풀](sql-database-elastic-pool.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="adbab-282">탄력적 풀 사용에 대한 지침을 보려면 [탄력적 풀의 가격 및 성능 고려 사항](sql-database-elastic-pool.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adbab-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="adbab-283">임의 개수의 hello 풀의 데이터베이스에 대해 toouse 탄력적 작업 toorun Transact SQL 스크립트 참조 [탄력적 작업 개요](sql-database-elastic-jobs-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="adbab-284">hello 풀의 데이터베이스 수 전체 tooquery 참조 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="adbab-285">트랜잭션에 대 한 여러 hello 풀에 데이터베이스 참조 [탄력적 트랜잭션을](sql-database-elastic-transactions-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="adbab-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
