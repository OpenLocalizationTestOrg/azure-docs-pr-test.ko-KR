---
title: "SMB를 사용 하 여 Linux Vm에 Azure 파일 저장소 aaaMount | Microsoft Docs"
description: "Azure 파일 저장소를 SMB를 사용 하 여 Linux Vm에서 toomount Azure CLI 2.0 hello 하는 방법"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="cac98-103">SMB를 사용하여 Linux VM에 Azure File Storage 탑재</span><span class="sxs-lookup"><span data-stu-id="cac98-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="cac98-104">이 문서에서는 hello Azure CLI 2.0을 사용 하 여 tooutilize hello Azure 파일 저장소 서비스는 SMB를 사용 하 여 Linux VM에 탑재 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="cac98-105">Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 hello 클라우드에서 파일 공유를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="cac98-106">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cac98-107">hello 요구 사항은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-107">hello requirements are:</span></span>

- [<span data-ttu-id="cac98-108">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="cac98-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="cac98-109">SSH 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="cac98-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="cac98-110">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="cac98-110">Quick Commands</span></span>

* <span data-ttu-id="cac98-111">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="cac98-111">A resource group</span></span>
* <span data-ttu-id="cac98-112">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="cac98-112">An Azure virtual network</span></span>
* <span data-ttu-id="cac98-113">SSH 인바운드를 사용하는 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="cac98-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="cac98-114">서브넷</span><span class="sxs-lookup"><span data-stu-id="cac98-114">A subnet</span></span>
* <span data-ttu-id="cac98-115">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="cac98-115">An Azure storage account</span></span>
* <span data-ttu-id="cac98-116">Azure Storage 계정 키</span><span class="sxs-lookup"><span data-stu-id="cac98-116">Azure storage account keys</span></span>
* <span data-ttu-id="cac98-117">Azure File Storage 공유</span><span class="sxs-lookup"><span data-stu-id="cac98-117">An Azure File storage share</span></span>
* <span data-ttu-id="cac98-118">Linux VM</span><span class="sxs-lookup"><span data-stu-id="cac98-118">A Linux VM</span></span>

<span data-ttu-id="cac98-119">모든 예제를 고유한 설정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="cac98-120">로컬 탑재 hello에 대 한 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="cac98-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="cac98-121">탑재 hello 파일 저장소 SMB 공유 toohello 탑재 지점</span><span class="sxs-lookup"><span data-stu-id="cac98-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="cac98-122">Hello 탑재 한 다시 부팅 후 유지</span><span class="sxs-lookup"><span data-stu-id="cac98-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="cac98-123">toodo 줄 toohello 다음 hello를 따라서 추가 `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="cac98-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cac98-124">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="cac98-124">Detailed walkthrough</span></span>

<span data-ttu-id="cac98-125">파일 저장소 hello 표준 SMB 프로토콜을 사용 하는 hello 클라우드에서 파일 공유를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="cac98-126">파일 저장소의 최신 릴리스에서 hello SMB 3.0을 지원 하는 모든 운영 체제에서 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="cac98-127">SMB 탑재를 사용 하 여 Linux에서 tooa 강력 하 고 영구 보관 저장소 위치는 SLA에서 지원 되는 쉽게 백업을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="cac98-128">파일 저장소에서 호스팅되는 VM tooan SMB 탑재에서 파일을 이동 위한 훌륭한 방법 toodebug 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="cac98-129">Hello 동일한 SMB 공유를 로컬에서 탑재할 수 없어서 즉 tooyour Mac, Linux 또는 Windows 워크스테이션.</span><span class="sxs-lookup"><span data-stu-id="cac98-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="cac98-130">SMB Linux 스트리밍에 대 한 최상의 솔루션 hello 아니거나 hello SMB 프로토콜 없기 때문에 응용 프로그램 로그를 실시간으로 toohandle 있다면 이러한 고급 로깅 작업을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="cac98-131">Linux 및 응용 프로그램 로그 출력을 수집하려는 경우 Fluentd와 같은 전용 통합 로깅 계층 도구가 SMB보다 더 적합할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="cac98-132">자세한 연습이 필요한 toofirst hello 파일 저장소 공유를 만든 다음 SMB를 통해 Linux VM에 탑재 hello 필수 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="cac98-133">리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) toohold hello 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="cac98-134">리소스 그룹 이름이 toocreate `myResourceGroup` hello "West US" 위치에서에서 다음 예제는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="cac98-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="cac98-135">Azure 저장소 계정을 만든 [az 저장소 계정에 create](/cli/azure/storage/account#create) toostore hello 실제 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="cac98-136">저장소 계정 toocreate 이라는 mystorageaccount hello Standard_LRS 저장소 SKU를 사용 하 여 hello 다음 예제를 사용 하 여 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="cac98-137">Hello 저장소 계정 키를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="cac98-138">저장소 계정을 만들 때 서비스 중단 없이 회전할 수 있도록 hello 계정 키 쌍에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="cac98-139">두 번째 키 toohello hello 쌍에서을 전환 하면 새 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="cac98-140">새 저장소 계정 키 쌍을 확보 하는 항상 하나 이상 사용 되지 않는 저장소 계정 키 준비 tooswitch을 항상 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="cac98-141">Hello로 hello 저장소 계정 키를 보려면 [az 저장소 계정 키 목록](/cli/azure/storage/account/keys#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="cac98-142">명명 된 hello에 대 한 저장소 계정 키를 hello `mystorageaccount` hello 다음 예제에에서 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="cac98-143">tooextract 한 개의 키를 사용 하 여 hello `--query` 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="cac98-144">hello 다음 예제에서는 추출 hello 첫 번째 키 (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="cac98-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="cac98-145">Hello 파일 저장소 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-145">Create hello File storage share.</span></span>

    <span data-ttu-id="cac98-146">hello와 SMB 공유를 포함 하는 hello 파일 저장소 공유 [az 저장소 공유 만들기](/cli/azure/storage/share#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="cac98-147">hello 할당량은 항상 기가바이트 (GB) 단위로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="cac98-148">Hello 앞에서 hello 키 중 하나에서 전달 `az storage account keys list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="cac98-149">다음 예제는 hello를 사용 하 여 10GB 할당량이 있는 mystorageshare 라는 공유 만들기:</span><span class="sxs-lookup"><span data-stu-id="cac98-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="cac98-150">탑재 지점 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="cac98-151">Hello Linux 파일 시스템 toomount hello에 SMB 공유의 로컬 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="cac98-152">아무 것도 기록 하거나 hello 로컬 탑재 디렉터리에서 읽을 파일 저장소에서 호스팅되는 SMB 공유 toohello를 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="cac98-153">toocreate/mnt/mymountdirectory 사용 하 여 hello 다음 예제에서 로컬 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="cac98-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="cac98-154">Hello SMB 공유 toohello 로컬 디렉터리를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="cac98-155">다음과 같이 고유한 저장소 계정 사용자 이름 및 hello 탑재 자격 증명에 대 한 저장소 계정 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="cac98-156">SMB를 통해 재부팅 탑재 hello를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="cac98-157">Linux VM hello를 다시 부팅 하면 hello 탑재 된 SMB 공유 경우 탑재 된 종료 하는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="cac98-158">SMB 공유에서 부팅, tooremount hello 줄 toohello Linux /etc/fstab을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="cac98-159">Linux는 hello 부팅 프로세스 중 필요 하다 고 판단 toomount hello fstab 파일 toolist hello 파일 시스템을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="cac98-160">추가 hello SMB 공유 hello 파일 저장소 공유 하는 hello Linux VM에 대 한 영구적으로 마운트된 파일 시스템을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="cac98-161">Hello 파일 저장소 SMB 공유 tooa 추가 새 VM 클라우드 초기화를 사용 하는 경우 가능한를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cac98-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="cac98-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cac98-162">Next steps</span></span>

- [<span data-ttu-id="cac98-163">클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cac98-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="cac98-164">디스크 tooa Linux VM 추가</span><span class="sxs-lookup"><span data-stu-id="cac98-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="cac98-165">Hello Azure CLI를 사용 하 여 Linux VM에서 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="cac98-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
