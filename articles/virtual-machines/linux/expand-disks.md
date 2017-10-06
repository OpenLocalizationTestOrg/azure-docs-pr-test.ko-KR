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
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Tooexpand 가상 하드 디스크 사용 하 여 Linux VM에 Azure CLI hello 하는 방법
hello 운영 체제 (OS) hello 기본 가상 하드 디스크 크기는 Azure에서 Linux 가상 컴퓨터 (VM)에서 일반적으로 30GB입니다. 있습니다 수 [데이터 디스크를 추가](add-disk.md) 추가 저장소 공간을 위한 tooprovide 라면 tooexpand 기존 데이터 디스크. 이 문서 tooexpand hello Azure CLI 2.0을 사용 하 여 Linux VM에 대 한 디스크를 관리 하는 방법을 설명 합니다. Hello로 관리 되지 않는 hello OS 디스크를 확장할 수도 있습니다 [Azure CLI 1.0](expand-disks-nodejs.md)합니다.

> [!WARNING]
> 항상 디스크 크기 조정 작업을 수행하기 전에 데이터를 백업해야 합니다. 자세한 내용은 [Azure에서 Linux VM 백업](tutorial-backup-vms.md)을 참조하세요.

## <a name="expand-disk"></a>디스크 확장
Hello 최신 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

이 문서는 Azure에 데이터 디스크가 하나 이상 연결되고 준비된 기존 VM이 필요합니다. 사용할 수 있는 VM이 아직 없는 경우 [데이터 디스크가 있는 VM 만들기 및 준비](tutorial-manage-disks.md#create-and-attach-disks)를 참조하세요.

Hello 다음 예제를 원하는 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup* 및 *myVM*이 포함됩니다.

1. VM hello로 가상 하드 디스크에 대 한 작업을 수행할 수 없습니다 실행 합니다. [az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 VM의 할당을 취소합니다. hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`hello 계산 리소스를 해제 하지 않습니다. toorelease 계산 리소스를 사용 하 여 `az vm deallocate`합니다. hello VM tooexpand hello 가상 하드 디스크를 해제 해야 합니다.

2. 이제 [az disk list](/cli/azure/disk#list)를 사용하여 리소스 그룹에서 Managed Disks 목록을 봅니다. hello 다음 예제에서는 표시는 관리 되는 디스크의 목록을 이라는 hello 리소스 그룹에 *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Hello 필요한 디스크와 확장 [az 디스크 업데이트](/cli/azure/disk#update)합니다. hello 다음 예제에서는 확장 이름이 관리 되는 디스크 hello *myDataDisk* toobe *200*4gb:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > 관리 되는 디스크를 확장 하면 hello 업데이트 크기는 관리 되는 디스크 크기에 가장 가까운 매핑된 toohello입니다. Hello 사용 가능한 관리 되는 디스크 크기와 계층의 테이블을 참조 하십시오. [Azure 관리 되는 디스크 개요-가격 및 요금 청구](../windows/managed-disks-overview.md#pricing-and-billing)합니다.

3. [az vm start](/cli/azure/vm#start)를 사용하여 VM을 시작합니다. 다음 예에서는 시작 하는 hello hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM hello 적절 한 자격 증명을 사용 합니다. Hello를 사용 하 여 VM의 공용 IP 주소를 가져올 수 있습니다 [az vm 표시](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. toouse hello 디스크를 확장 하 고 tooexpand hello 기본 파티션 및 파일 시스템 사용 해야 합니다.

    a. 이미 탑재 hello 디스크를 분리 합니다.

    ```bash
    sudo umount /dev/sdc1
    ```

    b. 사용 하 여 `parted` tooview 디스크 정보 및 hello 파티션 크기를 조정 합니다.

    ```bash
    sudo parted /dev/sdc
    ```

    Hello와 기존 파티션 레이아웃에 대 한 정보를 볼 `print`합니다. hello는 비슷한 toohello 다음 hello 기본 디스크의 크기 215 Gb는 보여 주는 예제 출력:

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

    c. Hello 파티션에 확장 `resizepart`합니다. Hello 파티션 번호를 입력 *1*, 새 파티션 hello에 대 한 크기 및:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, 입력`quit`

5. 크기를 조정 하는 hello 파티션과 hello 파티션 일관성을 확인 `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Hello 파일 시스템으로 크기를 조정할 `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. 탑재 hello 파티션 toohello 원하는 위치와 같은 `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. tooverify hello 운영 체제 디스크 크기가 조정 되었으므로, 사용 하 여 `df -h`합니다. 다음 예제 출력 hello hello 데이터 드라이브를 보여 줍니다. */개발/sdc1*, 200GB 포함 되었습니다.

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>다음 단계
추가 저장소가 필요 하면도 [추가 데이터 디스크 tooa Linux VM](add-disk.md)합니다. 디스크 암호화에 대 한 자세한 내용은 참조 [Encrypt 디스크를 사용 하 여 Linux VM에 Azure CLI hello](encrypt-disks.md)합니다.
