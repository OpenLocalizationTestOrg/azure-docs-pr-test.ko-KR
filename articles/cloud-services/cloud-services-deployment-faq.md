---
title: "Microsoft Azure Cloud Services FAQ에 대한 배포 문제 | Microsoft Docs"
description: "이 문서는 Microsoft Azure Cloud Services의 배포에 대한 질문과 대답을 나열합니다."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cb62cd4c4635d9e837dff81a9c4543781dd11adb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="2315b-103">Azure Cloud Services의 배포 문제: FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="2315b-103">Deployment issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="2315b-104">이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 배포 문제에 대한 질문과 대답을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-104">This article includes frequently asked questions about deployment issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="2315b-105">크기 정보는 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-to-the-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-the-production-slot"></a><span data-ttu-id="2315b-106">프로덕션 슬롯에 기존 배포가 있는 경우 스테이징 슬롯에 대한 클라우드 서비스 배포가 리소스 할당 오류로 인해 실패하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2315b-106">Why does deploying a cloud service to the staging slot sometimes fail with a resource allocation error if there is already an existing deployment in the production slot?</span></span>
<span data-ttu-id="2315b-107">클라우드 서비스가 두 슬롯 중 하나에 배포된 경우 전체 클라우드 서비스가 특정 클러스터에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-107">If a cloud service has a deployment in either slot, the entire cloud service is pinned to a specific cluster.</span></span> <span data-ttu-id="2315b-108">이는 프로덕션 슬롯에 이미 배포가 있을 경우 프로덕션 슬롯과 동일한 클러스터에만 새 스테이징 배포를 할당할 수 있다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-108">This means that if a deployment already exists in the production slot, a new staging deployment can only be allocated in the same cluster as the production slot.</span></span>

<span data-ttu-id="2315b-109">클라우드 서비스가 있는 클러스터가 배포 요청을 충족하기에 충분한 물리적 계산 리소스 없는 경우 할당 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-109">Allocation failures occur when the cluster where your cloud service is located does not have enough physical compute resources to satisfy your deployment request.</span></span>

<span data-ttu-id="2315b-110">이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-110">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a><span data-ttu-id="2315b-111">클라우드 서비스 배포를 스케일 업 또는 스케일 아웃하는 경우 할당 오류가 발생하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2315b-111">Why does scaling up or scaling out a cloud service deployment sometimes result in allocation failure?</span></span>
<span data-ttu-id="2315b-112">클라우드 서비스를 배포할 때 일반적으로 특정 클러스터에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-112">When a cloud service is deployed, it usually gets pinned to a specific cluster.</span></span> <span data-ttu-id="2315b-113">즉, 기존 클라우드 서비스를 스케일 업/아웃하면 동일한 클러스터에 새 인스턴스를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-113">This means scaling up/out an existing cloud service must allocate new instances in the same cluster.</span></span> <span data-ttu-id="2315b-114">클러스터가 수용작업량에 가까워지거나 원하는 VM 크기/형식을 사용할 수 없는 경우 요청이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-114">If the cluster is nearing capacity or the desired VM size/type is not available, the request may fail.</span></span>

<span data-ttu-id="2315b-115">이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-115">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a><span data-ttu-id="2315b-116">선호도 그룹에 클라우드 서비스를 배포하는 경우 할당 오류가 발생하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2315b-116">Why does deploying a cloud service into an affinity group sometimes result in allocation failure?</span></span>
<span data-ttu-id="2315b-117">클라우드 서비스가 선호도 그룹에 고정되어 있지 않는 한, 빈 클라우드 서비스에 새로 배포할 경우 해당 영역에 있는 클러스터의 패브릭에 의해서만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-117">A new deployment to an empty cloud service can be allocated by the fabric in any cluster in that region, unless the cloud service is pinned to an affinity group.</span></span> <span data-ttu-id="2315b-118">동일한 선호도 그룹에 대한 배포는 동일한 클러스터에서 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-118">Deployments to the same affinity group will be attempted on the same cluster.</span></span> <span data-ttu-id="2315b-119">클러스터의 용량이 거의 찼을 경우 요청이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-119">If the cluster is nearing capacity, the request may fail.</span></span>

<span data-ttu-id="2315b-120">이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-120">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-to-an-existing-cloud-service-sometimes-result-in-allocation-failure"></a><span data-ttu-id="2315b-121">VM 크기를 변경하거나 기존 클라우드 서비스에 새 VM을 추가하면 할당 오류가 발생하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2315b-121">Why does changing VM size or adding a new VM to an existing cloud service sometimes result in allocation failure?</span></span>
<span data-ttu-id="2315b-122">데이터 센터의 클러스터에는 다양한 컴퓨터 종류의 구성이 있습니다(예: A 시리즈, Av2 시리즈, D 시리즈, Dv2 시리즈, G 시리즈, H 시리즈 등).</span><span class="sxs-lookup"><span data-stu-id="2315b-122">The clusters in a datacenter may have different configurations of machine types (e.g., A series, Av2 series, D series, Dv2 series, G series, H series, etc.).</span></span> <span data-ttu-id="2315b-123">하지만 클러스터에는 일부 종류의 VM만이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-123">But not all the clusters would necessarily have all the kinds of VMs.</span></span> <span data-ttu-id="2315b-124">예를 들어 A 시리즈 전용 클러스터에 이미 배포된 클라우드 서비스에 D 시리즈 VM을 추가하려는 경우 할당 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-124">For example, if you try to add a D series VM to a cloud service that is already deployed in an A series-only cluster, you will experience an allocation failure.</span></span> <span data-ttu-id="2315b-125">또한 VM SKU의 크기를 변경하려는 경우에 발생합니다(예: A 시리즈에서 D 시리즈로 전환).</span><span class="sxs-lookup"><span data-stu-id="2315b-125">This will also happen if you try to change VM SKU sizes (for example, switching from an A series to a D series).</span></span>

<span data-ttu-id="2315b-126">이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-126">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

<span data-ttu-id="2315b-127">사용자 지역에서 사용할 수 있는 크기를 확인하려면 [Microsoft Azure: 지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-127">To check the sizes available in your region, see [Microsoft Azure: Products available by region](https://azure.microsoft.com/regions/services).</span></span>

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-to-limitsquotasconstraints-on-my-subscription-or-service"></a><span data-ttu-id="2315b-128">구독 또는 서비스에서 제한/할당량/제한 조건으로 인해 클라우드 서비스를 배포하는 데 실패하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2315b-128">Why does deploying a cloud service sometime fail due to limits/quotas/constraints on my subscription or service?</span></span>
<span data-ttu-id="2315b-129">할당하는 데 필요한 리소스가 지역/데이터 센터 수준에서 서비스에 허용되는 기본 또는 최대 할당량을 초과하는 경우 클라우드 서비스의 배포에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-129">Deployment of a cloud service may fail if the resources that are required to be allocated exceed the default or maximum quota allowed for your service at the region/datacenter level.</span></span> <span data-ttu-id="2315b-130">자세한 내용은 [Cloud Services 제한](../azure-subscription-service-limits.md#cloud-services-limits)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-130">For more information, see [Cloud Services limits](../azure-subscription-service-limits.md#cloud-services-limits).</span></span>

<span data-ttu-id="2315b-131">포털에서 구독에 대한 현재 사용량/할당량도 추적할 수 있습니다. Azure Portal =>구독=>\<적절한 구독=>"사용량 + 할당량"</span><span class="sxs-lookup"><span data-stu-id="2315b-131">You could also track the current usage/quota for your subscription at the portal: Azure Portal => Subscriptions => \<appropriate subscription> => “Usage + quota”.</span></span>

<span data-ttu-id="2315b-132">Azure 청구 API를 통해 리소스 사용/사용 관련 정보를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-132">Resource usage/consumption-related information can also be retrieved via the Azure Billing APIs.</span></span> <span data-ttu-id="2315b-133">[Azure 리소스 사용량 API(미리 보기)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-133">See [Azure Resource Usage API (Preview)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).</span></span>

## <a name="how-can-i-change-the-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a><span data-ttu-id="2315b-134">배포된 클라우드 서비스 VM을 다시 배포하지 않고 크기를 변경하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="2315b-134">How can I change the size of a deployed cloud service VM without redeploying it?</span></span>
<span data-ttu-id="2315b-135">배포된 클라우드 서비스 VM을 다시 배포하지 않고 크기를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-135">You cannot change the VM size of a deployed cloud service without redeploying it.</span></span> <span data-ttu-id="2315b-136">VM 크기는 CSDEF에 포함되며 재배포로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2315b-136">The VM size is built into the CSDEF, which can only be updated with a redeploy.</span></span>

<span data-ttu-id="2315b-137">자세한 내용은 [클라우드 서비스를 업데이트하는 방법](cloud-services-update-azure-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2315b-137">For more information, see [How to update a cloud service](cloud-services-update-azure-service.md).</span></span>

 
