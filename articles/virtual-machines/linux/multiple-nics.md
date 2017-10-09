---
title: "여러 Nic 사용 하 여 Azure에서 Linux VM aaaCreate | Microsoft Docs"
description: "여러 Nic 사용 하 여 Linux VM toocreate tooit hello Azure CLI 2.0 또는 리소스 관리자 템플릿을 사용 하 여 연결 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>여러 네트워크와 Azure에서 Linux 가상 컴퓨터를 toocreate 인터페이스 카드 방법
여러 가상 네트워크 인터페이스 (Nic) 연결 된 tooit가 Azure에서 가상 컴퓨터 (VM)를 만들 수 있습니다. 일반적인 시나리오는 toohave 프런트 엔드 및 백 엔드 연결에 대 한 서로 다른 서브넷 또는 네트워크를 전용 tooa 모니터링 또는 백업 솔루션입니다. 이 문서에 설명 하 고 여러 Nic 사용 하 여 VM toocreate tooit 연결 방법 기존 VM에서 Nic tooadd 또는 제거 합니다. 자세한 정보에 대 한 방법을 toocreate 자신의 내에서 여러 Nic를 이용한 적 비롯 하 여 스크립트에 대해 자세히 알아보세요 [다중 NIC Vm을 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)합니다. [VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.

이 문서와 여러 Nic 사용 하 여 VM a toocreate Azure CLI 2.0 hello 하는 방법을 설명 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](multiple-nics-nodejs.md)합니다.


## <a name="create-supporting-resources"></a>지원 리소스 만들기
최신 설치 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *myVM*이 포함됩니다.

먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

Hello 가상 네트워크를 만듭니다 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 와 명명 된 서브넷 *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

사용 하 여 백 엔드 트래픽 hello에 대 한 서브넷을 만든 [만드는 az 네트워크 vnet 서브넷](/cli/azure/network/vnet/subnet#create)합니다. hello 다음 예제에서는 서브넷을 만듭니다. 명명 된 *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

[az network nsg create](/cli/azure/network/nsg#create)를 사용하여 네트워크 보안 그룹을 만듭니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>여러 NIC 만들기 및 구성
[az network nic create](/cli/azure/network/nic#create)를 사용하여 두 개의 NIC를 만듭니다. hello 다음 예제에서는 라는 두 개의 nic가 *myNic1* 및 *myNic2*관계, hello 네트워크 보안 그룹을 tooeach 서브넷 연결 NIC 1 개:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>VM을 만들고 hello Nic 연결
Hello Nic 지정 hello VM을 만들 때 사용 하 여 만든 `--nics`합니다. 또한 해야 tootake 주의 hello v M 크기를 선택 합니다. hello tooa VM을 추가할 수 있는 Nic의 총 수에 대 한 제한이 있습니다. [Linux VM 크기](sizes.md)에 대해 자세히 읽어보세요. 

[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>NIC tooa VM 추가
여러 Nic를 사용 하 여 VM을 만든 hello 이전 단계입니다. 또한 Nic tooan hello Azure CLI 2.0 함께 존재 하는 VM을 추가할 수 있습니다. 

[az network nic create](/cli/azure/network/nic#create)를 사용하여 다른 NIC를 만듭니다. hello 다음 예제에서는 명명 된 NIC *myNic3* toohello 백 엔드 서브넷과 hello 이전 단계에서 만든 네트워크 보안 그룹을 연결 합니다.

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

NIC tooan tooadd 기존의 VM에 할당을 먼저 해제의 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다. hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

추가 인 NIC와 hello [az vm nic 추가](/cli/azure/vm/nic#add)합니다. hello 다음 예제에서는 추가 *myNic3* 너무*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

시작의 VM hello [az vm 시작](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>VM에서 NIC 제거
기존 VM에서 NIC tooremove 할당 hello VM을 먼저 해제와 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다. hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

제거 인 NIC와 hello [az vm nic 제거](/cli/azure/vm/nic#remove)합니다. hello 다음 예제에서는 제거 *myNic3* 에서 *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

시작의 VM hello [az vm 시작](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>Resource Manager 템플릿을 사용하여 여러 NIC 만들기
Azure 리소스 관리자 템플릿 선언적 JSON 파일 toodefine 환경의 사용 합니다. [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)에 대해 읽어볼 수 있습니다. 리소스 관리자 템플릿을 여러 Nic를 만들 때 처럼 배포 하는 동안 방식으로 toocreate 리소스를 여러 개 제공 합니다. 사용 하면 *복사* 인스턴스 toocreate toospecify hello 수:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

[*복사*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)에 대해 자세히 읽어보세요. 

사용할 수도 있습니다는 `copyIndex()` toothen toocreate 수 있는 숫자 tooa 자원 이름을 추가 `myNic1`, `myNic2`, 등 hello 다음 hello 인덱스 값을 추가 하는 모양의 예제가 나와 있습니다.

```json
"name": "[concat('myNic', copyIndex())]", 
```

[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.

## <a name="next-steps"></a>다음 단계
검토 [Linux VM 크기](sizes.md) toocreating 여러 Nic 사용 하 여 VM을 시도할 때. 각 VM 크기가 지원 Nic의 주의 기울여야 toohello 최대 수를 지불 합니다. 
