---
title: "Linux VM hello Azure CLI 1.0로 문제 해결 a aaaUse | Microsoft Docs"
description: "Linux VM 연결 hello OS 디스크 tooa 복구 VM 사용 하 여 발급 tootroubleshoot Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="94447-103">Linux VM hello OS 디스크 tooa 복구 VM을 연결 하 여 문제 해결 Azure CLI 1.0 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="94447-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="94447-104">Linux 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="94447-105">일반적인 예로 것에 잘못 된 항목이 `/etc/fstab` hello VM 성공적으로 tooboot 수 없도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="94447-106">이 문서에 자세히 설명 방법 toouse hello Azure CLI 1.0 tooconnect 가상 하드 디스크 tooanother Linux VM toofix 오류를 다음 다시 원래 VM를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94447-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="94447-107">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="94447-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="94447-108">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="94447-109">[Azure CLI 1.0](#recovery-process-overview) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="94447-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="94447-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="94447-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="94447-111">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="94447-111">Recovery process overview</span></span>
<span data-ttu-id="94447-112">hello 문제 해결 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="94447-113">Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="94447-114">첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Linux VM에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="94447-115">Toohello VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="94447-116">파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="94447-117">탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="94447-118">Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94447-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="94447-119">확인 했는지 [최신 Azure CLI 1.0 hello](../../cli-install-nodejs.md) 및 설치 하 고,에 로그인 하 고, 리소스 관리자 모드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="94447-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="94447-120">Hello 다음 예에서는 매개 변수 이름은 고유한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="94447-121">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="94447-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="94447-122">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="94447-122">Determine boot issues</span></span>
<span data-ttu-id="94447-123">VM 없는 이유 수 tooboot 올바르게 hello 직렬 출력 toodetermine를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="94447-124">일반적인 예로에 잘못 된 항목이 `/etc/fstab`, 또는 삭제 또는 이동 되 고 가상 하드 디스크를 기본 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="94447-125">hello 다음 예제에서는 가져옵니다 hello 직렬 출력 hello 라는 VM에서에서 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="94447-126">검토 hello 직렬 toodetermine hello VM tooboot를 실패 한 이유를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="94447-127">Hello 직렬 출력 되지 않습니다 되었다는 메시지를 제공 하는 경우 tooreview 로그 파일을 할 수 있습니다 `/var/log` 하드 디스크 연결 VM 문제 해결 tooa hello 가상 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="94447-128">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="94447-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="94447-129">가상 하드 디스크 tooanother VM에 연결할 수 있습니다, 전에 hello 가상 하드 디스크 (VHD)의 tooidentify hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="94447-130">hello 다음 예제에서는 가져옵니다 hello 라는 VM에 대 한 정보 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="94447-131">검색할 `Vhd URI` hello 명령 앞에서 hello 출력에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="94447-132">hello 다음 잘린된 예제는 출력 hello `Vhd URI` hello 마지막 줄에:</span><span class="sxs-lookup"><span data-stu-id="94447-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
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


## <a name="delete-existing-vm"></a><span data-ttu-id="94447-133">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="94447-133">Delete existing VM</span></span>
<span data-ttu-id="94447-134">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="94447-135">가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94447-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="94447-136">hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="94447-137">각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="94447-138">데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="94447-139">hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94447-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="94447-140">첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="94447-141">VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="94447-142">VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="94447-143">다음 예에서는 삭제 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에서 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="94447-144">Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="94447-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="94447-145">hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="94447-146">기존 가상 하드 디스크 tooanother VM 연결</span><span class="sxs-lookup"><span data-stu-id="94447-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="94447-147">에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="94447-148">Hello 기존 가상 하드 디스크 toothis VM toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="94447-149">이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템.</span><span class="sxs-lookup"><span data-stu-id="94447-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="94447-150">선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94447-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="94447-151">Hello 기존 가상 하드 디스크를 연결할 경우 hello 앞에서 만든 hello URL toohello 디스크 지정 `azure vm show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="94447-152">hello 다음 예제에서는 연결 가상 컴퓨터 V 문제를 해결 하는 기존 가상 하드 디스크 toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="94447-153">Hello 연결 된 데이터 디스크를 탑재</span><span class="sxs-lookup"><span data-stu-id="94447-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="94447-154">hello 다음 예에서는 Ubuntu VM에서 필요한 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="94447-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="94447-155">Red Hat Enterprise Linux, SUSE 등 다른 Linux 배포판을 사용 하는 경우 로그 파일 위치 hello 및 `mount` 명령을 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="94447-156">명령에 적절 한 변경 내용 hello에 대 한 특정 프로그램 distro toohello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94447-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="94447-157">SSH tooyour hello 적절 한 자격 증명을 사용 하 여 VM의 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="94447-158">이 디스크 hello 첫 번째 데이터 연결 된 디스크 tooyour VM 문제 해결 이면 hello 디스크가 연결 되어 있고 가능성이 너무`/dev/sdc`합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="94447-159">사용 하 여 `dmseg` tooview 연결 된 디스크:</span><span class="sxs-lookup"><span data-stu-id="94447-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="94447-160">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="94447-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="94447-161">앞 예제는 hello, hello OS 디스크에는 `/dev/sda` 및 hello 임시 디스크에는 각 VM에 대해 제공 된 `/dev/sdb`합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="94447-162">여러 데이터 디스크가 있는 경우 `/dev/sdd`, `/dev/sde` 등에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="94447-163">디렉터리 toomount 기존 가상 하드 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94447-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="94447-164">hello 다음 예에서는 라는 디렉터리를 만듭니다 `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="94447-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="94447-165">기존 가상 하드 디스크에 파티션이 여러 개 있으면 필요한 hello 파티션을 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="94447-166">hello 다음 예제에서는 탑재 hello에서 첫 번째 주 파티션 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="94447-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="94447-167">사용 하 여 Azure에서 Vm에 데이터 디스크 toomount hello hello 가상 하드 디스크의 범용 고유 식별자 (UUID) 하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="94447-168">이 짧은 문제 해결 시나리오에 대 한 탑재 hello 가상 하드 디스크 UUID hello를 사용 하 여 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="94447-169">그러나 일반적인 사용에서 편집 `/etc/fstab` toomount 가상 하드 디스크 UUID 않을 대신 장치 이름을 사용 하 여 VM toofail tooboot hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="94447-170">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="94447-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="94447-171">이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="94447-172">Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="94447-173">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="94447-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="94447-174">프로그램 오류가 해결 되 면 분리 하 고 문제 해결 VM에서 hello 기존 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="94447-175">VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="94447-176">Hello SSH 세션 tooyour VM 문제 해결에서 hello 기존 가상 하드 디스크를 분리 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94447-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="94447-177">먼저 탑재 지점에 대 한 부모 디렉터리 hello 밖으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="94447-178">이제 hello 기존 가상 하드 디스크를 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="94447-179">hello 다음 예제에서는 분리 hello 해당 장치 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="94447-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="94447-180">이제 hello hello VM에서에서 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="94447-181">Hello SSH 세션 tooyour VM 문제 해결을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="94447-182">Hello Azure CLI, 첫 번째 목록 hello 데이터 디스크 tooyour VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="94447-183">hello 목록 hello 데이터 디스크는 다음 예제에서는 연결 된 가상 컴퓨터 V toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="94447-184">참고 hello `Lun` 기존 가상 하드 디스크에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="94447-185">hello 다음 예제에서는 명령은 출력 LUN 0에 연결 된 hello 기존 가상 디스크:</span><span class="sxs-lookup"><span data-stu-id="94447-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="94447-186">적용 가능한 hello를 사용 하 여 VM에서 hello 데이터 디스크를 분리 `Lun` 값:</span><span class="sxs-lookup"><span data-stu-id="94447-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="94447-187">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="94447-187">Create VM from original hard disk</span></span>
<span data-ttu-id="94447-188">원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="94447-189">실제 JSON 템플릿 hello 링크 hello에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94447-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="94447-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="94447-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="94447-191">hello에서 VHD URL hello를 사용 하 여 기존 가상 네트워크를으로 VM을 배포 하는 hello 템플릿 이전 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="94447-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="94447-192">hello 다음 예제에서는 배포 이라는 hello 템플릿 toohello 리소스 그룹 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="94447-193">VM 이름 같은 hello 서식 파일에 대 한 응답 hello 라는 메시지가 표시 (`myDeployedVM` 예제 다음 hello), OS 유형 (`Linux`), 및 VM 크기 (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="94447-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="94447-194">hello `osDiskVhdUri` hello 기존 가상 하드 디스크 toohello VM 문제 해결을 연결할 때 이전에 사용 되는 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94447-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="94447-195">Hello 명령 출력 및 표시 되는 메시지의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
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
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="94447-196">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="94447-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="94447-197">Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94447-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="94447-198">hello 다음 예에서는 가상 컴퓨터 V hello에 진단 확장 hello `myDeployedVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="94447-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="94447-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94447-199">Next steps</span></span>
<span data-ttu-id="94447-200">Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="94447-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="94447-201">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Linux VM에서 응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94447-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
