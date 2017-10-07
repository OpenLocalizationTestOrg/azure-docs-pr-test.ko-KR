---
title: "프리미엄 저장소 aaaMigrating Vm tooAzure | Microsoft Docs"
description: "프로그램 기존 Vm tooAzure 프리미엄 저장소를 마이그레이션하십시오. 프리미엄 저장소는 Azure 가상 컴퓨터에서 실행되는 I/O 사용량이 많은 작업에 대해 대기 시간이 짧은 고성능 디스크 지원을 제공합니다."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="dbe33-104">마이그레이션 tooAzure 프리미엄 저장소 (관리 되지 않는 디스크)</span><span class="sxs-lookup"><span data-stu-id="dbe33-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="dbe33-105">이 문서에서는 toomigrate tooa 관리 되지 않는 표준 디스크를 사용 하는 VM을 사용 하는 VM에서 프리미엄 디스크를 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="dbe33-106">새 Vm에 Azure 관리 되는 디스크를 사용 하 고 이전 관리 되지 않는 디스크 toomanaged 디스크를 변환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="dbe33-107">관리 디스크 핸들 hello 기본 저장소 계정 하므로 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="dbe33-108">자세한 내용은 [Managed Disks 개요](../../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="dbe33-109">Azure 프리미엄 저장소는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="dbe33-110">Hello 속도 활용 하 고 이러한 디스크는 성능 응용 프로그램의 VM 디스크 tooAzure 프리미엄 저장소를 마이그레이션하여 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="dbe33-111">이 가이드의 hello 목적은 toohelp 더 나은 Azure 프리미엄 저장소의 새 사용자가 자신의 현재 시스템 tooPremium 저장소에서에서 부드럽게 전환 toomake 준비입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="dbe33-112">hello 가이드 hello이이 과정의 주요 구성 요소 중 3 개 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="dbe33-113">Hello 마이그레이션 tooPremium 저장소에 대 한 계획</span><span class="sxs-lookup"><span data-stu-id="dbe33-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="dbe33-114">준비 및 복사 가상 하드 디스크 (Vhd) tooPremium 저장소</span><span class="sxs-lookup"><span data-stu-id="dbe33-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="dbe33-115">Premium Storage를 사용하여 Azure 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="dbe33-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="dbe33-116">다른 플랫폼 tooAzure 프리미엄 저장소에서에서 Vm을 마이그레이션할 수도 있고 표준 저장소 tooPremium 저장소에서에서 기존 Azure Vm을 마이그레이션할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="dbe33-117">이 가이드에서는 두 시나리오의 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="dbe33-118">시나리오에 따라 hello 관련 섹션에 지정 된 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe33-119">Premium Storage의 기능 개요 및 가격 책정은 Premium Storage: [Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소](storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="dbe33-120">응용 프로그램에 대 한 hello 최상의 성능을 위해 높은 IOPS tooAzure 프리미엄 저장소를 필요로 하는 가상 컴퓨터 디스크를 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="dbe33-121">디스크에 높은 IOPS가 필요하지 않은 경우, 가상 컴퓨터 디스크 데이터를 SSD가 아닌 하드 디스크 드라이브(HDD)에 저자하는 표준 저장소를 사용하여 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="dbe33-122">이 가이드에서 제공 하는 hello 단계 앞뒤 모두 hello 마이그레이션 프로세스 완료의 전체 추가 작업 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="dbe33-123">Hello 응용 프로그램 내에서 자체 응용 프로그램에서 가동 중지 시간이 필요할 수 있는 코드를 변경 하거나 가상 네트워크 또는 끝점을 구성을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="dbe33-124">이러한 작업은 고유한 tooeach 응용 프로그램 및이 가이드 toomake hello 전체 전환 tooPremium 최대한 원활 하 게 저장소에에서 제공 된 hello 단계와 함께 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="dbe33-125"><a name="plan-the-migration-to-premium-storage"></a>Hello 마이그레이션 tooPremium 저장소에 대 한 계획</span><span class="sxs-lookup"><span data-stu-id="dbe33-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="dbe33-126">이 섹션 준비 toofollow이 문서의 hello 마이그레이션 단계는 toomake hello 최선의 결정 VM 및 디스크 유형에 대를 사용 하면을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dbe33-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dbe33-127">Prerequisites</span></span>
* <span data-ttu-id="dbe33-128">Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-128">You will need an Azure subscription.</span></span> <span data-ttu-id="dbe33-129">구독이 없다면, 한 달의 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 구독하거나 [Azure 가격 책정](https://azure.microsoft.com/pricing/)을 방문하여 추가 옵션을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="dbe33-130">PowerShell cmdlet tooexecute hello Microsoft Azure PowerShell 모듈을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="dbe33-131">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello에 대 한 지점 및 설치 지침을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="dbe33-132">프리미엄 저장소에서 실행 하는 Azure Vm toouse를 계획할 때는 toouse hello 프리미엄 저장소 가능 Vm 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="dbe33-133">Premium Storage 지원 VM에서 표준 저장소 디스크와 Premium Storage 디스크를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="dbe33-134">프리미엄 저장소 디스크는 이후 hello에서 더 많은 VM 형식과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="dbe33-135">사용 가능한 Azure VM 디스크 유형 및 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [클라우드 서비스 크기](../../cloud-services/cloud-services-sizes-specs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="dbe33-136">고려 사항</span><span class="sxs-lookup"><span data-stu-id="dbe33-136">Considerations</span></span>
<span data-ttu-id="dbe33-137">Azure VM 지원 응용 프로그램은 VM 당 저장소 too256 TB를 유지할 수 있도록 여러 프리미엄 저장소 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="dbe33-138">프리미엄 저장소를 사용할 경우 읽기 작업의 대기 시간이 매우 짧은 상태로 VM당 80,000 IOPS(초당 입/출력 작업 수) 및 VM당 디스크 처리량 초당 2000MB를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="dbe33-139">다양한 VM 및 디스크 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="dbe33-140">이 섹션은 toohelp toofind 워크 로드에 가장 적합 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="dbe33-141">VM 크기</span><span class="sxs-lookup"><span data-stu-id="dbe33-141">VM sizes</span></span>
<span data-ttu-id="dbe33-142">hello Azure VM 크기 사양에 나열 된 [가상 컴퓨터의 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dbe33-143">프리미엄 저장소를 사용 하 고 작업에 가장 적합 한 hello 가장 적절 한 VM 크기를 선택 하는 가상 컴퓨터의 hello 성능 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="dbe33-144">VM toodrive hello 디스크 트래픽에 사용할 수 있는 충분 한 대역폭이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="dbe33-145">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="dbe33-145">Disk sizes</span></span>
<span data-ttu-id="dbe33-146">VM에서 사용할 수 있는 디스크에는 다섯 종류가 있으며 각 종류에는 특정 IOP 및 처리량 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="dbe33-147">이러한 제한은 때 고려해 용량, 성능, 확장성, 관점에서 응용 프로그램의 hello 요구 사항에 따라 VM에 대 한 hello 디스크 유형을 선택 하 고 최대 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="dbe33-148">프리미엄 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="dbe33-148">Premium Disks Type</span></span>  | <span data-ttu-id="dbe33-149">P10</span><span class="sxs-lookup"><span data-stu-id="dbe33-149">P10</span></span>   | <span data-ttu-id="dbe33-150">P20</span><span class="sxs-lookup"><span data-stu-id="dbe33-150">P20</span></span>   | <span data-ttu-id="dbe33-151">P30</span><span class="sxs-lookup"><span data-stu-id="dbe33-151">P30</span></span>            | <span data-ttu-id="dbe33-152">P40</span><span class="sxs-lookup"><span data-stu-id="dbe33-152">P40</span></span>            | <span data-ttu-id="dbe33-153">P50</span><span class="sxs-lookup"><span data-stu-id="dbe33-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="dbe33-154">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="dbe33-154">Disk size</span></span>           | <span data-ttu-id="dbe33-155">128GB</span><span class="sxs-lookup"><span data-stu-id="dbe33-155">128 GB</span></span>| <span data-ttu-id="dbe33-156">512GB</span><span class="sxs-lookup"><span data-stu-id="dbe33-156">512 GB</span></span>| <span data-ttu-id="dbe33-157">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="dbe33-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="dbe33-158">2,048GB(2TB)</span><span class="sxs-lookup"><span data-stu-id="dbe33-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="dbe33-159">4,095GB(4TB)</span><span class="sxs-lookup"><span data-stu-id="dbe33-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="dbe33-160">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="dbe33-160">IOPS per disk</span></span>       | <span data-ttu-id="dbe33-161">500</span><span class="sxs-lookup"><span data-stu-id="dbe33-161">500</span></span>   | <span data-ttu-id="dbe33-162">2,300</span><span class="sxs-lookup"><span data-stu-id="dbe33-162">2300</span></span>  | <span data-ttu-id="dbe33-163">5,000</span><span class="sxs-lookup"><span data-stu-id="dbe33-163">5000</span></span>           | <span data-ttu-id="dbe33-164">7,500</span><span class="sxs-lookup"><span data-stu-id="dbe33-164">7500</span></span>           | <span data-ttu-id="dbe33-165">7,500</span><span class="sxs-lookup"><span data-stu-id="dbe33-165">7500</span></span>           | 
| <span data-ttu-id="dbe33-166">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="dbe33-166">Throughput per disk</span></span> | <span data-ttu-id="dbe33-167">초당 100MB</span><span class="sxs-lookup"><span data-stu-id="dbe33-167">100 MB per second</span></span> | <span data-ttu-id="dbe33-168">초당 150MB</span><span class="sxs-lookup"><span data-stu-id="dbe33-168">150 MB per second</span></span> | <span data-ttu-id="dbe33-169">초당 200MB</span><span class="sxs-lookup"><span data-stu-id="dbe33-169">200 MB per second</span></span> | <span data-ttu-id="dbe33-170">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="dbe33-170">250 MB per second</span></span> | <span data-ttu-id="dbe33-171">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="dbe33-171">250 MB per second</span></span> |

<span data-ttu-id="dbe33-172">사용자 워크로드에 따라 추가 데이터 디스크가 VM에 필요한 경우를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="dbe33-173">여러 영구 데이터 디스크 tooyour VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="dbe33-174">필요한 경우에 hello 디스크 tooincrease hello 용량 및 성능 hello 볼륨에 걸쳐 스트라이프 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="dbe33-175">(디스크 스트라이프란 무엇인지 [여기서](storage-premium-storage-performance.md#disk-striping) 확인하세요.) [저장소 공간][4]을 사용하여 프리미엄 저장소 데이터 디스크를 스트라이프하는 경우, 사용되는 각 디스크에 대해 하나의 열로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="dbe33-176">그렇지 않으면 hello 전반적인 성능이 hello 스트라이프 볼륨의 수 있습니다 hello 디스크에 걸쳐 트래픽의 toouneven 배포 인해 예상 보다 더 낮은.</span><span class="sxs-lookup"><span data-stu-id="dbe33-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="dbe33-177">Linux Vm에 대 한 hello를 사용할 수 있습니다 *mdadm* 유틸리티 tooachieve hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="dbe33-178">자세한 내용은 [Linux에서 소프트웨어 RAID 구성](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="dbe33-179">저장소 계정의 확장성 목표</span><span class="sxs-lookup"><span data-stu-id="dbe33-179">Storage account scalability targets</span></span>
<span data-ttu-id="dbe33-180">프리미엄 저장소 계정 추가 toohello의 확장성 목표를 수행 하는 hello가 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="dbe33-181">응용 프로그램 요구 사항 단일 저장소 계정의 확장성 목표 hello를 초과 하는 경우 응용 프로그램 toouse 여러 저장소 계정을 빌드하고 해당 저장소 계정에서 데이터를 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="dbe33-182">총 계정 용량</span><span class="sxs-lookup"><span data-stu-id="dbe33-182">Total Account Capacity</span></span> | <span data-ttu-id="dbe33-183">로컬 중복 저장소 계정의 총 대역폭</span><span class="sxs-lookup"><span data-stu-id="dbe33-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbe33-184">디스크 용량: 35TB</span><span class="sxs-lookup"><span data-stu-id="dbe33-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="dbe33-185">스냅숏 용량: 10TB</span><span class="sxs-lookup"><span data-stu-id="dbe33-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="dbe33-186">인바운드 + 아웃 바운드에 대 한 초당 기가 비트 too50</span><span class="sxs-lookup"><span data-stu-id="dbe33-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="dbe33-187">에 대 한 자세한 내용은 프리미엄 저장소 사양에 hello, 체크 아웃 [확장성 및 성능 목표 프리미엄 저장소를 사용 하는 경우](storage-premium-storage.md#scalability-and-performance-targets)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="dbe33-188">디스크 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="dbe33-188">Disk caching policy</span></span>
<span data-ttu-id="dbe33-189">디스크 캐싱 정책은 기본적으로 *읽기 전용* 모든 hello 프리미엄 데이터 디스크에 대 한 및 *읽기 / 쓰기* hello 프리미엄 운영 체제 디스크에 대 한 toohello VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="dbe33-190">이 구성 설정은 응용 프로그램의 IOs 용 tooachieve hello 최적의 성능은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="dbe33-191">쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="dbe33-192">사용 하 여 기존 데이터 디스크에 대 한 hello 캐시 설정을 업데이트할 수 [Azure 포털](https://portal.azure.com) 또는 hello *-HostCaching* hello의 매개 변수 *Set-azuredatadisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dbe33-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="dbe33-193">위치</span><span class="sxs-lookup"><span data-stu-id="dbe33-193">Location</span></span>
<span data-ttu-id="dbe33-194">Azure 프리미엄 저장소를 사용할 수 있는 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="dbe33-195">사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="dbe33-196">Hello에 Vm 있는 동일한 지역의 저장소 계정이 VM hello 별도 영역에 있는 경우에 비해 훨씬 더 나은 성능을 제공 됩니다에 대 한 저장소 디스크는 hello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="dbe33-197">기타 Azure VM 구성 설정</span><span class="sxs-lookup"><span data-stu-id="dbe33-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="dbe33-198">Azure VM을 만들 때 됩니다 tooconfigure 특정 VM 설정은 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="dbe33-199">수정 하거나 나중에 다른 사용자를 추가 하는 동안 VM hello의 hello 수명 동안 고정 되는 설정 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dbe33-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="dbe33-200">이러한 Azure VM 구성 설정 검토 하 고 있는지 확인이 적절 하 게 구성 toomatch 작업 부하 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="dbe33-201">최적화</span><span class="sxs-lookup"><span data-stu-id="dbe33-201">Optimization</span></span>
<span data-ttu-id="dbe33-202">[Azure Premium Storage: 고성능을 위한 설계](storage-premium-storage-performance.md) Azure Premium Storage를 사용하여 고성능 응용 프로그램을 구축하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="dbe33-203">성능 모범 사례 적용 가능한 tootechnologies 응용 프로그램에서 사용 하는 함께 hello 지침을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="dbe33-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>준비 하 고 가상 하드 디스크 (Vhd) tooPremium 저장소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="dbe33-205">다음 단원을 hello VM에서 Vhd를 준비 하 고 Vhd tooAzure 저장소 복사에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="dbe33-206">시나리오 1: "마이그레이션하는 중입니다 기존 Azure Vm tooAzure 프리미엄 저장소."</span><span class="sxs-lookup"><span data-stu-id="dbe33-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="dbe33-207">시나리오 2: "마이그레이션하는 중입니다 Vm에서 다른 플랫폼 tooAzure 프리미엄 저장소."</span><span class="sxs-lookup"><span data-stu-id="dbe33-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="dbe33-208">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dbe33-208">Prerequisites</span></span>
<span data-ttu-id="dbe33-209">tooprepare hello Vhd 마이그레이션에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="dbe33-210">Azure 구독, 저장소 계정 및 해당 저장소의 컨테이너 계정 toowhich VHD를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="dbe33-211">Hello 대상 저장소 계정 요구 사항에 따라 표준 또는 프리미엄 저장소 계정 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="dbe33-212">VHD에서 여러 VM 인스턴스 toocreate를 계획 하는 경우 도구 toogeneralize 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="dbe33-213">예를 들어 Ubuntu용 virt-sysprep 또는 Windows용 sysprep입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="dbe33-214">한 도구 tooupload hello VHD 파일 toohello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="dbe33-215">참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md) 하거나 사용 하 여 프로그램 [Azure 저장소 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="dbe33-216">이 가이드에서 설명 hello AzCopy 도구를 사용 하 여 VHD를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe33-217">최적의 성능을 위해서는 azcopy를 동기 복사 옵션을 선택 하면 VHD를 복사 하 여 hello에 있는 Azure VM에서 다음이 도구 중 하나를 실행 하 여 hello 대상 저장소 계정과 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="dbe33-218">다른 지역에는 Azure VM에서 VHD를 복사 하는 경우 성능이 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="dbe33-219">제한 된 대역폭을 통해 많은 양의 데이터를 복사 하기 위한 것이 좋습니다 [hello Azure 가져오기/내보내기 서비스 tootransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md); 이렇게 하면 tootransfer 전달 하드 디스크에서 데이터 tooan Azure 드라이브 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](../storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="dbe33-220">Hello Azure 가져오기/내보내기 서비스 toocopy 데이터 tooa 표준 저장소 계정 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="dbe33-221">Hello 데이터는 표준 저장소 계정에 사용 하 여 어느 hello [Blob 복사 API](https://msdn.microsoft.com/library/azure/dd894037.aspx) 또는 AzCopy tootransfer hello 데이터 tooyour 프리미엄 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="dbe33-222">Microsoft Azure는 고정된 크기의 VHD 파일만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="dbe33-223">동적 VHD 또는 VHDX 파일은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="dbe33-224">동적 VHD를 설정한 경우 변환할 수 있습니다 hello를 사용 하 여 toofixed 크기 [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dbe33-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="dbe33-225"><a name="scenario1"></a>시나리오 1: "마이그레이션하는 중입니다 기존 Azure Vm tooAzure 프리미엄 저장소."</span><span class="sxs-lookup"><span data-stu-id="dbe33-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="dbe33-226">기존 Azure Vm에서 VM 중지 hello 마이그레이션하는 경우 원하는 VHD의 hello 유형당 Vhd를 준비 하 고 hello AzCopy 또는 PowerShell VHD를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="dbe33-227">hello VM toomigrate 깨끗 한 상태로 아래로 완전히 toobe가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="dbe33-228">Hello 마이그레이션 완료 될 때까지 가동 중지 시간이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="dbe33-229">1단계.</span><span class="sxs-lookup"><span data-stu-id="dbe33-229">Step 1.</span></span> <span data-ttu-id="dbe33-230">마이그레이션할 VHD를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="dbe33-231">기존 Azure Vm tooPremium 저장소를 마이그레이션하는 경우 VHD 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="dbe33-232">일반화된 운영 체제 이미지</span><span class="sxs-lookup"><span data-stu-id="dbe33-232">A generalized operating system image</span></span>
* <span data-ttu-id="dbe33-233">고유의 운영 체제 디스크</span><span class="sxs-lookup"><span data-stu-id="dbe33-233">A unique operating system disk</span></span>
* <span data-ttu-id="dbe33-234">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="dbe33-234">A data disk</span></span>

<span data-ttu-id="dbe33-235">아래에서는 VHD를 준비하기 위한 3가지 시나리오를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="dbe33-236">사용 하 여 일반화 된 운영 체제 VHD toocreate 여러 VM 인스턴스</span><span class="sxs-lookup"><span data-stu-id="dbe33-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="dbe33-237">업로드 하는 경우 사용 되는 toocreate 될 VHD 제네릭 Azure VM의 여러 인스턴스를 sysprep 유틸리티를 사용 하 여 VHD를 먼저 일반화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="dbe33-238">이 적용 됩니다 tooa 온-프레미스에 VHD 또는 hello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="dbe33-239">Sysprep은 VHD hello에서 모든 컴퓨터 관련 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbe33-240">스냅숏을 찍거나 VM을 백업하기 전에 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="dbe33-241">Sysprep를 실행 중인 사용 중지 하 고 hello VM 인스턴스를 할당 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="dbe33-242">Windows 운영 체제 VHD toosysprep 아래 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="dbe33-243">Note는 hello Sysprep 명령을 실행 해야 합니다 tooshut hello 가상 컴퓨터를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="dbe33-244">Sysprep에 대한 자세한 내용은 [Sysprep 개요](http://technet.microsoft.com/library/hh825209.aspx) 또는 [Sysprep 기술 참조](http://technet.microsoft.com/library/cc766049.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="dbe33-245">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="dbe33-246">다음 명령은 tooopen Sysprep hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="dbe33-247">시스템 준비 도구 hello 선택 입력 시스템 기본적으로 (oobe 첫 실행 경험)을 선택 hello 일반화 확인란을 선택 **종료**, 클릭 하 고 **확인**hello 이미지 아래에 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="dbe33-248">Sysprep은 hello 운영 체제를 일반화 되 고 hello 시스템 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="dbe33-249">Ubuntu VM에 대 한 사용 virt sysprep tooachieve hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="dbe33-250">자세한 내용은 [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="dbe33-251">참고 항목 일부 hello 오픈 소스 [Linux 서버 프로 비전 소프트웨어](http://www.cyberciti.biz/tips/server-provisioning-software.html) 다른 Linux 운영 체제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="dbe33-252">고유 운영 체제 VHD toocreate 단일 VM 인스턴스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="dbe33-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="dbe33-253">Hello hello 컴퓨터 특정 데이터를 필요로 하는 VM에서 실행 중인 응용 프로그램를 설정한 경우에 VHD hello을 일반화 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="dbe33-254">일반화 되지 않은 VHD를 사용 하는 toocreate 고유한 Azure VM 인스턴스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="dbe33-255">예를들어 VHD에 도메인 컨트롤러가 있는 경우, sysprep를 실행하면 도메인 컨트롤러가 비효율적이게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="dbe33-256">VHD hello을 일반화 하기 전의 sysprep를 실행 중인 VM과 hello 영향을 실행 하는 hello 응용 프로그램을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="dbe33-257">데이터 디스크 VHD 등록</span><span class="sxs-lookup"><span data-stu-id="dbe33-257">Register data disk VHD</span></span>
<span data-ttu-id="dbe33-258">있는 경우 Azure toobe에 데이터 디스크 마이그레이션된를 이러한 데이터 디스크는 종료를 사용 하는 hello Vm 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="dbe33-259">프리미엄 저장소 toocopy VHD tooAzure 아래에 설명 된 hello 단계에 따라 프로 비전 된 데이터 디스크로 등록 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dbe33-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="dbe33-260">2단계.</span><span class="sxs-lookup"><span data-stu-id="dbe33-260">Step 2.</span></span> <span data-ttu-id="dbe33-261">VHD에 대 한 hello 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="dbe33-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="dbe33-262">VHD를 유지 관리하기 위한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="dbe33-263">Hello 지점 위치 계획할 때는 다음 고려 toostore Vhd:</span><span class="sxs-lookup"><span data-stu-id="dbe33-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="dbe33-264">hello 대상 프리미엄 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="dbe33-265">저장소 계정 위치 hello hello 최종 단계에서 만들 프리미엄 저장소 지원 되는 Azure Vm으로 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="dbe33-266">새 저장소 계정을 tooa 또는 필요에 따라 동일한 저장소 계정 계획 toouse hello를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="dbe33-267">복사 하 고 hello 다음 단계에 대 한 hello 대상 저장소 계정의 hello 저장소 계정 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="dbe33-268">데이터 디스크에 대 한 표준 저장소 계정 (예를 들어 디스크 냉각기 저장소에 있는)에 일부 데이터 디스크를 tookeep를 선택할 수 있지만 좋습니다 프로덕션 작업 toouse 프리미엄 저장소에 대 한 모든 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="dbe33-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>3단계.</span><span class="sxs-lookup"><span data-stu-id="dbe33-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="dbe33-270">AzCopy 또는 PowerShell을 사용하여 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="dbe33-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="dbe33-271">컨테이너 경로 저장소 계정 키 tooprocess를 이러한 두 옵션 중 하나 toofind 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="dbe33-272">컨테이너 경로 및 저장소 계정 키는 **Azure Portal** > **저장소**에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="dbe33-273">"https://myaccount.blob.core.windows.net/mycontainer/" hello 컨테이너 URL 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="dbe33-274">옵션 1: AzCopy를 사용하여 VHD 복사(비동기 복사)</span><span class="sxs-lookup"><span data-stu-id="dbe33-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="dbe33-275">AzCopy를 사용 하 여 hello VHD hello 인터넷을 통해 쉽게 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="dbe33-276">Hello Vhd의 hello 크기에 따라 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="dbe33-277">이 옵션을 사용 하는 경우 toocheck hello 저장소 계정 송/수신 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="dbe33-278">자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="dbe33-279">[최신 버전의 AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="dbe33-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="dbe33-280">Azure PowerShell 및 이동 toohello AzCopy를 설치한 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="dbe33-281">사용 하 여 hello 다음 명령에서 "Source" toocopy hello VHD 파일 너무 "Destination"입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="dbe33-282">예제:</span><span class="sxs-lookup"><span data-stu-id="dbe33-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="dbe33-283">Hello AzCopy 명령에에서 사용 되는 hello 매개 변수에 대 한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="dbe33-284">**/ 소스:  *&lt;소스&gt;:***  hello 폴더 또는 hello VHD를 포함 하는 저장소 컨테이너 URL의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="dbe33-285">**/ SourceKey:  *&lt;소스-계정 키&gt;:***  hello 원본 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="dbe33-286">**/ Dest:  *&lt;대상&gt;:***  저장소 컨테이너 URL toocopy hello VHD를 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="dbe33-287">**/ DestKey:  *&lt;dest-계정 키&gt;:***  hello 대상 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="dbe33-288">**/ 패턴:  *&lt;파일 이름&gt;:***  hello VHD toocopy의 hello 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="dbe33-289">AzCopy를 사용 하 여 대 한 자세한 내용은 도구, 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="dbe33-290">옵션 2: PowerShell을 사용하여 VHD 복사(동기 복사)</span><span class="sxs-lookup"><span data-stu-id="dbe33-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="dbe33-291">시작 AzureStorageBlobCopy hello PowerShell cmdlet을 사용 하 여 hello VHD 파일을 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="dbe33-292">Hello Azure PowerShell toocopy VHD에서 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="dbe33-293">원본 및 대상 저장소 계정에서 해당 값을 가진 <> hello 값을 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="dbe33-294">toouse이 명령에 대상 저장소 계정에 vhd를 호출 하는 컨테이너가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="dbe33-295">Hello 컨테이너가 존재 하지 않는 경우 hello 명령을 실행 하기 전에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="dbe33-296">예제:</span><span class="sxs-lookup"><span data-stu-id="dbe33-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="dbe33-297"><a name="scenario2"></a>시나리오 2: "마이그레이션하는 중입니다 Vm에서 다른 플랫폼 tooAzure 프리미엄 저장소."</span><span class="sxs-lookup"><span data-stu-id="dbe33-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="dbe33-298">비 Azure 클라우드 저장소 tooAzure에서 VHD를 마이그레이션하는 경우 먼저 hello VHD tooa 로컬 디렉터리를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="dbe33-299">Hello 로컬 VHD를 저장할 디렉터리를의 전체 소스 경로 hello 있고 다음 tooupload AzCopy를 사용 하 여 그 tooAzure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="dbe33-300">1단계.</span><span class="sxs-lookup"><span data-stu-id="dbe33-300">Step 1.</span></span> <span data-ttu-id="dbe33-301">내보내기 VHD tooa 로컬 디렉터리</span><span class="sxs-lookup"><span data-stu-id="dbe33-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="dbe33-302">AWS에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="dbe33-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="dbe33-303">AWS를 사용 하는 hello EC2 인스턴스 tooa Amazon S3 버킷에서 VHD를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="dbe33-304">Hello Amazon EC2 인스턴스 내보내기 tooinstall hello Amazon EC2 CLI (명령줄 인터페이스) 도구에 대 한 Amazon 설명서에에서 설명 된 hello 단계를 따르고 hello-인스턴스-내보내기-작업 만들기 명령 tooexport hello EC2 인스턴스 tooa VHD 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="dbe33-305">수 있는지 toouse **VHD** hello 디스크 &#95; 이미지 &#95;에 대 한 Hello를 실행 하는 경우 형식 변수 **-인스턴스-내보내기-작업 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="dbe33-306">hello 내보낸된 VHD 파일에에서 저장 됩니다 hello Amazon S3 버킷을 그 과정 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="dbe33-307">Hello S3 버킷을에서 hello VHD 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="dbe33-308">선택 hello VHD 파일에 다음 **동작** > **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="dbe33-309">다른 비-Azure 클라우드에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="dbe33-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="dbe33-310">비 Azure 클라우드 저장소 tooAzure에서 VHD를 마이그레이션하는 경우 먼저 hello VHD tooa 로컬 디렉터리를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="dbe33-311">VHD를 저장할 로컬 디렉터리 hello의 hello 전체 소스 경로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="dbe33-312">온-프레미스에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="dbe33-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="dbe33-313">온-프레미스 환경에서 VHD를 마이그레이션하는 hello 전체 소스 경로 VHD 저장 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="dbe33-314">hello 소스 경로 서버 위치 또는 파일 공유를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="dbe33-315">2단계.</span><span class="sxs-lookup"><span data-stu-id="dbe33-315">Step 2.</span></span> <span data-ttu-id="dbe33-316">VHD에 대 한 hello 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="dbe33-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="dbe33-317">VHD를 유지 관리하기 위한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="dbe33-318">Hello 지점 위치 계획할 때는 다음 고려 toostore Vhd:</span><span class="sxs-lookup"><span data-stu-id="dbe33-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="dbe33-319">hello 대상 저장소 계정에는 응용 프로그램 요구 사항에 따라 표준 또는 프리미엄 저장소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="dbe33-320">저장소 계정 지역이 hello hello 최종 단계에서 만들 프리미엄 저장소 지원 되는 Azure Vm으로 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="dbe33-321">새 저장소 계정을 tooa 또는 필요에 따라 동일한 저장소 계정 계획 toouse hello를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="dbe33-322">복사 하 고 hello 다음 단계에 대 한 hello 대상 저장소 계정의 hello 저장소 계정 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="dbe33-323">이 프로덕션 작업 toouse 프리미엄 저장소에 대 한 모든 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="dbe33-324">3단계.</span><span class="sxs-lookup"><span data-stu-id="dbe33-324">Step 3.</span></span> <span data-ttu-id="dbe33-325">Hello VHD tooAzure 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="dbe33-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="dbe33-326">Hello 로컬 디렉터리에 VHD를가지고 AzCopy 또는 AzurePowerShell tooupload hello.vhd 파일 tooAzure 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="dbe33-327">두 가지 업로드 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="dbe33-328">Azure PowerShell Add-azurevhd tooupload hello.vhd 파일을 사용 하 여 옵션 1:</span><span class="sxs-lookup"><span data-stu-id="dbe33-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="dbe33-329"><Uri>의 예로 ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="dbe33-330"><FileInfo>의 예로 ***"C:\path\to\upload.vhd"***를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="dbe33-331">AzCopy tooupload hello.vhd 파일을 사용 하 여 옵션 2:</span><span class="sxs-lookup"><span data-stu-id="dbe33-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="dbe33-332">AzCopy를 사용 하 여 hello VHD hello 인터넷을 통해 쉽게 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="dbe33-333">Hello Vhd의 hello 크기에 따라 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="dbe33-334">이 옵션을 사용 하는 경우 toocheck hello 저장소 계정 송/수신 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="dbe33-335">자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="dbe33-336">[최신 버전의 AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="dbe33-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="dbe33-337">Azure PowerShell 및 이동 toohello AzCopy를 설치한 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="dbe33-338">사용 하 여 hello 다음 명령에서 "Source" toocopy hello VHD 파일 너무 "Destination"입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="dbe33-339">예제:</span><span class="sxs-lookup"><span data-stu-id="dbe33-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="dbe33-340">Hello AzCopy 명령에에서 사용 되는 hello 매개 변수에 대 한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="dbe33-341">**/ 소스:  *&lt;소스&gt;:***  hello 폴더 또는 hello VHD를 포함 하는 저장소 컨테이너 URL의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="dbe33-342">**/ SourceKey:  *&lt;소스-계정 키&gt;:***  hello 원본 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="dbe33-343">**/ Dest:  *&lt;대상&gt;:***  저장소 컨테이너 URL toocopy hello VHD를 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="dbe33-344">**/ DestKey:  *&lt;dest-계정 키&gt;:***  hello 대상 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="dbe33-345">**/ BlobType: 페이지:** hello 대상 연결 되는 페이지 blob을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="dbe33-346">**/ 패턴:  *&lt;파일 이름&gt;:***  hello VHD toocopy의 hello 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="dbe33-347">AzCopy를 사용 하 여 대 한 자세한 내용은 도구, 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="dbe33-348">VHD를 업로드하기 위한 기타 옵션</span><span class="sxs-lookup"><span data-stu-id="dbe33-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="dbe33-349">Hello 방법을 다음 중 하나를 사용 하 여 VHD tooyour 저장소 계정을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="dbe33-350">Azure 저장소 Blob 복사 API</span><span class="sxs-lookup"><span data-stu-id="dbe33-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="dbe33-351">Azure Storage 탐색기 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="dbe33-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="dbe33-352">저장소 가져오기/내보내기 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="dbe33-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="dbe33-353">예상 업로드 시간이 7일보다 긴 경우 가져오기/내보내기 서비스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="dbe33-354">사용할 수 있습니다 [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) 데이터 크기와 전송 단위에서 tooestimate hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="dbe33-355">가져오기/내보내기 수 toocopy tooa 표준 저장소 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="dbe33-356">AzCopy와 같은 도구를 사용 하 여 표준 저장소 toopremium 저장소 계정에서 toocopy가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="dbe33-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Premium Storage를 사용하여 Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="dbe33-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="dbe33-358">Hello VHD를 업로드 또는 복사 toohello 원하는 저장소 계정으로 운영 체제 이미지 또는 운영 체제 디스크 시나리오에 따라이 섹션 tooregister hello VHD의에서 hello 지침을 따릅니다 한 다음 여기에서 VM 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="dbe33-359">hello 데이터 디스크 VHD 수 첨부 toohello VM 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="dbe33-360">예제 마이그레이션 스크립트는이 섹션의 hello 끝에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="dbe33-361">이 간단한 스크립트가 모든 시나리오에 적합한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="dbe33-362">특정 시나리오와 tooupdate hello 스크립트 toomatch를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="dbe33-363">이 스크립트는 tooyour 시나리오를 적용 하는 경우 toosee 아래를 참조 [A 예제 마이그레이션 스크립트](#a-sample-migration-script)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="dbe33-364">검사 목록</span><span class="sxs-lookup"><span data-stu-id="dbe33-364">Checklist</span></span>
1. <span data-ttu-id="dbe33-365">모든 hello VHD 디스크 복사 될 때까지 대기 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="dbe33-366">프리미엄 저장소를 마이그레이션하는 hello 지역에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="dbe33-367">사용 하려는 hello 새 VM 시리즈를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="dbe33-368">프리미엄 저장소를 사용할 수 있어야 하 고 hello 영역의 hello 가용성에 따라 및 사용자 요구에 따라 hello 크기 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="dbe33-369">사용 하 여 hello 정확한 VM 크기를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="dbe33-370">VM 크기에 있는 데이터 디스크 개수 충분히 큰 toosupport hello toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="dbe33-371">예:</span><span class="sxs-lookup"><span data-stu-id="dbe33-371">E.g.</span></span> <span data-ttu-id="dbe33-372">4 개의 데이터 디스크가 있는 경우 hello VM 2 개 이상의 코어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="dbe33-373">또한 처리 능력, 메모리 및 네트워크 대역폭 요구 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="dbe33-374">Hello 대상 지역에서 프리미엄 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="dbe33-375">이 계정이 hello hello에 대 한 사용 하 여 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="dbe33-376">정보 포함 하 고 hello 현재 VM 디스크 및 해당 VHD blob hello 목록을 포함 하 여 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="dbe33-377">응용 프로그램의 가동 중지 시간을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-377">Prepare your application for downtime.</span></span> <span data-ttu-id="dbe33-378">클린 마이그레이션 toodo toostop 모든 hello 처리는 hello 현재 시스템에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="dbe33-379">경우에 표시할 수 있습니다 마이그레이션할 수 없는 tooconsistent 상태 toohello 새 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="dbe33-380">작동 중단 기간 hello 디스크 toomigrate의 데이터 양을 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe33-381">특수 한 VHD 디스크에서 Azure 리소스 관리자 VM을 만드는 경우를 참조 하십시오 너무[이 서식 파일](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) 기존 디스크를 사용 하 여 리소스 관리자 VM을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="dbe33-382">장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-382">Register your VHD</span></span>
<span data-ttu-id="dbe33-383">운영 체제 VHD 또는 데이터 디스크 tooa tooattach에서 VM toocreate 새 VM을 먼저 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="dbe33-384">VHD 시나리오에 따라 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="dbe33-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="dbe33-385">운영 체제 VHD toocreate 여러 Azure VM 인스턴스 일반화</span><span class="sxs-lookup"><span data-stu-id="dbe33-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="dbe33-386">VHD는 운영 체제 이미지를 일반화 된 toohello 저장소 계정을 업로드 후 등록로 **Azure VM 이미지** 에서 하나 이상의 VM 인스턴스를 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="dbe33-387">Azure VM의 OS 이미지 형식으로 다음 PowerShell cmdlet tooregister hello VHD를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="dbe33-388">VHD 복사 된 위치의 hello 전체 컨테이너 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="dbe33-389">복사 하 고이 새 Azure VM 이미지의 hello 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="dbe33-390">위의 hello 예제 *OSImageName*합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="dbe33-391">고유 운영 체제 VHD toocreate 단일 Azure VM 인스턴스</span><span class="sxs-lookup"><span data-stu-id="dbe33-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="dbe33-392">Hello 후 고유 운영 체제 VHD는 업로드 된 toohello 저장소 계정로 등록 한 **Azure OS 디스크** 에서 VM 인스턴스를 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="dbe33-393">Azure OS 디스크로 이러한 PowerShell cmdlet tooregister VHD를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="dbe33-394">VHD 복사 된 위치의 hello 전체 컨테이너 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="dbe33-395">복사 하 고이 새 Azure 운영 체제 디스크의 hello 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="dbe33-396">위의 hello 예제 *OSDisk*합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="dbe33-397">데이터 디스크 VHD toobe toonew Azure VM 인스턴스 연결</span><span class="sxs-lookup"><span data-stu-id="dbe33-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="dbe33-398">Hello 데이터 디스크 VHD가 업로드 후 toostorage 계정으로 등록 된 Azure 데이터 디스크 연결된 tooyour 수 있도록 새 DS 시리즈, DSv2 시리즈 또는 GS 시리즈 Azure VM 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="dbe33-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="dbe33-399">Azure 데이터 디스크와 이러한 PowerShell cmdlet tooregister VHD를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="dbe33-400">VHD 복사 된 위치의 hello 전체 컨테이너 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="dbe33-401">복사 하 고이 새 Azure 데이터 디스크의 hello 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="dbe33-402">위의 hello 예제 *DataDisk*합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="dbe33-403">Premium Storage 지원 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="dbe33-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="dbe33-404">새 DS 시리즈, DSv2 시리즈 또는 GS 시리즈 VM 만들기, 운영 체제 이미지를 한 번 hello 또는 OS 디스크로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="dbe33-405">사용 하려는 hello 운영 체제 이미지 또는 운영 체제 디스크 이름을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="dbe33-406">Hello 프리미엄 저장소 계층에서 hello VM 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="dbe33-407">아래 예제에서 사용 하 여 hello *Standard_DS2* VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe33-408">Hello 디스크 크기 toomake 용량 및 성능 요구 사항 및 hello 사용 가능한 Azure 디스크 크기와 일치 하는지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="dbe33-409">Toocreate 아래에 따라 hello 단계별 PowerShell cmdlet에는 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="dbe33-410">먼저, hello 공통 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="dbe33-411">먼저, 클라우드 서비스를 호스트할 새 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="dbe33-412">다음으로 시나리오에 따라 hello Azure VM 인스턴스를 hello 운영 체제 이미지 또는 등록 OS 디스크를에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="dbe33-413">운영 체제 VHD toocreate 여러 Azure VM 인스턴스 일반화</span><span class="sxs-lookup"><span data-stu-id="dbe33-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="dbe33-414">Hello 하나 이상의 새 인스턴스를 만들고 DS 시리즈 Azure VM hello를 사용 하 여 **Azure OS 이미지** 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="dbe33-415">아래와 같이 새 VM을 만들 때이 OS 이미지 이름을 hello VM 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="dbe33-416">고유 운영 체제 VHD toocreate 단일 Azure VM 인스턴스</span><span class="sxs-lookup"><span data-stu-id="dbe33-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="dbe33-417">Hello를 사용 하 여 새 DS 시리즈 Azure VM 인스턴스를 만들고 **Azure OS 디스크** 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="dbe33-418">아래와 같이 새 VM을 hello 만들 때이 OS 디스크 이름은 hello VM 구성에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="dbe33-419">클라우드 서비스, 지역, 저장소 계정, 가용성 집합 및 캐싱 정책 등의 기타 Azure VM 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="dbe33-420">Note hello VM 인스턴스는 관련 된 운영 체제와 함께 배치 해야 합니다. 또는 데이터 디스크를 선택 하는 hello 클라우드 서비스, 지역 및 저장소 계정 모두에 있어야 하므로 hello hello 기본 해당 디스크의 Vhd와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="dbe33-421">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="dbe33-421">Attach data disk</span></span>
<span data-ttu-id="dbe33-422">마지막으로 등록 한 경우 데이터 디스크 Vhd로 toohello 첨부할 새로운 프리미엄 저장소 지원 Azure VM입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="dbe33-423">다음 PowerShell cmdlet tooattach 데이터 디스크 toohello 사용 하 여 새 VM hello 캐싱 정책을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="dbe33-424">Hello 아래 예에서 캐싱 정책은 설정 되어 너무*ReadOnly*합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="dbe33-425">추가 단계가 필요한 toosupport 있을 수 있는 응용 프로그램에서 다룰 수 없는이 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="dbe33-426">확인 및 백업 계획</span><span class="sxs-lookup"><span data-stu-id="dbe33-426">Checking and plan backup</span></span>
<span data-ttu-id="dbe33-427">동일한 로그인 id와 암호를 사용 하 여 hello 액세스 실행 되 고 새 VM이 위쪽 hello 한 번 hello 원본 VM으로 이며 모든 항목이 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="dbe33-428">Hello 스트라이프 볼륨을 포함 한 모든 hello 설정에 제공 됩니다. 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="dbe33-429">hello 마지막 단계는 새 VM hello 응용 프로그램의 요구 사항에 따라 hello에 대 한 tooplan 백업 및 유지 관리 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="dbe33-430"><a name="a-sample-migration-script"></a>샘플 마이그레이션 스크립트</span><span class="sxs-lookup"><span data-stu-id="dbe33-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="dbe33-431">여러 Vm toomigrate를 설정한 경우에 PowerShell 스크립트를 통해 자동화 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="dbe33-432">다음은 VM의 hello 마이그레이션을 자동화 하는 샘플 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="dbe33-433">참고는 아래 스크립트는 하나의 예 되며 hello 현재 VM 디스크에 대 한 몇 가지 가정을 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="dbe33-434">특정 시나리오와 tooupdate hello 스크립트 toomatch를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="dbe33-435">hello 가정은:</span><span class="sxs-lookup"><span data-stu-id="dbe33-435">hello assumptions are:</span></span>

* <span data-ttu-id="dbe33-436">클래식 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="dbe33-437">원본 OS 디스크와 원본 데이터 디스크가 동일한 저장소 계정 및 동일한 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="dbe33-438">OS 디스크 및 데이터 디스크에 없는 경우 동일한 hello를 저장소 계정 및 컨테이너를 통해 AzCopy 또는 Azure PowerShell toocopy Vhd를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="dbe33-439">Toohello 이전 단계를 참조 하십시오: [AzCopy 또는 PowerShell 복사 VHD](#copy-vhd-with-azcopy-or-powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="dbe33-440">이 스크립트 toomeet 편집 시나리오에는 다른 선택 하지만 더 쉽고 빠르게 이후 AzCopy 또는 PowerShell을 사용 하 여는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="dbe33-441">hello 자동화 스크립트는 아래에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-441">hello automation script is provided below.</span></span> <span data-ttu-id="dbe33-442">특정 시나리오를 hello 스크립트 toomatch 업데이트 및 사용자 정보로 텍스트를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe33-443">Hello 기존 스크립트를 사용 하 여 원본 VM의 네트워크 구성을 hello 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="dbe33-444">마이그레이션된 Vm에 toore-config hello 네트워킹 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="dbe33-445"><a name="optimization"></a>최적화</span><span class="sxs-lookup"><span data-stu-id="dbe33-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="dbe33-446">현재 VM 구성을 사용자 지정할 수 있습니다 표준 디스크와 잘 toowork 특히 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="dbe33-447">예를 들어, tooincrease hello 성능 스트라이프 볼륨에서 많은 디스크를 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="dbe33-448">예를 들어, 프리미엄 저장소에 개별적으로 4 개를 사용 하는 대신 단일 디스크를 포함 하면 수 toooptimize hello 비용을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="dbe33-449">최적화 등이 필요 toobe 상황별으로에서 처리 및 hello 마이그레이션 후 사용자 지정 단계를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="dbe33-450">또한, 이때 데이터베이스 및 hello 설치에 정의 된 hello 디스크 레이아웃에 의존 하는 응용 프로그램에 대 한이 프로세스 제대로 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="dbe33-451">준비</span><span class="sxs-lookup"><span data-stu-id="dbe33-451">Preparation</span></span>
1. <span data-ttu-id="dbe33-452">전체 hello hello에 설명 된 대로 간단한 마이그레이션을 이전 섹션.</span><span class="sxs-lookup"><span data-stu-id="dbe33-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="dbe33-453">Hello 최적화가 수행 될 됩니다 hello 마이그레이션 후 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="dbe33-454">최적화 된 hello 구성 필요한 hello 새 디스크 크기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="dbe33-455">현재 디스크/볼륨 toohello hello 새 디스크 사양의 매핑을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="dbe33-456">실행 단계</span><span class="sxs-lookup"><span data-stu-id="dbe33-456">Execution steps</span></span>
1. <span data-ttu-id="dbe33-457">프리미엄 저장소 VM hello에 hello 적절 한 크기와 hello 새 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="dbe33-458">로그인 toohello VM 및 복사 hello 데이터 hello 현재 볼륨 toohello 새 디스크 toothat 볼륨을 매핑하는입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="dbe33-459">Toomap tooa 새 디스크를 필요로 하는 모든 hello 현재 볼륨에 대해이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="dbe33-460">Hello 응용 프로그램 설정 tooswitch toohello 새 디스크를 바꾼 다음으로 hello 이전 볼륨을 분리 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dbe33-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="dbe33-461">디스크 성능 향상을 위해 hello 응용 프로그램 튜닝을 참조 하십시오 너무[응용 프로그램 성능 최적화](storage-premium-storage-performance.md#optimizing-application-performance)합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="dbe33-462">응용 프로그램 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="dbe33-462">Application migrations</span></span>
<span data-ttu-id="dbe33-463">데이터베이스 및 기타 복잡 한 응용 프로그램 hello 마이그레이션에 대 한 hello 응용 프로그램 공급자에 의해 정의 된 특별 한 단계가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="dbe33-464">Toorespective 응용 프로그램 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dbe33-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="dbe33-465">예:</span><span class="sxs-lookup"><span data-stu-id="dbe33-465">E.g.</span></span> <span data-ttu-id="dbe33-466">일반적으로 백업 및 복원을 통해 데이터베이스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbe33-467">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dbe33-467">Next steps</span></span>
<span data-ttu-id="dbe33-468">Hello 다음 가상 컴퓨터 마이그레이션에 대 한 특정 시나리오에 대 한 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dbe33-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="dbe33-469">저장소 계정 간에 Azure 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="dbe33-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="dbe33-470">만들고 Windows Server VHD tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="dbe33-471">만들고 해당 Contains hello Linux 운영 체제 가상 하드 디스크를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe33-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="dbe33-472">AWS Amazon tooMicrosoft Azure에서에서 가상 컴퓨터를 마이그레이션하거나</span><span class="sxs-lookup"><span data-stu-id="dbe33-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="dbe33-473">또한, 다음 Azure 저장소 및 Azure 가상 컴퓨터에 대 한 자세한 리소스 toolearn hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dbe33-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="dbe33-474">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="dbe33-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="dbe33-475">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="dbe33-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="dbe33-476">프리미엄 저장소: Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소</span><span class="sxs-lookup"><span data-stu-id="dbe33-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
