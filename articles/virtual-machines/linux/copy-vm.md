---
title: "Azure CLI 2.0을 사용 하 여 Linux VM aaaCopy | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure CLI 2.0 및 관리 하는 디스크를 사용 하 여 Azure Linux VM의 복사본입니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Azure CLI 2.0 및 Managed Disks를 사용하여 Linux VM의 복사본 만들기


이 문서에서는 Azure CLI 2.0 및 Azure 리소스 관리자 배포 모델 hello toocreate Linux를 사용 하 여 실행 중인 Azure 가상 컴퓨터 (VM)의 사본을 hello 하는 방법을 설명 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

[VHD에서 VM을 업로드하고 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)수도 있습니다.

## <a name="prerequisites"></a>필수 조건


-   [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치

-   Tooan 된 Azure 계정 로그인 [az 로그인](/cli/azure/#login)합니다.

-   Azure VM toouse 복사본에 대 한 hello 소스로 있어야 합니다.

## <a name="step-1-stop-hello-source-vm"></a>1 단계: hello 원본 VM 중지


사용 하 여 hello 원본 VM을 할당 취소 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.
hello 다음 예제에서는 할당 취소 hello 라는 VM **myVM** hello 리소스 그룹에 **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>2 단계: hello 원본 VM 복사


VM toocopy hello 기본 가상 하드 디스크의 복사본이 만들어집니다. 이 프로세스는 hello를 포함 하는 관리 되는 디스크도 특수화 된 VHD를 만듭니다 원본 VM 동일한 구성 및 hello로 설정 합니다.

Azure Managed Disks에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요. 

1.  해당 운영 체제 디스크의 각 VM 및 hello 이름 목록 [az vm 목록](/cli/azure/vm#list)합니다. hello 다음 예에서는 나열은 리소스 그룹에 모든 Vm **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  디스크를 사용 하 여 새 복사본 hello 디스크 관리 [az 디스크 만들기](/cli/azure/disk#create)합니다. hello 다음 예제에서는 명명 된 디스크 **myCopiedDisk** 관리 라는 디스크 hello에서 **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  이제 리소스 그룹에서에서 관리 하는 hello 디스크를 사용 하 여 확인 [az 디스크 목록](/cli/azure/disk#list)합니다. hello 다음 예에서는 나열 이라는 hello 리소스 그룹의 관리 되는 hello 디스크 **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  너무 건너뛸["3 단계: 가상 네트워크 설정"](#step-3-set-up-a-virtual-network)합니다.


## <a name="step-3-set-up-a-virtual-network"></a>3단계: 가상 네트워크 설정


hello 다음 옵션 단계로 만들 새 가상 네트워크, 서브넷, 공용 IP 주소 및 가상 네트워크 인터페이스 카드 (NIC).

용도 또는 추가 배포 문제 해결에 대 한 VM을 복사 하는 경우 하지 toouse 기존 가상 네트워크에 VM을 좋습니다.

복사 된 Vm에 대 한 가상 네트워크 인프라 toocreate 하려는 경우에 따라 hello 다음 몇 가지 단계입니다. Toocreate 가상 네트워크를 사용 하지 않으려는 경우 너무 건너뜁니다[4 단계: VM 만들기](#step-4-create-a-vm)합니다.

1.  사용 하 여 hello 가상 네트워크 만들기 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 **myVnet** 및 명명 된 서브넷 **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  [az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP를 만듭니다. hello 다음 예제에서는 명명 된 공용 IP **myPublicIP** 의 hello DNS 이름을 가진 **mypublicdns**합니다. (이므로 고유 이름을 제공, 고유 해야 hello DNS 이름입니다.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Hello NIC를 사용 하 여 만들 [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다.
    hello 다음 예제에서는 명명 된 NIC **myNic** 는 연결 된 toothe **mySubnet** 서브넷:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>4단계: VM 만들기

이제 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들 수 있습니다.

관리 되는 디스크 toouse hello OS 디스크로 복사 하는 hello 지정 (--os-디스크 연결), 다음과 같습니다.

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>다음 단계

toolearn 어떻게 toouse Azure CLI toomanage 새 VM 참조 [hello Azure 리소스 관리자에 대 한 Azure CLI 명령을](../azure-cli-arm-commands.md)합니다.
