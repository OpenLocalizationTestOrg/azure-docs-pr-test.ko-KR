---
title: "Azure CLI 1.0 hello로 Linux VM의 OS aaaExpand 디스크 | Microsoft Docs"
description: "Tooexpand hello Azure CLI 1.0 및 hello 리소스 관리자 배포 모델을 사용 하 여 Linux VM의 운영 체제 (OS) 가상 디스크를 hello 하는 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Azure CLI 1.0 hello로 hello Azure CLI를 사용 하 여 Linux VM의 OS 디스크를 확장 합니다.
hello 운영 체제 (OS) hello 기본 가상 하드 디스크 크기는 Azure에서 Linux 가상 컴퓨터 (VM)에서 일반적으로 30GB입니다. 할 수 있습니다 [데이터 디스크를 추가](add-disk.md) 추가 저장소 공간을 위한 tooprovide tooexpand hello OS 디스크를 수도 있습니다. 이 문서는 hello Azure CLI 1.0로 관리 되지 않는 디스크를 사용 하 여 Linux VM에 대 한 tooexpand hello OS 디스크 하는 방법을 설명 합니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#prerequisites) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](expand-disks.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="prerequisites"></a>필수 조건
Hello 필요한 [최신 Azure CLI 1.0](../../cli-install-nodejs.md) 설치 하 고 tooan 로그인 [Azure 계정](https://azure.microsoft.com/pricing/free-trial/) 다음과 같이 hello Resource Manager 모드를 사용 하 여:

```azurecli
azure config mode arm
```

Hello 다음 예제를 원하는 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup* 및 *myVM*이 포함됩니다.

## <a name="expand-os-disk"></a>OS 디스크 확장

1. VM hello로 가상 하드 디스크에 대 한 작업을 수행할 수 없습니다 실행 합니다. hello 다음 예제에서는 중지 하 고 hello 라는 VM의 할당을 취소할 *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`hello 계산 리소스를 해제 하지 않습니다. toorelease 계산 리소스를 사용 하 여 `azure vm deallocate`합니다. hello VM tooexpand hello 가상 하드 디스크를 해제 해야 합니다.

2. Hello를 사용 하 여 hello 관리 되지 않는 운영 체제 디스크의 hello 크기를 업데이트할 `azure vm set` 명령입니다. 다음 예에서는 업데이트 hello hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. 다음과 같이 VM을 시작합니다.

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM hello 적절 한 자격 증명을 사용 합니다. tooverify hello 운영 체제 디스크 크기가 조정 되었으므로, 사용 하 여 `df -h`합니다. 다음 예제 출력 hello hello 주 파티션 (*/개발/sda1*) 50GB 포함 되었습니다.

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>다음 단계
추가 저장소가 필요 하면도 [추가 데이터 디스크 tooa Linux VM](add-disk.md)합니다. 디스크 암호화에 대 한 자세한 내용은 참조 [Encrypt 디스크를 사용 하 여 Linux VM에 Azure CLI hello](encrypt-disks.md)합니다.
