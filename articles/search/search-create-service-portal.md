---
title: "포털에서 Azure Search 서비스 만들기 | Microsoft Docs"
description: "포털에서 Azure Search 서비스 프로비전합니다."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 58f4eab190e40e16ed261c165ffdfc8155eeb434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-search-service-in-the-portal"></a><span data-ttu-id="ab628-103">포털에서 Azure 검색서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ab628-103">Create an Azure Search service in the portal</span></span>

<span data-ttu-id="ab628-104">이 문서에서는 포털에서 Azure Search 서비스를 만들거나 프로비전하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-104">This article explains how to create or provision an Azure Search service in the portal.</span></span> <span data-ttu-id="ab628-105">PowerShell 지침에 대한 자세한 내용은 [PowerShell을 사용하여 Azure Search 관리](search-manage-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="ab628-106">구독(무료 또는 유료)</span><span class="sxs-lookup"><span data-stu-id="ab628-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="ab628-107">[무료 Azure 계정을 열고](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) 무료 크레딧을 사용하여 유료 Azure 서비스를 사용해보세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits to try out paid Azure services.</span></span> <span data-ttu-id="ab628-108">크레딧이 소진되더라도 계정이 유지되므로 Websites와 같은 무료 Azure 서비스를 계속 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-108">After credits are used up, keep the account and continue to use free Azure services, such as Websites.</span></span> <span data-ttu-id="ab628-109">설정을 명시적으로 변경하여 결제를 요청하지 않는 한 신용 카드로 결제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-109">Your credit card is never charged unless you explicitly change your settings and ask to be charged.</span></span>

<span data-ttu-id="ab628-110">아니면 [MSDN 구독자 혜택을 활성화합니다](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ab628-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="ab628-111">MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="ab628-112">Azure Search 찾기</span><span class="sxs-lookup"><span data-stu-id="ab628-112">Find Azure Search</span></span>
1. <span data-ttu-id="ab628-113">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-113">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ab628-114">왼쪽 위 모퉁이에서 더하기 기호("+")를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-114">Click the plus sign ("+") in the top left corner.</span></span>
3. <span data-ttu-id="ab628-115">**웹 + 모바일** > **Azure Search**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-the-service-and-url-endpoint"></a><span data-ttu-id="ab628-116">서비스 및 URL 끝점의 이름</span><span class="sxs-lookup"><span data-stu-id="ab628-116">Name the service and URL endpoint</span></span>

<span data-ttu-id="ab628-117">서비스 이름은 API 호출이 발급되는 URL 끝점의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-117">A service name is part of the URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="ab628-118">**URL** 필드에 서비스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-118">Type your service name in the **URL** field.</span></span> 

<span data-ttu-id="ab628-119">서비스 이름 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="ab628-119">Service name requirements:</span></span>
   * <span data-ttu-id="ab628-120">2 ~ 60자 길이</span><span class="sxs-lookup"><span data-stu-id="ab628-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="ab628-121">소문자, 숫자 또는 대시("-")</span><span class="sxs-lookup"><span data-stu-id="ab628-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="ab628-122">첫 두 문자 또는 마지막 한 문자에는 대시("-")를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ab628-122">no dash ("-") as the first 2 characters or last single character</span></span>
   * <span data-ttu-id="ab628-123">연속 대시("--")를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ab628-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="ab628-124">구독 선택</span><span class="sxs-lookup"><span data-stu-id="ab628-124">Select a subscription</span></span>
<span data-ttu-id="ab628-125">둘 이상의 구독이 있는 경우 데이터 또는 파일 저장소 서비스도 있는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="ab628-126">Azure Search는 *인덱서*를 통해 인덱싱하기 위해 Azure Table 및 Blob Storage, SQL Database, Azure Cosmos DB를 자동 검색할 수 있지만, 동일한 구독의 서비스에 대해서만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in the same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="ab628-127">리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="ab628-127">Select a resource group</span></span>
<span data-ttu-id="ab628-128">리소스 그룹은 함께 사용된 Azure 서비스 및 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="ab628-129">예를 들어 Azure Search를 사용하여 SQL Database를 인덱싱하는 경우 이들 두 서비스는 동일한 리소스 그룹의 일부여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-129">For example, if you are using Azure Search to index a SQL database, then both services should be part of the same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="ab628-130">리소스 그룹을 삭제하면 그 안의 서비스도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-130">Deleting a resource group also deletes the services within it.</span></span> <span data-ttu-id="ab628-131">여러 서비스를 이용하는 프로토타입 프로젝트의 경우, 이들을 모두 동일한 리소스 그룹에 배치하면 프로젝트가 종료된 후 쉽게 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-131">For prototype projects utilizing multiple services, putting all of them in the same resource group makes cleanup easier after the project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="ab628-132">호스팅 위치 선택</span><span class="sxs-lookup"><span data-stu-id="ab628-132">Select a hosting location</span></span> 
<span data-ttu-id="ab628-133">Azure 서비스인 Azure Search는 전 세계 데이터 센터에서 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-133">As an Azure service, Azure Search can be hosted in datacenters around the world.</span></span> <span data-ttu-id="ab628-134">지역별로 [가격이 다를 수](https://azure.microsoft.com/pricing/details/search/) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="ab628-135">가격 책정 계층(SKU) 선택</span><span class="sxs-lookup"><span data-stu-id="ab628-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="ab628-136">[Azure 검색은 무료, 기본 또는 표준 등 여러 가지 가격 책정 계층에서 현재 제공됩니다](https://azure.microsoft.com/pricing/details/search/).</span><span class="sxs-lookup"><span data-stu-id="ab628-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="ab628-137">각 계층에는 자체 [용량 및 제한](search-limits-quotas-capacity.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="ab628-138">지침은 [가격 책정 계층 또는 SKU 선택](search-sku-tier.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="ab628-139">이 연습에서는 서비스에 대한 표준 계층을 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-139">In this walkthrough, we have chosen the Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="ab628-140">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ab628-140">Create your service</span></span>

<span data-ttu-id="ab628-141">로그인할 때마다 손쉽게 액세스할 수 있도록 서비스를 대시보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-141">Remember to pin your service to the dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="ab628-142">서비스 확장</span><span class="sxs-lookup"><span data-stu-id="ab628-142">Scale your service</span></span>
<span data-ttu-id="ab628-143">서비스를 만드는 데 몇 분 정도 걸릴 수 있습니다(15분 이상 계층에 따라).</span><span class="sxs-lookup"><span data-stu-id="ab628-143">It can take a few minutes to create a service (15 minutes or more depending on the tier).</span></span> <span data-ttu-id="ab628-144">서비스가 프로비전되면 사용자의 요구에 맞게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-144">After your service is provisioned, you can scale it to meet your needs.</span></span> <span data-ttu-id="ab628-145">Azure Search 서비스에 대한 표준 계층을 선택했기 때문에 복제본과 파티션이라는 두 개의 차원에서 서비스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-145">Because you chose the Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="ab628-146">기본 계층을 선택한 경우 복제본만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-146">Had you chosen the Basic tier, you can only add replicas.</span></span> <span data-ttu-id="ab628-147">무료 서비스를 프로비전한 경우 확장이 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-147">If you provisioned the free service, scale is not available.</span></span>

<span data-ttu-id="ab628-148">***파티션***을 사용하면 서비스를 저장하고 더 많은 문서를 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-148">***Partitions*** allow your service to store and search through more documents.</span></span>

<span data-ttu-id="ab628-149">***복제본***을 사용하면 서비스가 더 큰 부하의 검색 쿼리를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-149">***Replicas*** allow your service to handle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="ab628-150">서비스는 [SLA 읽기 전용으로 2개의 복제본과 SLA 읽기/쓰기용으로 3개의 복제본](https://azure.microsoft.com/support/legal/sla/search/v1_0/)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="ab628-151">Azure Portal의 검색 서비스 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-151">Go to your search service blade in the Azure portal.</span></span>
2. <span data-ttu-id="ab628-152">왼쪽 탐색 창에서 **설정** > **규모**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-152">In the left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="ab628-153">슬라이드 바를 사용하여 복제본 또는 파티션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-153">Use the slidebar to add Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="ab628-154">각 계층에는 단일 서비스에서 허용하는 총 검색 단위 수(복제본 * 파티션 = 총 검색 단위)에 여러 [제한](search-limits-quotas-capacity.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-154">Each tier has different [limits](search-limits-quotas-capacity.md) on the total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-to-add-a-second-service"></a><span data-ttu-id="ab628-155">두 번째 서비스를 추가하는 경우</span><span class="sxs-lookup"><span data-stu-id="ab628-155">When to add a second service</span></span>

<span data-ttu-id="ab628-156">대부분의 고객은 [적절히 균형 잡힌 리소스](search-sku-tier.md)를 제공하는 계층에 프로비전되는 하나의 서비스만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-156">A large majority of customers use just one service provisioned at a tier that provides the [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="ab628-157">하나의 서비스는 [선택한 계층의 최대 제한](search-capacity-planning.md)에 따라 서로 분리된 여러 인덱스를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-157">One service can host multiple indexes, subject to the [maximum limits of the tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="ab628-158">Azure Search에서 요청은 하나의 인덱스로만 리디렉션될 수 있으므로 같은 서비스의 다른 인덱스에서 실수로 또는 의도적으로 데이터가 검색될 가능성이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-158">In Azure Search, requests can only be directed to one index, minimizing the chance of accidental or intentional data retrieval from other indexes in the same service.</span></span>

<span data-ttu-id="ab628-159">대부분의 고객이 하나의 서비스만 사용하지만 운영과 관련해서 다음과 같은 사항이 요구될 경우 서비스 중복성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include the following:</span></span>

+ <span data-ttu-id="ab628-160">재해 복구(데이터 센터 작동 중단).</span><span class="sxs-lookup"><span data-stu-id="ab628-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="ab628-161">Azure Search는 가동 중단 시 즉각적인 장애 조치(failover)를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-161">Azure Search does not provide instant failover in the event of an outage.</span></span> <span data-ttu-id="ab628-162">권장 사항 및 지침에 대해서는 [서비스 관리](search-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="ab628-163">다중 테넌트 모델링을 조사한 결과, 추가 서비스가 최적의 디자인이라는 사실이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-163">Your investigation of multi-tenancy modeling has determined that additional services is the optimal design.</span></span> <span data-ttu-id="ab628-164">자세한 내용은 [다중 테넌트 디자인](search-modeling-multitenant-saas-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="ab628-165">전역으로 배포된 응용 프로그램의 경우 응용 프로그램 해외 트래픽 대기 시간을 최소화하기 위해 여러 하위 지역에 Azure Search 인스턴스가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions to minimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="ab628-166">Azure Search에서는 인덱싱 및 쿼리 작업을 분리할 수 없습니다. 따라서 분리 된 작업에 대해 여러 서비스를 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="ab628-167">인덱스는 항상 만들어진 서비스에서 쿼리됩니다(한 서비스에서 인덱스를 만든 후 다른 서비스로 복사할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="ab628-167">An index is always queried on the service in which it was created (you cannot create an index in one service and copy it to another).</span></span>
>

<span data-ttu-id="ab628-168">고가용성을 위해 두 번째 서비스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-168">A second service is not required for high availability.</span></span> <span data-ttu-id="ab628-169">동일한 서비스에 두 개 이상의 복제본을 사용하는 경우 쿼리에 대한 가용성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-169">High availability for queries is achieved when you use 2 or more replicas in the same service.</span></span> <span data-ttu-id="ab628-170">복제본 업데이트는 순차적입니다. 즉, 서비스 업데이트가 롤아웃될 때도 적어도 하나의 서비스는 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out.</span></span> <span data-ttu-id="ab628-171">가동 시간에 대한 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/search/v1_0/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-171">For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab628-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab628-172">Next steps</span></span>
<span data-ttu-id="ab628-173">Azure Search 서비스를 프로비전한 후에 [인덱스를 정의](search-what-is-an-index.md)할 준비가 되었으므로 데이터를 업로드하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-173">After provisioning an Azure Search service, you are ready to [define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="ab628-174">코드 또는 스크립트에서 서비스에 액세스하려면 URL(*service-name*.search.windows.net)과 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-174">To access the service from code or script, provide the URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="ab628-175">관리 키는 모든 액세스 권한을 부여하고, 쿼리 키는 읽기 전용 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ab628-175">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="ab628-176">시작하려면 [.NET에서 Azure Search를 사용하는 방법](search-howto-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-176">See [How to use Azure Search in .NET](search-howto-dotnet-sdk.md) to get started.</span></span>

<span data-ttu-id="ab628-177">빠른 포털 기반 자습서는 [첫 번째 인덱스 빌드 및 쿼리](search-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab628-177">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

