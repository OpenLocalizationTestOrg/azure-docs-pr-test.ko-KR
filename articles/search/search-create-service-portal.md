---
title: "aaaCreate hello 포털에서 Azure 검색 서비스 | Microsoft Docs"
description: "Hello 포털에서 Azure 검색 서비스를 프로 비전 합니다."
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
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a><span data-ttu-id="96935-103">Hello 포털에서 Azure 검색 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="96935-103">Create an Azure Search service in hello portal</span></span>

<span data-ttu-id="96935-104">이 문서 어떻게 toocreate 또는 프로 비전 한 Azure 검색 서비스 hello 포털에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-104">This article explains how toocreate or provision an Azure Search service in hello portal.</span></span> <span data-ttu-id="96935-105">PowerShell 지침에 대한 자세한 내용은 [PowerShell을 사용하여 Azure Search 관리](search-manage-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96935-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="96935-106">구독(무료 또는 유료)</span><span class="sxs-lookup"><span data-stu-id="96935-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="96935-107">[무료 Azure 계정을 엽니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) 아웃 무료 크레딧을 tootry 유료 Azure 서비스를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits tootry out paid Azure services.</span></span> <span data-ttu-id="96935-108">크레딧을 모두 사용 된 후 hello 계정을 유지 하 고 toouse 무료 Azure 같은 서비스를 웹 사이트를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-108">After credits are used up, keep hello account and continue toouse free Azure services, such as Websites.</span></span> <span data-ttu-id="96935-109">명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드 청구 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96935-109">Your credit card is never charged unless you explicitly change your settings and ask toobe charged.</span></span>

<span data-ttu-id="96935-110">아니면 [MSDN 구독자 혜택을 활성화합니다](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="96935-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="96935-111">MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="96935-112">Azure Search 찾기</span><span class="sxs-lookup"><span data-stu-id="96935-112">Find Azure Search</span></span>
1. <span data-ttu-id="96935-113">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-113">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="96935-114">Hello 왼쪽 위 모서리의에서 hello 더하기 기호 ("+")를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-114">Click hello plus sign ("+") in hello top left corner.</span></span>
3. <span data-ttu-id="96935-115">**웹 + 모바일** > **Azure Search**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a><span data-ttu-id="96935-116">이름 hello 서비스와 끝점 URL</span><span class="sxs-lookup"><span data-stu-id="96935-116">Name hello service and URL endpoint</span></span>

<span data-ttu-id="96935-117">서비스 이름은 API 호출은 발급 된 hello URL 끝점의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="96935-117">A service name is part of hello URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="96935-118">Hello에 서비스 이름을 입력 **URL** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="96935-118">Type your service name in hello **URL** field.</span></span> 

<span data-ttu-id="96935-119">서비스 이름 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="96935-119">Service name requirements:</span></span>
   * <span data-ttu-id="96935-120">2 ~ 60자 길이</span><span class="sxs-lookup"><span data-stu-id="96935-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="96935-121">소문자, 숫자 또는 대시("-")</span><span class="sxs-lookup"><span data-stu-id="96935-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="96935-122">없음 대시 ("-")으로 hello 처음 두 문자나 마지막 단일 문자</span><span class="sxs-lookup"><span data-stu-id="96935-122">no dash ("-") as hello first 2 characters or last single character</span></span>
   * <span data-ttu-id="96935-123">연속 대시("--")를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="96935-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="96935-124">구독 선택</span><span class="sxs-lookup"><span data-stu-id="96935-124">Select a subscription</span></span>
<span data-ttu-id="96935-125">둘 이상의 구독이 있는 경우 데이터 또는 파일 저장소 서비스도 있는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="96935-126">Azure 검색 수 자동 검색 Azure 테이블 및 Blob 저장소, SQL 데이터베이스 및 Azure Cosmos DB를 통해 인덱싱을 *인덱서*, hello에 대 한 서비스에 대해서만 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in hello same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="96935-127">리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="96935-127">Select a resource group</span></span>
<span data-ttu-id="96935-128">리소스 그룹은 함께 사용된 Azure 서비스 및 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="96935-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="96935-129">예를 들어 Azure 검색 tooindex SQL 데이터베이스를 사용 하는 경우 다음 두 서비스의 일부 여야 hello 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="96935-129">For example, if you are using Azure Search tooindex a SQL database, then both services should be part of hello same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="96935-130">리소스 그룹을 삭제 하면 그 안에 hello 서비스도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96935-130">Deleting a resource group also deletes hello services within it.</span></span> <span data-ttu-id="96935-131">여러 서비스를 사용 하 여, 모든 hello에 넣는 프로토타입 프로젝트에 대 한 동일한 리소스 그룹 더 쉽게 정리 hello 프로젝트 끝난 후 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-131">For prototype projects utilizing multiple services, putting all of them in hello same resource group makes cleanup easier after hello project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="96935-132">호스팅 위치 선택</span><span class="sxs-lookup"><span data-stu-id="96935-132">Select a hosting location</span></span> 
<span data-ttu-id="96935-133">Azure 서비스로 hello 전 세계 데이터 센터에서 Azure 검색을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-133">As an Azure service, Azure Search can be hosted in datacenters around hello world.</span></span> <span data-ttu-id="96935-134">지역별로 [가격이 다를 수](https://azure.microsoft.com/pricing/details/search/) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="96935-135">가격 책정 계층(SKU) 선택</span><span class="sxs-lookup"><span data-stu-id="96935-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="96935-136">[Azure 검색은 무료, 기본 또는 표준 등 여러 가지 가격 책정 계층에서 현재 제공됩니다](https://azure.microsoft.com/pricing/details/search/).</span><span class="sxs-lookup"><span data-stu-id="96935-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="96935-137">각 계층에는 자체 [용량 및 제한](search-limits-quotas-capacity.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="96935-138">지침은 [가격 책정 계층 또는 SKU 선택](search-sku-tier.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96935-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="96935-139">이 연습에서는 서비스에 대 한 hello 표준 계층을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-139">In this walkthrough, we have chosen hello Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="96935-140">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="96935-140">Create your service</span></span>

<span data-ttu-id="96935-141">에 로그인 할 때마다 toopin 쉬운 액세스를 위해 서비스 toohello 대시보드를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-141">Remember toopin your service toohello dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="96935-142">서비스 확장</span><span class="sxs-lookup"><span data-stu-id="96935-142">Scale your service</span></span>
<span data-ttu-id="96935-143">몇 분 toocreate (15 분 이상 hello 계층에 따라) 서비스를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-143">It can take a few minutes toocreate a service (15 minutes or more depending on hello tier).</span></span> <span data-ttu-id="96935-144">서비스 프로 비전 되 면 있습니다 크기를 조정할 수 toomeet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-144">After your service is provisioned, you can scale it toomeet your needs.</span></span> <span data-ttu-id="96935-145">Azure 검색 서비스에 대 한 hello 표준 계층을 선택 했기 때문에 두 가지 차원에서 서비스를 확장할 수 있습니다: 복제본과 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-145">Because you chose hello Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="96935-146">Hello 기본 계층을 선택 했다면 있습니다, 복제본만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-146">Had you chosen hello Basic tier, you can only add replicas.</span></span> <span data-ttu-id="96935-147">Hello 무료 서비스를 프로 비전 하는 경우 배율 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="96935-147">If you provisioned hello free service, scale is not available.</span></span>

<span data-ttu-id="96935-148">***파티션*** 서비스 toostore 및 더 많은 문서를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-148">***Partitions*** allow your service toostore and search through more documents.</span></span>

<span data-ttu-id="96935-149">***복제본*** 서비스 toohandle 검색 쿼리의 더 높은 부하를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-149">***Replicas*** allow your service toohandle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="96935-150">서비스는 [SLA 읽기 전용으로 2개의 복제본과 SLA 읽기/쓰기용으로 3개의 복제본](https://azure.microsoft.com/support/legal/sla/search/v1_0/)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="96935-151">Hello Azure 포털에서에서 tooyour 검색 서비스 블레이드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-151">Go tooyour search service blade in hello Azure portal.</span></span>
2. <span data-ttu-id="96935-152">Hello 왼쪽 탐색 창에서 선택 **설정** > **배율**합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-152">In hello left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="96935-153">Hello slidebar tooadd 복제본 또는 파티션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-153">Use hello slidebar tooadd Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="96935-154">각 계층 마다 서로 다른 [제한](search-limits-quotas-capacity.md) hello 단일 서비스에서 허용 하는 검색 단위의 총 수 (복제본 * 파티션을 총 검색 단위 =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-154">Each tier has different [limits](search-limits-quotas-capacity.md) on hello total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-tooadd-a-second-service"></a><span data-ttu-id="96935-155">때 tooadd 두 번째 서비스</span><span class="sxs-lookup"><span data-stu-id="96935-155">When tooadd a second service</span></span>

<span data-ttu-id="96935-156">Hello를 제공 하는 계층에서 프로 비전 한 서비스를 사용 하는 대부분 고객의 [리소스의 균형을 마우스 오른쪽 단추로](search-sku-tier.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-156">A large majority of customers use just one service provisioned at a tier that provides hello [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="96935-157">여러 색인, 제목 toohello 하나의 서비스 호스팅할 수 있습니다 [선택한 hello 계층의 최대 제한](search-capacity-planning.md), 된 각 인덱스를 서로 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-157">One service can host multiple indexes, subject toohello [maximum limits of hello tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="96935-158">Azure 검색 요청 tooone 방향이 지정 된 인덱스 수, 다른에서 실수로 또는 의도적으로 데이터를 검색할 hello 가능성이 최소화 인덱스 hello에 동일한 수 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="96935-158">In Azure Search, requests can only be directed tooone index, minimizing hello chance of accidental or intentional data retrieval from other indexes in hello same service.</span></span>

<span data-ttu-id="96935-159">대부분의 고객이 한 서비스를 사용 하지만 서비스 중복성 운영 요구 사항을 hello 다음을 포함 하는 경우 필요한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include hello following:</span></span>

+ <span data-ttu-id="96935-160">재해 복구(데이터 센터 작동 중단).</span><span class="sxs-lookup"><span data-stu-id="96935-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="96935-161">Azure 검색에 즉각적인 장애 조치가 가동 중단의 hello 이벤트에서 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-161">Azure Search does not provide instant failover in hello event of an outage.</span></span> <span data-ttu-id="96935-162">권장 사항 및 지침에 대해서는 [서비스 관리](search-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96935-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="96935-163">다중 테 넌 트 모델링 조사 추가 서비스는 hello 최적의 디자인 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-163">Your investigation of multi-tenancy modeling has determined that additional services is hello optimal design.</span></span> <span data-ttu-id="96935-164">자세한 내용은 [다중 테넌트 디자인](search-modeling-multitenant-saas-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96935-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="96935-165">전체적으로 배포 된 응용 프로그램에 대 한 Azure 검색의 인스턴스를 응용 프로그램의 국제 트래픽의 여러 영역 toominimize 대기 시간에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions toominimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="96935-166">Azure Search에서는 인덱싱 및 쿼리 작업을 분리할 수 없습니다. 따라서 분리 된 작업에 대해 여러 서비스를 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="96935-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="96935-167">인덱스는 항상 쿼리할 hello 서비스에는 자신이 만든 (하면 하나의 서비스에는 인덱스를 만들 없으며 tooanother 복사).</span><span class="sxs-lookup"><span data-stu-id="96935-167">An index is always queried on hello service in which it was created (you cannot create an index in one service and copy it tooanother).</span></span>
>

<span data-ttu-id="96935-168">고가용성을 위해 두 번째 서비스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-168">A second service is not required for high availability.</span></span> <span data-ttu-id="96935-169">2를 사용 하거나 이상의 복제본에 동일한 서비스 hello 쿼리에 대 한 가용성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-169">High availability for queries is achieved when you use 2 or more replicas in hello same service.</span></span> <span data-ttu-id="96935-170">복제본 업데이트는 순차적입니다. 즉, 서비스 업데이트가 롤아웃될 때도 적어도 하나의 서비스는 작동됩니다. 가동 시간에 대한 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/search/v1_0/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96935-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96935-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="96935-171">Next steps</span></span>
<span data-ttu-id="96935-172">Azure 검색 서비스에서 프로 비전 후 준비가 너무[인덱스 정의](search-what-is-an-index.md) 업로드 하 고 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96935-172">After provisioning an Azure Search service, you are ready too[define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="96935-173">hello URL을 제공 하는 코드 또는 스크립트에서 tooaccess hello 서비스 (*서비스 이름*.으로 끝나므로)와 키입니다.</span><span class="sxs-lookup"><span data-stu-id="96935-173">tooaccess hello service from code or script, provide hello URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="96935-174">관리 키는 모든 액세스 권한을 부여하고, 쿼리 키는 읽기 전용 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-174">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="96935-175">참조 [toouse Azure 검색.NET 방법](search-howto-dotnet-sdk.md) tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="96935-175">See [How toouse Azure Search in .NET](search-howto-dotnet-sdk.md) tooget started.</span></span>

<span data-ttu-id="96935-176">빠른 포털 기반 자습서는 [첫 번째 인덱스 빌드 및 쿼리](search-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96935-176">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

