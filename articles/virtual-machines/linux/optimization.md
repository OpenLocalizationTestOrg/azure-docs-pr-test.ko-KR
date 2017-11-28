---
title: "aaaOptimize Azure에서 Linux VM | Microsoft Docs"
description: "최적의 성능을 위해서는 Azure에서 Linux VM을 설정 했는지 최적화 팁 toomake를 일부에 대해 알아봅니다"
keywords: "linux 가상 컴퓨터, 가상 컴퓨터 linux, ubuntu 가상 컴퓨터"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a><span data-ttu-id="728d2-104">Azure에서 Linux VM 최적화</span><span class="sxs-lookup"><span data-stu-id="728d2-104">Optimize your Linux VM on Azure</span></span>
<span data-ttu-id="728d2-105">Linux 가상 컴퓨터 (VM)를 만드는 쉽게 toodo hello 명령줄 나 hello 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-105">Creating a Linux virtual machine (VM) is easy toodo from hello command line or from hello portal.</span></span> <span data-ttu-id="728d2-106">이 자습서에서는 어떻게 tooensure 설정한 것 toooptimize 성능을 hello Microsoft Azure 플랫폼에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-106">This tutorial shows you how tooensure you have set it up toooptimize its performance on hello Microsoft Azure platform.</span></span> <span data-ttu-id="728d2-107">이 항목에서는 Ubuntu Server VM을 사용 하지만 [템플릿으로 사용자 고유의 이미지](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용하여 Linux 가상 컴퓨터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-107">This topic uses an Ubuntu Server VM, but you can also create Linux virtual machine using [your own images as templates](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="728d2-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="728d2-108">Prerequisites</span></span>
<span data-ttu-id="728d2-109">이 항목에서는 사용하는 Azure 구독([무료 평가판 등록](https://azure.microsoft.com/pricing/free-trial/))이 이미 있으며 Azure 구독에 VM을 이미 프로비전했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-109">This topic assumes you already have a working Azure subscription ([free trial signup](https://azure.microsoft.com/pricing/free-trial/)) and have already provisioned a VM into your Azure subscription.</span></span> <span data-ttu-id="728d2-110">Hello 최신 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 Azure 구독을 tooyour 로그인 [az 로그인](/cli/azure/#login) 하기 전에 [VM을 만들](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-110">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooyour Azure subscription with [az login](/cli/azure/#login) before you [create a VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="azure-os-disk"></a><span data-ttu-id="728d2-111">Azure OS 디스크</span><span class="sxs-lookup"><span data-stu-id="728d2-111">Azure OS Disk</span></span>
<span data-ttu-id="728d2-112">Azure에서 Linux VM을 만들면 이에 연결된 두 개의 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-112">Once you create a Linux VM in Azure, it has two disks associated with it.</span></span> <span data-ttu-id="728d2-113">**/dev/sda**는 OS 디스크이며 **/dev/sdb**는 임시 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-113">**/dev/sda** is your OS disk, **/dev/sdb** is your temporary disk.</span></span>  <span data-ttu-id="728d2-114">Hello 주 운영 체제 디스크를 사용 하지 마십시오 (**/개발/sda**) hello 운영 체제를 제외 하 고에 대 한 빠른 VM 부팅 시간에 최적화 된 및 작업에 대 한 좋은 성능을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-114">Do not use hello main OS disk (**/dev/sda**) for anything except hello operating system as it is optimized for fast VM boot time and does not provide good performance for your workloads.</span></span> <span data-ttu-id="728d2-115">하나 tooattach 하거나 tooyour VM tooget 영구 최적화를 위한 저장소 및 데이터 디스크를 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-115">You want tooattach one or more disks tooyour VM tooget persistent and optimized storage for your data.</span></span> 

## <a name="adding-disks-for-size-and-performance-targets"></a><span data-ttu-id="728d2-116">크기 및 성능 대상에 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="728d2-116">Adding Disks for Size and Performance targets</span></span>
<span data-ttu-id="728d2-117">Hello VM 크기에 따라, too16 추가 디스크 A 시리즈, D 시리즈 32 개의 디스크 및 too1 t B의 크기를 각각 G 시리즈 컴퓨터-64 개의 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-117">Based on hello VM size, you can attach up too16 additional disks on an A-Series, 32 disks on a D-Series and 64 disks on a G-Series machine - each up too1 TB in size.</span></span> <span data-ttu-id="728d2-118">공간 및 IOps 요구 사항에 따라 필요한 만큼 디스크를 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-118">You add extra disks as needed per your space and IOps requirements.</span></span> <span data-ttu-id="728d2-119">각 디스크에 500 IOps의 성능 목표에 대 한 표준 저장소 및 디스크당 too5000 IOps를 프리미엄 저장소에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-119">Each disk has a performance target of 500 IOps for Standard Storage and up too5000 IOps per disk for Premium Storage.</span></span>  <span data-ttu-id="728d2-120">Premium Storage에 대한 자세한 내용은 [Premium Storage: Azure VM용 고성능 저장소](../../storage/common/storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="728d2-120">For more information about Premium Storage disks, see [Premium Storage: High-Performance Storage for Azure VMs](../../storage/common/storage-premium-storage.md)</span></span>

<span data-ttu-id="728d2-121">tooachieve hello 여기서 캐시 설정을 설정한 tooeither 프리미엄 저장소 디스크에 가장 높은 IOps **ReadOnly** 또는 **None**, 사용 하지 않도록 설정 해야 **장벽을** 동안 Linux에서 hello 파일 시스템을 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-121">tooachieve hello highest IOps on Premium Storage disks where their cache settings have been set tooeither **ReadOnly** or **None**, you must disable **barriers** while mounting hello file system in Linux.</span></span> <span data-ttu-id="728d2-122">백업 된 디스크는 이러한 캐시 설정에 대 한 내구성 hello 쓰므로 tooPremium 저장소 장벽을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-122">You do not need barriers because hello writes tooPremium Storage backed disks are durable for these cache settings.</span></span>

* <span data-ttu-id="728d2-123">사용 하는 경우 **reiserFS**, 사용 안 함 장벽을 hello 마운트 옵션을 사용 하 여 `barrier=none` (장벽을 사용 하도록 설정한 사용 `barrier=flush`)</span><span class="sxs-lookup"><span data-stu-id="728d2-123">If you use **reiserFS**, disable barriers using hello mount option `barrier=none` (For enabling barriers, use `barrier=flush`)</span></span>
* <span data-ttu-id="728d2-124">사용 하는 경우 **ext3/ext4**, 사용 안 함 장벽을 hello 마운트 옵션을 사용 하 여 `barrier=0` (장벽을 사용 하도록 설정한 사용 `barrier=1`)</span><span class="sxs-lookup"><span data-stu-id="728d2-124">If you use **ext3/ext4**, disable barriers using hello mount option `barrier=0` (For enabling barriers, use `barrier=1`)</span></span>
* <span data-ttu-id="728d2-125">사용 하는 경우 **XFS**, 사용 안 함 장벽을 hello 마운트 옵션을 사용 하 여 `nobarrier` (장벽을 사용 하도록 설정 하는 것에 대 한 hello 옵션을 사용 하 여 `barrier`)</span><span class="sxs-lookup"><span data-stu-id="728d2-125">If you use **XFS**, disable barriers using hello mount option `nobarrier` (For enabling barriers, use hello option `barrier`)</span></span>

## <a name="unmanaged-storage-account-considerations"></a><span data-ttu-id="728d2-126">관리되지 않는 저장소 계정 고려 사항</span><span class="sxs-lookup"><span data-stu-id="728d2-126">Unmanaged storage account considerations</span></span>
<span data-ttu-id="728d2-127">hello 기본 동작은 Azure CLI 2.0 hello로 VM을 만들 때 toouse Azure 관리 되는 디스크를입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-127">hello default action when you create a VM with hello Azure CLI 2.0 is toouse Azure Managed Disks.</span></span>  <span data-ttu-id="728d2-128">이러한 디스크 hello Azure 플랫폼에서 처리 되 고 모든 준비 단계 또는 위치 toostore 필요 하지 않은 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-128">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span>  <span data-ttu-id="728d2-129">관리되지 않는 디스크는 저장소 계정이 필요하며 추가 성능 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-129">Unmanaged disks require a storage account and have some additional performance considerations.</span></span>  <span data-ttu-id="728d2-130">관리 디스크에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="728d2-130">For more information about managed disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>  <span data-ttu-id="728d2-131">관리 되지 않는 디스크를 사용 하는 경우에 윤곽선 성능 고려 사항 섹션을 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-131">hello following section outlines performance considerations only when you use unmanaged disks.</span></span>  <span data-ttu-id="728d2-132">기본 다시 hello 및 권장 되는 저장소 솔루션은 관리 되는 toouse 디스크.</span><span class="sxs-lookup"><span data-stu-id="728d2-132">Again, hello default and recommended storage solution is toouse managed disks.</span></span>

<span data-ttu-id="728d2-133">관리 되지 않는 디스크가 있는 VM을 만들 경우 동일한 hello에 있는 저장소 계정에서 디스크를 추가 하 고 있는지 확인 VM tooensure로 지역 가까운 및 네트워크 대기 시간을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-133">If you create a VM with unmanaged disks, make sure that you attach disks from storage accounts residing in hello same region as your VM tooensure close proximity and minimize network latency.</span></span>  <span data-ttu-id="728d2-134">각 표준 저장소 계정에는 최대 20,000IOps 및 500TB 크기의 용량이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-134">Each Standard storage account has a maximum of 20k IOps and a 500 TB size capacity.</span></span>  <span data-ttu-id="728d2-135">이 제한은 hello 운영 체제 디스크와 모든 데이터 디스크를 만들면 모두를 포함 하 여 tooapproximately 40 많이 사용 디스크 아웃 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-135">This  limit works out tooapproximately 40 heavily used disks including both hello OS disk and any data disks you create.</span></span> <span data-ttu-id="728d2-136">프리미엄 저장소 계정의 경우 최대 IOps 제한이 없지만 크기는 32TB로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-136">For Premium Storage accounts, there is no Maximum IOps limit but there is a 32 TB size limit.</span></span> 

<span data-ttu-id="728d2-137">높은 IOps 작업 및 다루는 표준 저장소 디스크를 선택한 경우 여러 저장소 계정 toomake 표준 저장소 계정에 대 한 20, 000 IOps를 제한 하는 hello 클릭 하지 있는지 간에 toosplit hello 디스크를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-137">When dealing with high IOps workloads and you have chosen Standard Storage for your disks, you might need toosplit hello disks across multiple storage accounts toomake sure you have not hit hello 20,000 IOps limit for Standard Storage accounts.</span></span> <span data-ttu-id="728d2-138">VM 포함 될 수 있습니다에서 디스크를 혼합 하 여 다른 저장소 계정 및 저장소 계정 형식 tooachieve에서 최적의 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-138">Your VM can contain a mix of disks from across different storage accounts and storage account types tooachieve your optimal configuration.</span></span>
 

## <a name="your-vm-temporary-drive"></a><span data-ttu-id="728d2-139">VM 임시 드라이브</span><span class="sxs-lookup"><span data-stu-id="728d2-139">Your VM Temporary drive</span></span>
<span data-ttu-id="728d2-140">기본적으로 VM을 만들 때 Azure는 OS 디스크(**/dev/sda**)와 임시 디스크(**/dev/sdb**)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-140">By default when you create a VM, Azure provides you with an OS disk (**/dev/sda**) and a temporary disk (**/dev/sdb**).</span></span>  <span data-ttu-id="728d2-141">추가한 모든 추가 디스크는 **/dev/sdc**, **/dev/sdd**, **/dev/sde** 등으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-141">All additional disks you add show up as **/dev/sdc**, **/dev/sdd**, **/dev/sde** and so on.</span></span> <span data-ttu-id="728d2-142">임시 디스크(**/dev/sdb**)의 모든 데이터는 영구적이지 않으며 VM 크기 조정, 다시 배포 또는 유지 관리와 같은 특정 이벤트가 강제로 VM을 다시 시작하는 경우 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-142">All data on your temporary disk (**/dev/sdb**) is not durable, and can be lost if specific events like VM Resizing, redeployment, or maintenance forces a restart of your VM.</span></span>  <span data-ttu-id="728d2-143">임시 디스크의 유형과 hello 크기는 배포 시 선택한 관련된 toohello VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-143">hello size and type of your temporary disk is related toohello VM size you chose at deployment time.</span></span> <span data-ttu-id="728d2-144">Hello 프리미엄 크기 (DS, G 및 DS_V2 시리즈) Vm hello 임시 드라이브의 모든 too48k IOps의 추가적인 성능에 대 한 로컬 SSD에 의해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-144">All of hello premium size VMs (DS, G, and DS_V2 series) hello temporary drive are backed by a local SSD for additional performance of up too48k IOps.</span></span> 

## <a name="linux-swap-file"></a><span data-ttu-id="728d2-145">Linux 스왑 파일</span><span class="sxs-lookup"><span data-stu-id="728d2-145">Linux Swap File</span></span>
<span data-ttu-id="728d2-146">Ubuntu 또는 CoreOS 이미지에서 Azure VM이 있는 경우 CustomData toosend 클라우드 구성을 toocloud 초기화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-146">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="728d2-147">cloud-init를 사용하는 [사용자 지정 Linux 이미지를 업로드](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)한 경우에도 cloud-init를 사용하여 스왑 파티션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-147">If you [uploaded a custom Linux image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that uses cloud-init, you also configure swap partitions using cloud-init.</span></span>

<span data-ttu-id="728d2-148">Ubuntu 클라우드 이미지에서 클라우드 init tooconfigure hello 스왑 파티션을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-148">On Ubuntu Cloud Images, you must use cloud-init tooconfigure hello swap partition.</span></span> <span data-ttu-id="728d2-149">자세한 내용은 [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="728d2-149">For more information, see [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<span data-ttu-id="728d2-150">클라우드 init 지원 없이 이미지에 대 한 hello Azure Marketplace에서에서 배포 된 VM 이미지는 OS hello와 통합 하는 VM Linux 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-150">For images without cloud-init support, VM images deployed from hello Azure Marketplace have a VM Linux Agent integrated with hello OS.</span></span> <span data-ttu-id="728d2-151">이 에이전트는 다양 한 Azure 서비스와 VM toointeract hello를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-151">This agent allows hello VM toointeract with various Azure services.</span></span> <span data-ttu-id="728d2-152">Hello Azure Marketplace에서에서 독립 실행형 이미지를 배치한 경우 toodo 해야 toocorrectly 다음 hello는 Linux 스왑 파일 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-152">Assuming you have deployed a standard image from hello Azure Marketplace, you would need toodo hello following toocorrectly configure your Linux swap file settings:</span></span>

<span data-ttu-id="728d2-153">찾아 수정 hello에 두 개의 항목이 **/etc/waagent.conf** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-153">Locate and modify two entries in hello **/etc/waagent.conf** file.</span></span> <span data-ttu-id="728d2-154">되지만 hello 스왑 파일의 크기와 전용된 스왑 파일 hello 있는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-154">They control hello existence of a dedicated swap file and size of hello swap file.</span></span> <span data-ttu-id="728d2-155">toomodify 원하는 hello 매개 변수는 `ResourceDisk.EnableSwap=N` 및`ResourceDisk.SwapSizeMB=0`</span><span class="sxs-lookup"><span data-stu-id="728d2-155">hello parameters you are looking toomodify are `ResourceDisk.EnableSwap=N` and `ResourceDisk.SwapSizeMB=0`</span></span> 

<span data-ttu-id="728d2-156">Hello 매개 변수 toohello 다음 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-156">Change hello parameters toohello following settings:</span></span>

* <span data-ttu-id="728d2-157">ResourceDisk.EnableSwap=Y</span><span class="sxs-lookup"><span data-stu-id="728d2-157">ResourceDisk.EnableSwap=Y</span></span>
* <span data-ttu-id="728d2-158">MB toomeet에 ResourceDisk.SwapSizeMB={size 요구에 맞게}</span><span class="sxs-lookup"><span data-stu-id="728d2-158">ResourceDisk.SwapSizeMB={size in MB toomeet your needs}</span></span> 

<span data-ttu-id="728d2-159">Hello 변경 했으면 toorestart hello waagent 또는 Linux VM tooreflect 해당 변경 내용을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-159">Once you have made hello change, you need toorestart hello waagent or restart your Linux VM tooreflect those changes.</span></span>  <span data-ttu-id="728d2-160">Hello 변경을 구현한 및 hello를 사용 하는 경우 스왑 파일을 만들었다고 알고 `free` tooview 여유 공간이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-160">You know hello changes have been implemented and a swap file has been created when you use hello `free` command tooview free space.</span></span> <span data-ttu-id="728d2-161">hello 다음 예제는 hello 수정 결과로 생성 되는 512MB 스왑 파일 **waagent.conf** 파일:</span><span class="sxs-lookup"><span data-stu-id="728d2-161">hello following example has a 512MB swap file created as a result of modifying hello **waagent.conf** file:</span></span>

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a><span data-ttu-id="728d2-162">프리미엄 저장소에 대한 I/O 일정 알고리즘</span><span class="sxs-lookup"><span data-stu-id="728d2-162">I/O scheduling algorithm for Premium Storage</span></span>
<span data-ttu-id="728d2-163">Hello 2.6.18 Linux 커널을와 hello 기본 I/O 예약 알고리즘은 최종 기한에 도달한 tooCFQ (fair 완전히 큐 알고리즘)에서 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-163">With hello 2.6.18 Linux kernel, hello default I/O scheduling algorithm was changed from Deadline tooCFQ (Completely fair queuing algorithm).</span></span> <span data-ttu-id="728d2-164">임의 액세스 I/O 패턴의 경우 CFQ와 최종 기한 간의 성능 차이의 차이는 무시할 수 있는 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-164">For random access I/O patterns, there is negligible difference in performance differences between CFQ and Deadline.</span></span>  <span data-ttu-id="728d2-165">여기서 hello 디스크 I/O 패턴은 주로 SSD 기반 디스크에 대 한 순차적으로 다시 전환 toohello NOOP 또는 최종 기한에 도달한 알고리즘 성능을 향상 시킬 수 I/O입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-165">For SSD-based disks where hello disk I/O pattern is predominantly sequential, switching back toohello NOOP or Deadline algorithm can achieve better I/O performance.</span></span>

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="728d2-166">보기 hello 현재 I/O 스케줄러</span><span class="sxs-lookup"><span data-stu-id="728d2-166">View hello current I/O scheduler</span></span>
<span data-ttu-id="728d2-167">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="728d2-167">Use hello following command:</span></span>  

```bash
cat /sys/block/sda/queue/scheduler
```

<span data-ttu-id="728d2-168">다음 출력 hello 현재 스케줄러를 나타내는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-168">You see following output, which indicates hello current scheduler.</span></span>  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a><span data-ttu-id="728d2-169">Hello 현재 장치 (/ 개발/sda) 알고리즘을 예약 하는 I/O의 변경</span><span class="sxs-lookup"><span data-stu-id="728d2-169">Change hello current device (/dev/sda) of I/O scheduling algorithm</span></span>
<span data-ttu-id="728d2-170">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="728d2-170">Use hello following commands:</span></span>  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> <span data-ttu-id="728d2-171">**/dev/sda**에 대해서만 이 설정 적용하는 것은 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-171">Applying this setting for **/dev/sda** alone is not useful.</span></span> <span data-ttu-id="728d2-172">모든 데이터 디스크에 있는 순차 I/O 보다 우위를 차지 hello I/O 패턴 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-172">Set on all data disks where sequential I/O dominates hello I/O pattern.</span></span>  

<span data-ttu-id="728d2-173">Hello 출력 수행, 하는지 여부를 나타내는 표시 되어야 **grub.cfg** 성공적으로 다시 작성 된 해당 hello 기본 스케줄러 tooNOOP 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-173">You should see hello following output, indicating that **grub.cfg** has been rebuilt successfully and that hello default scheduler has been updated tooNOOP.</span></span>  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

<span data-ttu-id="728d2-174">Hello Redhat 배포 제품군에 대 한 하기만 하면 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="728d2-174">For hello Redhat distribution family, you only need hello following command:</span></span>   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a><span data-ttu-id="728d2-175">소프트웨어 RAID tooachieve 더 높은 사용 하 여 I / Ops</span><span class="sxs-lookup"><span data-stu-id="728d2-175">Using Software RAID tooachieve higher I/Ops</span></span>
<span data-ttu-id="728d2-176">작업 요구할 경우 하나의 디스크가 제공할 수 있는 것 보다 많은 IOps, toouse 여러 디스크의 소프트웨어 RAID 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-176">If your workloads require more IOps than a single disk can provide, you need toouse a software RAID configuration of multiple disks.</span></span> <span data-ttu-id="728d2-177">이미 Azure hello 로컬 패브릭 계층에서 디스크 복구를 수행 하기 때문에 hello 가장 높은 수준의 RAID 0 스트라이프 구성에서 성능 달성 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-177">Because Azure already performs disk resiliency at hello local fabric layer, you achieve hello highest level of performance from a RAID-0 striping configuration.</span></span>  <span data-ttu-id="728d2-178">프로 비전 하 고 hello Azure 환경에서에서 디스크를 만들어 분할 서식 지정 및 탑재 hello 드라이브 전에 tooyour Linux VM 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-178">Provision and create disks in hello Azure environment and attach them tooyour Linux VM before partitioning, formatting and mounting hello drives.</span></span>  <span data-ttu-id="728d2-179">Azure에서 Linux VM에서 소프트웨어 RAID 설치를 구성 하는 방법에 대 한 자세한 내용은 hello에 있습니다  **[Linux에서 소프트웨어 RAID 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  문서.</span><span class="sxs-lookup"><span data-stu-id="728d2-179">More details on configuring a software RAID setup on your Linux VM in azure can be found in hello **[Configuring Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)** document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="728d2-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="728d2-180">Next Steps</span></span>
<span data-ttu-id="728d2-181">Tooperform 테스트 하기 전에 필요한 모든 최적화 토론 하 고 각 변경 toomeasure hello 영향 후 hello 변경의 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-181">Remember, as with all optimization discussions, you need tooperform tests before and after each change toomeasure hello impact hello change has.</span></span>  <span data-ttu-id="728d2-182">최적화는 환경에서 여러 컴퓨터에 다른 결과를 발생시키는 단계별 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-182">Optimization is a step by step process that has different results across different machines in your environment.</span></span>  <span data-ttu-id="728d2-183">하나의 구성에 작동한 최적화가 다른 사용자에게는 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="728d2-183">What works for one configuration may not work for others.</span></span>

<span data-ttu-id="728d2-184">몇 가지 유용한 링크 tooadditional 리소스:</span><span class="sxs-lookup"><span data-stu-id="728d2-184">Some useful links tooadditional resources:</span></span> 

* [<span data-ttu-id="728d2-185">프리미엄 저장소: Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소</span><span class="sxs-lookup"><span data-stu-id="728d2-185">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="728d2-186">Azure Linux 에이전트 사용자 가이드</span><span class="sxs-lookup"><span data-stu-id="728d2-186">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="728d2-187">Azure Linux VM에서 MySQL 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="728d2-187">Optimizing MySQL Performance on Azure Linux VMs</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="728d2-188">Linux에서 소프트웨어 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="728d2-188">Configure Software RAID on Linux</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

