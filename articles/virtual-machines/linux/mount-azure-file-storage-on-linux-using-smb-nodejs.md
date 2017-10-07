---
title: "Azure CLI 1.0과 함께 SMB를 사용 하 여 Linux Vm에서 Azure 파일 저장소 aaaMount | Microsoft Docs"
description: "어떻게 toomount SMB를 사용 하 여 Linux Vm에서 Azure 파일 저장소"
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
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="52da8-103">Azure CLI 1.0에서 SMB를 사용하여 Linux VM에 Azure File Storage 탑재</span><span class="sxs-lookup"><span data-stu-id="52da8-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="52da8-104">이 문서에서는 toomount Azure 파일 저장소를 사용 하 여 Linux VM에 서버 메시지 블록 (SMB) 프로토콜을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="52da8-105">파일 저장소 파일 공유 hello 표준 SMB 프로토콜을 통해 hello 클라우드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="52da8-106">hello 요구 사항은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-106">hello requirements are:</span></span>

* <span data-ttu-id="52da8-107">[Azure 계정](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="52da8-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="52da8-108">SSH(Secure Shell) 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="52da8-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="52da8-109">CLI 버전 toouse</span><span class="sxs-lookup"><span data-stu-id="52da8-109">CLI versions toouse</span></span>
<span data-ttu-id="52da8-110">Hello CLI (명령줄 인터페이스) 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="52da8-111">[Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="52da8-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="52da8-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="52da8-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="52da8-113">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="52da8-113">Quick commands</span></span>
<span data-ttu-id="52da8-114">신속 하 게 tooaccomplish hello 작업 hello이이 섹션의에서 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="52da8-115">Hello에 대 한 정보와 컨텍스트를 자세한 시작 ["자세한 연습"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) 섹션.</span><span class="sxs-lookup"><span data-stu-id="52da8-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="52da8-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="52da8-116">Prerequisites</span></span>
* <span data-ttu-id="52da8-117">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="52da8-117">A resource group</span></span>
* <span data-ttu-id="52da8-118">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="52da8-118">An Azure virtual network</span></span>
* <span data-ttu-id="52da8-119">SSH 인바운드를 사용하는 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="52da8-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="52da8-120">서브넷</span><span class="sxs-lookup"><span data-stu-id="52da8-120">A subnet</span></span>
* <span data-ttu-id="52da8-121">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="52da8-121">An Azure storage account</span></span>
* <span data-ttu-id="52da8-122">Azure Storage 계정 키</span><span class="sxs-lookup"><span data-stu-id="52da8-122">Azure storage account keys</span></span>
* <span data-ttu-id="52da8-123">Azure File Storage 공유</span><span class="sxs-lookup"><span data-stu-id="52da8-123">An Azure File storage share</span></span>
* <span data-ttu-id="52da8-124">Linux VM</span><span class="sxs-lookup"><span data-stu-id="52da8-124">A Linux VM</span></span>

<span data-ttu-id="52da8-125">모든 예제를 고유한 설정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="52da8-126">로컬 탑재 hello에 대 한 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="52da8-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="52da8-127">탑재 hello 파일 저장소 SMB 공유 toohello 탑재 지점</span><span class="sxs-lookup"><span data-stu-id="52da8-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="52da8-128">Hello 탑재 한 다시 부팅 후 유지</span><span class="sxs-lookup"><span data-stu-id="52da8-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="52da8-129">다음 줄을 너무 hello 추가`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="52da8-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="52da8-130">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="52da8-130">Detailed walkthrough</span></span>

<span data-ttu-id="52da8-131">파일 저장소 hello 표준 SMB 프로토콜을 사용 하는 hello 클라우드에서 파일 공유를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="52da8-132">파일 저장소의 최신 릴리스에서 hello SMB 3.0을 지원 하는 모든 운영 체제에서 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="52da8-133">SMB 탑재를 사용 하 여 Linux에서 tooa 강력 하 고 영구 보관 저장소 위치는 SLA에서 지원 되는 쉽게 백업을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="52da8-134">파일 저장소에서 호스팅되는 VM tooan SMB 탑재에서 파일을 이동 위한 훌륭한 방법 toodebug 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="52da8-135">Hello 동일한 SMB 공유를 로컬에서 탑재할 수 없어서 즉 tooyour Mac, Linux 또는 Windows 워크스테이션.</span><span class="sxs-lookup"><span data-stu-id="52da8-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="52da8-136">SMB Linux 스트리밍에 대 한 최상의 솔루션 hello 아니거나 hello SMB 프로토콜 없기 때문에 응용 프로그램 로그를 실시간으로 toohandle 있다면 이러한 고급 로깅 작업을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="52da8-137">Linux 및 응용 프로그램 로그 출력을 수집하려는 경우 Fluentd와 같은 전용 통합 로깅 계층 도구가 SMB보다 더 적합할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="52da8-138">자세한 연습이 필요한 toofirst hello 파일 저장소 공유를 만든 다음 SMB를 통해 Linux VM에 탑재 hello 필수 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="52da8-139">코드 다음 hello를 사용 하 여 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="52da8-140">Hello 저장소 계정 키를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="52da8-141">저장소 계정을 만들 때 서비스 중단 없이 회전할 수 있도록 hello 계정 키 쌍에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="52da8-142">두 번째 키 toohello hello 쌍에서을 전환 하면 새 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="52da8-143">새 저장소 계정 키 쌍을 확보 하는 항상 하나 이상 사용 되지 않는 저장소 키 준비 tooswitch을 항상 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="52da8-144">tooshow hello 저장소 계정 키 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="52da8-145">Hello 파일 저장소 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-145">Create hello File storage share.</span></span>

    <span data-ttu-id="52da8-146">hello 파일 저장소 공유 hello SMB 공유를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="52da8-147">hello 할당량은 항상 기가바이트 (GB) 단위로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="52da8-148">toocreate 파일 저장소 공유 hello, 코드 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="52da8-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="52da8-149">Hello 탑재 지점 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="52da8-150">Hello Linux 파일 시스템 toomount hello에 SMB 공유의 로컬 디렉터리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="52da8-151">아무 것도 기록 하거나 hello 로컬 탑재 디렉터리에서 읽을 파일 저장소에서 호스팅되는 SMB 공유 toohello를 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="52da8-152">사용 하 여 hello 코드 다음 toocreate hello 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="52da8-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="52da8-153">Hello 코드 다음 hello를 사용 하 여 SMB 공유를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="52da8-154">SMB를 통해 재부팅 탑재 hello를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="52da8-155">Linux VM hello를 다시 부팅 하면 hello 탑재 된 SMB 공유 경우 탑재 된 종료 하는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="52da8-156">부팅 시 tooremount hello SMB 공유를 줄 toohello Linux /etc/fstab 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="52da8-157">Linux는 hello 부팅 프로세스 중 필요 하다 고 판단 toomount hello fstab 파일 toolist hello 파일 시스템을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="52da8-158">추가 hello SMB 공유 hello 파일 저장소 공유 하는 hello Linux VM에 대 한 영구적으로 마운트된 파일 시스템을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="52da8-159">Hello 파일 저장소 SMB 공유 tooa 추가 새 VM 클라우드 초기화를 사용 하는 경우 가능한를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52da8-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="52da8-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52da8-160">Next steps</span></span>

- [<span data-ttu-id="52da8-161">클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="52da8-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="52da8-162">디스크 tooa Linux VM 추가</span><span class="sxs-lookup"><span data-stu-id="52da8-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="52da8-163">Hello Azure CLI를 사용 하 여 Linux VM에서 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="52da8-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
