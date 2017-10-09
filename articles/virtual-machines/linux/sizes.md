---
title: "Azure에서 aaaLinux VM의 크기를 조정 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터에 사용할 수 있는 hello 다른 크기를 나열합니다."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="5f28c-103">Azure에서 Linux 가상 컴퓨터에 대한 크기</span><span class="sxs-lookup"><span data-stu-id="5f28c-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="5f28c-104">이 문서는 hello 사용 가능한 크기에 설명 하 고 Azure 가상 컴퓨터에서는 toorun Linux 응용 프로그램 및 작업 hello에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="5f28c-105">또한 이러한 리소스 toouse를 계획 하 고 있는 경우 배포 고려 사항 toobe 인식를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="5f28c-106">이 문서는 [Windows 가상 컴퓨터](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="5f28c-107">형식</span><span class="sxs-lookup"><span data-stu-id="5f28c-107">Type</span></span>                     | <span data-ttu-id="5f28c-108">크기</span><span class="sxs-lookup"><span data-stu-id="5f28c-108">Sizes</span></span>           |    <span data-ttu-id="5f28c-109">설명</span><span class="sxs-lookup"><span data-stu-id="5f28c-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="5f28c-110">범용</span><span class="sxs-lookup"><span data-stu-id="5f28c-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="5f28c-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span><span class="sxs-lookup"><span data-stu-id="5f28c-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="5f28c-112">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="5f28c-113">테스트 및 개발, 작은 toomedium 데이터베이스 및 낮은 toomedium 트래픽이 웹 서버에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="5f28c-114">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="5f28c-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="5f28c-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="5f28c-115">Fs, F</span></span>             | <span data-ttu-id="5f28c-116">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="5f28c-117">트래픽이 중간 정도인 웹 서버, 네트워크 어플라이언스, 일괄 처리 프로세스 및 응용 프로그램 서버에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="5f28c-118">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="5f28c-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="5f28c-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="5f28c-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="5f28c-120">메모리 대 CPU 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="5f28c-121">관계형 데이터베이스 서버, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="5f28c-122">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="5f28c-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="5f28c-123">Ls</span><span class="sxs-lookup"><span data-stu-id="5f28c-123">Ls</span></span>                | <span data-ttu-id="5f28c-124">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="5f28c-124">High disk throughput and IO.</span></span> <span data-ttu-id="5f28c-125">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="5f28c-126">GPU</span><span class="sxs-lookup"><span data-stu-id="5f28c-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="5f28c-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="5f28c-127">NV, NC</span></span>            | <span data-ttu-id="5f28c-128">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 가상 컴퓨터로,</span><span class="sxs-lookup"><span data-stu-id="5f28c-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="5f28c-129">한 개 이상의 GPU를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="5f28c-130">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="5f28c-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="5f28c-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="5f28c-131">H, A8-11</span></span>          | <span data-ttu-id="5f28c-132">Microsoft의 가장 빠르고 강력한 CPU 가상 컴퓨터로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="5f28c-133">다양 한 크기의 hello 가격에 대 한 정보를 참조 하십시오. [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="5f28c-134">Azure 지역의 VM 크기 가용성에 대해서는 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f28c-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="5f28c-135">Azure Vm에서 일반적인 제한 사항이 toosee 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="5f28c-136">[ACU(Azure Compute 단위)](../windows/acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="5f28c-137">Rest API</span><span class="sxs-lookup"><span data-stu-id="5f28c-137">Rest API</span></span>

<span data-ttu-id="5f28c-138">VM 크기에 대 한 REST API tooquery hello를 사용 하는 방법은 hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="5f28c-139">크기 조정에 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="5f28c-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="5f28c-140">구독에 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="5f28c-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="5f28c-141">가용성 집합에서 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="5f28c-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="5f28c-142">ACU</span><span class="sxs-lookup"><span data-stu-id="5f28c-142">ACU</span></span>

<span data-ttu-id="5f28c-143">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f28c-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f28c-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f28c-144">Next steps</span></span>

<span data-ttu-id="5f28c-145">사용할 수 있는 hello 다른 VM 크기에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="5f28c-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="5f28c-146">범용</span><span class="sxs-lookup"><span data-stu-id="5f28c-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="5f28c-147">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="5f28c-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="5f28c-148">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="5f28c-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="5f28c-149">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="5f28c-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="5f28c-150">GPU</span><span class="sxs-lookup"><span data-stu-id="5f28c-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="5f28c-151">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="5f28c-151">High performance compute</span></span>](sizes-hpc.md)



