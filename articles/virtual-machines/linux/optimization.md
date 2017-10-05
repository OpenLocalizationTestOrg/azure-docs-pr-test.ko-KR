---
title: "Azure에서 Linux VM 최적화 | Microsoft Docs"
description: "Azure에서 최적의 성능을 위해 Linux VM을 설정하도록 하는 몇 가지 최적화 팁을 알아봅니다"
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
ms.openlocfilehash: eb79d574fd4dddfb986660cc338bc8748f2082c2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a><span data-ttu-id="6720b-104">Azure에서 Linux VM 최적화</span><span class="sxs-lookup"><span data-stu-id="6720b-104">Optimize your Linux VM on Azure</span></span>
<span data-ttu-id="6720b-105">Linux 가상 컴퓨터(VM) 만들기는 명령줄 또는 포털에서 수행하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-105">Creating a Linux virtual machine (VM) is easy to do from the command line or from the portal.</span></span> <span data-ttu-id="6720b-106">이 자습서에서는 Microsoft Azure Platform에서 해당 성능을 최적화하도록 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-106">This tutorial shows you how to ensure you have set it up to optimize its performance on the Microsoft Azure platform.</span></span> <span data-ttu-id="6720b-107">이 항목에서는 Ubuntu Server VM을 사용 하지만 [템플릿으로 사용자 고유의 이미지](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용하여 Linux 가상 컴퓨터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-107">This topic uses an Ubuntu Server VM, but you can also create Linux virtual machine using [your own images as templates](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6720b-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6720b-108">Prerequisites</span></span>
<span data-ttu-id="6720b-109">이 항목에서는 사용하는 Azure 구독([무료 평가판 등록](https://azure.microsoft.com/pricing/free-trial/))이 이미 있으며 Azure 구독에 VM을 이미 프로비전했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-109">This topic assumes you already have a working Azure subscription ([free trial signup](https://azure.microsoft.com/pricing/free-trial/)) and have already provisioned a VM into your Azure subscription.</span></span> <span data-ttu-id="6720b-110">[VM을 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 전에 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 구독에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-110">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to your Azure subscription with [az login](/cli/azure/#login) before you [create a VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="azure-os-disk"></a><span data-ttu-id="6720b-111">Azure OS 디스크</span><span class="sxs-lookup"><span data-stu-id="6720b-111">Azure OS Disk</span></span>
<span data-ttu-id="6720b-112">Azure에서 Linux VM을 만들면 이에 연결된 두 개의 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-112">Once you create a Linux VM in Azure, it has two disks associated with it.</span></span> <span data-ttu-id="6720b-113">**/dev/sda**는 OS 디스크이며 **/dev/sdb**는 임시 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-113">**/dev/sda** is your OS disk, **/dev/sdb** is your temporary disk.</span></span>  <span data-ttu-id="6720b-114">OS 디스크(**/dev/sda**)는 신속한 VM 부팅 시간에 최적화되고 워크로드에 좋은 성능을 제공하지 않으므로 운영 체제 이외에 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-114">Do not use the main OS disk (**/dev/sda**) for anything except the operating system as it is optimized for fast VM boot time and does not provide good performance for your workloads.</span></span> <span data-ttu-id="6720b-115">데이터에 대한 영구적이고 최적화된 저장소를 얻기 위해 VM에 하나 이상의 디스크를 연결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-115">You want to attach one or more disks to your VM to get persistent and optimized storage for your data.</span></span> 

## <a name="adding-disks-for-size-and-performance-targets"></a><span data-ttu-id="6720b-116">크기 및 성능 대상에 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="6720b-116">Adding Disks for Size and Performance targets</span></span>
<span data-ttu-id="6720b-117">VM 크기에 따라 A 시리즈에 16개, D 시리즈에 32개 및 G 시리즈에 64개의 디스크를 최대로 연결할 수 있고 각각 최대 크기는 1TB입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-117">Based on the VM size, you can attach up to 16 additional disks on an A-Series, 32 disks on a D-Series and 64 disks on a G-Series machine - each up to 1 TB in size.</span></span> <span data-ttu-id="6720b-118">공간 및 IOps 요구 사항에 따라 필요한 만큼 디스크를 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-118">You add extra disks as needed per your space and IOps requirements.</span></span> <span data-ttu-id="6720b-119">각 디스크의 성능 목표는 표준 저장소의 경우 최대 500IOps이며 프리미엄 저장소의 경우 디스크당 최대 5000IOps입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-119">Each disk has a performance target of 500 IOps for Standard Storage and up to 5000 IOps per disk for Premium Storage.</span></span>  <span data-ttu-id="6720b-120">Premium Storage에 대한 자세한 내용은 [Premium Storage: Azure VM용 고성능 저장소](../../storage/common/storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6720b-120">For more information about Premium Storage disks, see [Premium Storage: High-Performance Storage for Azure VMs](../../storage/common/storage-premium-storage.md)</span></span>

<span data-ttu-id="6720b-121">**읽기 전용** 또는 **해당 없음**으로 캐시를 설정한 Premium Storage 디스크에서 가장 높은 IOps를 수행하기 위해 Linux에서 파일 시스템을 탑재하는 동안 **장벽**을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-121">To achieve the highest IOps on Premium Storage disks where their cache settings have been set to either **ReadOnly** or **None**, you must disable **barriers** while mounting the file system in Linux.</span></span> <span data-ttu-id="6720b-122">프리미엄 저장소 백업 디스크에 쓰기는 이러한 캐시 설정에 대해 내구성이 있기 때문에 장벽이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-122">You do not need barriers because the writes to Premium Storage backed disks are durable for these cache settings.</span></span>

* <span data-ttu-id="6720b-123">**reiserFS**를 사용하는 경우 탑재 옵션 `barrier=none`을 사용하여 장벽을 사용하지 않도록 설정합니다(장벽 사용의 경우 `barrier=flush` 사용).</span><span class="sxs-lookup"><span data-stu-id="6720b-123">If you use **reiserFS**, disable barriers using the mount option `barrier=none` (For enabling barriers, use `barrier=flush`)</span></span>
* <span data-ttu-id="6720b-124">**ext3/ext4**를 사용하는 경우 탑재 옵션 `barrier=0`을 사용하여 장벽을 사용하지 않도록 설정합니다(장벽 사용의 경우 `barrier=1` 사용).</span><span class="sxs-lookup"><span data-stu-id="6720b-124">If you use **ext3/ext4**, disable barriers using the mount option `barrier=0` (For enabling barriers, use `barrier=1`)</span></span>
* <span data-ttu-id="6720b-125">**XFS**를 사용하는 경우 탑재 옵션 `nobarrier`을 사용하여 장벽을 사용하지 않도록 설정합니다(장벽 사용의 경우 `barrier` 옵션 사용).</span><span class="sxs-lookup"><span data-stu-id="6720b-125">If you use **XFS**, disable barriers using the mount option `nobarrier` (For enabling barriers, use the option `barrier`)</span></span>

## <a name="unmanaged-storage-account-considerations"></a><span data-ttu-id="6720b-126">관리되지 않는 저장소 계정 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6720b-126">Unmanaged storage account considerations</span></span>
<span data-ttu-id="6720b-127">Azure CLI 2.0을 사용하여 VM을 만들 때 기본 작업은 Azure Managed Disks를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-127">The default action when you create a VM with the Azure CLI 2.0 is to use Azure Managed Disks.</span></span>  <span data-ttu-id="6720b-128">이들 디스크는 Azure 플랫폼을 통해 처리되며 디스크를 저장할 위치나 준비가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-128">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span>  <span data-ttu-id="6720b-129">관리되지 않는 디스크는 저장소 계정이 필요하며 추가 성능 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-129">Unmanaged disks require a storage account and have some additional performance considerations.</span></span>  <span data-ttu-id="6720b-130">관리 디스크에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6720b-130">For more information about managed disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>  <span data-ttu-id="6720b-131">다음 섹션에서는 관리되지 않는 디스크를 사용하는 경우에만 성능 고려 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-131">The following section outlines performance considerations only when you use unmanaged disks.</span></span>  <span data-ttu-id="6720b-132">권장되는 기본 저장소 솔루션은 Managed Disks를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-132">Again, the default and recommended storage solution is to use managed disks.</span></span>

<span data-ttu-id="6720b-133">관리되지 않는 디스크를 사용하여 VM을 만들 경우 가까운 근접성을 제공하고 네트워크 대기 시간을 최소화하기 위해 VM과 동일한 지역에 위치한 저장소 계정에서 디스크를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-133">If you create a VM with unmanaged disks, make sure that you attach disks from storage accounts residing in the same region as your VM to ensure close proximity and minimize network latency.</span></span>  <span data-ttu-id="6720b-134">각 표준 저장소 계정에는 최대 20,000IOps 및 500TB 크기의 용량이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-134">Each Standard storage account has a maximum of 20k IOps and a 500 TB size capacity.</span></span>  <span data-ttu-id="6720b-135">이러한 제한은 만든 OS 디스크 및 데이터 디스크를 비롯한 약 40개의 많이 사용되는 디스크에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-135">This  limit works out to approximately 40 heavily used disks including both the OS disk and any data disks you create.</span></span> <span data-ttu-id="6720b-136">프리미엄 저장소 계정의 경우 최대 IOps 제한이 없지만 크기는 32TB로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-136">For Premium Storage accounts, there is no Maximum IOps limit but there is a 32 TB size limit.</span></span> 

<span data-ttu-id="6720b-137">높은 IOps 워크로드를 다루고 디스크에 Standard Storage를 선택한 경우 여러 저장소 계정에 디스크를 분할하여 Standard Storage 계정에 대한 20,000IOps 제한을 넘지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-137">When dealing with high IOps workloads and you have chosen Standard Storage for your disks, you might need to split the disks across multiple storage accounts to make sure you have not hit the 20,000 IOps limit for Standard Storage accounts.</span></span> <span data-ttu-id="6720b-138">VM은 다른 저장소 계정 및 저장소 계정 유형에서 혼합된 디스크를 포함하여 최적의 구성을 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-138">Your VM can contain a mix of disks from across different storage accounts and storage account types to achieve your optimal configuration.</span></span>
 

## <a name="your-vm-temporary-drive"></a><span data-ttu-id="6720b-139">VM 임시 드라이브</span><span class="sxs-lookup"><span data-stu-id="6720b-139">Your VM Temporary drive</span></span>
<span data-ttu-id="6720b-140">기본적으로 VM을 만들 때 Azure는 OS 디스크(**/dev/sda**)와 임시 디스크(**/dev/sdb**)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-140">By default when you create a VM, Azure provides you with an OS disk (**/dev/sda**) and a temporary disk (**/dev/sdb**).</span></span>  <span data-ttu-id="6720b-141">추가한 모든 추가 디스크는 **/dev/sdc**, **/dev/sdd**, **/dev/sde** 등으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-141">All additional disks you add show up as **/dev/sdc**, **/dev/sdd**, **/dev/sde** and so on.</span></span> <span data-ttu-id="6720b-142">임시 디스크(**/dev/sdb**)의 모든 데이터는 영구적이지 않으며 VM 크기 조정, 다시 배포 또는 유지 관리와 같은 특정 이벤트가 강제로 VM을 다시 시작하는 경우 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-142">All data on your temporary disk (**/dev/sdb**) is not durable, and can be lost if specific events like VM Resizing, redeployment, or maintenance forces a restart of your VM.</span></span>  <span data-ttu-id="6720b-143">임시 디스크의 크기 및 유형은 배포 시에 선택한 VM 크기와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-143">The size and type of your temporary disk is related to the VM size you chose at deployment time.</span></span> <span data-ttu-id="6720b-144">모든 프리미엄 크기 VM(DS, G 및 DS_V2 시리즈)의 경우 임시 드라이브는 최대 48,000IOps의 추가 성능을 가진 로컬 SSD에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-144">All of the premium size VMs (DS, G, and DS_V2 series) the temporary drive are backed by a local SSD for additional performance of up to 48k IOps.</span></span> 

## <a name="linux-swap-file"></a><span data-ttu-id="6720b-145">Linux 스왑 파일</span><span class="sxs-lookup"><span data-stu-id="6720b-145">Linux Swap File</span></span>
<span data-ttu-id="6720b-146">Azure VM을 Ubuntu 또는 CoreOS 이미지에서 가져온 경우 CustomData를 사용하여 cloud-config를 cloud-init으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-146">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="6720b-147">cloud-init를 사용하는 [사용자 지정 Linux 이미지를 업로드](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)한 경우에도 cloud-init를 사용하여 스왑 파티션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-147">If you [uploaded a custom Linux image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that uses cloud-init, you also configure swap partitions using cloud-init.</span></span>

<span data-ttu-id="6720b-148">Ubuntu Cloud Images에서는 cloud-init를 사용하여 스왑 파티션을 구성하해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-148">On Ubuntu Cloud Images, you must use cloud-init to configure the swap partition.</span></span> <span data-ttu-id="6720b-149">자세한 내용은 [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6720b-149">For more information, see [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<span data-ttu-id="6720b-150">cloud-init를 지원하지 않는 이미지의 경우 Azure Marketplace에서 배포된 VM 이미지에는 OS와 통합된 VM Linux 에이전트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-150">For images without cloud-init support, VM images deployed from the Azure Marketplace have a VM Linux Agent integrated with the OS.</span></span> <span data-ttu-id="6720b-151">이 에이전트를 사용하면 VM에서 다양한 Azure 서비스와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-151">This agent allows the VM to interact with various Azure services.</span></span> <span data-ttu-id="6720b-152">Azure 마켓플레이스에서 표준 이미지를 배포한 경우 다음을 수행하여 Linux 스왑 파일 설정을 올바르게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-152">Assuming you have deployed a standard image from the Azure Marketplace, you would need to do the following to correctly configure your Linux swap file settings:</span></span>

<span data-ttu-id="6720b-153">**/etc/waagent.conf** 파일에서 두 개의 항목을 찾아 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-153">Locate and modify two entries in the **/etc/waagent.conf** file.</span></span> <span data-ttu-id="6720b-154">전용 스왑 파일의 존재 여부 및 스왑 파일의 크기를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-154">They control the existence of a dedicated swap file and size of the swap file.</span></span> <span data-ttu-id="6720b-155">수정하려는 매개 변수는 `ResourceDisk.EnableSwap=N` 및 `ResourceDisk.SwapSizeMB=0`입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-155">The parameters you are looking to modify are `ResourceDisk.EnableSwap=N` and `ResourceDisk.SwapSizeMB=0`</span></span> 

<span data-ttu-id="6720b-156">매개 변수를 다음 설정으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-156">Change the parameters to the following settings:</span></span>

* <span data-ttu-id="6720b-157">ResourceDisk.EnableSwap=Y</span><span class="sxs-lookup"><span data-stu-id="6720b-157">ResourceDisk.EnableSwap=Y</span></span>
* <span data-ttu-id="6720b-158">ResourceDisk.SwapSizeMB={필요에 맞는 크기(MB)}</span><span class="sxs-lookup"><span data-stu-id="6720b-158">ResourceDisk.SwapSizeMB={size in MB to meet your needs}</span></span> 

<span data-ttu-id="6720b-159">변경한 후에는 변경 내용을 반영하기 위해 waagent를 다시 시작하거나 Linux VM을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-159">Once you have made the change, you need to restart the waagent or restart your Linux VM to reflect those changes.</span></span>  <span data-ttu-id="6720b-160">변경 내용을 구현했다면 `free` 명령을 사용하여 여유 공간을 볼 때 스왑 파일이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-160">You know the changes have been implemented and a swap file has been created when you use the `free` command to view free space.</span></span> <span data-ttu-id="6720b-161">다음 예제에서는 **waagent.conf** 파일을 수정한 결과로 생성된 512MB 스왑 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-161">The following example has a 512MB swap file created as a result of modifying the **waagent.conf** file:</span></span>

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a><span data-ttu-id="6720b-162">프리미엄 저장소에 대한 I/O 일정 알고리즘</span><span class="sxs-lookup"><span data-stu-id="6720b-162">I/O scheduling algorithm for Premium Storage</span></span>
<span data-ttu-id="6720b-163">2.6.18 Linux 커널로 기본 I/O 일정 알고리즘은 최종 기한에서 CFQ로 변경되었습니다(완전히 공정한 큐 대기 알고리즘).</span><span class="sxs-lookup"><span data-stu-id="6720b-163">With the 2.6.18 Linux kernel, the default I/O scheduling algorithm was changed from Deadline to CFQ (Completely fair queuing algorithm).</span></span> <span data-ttu-id="6720b-164">임의 액세스 I/O 패턴의 경우 CFQ와 최종 기한 간의 성능 차이의 차이는 무시할 수 있는 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-164">For random access I/O patterns, there is negligible difference in performance differences between CFQ and Deadline.</span></span>  <span data-ttu-id="6720b-165">디스크 I/O 패턴이 대부분 순차적인 SSD 기반 디스크의 경우 NOOP 또는 최종 기한 알고리즘으로 다시 전환하면 I/O 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-165">For SSD-based disks where the disk I/O pattern is predominantly sequential, switching back to the NOOP or Deadline algorithm can achieve better I/O performance.</span></span>

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="6720b-166">현재 I/O 스케줄러 보기</span><span class="sxs-lookup"><span data-stu-id="6720b-166">View the current I/O scheduler</span></span>
<span data-ttu-id="6720b-167">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-167">Use the following command:</span></span>  

```bash
cat /sys/block/sda/queue/scheduler
```

<span data-ttu-id="6720b-168">현재 스케줄러를 나타내는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-168">You see following output, which indicates the current scheduler.</span></span>  

```bash
noop [deadline] cfq
```

### <a name="change-the-current-device-devsda-of-io-scheduling-algorithm"></a><span data-ttu-id="6720b-169">I/O 일정 알고리즘의 현재 장치(/dev/sda) 변경</span><span class="sxs-lookup"><span data-stu-id="6720b-169">Change the current device (/dev/sda) of I/O scheduling algorithm</span></span>
<span data-ttu-id="6720b-170">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-170">Use the following commands:</span></span>  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> <span data-ttu-id="6720b-171">**/dev/sda**에 대해서만 이 설정 적용하는 것은 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-171">Applying this setting for **/dev/sda** alone is not useful.</span></span> <span data-ttu-id="6720b-172">순차 I/O가 I/O 패턴의 우위를 차지한 모든 데이터 디스크에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-172">Set on all data disks where sequential I/O dominates the I/O pattern.</span></span>  

<span data-ttu-id="6720b-173">**grub.cfg**가 성공적으로 다시 빌드되었으며 기본 스케줄러가 NOOP로 업데이트되었음을 나타내는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-173">You should see the following output, indicating that **grub.cfg** has been rebuilt successfully and that the default scheduler has been updated to NOOP.</span></span>  

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

<span data-ttu-id="6720b-174">Redhat 배포 패밀리의 경우 다음 명령만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-174">For the Redhat distribution family, you only need the following command:</span></span>   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-to-achieve-higher-iops"></a><span data-ttu-id="6720b-175">소프트웨어 RAID를 사용하여 높은 I/Ops 달성</span><span class="sxs-lookup"><span data-stu-id="6720b-175">Using Software RAID to achieve higher I/Ops</span></span>
<span data-ttu-id="6720b-176">워크로드가 단일 디스크에서 제공하는 것보다 많은 IOps를 필요로 하는 경우 여러 디스크의 소프트웨어 RAID 구성을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-176">If your workloads require more IOps than a single disk can provide, you need to use a software RAID configuration of multiple disks.</span></span> <span data-ttu-id="6720b-177">Azure는 이미 로컬 패브릭 계층에서 디스크 복구를 수행하기 때문에 가장 높은 수준의 성능 RAID-0 스트라이프 구성을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-177">Because Azure already performs disk resiliency at the local fabric layer, you achieve the highest level of performance from a RAID-0 striping configuration.</span></span>  <span data-ttu-id="6720b-178">Azure 환경에서 디스크를 프로비전하고 만들며 드라이브를 분할하고 서식을 지정하며 탑재하기 전에 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-178">Provision and create disks in the Azure environment and attach them to your Linux VM before partitioning, formatting and mounting the drives.</span></span>  <span data-ttu-id="6720b-179">Azure에서 Linux VM의 소프트웨어 RAID 설정을 구성하는 방법에 대한 자세한 내용은 **[Linux에서 소프트웨어 RAID 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)** 문서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-179">More details on configuring a software RAID setup on your Linux VM in azure can be found in the **[Configuring Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)** document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6720b-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6720b-180">Next Steps</span></span>
<span data-ttu-id="6720b-181">모든 최적화에 관련된 토론 대로 변경 사항이 가져올 영향을 측정하기 위해 각 변경 사항의 전후에 테스트를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-181">Remember, as with all optimization discussions, you need to perform tests before and after each change to measure the impact the change has.</span></span>  <span data-ttu-id="6720b-182">최적화는 환경에서 여러 컴퓨터에 다른 결과를 발생시키는 단계별 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-182">Optimization is a step by step process that has different results across different machines in your environment.</span></span>  <span data-ttu-id="6720b-183">하나의 구성에 작동한 최적화가 다른 사용자에게는 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6720b-183">What works for one configuration may not work for others.</span></span>

<span data-ttu-id="6720b-184">추가 리소스에 대한 몇 가지 유용한 링크:</span><span class="sxs-lookup"><span data-stu-id="6720b-184">Some useful links to additional resources:</span></span> 

* [<span data-ttu-id="6720b-185">프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소</span><span class="sxs-lookup"><span data-stu-id="6720b-185">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="6720b-186">Azure Linux 에이전트 사용자 가이드</span><span class="sxs-lookup"><span data-stu-id="6720b-186">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6720b-187">Azure Linux VM에서 MySQL 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="6720b-187">Optimizing MySQL Performance on Azure Linux VMs</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="6720b-188">Linux에서 소프트웨어 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="6720b-188">Configure Software RAID on Linux</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

