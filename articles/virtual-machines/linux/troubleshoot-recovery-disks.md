---
title: "Linux VM hello Azure CLI 2.0 문제 해결 a aaaUse | Microsoft Docs"
description: "Linux VM 연결 hello OS 디스크 tooa 복구 VM 사용 하 여 발급 tootroubleshoot Azure CLI 2.0 hello 하는 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="11e37-103">Linux VM Azure CLI 2.0 hello로 hello OS 디스크 tooa 복구 VM을 연결 하 여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="11e37-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="11e37-104">Linux 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="11e37-105">일반적인 예로 것에 잘못 된 항목이 `/etc/fstab` hello VM 성공적으로 tooboot 수 없도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="11e37-106">이 문서에 자세히 설명 방법 toouse hello Azure CLI 2.0 tooconnect 가상 하드 디스크 tooanother Linux VM toofix 오류를 다음 다시 원래 VM를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="11e37-107">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="11e37-108">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="11e37-108">Recovery process overview</span></span>
<span data-ttu-id="11e37-109">hello 문제 해결 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="11e37-110">Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="11e37-111">첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Linux VM에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="11e37-112">Toohello VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="11e37-113">파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="11e37-114">탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="11e37-115">Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="11e37-116">tooperform 이러한 문제 해결 단계를 최신 버전의 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="11e37-117">Hello 다음 예에서는 매개 변수 이름은 고유한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="11e37-118">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="11e37-119">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="11e37-119">Determine boot issues</span></span>
<span data-ttu-id="11e37-120">VM 없는 이유 수 tooboot 올바르게 hello 직렬 출력 toodetermine를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="11e37-121">일반적인 예로에 잘못 된 항목이 `/etc/fstab`, 또는 삭제 또는 이동 되 고 가상 하드 디스크를 기본 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="11e37-122">사용 하 여 hello 부팅 로그 가져오기 [az vm 부팅 진단 get-부팅-로그](/cli/azure/vm/boot-diagnostics#get-boot-log)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="11e37-123">hello 다음 예제에서는 가져옵니다 hello 직렬 출력 hello 라는 VM에서에서 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="11e37-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="11e37-124">검토 hello 직렬 toodetermine hello VM tooboot를 실패 한 이유를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="11e37-125">Hello 직렬 출력 되지 않습니다 되었다는 메시지를 제공 하는 경우 tooreview 로그 파일을 할 수 있습니다 `/var/log` 하드 디스크 연결 VM 문제 해결 tooa hello 가상 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="11e37-126">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="11e37-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="11e37-127">가상 하드 디스크 (VHD) tooanother VM에 연결할 수 있습니다, 전에 tooidentify hello hello OS 디스크의 URI 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="11e37-128">[az vm show](/cli/azure/vm#show)를 사용하여 VM에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="11e37-129">사용 하 여 hello `--query` 플래그 tooextract hello URI toohello OS 디스크.</span><span class="sxs-lookup"><span data-stu-id="11e37-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="11e37-130">hello 다음 예제에서는 가져옵니다 hello 라는 VM의 디스크 정보 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="11e37-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="11e37-131">hello URI는 너무 유사**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="11e37-132">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="11e37-132">Delete existing VM</span></span>
<span data-ttu-id="11e37-133">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="11e37-134">가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="11e37-135">hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="11e37-136">각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="11e37-137">데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="11e37-138">hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="11e37-139">첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="11e37-140">VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="11e37-141">VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="11e37-142">삭제 사용 하 여 VM hello [az vm 삭제](/cli/azure/vm#delete)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="11e37-143">다음 예에서는 삭제 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에서 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="11e37-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="11e37-144">Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="11e37-145">hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="11e37-146">기존 가상 하드 디스크 tooanother VM 연결</span><span class="sxs-lookup"><span data-stu-id="11e37-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="11e37-147">에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="11e37-148">Hello 기존 가상 하드 디스크 toothis VM toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="11e37-149">이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템.</span><span class="sxs-lookup"><span data-stu-id="11e37-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="11e37-150">선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="11e37-151">Hello 기존 가상 하드 디스크를 연결 된 [az vm 관리 되지 않는 디스크 연결](/cli/azure/vm/unmanaged-disk#attach)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="11e37-152">Hello 기존 가상 하드 디스크를 연결할 경우 hello 앞에서 만든 hello URI toohello 디스크 지정 `az vm show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="11e37-153">hello 다음 예제에서는 연결 가상 컴퓨터 V 문제를 해결 하는 기존 가상 하드 디스크 toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="11e37-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="11e37-154">Hello 연결 된 데이터 디스크를 탑재</span><span class="sxs-lookup"><span data-stu-id="11e37-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="11e37-155">hello 다음 예에서는 Ubuntu VM에서 필요한 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="11e37-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="11e37-156">Red Hat Enterprise Linux, SUSE 등 다른 Linux 배포판을 사용 하는 경우 로그 파일 위치 hello 및 `mount` 명령을 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="11e37-157">명령에 적절 한 변경 내용 hello에 대 한 특정 프로그램 distro toohello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="11e37-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="11e37-158">SSH tooyour hello 적절 한 자격 증명을 사용 하 여 VM의 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="11e37-159">이 디스크 hello 첫 번째 데이터 연결 된 디스크 tooyour VM 문제 해결 이면 hello 디스크가 연결 되어 있고 가능성이 너무`/dev/sdc`합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="11e37-160">사용 하 여 `dmseg` tooview 연결 된 디스크:</span><span class="sxs-lookup"><span data-stu-id="11e37-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="11e37-161">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="11e37-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="11e37-162">앞 예제는 hello, hello OS 디스크에는 `/dev/sda` 및 hello 임시 디스크에는 각 VM에 대해 제공 된 `/dev/sdb`합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="11e37-163">여러 데이터 디스크가 있는 경우 `/dev/sdd`, `/dev/sde` 등에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="11e37-164">디렉터리 toomount 기존 가상 하드 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="11e37-165">hello 다음 예에서는 라는 디렉터리를 만듭니다 `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="11e37-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="11e37-166">기존 가상 하드 디스크에 파티션이 여러 개 있으면 필요한 hello 파티션을 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="11e37-167">hello 다음 예제에서는 탑재 hello에서 첫 번째 주 파티션 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="11e37-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="11e37-168">사용 하 여 Azure에서 Vm에 데이터 디스크 toomount hello hello 가상 하드 디스크의 범용 고유 식별자 (UUID) 하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="11e37-169">이 짧은 문제 해결 시나리오에 대 한 탑재 hello 가상 하드 디스크 UUID hello를 사용 하 여 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="11e37-170">그러나 일반적인 사용에서 편집 `/etc/fstab` toomount 가상 하드 디스크 UUID 않을 대신 장치 이름을 사용 하 여 VM toofail tooboot hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="11e37-171">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="11e37-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="11e37-172">이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="11e37-173">Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="11e37-174">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="11e37-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="11e37-175">프로그램 오류가 해결 되 면 분리 하 고 문제 해결 VM에서 hello 기존 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="11e37-176">VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="11e37-177">Hello SSH 세션 tooyour VM 문제 해결에서 hello 기존 가상 하드 디스크를 분리 하십시오.</span><span class="sxs-lookup"><span data-stu-id="11e37-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="11e37-178">먼저 탑재 지점에 대 한 부모 디렉터리 hello 밖으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="11e37-179">이제 hello 기존 가상 하드 디스크를 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="11e37-180">hello 다음 예제에서는 분리 hello 해당 장치 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="11e37-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="11e37-181">이제 hello hello VM에서에서 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="11e37-182">Hello SSH 세션 tooyour VM 문제 해결을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="11e37-183">목록 hello 연결 된 VM의 문제를 해결 하는 데이터 디스크 tooyour [az vm 관리 되지 않는 디스크 목록](/cli/azure/vm/unmanaged-disk#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="11e37-184">hello 목록 hello 데이터 디스크는 다음 예제에서는 연결 된 가상 컴퓨터 V toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="11e37-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="11e37-185">기존 가상 하드 디스크에 대 한 참고 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="11e37-186">예를 들어 있는 디스크의 hello 이름 hello의 URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** 은 **myVHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="11e37-187">VM에서 hello 데이터 디스크를 분리 [az vm 관리 되지 않는 디스크 분리](/cli/azure/vm/unmanaged-disk#detach)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="11e37-188">hello 다음 예제에서는 분리 hello 디스크 이름은 `myVHD` hello 라는 VM에서에서 `myVMRecovery` hello에 `myResourceGroup` 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="11e37-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="11e37-189">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="11e37-189">Create VM from original hard disk</span></span>
<span data-ttu-id="11e37-190">원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="11e37-191">실제 JSON 템플릿 hello 링크 hello에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="11e37-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="11e37-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="11e37-193">hello 템플릿 VM을 배포 hello에서 VHD URI hello를 사용 하 여 이전 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="11e37-194">배포 된 hello 템플릿 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="11e37-195">Hello URI tooyour 제공 원본 VHD 다음 hello 운영 체제 종류, VM 크기 및 VM 이름을 다음과 같이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="11e37-196">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="11e37-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="11e37-197">Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="11e37-198">[az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable)을 사용하여 부팅 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="11e37-199">hello 다음 예에서는 가상 컴퓨터 V hello에 진단 확장 hello `myDeployedVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="11e37-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="11e37-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11e37-200">Next steps</span></span>
<span data-ttu-id="11e37-201">Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="11e37-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="11e37-202">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Linux VM에서 응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11e37-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
