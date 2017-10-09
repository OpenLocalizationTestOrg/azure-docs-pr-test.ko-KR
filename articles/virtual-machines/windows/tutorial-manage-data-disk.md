---
title: "Azure PowerShell hello로 aaaManage Azure 디스크 | Microsoft Docs"
description: "자습서-hello Azure PowerShell로 Azure 디스크 관리"
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="4dc6c-103">PowerShell을 사용하여 Azure 디스크 관리</span><span class="sxs-lookup"><span data-stu-id="4dc6c-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="4dc6c-104">Azure 가상 컴퓨터 디스크 toostore hello Vm 운영 체제, 응용 프로그램 및 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="4dc6c-105">VM을 만들 때 중요 한 toochoose 디스크 크기 및 구성 필요 합니다. 적절 한 toohello 작업 부하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="4dc6c-106">이 자습서에서는 VM 디스크의 배포 및 관리에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="4dc6c-107">다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4dc6c-108">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="4dc6c-109">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-109">Data disks</span></span>
> * <span data-ttu-id="4dc6c-110">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="4dc6c-111">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="4dc6c-111">Disk performance</span></span>
> * <span data-ttu-id="4dc6c-112">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="4dc6c-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="4dc6c-113">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="4dc6c-114">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="4dc6c-115">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="4dc6c-116">기본 Azure 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-116">Default Azure disks</span></span>

<span data-ttu-id="4dc6c-117">Azure 가상 컴퓨터를 만들면 두 디스크는 자동으로 연결 된 toohello 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="4dc6c-118">**운영 체제 디스크** -운영 체제 디스크를 too1 테라바이트 크기를 조정할 수 및 호스트 hello Vm 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="4dc6c-119">hello OS 디스크의 드라이브 문자 할당 *c:* 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="4dc6c-120">hello 디스크 캐싱 구성 hello OS 디스크의 운영 체제 성능을 위해 최적화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="4dc6c-121">hello OS 디스크 **없는** 응용 프로그램이 나 데이터를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="4dc6c-122">응용 프로그램 및 데이터는 데이터 디스크를 사용하며 여기에 대해서는 이 문서의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="4dc6c-123">**임시 디스크** -임시 디스크에 있는 반도체 드라이브를 사용 하 여 hello에 hello VM과 동일한 Azure 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="4dc6c-124">임시 디스크는 성능이 높고 임시 데이터 처리 등의 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="4dc6c-125">그러나 이동된 tooa 새 호스트가 hello VM을 사용 하는 경우 임시 디스크에 저장 된 모든 데이터가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="4dc6c-126">hello 임시 디스크의 hello 크기는 hello VM 크기에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="4dc6c-127">임시 디스크는 기본적으로 *d:* 드라이브 문자가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="4dc6c-128">임시 디스크 크기</span><span class="sxs-lookup"><span data-stu-id="4dc6c-128">Temporary disk sizes</span></span>

| <span data-ttu-id="4dc6c-129">형식</span><span class="sxs-lookup"><span data-stu-id="4dc6c-129">Type</span></span> | <span data-ttu-id="4dc6c-130">VM 크기</span><span class="sxs-lookup"><span data-stu-id="4dc6c-130">VM Size</span></span> | <span data-ttu-id="4dc6c-131">최대 임시 디스크 크기(GB)</span><span class="sxs-lookup"><span data-stu-id="4dc6c-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="4dc6c-132">범용</span><span class="sxs-lookup"><span data-stu-id="4dc6c-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="4dc6c-133">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-133">A and D series</span></span> | <span data-ttu-id="4dc6c-134">800</span><span class="sxs-lookup"><span data-stu-id="4dc6c-134">800</span></span> |
| [<span data-ttu-id="4dc6c-135">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="4dc6c-136">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-136">F series</span></span> | <span data-ttu-id="4dc6c-137">800</span><span class="sxs-lookup"><span data-stu-id="4dc6c-137">800</span></span> |
| [<span data-ttu-id="4dc6c-138">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="4dc6c-139">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-139">D and G series</span></span> | <span data-ttu-id="4dc6c-140">6144</span><span class="sxs-lookup"><span data-stu-id="4dc6c-140">6144</span></span> |
| [<span data-ttu-id="4dc6c-141">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="4dc6c-142">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-142">L series</span></span> | <span data-ttu-id="4dc6c-143">5630</span><span class="sxs-lookup"><span data-stu-id="4dc6c-143">5630</span></span> |
| [<span data-ttu-id="4dc6c-144">GPU</span><span class="sxs-lookup"><span data-stu-id="4dc6c-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="4dc6c-145">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-145">N series</span></span> | <span data-ttu-id="4dc6c-146">1,440</span><span class="sxs-lookup"><span data-stu-id="4dc6c-146">1440</span></span> |
| [<span data-ttu-id="4dc6c-147">고성능</span><span class="sxs-lookup"><span data-stu-id="4dc6c-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="4dc6c-148">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-148">A and H series</span></span> | <span data-ttu-id="4dc6c-149">2000</span><span class="sxs-lookup"><span data-stu-id="4dc6c-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="4dc6c-150">Azure 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-150">Azure data disks</span></span>

<span data-ttu-id="4dc6c-151">응용 프로그램을 설치하고 데이터를 저장하기 위해 데이터 디스크를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="4dc6c-152">데이터 디스크는 지속형 및 반응형 데이터 저장소가 필요한 상황에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="4dc6c-153">각 데이터 디스크의 최대 용량은 1테라바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="4dc6c-154">hello 크기 hello 가상 컴퓨터의 데이터 디스크 수는 연결 된 tooa VM 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="4dc6c-155">각 VM 코어에 대해 두 개의 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="4dc6c-156">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="4dc6c-156">Max data disks per VM</span></span>

| <span data-ttu-id="4dc6c-157">형식</span><span class="sxs-lookup"><span data-stu-id="4dc6c-157">Type</span></span> | <span data-ttu-id="4dc6c-158">VM 크기</span><span class="sxs-lookup"><span data-stu-id="4dc6c-158">VM Size</span></span> | <span data-ttu-id="4dc6c-159">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="4dc6c-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="4dc6c-160">범용</span><span class="sxs-lookup"><span data-stu-id="4dc6c-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="4dc6c-161">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-161">A and D series</span></span> | <span data-ttu-id="4dc6c-162">32</span><span class="sxs-lookup"><span data-stu-id="4dc6c-162">32</span></span> |
| [<span data-ttu-id="4dc6c-163">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="4dc6c-164">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-164">F series</span></span> | <span data-ttu-id="4dc6c-165">32</span><span class="sxs-lookup"><span data-stu-id="4dc6c-165">32</span></span> |
| [<span data-ttu-id="4dc6c-166">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="4dc6c-167">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-167">D and G series</span></span> | <span data-ttu-id="4dc6c-168">64</span><span class="sxs-lookup"><span data-stu-id="4dc6c-168">64</span></span> |
| [<span data-ttu-id="4dc6c-169">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="4dc6c-170">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-170">L series</span></span> | <span data-ttu-id="4dc6c-171">64</span><span class="sxs-lookup"><span data-stu-id="4dc6c-171">64</span></span> |
| [<span data-ttu-id="4dc6c-172">GPU</span><span class="sxs-lookup"><span data-stu-id="4dc6c-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="4dc6c-173">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-173">N series</span></span> | <span data-ttu-id="4dc6c-174">48</span><span class="sxs-lookup"><span data-stu-id="4dc6c-174">48</span></span> |
| [<span data-ttu-id="4dc6c-175">고성능</span><span class="sxs-lookup"><span data-stu-id="4dc6c-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="4dc6c-176">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="4dc6c-176">A and H series</span></span> | <span data-ttu-id="4dc6c-177">32</span><span class="sxs-lookup"><span data-stu-id="4dc6c-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="4dc6c-178">VM 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="4dc6c-178">VM disk types</span></span>

<span data-ttu-id="4dc6c-179">Azure는 두 가지 유형의 디스크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="4dc6c-180">표준 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-180">Standard disk</span></span>

<span data-ttu-id="4dc6c-181">Standard Storage는 HDD에 의해 지원되며 성능은 그대로이면서 비용 효율적인 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="4dc6c-182">표준 디스크는 비용 효율적인 개발 및 테스트 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="4dc6c-183">프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-183">Premium disk</span></span>

<span data-ttu-id="4dc6c-184">프리미엄 디스크는 SSD 기반 고성능의 대기 시간이 짧은 디스크에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="4dc6c-185">프로덕션 워크로드를 실행하는 VM에 완벽한 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="4dc6c-186">Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 FS 시리즈 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="4dc6c-187">프리미엄 디스크 세 가지 유형 (P10, P20, P30)을 hello 디스크의 크기 hello hello 디스크 형식을 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="4dc6c-188">선택 하 고, 디스크 크기 hello 값 toohello 다음 형식으로 반올림 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="4dc6c-189">예를 들어 hello 크기는 128GB hello 디스크 유형 아래 됩니다 P10, 129 및 512 P20, 사이의 P30 512 개.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="4dc6c-190">프리미엄 디스크 성능</span><span class="sxs-lookup"><span data-stu-id="4dc6c-190">Premium disk performance</span></span>

|<span data-ttu-id="4dc6c-191">Premium Storage 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="4dc6c-191">Premium storage disk type</span></span> | <span data-ttu-id="4dc6c-192">P10</span><span class="sxs-lookup"><span data-stu-id="4dc6c-192">P10</span></span> | <span data-ttu-id="4dc6c-193">P20</span><span class="sxs-lookup"><span data-stu-id="4dc6c-193">P20</span></span> | <span data-ttu-id="4dc6c-194">P30</span><span class="sxs-lookup"><span data-stu-id="4dc6c-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4dc6c-195">디스크 크기(반올림)</span><span class="sxs-lookup"><span data-stu-id="4dc6c-195">Disk size (round up)</span></span> | <span data-ttu-id="4dc6c-196">128GB</span><span class="sxs-lookup"><span data-stu-id="4dc6c-196">128 GB</span></span> | <span data-ttu-id="4dc6c-197">512GB</span><span class="sxs-lookup"><span data-stu-id="4dc6c-197">512 GB</span></span> | <span data-ttu-id="4dc6c-198">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="4dc6c-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="4dc6c-199">디스크당 IOPS</span><span class="sxs-lookup"><span data-stu-id="4dc6c-199">IOPS per disk</span></span> | <span data-ttu-id="4dc6c-200">500</span><span class="sxs-lookup"><span data-stu-id="4dc6c-200">500</span></span> | <span data-ttu-id="4dc6c-201">2,300</span><span class="sxs-lookup"><span data-stu-id="4dc6c-201">2,300</span></span> | <span data-ttu-id="4dc6c-202">5,000</span><span class="sxs-lookup"><span data-stu-id="4dc6c-202">5,000</span></span> |
<span data-ttu-id="4dc6c-203">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="4dc6c-203">Throughput per disk</span></span> | <span data-ttu-id="4dc6c-204">100MB/초</span><span class="sxs-lookup"><span data-stu-id="4dc6c-204">100 MB/s</span></span> | <span data-ttu-id="4dc6c-205">150MB/초</span><span class="sxs-lookup"><span data-stu-id="4dc6c-205">150 MB/s</span></span> | <span data-ttu-id="4dc6c-206">200MB/s</span><span class="sxs-lookup"><span data-stu-id="4dc6c-206">200 MB/s</span></span> |

<span data-ttu-id="4dc6c-207">테이블 위에 hello 디스크당 최대 IOPS를 식별 하는 동안에 더 높은 수준의 성능 여러 데이터 디스크를 스트라이프 하 여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="4dc6c-208">예를 들어, 64 데이터 디스크 수 tooStandard_GS5 VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="4dc6c-209">이러한 각 디스크는 P30에 해당하는 크기이며 최대 80,000 IOPS를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="4dc6c-210">VM당 최대 IOPS에 대한 자세한 내용은 [Linux VM 크기](./sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="4dc6c-211">디스크 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="4dc6c-211">Create and attach disks</span></span>

<span data-ttu-id="4dc6c-212">이 자습서에서는 toocomplete hello 예제에서는 기존 가상 컴퓨터 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="4dc6c-213">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="4dc6c-214">Hello 자습서를 통해 작업 대체 필요한 경우 hello 리소스 그룹 및 VM 이름 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="4dc6c-215">Hello와 초기 구성 만들기 [새로 AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="4dc6c-216">다음 예에서는 hello 디스크 128 기가바이트 크기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="4dc6c-217">Hello로 hello 데이터 디스크를 만들 [새로 AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="4dc6c-218">Get hello 가상 컴퓨터가 원하는 tooadd hello 데이터 디스크 toowith hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="4dc6c-219">추가 hello 데이터 디스크 toohello 인 가상 컴퓨터 구성 hello [추가 AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="4dc6c-220">Hello로 hello 가상 컴퓨터를 업데이트 [업데이트 AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="4dc6c-221">데이터 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="4dc6c-221">Prepare data disks</span></span>

<span data-ttu-id="4dc6c-222">디스크에 대 한 연결 된 toohello 가상 컴퓨터를 수행한 hello 운영 체제 구성 toobe toouse hello 디스크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="4dc6c-223">hello 다음 예제에서는 toomanually 추가 hello 첫 번째 디스크를 구성 하는 방법 toohello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="4dc6c-224">Hello를 사용 하 여이 프로세스 자동화할 수도 있습니다 [사용자 지정 스크립트 확장](./tutorial-automate-vm-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="4dc6c-225">수동 구성</span><span class="sxs-lookup"><span data-stu-id="4dc6c-225">Manual configuration</span></span>

<span data-ttu-id="4dc6c-226">Hello 가상 컴퓨터에 대 한 RDP 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="4dc6c-227">PowerShell을 열고 이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="4dc6c-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4dc6c-228">Next steps</span></span>

<span data-ttu-id="4dc6c-229">이 자습서에서는 다음과 같은 VM 디스크 항목에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4dc6c-230">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="4dc6c-231">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-231">Data disks</span></span>
> * <span data-ttu-id="4dc6c-232">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="4dc6c-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="4dc6c-233">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="4dc6c-233">Disk performance</span></span>
> * <span data-ttu-id="4dc6c-234">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="4dc6c-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="4dc6c-235">VM 구성을 자동화 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc6c-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4dc6c-236">VM 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="4dc6c-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
