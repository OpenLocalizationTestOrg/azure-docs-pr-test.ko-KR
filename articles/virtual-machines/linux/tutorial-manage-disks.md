---
title: "Azure CLI를 사용하여 Azure 디스크 관리 | Microsoft Docs"
description: "자습서 - Azure CLI를 사용하여 Azure 디스크 관리"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="642a7-103">Azure CLI를 사용하여 Azure 디스크 관리</span><span class="sxs-lookup"><span data-stu-id="642a7-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="642a7-104">Azure 가상 컴퓨터는 디스크를 사용하여 VM 운영 체제, 응용 프로그램 및 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="642a7-105">VM을 만들 때 예상되는 워크로드에 적합한 디스크 크기와 구성을 선택하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="642a7-106">이 자습서에서는 VM 디스크의 배포 및 관리에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="642a7-107">다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="642a7-108">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="642a7-109">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-109">Data disks</span></span>
> * <span data-ttu-id="642a7-110">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="642a7-111">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="642a7-111">Disk performance</span></span>
> * <span data-ttu-id="642a7-112">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="642a7-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="642a7-113">디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="642a7-113">Resizing disks</span></span>
> * <span data-ttu-id="642a7-114">디스크 스냅숏</span><span class="sxs-lookup"><span data-stu-id="642a7-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="642a7-115">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="642a7-116">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="642a7-117">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="642a7-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="642a7-118">기본 Azure 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-118">Default Azure disks</span></span>

<span data-ttu-id="642a7-119">Azure Virtual Machine을 만들면 두 개의 디스크가 자동으로 가상 컴퓨터에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="642a7-120">**운영 체제 디스크** - 운영 체제 디스크는 최대 1TB까지 가능하며 VM 운영 체제를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="642a7-121">OS 디스크는 기본적으로 */dev/sda*로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="642a7-122">OS 디스크의 디스크 캐싱 구성은 OS 성능에 맞게 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="642a7-123">이 구성으로 인해 OS 디스크는 응용 프로그램 또는 데이터를 호스트해서는 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="642a7-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="642a7-124">응용 프로그램 및 데이터는 데이터 디스크를 사용하며 여기에 대해서는 이 문서의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="642a7-125">**임시 디스크** - 임시 디스크는 VM과 같은 Azure 호스트에 있는 반도체 드라이브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="642a7-126">임시 디스크는 성능이 높고 임시 데이터 처리 등의 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="642a7-127">그러나 VM이 새 호스트로 이동되면 임시 디스크에 저장된 모든 데이터는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="642a7-128">임시 디스크의 크기는 VM 크기에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="642a7-129">임시 디스크는 */dev/sdb*로 레이블이 지정되고 탑재 지점은 */mnt*입니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="642a7-130">임시 디스크 크기</span><span class="sxs-lookup"><span data-stu-id="642a7-130">Temporary disk sizes</span></span>

| <span data-ttu-id="642a7-131">형식</span><span class="sxs-lookup"><span data-stu-id="642a7-131">Type</span></span> | <span data-ttu-id="642a7-132">VM 크기</span><span class="sxs-lookup"><span data-stu-id="642a7-132">VM Size</span></span> | <span data-ttu-id="642a7-133">최대 임시 디스크 크기(GB)</span><span class="sxs-lookup"><span data-stu-id="642a7-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="642a7-134">범용</span><span class="sxs-lookup"><span data-stu-id="642a7-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="642a7-135">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-135">A and D series</span></span> | <span data-ttu-id="642a7-136">800</span><span class="sxs-lookup"><span data-stu-id="642a7-136">800</span></span> |
| [<span data-ttu-id="642a7-137">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="642a7-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="642a7-138">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-138">F series</span></span> | <span data-ttu-id="642a7-139">800</span><span class="sxs-lookup"><span data-stu-id="642a7-139">800</span></span> |
| [<span data-ttu-id="642a7-140">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="642a7-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="642a7-141">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-141">D and G series</span></span> | <span data-ttu-id="642a7-142">6144</span><span class="sxs-lookup"><span data-stu-id="642a7-142">6144</span></span> |
| [<span data-ttu-id="642a7-143">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="642a7-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="642a7-144">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-144">L series</span></span> | <span data-ttu-id="642a7-145">5630</span><span class="sxs-lookup"><span data-stu-id="642a7-145">5630</span></span> |
| [<span data-ttu-id="642a7-146">GPU</span><span class="sxs-lookup"><span data-stu-id="642a7-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="642a7-147">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-147">N series</span></span> | <span data-ttu-id="642a7-148">1,440</span><span class="sxs-lookup"><span data-stu-id="642a7-148">1440</span></span> |
| [<span data-ttu-id="642a7-149">고성능</span><span class="sxs-lookup"><span data-stu-id="642a7-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="642a7-150">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-150">A and H series</span></span> | <span data-ttu-id="642a7-151">2000</span><span class="sxs-lookup"><span data-stu-id="642a7-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="642a7-152">Azure 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-152">Azure data disks</span></span>

<span data-ttu-id="642a7-153">응용 프로그램을 설치하고 데이터를 저장하기 위해 데이터 디스크를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="642a7-154">데이터 디스크는 지속형 및 반응형 데이터 저장소가 필요한 상황에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="642a7-155">각 데이터 디스크의 최대 용량은 1테라바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="642a7-156">가상 컴퓨터의 크기에 따라 VM에 연결할 수 있는 데이터 디스크 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="642a7-157">각 VM 코어에 대해 두 개의 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="642a7-158">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="642a7-158">Max data disks per VM</span></span>

| <span data-ttu-id="642a7-159">형식</span><span class="sxs-lookup"><span data-stu-id="642a7-159">Type</span></span> | <span data-ttu-id="642a7-160">VM 크기</span><span class="sxs-lookup"><span data-stu-id="642a7-160">VM Size</span></span> | <span data-ttu-id="642a7-161">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="642a7-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="642a7-162">범용</span><span class="sxs-lookup"><span data-stu-id="642a7-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="642a7-163">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-163">A and D series</span></span> | <span data-ttu-id="642a7-164">32</span><span class="sxs-lookup"><span data-stu-id="642a7-164">32</span></span> |
| [<span data-ttu-id="642a7-165">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="642a7-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="642a7-166">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-166">F series</span></span> | <span data-ttu-id="642a7-167">32</span><span class="sxs-lookup"><span data-stu-id="642a7-167">32</span></span> |
| [<span data-ttu-id="642a7-168">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="642a7-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="642a7-169">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-169">D and G series</span></span> | <span data-ttu-id="642a7-170">64</span><span class="sxs-lookup"><span data-stu-id="642a7-170">64</span></span> |
| [<span data-ttu-id="642a7-171">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="642a7-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="642a7-172">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-172">L series</span></span> | <span data-ttu-id="642a7-173">64</span><span class="sxs-lookup"><span data-stu-id="642a7-173">64</span></span> |
| [<span data-ttu-id="642a7-174">GPU</span><span class="sxs-lookup"><span data-stu-id="642a7-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="642a7-175">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-175">N series</span></span> | <span data-ttu-id="642a7-176">48</span><span class="sxs-lookup"><span data-stu-id="642a7-176">48</span></span> |
| [<span data-ttu-id="642a7-177">고성능</span><span class="sxs-lookup"><span data-stu-id="642a7-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="642a7-178">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="642a7-178">A and H series</span></span> | <span data-ttu-id="642a7-179">32</span><span class="sxs-lookup"><span data-stu-id="642a7-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="642a7-180">VM 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="642a7-180">VM disk types</span></span>

<span data-ttu-id="642a7-181">Azure는 두 가지 유형의 디스크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="642a7-182">표준 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-182">Standard disk</span></span>

<span data-ttu-id="642a7-183">Standard Storage는 HDD에 의해 지원되며 성능은 그대로이면서 비용 효율적인 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="642a7-184">표준 디스크는 비용 효율적인 개발 및 테스트 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="642a7-185">프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-185">Premium disk</span></span>

<span data-ttu-id="642a7-186">프리미엄 디스크는 SSD 기반 고성능의 대기 시간이 짧은 디스크에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="642a7-187">프로덕션 워크로드를 실행하는 VM에 완벽한 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="642a7-188">Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 FS 시리즈 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="642a7-189">프리미엄 디스크는 세 가지 유형(P10, P20 P30)으로 제공되며 디스크 크기에 따라 디스크 유형이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="642a7-190">디스크 유형 선택 시 디스크 크기 값은 다음 유형으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="642a7-191">예를 들어 디스크 크기가 128GB 미만인 경우 디스크 유형은 P10입니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="642a7-192">디스크 크기가 129GB에서 512GB 사이이면 크기는 P20입니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="642a7-193">512GB가 넘으면 P30입니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="642a7-194">프리미엄 디스크 성능</span><span class="sxs-lookup"><span data-stu-id="642a7-194">Premium disk performance</span></span>

|<span data-ttu-id="642a7-195">Premium Storage 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="642a7-195">Premium storage disk type</span></span> | <span data-ttu-id="642a7-196">P10</span><span class="sxs-lookup"><span data-stu-id="642a7-196">P10</span></span> | <span data-ttu-id="642a7-197">P20</span><span class="sxs-lookup"><span data-stu-id="642a7-197">P20</span></span> | <span data-ttu-id="642a7-198">P30</span><span class="sxs-lookup"><span data-stu-id="642a7-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="642a7-199">디스크 크기(반올림)</span><span class="sxs-lookup"><span data-stu-id="642a7-199">Disk size (round up)</span></span> | <span data-ttu-id="642a7-200">128GB</span><span class="sxs-lookup"><span data-stu-id="642a7-200">128 GB</span></span> | <span data-ttu-id="642a7-201">512GB</span><span class="sxs-lookup"><span data-stu-id="642a7-201">512 GB</span></span> | <span data-ttu-id="642a7-202">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="642a7-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="642a7-203">디스크당 최대 IOPS</span><span class="sxs-lookup"><span data-stu-id="642a7-203">Max IOPS per disk</span></span> | <span data-ttu-id="642a7-204">500</span><span class="sxs-lookup"><span data-stu-id="642a7-204">500</span></span> | <span data-ttu-id="642a7-205">2,300</span><span class="sxs-lookup"><span data-stu-id="642a7-205">2,300</span></span> | <span data-ttu-id="642a7-206">5,000</span><span class="sxs-lookup"><span data-stu-id="642a7-206">5,000</span></span> |
<span data-ttu-id="642a7-207">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="642a7-207">Throughput per disk</span></span> | <span data-ttu-id="642a7-208">100MB/초</span><span class="sxs-lookup"><span data-stu-id="642a7-208">100 MB/s</span></span> | <span data-ttu-id="642a7-209">150MB/초</span><span class="sxs-lookup"><span data-stu-id="642a7-209">150 MB/s</span></span> | <span data-ttu-id="642a7-210">200MB/s</span><span class="sxs-lookup"><span data-stu-id="642a7-210">200 MB/s</span></span> |

<span data-ttu-id="642a7-211">위의 표에 디스크당 최대 IOPS가 나와 있지만 여러 데이터 디스크를 스트라이프하여 더 높은 수준의 성능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="642a7-212">예를 들어 Standard_GS5 VM은 최대 80,000 IOPS를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="642a7-213">VM당 최대 IOPS에 대한 자세한 내용은 [Linux VM 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="642a7-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="642a7-214">디스크 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="642a7-214">Create and attach disks</span></span>

<span data-ttu-id="642a7-215">VM을 만들 때 또는 기존 VM에 데이터 디스크를 만들고 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="642a7-216">VM을 만들 때 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="642a7-216">Attach disk at VM creation</span></span>

<span data-ttu-id="642a7-217">[az group create](https://docs.microsoft.com/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="642a7-218">[az vm create]( /cli/azure/vm#create) 명령을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="642a7-219">`--datadisk-sizes-gb` 인수를 사용하여 가상 컴퓨터에 추가 디스크를 만들고 연결하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="642a7-220">둘 이상의 디스크를 만들고 연결하려면 공백으로 구분된 디스크 크기 값 목록을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="642a7-221">다음 예제에서는 128GB 데이터 디스크 두 개가 있는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="642a7-222">디스크 크기가 128GB이므로 이러한 디스크는 모두 디스크당 최대 500 IOPS를 제공하는 P10으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="642a7-223">기존 VM에 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="642a7-223">Attach disk to existing VM</span></span>

<span data-ttu-id="642a7-224">기존 가상 컴퓨터에 새 디스크를 만들고 연결하려면 [az vm disk attach](/cli/azure/vm/disk#attach) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="642a7-225">다음 예제에서는 크기가 128GB인 프리미엄 디스크를 만들고 마지막 단계에서 만든 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="642a7-226">데이터 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="642a7-226">Prepare data disks</span></span>

<span data-ttu-id="642a7-227">디스크가 가상 컴퓨터에 연결된 후 디스크를 사용하도록 운영 체제를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="642a7-228">다음 예제에는 디스크를 수동으로 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="642a7-229">이 프로세스는 cloud-init를 사용하여 자동화할 수도 있으며 여기에 대해서는 [이후의 자습서](./tutorial-automate-vm-deployment.md)에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="642a7-230">수동 구성</span><span class="sxs-lookup"><span data-stu-id="642a7-230">Manual configuration</span></span>

<span data-ttu-id="642a7-231">가상 컴퓨터와 SSH 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="642a7-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="642a7-232">예제 IP 주소를 가상 컴퓨터의 공용 IP로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="642a7-233">`fdisk`를 사용하여 디스크를 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="642a7-234">`mkfs` 명령을 사용하여 파티션에 파일 시스템을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="642a7-235">운영 체제에서 액세스할 수 있도록 새 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="642a7-236">이제 *datadrive* 탑재 지점을 통해 디스크에 액세스할 수 있으며, `df -h` 명령을 실행하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="642a7-237">*/datadrive*에 탑재된 새 드라이브가 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="642a7-238">다시 부팅 후 드라이브가 다시 탑재되도록 하려면 */etc/fstab* 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="642a7-239">이렇게 하려면 `blkid` 유틸리티를 사용하여 디스크의 UUID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="642a7-240">출력에 드라이브의 UUID가 표시됩니다(이 경우 `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="642a7-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="642a7-241">다음과 유사한 줄을 */etc/fstab* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="642a7-242">*barrier=0*을 사용하여 쓰기 장벽을 사용하지 않도록 설정할 수 있으며 이 구성으로 디스크 성능이 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="642a7-243">이제 디스크가 구성되었으니 SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="642a7-244">VM 디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="642a7-244">Resize VM disk</span></span>

<span data-ttu-id="642a7-245">VM을 배포한 후 운영 체제 디스크 또는 모든 연결된 데이터 디스크의 크기를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="642a7-246">디스크의 크기를 늘리면 더 많은 저장소 공간이나 더 높은 수준의 성능(P10, P20, P30)이 필요한 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="642a7-247">디스크 크기를 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="642a7-248">디스크 크기를 늘리려면 디스크의 ID 또는 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="642a7-249">[az disk list](/cli/azure/vm/disk#list) 명령을 사용하여 리소스 그룹의 모든 디스크를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="642a7-250">크기를 조정할 디스크 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="642a7-251">VM 할당도 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-251">The VM must also be deallocated.</span></span> <span data-ttu-id="642a7-252">[az vm deallocate]( /cli/azure/vm#deallocate) 명령을 사용하여 VM을 중지하고 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="642a7-253">[az disk update](/cli/azure/vm/disk#update) 명령을 사용하여 디스크의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="642a7-254">이 예제에서는 *myDataDisk*라는 디스크의 크기를 1테라바이트로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="642a7-255">크기 조정 작업이 완료되면 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="642a7-256">운영 체제 디스크의 크기를 조정한 경우 파티션은 자동으로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="642a7-257">데이터 디스크의 크기를 조정한 경우 현재 파티션을 모두 VM 운영 체제에서 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="642a7-258">스냅숏 Azure 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-258">Snapshot Azure disks</span></span>

<span data-ttu-id="642a7-259">디스크 스냅숏을 생성하면 디스크의 읽기 전용, 지정 시간 복사본이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="642a7-260">Azure VM 스냅숏은 구성을 변경하기 전에 VM의 상태를 신속하게 저장하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="642a7-261">원하지 않게 구성이 변경된 경우 스냅숏을 사용하여 VM 상태를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="642a7-262">VM에 둘 이상의 디스크가 있는 경우 각 디스크의 스냅숏은 다른 디스크의 스냅숏과 독립적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="642a7-263">응용 프로그램 일치 백업을 만들려면 디스크 스냅숏을 만들기 전에 VM을 중지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="642a7-264">또는 [Azure Backup 서비스](/azure/backup/)를 사용하면 VM을 실행하는 동안 자동화된 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="642a7-265">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="642a7-265">Create snapshot</span></span>

<span data-ttu-id="642a7-266">가상 컴퓨터 디스크 스냅숏을 만들려면 디스크의 ID 또는 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="642a7-267">[az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) 명령을 사용하여 디스크 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="642a7-268">이 예제에서는 디스크 ID가 변수에 저장되고 이후 단계에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="642a7-269">이제 가상 컴퓨터의 ID를 알고 있으므로 다음 명령을 실행하여 디스크 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="642a7-270">스냅숏에서 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="642a7-270">Create disk from snapshot</span></span>

<span data-ttu-id="642a7-271">그런 다음 스냅숏을 디스크로 복원하여 가상 컴퓨터를 다시 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="642a7-272">스냅숏에서 가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="642a7-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="642a7-273">가상 컴퓨터 복구를 보여 주기 위해 기존 가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="642a7-274">스냅숏 디스크에서 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="642a7-275">데이터 디스크 다시 연결</span><span class="sxs-lookup"><span data-stu-id="642a7-275">Reattach data disk</span></span>

<span data-ttu-id="642a7-276">모든 데이터 디스크를 가상 컴퓨터에 다시 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="642a7-277">먼저 [az disk list](https://docs.microsoft.com/cli/azure/disk#list) 명령을 사용하여 데이터 디스크 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="642a7-278">이 예제에서는 *datadisk*라는 변수에 디스크의 이름을 추가합니다. 이 변수는 다음 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="642a7-279">[az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) 명령을 사용하여 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="642a7-280">다음 단계</span><span class="sxs-lookup"><span data-stu-id="642a7-280">Next steps</span></span>

<span data-ttu-id="642a7-281">이 자습서에서는 다음과 같은 VM 디스크 항목에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="642a7-282">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="642a7-283">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-283">Data disks</span></span>
> * <span data-ttu-id="642a7-284">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="642a7-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="642a7-285">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="642a7-285">Disk performance</span></span>
> * <span data-ttu-id="642a7-286">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="642a7-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="642a7-287">디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="642a7-287">Resizing disks</span></span>
> * <span data-ttu-id="642a7-288">디스크 스냅숏</span><span class="sxs-lookup"><span data-stu-id="642a7-288">Disk snapshots</span></span>

<span data-ttu-id="642a7-289">VM 구성 자동화에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="642a7-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="642a7-290">VM 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="642a7-290">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
