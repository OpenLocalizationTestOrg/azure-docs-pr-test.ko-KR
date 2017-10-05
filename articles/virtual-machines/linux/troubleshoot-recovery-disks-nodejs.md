---
title: "Azure CLI 1.0을 사용하여 Linux 문제 해결 VM 사용 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 OS 디스크를 복구 VM에 연결함으로써 Linux VM 문제를 해결하는 방법 알아보기"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: d817358211f123c96d899c5cff88cc47aeb5c9c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="8a236-103">Azure CLI 1.0을 사용하여 OS 디스크를 복구 VM에 연결함으로써 Linux VM 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8a236-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="8a236-104">Linux 가상 컴퓨터(VM)에 부팅 또는 디스크 오류가 발생하는 경우 가상 하드 디스크에서 바로 문제 해결 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="8a236-105">일반적인 예로는 `/etc/fstab`의 잘못된 항목으로 인해 VM이 성공적으로 부팅되지 않는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="8a236-106">이 문서에는 가상 하드 디스크를 다른 Linux VM에 연결하여 모든 오류를 수정한 후 원래 VM을 다시 만들기 위해 Azure CLI 1.0을 사용하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8a236-107">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="8a236-107">CLI versions to complete the task</span></span>
<span data-ttu-id="8a236-108">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="8a236-109">[Azure CLI 1.0](#recovery-process-overview) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="8a236-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8a236-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="8a236-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="8a236-111">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="8a236-111">Recovery process overview</span></span>
<span data-ttu-id="8a236-112">문제 해결 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="8a236-113">문제가 발생하는 VM을 삭제하여, 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="8a236-114">문제 해결을 위해 가상 하드 디스크를 다른 Linux VM에 연결하고 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="8a236-115">문제 해결 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="8a236-116">파일을 편집하거나 도구를 실행하여 원래의 가상 하드 디스크에서 문제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="8a236-117">문제 해결 VM에서 가상 하드 디스크를 탑재 해제하고 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="8a236-118">원래 가상 하드 디스크를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="8a236-119">[최신 Azure CLI 1.0](../../cli-install-nodejs.md)이 설치되어 있고 Resource Manager 모드를 사용하여 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8a236-120">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="8a236-121">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="8a236-122">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="8a236-122">Determine boot issues</span></span>
<span data-ttu-id="8a236-123">VM이 올바르게 부팅할 수 없는 원인을 확인하려면 직렬 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="8a236-124">일반적인 예로는 `/etc/fstab`의 잘못된 항목 또는 삭제하거나 이동 중인 기본 가상 하드 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="8a236-125">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`에서 직렬 출력을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8a236-126">직렬 출력을 검토하여 VM가 부팅되지 않는 원인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="8a236-127">직렬 출력에 아무런 표시가 없는 경우, 가상 하드 디스크가 문제 해결 VM에 연결하고 `/var/log`에 로그 파일을 검토해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="8a236-128">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="8a236-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="8a236-129">가상 하드 디스크를 다른 VM에 연결하기 전에 가상 하드 디스크(VHD)의 이름을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="8a236-130">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`에 대한 정보를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8a236-131">이전 명령의 출력에서 `Vhd URI`를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="8a236-132">다음의 잘린 예제 출력은 마지막 줄에 `Vhd URI`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="8a236-133">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="8a236-133">Delete existing VM</span></span>
<span data-ttu-id="8a236-134">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="8a236-135">가상 하드 디스크에는 운영 체제 자체, 응용 프로그램 및 구성이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="8a236-136">VM 자체는 크기 또는 위치를 정의하고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드(NIC)와 같은 리소스를 참조하는 메타데이터일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="8a236-137">각 가상 하드 디스크에는 VM에 연결할 때 할당된 임대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="8a236-138">VM을 실행하는 동안에도 데이터 디스크를 연결하고 분리할 수 있지만, VM 리소스를 삭제하지 않는 한 OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="8a236-139">해당 VM이 중지 및 할당 취소된 상태에 있을 때에도 임대는 OS 디스크와 VM을 계속 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="8a236-140">VM을 복구하는 첫 번째 단계는 자체 VM 리소스를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="8a236-141">VM을 삭제하면 가상 하드 디스크는 저장소 계정에 남게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="8a236-142">VM을 삭제한 후 가상 하드 디스크를 다른 VM에 연결하여 문제와 오류를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="8a236-143">다음 예제에서는 리소스 그룹 `myResourceGroup`에서 VM `myVM`을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="8a236-144">가상 하드 디스크를 다른 VM에 연결 하기 전에 VM이 삭제 작업을 끝낼 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="8a236-145">VM과 연결하는 가상 하드 디스크의 임대는 가상 하드 디스크를 다른 VM에 연결하기 전에 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="8a236-146">기존 가상 하드 디스크를 다른 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="8a236-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="8a236-147">다음 몇 단계에서는 문제 해결을 위해 다른 VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="8a236-148">기존 가상 하드 디스크를 이 문제 해결 VM에 연결하여 디스크의 콘텐츠를 찾아 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="8a236-149">예를 들어 이 프로세스를 사용하면 구성 오류를 수정하거나 추가 응용 프로그램 또는 시스템 로그 파일을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="8a236-150">다른 VM을 선택하거나 만들어 문제 해결에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="8a236-151">기존 가상 하드 디스크를 연결하는 경우 이전 `azure vm show` 명령에서 획득한 디스크에 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="8a236-152">다음 예제에서는 리소스 그룹 `myResourceGroup`의 문제 해결 VM `myVMRecovery`에 기존 가상 하드 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="8a236-153">연결된 데이터 디스크 탑재</span><span class="sxs-lookup"><span data-stu-id="8a236-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="8a236-154">다음 예제에서는 Ubuntu VM에 필요한 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="8a236-155">Red Hat Enterprise Linux 또는 SUSE와 같은 다른 Linux 배포판을 사용하는 경우 로그 파일 위치와 `mount` 명령을 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="8a236-156">명령의 적절한 변경에 대한 특정 배포에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a236-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="8a236-157">적절한 자격 증명을 사용하여 문제 해결 VM에 대한 SSH입니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="8a236-158">이 디스크가 문제 해결 VM에 연결된 첫 번째 데이터 디스크인 경우 디스크는 `/dev/sdc`에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="8a236-159">`dmseg`를 사용하여 연결된 디스크를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="8a236-160">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="8a236-161">앞의 예제에서 OS 디스크는 `/dev/sda`에 있으며 각 VM에 제공된 임시 디스크는 `/dev/sdb`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="8a236-162">여러 데이터 디스크가 있는 경우 `/dev/sdd`, `/dev/sde` 등에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="8a236-163">디렉터리를 만들어 기존 가상 하드 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="8a236-164">다음 예제는 디렉터리 `troubleshootingdisk`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="8a236-165">기존 가상 하드 디스크에 여러 개의 파티션이 있는 경우 필수 파티션을 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="8a236-166">다음 예제에서는 `/dev/sdc1`에 첫 번째 주 파티션을 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="8a236-167">가상 하드 디스크의 UUID(Universally Unique Identifier)를 사용하여 Azure의 VM에 데이터 디스크를 마운트하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="8a236-168">이 짧은 문제 해결 시나리오에서는 UUID를 사용하여 가상 하드 디스크를 탑재할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="8a236-169">그러나 일반적인 사용 환경에서 UUID 대신 장치 이름을 사용하여 가상 하드 디스크를 탑재하기 위해 `/etc/fstab`을 편집하면 VM이 부팅되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="8a236-170">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8a236-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="8a236-171">기존 가상 하드 디스크가 탑재되면 이제 필요에 따라 모든 유지 관리 및 문제 해결 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="8a236-172">문제가 해결되면 다음 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="8a236-173">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="8a236-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="8a236-174">오류가 해결되면 문제 해결 VM에서 기존 가상 하드 디스크를 탑재 해제하고 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="8a236-175">가상 하드 디스크를 문제 해결 VM에 연결하는 임대가 해제될 때까지 가상 하드 디스크를 다른 VM과 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="8a236-176">SSH 세션에서 문제 해결 VM까지 기존 가상 하드 디스크를 탑재 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="8a236-177">먼저 탑재 지점에 대한 상위 디렉터리에서 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="8a236-178">이제 기존 가상 하드 디스크를 탑재 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="8a236-179">다음 예제는 `/dev/sdc1`에 있는 장치를 탑재 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="8a236-180">이제 VM에서 가상 하드 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="8a236-181">문제 해결 VM에 대한 SSH 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="8a236-182">Azure CLI에서 먼저 문제 해결 VM에 연결된 데이터 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="8a236-183">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVMRecovery`에 연결된 데이터 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="8a236-184">기존 가상 하드 디스크에 대한 `Lun` 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="8a236-185">다음 예제 명령 출력은 LUN 0에서 연결된 기존 가상 디스크를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="8a236-186">적용 가능한 `Lun` 값을 사용하여 VM에서 데이터 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="8a236-187">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="8a236-187">Create VM from original hard disk</span></span>
<span data-ttu-id="8a236-188">원래 가상 하드 디스크에서 VM을 만들려면 [이 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="8a236-189">실제 JSON 템플릿은 다음 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-189">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="8a236-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="8a236-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="8a236-191">템플릿은 이전 명령의 VHD URL을 사용하여 VM을 기존 가상 네트워크에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-191">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="8a236-192">다음 예제에서는 리소스 그룹 `myResourceGroup`에 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-192">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="8a236-193">VM 이름(다음 예제의 `myDeployedVM`), OS 유형(`Linux`) 및 VM 크기(`Standard_DS1_v2`) 등 템플릿에 대한 프롬프트에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-193">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="8a236-194">`osDiskVhdUri`는 기존 가상 하드 디스크를 문제 해결 VM에 연결할 때 이전에 사용된 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-194">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="8a236-195">명령 출력과 프롬프트의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-195">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="8a236-196">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="8a236-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="8a236-197">기존 가상 하드 디스크에서 VM을 만든 경우 부팅 진단을 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="8a236-198">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myDeployedVM`에서 진단 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a236-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="8a236-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a236-199">Next steps</span></span>
<span data-ttu-id="8a236-200">VM에 연결하는 데 문제가 있는 경우 [Azure VM에 SSH 연결 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a236-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8a236-201">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Linux VM에서 응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a236-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>