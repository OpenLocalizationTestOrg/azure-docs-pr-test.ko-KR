---
title: "VM을 Azure Premium Storage로 마이그레이션 | Microsoft Docs"
description: "기존 VM을 Azure Premium Storage로 마이그레이션합니다. 프리미엄 저장소는 Azure 가상 컴퓨터에서 실행되는 I/O 사용량이 많은 작업에 대해 대기 시간이 짧은 고성능 디스크 지원을 제공합니다."
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
ms.openlocfilehash: 645b37fff2dd6a12114719bac66a937cf8e8ffaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="3f799-104">Azure Premium Storage로 마이그레이션(관리되지 않는 디스크)</span><span class="sxs-lookup"><span data-stu-id="3f799-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="3f799-105">이 문서는 관리되지 않는 표준 디스크를 사용하는 VM을 관리되지 않는 프리미엄 디스크를 사용하는 VM으로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="3f799-106">새 VM에 Azure Managed Disks를 사용하고 이전의 관리되지 않은 디스크를 Managed Disks로 변환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="3f799-107">Managed Disks에서 내부 저장소 계정을 처리해 주기 때문에 사용자가 처리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="3f799-108">자세한 내용은 [Managed Disks 개요](storage-managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="3f799-109">Azure 프리미엄 저장소는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="3f799-110">응용 프로그램의 VM 디스크를 Azure Premium Storage로 마이그레이션하여 이러한 디스크의 속도와 성능 혜택을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="3f799-111">이 가이드의 목적은 Azure 프리미엄 저장소를 처음 사용하는 사용자가 현재 시스템에서 프리미엄 저장소로 원활한 전환이 가능하도록 돕는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="3f799-112">이 가이드에서는 이 프로세스의 세 가지 주요 구성 요소를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="3f799-113">Premium Storage로 마이그레이션 계획 수립</span><span class="sxs-lookup"><span data-stu-id="3f799-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="3f799-114">VHD(가상 하드 디스크)를 준비하여 Premium Storage로 복사</span><span class="sxs-lookup"><span data-stu-id="3f799-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="3f799-115">Premium Storage를 사용하여 Azure 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="3f799-116">VM을 다른 플랫폼에서 Azure Premium Storage로 마이그레이션할 수도 있고 기존 Azure VM을 표준 저장소에서 Premium Storage로 마이그레이션할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="3f799-117">이 가이드에서는 두 시나리오의 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="3f799-118">시나리오에 따라 관련 섹션에 지정된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="3f799-119">Premium Storage의 기능 개요 및 가격 책정은 Premium Storage: [Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소](storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="3f799-120">응용 프로그램이 최고 성능을 낼 수 있도록 높은 IOPS가 필요한 모든 가상 컴퓨터 디스크를 Azure 프리미엄 디스크로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="3f799-121">디스크에 높은 IOPS가 필요하지 않은 경우, 가상 컴퓨터 디스크 데이터를 SSD가 아닌 하드 디스크 드라이브(HDD)에 저자하는 표준 저장소를 사용하여 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="3f799-122">전체 마이그레이션 프로세스를 완료하기 위해서는 이 가이드에 제공된 단계 전과 후에 추가 작업이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="3f799-123">이러한 작업의 예로는 가상 네트워크 또는 끝점을 구성하거나 응용 프로그램 자체 내에서 코드를 변경하는 것이 포함되며 이러한 작업은 응용 프로그램에서 약간의 가동 중지 시간이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="3f799-124">이러한 작업은 각 응용 프로그램에 대해 고유하며 Premium Storage로 가능한 한 원활하게 완전히 전환하기 위해서는 이 가이드에 제공된 단계에 따라 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="3f799-125"><a name="plan-the-migration-to-premium-storage"></a>Premium Storage로 마이그레이션 계획 수립</span><span class="sxs-lookup"><span data-stu-id="3f799-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="3f799-126">이 섹션은 이 문서의 마이그레이션 단계를 수행할 준비를 하고 가장 적합한 VM 및 디스크 유형을 선택할 수 있도록 도와주기 위한 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3f799-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3f799-127">Prerequisites</span></span>
* <span data-ttu-id="3f799-128">Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-128">You will need an Azure subscription.</span></span> <span data-ttu-id="3f799-129">구독이 없다면, 한 달의 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 구독하거나 [Azure 가격 책정](https://azure.microsoft.com/pricing/)을 방문하여 추가 옵션을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="3f799-130">PowerShell cmdlet을 실행하려면 Microsoft Azure PowerShell 모듈이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="3f799-131">설치 지점 및 설치 지침에 대해서는 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="3f799-132">Premium Storage에서 실행되는 Azure VM을 사용하려는 경우 Premium Storage 지원 VM을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="3f799-133">Premium Storage 지원 VM에서 표준 저장소 디스크와 Premium Storage 디스크를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="3f799-134">프리미엄 저장소 디스크를 나중에 더 많은 VM 형식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="3f799-135">사용 가능한 Azure VM 디스크 유형 및 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [클라우드 서비스 크기](../cloud-services/cloud-services-sizes-specs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="3f799-136">고려 사항</span><span class="sxs-lookup"><span data-stu-id="3f799-136">Considerations</span></span>
<span data-ttu-id="3f799-137">Azure VM은 여러 Premium Storage 디스크의 연결을 지원하므로 응용 프로그램이 VM당 최대 256TB의 저장소를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="3f799-138">프리미엄 저장소를 사용할 경우 읽기 작업의 대기 시간이 매우 짧은 상태로 VM당 80,000 IOPS(초당 입/출력 작업 수) 및 VM당 디스크 처리량 초당 2000MB를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="3f799-139">다양한 VM 및 디스크 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="3f799-140">이 섹션은 워크로드에 가장 적합한 옵션을 찾을 수 있도록 도와주기 위해 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="3f799-141">VM 크기</span><span class="sxs-lookup"><span data-stu-id="3f799-141">VM sizes</span></span>
<span data-ttu-id="3f799-142">Azure VM 크기 사양은 [가상 컴퓨터의 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3f799-143">프리미엄 저장소와 작동하는 가상 컴퓨터의 성능 특징을 검토하고 워크로드에 가장 적합한 VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="3f799-144">VM에서 디스크 트래픽을 제어하기에 충분한 대역폭을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="3f799-145">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="3f799-145">Disk sizes</span></span>
<span data-ttu-id="3f799-146">VM에서 사용할 수 있는 디스크에는 다섯 종류가 있으며 각 종류에는 특정 IOP 및 처리량 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="3f799-147">용량, 성능, 확장성 및 최대 로드 측면에서 응용 프로그램의 필요에 따라 VM에 대한 디스크 유형을 선택할 때 이 제한을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="3f799-148">프리미엄 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="3f799-148">Premium Disks Type</span></span>  | <span data-ttu-id="3f799-149">P10</span><span class="sxs-lookup"><span data-stu-id="3f799-149">P10</span></span>   | <span data-ttu-id="3f799-150">P20</span><span class="sxs-lookup"><span data-stu-id="3f799-150">P20</span></span>   | <span data-ttu-id="3f799-151">P30</span><span class="sxs-lookup"><span data-stu-id="3f799-151">P30</span></span>            | <span data-ttu-id="3f799-152">P40</span><span class="sxs-lookup"><span data-stu-id="3f799-152">P40</span></span>            | <span data-ttu-id="3f799-153">P50</span><span class="sxs-lookup"><span data-stu-id="3f799-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="3f799-154">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="3f799-154">Disk size</span></span>           | <span data-ttu-id="3f799-155">128GB</span><span class="sxs-lookup"><span data-stu-id="3f799-155">128 GB</span></span>| <span data-ttu-id="3f799-156">512GB</span><span class="sxs-lookup"><span data-stu-id="3f799-156">512 GB</span></span>| <span data-ttu-id="3f799-157">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="3f799-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="3f799-158">2,048GB(2TB)</span><span class="sxs-lookup"><span data-stu-id="3f799-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="3f799-159">4,095GB(4TB)</span><span class="sxs-lookup"><span data-stu-id="3f799-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="3f799-160">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="3f799-160">IOPS per disk</span></span>       | <span data-ttu-id="3f799-161">500</span><span class="sxs-lookup"><span data-stu-id="3f799-161">500</span></span>   | <span data-ttu-id="3f799-162">2,300</span><span class="sxs-lookup"><span data-stu-id="3f799-162">2300</span></span>  | <span data-ttu-id="3f799-163">5,000</span><span class="sxs-lookup"><span data-stu-id="3f799-163">5000</span></span>           | <span data-ttu-id="3f799-164">7,500</span><span class="sxs-lookup"><span data-stu-id="3f799-164">7500</span></span>           | <span data-ttu-id="3f799-165">7,500</span><span class="sxs-lookup"><span data-stu-id="3f799-165">7500</span></span>           | 
| <span data-ttu-id="3f799-166">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="3f799-166">Throughput per disk</span></span> | <span data-ttu-id="3f799-167">초당 100MB</span><span class="sxs-lookup"><span data-stu-id="3f799-167">100 MB per second</span></span> | <span data-ttu-id="3f799-168">초당 150MB</span><span class="sxs-lookup"><span data-stu-id="3f799-168">150 MB per second</span></span> | <span data-ttu-id="3f799-169">초당 200MB</span><span class="sxs-lookup"><span data-stu-id="3f799-169">200 MB per second</span></span> | <span data-ttu-id="3f799-170">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="3f799-170">250 MB per second</span></span> | <span data-ttu-id="3f799-171">초당 250MB</span><span class="sxs-lookup"><span data-stu-id="3f799-171">250 MB per second</span></span> |

<span data-ttu-id="3f799-172">사용자 워크로드에 따라 추가 데이터 디스크가 VM에 필요한 경우를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="3f799-173">VM에 여러 영구 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="3f799-174">필요한 경우, 볼륨의 성능과 용량을 늘리도록 디스크에 걸쳐 스트라이핑 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="3f799-175">(디스크 스트라이프란 무엇인지 [여기서](storage-premium-storage-performance.md#disk-striping) 확인하세요.) [저장소 공간][4]을 사용하여 프리미엄 저장소 데이터 디스크를 스트라이프하는 경우, 사용되는 각 디스크에 대해 하나의 열로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="3f799-176">그렇지 않으면 디스크에 트래픽이 고르게 분배되지 않아 스트라이프 볼륨의 전반적인 성능이 예상보다 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="3f799-177">Linux VM의 경우 *mdadm* 유틸리티를 사용하여 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="3f799-178">자세한 내용은 [Linux에서 소프트웨어 RAID 구성](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="3f799-179">저장소 계정의 확장성 목표</span><span class="sxs-lookup"><span data-stu-id="3f799-179">Storage account scalability targets</span></span>
<span data-ttu-id="3f799-180">Premium Storage 계정에는 [Azure Storage 확장성 및 성능 목표](storage-scalability-targets.md) 이외에 다음 확장성 목표가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="3f799-181">응용 프로그램의 요구가 단일 저장소 계정의 확장성 목표를 초과하는 경우, 여러 저장소 계정을 사용하도록 응용 프로그램을 빌드하고 데이터를 이러한 저장소 계정에 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="3f799-182">총 계정 용량</span><span class="sxs-lookup"><span data-stu-id="3f799-182">Total Account Capacity</span></span> | <span data-ttu-id="3f799-183">로컬 중복 저장소 계정의 총 대역폭</span><span class="sxs-lookup"><span data-stu-id="3f799-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="3f799-184">디스크 용량: 35TB</span><span class="sxs-lookup"><span data-stu-id="3f799-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="3f799-185">스냅숏 용량: 10TB</span><span class="sxs-lookup"><span data-stu-id="3f799-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="3f799-186">인바운드+아웃바운드에 대해 초당 최대 50기가비트</span><span class="sxs-lookup"><span data-stu-id="3f799-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="3f799-187">프리미엄 저장소 사양에 대한 자세한 내용은 [Premium Storage를 사용하는 경우 확장성 및 성능 목표](storage-premium-storage.md#scalability-and-performance-targets)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="3f799-188">디스크 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="3f799-188">Disk caching policy</span></span>
<span data-ttu-id="3f799-189">기본적으로 디스크 캐싱 정책은 VM에 연결된 프리미엄 운영 체제 디스크에 대한 *읽기 / 쓰기* 및 모든 프리미엄 데이터 디스크에 대한 *읽기 전용*입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="3f799-190">응용 프로그램의 IO에 대한 최적의 성능을 얻으려면 이 구성 설정이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="3f799-191">쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="3f799-192">[Azure Portal](https://portal.azure.com) 또는 *Set-AzureDataDisk* cmdlet의 *-HostCaching* 매개 변수를 사용하여 기존 데이터 디스크에 대한 캐시 설정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="3f799-193">위치</span><span class="sxs-lookup"><span data-stu-id="3f799-193">Location</span></span>
<span data-ttu-id="3f799-194">Azure 프리미엄 저장소를 사용할 수 있는 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="3f799-195">사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="3f799-196">VM에 대한 디스크를 저장하는 저장소 계정과 동일한 지역에 있는 VM은 별도 영역에 있는 경우보다 훨씬 우수한 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="3f799-197">기타 Azure VM 구성 설정</span><span class="sxs-lookup"><span data-stu-id="3f799-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="3f799-198">Azure VM을 만들 때 특정 VM 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="3f799-199">나중에 다른 설정을 수정하거나 추가할 수 있지만 몇 가지 설정은 VM의 수명 동안 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="3f799-200">이러한 Azure VM 구성 설정을 검토 하고 워크로드 부하 요구 사항과 일치하도록 적절하게 구성되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="3f799-201">최적화</span><span class="sxs-lookup"><span data-stu-id="3f799-201">Optimization</span></span>
<span data-ttu-id="3f799-202">[Azure Premium Storage: 고성능을 위한 설계](storage-premium-storage-performance.md) Azure Premium Storage를 사용하여 고성능 응용 프로그램을 구축하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="3f799-203">응용 프로그램에서 사용되는 기술에 적용 가능한 성능 모범 사례가 결합된 지침을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="3f799-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>VHD(가상 하드 디스크)를 준비하여 Premium Storage로 복사</span><span class="sxs-lookup"><span data-stu-id="3f799-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="3f799-205">다음 섹션에서는 VM에서 VHD를 준비하여 Azure Storage에 VHD를 복사하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="3f799-206">시나리오 1: "기존 Azure VM을 Azure Premium Storage로 마이그레이션하려 합니다."</span><span class="sxs-lookup"><span data-stu-id="3f799-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="3f799-207">시나리오 2: "다른 플랫폼에서 Azure Premium Storage로 VM을 마이그레이션하려 합니다."</span><span class="sxs-lookup"><span data-stu-id="3f799-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="3f799-208">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3f799-208">Prerequisites</span></span>
<span data-ttu-id="3f799-209">마이그레이션에 사용할 VHD를 준비하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="3f799-210">Azure 구독, 저장소 계정 및 VHD를 복사할 수 있는 저장소 계정의 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="3f799-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="3f799-211">요구 사항에 따라 대상 저장소 계정은 표준 또는 프리미엄 저장소 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="3f799-212">여러 VM 인스턴스를 만들 계획인 경우 VHD를 일반화하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="3f799-213">예를 들어 Ubuntu용 virt-sysprep 또는 Windows용 sysprep입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="3f799-214">VHD 파일을 저장소 계정에 업로드하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="3f799-215">[AzCopy 명령줄 유틸리티로 데이터 전송](storage-use-azcopy.md)을 참조하거나 [Azure Storage 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="3f799-216">이 가이드는 AzCopy 도구를 사용하여 VHD 복사를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="3f799-217">AzCopy를 사용한 동기 복사 옵션을 선택하는 경우 최적의 성능을 위해 대상 저장소 계정과 동일한 지역에 있는 Azure VM에서 이러한 도구 중 하나를 실행하여 VHD를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="3f799-218">다른 지역에는 Azure VM에서 VHD를 복사 하는 경우 성능이 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="3f799-219">대역폭이 제한된 많은 양의 데이터를 복사하는 경우 [Azure 가져오기/내보내기 서비스를 사용하여 Blob Storage로 데이터 전송](storage-import-export-service.md)을 사용하는 것이 좋습니다. 이렇게 하면 디스크 드라이브를 Azure 데이터 센터에 전달하여 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="3f799-220">가져오기/내보내기 서비스를 사용하여 표준 저장소 계정에만 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="3f799-221">데이터가 표준 저장소 계정에 있는 경우 [Blob API 복사](https://msdn.microsoft.com/library/azure/dd894037.aspx) 또는 AzCopy를 사용하여 Premium Storage 계정에 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="3f799-222">Microsoft Azure는 고정된 크기의 VHD 파일만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="3f799-223">동적 VHD 또는 VHDX 파일은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="3f799-224">동적 VHD를 설정한 경우 [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet을 사용하여 고정된 크기를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="3f799-225"><a name="scenario1"></a>시나리오 1: "기존 Azure VM을 Azure Premium Storage로 마이그레이션하려 합니다."</span><span class="sxs-lookup"><span data-stu-id="3f799-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="3f799-226">기존 Azure VM을 마이그레이션하는 경우 VM을 중지하고, 원하는 VHD 유형마다 VHD를 준비하고, AzCopy 또는 PowerShell을 사용하여 VHD를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="3f799-227">깨끗한 상태로 마이그레이션하려면 VM을 완전히 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="3f799-228">마이그레이션이 완료될 때까지 가동 중지 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="3f799-229">1단계.</span><span class="sxs-lookup"><span data-stu-id="3f799-229">Step 1.</span></span> <span data-ttu-id="3f799-230">마이그레이션할 VHD를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="3f799-231">기존 Azure VM을 Premium Storage로 마이그레이션하려는 경우 VHD가 다음일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="3f799-232">일반화된 운영 체제 이미지</span><span class="sxs-lookup"><span data-stu-id="3f799-232">A generalized operating system image</span></span>
* <span data-ttu-id="3f799-233">고유의 운영 체제 디스크</span><span class="sxs-lookup"><span data-stu-id="3f799-233">A unique operating system disk</span></span>
* <span data-ttu-id="3f799-234">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="3f799-234">A data disk</span></span>

<span data-ttu-id="3f799-235">아래에서는 VHD를 준비하기 위한 3가지 시나리오를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="3f799-236">일반화된 운영 체제 VHD를 사용하여 여러 VM 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="3f799-237">여러 일반 Azure VM 인스턴스를 만드는데 사용할 VHD를 업로드하는 경우 , sysprep 유틸리티를 사용하여 VHD를 먼저 일반화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="3f799-238">온-프레미스 또는 클라우드에 있는 VHD에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="3f799-239">Sysprep는 VHD에서 모든 컴퓨터의 특정 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f799-240">스냅숏을 찍거나 VM을 백업하기 전에 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="3f799-241">실행 중인 sysprep가 중지되고 VM 인스턴스의 할당이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="3f799-242">Windows 운영 체제 VHD를 sysprep 하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="3f799-243">Sysprep 명령을 가상 컴퓨터 종료를 해야한다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="3f799-244">Sysprep에 대한 자세한 내용은 [Sysprep 개요](http://technet.microsoft.com/library/hh825209.aspx) 또는 [Sysprep 기술 참조](http://technet.microsoft.com/library/cc766049.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="3f799-245">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="3f799-246">다음 명령을 입력하여 Sysprep을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="3f799-247">아래 이미지와 같이 시스템 준비 도구에서 시스템 OOBE(첫 실행 경험) 시작을 선택하고 일반화 확인란을 선택한 다음 **종료**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="3f799-248">Sysprep는 이 운영 체제를 일반화하고 시스템을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="3f799-249">Ubuntu VM에 대해 동일한 작업을 수행할 virt sysprep를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="3f799-250">자세한 내용은 [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="3f799-251">다른 Linux 운영 체제는 공개 소스 [Linux 서버 프로비전 소프트웨어](http://www.cyberciti.biz/tips/server-provisioning-software.html) 의 일부도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="3f799-252">고유의 운영 체제 VHD를 사용하여 단일 VM 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="3f799-253">컴퓨터 특정 데이터를 필요로 하는 VM에서 실행 중인 응용 프로그램이 있는 경우 VHD를 일반화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="3f799-254">일반화되지 않은 VHD는 고유한 Azure VM 인스턴스를 만드는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="3f799-255">예를들어 VHD에 도메인 컨트롤러가 있는 경우, sysprep를 실행하면 도메인 컨트롤러가 비효율적이게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="3f799-256">VHD를 일반화하기 전에 VM에서 실행 중인 응용 프로그램을 검토하고 이러한 응용 프로그램에서 sysprep를 실행할 때의 영향을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="3f799-257">데이터 디스크 VHD 등록</span><span class="sxs-lookup"><span data-stu-id="3f799-257">Register data disk VHD</span></span>
<span data-ttu-id="3f799-258">Azure에 마이그레이션할 데이터 디스크가 있는 경우 이 데이터 디스크를 사용하는 VM을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="3f799-259">아래에 설명된 단계에 따라 Azure Premium Storage에 VHD를 복사하고 프로비전된 데이터 디스크로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="3f799-260">2단계.</span><span class="sxs-lookup"><span data-stu-id="3f799-260">Step 2.</span></span> <span data-ttu-id="3f799-261">VHD에 대한 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-261">Create the destination for your VHD</span></span>
<span data-ttu-id="3f799-262">VHD를 유지 관리하기 위한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="3f799-263">VHD를 저장할 위치를 계획할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="3f799-264">대상 Premium Storage 계정.</span><span class="sxs-lookup"><span data-stu-id="3f799-264">The target Premium storage account.</span></span>
* <span data-ttu-id="3f799-265">저장소 계정 위치는 최종 단계에서 만들 Premium Storage 지원 Azure VM과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="3f799-266">새 저장소 계정으로 복사하거나 필요에 따라 동일한 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="3f799-267">다음 단계는 대상 저장소 계정의 저장소 계정 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="3f799-268">데이터 디스크의 경우 표준 저장소 계정에 일부 데이터 디스크(예: 냉각 저장소가 있는 디스크)를 보관할 수 있지만, 프로덕션 워크로드에서 Premium Storage를 사용하도록 모든 데이터를 이동할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="3f799-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>3단계.</span><span class="sxs-lookup"><span data-stu-id="3f799-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="3f799-270">AzCopy 또는 PowerShell을 사용하여 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="3f799-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="3f799-271">컨테이너 경로 및 저장소 계정 키를 찾아서 이러한 두 옵션 중 하나를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="3f799-272">컨테이너 경로 및 저장소 계정 키는 **Azure Portal** > **저장소**에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="3f799-273">컨테이너 URL은 "https://myaccount.blob.core.windows.net/mycontainer/" 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="3f799-274">옵션 1: AzCopy를 사용하여 VHD 복사(비동기 복사)</span><span class="sxs-lookup"><span data-stu-id="3f799-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="3f799-275">AzCopy를 사용하여 인터넷을 통해 VHD를 쉽게 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="3f799-276">소요되는 시간은 VHD의 크기에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="3f799-277">이 옵션을 사용하는 경우 저장소 계정 송/수신 제한을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="3f799-278">자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="3f799-279">[최신 버전의 AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="3f799-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="3f799-280">Azure PowerShell을 열고 AzCopy를 설치한 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="3f799-281">"원본"에서 "대상"으로 VHD 파일을 복사하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="3f799-282">예제:</span><span class="sxs-lookup"><span data-stu-id="3f799-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="3f799-283">AzCopy 명령을 사용 하는 매개 변수에 대한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="3f799-284">**/Source: *&lt;source&gt;:*** VHD를 포함하는 폴더 또는 저장소 컨테이너 URL의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="3f799-285">**/SourceKey: *&lt;source-account-key&gt;:*** 원본 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="3f799-286">**/Dest: *&lt;destination&gt;:*** VHD를 복사할 저장소 컨테이너 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="3f799-287">**/DestKey: *&lt;dest-account-key&gt;:*** 대상 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="3f799-288">**/Pattern: *&lt;file-name&gt;:*** 복사할 VHD의 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="3f799-289">AzCopy 도구 사용에 대한 자세한 내용은 [AzCopy 명령줄 유틸리티로 데이터 전송](storage-use-azcopy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="3f799-290">옵션 2: PowerShell을 사용하여 VHD 복사(동기 복사)</span><span class="sxs-lookup"><span data-stu-id="3f799-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="3f799-291">또한 PowerShell cmdlet Start-AzureStorageBlobCopy를 사용하여 VHD 파일을 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="3f799-292">Azure PowerShell에서 다음 명령을 사용하여 VHD를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="3f799-293">원본 및 대상 저장소 계정에서 해당 값으로 <>의 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="3f799-294">이 명령을 사용하려면 대상 저장소 계정에 vhd라는 컨테이너가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="3f799-295">컨테이너가 존재하지 않으면 명령을 실행하기 전에 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="3f799-296">예제:</span><span class="sxs-lookup"><span data-stu-id="3f799-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="3f799-297"><a name="scenario2"></a>시나리오 2: "다른 플랫폼에서 Azure Premium Storage로 VM을 마이그레이션하려 합니다."</span><span class="sxs-lookup"><span data-stu-id="3f799-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="3f799-298">비-Azure 클라우드 저장소에서 Azure로 VHD를 마이그레이션하는 경우, 먼저 VHD를 로컬 디렉터리로 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="3f799-299">VHD가 저장된 로컬 디렉터리의 전체 소스 경로를 찾은 다음 AzCopy를 사용하여 Azure Storage에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="3f799-300">1단계.</span><span class="sxs-lookup"><span data-stu-id="3f799-300">Step 1.</span></span> <span data-ttu-id="3f799-301">VHD를 로컬 디렉터리로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="3f799-302">AWS에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="3f799-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="3f799-303">AWS를 사용하는 경우, EC2 인스턴스를 Amazon S3 버킷의 VHD로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="3f799-304">Amazon 설명서에 제공된 Amazon EC2 인스턴스 내보내기 단계에 따라 Amazon EC2 CLI(명령줄 인터페이스) 도구를 설치하고 create-instance-export-task 명령을 실행하여 EC2 인스턴스를 VHD 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="3f799-305">**create-instance-export-task** 명령 실행 시 DISK&#95;IMAGE&#95;FORMAT 변수에 **VHD**를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="3f799-306">내보낸 VHD 파일은 해당 프로세스 중 지정된 Amazon S3 버킷에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="3f799-307">S3 버킷에서 VHD 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="3f799-308">VHD 파일을 선택한 다음 **작업** > **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="3f799-309">다른 비-Azure 클라우드에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="3f799-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="3f799-310">비-Azure 클라우드 저장소에서 Azure로 VHD를 마이그레이션하는 경우, 먼저 VHD를 로컬 디렉터리로 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="3f799-311">VHD가 저장된 로컬 디렉터리의 전체 소스 경로를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="3f799-312">온-프레미스에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="3f799-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="3f799-313">온-프레미스 환경에서 VHD를 마이그레이션하는 경우 VHD가 저장된 전체 소스 경로가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="3f799-314">이 소스 경로는 서버 위치 또는 파일 공유일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="3f799-315">2단계.</span><span class="sxs-lookup"><span data-stu-id="3f799-315">Step 2.</span></span> <span data-ttu-id="3f799-316">VHD에 대한 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-316">Create the destination for your VHD</span></span>
<span data-ttu-id="3f799-317">VHD를 유지 관리하기 위한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="3f799-318">VHD를 저장할 위치를 계획할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="3f799-319">응용 프로그램 요구 사항에 따라 대상 저장소 계정은 표준 또는 프리미엄 저장소가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="3f799-320">저장소 계정 지역은 최종 단계에서 만들 Premium Storage 지원 Azure VM과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="3f799-321">새 저장소 계정으로 복사하거나 필요에 따라 동일한 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="3f799-322">다음 단계는 대상 저장소 계정의 저장소 계정 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="3f799-323">프로덕션 워크로드에서 Premium Storage를 사용하도록 모든 데이터를 이동할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="3f799-324">3단계.</span><span class="sxs-lookup"><span data-stu-id="3f799-324">Step 3.</span></span> <span data-ttu-id="3f799-325">Azure Storage에 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="3f799-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="3f799-326">이제 VHD가 로컬 디렉터리에 있으니, AzCopy 또는 Azure PowerShell을 사용하여 .vhd 파일을 Azure Storage에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="3f799-327">두 가지 업로드 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="3f799-328">옵션 1: Azure PowerShell Add-AzureVhd를 사용하여 .vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="3f799-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="3f799-329"><Uri>의 예로 ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="3f799-330"><FileInfo>의 예로 ***"C:\path\to\upload.vhd"***를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="3f799-331">옵션 2: AzCopy를 사용하여 .vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="3f799-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="3f799-332">AzCopy를 사용하여 인터넷을 통해 VHD를 쉽게 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="3f799-333">소요되는 시간은 VHD의 크기에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="3f799-334">이 옵션을 사용하는 경우 저장소 계정 송/수신 제한을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="3f799-335">자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="3f799-336">[최신 버전의 AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="3f799-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="3f799-337">Azure PowerShell을 열고 AzCopy를 설치한 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="3f799-338">"원본"에서 "대상"으로 VHD 파일을 복사하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="3f799-339">예제:</span><span class="sxs-lookup"><span data-stu-id="3f799-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="3f799-340">AzCopy 명령을 사용 하는 매개 변수에 대한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="3f799-341">**/Source: *&lt;source&gt;:*** VHD를 포함하는 폴더 또는 저장소 컨테이너 URL의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="3f799-342">**/SourceKey: *&lt;source-account-key&gt;:*** 원본 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="3f799-343">**/Dest: *&lt;destination&gt;:*** VHD를 복사할 저장소 컨테이너 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="3f799-344">**/DestKey: *&lt;dest-account-key&gt;:*** 대상 저장소 계정의 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="3f799-345">**/BlobType: page:** 대상을 페이지 Blob으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="3f799-346">**/Pattern: *&lt;file-name&gt;:*** 복사할 VHD의 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="3f799-347">AzCopy 도구 사용에 대한 자세한 내용은 [AzCopy 명령줄 유틸리티로 데이터 전송](storage-use-azcopy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="3f799-348">VHD를 업로드하기 위한 기타 옵션</span><span class="sxs-lookup"><span data-stu-id="3f799-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="3f799-349">또한 다음과 같은 방법 중 하나를 사용하여 저장소 계정에 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="3f799-350">Azure 저장소 Blob 복사 API</span><span class="sxs-lookup"><span data-stu-id="3f799-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="3f799-351">Azure Storage 탐색기 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="3f799-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="3f799-352">저장소 가져오기/내보내기 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="3f799-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="3f799-353">예상 업로드 시간이 7일보다 긴 경우 가져오기/내보내기 서비스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="3f799-354">[DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html)를 사용하여 데이터 크기 및 전송 단위로 시간을 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="3f799-355">가져오기/내보내기를 사용하여 표준 저장소 계정을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="3f799-356">AzCopy와 같은 도구를 사용하여 표준 저장소에서 프리미엄 저장소 계정으로 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="3f799-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Premium Storage를 사용하여 Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="3f799-358">VHD를 원하는 저장소 계정에 업로드 또는 복사한 후에는 이 섹션의 설명에 따라 VHD를 OS 이미지로 등록하거나 사용자 시나리오에 따라 OS 디스크를 등록한 다음, 해당 이미지나 디스크에서 VM 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="3f799-359">생성되면 데이터 디스크 VHD를 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="3f799-360">이 섹션의 끝부분에 마이그레이션 스크립트 예제가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="3f799-361">이 간단한 스크립트가 모든 시나리오에 적합한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="3f799-362">특정 시나리오에 맞게 스크립트를 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="3f799-363">이 스크립트가 내 시나리오에 적용되는지 알아보려면 아래의 [샘플 마이그레이션 스크립트](#a-sample-migration-script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="3f799-364">검사 목록</span><span class="sxs-lookup"><span data-stu-id="3f799-364">Checklist</span></span>
1. <span data-ttu-id="3f799-365">VHD 디스크 복사가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="3f799-366">프리미엄 저장소를 마이그레이션하는 지역에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="3f799-367">사용할 새 VM 시리즈를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="3f799-368">Premium Storage를 지원해야 하며, 크기는 해당 지역의 제품 제공 여부와 사용자 요구 사항에 따라 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="3f799-369">사용할 정확한 VM 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="3f799-370">VM 크기는 현재 포함하고 있는 데이터 디스크 수를 지원할 만큼 충분히 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="3f799-371">예:</span><span class="sxs-lookup"><span data-stu-id="3f799-371">E.g.</span></span> <span data-ttu-id="3f799-372">데이터 디스크가 4개 있는 경우 VM은 2개 이상의 코어를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="3f799-373">또한 처리 능력, 메모리 및 네트워크 대역폭 요구 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="3f799-374">대상 지역에 프리미엄 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="3f799-375">새 VM에 사용할 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="3f799-376">디스크 및 해당 VHD Blob의 목록을 포함하여 도움이 될 현재 VM 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="3f799-377">응용 프로그램의 가동 중지 시간을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-377">Prepare your application for downtime.</span></span> <span data-ttu-id="3f799-378">원활한 마이그레이션 작업을 수행하려면 현재 시스템에서 모든 처리를 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="3f799-379">그런 다음 새 플랫폼으로 마이그레이션할 수 있는 일관된 상태로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="3f799-380">가동 중지 시간은 디스크에서 마이그레이션할 데이터 양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="3f799-381">특수한 VHD 디스크에서 Azure Resource Manager VM을 만드는 경우 기존 디스크를 사용하여 Resource Manager VM을 배포하는 데 사용되는 [이 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="3f799-382">장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-382">Register your VHD</span></span>
<span data-ttu-id="3f799-383">OS VHD에서 VM을 만들거나 새 VM에 데이터 디스크를 연결하려면 먼저 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="3f799-384">VHD 시나리오에 따라 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="3f799-385">여러 Azure VM 인스턴스를 만드는 일반화된 운영 체제 VHD</span><span class="sxs-lookup"><span data-stu-id="3f799-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="3f799-386">일반화된 OS 이미지를 저장소 계정에 업로드한 후에는 이 이미지에서 하나 이상의 VM 인스턴스를 만들 수 있도록 이미지를 **Azure VM 이미지**로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="3f799-387">Azure VM OS 이미지로 VHD를 등록 하려면 다음 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="3f799-388">VHD가 복사된 완전한 컨테이너 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="3f799-389">새 Azure VM 이미지의 이름을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="3f799-390">위의 예제에서는 *OSImageName*입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="3f799-391">단일 Azure VM 인스턴스를 만드는 고유 운영 체제 VHD</span><span class="sxs-lookup"><span data-stu-id="3f799-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="3f799-392">고유 OS VHD를 저장소 계정에 업로드 한 후에는 이 디스크에서 VM 인스턴스를 만들 수 있도록 디스크를 **Azure OS 디스크**로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="3f799-393">이 PowerShell cmdlet을 사용하여 Azure OS 이미지로 VHD를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="3f799-394">VHD가 복사된 완전한 컨테이너 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="3f799-395">새 Azure OS 이미지의 이름을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="3f799-396">위의 예제에서는 *OSDisk*입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="3f799-397">Azure VM 인스턴스에 연결될 데이터 디스크 VHD</span><span class="sxs-lookup"><span data-stu-id="3f799-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="3f799-398">데이터 디스크 VHD를 저장소 계정에 업로드한 후 Azure 데이터 디스크로 등록되면 새 DS 시리즈, DSv2 시리즈 또는 GS 시리즈 Azure VM 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="3f799-399">이 PowerShell cmdlet을 사용하여 Azure 데이터 디스크로 VHD를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="3f799-400">VHD가 복사된 완전한 컨테이너 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="3f799-401">새 Azure 데이터 디스크의 이름을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="3f799-402">위의 예제에서는 *DataDisk*입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="3f799-403">Premium Storage 지원 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3f799-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="3f799-404">OS 이미지나 OS 디스크가 등록되면 새 DS 시리즈, DSv2 시리즈 또는 GS 시리즈 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="3f799-405">등록된 운영 체제 이미지 또는 운영 체제 디스크 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="3f799-406">프리미엄 저장소 계층에서 VM 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="3f799-407">아래 예제에서는 *Standard_DS2* VM 크기를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="3f799-408">디스크 크기를 업데이트하여 용량, 성능 요구 사항 및 사용 가능한 Azure 디스크 크기가 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="3f799-409">아래 PowerShell cmdlet을 단계별로 수행하여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="3f799-410">먼저, 공통 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="3f799-411">먼저, 클라우드 서비스를 호스트할 새 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="3f799-412">다음, 시나리오에 따라 등록된 OS 이미지 또는 OS 디스크에서 Azure VM 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="3f799-413">여러 Azure VM 인스턴스를 만드는 일반화된 운영 체제 VHD</span><span class="sxs-lookup"><span data-stu-id="3f799-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="3f799-414">등록된 **Azure OS 이미지** 를 사용하여 하나 이상의 새 DS 시리즈 Azure VM 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="3f799-415">아래와 같이 새 VM을 만들 때 VM 구성에서 이 OS 이미지 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="3f799-416">단일 Azure VM 인스턴스를 만드는 고유 운영 체제 VHD</span><span class="sxs-lookup"><span data-stu-id="3f799-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="3f799-417">등록된 **Azure OS 디스크** 를 사용하여 새 DS 시리즈 Azure VM 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="3f799-418">아래와 같이 새 VM을 만들 때 VM 구성에서 이 OS 디스크 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="3f799-419">클라우드 서비스, 지역, 저장소 계정, 가용성 집합 및 캐싱 정책 등의 기타 Azure VM 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="3f799-420">VM 인스턴스는 연관된 운영 체제 또는 데이터 디스크와 배치되므로 선택된 클라우드 서비스, 지역 및 저장소 계정은 모두 해당 디스크의 기본 VHD와 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="3f799-421">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="3f799-421">Attach data disk</span></span>
<span data-ttu-id="3f799-422">마지막으로, 데이터 디스크 VHD를 등록한 경우 새 Premium Storage 지원 Azure VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="3f799-423">새 VM에 데이터 디스크를 연결하고 캐싱 정책을 지정하려면 다음 PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="3f799-424">아래 예제에서는 캐싱 정책이 *ReadOnly*로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="3f799-425">이 가이드에서 다루지 않은 응용 프로그램을 지원하기 위해 추가 단계가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="3f799-426">확인 및 백업 계획</span><span class="sxs-lookup"><span data-stu-id="3f799-426">Checking and plan backup</span></span>
<span data-ttu-id="3f799-427">새 VM이 준비되고 실행 중이면 원본 VM과 동일한 로그인 ID 및 암호를 사용하여 액세스하고 모든 항목이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="3f799-428">스트라이프 볼륨을 포함한 모든 설정이 새 VM에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="3f799-429">마지막 단계는 응용 프로그램 요구 사항에 따라 새 VM의 백업 및 유지 관리 일정을 계획하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="3f799-430"><a name="a-sample-migration-script"></a>샘플 마이그레이션 스크립트</span><span class="sxs-lookup"><span data-stu-id="3f799-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="3f799-431">마이그레이션할 여러 VM이 있는 경우 PowerShell 스크립트를 통한 자동화가 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="3f799-432">다음은 VM의 마이그레이션을 자동화하는 예제 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="3f799-433">아래의 스크립트는 현재 VM 디스크에 대해 몇 가지 조건을 가정하고 만든 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="3f799-434">특정 시나리오에 맞게 스크립트를 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="3f799-435">가정한 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-435">The assumptions are:</span></span>

* <span data-ttu-id="3f799-436">클래식 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="3f799-437">원본 OS 디스크와 원본 데이터 디스크가 동일한 저장소 계정 및 동일한 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="3f799-438">OS 디스크와 데이터 디스크가 같은 위치에 있지 않으면 AzCopy 또는 Azure PowerShell을 사용하여 저장소 계정 및 컨테이너를 통해 VHD를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="3f799-439">이전 단계 [AzCopy 또는 PowerShell을 사용하여 VHD 복사](#copy-vhd-with-azcopy-or-powershell)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="3f799-440">시나리오를 충족하도록 이 스크립트를 편집하는 방법도 있지만 더 간편하고 빠른 AzCopy 또는 PowerShell을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="3f799-441">자동화 스크립트는 아래에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-441">The automation script is provided below.</span></span> <span data-ttu-id="3f799-442">텍스트를 사용자의 정보로 바꾸고 사용자의 특정 시나리오와 일치하도록 스크립트를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="3f799-443">기존 스크립트를 사용하면 원본 VM의 네트워크 구성이 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="3f799-444">마이그레이션된 VM의 네트워킹 설정을 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
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


    #Check the Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
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
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="3f799-445"><a name="optimization"></a>최적화</span><span class="sxs-lookup"><span data-stu-id="3f799-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="3f799-446">표준 디스크와 잘 작동하도록 현재 VM 구성을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="3f799-447">예를 들어, 스트라이프 볼륨의 많은 디스크를 사용하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="3f799-448">예를 들어 Premium Storage에서 4개의 디스크를 개별적으로 사용하는 대신 단일 디스크를 사용하여 비용을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="3f799-449">이와 같은 최적화는 상황별로 처리해야 하며 마이그레이션 후 사용자 지정 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="3f799-450">이 프로세스는 설치 시 정의된 디스크 레이아웃에 종속된 응용 프로그램 및 데이터베이스에 대해서는 제대로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="3f799-451">준비</span><span class="sxs-lookup"><span data-stu-id="3f799-451">Preparation</span></span>
1. <span data-ttu-id="3f799-452">이전 섹션에서 설명한 대로 간단한 마이그레이션을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="3f799-453">마이그레이션 후 새 VM에서 최적화가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="3f799-454">최적화된 구성에 필요한 새 디스크 크기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="3f799-455">새 디스크 사양에 대해 현재 디스크/볼륨의 매핑을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="3f799-456">실행 단계</span><span class="sxs-lookup"><span data-stu-id="3f799-456">Execution steps</span></span>
1. <span data-ttu-id="3f799-457">프리미엄 저장소 VM에 올바른 크기의 새 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="3f799-458">VM에 로그인하고 현재 볼륨의 데이터를 해당 볼륨에 매핑되는 새 디스크로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="3f799-459">새 디스크에 매핑해야 하는 모든 현재 볼륨에 대해 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="3f799-460">다음으로, 새 디스크로 전환하도록 응용 프로그램 설정을 변경하고 이전 볼륨을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="3f799-461">디스크 성능 향상을 위해 응용 프로그램을 튜닝하는 방법은 [응용 프로그램 성능 최적화](storage-premium-storage-performance.md#optimizing-application-performance)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="3f799-462">응용 프로그램 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="3f799-462">Application migrations</span></span>
<span data-ttu-id="3f799-463">데이터베이스 및 기타 복잡한 응용 프로그램에는 응용 프로그램 공급자가 마이그레이션에 대해 정의한 특별한 단계가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="3f799-464">각각의 응용 프로그램 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="3f799-465">예:</span><span class="sxs-lookup"><span data-stu-id="3f799-465">E.g.</span></span> <span data-ttu-id="3f799-466">일반적으로 백업 및 복원을 통해 데이터베이스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f799-467">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f799-467">Next steps</span></span>
<span data-ttu-id="3f799-468">가상 컴퓨터 마이그레이션에 대한 특정 시나리오에 대한 다음 리소스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="3f799-469">저장소 계정 간에 Azure 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="3f799-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="3f799-470">Windows Server VHD를 만들고 Azure에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f799-470">Create and upload a Windows Server VHD to Azure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f799-471">Linux 운영 체제를 포함하는 가상 하드 디스크 만들기 및 업로드</span><span class="sxs-lookup"><span data-stu-id="3f799-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f799-472">Amazon AWS에서 Microsoft Azure로 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="3f799-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="3f799-473">Azure Storage 및 Azure 가상 컴퓨터에 대한 자세한 내용을 보려면 다음 리소스도 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3f799-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="3f799-474">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="3f799-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="3f799-475">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f799-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="3f799-476">프리미엄 저장소: Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소</span><span class="sxs-lookup"><span data-stu-id="3f799-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
