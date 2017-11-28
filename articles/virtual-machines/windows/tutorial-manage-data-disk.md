---
title: "Azure PowerShell을 사용하여 Azure 디스크 관리 | Microsoft Docs"
description: "자습서 - Azure PowerShell을 사용하여 Azure 디스크 관리"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="0e3d6-103">PowerShell을 사용하여 Azure 디스크 관리</span><span class="sxs-lookup"><span data-stu-id="0e3d6-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="0e3d6-104">Azure 가상 컴퓨터는 디스크를 사용하여 VM 운영 체제, 응용 프로그램 및 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="0e3d6-105">VM을 만들 때 예상되는 워크로드에 적합한 디스크 크기와 구성을 선택하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="0e3d6-106">이 자습서에서는 VM 디스크의 배포 및 관리에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="0e3d6-107">다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e3d6-108">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="0e3d6-109">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-109">Data disks</span></span>
> * <span data-ttu-id="0e3d6-110">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="0e3d6-111">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="0e3d6-111">Disk performance</span></span>
> * <span data-ttu-id="0e3d6-112">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="0e3d6-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="0e3d6-113">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="0e3d6-114">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="0e3d6-115">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="0e3d6-116">기본 Azure 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-116">Default Azure disks</span></span>

<span data-ttu-id="0e3d6-117">Azure Virtual Machine을 만들면 두 개의 디스크가 자동으로 가상 컴퓨터에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="0e3d6-118">**운영 체제 디스크** - 운영 체제 디스크는 최대 1TB까지 가능하며 VM 운영 체제를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="0e3d6-119">OS 디스크는 기본적으로 *c:* 드라이브 문자가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="0e3d6-120">OS 디스크의 디스크 캐싱 구성은 OS 성능에 맞게 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="0e3d6-121">OS 디스크는 응용 프로그램 또는 데이터를 호스트해서는 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="0e3d6-122">응용 프로그램 및 데이터는 데이터 디스크를 사용하며 여기에 대해서는 이 문서의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="0e3d6-123">**임시 디스크** - 임시 디스크는 VM과 같은 Azure 호스트에 있는 반도체 드라이브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="0e3d6-124">임시 디스크는 성능이 높고 임시 데이터 처리 등의 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="0e3d6-125">그러나 VM이 새 호스트로 이동되면 임시 디스크에 저장된 모든 데이터는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="0e3d6-126">임시 디스크의 크기는 VM 크기에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="0e3d6-127">임시 디스크는 기본적으로 *d:* 드라이브 문자가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="0e3d6-128">임시 디스크 크기</span><span class="sxs-lookup"><span data-stu-id="0e3d6-128">Temporary disk sizes</span></span>

| <span data-ttu-id="0e3d6-129">형식</span><span class="sxs-lookup"><span data-stu-id="0e3d6-129">Type</span></span> | <span data-ttu-id="0e3d6-130">VM 크기</span><span class="sxs-lookup"><span data-stu-id="0e3d6-130">VM Size</span></span> | <span data-ttu-id="0e3d6-131">최대 임시 디스크 크기(GB)</span><span class="sxs-lookup"><span data-stu-id="0e3d6-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="0e3d6-132">범용</span><span class="sxs-lookup"><span data-stu-id="0e3d6-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="0e3d6-133">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-133">A and D series</span></span> | <span data-ttu-id="0e3d6-134">800</span><span class="sxs-lookup"><span data-stu-id="0e3d6-134">800</span></span> |
| [<span data-ttu-id="0e3d6-135">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="0e3d6-136">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-136">F series</span></span> | <span data-ttu-id="0e3d6-137">800</span><span class="sxs-lookup"><span data-stu-id="0e3d6-137">800</span></span> |
| [<span data-ttu-id="0e3d6-138">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="0e3d6-139">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-139">D and G series</span></span> | <span data-ttu-id="0e3d6-140">6144</span><span class="sxs-lookup"><span data-stu-id="0e3d6-140">6144</span></span> |
| [<span data-ttu-id="0e3d6-141">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="0e3d6-142">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-142">L series</span></span> | <span data-ttu-id="0e3d6-143">5630</span><span class="sxs-lookup"><span data-stu-id="0e3d6-143">5630</span></span> |
| [<span data-ttu-id="0e3d6-144">GPU</span><span class="sxs-lookup"><span data-stu-id="0e3d6-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="0e3d6-145">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-145">N series</span></span> | <span data-ttu-id="0e3d6-146">1,440</span><span class="sxs-lookup"><span data-stu-id="0e3d6-146">1440</span></span> |
| [<span data-ttu-id="0e3d6-147">고성능</span><span class="sxs-lookup"><span data-stu-id="0e3d6-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="0e3d6-148">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-148">A and H series</span></span> | <span data-ttu-id="0e3d6-149">2000</span><span class="sxs-lookup"><span data-stu-id="0e3d6-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="0e3d6-150">Azure 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-150">Azure data disks</span></span>

<span data-ttu-id="0e3d6-151">응용 프로그램을 설치하고 데이터를 저장하기 위해 데이터 디스크를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="0e3d6-152">데이터 디스크는 지속형 및 반응형 데이터 저장소가 필요한 상황에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="0e3d6-153">각 데이터 디스크의 최대 용량은 1테라바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="0e3d6-154">가상 컴퓨터의 크기에 따라 VM에 연결할 수 있는 데이터 디스크 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="0e3d6-155">각 VM 코어에 대해 두 개의 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="0e3d6-156">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="0e3d6-156">Max data disks per VM</span></span>

| <span data-ttu-id="0e3d6-157">형식</span><span class="sxs-lookup"><span data-stu-id="0e3d6-157">Type</span></span> | <span data-ttu-id="0e3d6-158">VM 크기</span><span class="sxs-lookup"><span data-stu-id="0e3d6-158">VM Size</span></span> | <span data-ttu-id="0e3d6-159">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="0e3d6-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="0e3d6-160">범용</span><span class="sxs-lookup"><span data-stu-id="0e3d6-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="0e3d6-161">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-161">A and D series</span></span> | <span data-ttu-id="0e3d6-162">32</span><span class="sxs-lookup"><span data-stu-id="0e3d6-162">32</span></span> |
| [<span data-ttu-id="0e3d6-163">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="0e3d6-164">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-164">F series</span></span> | <span data-ttu-id="0e3d6-165">32</span><span class="sxs-lookup"><span data-stu-id="0e3d6-165">32</span></span> |
| [<span data-ttu-id="0e3d6-166">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="0e3d6-167">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-167">D and G series</span></span> | <span data-ttu-id="0e3d6-168">64</span><span class="sxs-lookup"><span data-stu-id="0e3d6-168">64</span></span> |
| [<span data-ttu-id="0e3d6-169">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="0e3d6-170">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-170">L series</span></span> | <span data-ttu-id="0e3d6-171">64</span><span class="sxs-lookup"><span data-stu-id="0e3d6-171">64</span></span> |
| [<span data-ttu-id="0e3d6-172">GPU</span><span class="sxs-lookup"><span data-stu-id="0e3d6-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="0e3d6-173">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-173">N series</span></span> | <span data-ttu-id="0e3d6-174">48</span><span class="sxs-lookup"><span data-stu-id="0e3d6-174">48</span></span> |
| [<span data-ttu-id="0e3d6-175">고성능</span><span class="sxs-lookup"><span data-stu-id="0e3d6-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="0e3d6-176">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="0e3d6-176">A and H series</span></span> | <span data-ttu-id="0e3d6-177">32</span><span class="sxs-lookup"><span data-stu-id="0e3d6-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="0e3d6-178">VM 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="0e3d6-178">VM disk types</span></span>

<span data-ttu-id="0e3d6-179">Azure는 두 가지 유형의 디스크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="0e3d6-180">표준 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-180">Standard disk</span></span>

<span data-ttu-id="0e3d6-181">Standard Storage는 HDD에 의해 지원되며 성능은 그대로이면서 비용 효율적인 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="0e3d6-182">표준 디스크는 비용 효율적인 개발 및 테스트 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="0e3d6-183">프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-183">Premium disk</span></span>

<span data-ttu-id="0e3d6-184">프리미엄 디스크는 SSD 기반 고성능의 대기 시간이 짧은 디스크에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="0e3d6-185">프로덕션 워크로드를 실행하는 VM에 완벽한 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="0e3d6-186">Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 FS 시리즈 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="0e3d6-187">프리미엄 디스크는 세 가지 유형(P10, P20 P30)으로 제공되며 디스크 크기에 따라 디스크 유형이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="0e3d6-188">디스크 유형 선택 시 디스크 크기 값은 다음 유형으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="0e3d6-189">예를 들어 크기가 128GB 미만인 경우 디스크 유형은 P10, 129~512GB인 경우 P20, 512GB가 넘으면 P30이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="0e3d6-190">프리미엄 디스크 성능</span><span class="sxs-lookup"><span data-stu-id="0e3d6-190">Premium disk performance</span></span>

|<span data-ttu-id="0e3d6-191">Premium Storage 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="0e3d6-191">Premium storage disk type</span></span> | <span data-ttu-id="0e3d6-192">P10</span><span class="sxs-lookup"><span data-stu-id="0e3d6-192">P10</span></span> | <span data-ttu-id="0e3d6-193">P20</span><span class="sxs-lookup"><span data-stu-id="0e3d6-193">P20</span></span> | <span data-ttu-id="0e3d6-194">P30</span><span class="sxs-lookup"><span data-stu-id="0e3d6-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0e3d6-195">디스크 크기(반올림)</span><span class="sxs-lookup"><span data-stu-id="0e3d6-195">Disk size (round up)</span></span> | <span data-ttu-id="0e3d6-196">128GB</span><span class="sxs-lookup"><span data-stu-id="0e3d6-196">128 GB</span></span> | <span data-ttu-id="0e3d6-197">512GB</span><span class="sxs-lookup"><span data-stu-id="0e3d6-197">512 GB</span></span> | <span data-ttu-id="0e3d6-198">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="0e3d6-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="0e3d6-199">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="0e3d6-199">IOPS per disk</span></span> | <span data-ttu-id="0e3d6-200">500</span><span class="sxs-lookup"><span data-stu-id="0e3d6-200">500</span></span> | <span data-ttu-id="0e3d6-201">2,300</span><span class="sxs-lookup"><span data-stu-id="0e3d6-201">2,300</span></span> | <span data-ttu-id="0e3d6-202">5,000</span><span class="sxs-lookup"><span data-stu-id="0e3d6-202">5,000</span></span> |
<span data-ttu-id="0e3d6-203">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="0e3d6-203">Throughput per disk</span></span> | <span data-ttu-id="0e3d6-204">100MB/초</span><span class="sxs-lookup"><span data-stu-id="0e3d6-204">100 MB/s</span></span> | <span data-ttu-id="0e3d6-205">150MB/초</span><span class="sxs-lookup"><span data-stu-id="0e3d6-205">150 MB/s</span></span> | <span data-ttu-id="0e3d6-206">200MB/s</span><span class="sxs-lookup"><span data-stu-id="0e3d6-206">200 MB/s</span></span> |

<span data-ttu-id="0e3d6-207">위의 표에 디스크당 최대 IOPS가 나와 있지만 여러 데이터 디스크를 스트라이프하여 더 높은 수준의 성능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="0e3d6-208">예를 들어 64 데이터 디스크는 Standard_GS5 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="0e3d6-209">이러한 각 디스크는 P30에 해당하는 크기이며 최대 80,000 IOPS를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="0e3d6-210">VM당 최대 IOPS에 대한 자세한 내용은 [Linux VM 크기](./sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="0e3d6-211">디스크 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="0e3d6-211">Create and attach disks</span></span>

<span data-ttu-id="0e3d6-212">이 자습서의 예제를 완료하려면 기존 가상 컴퓨터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="0e3d6-213">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="0e3d6-214">이 자습서를 진행할 때 필요한 경우 리소스 그룹 및 VM 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="0e3d6-215">[New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig)를 사용하여 초기 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="0e3d6-216">다음 예제에서는 크기가 128GB인 디스크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="0e3d6-217">[New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) 명령을 사용하여 데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="0e3d6-218">[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 명령을 사용하여 데이터 디스크를 추가할 가상 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="0e3d6-219">[Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 명령을 사용하여 데이터 디스크를 가상 컴퓨터 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="0e3d6-220">[Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 명령을 사용하여 가상 컴퓨터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="0e3d6-221">데이터 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="0e3d6-221">Prepare data disks</span></span>

<span data-ttu-id="0e3d6-222">디스크가 가상 컴퓨터에 연결된 후 디스크를 사용하도록 운영 체제를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="0e3d6-223">다음 예제에서는 VM에 추가된 첫 번째 디스크를 수동으로 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="0e3d6-224">[사용자 지정 스크립트 확장](./tutorial-automate-vm-deployment.md)을 사용하여 이 프로세스를 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="0e3d6-225">수동 구성</span><span class="sxs-lookup"><span data-stu-id="0e3d6-225">Manual configuration</span></span>

<span data-ttu-id="0e3d6-226">가상 컴퓨터와 RDP 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="0e3d6-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="0e3d6-227">PowerShell을 열고 이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="0e3d6-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e3d6-228">Next steps</span></span>

<span data-ttu-id="0e3d6-229">이 자습서에서는 다음과 같은 VM 디스크 항목에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e3d6-230">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="0e3d6-231">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-231">Data disks</span></span>
> * <span data-ttu-id="0e3d6-232">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="0e3d6-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="0e3d6-233">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="0e3d6-233">Disk performance</span></span>
> * <span data-ttu-id="0e3d6-234">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="0e3d6-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="0e3d6-235">VM 구성 자동화에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e3d6-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e3d6-236">VM 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="0e3d6-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
