---
title: "Azure에서 Linux VM의 가상 하드 디스크 aaaExpand | Microsoft Docs"
description: "Tooexpand 가상 하드 디스크 사용 하 여 Linux VM에 Azure CLI 2.0 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="63a09-103">Tooexpand 가상 하드 디스크 사용 하 여 Linux VM에 Azure CLI hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="63a09-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="63a09-104">hello 운영 체제 (OS) hello 기본 가상 하드 디스크 크기는 Azure에서 Linux 가상 컴퓨터 (VM)에서 일반적으로 30GB입니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="63a09-105">있습니다 수 [데이터 디스크를 추가](add-disk.md) 추가 저장소 공간을 위한 tooprovide 라면 tooexpand 기존 데이터 디스크.</span><span class="sxs-lookup"><span data-stu-id="63a09-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="63a09-106">이 문서 tooexpand hello Azure CLI 2.0을 사용 하 여 Linux VM에 대 한 디스크를 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="63a09-107">Hello로 관리 되지 않는 hello OS 디스크를 확장할 수도 있습니다 [Azure CLI 1.0](expand-disks-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="63a09-108">항상 디스크 크기 조정 작업을 수행하기 전에 데이터를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="63a09-109">자세한 내용은 [Azure에서 Linux VM 백업](tutorial-backup-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63a09-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="63a09-110">디스크 확장</span><span class="sxs-lookup"><span data-stu-id="63a09-110">Expand disk</span></span>
<span data-ttu-id="63a09-111">Hello 최신 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="63a09-112">이 문서는 Azure에 데이터 디스크가 하나 이상 연결되고 준비된 기존 VM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="63a09-113">사용할 수 있는 VM이 아직 없는 경우 [데이터 디스크가 있는 VM 만들기 및 준비](tutorial-manage-disks.md#create-and-attach-disks)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63a09-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="63a09-114">Hello 다음 예제를 원하는 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="63a09-115">예제 매개 변수 이름에는 *myResourceGroup* 및 *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="63a09-116">VM hello로 가상 하드 디스크에 대 한 작업을 수행할 수 없습니다 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="63a09-117">[az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="63a09-118">hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="63a09-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="63a09-119">`az vm stop`hello 계산 리소스를 해제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="63a09-120">toorelease 계산 리소스를 사용 하 여 `az vm deallocate`합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="63a09-121">hello VM tooexpand hello 가상 하드 디스크를 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="63a09-122">이제 [az disk list](/cli/azure/disk#list)를 사용하여 리소스 그룹에서 Managed Disks 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="63a09-123">hello 다음 예제에서는 표시는 관리 되는 디스크의 목록을 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="63a09-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="63a09-124">Hello 필요한 디스크와 확장 [az 디스크 업데이트](/cli/azure/disk#update)합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="63a09-125">hello 다음 예제에서는 확장 이름이 관리 되는 디스크 hello *myDataDisk* toobe *200*4gb:</span><span class="sxs-lookup"><span data-stu-id="63a09-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="63a09-126">관리 되는 디스크를 확장 하면 hello 업데이트 크기는 관리 되는 디스크 크기에 가장 가까운 매핑된 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="63a09-127">Hello 사용 가능한 관리 되는 디스크 크기와 계층의 테이블을 참조 하십시오. [Azure 관리 되는 디스크 개요-가격 및 요금 청구](../windows/managed-disks-overview.md#pricing-and-billing)합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="63a09-128">[az vm start](/cli/azure/vm#start)를 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="63a09-129">다음 예에서는 시작 하는 hello hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="63a09-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="63a09-130">SSH tooyour VM hello 적절 한 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="63a09-131">Hello를 사용 하 여 VM의 공용 IP 주소를 가져올 수 있습니다 [az vm 표시](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="63a09-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="63a09-132">toouse hello 디스크를 확장 하 고 tooexpand hello 기본 파티션 및 파일 시스템 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="63a09-133">a.</span><span class="sxs-lookup"><span data-stu-id="63a09-133">a.</span></span> <span data-ttu-id="63a09-134">이미 탑재 hello 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="63a09-135">b.</span><span class="sxs-lookup"><span data-stu-id="63a09-135">b.</span></span> <span data-ttu-id="63a09-136">사용 하 여 `parted` tooview 디스크 정보 및 hello 파티션 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="63a09-137">Hello와 기존 파티션 레이아웃에 대 한 정보를 볼 `print`합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="63a09-138">hello는 비슷한 toohello 다음 hello 기본 디스크의 크기 215 Gb는 보여 주는 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="63a09-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="63a09-139">c.</span><span class="sxs-lookup"><span data-stu-id="63a09-139">c.</span></span> <span data-ttu-id="63a09-140">Hello 파티션에 확장 `resizepart`합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="63a09-141">Hello 파티션 번호를 입력 *1*, 새 파티션 hello에 대 한 크기 및:</span><span class="sxs-lookup"><span data-stu-id="63a09-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="63a09-142">d.</span><span class="sxs-lookup"><span data-stu-id="63a09-142">d.</span></span> <span data-ttu-id="63a09-143">tooexit, 입력`quit`</span><span class="sxs-lookup"><span data-stu-id="63a09-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="63a09-144">크기를 조정 하는 hello 파티션과 hello 파티션 일관성을 확인 `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="63a09-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="63a09-145">Hello 파일 시스템으로 크기를 조정할 `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="63a09-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="63a09-146">탑재 hello 파티션 toohello 원하는 위치와 같은 `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="63a09-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="63a09-147">tooverify hello 운영 체제 디스크 크기가 조정 되었으므로, 사용 하 여 `df -h`합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="63a09-148">다음 예제 출력 hello hello 데이터 드라이브를 보여 줍니다. */개발/sdc1*, 200GB 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="63a09-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63a09-149">Next steps</span></span>
<span data-ttu-id="63a09-150">추가 저장소가 필요 하면도 [추가 데이터 디스크 tooa Linux VM](add-disk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="63a09-151">디스크 암호화에 대 한 자세한 내용은 참조 [Encrypt 디스크를 사용 하 여 Linux VM에 Azure CLI hello](encrypt-disks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63a09-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
