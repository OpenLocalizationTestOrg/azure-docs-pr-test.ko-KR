---
title: "aaaAzure 구독 제한 및 할당량 | Microsoft Docs"
description: "일반적인 Azure 구독 및 서비스 제한, 할당량 및 제약 조건 목록을 제공합니다. 최대 값과 함께 tooincrease 제한 하는 방법에 대 한 정보가 포함 됩니다."
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
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="df00c-104">Azure 구독 및 서비스 제한, 할당량 및 제약 조건</span><span class="sxs-lookup"><span data-stu-id="df00c-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="df00c-105">이 문서 라고도 할당량 hello 가장 일반적인 Microsoft Azure 제한을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="df00c-106">현재 이 문서에서는 일부 Azure 서비스에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="df00c-107">시간이 지남에 따라 hello 목록 확장 될 것이 고 hello 플랫폼의 자세한 toocover를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="df00c-108">방문 하세요 [Azure 가격 책정 개요](https://azure.microsoft.com/pricing/) toolearn Azure 가격에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="df00c-109">Hello를 사용 하 여 비용을 예측할 수, [가격 계산기](https://azure.microsoft.com/pricing/calculator/) 또는 hello 가격 책정 서비스에 대 한 세부 정보 페이지를 방문 하 여 (예를 들어 [Windows Vm](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="df00c-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="df00c-110">팁 toohelp에 대 한 비용을 관리, 참조 [Azure 청구 및 비용 관리를 사용 하 여 예기치 않은 비용을 방지](billing/billing-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="df00c-111">Tooraise hello 제한 또는 hello 위에 할당량 원하면 **기본 제한**, [비용 없이 온라인 고객 지원 요청을 개시](azure-supportability/resource-manager-core-quotas-request.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="df00c-112">hello 제한 수준을 올릴 수 없습니다 hello 위에 **최대 한도** 다음 표에서 hello에 표시 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="df00c-113">없는 경우 없는 **최대 한도** 열에서 다음 hello 리소스 제한을 조정할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="df00c-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="df00c-114">무료 평가판 구독을 제한하거나 할당량을 증가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="df00c-115">무료 평가판을 설정한 경우 업그레이드할 수 tooa [종 량 제](https://azure.microsoft.com/offers/ms-azr-0003p/) 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="df00c-116">자세한 내용은 참조 [Azure 무료 평가판 업그레이드 tooPay-으로--제](billing/billing-upgrade-azure-subscription.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="df00c-117">제한 및 hello Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="df00c-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="df00c-118">가능한 toocombine은 이제 여러 Azure 리소스 tooa에서 단일 Azure 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="df00c-119">리소스 그룹을 사용할 때 전역 졌 제한 될 hello Azure 리소스 관리자가 있는 지역 수준에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="df00c-120">Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df00c-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="df00c-121">새 테이블 아래의 hello 제한 되었습니다 추가 tooreflect 제한에서 모든 차이점 hello Azure 리소스 관리자를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="df00c-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="df00c-122">예를 들어, **구독 제한** 테이블 및 **구독 제한 - Azure Resource Manager** 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="df00c-123">제한 tooboth 시나리오에 적용 되 hello 첫 번째 테이블에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="df00c-124">별도로 지정하지 않으면 제한은 모든 지역에 걸쳐 전역으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="df00c-125">Hello 서비스 관리 할당량은 Azure 리소스 그룹의 리소스에 대 한 할당량 지역 구독에 액세스할 수 있으며이 아닌 구독 당 중요 tooemphasize 상태가.</span><span class="sxs-lookup"><span data-stu-id="df00c-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="df00c-126">코어 할당량을 한 예로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="df00c-127">Toodecide 어떻게 필요한 toorequest 코어를 지 원하는 할당량 증가 해야 할 경우 어떤 지역에서 toouse을 다음 Azure 리소스 그룹에 대 한 특정 요청을 확인 하는 많은 코어 할당량을 hello 금액 및 원하는 지역에 대 한 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="df00c-128">따라서 toouse 30 해야 할 경우 코어가 서 부 유럽 toorun에서 응용 프로그램에 있습니다. 특히 서 부 유럽에서 30 개 코어를 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="df00c-129">하지만 다른 지역에 코어 할당량 없을 것-hello 30 코어 할당량을 갖는 서 부 유럽만 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="df00c-130">결과적으로, Azure 리소스 그룹 할당량 필요한 toobe 금액을 고려 하 고 배포 하는 각 지역에는 하나의 영역 및 요청 작업에 대 한 결정 하는 유용한 tooconsider 것 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="df00c-131">특정 지역의 현재 할당량 검색에 대한 자세한 내용은 [배포 문제 해결](resource-manager-common-deployment-errors.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df00c-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="df00c-132">서비스 특정 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-132">Service-specific limits</span></span>
* [<span data-ttu-id="df00c-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="df00c-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="df00c-134">API 관리</span><span class="sxs-lookup"><span data-stu-id="df00c-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="df00c-135">앱 서비스</span><span class="sxs-lookup"><span data-stu-id="df00c-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="df00c-136">응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="df00c-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="df00c-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="df00c-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="df00c-138">자동화</span><span class="sxs-lookup"><span data-stu-id="df00c-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="df00c-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="df00c-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="df00c-140">Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="df00c-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="df00c-141">Azure Redis 캐시(영문)</span><span class="sxs-lookup"><span data-stu-id="df00c-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="df00c-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="df00c-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="df00c-143">백업</span><span class="sxs-lookup"><span data-stu-id="df00c-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="df00c-144">배치</span><span class="sxs-lookup"><span data-stu-id="df00c-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="df00c-145">BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="df00c-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="df00c-146">CDN</span><span class="sxs-lookup"><span data-stu-id="df00c-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="df00c-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="df00c-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="df00c-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="df00c-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="df00c-149">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="df00c-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="df00c-150">데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="df00c-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="df00c-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="df00c-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="df00c-152">DNS</span><span class="sxs-lookup"><span data-stu-id="df00c-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="df00c-153">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="df00c-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="df00c-154">IoT 허브</span><span class="sxs-lookup"><span data-stu-id="df00c-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="df00c-155">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="df00c-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="df00c-156">Log Analytics/Operational Insights</span><span class="sxs-lookup"><span data-stu-id="df00c-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="df00c-157">미디어 서비스</span><span class="sxs-lookup"><span data-stu-id="df00c-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="df00c-158">모바일 고객 관리</span><span class="sxs-lookup"><span data-stu-id="df00c-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="df00c-159">모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="df00c-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="df00c-160">모니터</span><span class="sxs-lookup"><span data-stu-id="df00c-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="df00c-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="df00c-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="df00c-162">네트워킹</span><span class="sxs-lookup"><span data-stu-id="df00c-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="df00c-163">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="df00c-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="df00c-164">알림 허브 서비스</span><span class="sxs-lookup"><span data-stu-id="df00c-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="df00c-165">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="df00c-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="df00c-166">스케줄러</span><span class="sxs-lookup"><span data-stu-id="df00c-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="df00c-167">이를 통해 검색</span><span class="sxs-lookup"><span data-stu-id="df00c-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="df00c-168">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="df00c-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="df00c-169">사이트 복구</span><span class="sxs-lookup"><span data-stu-id="df00c-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="df00c-170">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="df00c-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="df00c-171">저장소</span><span class="sxs-lookup"><span data-stu-id="df00c-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="df00c-172">StorSimple 시스템</span><span class="sxs-lookup"><span data-stu-id="df00c-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="df00c-173">스트림 분석</span><span class="sxs-lookup"><span data-stu-id="df00c-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="df00c-174">구독</span><span class="sxs-lookup"><span data-stu-id="df00c-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="df00c-175">트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="df00c-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="df00c-176">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="df00c-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="df00c-177">가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="df00c-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="df00c-178">구독 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="df00c-179">구독 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="df00c-180">구독 제한 - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="df00c-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="df00c-181">다음 제한 hello hello Azure 리소스 관리자 및 Azure 리소스 그룹을 사용할 때 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="df00c-182">Azure 리소스 관리자 hello로 변경 되지 않은 제한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="df00c-183">이러한 제한에 대 한 toohello 이전 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df00c-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="df00c-184">리소스 관리자 요청의 제한 처리에 대한 정보는 [리소스 관리자 요청 제한](resource-manager-request-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df00c-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="df00c-185">리소스 그룹 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="df00c-186">가상 컴퓨터 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="df00c-187">가상 컴퓨터 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="df00c-188">가상 컴퓨터 제한 - Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="df00c-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="df00c-189">다음 제한 hello hello Azure 리소스 관리자 및 Azure 리소스 그룹을 사용할 때 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="df00c-190">Azure 리소스 관리자 hello로 변경 되지 않은 제한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="df00c-191">이러한 제한에 대 한 toohello 이전 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df00c-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="df00c-192">가상 컴퓨터 크기 집합 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="df00c-193">Container Instances 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="df00c-194">네트워킹 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="df00c-195">네트워킹 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="df00c-196">Application Gateway 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="df00c-197">Network Watcher 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="df00c-198">트래픽 관리자 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="df00c-199">DNS 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="df00c-200">저장소 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-200">Storage limits</span></span>
<span data-ttu-id="df00c-201">저장소 계정 제한에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage/common/storage-scalability-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df00c-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="df00c-202">저장소 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="df00c-203">가상 컴퓨터 디스크 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="df00c-204">자세한 내용은 [가상 컴퓨터 크기](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df00c-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="df00c-205">관리되는 가상 컴퓨터 디스크</span><span class="sxs-lookup"><span data-stu-id="df00c-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="df00c-206">관리되지 않는 가상 컴퓨터 디스크</span><span class="sxs-lookup"><span data-stu-id="df00c-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="df00c-207">저장소 리소스 공급자 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="df00c-208">클라우드 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="df00c-209">앱 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-209">App Service limits</span></span>
<span data-ttu-id="df00c-210">앱 서비스 제한 hello 다음 웹 앱, 모바일 앱, API 앱 및 논리 앱에 대 한 제한을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="df00c-211">스케줄러 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="df00c-212">배치 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="df00c-213">BizTalk 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-213">BizTalk Services limits</span></span>
<span data-ttu-id="df00c-214">hello 다음 표에 hello 제한을 Azure Biztalk 서비스에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="df00c-215">Azure Cosmos DB 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="df00c-216">Azure Cosmos DB에는 처리량 및 저장소 수 크기 조정 된 toohandle 응용 프로그램에 필요한 대로 지정 세계적인 규모 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="df00c-217">Azure Cosmos DB에는 hello 눈금에 대 한 질문이 있으면 전자 메일을 보내 주십시오 tooaskcosmosdb@microsoft.com합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="df00c-218">모바일 참여 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="df00c-219">검색 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-219">Search limits</span></span>
<span data-ttu-id="df00c-220">가격 책정 hello 용량 및 검색 서비스의 한계를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="df00c-221">계층은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-221">Tiers include:</span></span>

* <span data-ttu-id="df00c-222">*무료* 다중 테넌트 서비스는 다른 Azure 구독자와 공유되며 평가 및 소규모 개발 프로젝트용으로 사용하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="df00c-223">*기본* 를 항상 사용 가능한 쿼리 워크 로드에 대 한 toothree 복제본에 더 작은 규모로 프로덕션 작업에 대 한 전용된 컴퓨팅 리소스 제공.</span><span class="sxs-lookup"><span data-stu-id="df00c-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="df00c-224">*표준(S1, S2, S3, S3 고밀도)* 은 더 큰 프로덕션 작업용입니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="df00c-225">여러 수준 작업 부하 프로필에 가장 적합 한 리소스 구성을 선택할 수 있도록 hello 표준 계층 내에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="df00c-226">**구독당 제한**</span><span class="sxs-lookup"><span data-stu-id="df00c-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="df00c-227">**검색 서비스당 제한**</span><span class="sxs-lookup"><span data-stu-id="df00c-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="df00c-228">문서 크기, 초, 키, 요청 및 응답을 당 쿼리 등의 보다 세부적인 수준에 대 한 제한에 대해 자세히 toolearn 참조 [서비스에서 Azure 검색의 제한](search/search-limits-quotas-capacity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df00c-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="df00c-229">미디어 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="df00c-230">CDN 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="df00c-231">모바일 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="df00c-232">모니터 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="df00c-233">알림 허브 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="df00c-234">이벤트 허브 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="df00c-235">서비스 버스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="df00c-236">IoT Hub 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="df00c-237">데이터 팩터리 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="df00c-238">Data Lake Analytics 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="df00c-239">Data Lake Store 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="df00c-240">스트림 분석 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="df00c-241">Active Directory 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="df00c-242">Azure Event Grid 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="df00c-243">Azure RemoteApp 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="df00c-244">StorSimple 시스템 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="df00c-245">Log Analytics 한도</span><span class="sxs-lookup"><span data-stu-id="df00c-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="df00c-246">백업 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="df00c-247">사이트 복구 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="df00c-248">Application Insights 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="df00c-249">API 관리 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="df00c-250">Azure Redis 캐시 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="df00c-251">키 값 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="df00c-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="df00c-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="df00c-253">자동화 한도</span><span class="sxs-lookup"><span data-stu-id="df00c-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="df00c-254">SQL 데이터베이스 제한</span><span class="sxs-lookup"><span data-stu-id="df00c-254">SQL Database limits</span></span>
<span data-ttu-id="df00c-255">SQL 데이터베이스 제한은 [SQL 데이터베이스 리소스 제한](sql-database/sql-database-resource-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df00c-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="df00c-256">참고 항목</span><span class="sxs-lookup"><span data-stu-id="df00c-256">See also</span></span>
[<span data-ttu-id="df00c-257">Azure 제한 및 증가 이해</span><span class="sxs-lookup"><span data-stu-id="df00c-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="df00c-258">Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기</span><span class="sxs-lookup"><span data-stu-id="df00c-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="df00c-259">클라우드 서비스 크기</span><span class="sxs-lookup"><span data-stu-id="df00c-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

