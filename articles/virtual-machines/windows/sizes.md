---
title: "Azure의 Windows VM 크기 | Microsoft Docs"
description: "Azure의 Windows 가상 컴퓨터에 사용할 수 있는 다양한 크기를 나열합니다."
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
ms.openlocfilehash: b3a674137ed3dd47188d4af0bc845104eabc885e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="d880a-103">Azure에서 Windows 가상 컴퓨터에 대한 크기</span><span class="sxs-lookup"><span data-stu-id="d880a-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="d880a-104">이 문서에서는 Windows 앱 및 워크로드를 실행하는 데 사용할 수 있는 Azure 가상 컴퓨터에 대한 크기 및 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span></span> <span data-ttu-id="d880a-105">또한 이러한 리소스의 사용 계획을 세울 때 알아야 할 배포 고려 사항도 제공합니다.또한 이러한 리소스의 사용 계획을 세울 때 알아야 할 배포 고려 사항도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span>  <span data-ttu-id="d880a-106">이 문서는 [Linux 가상 컴퓨터](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="d880a-107">형식</span><span class="sxs-lookup"><span data-stu-id="d880a-107">Type</span></span>                     | <span data-ttu-id="d880a-108">크기</span><span class="sxs-lookup"><span data-stu-id="d880a-108">Sizes</span></span>           |    <span data-ttu-id="d880a-109">설명</span><span class="sxs-lookup"><span data-stu-id="d880a-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="d880a-110">범용</span><span class="sxs-lookup"><span data-stu-id="d880a-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="d880a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="d880a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="d880a-112">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="d880a-113">테스트 및 개발, 중소 규모 데이터베이스 및 트래픽이 적거나 중간 정도인 웹 서버에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="d880a-114">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="d880a-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="d880a-115">Fs, F</span></span>             | <span data-ttu-id="d880a-116">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="d880a-117">트래픽이 중간 정도인 웹 서버, 네트워크 어플라이언스, 일괄 처리 프로세스 및 응용 프로그램 서버에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="d880a-118">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="d880a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="d880a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="d880a-120">메모리 대 CPU 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="d880a-121">관계형 데이터베이스 서버, 중대형 캐시 및 메모리 내 분석에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="d880a-122">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="d880a-123">Ls</span><span class="sxs-lookup"><span data-stu-id="d880a-123">Ls</span></span>                | <span data-ttu-id="d880a-124">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="d880a-124">High disk throughput and IO.</span></span> <span data-ttu-id="d880a-125">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="d880a-126">GPU</span><span class="sxs-lookup"><span data-stu-id="d880a-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="d880a-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="d880a-127">NV, NC</span></span>            | <span data-ttu-id="d880a-128">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 가상 컴퓨터로,</span><span class="sxs-lookup"><span data-stu-id="d880a-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="d880a-129">한 개 이상의 GPU를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="d880a-130">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="d880a-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="d880a-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="d880a-131">H, A8-11</span></span>          | <span data-ttu-id="d880a-132">Microsoft의 가장 빠르고 강력한 CPU 가상 컴퓨터로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="d880a-133">다양한 크기의 가격 책정에 대한 자세한 내용은 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d880a-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="d880a-134">Azure VM에 대한 일반적인 제한은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d880a-134">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="d880a-135">저장소 비용은 저장소 계정에 사용된 페이지에 따라 개별적으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-135">Storage costs are calculated separately based on used pages in the storage account.</span></span> <span data-ttu-id="d880a-136">자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d880a-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="d880a-137">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="d880a-138">Rest API</span><span class="sxs-lookup"><span data-stu-id="d880a-138">Rest API</span></span>

<span data-ttu-id="d880a-139">REST API를 사용하여 VM 크기에 대해 쿼리하는 방법은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d880a-139">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="d880a-140">크기 조정에 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="d880a-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="d880a-141">구독에 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="d880a-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="d880a-142">가용성 집합에서 사용 가능한 가상 컴퓨터 크기 나열</span><span class="sxs-lookup"><span data-stu-id="d880a-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="d880a-143">ACU</span><span class="sxs-lookup"><span data-stu-id="d880a-143">ACU</span></span>

<span data-ttu-id="d880a-144">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d880a-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d880a-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d880a-145">Next steps</span></span>

<span data-ttu-id="d880a-146">사용할 수 있는 다른 VM 크기에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d880a-146">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="d880a-147">범용</span><span class="sxs-lookup"><span data-stu-id="d880a-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="d880a-148">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="d880a-149">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="d880a-150">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="d880a-151">GPU에 최적화</span><span class="sxs-lookup"><span data-stu-id="d880a-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="d880a-152">고성능 계산</span><span class="sxs-lookup"><span data-stu-id="d880a-152">High performance compute</span></span>](sizes-hpc.md)



