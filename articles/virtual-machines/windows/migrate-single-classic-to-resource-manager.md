---
title: "클래식 VM을 ARM 관리 디스크 VM으로 마이그레이션 | Microsoft Docs"
description: "Resource Manager 배포 모델에서는 단일 Azure VM을 클래식 배포 모델에서 Managed Disks로 마이그레이션합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 82389834d85981c0ed71bdcc891fbfdbe1377654
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="76bbc-103">VHD에서 클래식 VM을 새 ARM 관리 디스크 VM으로 수동으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="76bbc-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="76bbc-104">이 섹션을 통해 Resource Manager 배포 모델에서는 기존 Azure VM을 클래식 배포 모델에서 [Managed Disks](managed-disks-overview.md)로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="76bbc-105">Managed Disks로 마이그레이션 계획 수립</span><span class="sxs-lookup"><span data-stu-id="76bbc-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="76bbc-106">이 섹션을 통해 VM 및 디스크 유형에 대한 최선의 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="76bbc-107">위치</span><span class="sxs-lookup"><span data-stu-id="76bbc-107">Location</span></span>

<span data-ttu-id="76bbc-108">Azure Managed Disks를 사용할 수 있는 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="76bbc-109">프리미엄 Managed Disks를 마이그레이션하는 경우에도 마이그레이션하려고 계획한 지역에서 Premium Storage를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="76bbc-110">사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76bbc-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="76bbc-111">VM 크기</span><span class="sxs-lookup"><span data-stu-id="76bbc-111">VM sizes</span></span>

<span data-ttu-id="76bbc-112">프리미엄 Managed Disks를 마이그레이션하는 경우 VM 크기를 VM이 위치한 지역에서 제공하는 Premium Storage 지원 가능 크기로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="76bbc-113">Premium Storage를 사용할 수 있는 VM 크기를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="76bbc-114">Azure VM 크기 사양은 [가상 컴퓨터의 크기](sizes.md)에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="76bbc-115">프리미엄 저장소와 작동하는 가상 컴퓨터의 성능 특징을 검토하고 워크로드에 가장 적합한 VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="76bbc-116">VM에서 디스크 트래픽을 제어하기에 충분한 대역폭을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="76bbc-117">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="76bbc-117">Disk sizes</span></span>

<span data-ttu-id="76bbc-118">**프리미엄 Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="76bbc-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="76bbc-119">VM에서 사용할 수 있는 프리미엄 관리 디스크에는 7가지 형식이 있으며 각 형식에는 특정 IOP 및 처리량 한도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="76bbc-120">용량, 성능, 확장성 및 최대 로드 측면에서 응용 프로그램의 필요에 따라 VM에 대한 프리미엄 디스크 유형을 선택할 때 이 제한을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="76bbc-121">프리미엄 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="76bbc-121">Premium Disks Type</span></span>  | <span data-ttu-id="76bbc-122">P4</span><span class="sxs-lookup"><span data-stu-id="76bbc-122">P4</span></span>    | <span data-ttu-id="76bbc-123">P6</span><span class="sxs-lookup"><span data-stu-id="76bbc-123">P6</span></span>    | <span data-ttu-id="76bbc-124">P10</span><span class="sxs-lookup"><span data-stu-id="76bbc-124">P10</span></span>   | <span data-ttu-id="76bbc-125">P20</span><span class="sxs-lookup"><span data-stu-id="76bbc-125">P20</span></span>   | <span data-ttu-id="76bbc-126">P30</span><span class="sxs-lookup"><span data-stu-id="76bbc-126">P30</span></span>   | <span data-ttu-id="76bbc-127">P40</span><span class="sxs-lookup"><span data-stu-id="76bbc-127">P40</span></span>   | <span data-ttu-id="76bbc-128">P50</span><span class="sxs-lookup"><span data-stu-id="76bbc-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="76bbc-129">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="76bbc-129">Disk size</span></span>           | <span data-ttu-id="76bbc-130">128GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-130">128 GB</span></span>| <span data-ttu-id="76bbc-131">512GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-131">512 GB</span></span>| <span data-ttu-id="76bbc-132">128GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-132">128 GB</span></span>| <span data-ttu-id="76bbc-133">512GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-133">512 GB</span></span>            | <span data-ttu-id="76bbc-134">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="76bbc-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="76bbc-135">2,048GB(2TB)</span><span class="sxs-lookup"><span data-stu-id="76bbc-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="76bbc-136">4,095GB(4TB)</span><span class="sxs-lookup"><span data-stu-id="76bbc-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="76bbc-137">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="76bbc-137">IOPS per disk</span></span>       | <span data-ttu-id="76bbc-138">120</span><span class="sxs-lookup"><span data-stu-id="76bbc-138">120</span></span>   | <span data-ttu-id="76bbc-139">240</span><span class="sxs-lookup"><span data-stu-id="76bbc-139">240</span></span>   | <span data-ttu-id="76bbc-140">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-140">500</span></span>   | <span data-ttu-id="76bbc-141">2,300</span><span class="sxs-lookup"><span data-stu-id="76bbc-141">2300</span></span>              | <span data-ttu-id="76bbc-142">5,000</span><span class="sxs-lookup"><span data-stu-id="76bbc-142">5000</span></span>              | <span data-ttu-id="76bbc-143">7,500</span><span class="sxs-lookup"><span data-stu-id="76bbc-143">7500</span></span>              | <span data-ttu-id="76bbc-144">7,500</span><span class="sxs-lookup"><span data-stu-id="76bbc-144">7500</span></span>              | 
| <span data-ttu-id="76bbc-145">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="76bbc-145">Throughput per disk</span></span> | <span data-ttu-id="76bbc-146">초당 25MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-146">25 MB per second</span></span>  | <span data-ttu-id="76bbc-147">초당 50MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-147">50 MB per second</span></span>  | <span data-ttu-id="76bbc-148">초당 100MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-148">100 MB per second</span></span> | <span data-ttu-id="76bbc-149">초당 150MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-149">150 MB per second</span></span> | <span data-ttu-id="76bbc-150">초당 200MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-150">200 MB per second</span></span> | <span data-ttu-id="76bbc-151">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-151">250 MB per second</span></span> | <span data-ttu-id="76bbc-152">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="76bbc-152">250 MB per second</span></span> | 

<span data-ttu-id="76bbc-153">**표준 Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="76bbc-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="76bbc-154">VM에서 사용할 수 있는 표준 관리 디스크에는 7가지 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="76bbc-155">각각은 용량이 다르지만 동일한 IOPS 및 처리량이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="76bbc-156">응용 프로그램의 용량 요구 사항에 따라 표준 Managed Disks의 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="76bbc-157">표준 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="76bbc-157">Standard Disk Type</span></span>  | <span data-ttu-id="76bbc-158">S4</span><span class="sxs-lookup"><span data-stu-id="76bbc-158">S4</span></span>               | <span data-ttu-id="76bbc-159">S6</span><span class="sxs-lookup"><span data-stu-id="76bbc-159">S6</span></span>               | <span data-ttu-id="76bbc-160">S10</span><span class="sxs-lookup"><span data-stu-id="76bbc-160">S10</span></span>              | <span data-ttu-id="76bbc-161">S20</span><span class="sxs-lookup"><span data-stu-id="76bbc-161">S20</span></span>              | <span data-ttu-id="76bbc-162">S30</span><span class="sxs-lookup"><span data-stu-id="76bbc-162">S30</span></span>              | <span data-ttu-id="76bbc-163">S40</span><span class="sxs-lookup"><span data-stu-id="76bbc-163">S40</span></span>              | <span data-ttu-id="76bbc-164">S50</span><span class="sxs-lookup"><span data-stu-id="76bbc-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="76bbc-165">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="76bbc-165">Disk size</span></span>           | <span data-ttu-id="76bbc-166">30GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-166">30 GB</span></span>            | <span data-ttu-id="76bbc-167">64GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-167">64 GB</span></span>            | <span data-ttu-id="76bbc-168">128GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-168">128 GB</span></span>           | <span data-ttu-id="76bbc-169">512GB</span><span class="sxs-lookup"><span data-stu-id="76bbc-169">512 GB</span></span>           | <span data-ttu-id="76bbc-170">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="76bbc-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="76bbc-171">2,048GB(2TB)</span><span class="sxs-lookup"><span data-stu-id="76bbc-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="76bbc-172">4,095GB(4TB)</span><span class="sxs-lookup"><span data-stu-id="76bbc-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="76bbc-173">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="76bbc-173">IOPS per disk</span></span>       | <span data-ttu-id="76bbc-174">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-174">500</span></span>              | <span data-ttu-id="76bbc-175">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-175">500</span></span>              | <span data-ttu-id="76bbc-176">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-176">500</span></span>              | <span data-ttu-id="76bbc-177">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-177">500</span></span>              | <span data-ttu-id="76bbc-178">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-178">500</span></span>              | <span data-ttu-id="76bbc-179">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-179">500</span></span>             | <span data-ttu-id="76bbc-180">500</span><span class="sxs-lookup"><span data-stu-id="76bbc-180">500</span></span>              | 
| <span data-ttu-id="76bbc-181">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="76bbc-181">Throughput per disk</span></span> | <span data-ttu-id="76bbc-182">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-182">60 MB per second</span></span> | <span data-ttu-id="76bbc-183">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-183">60 MB per second</span></span> | <span data-ttu-id="76bbc-184">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-184">60 MB per second</span></span> | <span data-ttu-id="76bbc-185">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-185">60 MB per second</span></span> | <span data-ttu-id="76bbc-186">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-186">60 MB per second</span></span> | <span data-ttu-id="76bbc-187">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-187">60 MB per second</span></span> | <span data-ttu-id="76bbc-188">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="76bbc-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="76bbc-189">디스크 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="76bbc-189">Disk caching policy</span></span> 

<span data-ttu-id="76bbc-190">**프리미엄 Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="76bbc-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="76bbc-191">기본적으로 디스크 캐싱 정책은 VM에 연결된 프리미엄 운영 체제 디스크에 대한 *읽기 / 쓰기* 및 모든 프리미엄 데이터 디스크에 대한 *읽기 전용*입니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="76bbc-192">응용 프로그램의 IO에 대한 최적의 성능을 얻으려면 이 구성 설정이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="76bbc-193">쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="76bbc-194">가격</span><span class="sxs-lookup"><span data-stu-id="76bbc-194">Pricing</span></span>

<span data-ttu-id="76bbc-195">[Managed Disks에 대한 가격 책정](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="76bbc-196">프리미엄 Managed Disks의 가격 책정은 관리되지 않는 프리미엄 디스크와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="76bbc-197">하지만 표준 Managed Disks의 가격 책정은 관리되지 않는 표준 디스크와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="76bbc-198">검사 목록</span><span class="sxs-lookup"><span data-stu-id="76bbc-198">Checklist</span></span>

1.  <span data-ttu-id="76bbc-199">프리미엄 Managed Disks를 마이그레이션하는 경우 마이그레이션하는 지역에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="76bbc-200">사용할 새 VM 시리즈를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="76bbc-201">프리미엄 Managed Disks로 마이그레이션하는 경우 Premium Storage를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="76bbc-202">마이그레이션하는 지역에서 사용할 수 있는 정확한 VM 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="76bbc-203">VM 크기는 현재 포함하고 있는 데이터 디스크 수를 지원할 만큼 충분히 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="76bbc-204">예를 들어, 4개의 데이터 디스크가 있는 경우 VM에는 두 개 이상의 코어가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="76bbc-205">또한 처리 능력, 메모리 및 네트워크 대역폭 요구 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="76bbc-206">디스크 및 해당 VHD Blob의 목록을 포함하여 도움이 될 현재 VM 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="76bbc-207">응용 프로그램의 가동 중지 시간을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-207">Prepare your application for downtime.</span></span> <span data-ttu-id="76bbc-208">원활한 마이그레이션 작업을 수행하려면 현재 시스템에서 모든 처리를 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="76bbc-209">그런 다음 새 플랫폼으로 마이그레이션할 수 있는 일관된 상태로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="76bbc-210">가동 중지 시간은 디스크에서 마이그레이션할 데이터 양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="76bbc-211">VM 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="76bbc-211">Migrate the VM</span></span>

<span data-ttu-id="76bbc-212">응용 프로그램의 가동 중지 시간을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-212">Prepare your application for downtime.</span></span> <span data-ttu-id="76bbc-213">원활한 마이그레이션 작업을 수행하려면 현재 시스템에서 모든 처리를 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="76bbc-214">그런 다음 새 플랫폼으로 마이그레이션할 수 있는 일관된 상태로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="76bbc-215">가동 중지 시간은 디스크에서 마이그레이션할 데이터 양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="76bbc-216">먼저, 공통 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-216">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="76bbc-217">클래식 VM에서 VHD를 사용하여 관리되는 OS 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-217">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="76bbc-218">$osVhdUri 매개 변수에 OS VHD의 전체 URI를 제공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-218">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="76bbc-219">또한 마이그레이션하는 디스크의 종류(프리미엄 또는 표준)에 따라 **-AccountType**을 **PremiumLRS** 또는 **StandardLRS**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="76bbc-220">새 VM에 OS 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-220">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="76bbc-221">데이터 VHD 파일에서 관리되는 데이터 디스크를 만들고 새 VM에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-221">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="76bbc-222">공용 IP, Virtual Network 및 NIC를 설정하여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-222">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="76bbc-223">이 가이드에서 다루지 않은 응용 프로그램을 지원하기 위해 추가 단계가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-223">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="76bbc-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76bbc-224">Next steps</span></span>

- <span data-ttu-id="76bbc-225">가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="76bbc-225">Connect to the virtual machine.</span></span> <span data-ttu-id="76bbc-226">자세한 내용은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76bbc-226">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

