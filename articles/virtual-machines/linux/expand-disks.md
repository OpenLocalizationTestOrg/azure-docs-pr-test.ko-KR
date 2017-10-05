---
title: "Azure의 Linux VM에서 가상 하드 디스크 확장 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 Linux VM에서 가상 하드 디스크를 확장하는 방법 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: b82cc0473c003da767ee230ab485c69b233977d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="1ed62-103">Azure CLI를 사용하여 Linux VM에서 가상 하드 디스크를 확장하는 방법</span><span class="sxs-lookup"><span data-stu-id="1ed62-103">How to expand virtual hard disks on a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="1ed62-104">Azure에서 Linux VM(가상 컴퓨터)에서 OS(운영 체제)에 대한 기본 가상 하드 디스크 크기는 일반적으로 30GB입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="1ed62-105">[데이터 디스크를 추가](add-disk.md)하여 추가 저장소 공간을 제공할 수 있으나, 기존 데이터 디스크를 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand an existing data disk.</span></span> <span data-ttu-id="1ed62-106">이 문서에서는 Azure CLI 2.0을 사용하여 Linux VM에서 Managed Disks를 확장하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="1ed62-107">[Azure CLI 1.0](expand-disks-nodejs.md)을 사용하여 관리되지 않는 OS 디스크를 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="1ed62-108">항상 디스크 크기 조정 작업을 수행하기 전에 데이터를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="1ed62-109">자세한 내용은 [Azure에서 Linux VM 백업](tutorial-backup-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed62-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="1ed62-110">디스크 확장</span><span class="sxs-lookup"><span data-stu-id="1ed62-110">Expand disk</span></span>
<span data-ttu-id="1ed62-111">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1ed62-112">이 문서는 Azure에 데이터 디스크가 하나 이상 연결되고 준비된 기존 VM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="1ed62-113">사용할 수 있는 VM이 아직 없는 경우 [데이터 디스크가 있는 VM 만들기 및 준비](tutorial-manage-disks.md#create-and-attach-disks)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed62-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="1ed62-114">다음 샘플에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-114">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1ed62-115">예제 매개 변수 이름에는 *myResourceGroup* 및 *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="1ed62-116">VM 실행 중에 가상 하드 디스크에 대한 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="1ed62-117">[az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="1ed62-118">다음 예제에서는 리소스 그룹 *myResourceGroup*에서 *myVM*이라는 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-118">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="1ed62-119">`az vm stop`은 계산 리소스를 릴리스하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-119">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="1ed62-120">계산 리소스를 릴리스하려면 `az vm deallocate`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-120">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="1ed62-121">VM 할당을 취소하여 가상 하드 디스크를 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-121">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="1ed62-122">이제 [az disk list](/cli/azure/disk#list)를 사용하여 리소스 그룹에서 Managed Disks 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="1ed62-123">다음 예제에서는 리소스 그룹 *myResourceGroup*의 Managed Disks 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-123">The following example displays a list of managed disks in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="1ed62-124">[az disk update](/cli/azure/disk#update)를 사용하여 필요한 디스크를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-124">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="1ed62-125">다음 예제에서는 *myDataDisk*이라는 Managed Disk를 *200*GB 크기로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-125">The following example expands the managed disk named *myDataDisk* to be *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="1ed62-126">Managed Disk를 확장하면 업데이트된 크기는 가장 가까운 Managed Disk 크기에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-126">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="1ed62-127">사용 가능한 Managed Disk 크기 및 계층의 테이블은 [Azure Managed Disks 개요 - 가격 책정 및 청구](../windows/managed-disks-overview.md#pricing-and-billing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed62-127">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="1ed62-128">[az vm start](/cli/azure/vm#start)를 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="1ed62-129">다음 예제에서는 리소스 그룹 *myResourceGroup*에서 *myVM*이라는 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-129">The following example starts the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="1ed62-130">적절한 자격 증명을 사용하여 VM에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-130">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="1ed62-131">[az vm show](/cli/azure/vm#show)를 사용하여 VM의 공용 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-131">You can obtain the public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="1ed62-132">확장된 디스크를 사용하려면 기본 파티션 및 파일 시스템을 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-132">To use the expanded disk, you need to expand the underlying partition and filesystem.</span></span>

    <span data-ttu-id="1ed62-133">a.</span><span class="sxs-lookup"><span data-stu-id="1ed62-133">a.</span></span> <span data-ttu-id="1ed62-134">이미 탑재되어 있는 경우 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-134">If already mounted, unmount the disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="1ed62-135">b.</span><span class="sxs-lookup"><span data-stu-id="1ed62-135">b.</span></span> <span data-ttu-id="1ed62-136">`parted`를 사용하여 디스크 정보를 보고 파티션 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-136">Use `parted` to view disk information and resize the partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="1ed62-137">`print`를 사용하여 기존 파티션 레이아웃에 대한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-137">View information about the existing partition layout with `print`.</span></span> <span data-ttu-id="1ed62-138">출력은 기본 디스크 크기가 215Gb임을 보여 주는 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-138">The output is similar to the following example, which shows the underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="1ed62-139">c.</span><span class="sxs-lookup"><span data-stu-id="1ed62-139">c.</span></span> <span data-ttu-id="1ed62-140">`resizepart`를 사용하여 파티션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-140">Expand the partition with `resizepart`.</span></span> <span data-ttu-id="1ed62-141">파티션 수 *1*과 새 파티션에 대한 크기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-141">Enter the partition number, *1*, and a size for the new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="1ed62-142">d.</span><span class="sxs-lookup"><span data-stu-id="1ed62-142">d.</span></span> <span data-ttu-id="1ed62-143">끝내려면 `quit`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-143">To exit, enter `quit`</span></span>

5. <span data-ttu-id="1ed62-144">파티션 크기를 조정했으면 `e2fsck`를 사용하여 파티션 일관성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-144">With the partition resized, verify the partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="1ed62-145">이제 파일 시스템 크기를 `resize2fs`로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-145">Now resize the filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="1ed62-146">`/datadrive`와 같이 파티션을 원하는 위치로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-146">Mount the partition to the desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="1ed62-147">OS 디스크 크기를 조정했는지 확인하려면 `df -h`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-147">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="1ed62-148">다음 예제 출력에서는 데이터 드라이브(*/dev/sdc1*)가 200GB임을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-148">The following example output shows the data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="1ed62-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ed62-149">Next steps</span></span>
<span data-ttu-id="1ed62-150">또한 추가 저장소가 필요한 경우 [Linux VM에 데이터 디스크를 추가](add-disk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed62-150">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="1ed62-151">디스크 암호화에 대한 자세한 내용은 [Azure CLI를 사용하여 Linux VM에서 디스크 암호화](encrypt-disks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed62-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
