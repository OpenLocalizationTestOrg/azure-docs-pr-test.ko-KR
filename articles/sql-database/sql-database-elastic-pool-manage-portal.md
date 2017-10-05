---
title: "Azure Portal: SQL Database 탄력적 풀 만들기 및 관리 | Microsoft Docs"
description: "Azure Portal 및 SQL Database의 기본 제공 인텔리전스를 사용하여 데이터베이스 성능을 최적화하고 비용을 관리하기 위해 확장성 있는 탄력적 풀을 관리하고, 모니터링하고, 적정 크기로 조정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="07848-103">Azure Portal을 사용하여 탄력적 풀 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="07848-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="07848-104">이 항목에서는 Azure Portal을 사용하여 확장 가능한 [탄력적 풀](sql-database-elastic-pool.md)을 만들고 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07848-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="07848-105">[PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API 또는 [C#](sql-database-elastic-pool-manage-csharp.md)을 사용하여 Azure 탄력적 풀을 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="07848-106">[Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="07848-107">탄력적 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="07848-107">Create an elastic pool</span></span> 

<span data-ttu-id="07848-108">두 가지 방법으로 탄력적 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="07848-109">원하는 풀 설정을 알고 있는 경우 처음부터 수행하거나 서비스에서 권장 내용으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="07848-110">SQL Database에는 데이터베이스에 대한 과거 사용량 원격 분석을 기반으로 보다 비용 효율적인 경우 탄력적 풀 설정을 권장하는 기본 제공 인텔리전스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="07848-111">서버에 풀을 여러 개 만들 수 있지만 다른 서버에 속하는 데이터베이스를 동일한 풀에 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="07848-112">탄력적 풀은 현재 미리 보기 상태인 인도 서부를 제외한 모든 Azure 지역에서 일반 공급(GA) 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="07848-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="07848-113">이 영역에서 탄력적 풀의 GA는 가능한 한 빨리 수행될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="07848-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="07848-114">1단계: 탄력적 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="07848-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="07848-115">포털의 기존 **서버** 블레이드에서 탄력적 풀을 만드는 것은 기존 데이터베이스를 탄력적 풀로 이동하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07848-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="07848-116">**Marketplace**에서 **SQL 탄력적 풀**을 검색하거나 **SQL 탄력적 풀** 찾아보기 블레이드에서 **+추가**를 클릭하여 탄력적 풀을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="07848-117">이 풀 프로비저닝 워크플로를 통해 새 서버 또는 기존 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="07848-118">[Azure Portal](http://portal.azure.com/)에서 **더 많은 서비스** **>** **SQL Server**를 클릭한 다음 탄력적 풀에 추가할 데이터베이스를 포함하는 서버를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="07848-119">**새 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-119">Click **New pool**.</span></span>

    ![서버에 풀 추가](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="07848-121">**또는**</span><span class="sxs-lookup"><span data-stu-id="07848-121">**-OR-**</span></span>

    <span data-ttu-id="07848-122">서버에 대해 권장되는 탄력적 풀이 있다는 메시지를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="07848-123">메시지를 클릭하여 기록 데이터베이스 사용량 원격 분석에 따라 권장된 풀을 확인한 다음 계층을 클릭하여 자세한 내용을 보고 풀을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="07848-124">권장 사항을 만드는 방법은 이 항목의 뒷부분에서 [풀 권장 사항 이해](#understand-elastic-pool-recommendations) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="07848-126">풀에 대한 설정을 지정하는 **탄력적 풀** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07848-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="07848-127">이전 단계에서 **새 풀**을 클릭한 경우 가격 책정 계층은 기본적으로 **표준**이며 선택한 데이터베이스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="07848-128">빈 풀을 만들거나 해당 서버에서 풀로 이동할 기존 데이터베이스의 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="07848-129">권장되는 풀을 만드는 경우 권장되는 가격 책정 계층, 성능 설정 및 데이터베이스 목록이 채워지지만 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![탄력적 풀 구성](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="07848-131">탄력적 풀의 이름을 지정하거나 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="07848-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="07848-132">2단계: 가격 책정 계층 선택</span><span class="sxs-lookup"><span data-stu-id="07848-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="07848-133">풀의 가격 책정 계층에 따라 풀에 있는 탄력적 데이터베이스에서 사용 가능한 기능과 각 데이터베이스에서 사용 가능한 최대 eDTU 수(eDTU MAX) 및 저장소(GB)가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="07848-134">자세한 내용은 서비스 계층을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="07848-135">풀에 대한 가격 책정 계층을 변경하려면 **가격 책정 계층**, 원하는 가격 책정 계층, **선택**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07848-136">가격 책정 계층을 선택하고 마지막 단계에서 **확인**을 클릭하여 변경 내용을 적용한 후에는 풀의 가격 책정 계층을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="07848-137">기존 탄력적 풀의 가격 책정 계층을 변경하려면 원하는 가격 책정 계층에서 탄력적 풀을 만들고 데이터베이스를 이 새로운 풀로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![가격 책정 계층 선택](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="07848-139">3단계: 풀 구성</span><span class="sxs-lookup"><span data-stu-id="07848-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="07848-140">가격 책정 계층을 설정한 후에, 데이터베이스를 추가할 풀의 구성을 클릭하고, 풀 eDTU 및 저장소(풀 GB), 그리고 풀의 탄력적 데이터베이스에 대한 최대 및 최소 eDTU를 설정할 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="07848-141">**풀 구성**</span><span class="sxs-lookup"><span data-stu-id="07848-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="07848-142">풀에 추가하려는 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="07848-143">이 단계는 풀을 만드는 과정의 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="07848-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="07848-144">데이터베이스는 풀이 생성된 후에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="07848-145">데이터베이스를 추가하려면 **데이터베이스 추가**, 추가하려는 데이터베이스, **선택** 단추를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![데이터베이스 추가](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="07848-147">사용하고 있는 데이터베이스에 충분한 기록 사용량 원격 분석이 있는 경우 **예상되는 eDTU 및 GB 사용량** 그래프 및 **실제 eDTU 사용량** 막대형 차트는 구성을 결정할 수 있도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="07848-148">또한 서비스가 적정 크기의 풀을 만들도록 권장 사항 메시지를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="07848-149">[동적 권장 사항](#understand-elastic-pool-recommendations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="07848-150">**풀 구성** 페이지에서 제어를 사용하여 설정을 탐색하고 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="07848-151">각 서비스 계층의 제한에 대한 자세한 내용은 [탄력적 풀 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하고 적정한 탄력적 풀의 크기에 대한 자세한 지침은 [탄력적 풀에 대한 가격 및 성능 고려 사항](sql-database-elastic-pool.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="07848-152">풀 설정에 대한 자세한 내용은 [탄력적 풀 속성](sql-database-elastic-pool.md#database-properties-for-pooled-databases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![탄력적 풀 구성](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="07848-154">**선택** in the **Configure Pool** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="07848-155">**확인** 을 클릭하여 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07848-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="07848-156">탄력적 풀 권장 사항 이해</span><span class="sxs-lookup"><span data-stu-id="07848-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="07848-157">SQL 데이터베이스 서비스는 사용 기록을 평가하고 단일 데이터베이스를 사용하는 경우보다 비용 효율적인 경우 하나 이상의 풀을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="07848-158">각 권장 사항은 풀에 가장 적합한 서버 데이터베이스의 고유한 하위 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="07848-160">풀 권장 사항은 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="07848-161">풀에 대한 가격 책정 계층(Basic, Standard, Premium 또는 Premium RS)</span><span class="sxs-lookup"><span data-stu-id="07848-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="07848-162">적절한 **풀 eDTU** (풀당 최대 eDTU)</span><span class="sxs-lookup"><span data-stu-id="07848-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="07848-163">데이터베이스당 **eDTU 최대** 및 **eDTU 최소**</span><span class="sxs-lookup"><span data-stu-id="07848-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="07848-164">풀에 대한 권장 데이터베이스 목록</span><span class="sxs-lookup"><span data-stu-id="07848-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07848-165">서비스는 풀을 권장할 때 최근 30일간의 원격 분석을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="07848-166">데이터베이스가 탄력적 풀의 후보로 간주되려면 7일 이상 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="07848-167">이미 탄력적 풀에 있는 데이터베이스는 탄력적 풀 권장 사항에 대한 후보로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="07848-168">서비스는 리소스 요구와 각 서비스 계층에 있는 단일 데이터베이스를 동일한 계층의 풀로 이동하는 경우 비용 효율성을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="07848-169">예를 들어 서버의 모든 Standard 데이터베이스는 표준 탄력적 풀에 적합한지 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="07848-170">즉, 서비스는 Standard 데이터베이스를 Premium 풀로 이동하는 경우와 같은 계층 간 권장 사항을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="07848-171">풀에 데이터베이스를 추가한 후에는, 사용자가 선택한 데이터베이스의 기존 사용 정보를 기반으로 권장 사항이 동적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="07848-172">권장 사항은 eDTU 및 GB 사용 현황 차트는 물론 **풀 구성** 블레이드 상단의 권장 사항 배너에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="07848-173">권장 사항은 특정 데이터베이스에 최적화된 탄력적 풀을 만드는 데 도움을 주기 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![동적 권장 사항](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="07848-175">탄력적 풀 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="07848-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="07848-176">Azure Portal을 사용하여 풀에서 탄력적 풀 및 데이터베이스를 모니터링하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="07848-177">포털에서 탄력적 풀 및 해당 풀 내의 데이터베이스의 사용률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="07848-178">탄력적 풀에 일련의 내용을 변경하는 동시에 모든 변경 내용을 전송할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="07848-179">이러한 변경 내용에는 데이터베이스 추가 또는 제거, 탄력적 풀 설정 변경, 데이터베이스 설정 변경이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="07848-180">다음 그림에서는 탄력적 풀 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07848-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="07848-181">보기에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-181">The view includes:</span></span>

*  <span data-ttu-id="07848-182">탄력적 풀과 풀에 포함된 데이터베이스 모두의 리소스 사용을 모니터링하는 차트</span><span class="sxs-lookup"><span data-stu-id="07848-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="07848-183">탄력적 풀을 변경하는 **구성** 풀 단추</span><span class="sxs-lookup"><span data-stu-id="07848-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="07848-184">데이터베이스를 만들고 현재 탄력적 풀에 추가하는 **데이터베이스 만들기** 단추</span><span class="sxs-lookup"><span data-stu-id="07848-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="07848-185">목록의 모든 데이터베이스에 대해 Transact SQL 스크립트를 실행하여 많은 데이터베이스를 관리하는 데 도움이 되는 탄력적 작업</span><span class="sxs-lookup"><span data-stu-id="07848-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![풀 보기][2]

<span data-ttu-id="07848-187">특정 풀로 이동하여 해당 리소스 사용률을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="07848-188">기본적으로 풀은 지난 1시간 동안 저장소 및 eDTU 사용량을 표시하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="07848-189">다양한 시간 창에 다양한 메트릭이 표시되도록 차트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="07848-190">사용할 탄력적 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="07848-191">**탄력적 풀 모니터링**에는 차트 레이블이 지정된 **리소스 사용률**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="07848-192">차트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-192">Click the chart.</span></span>

    ![탄력적 풀 모니터링][3]

    <span data-ttu-id="07848-194">**메트릭** 블레이드가 열리고 지정된 시간 창에 지정된 메트릭의 자세히 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07848-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![메트릭 블레이드][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="07848-196">차트 표시를 사용자 지정하려면</span><span class="sxs-lookup"><span data-stu-id="07848-196">To customize the chart display</span></span>

<span data-ttu-id="07848-197">차트 및 메트릭 블레이드를 편집하여 CPU 비율, 데이터 IO 비율, 사용되는 로그 IO 백분율 등 다른 메트릭을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="07848-198">메트릭 블레이드에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-198">On the metric blade, click **Edit**.</span></span>

    ![편집 클릭][6]

2. <span data-ttu-id="07848-200">**차트 편집** 블레이드에서 시간 범위(지난 시간, 오늘 또는 지난 주)를 선택하거나 **사용자 지정**을 클릭하여 지난 두 주 동안의 데이터 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="07848-201">차트 종류(가로 막대형 또는 꺾은선형)를 선택하고 모니터링할 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="07848-202">측정 단위가 동일한 메트릭만 차트에 동시에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="07848-203">예를 들어, “eDTU 백분율”을 선택하면 측정 단위로 다른 백분율 메트릭만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![편집 클릭](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="07848-205">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="07848-206">탄력적 풀의 데이터베이스 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="07848-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="07848-207">문제 발생 가능성에 대한 개별 데이터베이스를 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="07848-208">**탄력적 데이터베이스 모니터링**에는 다섯 개의 데이터베이스에 대한 메트릭을 표시하는 차트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="07848-209">기본적으로 차트는 지난 한 시간 동안 평균 eDTU별로 풀의 상위 5개 데이터베이스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="07848-210">차트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-210">Click the chart.</span></span>

    ![탄력적 풀 모니터링][4]

2. <span data-ttu-id="07848-212">**데이터베이스 리소스 사용률** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07848-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="07848-213">풀에서 데이터베이스 사용량의 세부 정보 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="07848-214">블레이드의 아래쪽에 있는 표를 사용하여 차트(최대 5개의 데이터베이스)에서 사용량을 표시하도록 풀에서 모든 데이터베이스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="07848-215">**차트 편집**을 클릭하여 차트에 표시되는 메트릭 및 시간 창을 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![데이터베이스 리소스 사용률 블레이드][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="07848-217">보기를 사용자 지정하려면</span><span class="sxs-lookup"><span data-stu-id="07848-217">To customize the view</span></span>

1. <span data-ttu-id="07848-218">**데이터베이스 리소스 사용률** 블레이드에서 **차트 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![차트 편집 클릭](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="07848-220">**차트** 편집 블레이드에서 시간 범위(지난 시간 또는 지난 24시간)를 선택하거나 **사용자 지정**을 클릭하여 지난 2주 동안에서 표시할 다른 날을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![사용자 지정 클릭](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="07848-222">**데이터베이스 비교 기준** 드롭다운을 클릭하여 데이터베이스를 비교할 경우 사용할 다른 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![차트 편집](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="07848-224">모니터링할 데이터베이스를 선택하려면</span><span class="sxs-lookup"><span data-stu-id="07848-224">To select databases to monitor</span></span>

<span data-ttu-id="07848-225">데이터베이스 목록의 **데이터베이스 리소스 사용률** 블레이드에서 목록에 있는 페이지를 탐색하거나 데이터베이스의 이름을 입력하여 특정 데이터베이스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="07848-226">확인란을 사용하여 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-226">Use the checkbox to select the database.</span></span>

![모니터링할 데이터베이스 검색][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="07848-228">탄력적 풀 리소스에 경고 추가</span><span class="sxs-lookup"><span data-stu-id="07848-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="07848-229">탄력적 풀에 규칙을 추가하여 탄력적 풀이 설정한 사용률 임계값에 도달할 경우 사용자에게 전자 메일을 보내거나 URL 끝점에 경고 문자열을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="07848-230">**리소스에 경고 추가:**</span><span class="sxs-lookup"><span data-stu-id="07848-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="07848-231">**리소스 사용률** 차트를 클릭하여 **메트릭** 블레이드를 열고 **경고 추가**를 클릭한 다음 **경고 규칙 추가** 블레이드에 정보를 입력합니다(**리소스**는 자동으로 작업 중인 풀로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="07848-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="07848-232">사용자 및 받는 사람에 대한 경고를 식별하는 **이름** 및 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="07848-233">목록에서 경고하려는 **메트릭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="07848-234">차트는 동적으로 임계값을 선택할 수 있도록 해당 메트릭에 대한 리소스 사용률을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="07848-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="07848-235">**조건**(보다 큼, 보다 작음 등) 및 **임계값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="07848-236">경고를 트리거하기 전에 메트릭 규칙을 만족해야 하는 **기간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="07848-237">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-237">Click **OK**.</span></span>

<span data-ttu-id="07848-238">자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="07848-239">탄력적 풀로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="07848-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="07848-240">기존 풀에서 데이터베이스를 제거하거나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="07848-241">데이터베이스가 다른 풀에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-241">The databases can be in other pools.</span></span> <span data-ttu-id="07848-242">그러나 동일한 논리 서버에 있는 데이터베이스만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="07848-243">풀에 대한 블레이드에서, **Elastic Database** 아래에서 **풀 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![풀 구성 클릭][1]

2. <span data-ttu-id="07848-245">**풀 구성** 블레이드에서 **풀에 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![풀에 추가 클릭](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="07848-247">**데이터베이스 추가** 블레이드에서 풀에 추가할 데이터베이스를 하나 이상 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="07848-248">그런 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-248">Then click **Select**.</span></span>

    ![추가할 데이터베이스 선택](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="07848-250">이제 **풀 구성** 블레이드에 추가하려고 선택한 데이터베이스가 **보류 중**으로 상태가 설정되어 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![보류 중인 풀 추가](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="07848-252">**풀 구성 블레이드**에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="07848-254">탄력적 풀 외부로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="07848-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="07848-255">**풀 구성** 블레이드에서 제거할 데이터베이스를 하나 이상 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="07848-257">**풀에서 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-257">Click **Remove from pool**.</span></span>

    ![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="07848-259">이제 **풀 구성** 블레이드에 제거하려고 선택한 데이터베이스가 **보류 중**으로 상태가 설정되어 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![데이터베이스 추가 및 제거 미리 보기](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="07848-261">**풀 구성 블레이드**에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="07848-263">탄력적 풀의 성능 설정 변경</span><span class="sxs-lookup"><span data-stu-id="07848-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="07848-264">탄력적 풀의 리소스 사용률을 모니터링하면서 일부 조정이 필요함을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="07848-265">어쩌면 풀에서 성능이나 저장소 제한을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="07848-266">풀에서 데이터베이스 설정을 변경하려고 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="07848-267">언제든지 풀의 설치 프로그램을 변경하여 적절한 성능 및 비용을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07848-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="07848-268">자세한 내용은 [탄력적 풀을 사용해야 하는 경우](sql-database-elastic-pool.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="07848-269">풀당 eDTU 또는 저장소 제한 및 데이터베이스당 eDTU를 변경하려면:</span><span class="sxs-lookup"><span data-stu-id="07848-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="07848-270">**풀 구성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07848-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="07848-271">**탄력적 풀 설정**에서 슬라이더를 사용하여 풀 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="07848-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![탄력적 풀 리소스 사용률](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="07848-273">설정이 변경되면 디스플레이에 변경의 예상된 월별 비용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![탄력적 풀 및 새 월별 비용 업데이트](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="07848-275">탄력적 풀 작업의 대기 시간</span><span class="sxs-lookup"><span data-stu-id="07848-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="07848-276">데이터베이스당 최소 eDTU 또는 데이터베이스당 최대 eDTU를 변경하는 작업은 일반적으로 5분 이내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="07848-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="07848-277">풀당 eDTU를 변경하는 작업은 풀에 있는 모든 데이터베이스에서 사용한 공간의 전체 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="07848-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="07848-278">변경 시간은 100GB당 평균 90분 이하입니다.</span><span class="sxs-lookup"><span data-stu-id="07848-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="07848-279">예를 들어 풀에 있는 모든 데이터베이스에서 사용 중인 총 공간이 200GB일 경우, 풀당 풀 eDTU를 변경하는 예상 대기 시간은 3시간 이하입니다.</span><span class="sxs-lookup"><span data-stu-id="07848-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07848-280">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07848-280">Next steps</span></span>

- <span data-ttu-id="07848-281">탄력적 풀을 이해하려면 [SQL Database 탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="07848-282">탄력적 풀 사용에 대한 지침을 보려면 [탄력적 풀의 가격 및 성능 고려 사항](sql-database-elastic-pool.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="07848-283">탄력적 작업을 사용하여 개수에 관계없이 풀에 있는 데이터베이스에 대해 Transact-SQL 스크립트를 실행하려면 [탄력적 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="07848-284">개수에 관계없이 풀에 있는 데이터베이스를 쿼리하려면 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="07848-285">개수에 관계없는 풀의 데이터베이스 트랜잭션의 경우 [탄력적 트랜잭션](sql-database-elastic-transactions-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07848-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
