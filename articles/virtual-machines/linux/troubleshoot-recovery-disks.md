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
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Linux VM Azure CLI 2.0 hello로 hello OS 디스크 tooa 복구 VM을 연결 하 여 문제 해결
Linux 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다. 일반적인 예로 것에 잘못 된 항목이 `/etc/fstab` hello VM 성공적으로 tooboot 수 없도록 방지 합니다. 이 문서에 자세히 설명 방법 toouse hello Azure CLI 2.0 tooconnect 가상 하드 디스크 tooanother Linux VM toofix 오류를 다음 다시 원래 VM를 만듭니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.


## <a name="recovery-process-overview"></a>복구 프로세스 개요
hello 문제 해결 과정은 다음과 같습니다.

1. Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.
2. 첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Linux VM에 탑재 합니다.
3. Toohello VM 문제 해결을 연결 합니다. 파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.
4. 탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.
5. Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.

tooperform 이러한 문제 해결 단계를 최신 버전의 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예에서는 매개 변수 이름은 고유한 값으로 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.


## <a name="determine-boot-issues"></a>부팅 문제 확인
VM 없는 이유 수 tooboot 올바르게 hello 직렬 출력 toodetermine를 검사 합니다. 일반적인 예로에 잘못 된 항목이 `/etc/fstab`, 또는 삭제 또는 이동 되 고 가상 하드 디스크를 기본 환영 합니다.

사용 하 여 hello 부팅 로그 가져오기 [az vm 부팅 진단 get-부팅-로그](/cli/azure/vm/boot-diagnostics#get-boot-log)합니다. hello 다음 예제에서는 가져옵니다 hello 직렬 출력 hello 라는 VM에서에서 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

검토 hello 직렬 toodetermine hello VM tooboot를 실패 한 이유를 출력 합니다. Hello 직렬 출력 되지 않습니다 되었다는 메시지를 제공 하는 경우 tooreview 로그 파일을 할 수 있습니다 `/var/log` 하드 디스크 연결 VM 문제 해결 tooa hello 가상 있으면 합니다.


## <a name="view-existing-virtual-hard-disk-details"></a>기존 가상 하드 디스크 세부 정보 보기
가상 하드 디스크 (VHD) tooanother VM에 연결할 수 있습니다, 전에 tooidentify hello hello OS 디스크의 URI 해야 합니다. 

[az vm show](/cli/azure/vm#show)를 사용하여 VM에 대한 정보를 볼 수 있습니다. 사용 하 여 hello `--query` 플래그 tooextract hello URI toohello OS 디스크. hello 다음 예제에서는 가져옵니다 hello 라는 VM의 디스크 정보 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

hello URI는 너무 유사**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**합니다.

## <a name="delete-existing-vm"></a>기존 VM 삭제
가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다. 가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다. hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다. 각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다. 데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다. hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.

첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다. VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다. VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.

삭제 사용 하 여 VM hello [az vm 삭제](/cli/azure/vm#delete)합니다. 다음 예에서는 삭제 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에서 `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다. hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>기존 가상 하드 디스크 tooanother VM 연결
에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다. Hello 기존 가상 하드 디스크 toothis VM toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다. 이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템. 선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.

Hello 기존 가상 하드 디스크를 연결 된 [az vm 관리 되지 않는 디스크 연결](/cli/azure/vm/unmanaged-disk#attach)합니다. Hello 기존 가상 하드 디스크를 연결할 경우 hello 앞에서 만든 hello URI toohello 디스크 지정 `az vm show` 명령입니다. hello 다음 예제에서는 연결 가상 컴퓨터 V 문제를 해결 하는 기존 가상 하드 디스크 toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Hello 연결 된 데이터 디스크를 탑재

> [!NOTE]
> hello 다음 예에서는 Ubuntu VM에서 필요한 hello 단계. Red Hat Enterprise Linux, SUSE 등 다른 Linux 배포판을 사용 하는 경우 로그 파일 위치 hello 및 `mount` 명령을 약간 다를 수 있습니다. 명령에 적절 한 변경 내용 hello에 대 한 특정 프로그램 distro toohello 설명서를 참조 하십시오.

1. SSH tooyour hello 적절 한 자격 증명을 사용 하 여 VM의 문제를 해결 합니다. 이 디스크 hello 첫 번째 데이터 연결 된 디스크 tooyour VM 문제 해결 이면 hello 디스크가 연결 되어 있고 가능성이 너무`/dev/sdc`합니다. 사용 하 여 `dmseg` tooview 연결 된 디스크:

    ```bash
    dmesg | grep SCSI
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    앞 예제는 hello, hello OS 디스크에는 `/dev/sda` 및 hello 임시 디스크에는 각 VM에 대해 제공 된 `/dev/sdb`합니다. 여러 데이터 디스크가 있는 경우 `/dev/sdd`, `/dev/sde` 등에 있어야 합니다.

2. 디렉터리 toomount 기존 가상 하드 디스크를 만듭니다. hello 다음 예에서는 라는 디렉터리를 만듭니다 `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. 기존 가상 하드 디스크에 파티션이 여러 개 있으면 필요한 hello 파티션을 탑재 합니다. hello 다음 예제에서는 탑재 hello에서 첫 번째 주 파티션 `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > 사용 하 여 Azure에서 Vm에 데이터 디스크 toomount hello hello 가상 하드 디스크의 범용 고유 식별자 (UUID) 하는 것이 가장 좋습니다. 이 짧은 문제 해결 시나리오에 대 한 탑재 hello 가상 하드 디스크 UUID hello를 사용 하 여 필요는 없습니다. 그러나 일반적인 사용에서 편집 `/etc/fstab` toomount 가상 하드 디스크 UUID 않을 대신 장치 이름을 사용 하 여 VM toofail tooboot hello 합니다.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>원래 가상 하드 디스크의 문제 해결
이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다. Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>원래 가상 하드 디스크의 탑재 해제 및 분리
프로그램 오류가 해결 되 면 분리 하 고 문제 해결 VM에서 hello 기존 가상 하드 디스크를 분리 합니다. VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.

1. Hello SSH 세션 tooyour VM 문제 해결에서 hello 기존 가상 하드 디스크를 분리 하십시오. 먼저 탑재 지점에 대 한 부모 디렉터리 hello 밖으로 변경 합니다.

    ```bash
    cd /
    ```

    이제 hello 기존 가상 하드 디스크를 탑재 해제 합니다. hello 다음 예제에서는 분리 hello 해당 장치 `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. 이제 hello hello VM에서에서 가상 하드 디스크를 분리 합니다. Hello SSH 세션 tooyour VM 문제 해결을 종료 합니다. 목록 hello 연결 된 VM의 문제를 해결 하는 데이터 디스크 tooyour [az vm 관리 되지 않는 디스크 목록](/cli/azure/vm/unmanaged-disk#list)합니다. hello 목록 hello 데이터 디스크는 다음 예제에서는 연결 된 가상 컴퓨터 V toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    기존 가상 하드 디스크에 대 한 참고 hello 이름입니다. 예를 들어 있는 디스크의 hello 이름 hello의 URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** 은 **myVHD**합니다. 

    VM에서 hello 데이터 디스크를 분리 [az vm 관리 되지 않는 디스크 분리](/cli/azure/vm/unmanaged-disk#detach)합니다. hello 다음 예제에서는 분리 hello 디스크 이름은 `myVHD` hello 라는 VM에서에서 `myVMRecovery` hello에 `myResourceGroup` 리소스 그룹:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>원래 하드 디스크에서 VM 만들기
원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)합니다. 실제 JSON 템플릿 hello 링크 hello에 됩니다.

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

hello 템플릿 VM을 배포 hello에서 VHD URI hello를 사용 하 여 이전 명령입니다. 배포 된 hello 템플릿 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다. Hello URI tooyour 제공 원본 VHD 다음 hello 운영 체제 종류, VM 크기 및 VM 이름을 다음과 같이 지정 합니다.

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>부트 진단 다시 사용
Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다. [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable)을 사용하여 부팅 진단을 사용하도록 설정합니다. hello 다음 예에서는 가상 컴퓨터 V hello에 진단 확장 hello `myDeployedVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>다음 단계
Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Linux VM에서 응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.
