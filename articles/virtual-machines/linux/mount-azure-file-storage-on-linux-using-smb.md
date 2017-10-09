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
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>SMB를 사용하여 Linux VM에 Azure File Storage 탑재

이 문서에서는 hello Azure CLI 2.0을 사용 하 여 tooutilize hello Azure 파일 저장소 서비스는 SMB를 사용 하 여 Linux VM에 탑재 하는 방법을 보여 줍니다. Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 hello 클라우드에서 파일 공유를 제공 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. hello 요구 사항은 같습니다.

- [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)
- [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>빠른 명령

* 리소스 그룹
* Azure Virtual Network
* SSH 인바운드를 사용하는 네트워크 보안 그룹
* 서브넷
* Azure Storage 계정
* Azure Storage 계정 키
* Azure File Storage 공유
* Linux VM

모든 예제를 고유한 설정으로 바꿉니다.

### <a name="create-a-directory-for-hello-local-mount"></a>로컬 탑재 hello에 대 한 디렉터리 만들기

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>탑재 hello 파일 저장소 SMB 공유 toohello 탑재 지점

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Hello 탑재 한 다시 부팅 후 유지
toodo 줄 toohello 다음 hello를 따라서 추가 `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>자세한 연습

파일 저장소 hello 표준 SMB 프로토콜을 사용 하는 hello 클라우드에서 파일 공유를 제공 합니다. 파일 저장소의 최신 릴리스에서 hello SMB 3.0을 지원 하는 모든 운영 체제에서 파일 공유를 탑재할 수 있습니다. SMB 탑재를 사용 하 여 Linux에서 tooa 강력 하 고 영구 보관 저장소 위치는 SLA에서 지원 되는 쉽게 백업을 얻게 됩니다.

파일 저장소에서 호스팅되는 VM tooan SMB 탑재에서 파일을 이동 위한 훌륭한 방법 toodebug 로그입니다. Hello 동일한 SMB 공유를 로컬에서 탑재할 수 없어서 즉 tooyour Mac, Linux 또는 Windows 워크스테이션. SMB Linux 스트리밍에 대 한 최상의 솔루션 hello 아니거나 hello SMB 프로토콜 없기 때문에 응용 프로그램 로그를 실시간으로 toohandle 있다면 이러한 고급 로깅 작업을 작성 합니다. Linux 및 응용 프로그램 로그 출력을 수집하려는 경우 Fluentd와 같은 전용 통합 로깅 계층 도구가 SMB보다 더 적합할 것입니다.

자세한 연습이 필요한 toofirst hello 파일 저장소 공유를 만든 다음 SMB를 통해 Linux VM에 탑재 hello 필수 구성 요소를 만듭니다.

1. 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) toohold hello 파일 공유 합니다.

    리소스 그룹 이름이 toocreate `myResourceGroup` hello "West US" 위치에서에서 다음 예제는 hello를 사용 하 여:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Azure 저장소 계정을 만든 [az 저장소 계정에 create](/cli/azure/storage/account#create) toostore hello 실제 파일입니다.

    저장소 계정 toocreate 이라는 mystorageaccount hello Standard_LRS 저장소 SKU를 사용 하 여 hello 다음 예제를 사용 하 여 입력 합니다.

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Hello 저장소 계정 키를 표시 합니다.

    저장소 계정을 만들 때 서비스 중단 없이 회전할 수 있도록 hello 계정 키 쌍에 만들어집니다. 두 번째 키 toohello hello 쌍에서을 전환 하면 새 키 쌍을 만듭니다. 새 저장소 계정 키 쌍을 확보 하는 항상 하나 이상 사용 되지 않는 저장소 계정 키 준비 tooswitch을 항상 생성 됩니다.

    Hello로 hello 저장소 계정 키를 보려면 [az 저장소 계정 키 목록](/cli/azure/storage/account/keys#list)합니다. 명명 된 hello에 대 한 저장소 계정 키를 hello `mystorageaccount` hello 다음 예제에에서 나열 됩니다.

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract 한 개의 키를 사용 하 여 hello `--query` 플래그입니다. hello 다음 예제에서는 추출 hello 첫 번째 키 (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Hello 파일 저장소 공유를 만듭니다.

    hello와 SMB 공유를 포함 하는 hello 파일 저장소 공유 [az 저장소 공유 만들기](/cli/azure/storage/share#create)합니다. hello 할당량은 항상 기가바이트 (GB) 단위로 표현 됩니다. Hello 앞에서 hello 키 중 하나에서 전달 `az storage account keys list` 명령입니다. 다음 예제는 hello를 사용 하 여 10GB 할당량이 있는 mystorageshare 라는 공유 만들기:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. 탑재 지점 디렉터리를 만듭니다.

    Hello Linux 파일 시스템 toomount hello에 SMB 공유의 로컬 디렉터리를 만듭니다. 아무 것도 기록 하거나 hello 로컬 탑재 디렉터리에서 읽을 파일 저장소에서 호스팅되는 SMB 공유 toohello를 전달 됩니다. toocreate/mnt/mymountdirectory 사용 하 여 hello 다음 예제에서 로컬 디렉터리:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Hello SMB 공유 toohello 로컬 디렉터리를 탑재 합니다.

    다음과 같이 고유한 저장소 계정 사용자 이름 및 hello 탑재 자격 증명에 대 한 저장소 계정 키를 제공 합니다.

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. SMB를 통해 재부팅 탑재 hello를 유지 합니다.

    Linux VM hello를 다시 부팅 하면 hello 탑재 된 SMB 공유 경우 탑재 된 종료 하는 동안 있습니다. SMB 공유에서 부팅, tooremount hello 줄 toohello Linux /etc/fstab을 추가 합니다. Linux는 hello 부팅 프로세스 중 필요 하다 고 판단 toomount hello fstab 파일 toolist hello 파일 시스템을 사용 합니다. 추가 hello SMB 공유 hello 파일 저장소 공유 하는 hello Linux VM에 대 한 영구적으로 마운트된 파일 시스템을 확인 합니다. Hello 파일 저장소 SMB 공유 tooa 추가 새 VM 클라우드 초기화를 사용 하는 경우 가능한를 있습니다.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>다음 단계

- [클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [디스크 tooa Linux VM 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Hello Azure CLI를 사용 하 여 Linux VM에서 디스크 암호화](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
