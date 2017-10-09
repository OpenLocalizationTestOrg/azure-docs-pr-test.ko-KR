---
title: "Azure에서 aaaWindows VM의 크기를 조정 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터에 사용할 수 있는 hello 다른 크기를 나열합니다."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="f81e3-103">Azure에서 Windows 가상 컴퓨터에 대한 크기</span><span class="sxs-lookup"><span data-stu-id="f81e3-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="f81e3-104">이 문서는 hello 사용 가능한 크기에 설명 하 고 옵션을 hello에 대 한 Azure 가상 컴퓨터를 Windows 응용 프로그램 및 작업 toorun를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="f81e3-105">또한 이러한 리소스 toouse를 계획 하 고 있는 경우 배포 고려 사항 toobe 인식를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="f81e3-106">이 문서는 [Linux 가상 컴퓨터](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="f81e3-107">형식</span><span class="sxs-lookup"><span data-stu-id="f81e3-107">Type</span></span>                     | <span data-ttu-id="f81e3-108">크기</span><span class="sxs-lookup"><span data-stu-id="f81e3-108">Sizes</span></span>           |    <span data-ttu-id="f81e3-109">설명</span><span class="sxs-lookup"><span data-stu-id="f81e3-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="f81e3-110">범용</span><span class="sxs-lookup"><span data-stu-id="f81e3-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="f81e3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="f81e3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="f81e3-112">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="f81e3-113">테스트 및 개발, 작은 toomedium 데이터베이스 및 낮은 toomedium 트래픽이 웹 서버에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="f81e3-114">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="f81e3-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="f81e3-115">Fs, F</span></span>             | <span data-ttu-id="f81e3-116">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="f81e3-117">트래픽이 중간 정도인 웹 서버, 네트워크 어플라이언스, 일괄 처리 프로세스 및 응용 프로그램 서버에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="f81e3-118">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="f81e3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="f81e3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="f81e3-120">메모리 대 CPU 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="f81e3-121">관계형 데이터베이스 서버, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="f81e3-122">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="f81e3-123">Ls</span><span class="sxs-lookup"><span data-stu-id="f81e3-123">Ls</span></span>                | <span data-ttu-id="f81e3-124">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="f81e3-124">High disk throughput and IO.</span></span> <span data-ttu-id="f81e3-125">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="f81e3-126">GPU</span><span class="sxs-lookup"><span data-stu-id="f81e3-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="f81e3-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="f81e3-127">NV, NC</span></span>            | <span data-ttu-id="f81e3-128">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 가상 컴퓨터로,</span><span class="sxs-lookup"><span data-stu-id="f81e3-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="f81e3-129">한 개 이상의 GPU를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="f81e3-130">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="f81e3-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="f81e3-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="f81e3-131">H, A8-11</span></span>          | <span data-ttu-id="f81e3-132">Microsoft의 가장 빠르고 강력한 CPU 가상 컴퓨터로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="f81e3-133">다양 한 크기의 hello 가격에 대 한 정보를 참조 하십시오. [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="f81e3-134">Azure Vm에서 일반적인 제한 사항이 toosee 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="f81e3-135">저장소 비용이 hello 저장소 계정에 사용 되는 페이지 기반 별도로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="f81e3-136">자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f81e3-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="f81e3-137">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="f81e3-138">Rest API</span><span class="sxs-lookup"><span data-stu-id="f81e3-138">Rest API</span></span>

<span data-ttu-id="f81e3-139">VM 크기에 대 한 REST API tooquery hello를 사용 하는 방법은 hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="f81e3-140">크기 조정에 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="f81e3-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="f81e3-141">구독에 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="f81e3-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="f81e3-142">가용성 집합에서 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="f81e3-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="f81e3-143">ACU</span><span class="sxs-lookup"><span data-stu-id="f81e3-143">ACU</span></span>

<span data-ttu-id="f81e3-144">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f81e3-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f81e3-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f81e3-145">Next steps</span></span>

<span data-ttu-id="f81e3-146">사용할 수 있는 hello 다른 VM 크기에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="f81e3-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="f81e3-147">범용</span><span class="sxs-lookup"><span data-stu-id="f81e3-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="f81e3-148">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="f81e3-149">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="f81e3-150">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="f81e3-151">GPU에 최적화</span><span class="sxs-lookup"><span data-stu-id="f81e3-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="f81e3-152">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="f81e3-152">High performance compute</span></span>](sizes-hpc.md)



