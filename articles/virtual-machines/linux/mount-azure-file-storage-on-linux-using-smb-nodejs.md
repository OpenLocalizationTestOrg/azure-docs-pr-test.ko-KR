---
title: "Azure CLI 1.0에서 SMB를 사용하여 Linux VM에 Azure File Storage 탑재 | Microsoft Docs"
description: "SMB를 사용하여 Linux VM에 Azure File Storage를 탑재하는 방법"
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
ms.openlocfilehash: 4951860630f0aad107d0846d52ebe4423ee0b91c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="2a9ed-103">Azure CLI 1.0에서 SMB를 사용하여 Linux VM에 Azure File Storage 탑재</span><span class="sxs-lookup"><span data-stu-id="2a9ed-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="2a9ed-104">이 문서에서는 SMB(서버 메시지 블록) 프로토콜을 사용하여 Linux VM에서 Azure File Storage를 탑재하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-104">This article shows how to mount Azure File storage on a Linux VM by using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="2a9ed-105">File Storage는 표준 SMB 프로토콜을 통해 클라우드에서 파일 공유를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-105">File storage offers file shares in the cloud via the standard SMB protocol.</span></span> <span data-ttu-id="2a9ed-106">요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-106">The requirements are:</span></span>

* <span data-ttu-id="2a9ed-107">[Azure 계정](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="2a9ed-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="2a9ed-108">SSH(Secure Shell) 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="2a9ed-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-to-use"></a><span data-ttu-id="2a9ed-109">사용할 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="2a9ed-109">CLI versions to use</span></span>
<span data-ttu-id="2a9ed-110">다음 CLI(명령줄 인터페이스) 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-110">You can complete the task by using one of the following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="2a9ed-111">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="2a9ed-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2a9ed-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="2a9ed-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="2a9ed-113">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="2a9ed-113">Quick commands</span></span>
<span data-ttu-id="2a9ed-114">태스크를 신속하게 수행하려면 이 섹션의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-114">To accomplish the task quickly, follow the steps in this section.</span></span> <span data-ttu-id="2a9ed-115">자세한 정보 및 컨텍스트는 ["자세한 연습"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) 섹션을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-115">For more detailed information and context, begin at the ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2a9ed-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2a9ed-116">Prerequisites</span></span>
* <span data-ttu-id="2a9ed-117">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="2a9ed-117">A resource group</span></span>
* <span data-ttu-id="2a9ed-118">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="2a9ed-118">An Azure virtual network</span></span>
* <span data-ttu-id="2a9ed-119">SSH 인바운드를 사용하는 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="2a9ed-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="2a9ed-120">서브넷</span><span class="sxs-lookup"><span data-stu-id="2a9ed-120">A subnet</span></span>
* <span data-ttu-id="2a9ed-121">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="2a9ed-121">An Azure storage account</span></span>
* <span data-ttu-id="2a9ed-122">Azure Storage 계정 키</span><span class="sxs-lookup"><span data-stu-id="2a9ed-122">Azure storage account keys</span></span>
* <span data-ttu-id="2a9ed-123">Azure File Storage 공유</span><span class="sxs-lookup"><span data-stu-id="2a9ed-123">An Azure File storage share</span></span>
* <span data-ttu-id="2a9ed-124">Linux VM</span><span class="sxs-lookup"><span data-stu-id="2a9ed-124">A Linux VM</span></span>

<span data-ttu-id="2a9ed-125">모든 예제를 고유한 설정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="2a9ed-126">로컬 탑재를 위한 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="2a9ed-126">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="2a9ed-127">File Storage SMB 공유를 탑재 지점에 탑재</span><span class="sxs-lookup"><span data-stu-id="2a9ed-127">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="2a9ed-128">다시 부팅한 후 탑재 유지</span><span class="sxs-lookup"><span data-stu-id="2a9ed-128">Persist the mount after a reboot</span></span>
<span data-ttu-id="2a9ed-129">다음 줄을 `/etc/fstab`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-129">Add the following line to `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="2a9ed-130">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="2a9ed-130">Detailed walkthrough</span></span>

<span data-ttu-id="2a9ed-131">File Storage는 표준 SMB 프로토콜을 사용하는 클라우드에서 파일 공유를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-131">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="2a9ed-132">File Storage의 최신 릴리스를 사용하면 SMB 3.0을 지원하는 OS에서 파일 공유를 탑재할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-132">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="2a9ed-133">Linux에서 SMB 탑재를 사용하면 SLA에서 지원되는 강력한 영구 보관 저장소 위치에 쉽게 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-133">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="2a9ed-134">VM에서 File Storage에서 호스팅되는 SMB 탑재로 파일을 이동하는 것은 로그를 디버깅하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-134">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="2a9ed-135">동일한 SMB 공유를 Mac, Linux 또는 Windows 워크스테이션에 로컬로 탑재하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-135">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="2a9ed-136">SMB 프로토콜이 이러한 과도한 로깅 작업을 다루도록 빌드되지 않았기 때문에 SMB는 Linux 또는 응용 프로그램 로그를 실시간으로 스트리밍하기 위한 최선의 솔루션은 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-136">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="2a9ed-137">Linux 및 응용 프로그램 로그 출력을 수집하려는 경우 Fluentd와 같은 전용 통합 로깅 계층 도구가 SMB보다 더 적합할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="2a9ed-138">이 자세한 연습 과정에서는 먼저 File Storage 공유를 만드는 데 필요한 필수 구성 요소 만든 다음 Linux VM에서 SMB를 통해 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-138">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="2a9ed-139">다음 코드를 사용하여 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-139">Create an Azure storage account by using the following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="2a9ed-140">저장소 계정 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-140">Show the storage account keys.</span></span>

    <span data-ttu-id="2a9ed-141">저장소 계정을 만드는 경우 서비스 중단 없이 키를 순환할 수 있도록 저장소 계정 키는 쌍으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-141">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="2a9ed-142">쌍에서 두 번째 키로 전환하는 경우 새 키 쌍이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-142">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="2a9ed-143">새 저장소 계정 키는 항상 쌍으로 만들어지므로 항상 사용하지 않은 저장소 키를 전환할 준비가 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready to switch to.</span></span> <span data-ttu-id="2a9ed-144">저장소 계정 키를 표시하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-144">To show the storage account keys, use the following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="2a9ed-145">File Storage 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-145">Create the File storage share.</span></span>

    <span data-ttu-id="2a9ed-146">File Storage 공유는 SMB 공유를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-146">The File storage share contains the SMB share.</span></span> <span data-ttu-id="2a9ed-147">할당량은 항상 GB(기가바이트) 단위로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="2a9ed-148">File Storage 공유를 만들려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-148">To create the File storage share, use the following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="2a9ed-149">탑재 지점 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-149">Create the mount-point directory.</span></span>

    <span data-ttu-id="2a9ed-150">Linux 파일 시스템에서 로컬 디렉터리를 만들어서 SMB 공유를 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-150">You must create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="2a9ed-151">로컬 탑재 디렉터리에서 쓰거나 읽은 모든 내용은 File Storage에 호스팅된 SMB 공유로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-151">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="2a9ed-152">디렉터리를 만들려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-152">To create the directory, use the following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="2a9ed-153">다음 코드를 사용하여 SMB 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-153">Mount the SMB share by using the following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="2a9ed-154">재부팅을 통해 SMB 탑재를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-154">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="2a9ed-155">Linux VM를 다시 부팅하면 탑재된 SMB 공유가 종료하는 동안 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-155">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="2a9ed-156">부팅 시 SMB 공유를 다시 탑재하려면 Linux /etc/fstab에 줄을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-156">To remount the SMB share on boot, you must add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="2a9ed-157">Linux는 부팅 프로세스 중에 탑재해야 하는 파일 시스템을 나열하기 위해 /etc/fstab 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-157">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="2a9ed-158">SMB 공유를 추가하면 File Storage 공유가 Linux VM용으로 영구히 탑재된 파일 시스템이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-158">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="2a9ed-159">cloud-init를 사용하는 경우 File Storage SMB 공유를 새 VM에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a9ed-159">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="2a9ed-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a9ed-160">Next steps</span></span>

- [<span data-ttu-id="2a9ed-161">cloud-init를 사용하여 생성 중인 Linux VM 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2a9ed-161">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="2a9ed-162">Linux VM에 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="2a9ed-162">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="2a9ed-163">Azure CLI를 사용하여 Linux VM에서 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="2a9ed-163">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
