---
title: "hello Azure CLI로 aaaManage Azure 디스크 | Microsoft Docs"
description: "자습서-Azure CLI hello로 Azure 디스크 관리"
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="8975b-103">Hello Azure CLI로 Azure 디스크 관리</span><span class="sxs-lookup"><span data-stu-id="8975b-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="8975b-104">Azure 가상 컴퓨터 디스크 toostore hello Vm 운영 체제, 응용 프로그램 및 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="8975b-105">VM을 만들 때 중요 한 toochoose 디스크 크기 및 구성 필요 합니다. 적절 한 toohello 작업 부하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="8975b-106">이 자습서에서는 VM 디스크의 배포 및 관리에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="8975b-107">다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8975b-108">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="8975b-109">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-109">Data disks</span></span>
> * <span data-ttu-id="8975b-110">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="8975b-111">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="8975b-111">Disk performance</span></span>
> * <span data-ttu-id="8975b-112">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="8975b-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="8975b-113">디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8975b-113">Resizing disks</span></span>
> * <span data-ttu-id="8975b-114">디스크 스냅숏</span><span class="sxs-lookup"><span data-stu-id="8975b-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8975b-115">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="8975b-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8975b-116">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8975b-117">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="8975b-118">기본 Azure 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-118">Default Azure disks</span></span>

<span data-ttu-id="8975b-119">Azure 가상 컴퓨터를 만들면 두 디스크는 자동으로 연결 된 toohello 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="8975b-120">**운영 체제 디스크** -운영 체제 디스크를 too1 테라바이트 크기를 조정할 수 및 호스트 hello Vm 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="8975b-121">hello OS 디스크 레이블이 */개발/sda* 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="8975b-122">hello 디스크 캐싱 구성 hello OS 디스크의 운영 체제 성능을 위해 최적화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="8975b-123">이 구성으로 인해 OS 디스크 hello **없는** 응용 프로그램이 나 데이터를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="8975b-124">응용 프로그램 및 데이터는 데이터 디스크를 사용하며 여기에 대해서는 이 문서의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="8975b-125">**임시 디스크** -임시 디스크에 있는 반도체 드라이브를 사용 하 여 hello에 hello VM과 동일한 Azure 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="8975b-126">임시 디스크는 성능이 높고 임시 데이터 처리 등의 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="8975b-127">그러나 이동된 tooa 새 호스트가 hello VM을 사용 하는 경우 임시 디스크에 저장 된 모든 데이터가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="8975b-128">hello 임시 디스크의 hello 크기는 hello VM 크기에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="8975b-129">임시 디스크는 */dev/sdb*로 레이블이 지정되고 탑재 지점은 */mnt*입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="8975b-130">임시 디스크 크기</span><span class="sxs-lookup"><span data-stu-id="8975b-130">Temporary disk sizes</span></span>

| <span data-ttu-id="8975b-131">형식</span><span class="sxs-lookup"><span data-stu-id="8975b-131">Type</span></span> | <span data-ttu-id="8975b-132">VM 크기</span><span class="sxs-lookup"><span data-stu-id="8975b-132">VM Size</span></span> | <span data-ttu-id="8975b-133">최대 임시 디스크 크기(GB)</span><span class="sxs-lookup"><span data-stu-id="8975b-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="8975b-134">범용</span><span class="sxs-lookup"><span data-stu-id="8975b-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="8975b-135">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-135">A and D series</span></span> | <span data-ttu-id="8975b-136">800</span><span class="sxs-lookup"><span data-stu-id="8975b-136">800</span></span> |
| [<span data-ttu-id="8975b-137">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="8975b-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="8975b-138">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-138">F series</span></span> | <span data-ttu-id="8975b-139">800</span><span class="sxs-lookup"><span data-stu-id="8975b-139">800</span></span> |
| [<span data-ttu-id="8975b-140">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="8975b-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="8975b-141">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-141">D and G series</span></span> | <span data-ttu-id="8975b-142">6144</span><span class="sxs-lookup"><span data-stu-id="8975b-142">6144</span></span> |
| [<span data-ttu-id="8975b-143">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="8975b-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="8975b-144">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-144">L series</span></span> | <span data-ttu-id="8975b-145">5630</span><span class="sxs-lookup"><span data-stu-id="8975b-145">5630</span></span> |
| [<span data-ttu-id="8975b-146">GPU</span><span class="sxs-lookup"><span data-stu-id="8975b-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="8975b-147">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-147">N series</span></span> | <span data-ttu-id="8975b-148">1,440</span><span class="sxs-lookup"><span data-stu-id="8975b-148">1440</span></span> |
| [<span data-ttu-id="8975b-149">고성능</span><span class="sxs-lookup"><span data-stu-id="8975b-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8975b-150">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-150">A and H series</span></span> | <span data-ttu-id="8975b-151">2000</span><span class="sxs-lookup"><span data-stu-id="8975b-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="8975b-152">Azure 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-152">Azure data disks</span></span>

<span data-ttu-id="8975b-153">응용 프로그램을 설치하고 데이터를 저장하기 위해 데이터 디스크를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="8975b-154">데이터 디스크는 지속형 및 반응형 데이터 저장소가 필요한 상황에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="8975b-155">각 데이터 디스크의 최대 용량은 1테라바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="8975b-156">hello 크기 hello 가상 컴퓨터의 데이터 디스크 수는 연결 된 tooa VM 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="8975b-157">각 VM 코어에 대해 두 개의 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="8975b-158">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="8975b-158">Max data disks per VM</span></span>

| <span data-ttu-id="8975b-159">형식</span><span class="sxs-lookup"><span data-stu-id="8975b-159">Type</span></span> | <span data-ttu-id="8975b-160">VM 크기</span><span class="sxs-lookup"><span data-stu-id="8975b-160">VM Size</span></span> | <span data-ttu-id="8975b-161">VM당 최대 데이터 디스크 수</span><span class="sxs-lookup"><span data-stu-id="8975b-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="8975b-162">범용</span><span class="sxs-lookup"><span data-stu-id="8975b-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="8975b-163">A 및 D 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-163">A and D series</span></span> | <span data-ttu-id="8975b-164">32</span><span class="sxs-lookup"><span data-stu-id="8975b-164">32</span></span> |
| [<span data-ttu-id="8975b-165">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="8975b-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="8975b-166">F 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-166">F series</span></span> | <span data-ttu-id="8975b-167">32</span><span class="sxs-lookup"><span data-stu-id="8975b-167">32</span></span> |
| [<span data-ttu-id="8975b-168">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="8975b-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="8975b-169">D 및 G 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-169">D and G series</span></span> | <span data-ttu-id="8975b-170">64</span><span class="sxs-lookup"><span data-stu-id="8975b-170">64</span></span> |
| [<span data-ttu-id="8975b-171">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="8975b-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="8975b-172">L 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-172">L series</span></span> | <span data-ttu-id="8975b-173">64</span><span class="sxs-lookup"><span data-stu-id="8975b-173">64</span></span> |
| [<span data-ttu-id="8975b-174">GPU</span><span class="sxs-lookup"><span data-stu-id="8975b-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="8975b-175">N 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-175">N series</span></span> | <span data-ttu-id="8975b-176">48</span><span class="sxs-lookup"><span data-stu-id="8975b-176">48</span></span> |
| [<span data-ttu-id="8975b-177">고성능</span><span class="sxs-lookup"><span data-stu-id="8975b-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8975b-178">A 및 H 시리즈</span><span class="sxs-lookup"><span data-stu-id="8975b-178">A and H series</span></span> | <span data-ttu-id="8975b-179">32</span><span class="sxs-lookup"><span data-stu-id="8975b-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="8975b-180">VM 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="8975b-180">VM disk types</span></span>

<span data-ttu-id="8975b-181">Azure는 두 가지 유형의 디스크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="8975b-182">표준 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-182">Standard disk</span></span>

<span data-ttu-id="8975b-183">Standard Storage는 HDD에 의해 지원되며 성능은 그대로이면서 비용 효율적인 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="8975b-184">표준 디스크는 비용 효율적인 개발 및 테스트 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="8975b-185">프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-185">Premium disk</span></span>

<span data-ttu-id="8975b-186">프리미엄 디스크는 SSD 기반 고성능의 대기 시간이 짧은 디스크에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="8975b-187">프로덕션 워크로드를 실행하는 VM에 완벽한 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="8975b-188">Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 FS 시리즈 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="8975b-189">프리미엄 디스크 세 가지 유형 (P10, P20, P30)을 hello 디스크의 크기 hello hello 디스크 형식을 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="8975b-190">선택 하 고, 디스크 크기 hello 값 toohello 다음 형식으로 반올림 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="8975b-191">예를 들어 hello 디스크 크기가 128 g B 미만인 경우 hello 디스크 유형 P10입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="8975b-192">Hello 디스크 크기 129 GB와 512GB 사이 있으면 hello 크기는 P20는입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="8975b-193">아무 것도 512GB 넘는 hello 크기는는 P30 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="8975b-194">프리미엄 디스크 성능</span><span class="sxs-lookup"><span data-stu-id="8975b-194">Premium disk performance</span></span>

|<span data-ttu-id="8975b-195">Premium Storage 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="8975b-195">Premium storage disk type</span></span> | <span data-ttu-id="8975b-196">P10</span><span class="sxs-lookup"><span data-stu-id="8975b-196">P10</span></span> | <span data-ttu-id="8975b-197">P20</span><span class="sxs-lookup"><span data-stu-id="8975b-197">P20</span></span> | <span data-ttu-id="8975b-198">P30</span><span class="sxs-lookup"><span data-stu-id="8975b-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8975b-199">디스크 크기(반올림)</span><span class="sxs-lookup"><span data-stu-id="8975b-199">Disk size (round up)</span></span> | <span data-ttu-id="8975b-200">128GB</span><span class="sxs-lookup"><span data-stu-id="8975b-200">128 GB</span></span> | <span data-ttu-id="8975b-201">512GB</span><span class="sxs-lookup"><span data-stu-id="8975b-201">512 GB</span></span> | <span data-ttu-id="8975b-202">1,024GB(1TB)</span><span class="sxs-lookup"><span data-stu-id="8975b-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="8975b-203">디스크당 최대 IOPS</span><span class="sxs-lookup"><span data-stu-id="8975b-203">Max IOPS per disk</span></span> | <span data-ttu-id="8975b-204">500</span><span class="sxs-lookup"><span data-stu-id="8975b-204">500</span></span> | <span data-ttu-id="8975b-205">2,300</span><span class="sxs-lookup"><span data-stu-id="8975b-205">2,300</span></span> | <span data-ttu-id="8975b-206">5,000</span><span class="sxs-lookup"><span data-stu-id="8975b-206">5,000</span></span> |
<span data-ttu-id="8975b-207">디스크당 처리량</span><span class="sxs-lookup"><span data-stu-id="8975b-207">Throughput per disk</span></span> | <span data-ttu-id="8975b-208">100MB/초</span><span class="sxs-lookup"><span data-stu-id="8975b-208">100 MB/s</span></span> | <span data-ttu-id="8975b-209">150MB/초</span><span class="sxs-lookup"><span data-stu-id="8975b-209">150 MB/s</span></span> | <span data-ttu-id="8975b-210">200MB/s</span><span class="sxs-lookup"><span data-stu-id="8975b-210">200 MB/s</span></span> |

<span data-ttu-id="8975b-211">테이블 위에 hello 디스크당 최대 IOPS를 식별 하는 동안에 더 높은 수준의 성능 여러 데이터 디스크를 스트라이프 하 여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="8975b-212">예를 들어 Standard_GS5 VM은 최대 80,000 IOPS를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="8975b-213">VM당 최대 IOPS에 대한 자세한 내용은 [Linux VM 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8975b-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="8975b-214">디스크 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="8975b-214">Create and attach disks</span></span>

<span data-ttu-id="8975b-215">데이터 디스크를 만들고 VM 생성 시간 또는 tooan 기존 VM에 연결 된 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="8975b-216">VM을 만들 때 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="8975b-216">Attach disk at VM creation</span></span>

<span data-ttu-id="8975b-217">Hello로 리소스 그룹 만들기 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="8975b-218">Hello를 사용 하 여 VM 만들기 [az vm 만들기]( /cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="8975b-219">hello `--datadisk-sizes-gb` 인수는 사용 되는 toospecify 추가 디스크는 만들어야 하며 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="8975b-220">toocreate 둘 이상의 디스크를 연결 하 고, 디스크 크기 값은 공백으로 구분 된 목록을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="8975b-221">다음 예제는 hello, VM 두 개의 데이터 디스크를 모두 128GB 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="8975b-222">Hello 디스크 크기는 128GB 이기 때문에 이러한 디스크 둘 다 P10s 500 최대 디스크 IOPS를 제공 하는로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="8975b-223">디스크 tooexisting VM 연결</span><span class="sxs-lookup"><span data-stu-id="8975b-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="8975b-224">toocreate hello를 사용 하 여, 새 디스크 tooan 기존 가상 컴퓨터를 연결 하 고 [az vm 디스크를 연결](/cli/azure/vm/disk#attach) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="8975b-225">hello 다음 예제에서는 128gb 크기에서 프리미엄 디스크를 만들고 toohello hello 마지막 단계에서 만든 VM에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="8975b-226">데이터 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="8975b-226">Prepare data disks</span></span>

<span data-ttu-id="8975b-227">디스크에 대 한 연결 된 toohello 가상 컴퓨터를 수행한 hello 운영 체제 구성 toobe toouse hello 디스크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="8975b-228">다음 예제는 hello toomanually 디스크를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="8975b-229">이 프로세스는 cloud-init를 사용하여 자동화할 수도 있으며 여기에 대해서는 [이후의 자습서](./tutorial-automate-vm-deployment.md)에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="8975b-230">수동 구성</span><span class="sxs-lookup"><span data-stu-id="8975b-230">Manual configuration</span></span>

<span data-ttu-id="8975b-231">Hello 가상 컴퓨터와 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="8975b-232">Hello hello 가상 컴퓨터의 공용 IP로 hello 예제 IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="8975b-233">파티션에 hello 디스크 `fdisk`합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="8975b-234">Hello를 사용 하 여 파일 시스템 toohello 파티션을 작성 `mkfs` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="8975b-235">Hello 운영 체제에 액세스할 수 있도록 hello 새 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="8975b-236">hello를 통해 이제 hello 디스크에 액세스할 수 *datadrive* hello를 실행 하 여 확인할 수 있는 탑재 지점, `df -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="8975b-237">hello 출력과 hello 새 드라이브에 탑재 된 */datadrive*합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="8975b-238">다시 부팅 한 후 다시 탑재 될 드라이브 hello tooensure, toohello 추가 해야 */등/fstab* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="8975b-239">toodo hello로 hello hello 디스크의 UUID를 따라서가 `blkid` 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="8975b-240">hello hello 드라이브의 UUID를 표시 하는 hello 출력 `/dev/sdc1` 이 경우.</span><span class="sxs-lookup"><span data-stu-id="8975b-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="8975b-241">Toohello 다음 줄 비슷한 toohello 추가 */등/fstab* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="8975b-242">*barrier=0*을 사용하여 쓰기 장벽을 사용하지 않도록 설정할 수 있으며 이 구성으로 디스크 성능이 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="8975b-243">Hello 디스크에 구성 된 했으므로 hello SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="8975b-244">VM 디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8975b-244">Resize VM disk</span></span>

<span data-ttu-id="8975b-245">VM이 배포 된 후 모든 연결 된 데이터 디스크 또는 hello 운영 체제 디스크 크기가 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="8975b-246">더 많은 저장 공간이 또는 더 높은 수준의 성능 (P10, P20, P30) 확장이 필요할 때 디스크의 hello 크기 증가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="8975b-247">디스크 크기를 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="8975b-248">디스크 크기를 증가 하기 전에 Id hello 또는 hello 디스크의 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="8975b-249">사용 하 여 hello [az 디스크 목록](/cli/azure/vm/disk#list) 명령 tooreturn 모든 리소스 그룹의 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="8975b-250">Hello 디스크 이름을 기록해 싶다는 의사를 tooresize 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="8975b-251">hello VM 할당이 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="8975b-252">사용 하 여 hello [az vm 할당을 취소]( /cli/azure/vm#deallocate) toostop 명령 및 hello VM 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="8975b-253">사용 하 여 hello [az 디스크 업데이트](/cli/azure/vm/disk#update) 명령 tooresize hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="8975b-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="8975b-254">이 예제에서는 명명 된 디스크의 크기를 조정 *myDataDisk* too1 테라바이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="8975b-255">Hello 크기 조정 작업이 완료 되 면 hello VM을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="8975b-256">Hello 운영 체제 디스크 크기를 조정 했습니다 hello 파티션이 자동으로 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="8975b-257">현재 파티션에서 데이터 디스크 크기를 조정 했습니다 하면 toobe hello Vm 운영 체제에서 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="8975b-258">스냅숏 Azure 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-258">Snapshot Azure disks</span></span>

<span data-ttu-id="8975b-259">디스크 스냅숏을 만드는 hello 디스크의 읽기 전용, 지정 시간 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="8975b-260">Azure VM 스냅숏은 구성을 변경 하기 전에 VM의 hello 상태를 신속 하 게 저장 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="8975b-261">Hello 이벤트에서 hello 구성 변경 내용을 증명 toobe 의도 하지 않은, hello 스냅숏을 사용 하 여 VM 상태를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="8975b-262">Hello와 독립적으로 각 디스크의 스냅숏을 VM에 하나 이상의 디스크가 있는 경우 다른 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="8975b-263">응용 프로그램 일치 백업을 만들도록, 디스크에 대 한 스냅숏을 하기 전에 hello VM을 중지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="8975b-264">또는 hello를 사용 하 여 [Azure 백업 서비스](/azure/backup/), 있습니다 tooperform 자동 백업 중 VM이 실행 되 고 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="8975b-265">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="8975b-265">Create snapshot</span></span>

<span data-ttu-id="8975b-266">가상 컴퓨터 디스크 스냅숏을 만들기 전에 hello Id 또는 hello 디스크의 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="8975b-267">사용 하 여 hello [az vm 표시](https://docs.microsoft.com/en-us/cli/azure/vm#show) 명령 tooreturn hello 디스크 id입니다. 이 예제에서는 hello 디스크 id는 이후 단계에서 사용할 수 있도록 변수에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="8975b-268">Hello 가상 컴퓨터 디스크의 hello id를가지고 hello 다음 명령은 hello 디스크의 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="8975b-269">스냅숏에서 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="8975b-269">Create disk from snapshot</span></span>

<span data-ttu-id="8975b-270">이 스냅숏은 사용 하는 toorecreate hello 가상 컴퓨터 하나일 수 있습니다를 디스크에 다음 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="8975b-271">스냅숏에서 가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="8975b-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="8975b-272">delete hello 기존 가상 컴퓨터 toodemonstrate 가상 컴퓨터 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="8975b-273">Hello 스냅숏 디스크에서 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="8975b-274">데이터 디스크 다시 연결</span><span class="sxs-lookup"><span data-stu-id="8975b-274">Reattach data disk</span></span>

<span data-ttu-id="8975b-275">모든 데이터 디스크를 다시 연결 toobe toohello 가상 컴퓨터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="8975b-276">먼저 hello를 사용 하 여 hello 데이터 디스크 이름의 찾을 [az 디스크 목록](https://docs.microsoft.com/cli/azure/disk#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="8975b-277">이 예에서는 위치 hello 라는 변수에 hello 디스크의 이름을 *datadisk*, hello 다음 단계에서 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="8975b-278">사용 하 여 hello [az vm 디스크를 연결](https://docs.microsoft.com/cli/azure/vm/disk#attach) 명령 tooattach hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="8975b-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="8975b-279">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8975b-279">Next steps</span></span>

<span data-ttu-id="8975b-280">이 자습서에서는 다음과 같은 VM 디스크 항목에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8975b-281">OS 디스크 및 임시 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="8975b-282">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-282">Data disks</span></span>
> * <span data-ttu-id="8975b-283">표준 및 프리미엄 디스크</span><span class="sxs-lookup"><span data-stu-id="8975b-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="8975b-284">디스크 성능</span><span class="sxs-lookup"><span data-stu-id="8975b-284">Disk performance</span></span>
> * <span data-ttu-id="8975b-285">데이터 디스크 연결 및 준비</span><span class="sxs-lookup"><span data-stu-id="8975b-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="8975b-286">디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8975b-286">Resizing disks</span></span>
> * <span data-ttu-id="8975b-287">디스크 스냅숏</span><span class="sxs-lookup"><span data-stu-id="8975b-287">Disk snapshots</span></span>

<span data-ttu-id="8975b-288">VM 구성을 자동화 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8975b-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8975b-289">VM 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="8975b-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
