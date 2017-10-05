---
title: "Azure 구독 제한 및 할당량 | Microsoft Docs"
description: "일반적인 Azure 구독 및 서비스 제한, 할당량 및 제약 조건 목록을 제공합니다. 여기에는 최대값과 함께 제한을 늘리는 방법에 대한 정보가 포함됩니다."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a76acd67e9ba7822f2837b3c08e2ede389047f11
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="395f1-104">Azure 구독 및 서비스 제한, 할당량 및 제약 조건</span><span class="sxs-lookup"><span data-stu-id="395f1-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="395f1-105">이 문서는 때때로 할당량이라고도 하는 가장 일반적인 Microsoft Azure 제한의 일부를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="395f1-106">현재 이 문서에서는 일부 Azure 서비스에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="395f1-107">시간 경과에 따라 이 목록은 더 많은 플랫폼에 적용되도록 확장 및 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-107">Over time, the list will be expanded and updated to cover more of the platform.</span></span>

<span data-ttu-id="395f1-108">Azure 가격에 대한 자세한 정보는 [Azure 가격 책정 개요](https://azure.microsoft.com/pricing/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span></span> <span data-ttu-id="395f1-109">여기에서 [가격 계산기](https://azure.microsoft.com/pricing/calculator/)를 사용하거나 서비스에 대한 가격 정보 페이지를 방문하여 비용을 예측할 수 있습니다(예: [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="395f1-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="395f1-110">비용 관리에 대한 팁은 [Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지](billing/billing-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="395f1-111">**기본 제한**이상으로 제한 또는 할당량을 높이려는 경우 [무료로 온라인 고객 지원 요청을 개설](azure-supportability/resource-manager-core-quotas-request.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="395f1-112">다음 표에 나오는 **최대 제한** 값 이상으로 제한을 높일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span></span> <span data-ttu-id="395f1-113">**최대 제한** 열이 없는 경우는 리소스에 조정 가능한 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="395f1-114">무료 평가판 구독을 제한하거나 할당량을 증가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="395f1-115">무료 평가판을 사용하는 경우 [종량제](https://azure.microsoft.com/offers/ms-azr-0003p/) 구독으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="395f1-116">자세한 내용은 [Azure 무료 평가판에서 종량제로 업그레이드](billing/billing-upgrade-azure-subscription.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-the-azure-resource-manager"></a><span data-ttu-id="395f1-117">제한 및 Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="395f1-117">Limits and the Azure Resource Manager</span></span>
<span data-ttu-id="395f1-118">이제 단일 Azure 리소스 그룹에 여러 Azure 리소스를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span></span> <span data-ttu-id="395f1-119">리소스 그룹을 사용하는 경우 전역이었던 제한이 Azure 리소스 관리자에서 지역 수준으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span></span> <span data-ttu-id="395f1-120">Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="395f1-121">아래 제한에서는 Azure 리소스 관리자를 사용할 때 제한에 차이를 반영할 수 있도록 새로운 테이블이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span></span> <span data-ttu-id="395f1-122">예를 들어, **구독 제한** 테이블 및 **구독 제한 - Azure Resource Manager** 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="395f1-123">두 시나리오에 모두 제한이 적용되면 첫 번째 테이블에서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-123">When a limit applies to both scenarios, it is only shown in the first table.</span></span> <span data-ttu-id="395f1-124">별도로 지정하지 않으면 제한은 모든 지역에 걸쳐 전역으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="395f1-125">Azure 리소스 그룹의 리소스에 대한 할당량은 구독을 통해 지역별로 액세스할 수 있으며, 구독별로는 액세스할 수 없는데 서비스 관리 할당량이 구독별로 액세스되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span></span> <span data-ttu-id="395f1-126">코어 할당량을 한 예로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="395f1-127">코어를 지원하는 할당량 증가를 요청해야 하는 경우 어떤 지역에서 얼마나 많은 코어를 사용할 것인지 결정한 다음, 원하는 금액 및 지역에 대한 Azure 리소스 그룹 코어 할당량에 대해 특정 요청을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span></span> <span data-ttu-id="395f1-128">따라서 서유럽 지역에서 응용 프로그램을 실행하려면 30개의 코어를 사용해야 하는 경우, 확실하게 서유럽에서 30개의 코어를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="395f1-129">하지만 다른 지역에는 코어 할당량 증가가 없고 서유럽만 30개의 코어 할당량이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="395f1-130">따라서 어떤 한 지역에서 워크로드에 필요한 Azure 리소스 그룹 할당량을 결정하고 배포를 고려 중인 각 지역에서 해당 금액을 요청하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-130">As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="395f1-131">특정 지역의 현재 할당량 검색에 대한 자세한 내용은 [배포 문제 해결](resource-manager-common-deployment-errors.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="395f1-132">서비스 특정 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-132">Service-specific limits</span></span>
* [<span data-ttu-id="395f1-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="395f1-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="395f1-134">API 관리</span><span class="sxs-lookup"><span data-stu-id="395f1-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="395f1-135">앱 서비스</span><span class="sxs-lookup"><span data-stu-id="395f1-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="395f1-136">응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="395f1-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="395f1-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="395f1-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="395f1-138">자동화</span><span class="sxs-lookup"><span data-stu-id="395f1-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="395f1-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="395f1-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="395f1-140">Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="395f1-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="395f1-141">Azure Redis 캐시(영문)</span><span class="sxs-lookup"><span data-stu-id="395f1-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="395f1-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="395f1-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="395f1-143">백업</span><span class="sxs-lookup"><span data-stu-id="395f1-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="395f1-144">배치</span><span class="sxs-lookup"><span data-stu-id="395f1-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="395f1-145">BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="395f1-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="395f1-146">CDN</span><span class="sxs-lookup"><span data-stu-id="395f1-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="395f1-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="395f1-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="395f1-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="395f1-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="395f1-149">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="395f1-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="395f1-150">데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="395f1-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="395f1-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="395f1-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="395f1-152">DNS</span><span class="sxs-lookup"><span data-stu-id="395f1-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="395f1-153">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="395f1-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="395f1-154">IoT 허브</span><span class="sxs-lookup"><span data-stu-id="395f1-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="395f1-155">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="395f1-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="395f1-156">Log Analytics/Operational Insights</span><span class="sxs-lookup"><span data-stu-id="395f1-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="395f1-157">미디어 서비스</span><span class="sxs-lookup"><span data-stu-id="395f1-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="395f1-158">모바일 고객 관리</span><span class="sxs-lookup"><span data-stu-id="395f1-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="395f1-159">모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="395f1-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="395f1-160">모니터</span><span class="sxs-lookup"><span data-stu-id="395f1-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="395f1-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="395f1-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="395f1-162">네트워킹</span><span class="sxs-lookup"><span data-stu-id="395f1-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="395f1-163">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="395f1-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="395f1-164">알림 허브 서비스</span><span class="sxs-lookup"><span data-stu-id="395f1-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="395f1-165">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="395f1-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="395f1-166">스케줄러</span><span class="sxs-lookup"><span data-stu-id="395f1-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="395f1-167">이를 통해 검색</span><span class="sxs-lookup"><span data-stu-id="395f1-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="395f1-168">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="395f1-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="395f1-169">사이트 복구</span><span class="sxs-lookup"><span data-stu-id="395f1-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="395f1-170">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="395f1-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="395f1-171">저장소</span><span class="sxs-lookup"><span data-stu-id="395f1-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="395f1-172">StorSimple 시스템</span><span class="sxs-lookup"><span data-stu-id="395f1-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="395f1-173">스트림 분석</span><span class="sxs-lookup"><span data-stu-id="395f1-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="395f1-174">구독</span><span class="sxs-lookup"><span data-stu-id="395f1-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="395f1-175">트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="395f1-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="395f1-176">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="395f1-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="395f1-177">가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="395f1-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="395f1-178">구독 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="395f1-179">구독 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="395f1-180">구독 제한 - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="395f1-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="395f1-181">Azure 리소스 관리자 및 Azure 리소스 그룹을 사용하는 경우 다음과 같은 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-181">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="395f1-182">Azure 리소스 관리자에서 변경되지 않는 제한은 아래에 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-182">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="395f1-183">이러한 제한에 대해서는 이전 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-183">Please refer to the previous table for those limits.</span></span>

<span data-ttu-id="395f1-184">리소스 관리자 요청의 제한 처리에 대한 정보는 [리소스 관리자 요청 제한](resource-manager-request-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="395f1-185">리소스 그룹 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="395f1-186">가상 컴퓨터 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="395f1-187">가상 컴퓨터 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="395f1-188">가상 컴퓨터 제한 - Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="395f1-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="395f1-189">Azure 리소스 관리자 및 Azure 리소스 그룹을 사용하는 경우 다음과 같은 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-189">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="395f1-190">Azure 리소스 관리자에서 변경되지 않는 제한은 아래에 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-190">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="395f1-191">이러한 제한에 대해서는 이전 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-191">Please refer to the previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="395f1-192">가상 컴퓨터 크기 집합 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="395f1-193">Container Instances 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="395f1-194">네트워킹 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="395f1-195">네트워킹 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="395f1-196">Application Gateway 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="395f1-197">Network Watcher 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="395f1-198">트래픽 관리자 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="395f1-199">DNS 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="395f1-200">저장소 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-200">Storage limits</span></span>
<span data-ttu-id="395f1-201">저장소 계정 제한에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage/common/storage-scalability-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="395f1-202">저장소 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="395f1-203">가상 컴퓨터 디스크 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="395f1-204">자세한 내용은 [가상 컴퓨터 크기](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="395f1-205">관리되는 가상 컴퓨터 디스크</span><span class="sxs-lookup"><span data-stu-id="395f1-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="395f1-206">관리되지 않는 가상 컴퓨터 디스크</span><span class="sxs-lookup"><span data-stu-id="395f1-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="395f1-207">저장소 리소스 공급자 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="395f1-208">클라우드 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="395f1-209">앱 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-209">App Service limits</span></span>
<span data-ttu-id="395f1-210">다음 앱 서비스 제한에는 웹앱, 모바일 앱, API 앱 및 논리 앱에 대한 제한이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-210">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="395f1-211">스케줄러 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="395f1-212">배치 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="395f1-213">BizTalk 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-213">BizTalk Services limits</span></span>
<span data-ttu-id="395f1-214">다음 표에서는 Azure Biztalk 서비스에 대한 제한을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-214">The following table shows the limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="395f1-215">Azure Cosmos DB 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="395f1-216">Azure Cosmos DB는 어떠한 응용 프로그램의 요구도 처리하도록 처리량과 저장소 크기를 조정할 수 있는 뛰어난 확장성의 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span></span> <span data-ttu-id="395f1-217">Azure Cosmos DB가 제공하는 규모에 대한 궁금한 사항은 askcosmosdb@microsoft.com에 메일을 보내 주세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-217">If you have any questions about the scale Azure Cosmos DB provides, please send email to askcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="395f1-218">모바일 참여 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="395f1-219">검색 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-219">Search limits</span></span>
<span data-ttu-id="395f1-220">가격 책정 계층은 검색 서비스의 용량 및 제한을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-220">Pricing tiers determine the capacity and limits of your search service.</span></span> <span data-ttu-id="395f1-221">계층은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-221">Tiers include:</span></span>

* <span data-ttu-id="395f1-222">*무료* 다중 테넌트 서비스는 다른 Azure 구독자와 공유되며 평가 및 소규모 개발 프로젝트용으로 사용하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="395f1-223">*기본* 은 높은 가용성의 쿼리 작업에 대한 최대 3개의 복제본과 함께 프로덕션 워크로드 전용 컴퓨팅 리소스를 더 작은 규모로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span></span>
* <span data-ttu-id="395f1-224">*표준(S1, S2, S3, S3 고밀도)* 은 더 큰 프로덕션 작업용입니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="395f1-225">표준 계층 내에는 여러 수준이 있으므로 워크로드 프로필에 가장 적합한 리소스 구성을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="395f1-225">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="395f1-226">**구독당 제한**</span><span class="sxs-lookup"><span data-stu-id="395f1-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="395f1-227">**검색 서비스당 제한**</span><span class="sxs-lookup"><span data-stu-id="395f1-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="395f1-228">문서 크기, 초당 쿼리, 키, 요청 및 응답을 비롯한 좀 더 자세한 수준의 제한 사항에 대한 자세한 내용은 [Azure Search의 서비스 제한 사항](search/search-limits-quotas-capacity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-228">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="395f1-229">미디어 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="395f1-230">CDN 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="395f1-231">모바일 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="395f1-232">모니터 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="395f1-233">알림 허브 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="395f1-234">이벤트 허브 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="395f1-235">서비스 버스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="395f1-236">IoT Hub 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="395f1-237">데이터 팩터리 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="395f1-238">Data Lake Analytics 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="395f1-239">Data Lake Store 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="395f1-240">스트림 분석 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="395f1-241">Active Directory 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="395f1-242">Azure Event Grid 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="395f1-243">Azure RemoteApp 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="395f1-244">StorSimple 시스템 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="395f1-245">Log Analytics 한도</span><span class="sxs-lookup"><span data-stu-id="395f1-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="395f1-246">백업 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="395f1-247">사이트 복구 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="395f1-248">Application Insights 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="395f1-249">API 관리 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="395f1-250">Azure Redis 캐시 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="395f1-251">키 값 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="395f1-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="395f1-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="395f1-253">자동화 한도</span><span class="sxs-lookup"><span data-stu-id="395f1-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="395f1-254">SQL 데이터베이스 제한</span><span class="sxs-lookup"><span data-stu-id="395f1-254">SQL Database limits</span></span>
<span data-ttu-id="395f1-255">SQL 데이터베이스 제한은 [SQL 데이터베이스 리소스 제한](sql-database/sql-database-resource-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="395f1-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="395f1-256">참고 항목</span><span class="sxs-lookup"><span data-stu-id="395f1-256">See also</span></span>
[<span data-ttu-id="395f1-257">Azure 제한 및 증가 이해</span><span class="sxs-lookup"><span data-stu-id="395f1-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="395f1-258">Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기</span><span class="sxs-lookup"><span data-stu-id="395f1-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="395f1-259">클라우드 서비스 크기</span><span class="sxs-lookup"><span data-stu-id="395f1-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

