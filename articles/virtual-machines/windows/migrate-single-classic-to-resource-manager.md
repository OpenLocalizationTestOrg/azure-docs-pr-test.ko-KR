---
title: "클래식 VM tooan ARM 관리 디스크 VM aaaMigrate | Microsoft Docs"
description: "단일 Azure VM hello 클래식 배포에서 마이그레이션 tooManaged 디스크 hello 리소스 관리자 배포 모델에서 모델입니다."
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="bbdb6-103">기본 VM tooa로 직접 마이그레이션하 ARM 관리 되는 디스크의에서 새 VM VHD hello</span><span class="sxs-lookup"><span data-stu-id="bbdb6-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="bbdb6-104">이 섹션에서는 toomigrate 하면 기존 Azure Vm에 hello 클래식 배포 모델에서 너무[관리 하는 디스크](managed-disks-overview.md) hello 리소스 관리자 배포 모델에서.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="bbdb6-105">Hello 마이그레이션 계획 tooManaged 디스크</span><span class="sxs-lookup"><span data-stu-id="bbdb6-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="bbdb6-106">이 섹션 toomake hello 최선의 결정을 VM 및 디스크 유형에 대 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="bbdb6-107">위치</span><span class="sxs-lookup"><span data-stu-id="bbdb6-107">Location</span></span>

<span data-ttu-id="bbdb6-108">Azure Managed Disks를 사용할 수 있는 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="bbdb6-109">TooPremium 관리 하는 디스크를 마이그레이션하는 경우 또한 toomigrate를 계획 하는 hello 지역에서 프리미엄 저장소를 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="bbdb6-110">사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="bbdb6-111">VM 크기</span><span class="sxs-lookup"><span data-stu-id="bbdb6-111">VM sizes</span></span>

<span data-ttu-id="bbdb6-112">TooPremium 관리 하는 디스크를 마이그레이션하는 경우 VM이 있는 hello 영역의 tooupdate hello 크기인 hello VM tooPremium 사용 가능한 저장소 가능 크기를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="bbdb6-113">프리미엄 저장소 수 있는 hello VM 크기를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="bbdb6-114">hello Azure VM 크기 사양에 나열 된 [가상 컴퓨터의 크기](sizes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="bbdb6-115">프리미엄 저장소를 사용 하 고 작업에 가장 적합 한 hello 가장 적절 한 VM 크기를 선택 하는 가상 컴퓨터의 hello 성능 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="bbdb6-116">VM toodrive hello 디스크 트래픽에 사용할 수 있는 충분 한 대역폭이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="bbdb6-117">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="bbdb6-117">Disk sizes</span></span>

<span data-ttu-id="bbdb6-118">**프리미엄 Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="bbdb6-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="bbdb6-119">VM에서 사용할 수 있는 프리미엄 관리 디스크에는 7가지 형식이 있으며 각 형식에는 특정 IOP 및 처리량 한도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="bbdb6-120">Hello 프리미엄 디스크 유형 VM에 대 한 용량, 성능, 확장성, 관점에서 응용 프로그램의 hello 요구 사항에 따라 적중 영향과 최고 선택할 때 이러한 제한을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="bbdb6-121">프리미엄 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="bbdb6-121">Premium Disks Type</span></span>  | <span data-ttu-id="bbdb6-122">P4</span><span class="sxs-lookup"><span data-stu-id="bbdb6-122">P4</span></span>    | <span data-ttu-id="bbdb6-123">P6</span><span class="sxs-lookup"><span data-stu-id="bbdb6-123">P6</span></span>    | <span data-ttu-id="bbdb6-124">P10</span><span class="sxs-lookup"><span data-stu-id="bbdb6-124">P10</span></span>   | <span data-ttu-id="bbdb6-125">P20</span><span class="sxs-lookup"><span data-stu-id="bbdb6-125">P20</span></span>   | <span data-ttu-id="bbdb6-126">P30</span><span class="sxs-lookup"><span data-stu-id="bbdb6-126">P30</span></span>   | <span data-ttu-id="bbdb6-127">P40</span><span class="sxs-lookup"><span data-stu-id="bbdb6-127">P40</span></span>   | <span data-ttu-id="bbdb6-128">P50</span><span class="sxs-lookup"><span data-stu-id="bbdb6-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="bbdb6-129">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="bbdb6-129">Disk size</span></span>           | <span data-ttu-id="bbdb6-130">128GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-130">128 GB</span></span>| <span data-ttu-id="bbdb6-131">512GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-131">512 GB</span></span>| <span data-ttu-id="bbdb6-132">128GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-132">128 GB</span></span>| <span data-ttu-id="bbdb6-133">512GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-133">512 GB</span></span>            | <span data-ttu-id="bbdb6-134">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="bbdb6-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="bbdb6-135">2,048GB(2TB)</span><span class="sxs-lookup"><span data-stu-id="bbdb6-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="bbdb6-136">4,095GB(4TB)</span><span class="sxs-lookup"><span data-stu-id="bbdb6-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="bbdb6-137">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="bbdb6-137">IOPS per disk</span></span>       | <span data-ttu-id="bbdb6-138">120</span><span class="sxs-lookup"><span data-stu-id="bbdb6-138">120</span></span>   | <span data-ttu-id="bbdb6-139">240</span><span class="sxs-lookup"><span data-stu-id="bbdb6-139">240</span></span>   | <span data-ttu-id="bbdb6-140">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-140">500</span></span>   | <span data-ttu-id="bbdb6-141">2,300</span><span class="sxs-lookup"><span data-stu-id="bbdb6-141">2300</span></span>              | <span data-ttu-id="bbdb6-142">5,000</span><span class="sxs-lookup"><span data-stu-id="bbdb6-142">5000</span></span>              | <span data-ttu-id="bbdb6-143">7,500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-143">7500</span></span>              | <span data-ttu-id="bbdb6-144">7,500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-144">7500</span></span>              | 
| <span data-ttu-id="bbdb6-145">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="bbdb6-145">Throughput per disk</span></span> | <span data-ttu-id="bbdb6-146">초당 25MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-146">25 MB per second</span></span>  | <span data-ttu-id="bbdb6-147">초당 50MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-147">50 MB per second</span></span>  | <span data-ttu-id="bbdb6-148">초당 100MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-148">100 MB per second</span></span> | <span data-ttu-id="bbdb6-149">초당 150MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-149">150 MB per second</span></span> | <span data-ttu-id="bbdb6-150">초당 200MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-150">200 MB per second</span></span> | <span data-ttu-id="bbdb6-151">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-151">250 MB per second</span></span> | <span data-ttu-id="bbdb6-152">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-152">250 MB per second</span></span> | 

<span data-ttu-id="bbdb6-153">**표준 Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="bbdb6-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="bbdb6-154">VM에서 사용할 수 있는 표준 관리 디스크에는 7가지 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="bbdb6-155">각각은 용량이 다르지만 동일한 IOPS 및 처리량이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="bbdb6-156">Hello 유형의 응용 프로그램의 hello 용량 요구 사항에 따라 관리 되는 표준 디스크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="bbdb6-157">표준 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="bbdb6-157">Standard Disk Type</span></span>  | <span data-ttu-id="bbdb6-158">S4</span><span class="sxs-lookup"><span data-stu-id="bbdb6-158">S4</span></span>               | <span data-ttu-id="bbdb6-159">S6</span><span class="sxs-lookup"><span data-stu-id="bbdb6-159">S6</span></span>               | <span data-ttu-id="bbdb6-160">S10</span><span class="sxs-lookup"><span data-stu-id="bbdb6-160">S10</span></span>              | <span data-ttu-id="bbdb6-161">S20</span><span class="sxs-lookup"><span data-stu-id="bbdb6-161">S20</span></span>              | <span data-ttu-id="bbdb6-162">S30</span><span class="sxs-lookup"><span data-stu-id="bbdb6-162">S30</span></span>              | <span data-ttu-id="bbdb6-163">S40</span><span class="sxs-lookup"><span data-stu-id="bbdb6-163">S40</span></span>              | <span data-ttu-id="bbdb6-164">S50</span><span class="sxs-lookup"><span data-stu-id="bbdb6-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="bbdb6-165">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="bbdb6-165">Disk size</span></span>           | <span data-ttu-id="bbdb6-166">30GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-166">30 GB</span></span>            | <span data-ttu-id="bbdb6-167">64GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-167">64 GB</span></span>            | <span data-ttu-id="bbdb6-168">128GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-168">128 GB</span></span>           | <span data-ttu-id="bbdb6-169">512GB</span><span class="sxs-lookup"><span data-stu-id="bbdb6-169">512 GB</span></span>           | <span data-ttu-id="bbdb6-170">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="bbdb6-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="bbdb6-171">2,048GB(2TB)</span><span class="sxs-lookup"><span data-stu-id="bbdb6-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="bbdb6-172">4,095GB(4TB)</span><span class="sxs-lookup"><span data-stu-id="bbdb6-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="bbdb6-173">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="bbdb6-173">IOPS per disk</span></span>       | <span data-ttu-id="bbdb6-174">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-174">500</span></span>              | <span data-ttu-id="bbdb6-175">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-175">500</span></span>              | <span data-ttu-id="bbdb6-176">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-176">500</span></span>              | <span data-ttu-id="bbdb6-177">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-177">500</span></span>              | <span data-ttu-id="bbdb6-178">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-178">500</span></span>              | <span data-ttu-id="bbdb6-179">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-179">500</span></span>             | <span data-ttu-id="bbdb6-180">500</span><span class="sxs-lookup"><span data-stu-id="bbdb6-180">500</span></span>              | 
| <span data-ttu-id="bbdb6-181">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="bbdb6-181">Throughput per disk</span></span> | <span data-ttu-id="bbdb6-182">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-182">60 MB per second</span></span> | <span data-ttu-id="bbdb6-183">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-183">60 MB per second</span></span> | <span data-ttu-id="bbdb6-184">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-184">60 MB per second</span></span> | <span data-ttu-id="bbdb6-185">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-185">60 MB per second</span></span> | <span data-ttu-id="bbdb6-186">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-186">60 MB per second</span></span> | <span data-ttu-id="bbdb6-187">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-187">60 MB per second</span></span> | <span data-ttu-id="bbdb6-188">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="bbdb6-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="bbdb6-189">디스크 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="bbdb6-189">Disk caching policy</span></span> 

<span data-ttu-id="bbdb6-190">**프리미엄 Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="bbdb6-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="bbdb6-191">디스크 캐싱 정책은 기본적으로 *읽기 전용* 모든 hello 프리미엄 데이터 디스크에 대 한 및 *읽기 / 쓰기* hello 프리미엄 운영 체제 디스크에 대 한 toohello VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="bbdb6-192">이 구성 설정은 응용 프로그램의 IOs 용 tooachieve hello 최적의 성능은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="bbdb6-193">쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="bbdb6-194">가격</span><span class="sxs-lookup"><span data-stu-id="bbdb6-194">Pricing</span></span>

<span data-ttu-id="bbdb6-195">검토 hello [관리 하는 디스크에 대 한 가격 책정](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="bbdb6-196">프리미엄 관리 되는 디스크의 가격 책정은 hello 프리미엄 관리 되지 않는 디스크와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="bbdb6-197">하지만 표준 Managed Disks의 가격 책정은 관리되지 않는 표준 디스크와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="bbdb6-198">검사 목록</span><span class="sxs-lookup"><span data-stu-id="bbdb6-198">Checklist</span></span>

1.  <span data-ttu-id="bbdb6-199">TooPremium 관리 하는 디스크를 마이그레이션하는 경우은로 마이그레이션하는 hello 영역에 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="bbdb6-200">사용 하려는 hello 새 VM 시리즈를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="bbdb6-201">TooPremium 관리 하는 디스크를 마이그레이션하는 경우 프리미엄 저장소를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="bbdb6-202">Hello 정확한 VM 크기 사용 하 여로 마이그레이션하는 hello 지역에서 사용할 수 있는 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="bbdb6-203">VM 크기에 있는 데이터 디스크 개수 충분히 큰 toosupport hello toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="bbdb6-204">예를 들어 4 개의 데이터 디스크를 사용 하도록 설정한 경우 hello VM 두 개 이상의 코어에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="bbdb6-205">또한 처리 능력, 메모리 및 네트워크 대역폭 요구 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="bbdb6-206">정보 포함 하 고 hello 현재 VM 디스크 및 해당 VHD blob hello 목록을 포함 하 여 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="bbdb6-207">응용 프로그램의 가동 중지 시간을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-207">Prepare your application for downtime.</span></span> <span data-ttu-id="bbdb6-208">클린 마이그레이션 toodo toostop 모든 hello 처리는 hello 현재 시스템에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="bbdb6-209">경우에 표시할 수 있습니다 마이그레이션할 수 없는 tooconsistent 상태 toohello 새 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="bbdb6-210">작동 중단 기간 hello 디스크 toomigrate의 데이터 양을 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="bbdb6-211">Hello VM 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="bbdb6-211">Migrate hello VM</span></span>

<span data-ttu-id="bbdb6-212">응용 프로그램의 가동 중지 시간을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-212">Prepare your application for downtime.</span></span> <span data-ttu-id="bbdb6-213">클린 마이그레이션 toodo toostop 모든 hello 처리는 hello 현재 시스템에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="bbdb6-214">경우에 표시할 수 있습니다 마이그레이션할 수 없는 tooconsistent 상태 toohello 새 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="bbdb6-215">작동 중단 기간 hello hello 디스크 toomigrate의 데이터 양에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="bbdb6-216">먼저, hello 공통 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-216">First, set hello common parameters:</span></span>

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

2.  <span data-ttu-id="bbdb6-217">Hello에서 VHD hello를 사용 하 여 관리 되는 운영 체제 디스크를 만들 클래식 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="bbdb6-218">Hello 완료 URI hello OS VHD toohello $osVhdUri 매개 변수를 제공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="bbdb6-219">또한 마이그레이션하는 디스크의 종류(프리미엄 또는 표준)에 따라 **-AccountType**을 **PremiumLRS** 또는 **StandardLRS**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="bbdb6-220">Hello OS 디스크 toohello 연결 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="bbdb6-221">Hello 데이터 VHD 파일에서 관리 되는 데이터 디스크를 만들고 toohello 추가 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="bbdb6-222">만들 공용 IP, 가상 네트워크 및 NIC. 설정 하 여 새 VM을 hello</span><span class="sxs-lookup"><span data-stu-id="bbdb6-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

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
><span data-ttu-id="bbdb6-223">추가 단계가 필요한 toosupport 있을 수 있는 응용 프로그램에서 다룰 수 없는이 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bbdb6-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bbdb6-224">Next steps</span></span>

- <span data-ttu-id="bbdb6-225">Toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="bbdb6-226">자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb6-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

