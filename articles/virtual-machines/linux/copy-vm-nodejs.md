---
title: "Azure CLI 1.0 hello로 Linux VM의 복사본을 aaaCreate | Microsoft Docs"
description: "와 Azure Linux 가상 컴퓨터의 복사본 toocreate Azure CLI 1.0 hello 리소스 관리자 배포 모델에서 hello 하는 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Azure CLI 1.0 hello로 Azure에서 실행 중인 Linux 가상 컴퓨터의 복사본 만들기
이 문서에서는 toocreate Azure 가상 컴퓨터 (VM) 실행 중인 Linux 사용 하 여 프로그램의 복사본을 리소스 관리자 배포 모델을 hello 하는 방법을 설명 합니다. 먼저 hello 운영 체제 및 데이터 디스크 tooa 새 컨테이너를 통해 다음 hello 네트워크 리소스를 설정 복사한 hello 새 가상 컴퓨터를 만듭니다.

[사용자 지정 디스크 이미지에서 VM 업로드 및 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)수도 있습니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- Azure CLI 1.0 – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="before-you-begin"></a>시작하기 전에
Hello hello 단계를 시작 하기 전에 필수 구성 요소를 다음을 충족 하는지 확인 합니다.

* Hello 있는 [Azure CLI](../../cli-install-nodejs.md) 다운로드 하 고 컴퓨터에 설치 합니다. 
* 또한 기존 Azure Linux VM에 대한 다음과 같은 몇 가지 정보가 필요합니다.

| 소스 VM 정보 | 여기서 tooget 것 |
| --- | --- |
| VM 이름 |`azure vm list` |
| 리소스 그룹 이름 |`azure vm list` |
| 위치 |`azure vm list` |
| 저장소 계정 이름 |`azure storage account list -g <resourceGroup>` |
| 컨테이너 이름 |`azure storage container list -a <sourcestorageaccountname>` |
| 소스 VM VHD 파일 이름 |`azure storage blob list --container <containerName>` |

* 새 VM에 대 한 약간의 조정이 toomake이 필요 합니다.   <br> -컨테이너 이름    <br> -VM 이름    <br> -VM 크기    <br> -vNet 이름    <br> -SubNet 이름    <br> -IP 이름    <br> -NIC 이름

## <a name="login-and-set-your-subscription"></a>로그인 및 구독 설정
1. 로그인 toohello CLI 합니다.

    ```azurecli
    azure login
    ```
2. Resource Manager 모드에 있는지 확인합니다.

    ```azurecli
    azure config mode arm
    ```
3. Hello 올바른 구독을 설정 합니다. 'Azure 계정 목록' toosee에서는 모든 구독.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Hello VM 중지
중지 하 고 hello 원본 VM 할당을 취소 합니다. 구독 및 해당 리소스 그룹 이름은 'azure vm 목록' tooget hello Vm의 모든 목록을 사용할 수 있습니다.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Hello VHD 복사
Hello를 사용 하 여 hello 원본 저장소 toohello 대상에서 hello VHD를 복사할 수 있습니다 `azure storage blob copy start`합니다. 이 예제에서는 toocopy hello VHD toohello 것 이며 동일한 저장소 계정에는 있지만 다른 컨테이너입니다.

toocopy hello VHD tooanother 컨테이너 hello에 동일한 저장소 계정, 유형:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>새 VM에 대 한 hello 가상 네트워크를 설정 합니다.
새 VM에 대한 가상 네트워크 및 NIC를 설정합니다. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>만들 새 VM hello
업로드 된 가상 디스크에서 이제 VM을 만들 수 있습니다 [리소스 관리자 템플릿을 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) 또는 디스크를 입력 하 여 hello URI tooyour를 지정 하 여 CLI hello를 통해 복사:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>다음 단계
toolearn 어떻게 toouse Azure CLI toomanage 새 가상 컴퓨터에 참조 [hello Azure 리소스 관리자에 대 한 Azure CLI 명령을](../azure-cli-arm-commands.md)합니다.

