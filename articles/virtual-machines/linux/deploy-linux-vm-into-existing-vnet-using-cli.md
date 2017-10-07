---
title: "Linux Vm의 경우 Azure CLI 2.0의 기존 네트워크에 aaaDeploy | Microsoft Docs"
description: "Toodeploy Linux 가상 컴퓨터를 사용 하 여 기존 가상 네트워크에 Azure CLI 2.0 hello 하는 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>어떻게 toodeploy hello Azure CLI로 기존 Azure 가상 네트워크로 Linux 가상 컴퓨터

이 문서에서는 어떻게 toouse hello Azure CLI 2.0 toodeploy 가상 컴퓨터 (VM)는 기존 가상 네트워크로 합니다. hello 요구 사항은 같습니다.

- [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)
- [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md)

Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md)합니다.


## <a name="quick-commands"></a>빠른 명령
Hello 작업을 수행를 tooquickly가 필요한 경우 다음 단원을 hello 필요한 hello 명령에 자세히 설명 합니다. 각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#detailed-walkthrough)합니다.

toocreate이 사용자 지정 환경을 hello 최신 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.

**사전 요구 사항:** Azure 리소스 그룹, 가상 네트워크 및 서브넷, 인바운드 SSH가 있는 네트워크 보안 그룹, 가상 네트워크 인터페이스 카드.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hello VM hello 가상 네트워크 인프라에 배포

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>자세한 연습

가상 네트워크 및 네트워크 보안 그룹과 같은 Azure 자산이 정적이고 거의 배포되지 않은 수명이 긴 리소스인 것이 좋습니다. 가상 네트워크에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 새 배포 재사용할 수 있습니다. 기존 하드웨어 네트워크 스위치가 있는 것으로 가상 네트워크에 대해 생각-각 배포와 새로운 하드웨어 전환 tooconfigure 필요는 없습니다. Toodeploy 올바르게 구성 된 가상 네트워크를 계속 지원 되는 몇를 사용 하 여 반복 해 해당 가상 네트워크에 새 Vm 필요한 경우 해당 변경 내용이 hello 가상 네트워크의 hello 수명 기간 동안 합니다.

toocreate이 사용자 지정 환경을 hello 최신 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

먼저 만듭니다 Azure 리소스 그룹 tooorganize이이 연습에서 만드는 모든 항목입니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요. Hello 리소스 그룹을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Hello 가상 네트워크 만들기

Vm에 Azure 가상 네트워크 toolaunch hello를 작성할 수 있습니다. 가상 네트워크에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI를 사용 하 여 가상 네트워크를 만들](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)합니다. Hello 가상 네트워크를 만듭니다 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 와 명명 된 서브넷 *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Hello 네트워크 보안 그룹 만들기

Azure 네트워크 보안 그룹은 hello 네트워크 계층에서 해당 tooa 방화벽입니다. 네트워크 보안 그룹에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI에에서 toocreate 네트워크 보안 그룹의 방법을](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)합니다. Hello 네트워크 보안 그룹을 만들 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>인바운드 SSH 허용 규칙 추가

hello VM 인터넷, 인바운드 포트 22 트래픽 toobe 허용 하는 규칙 hello VM hello 네트워크 tooport 22 통해 전달 되므로 필요한 hello에서 액세스를 해야 합니다. 네트워크 보안 그룹을 hello에 대 한 인바운드 규칙 추가 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create)합니다. hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Hello 서브넷 toohello 네트워크 보안 그룹 연결

hello 네트워크 보안 그룹 규칙 적용된 tooa 서브넷 또는 특정 가상 네트워크 인터페이스 수 있습니다. Hello 네트워크 보안 그룹 tooour 서브넷에 연결할 수 있습니다. 연결 된 서브넷 toohello 네트워크 보안 그룹 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>가상 네트워크 인터페이스 카드 toohello 서브넷 추가

가상 네트워크 인터페이스 카드 (VNics)는 중요 toodifferent Vm을 연결 하 여 다시 사용할 수 있습니다. 이 다시 사용 하면 tookeep hello VNic 정적 리소스로 hello Vm 임시 수 있습니다. VNic를 만들고 사용 하는 hello 서브넷에 연결할 [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다. hello 다음 예제에서는 명명 된 VNic *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hello VM hello 가상 네트워크 인프라에 배포

이제 SSH에 대 한 포트 22 제외한 모든 인바운드 트래픽 차단 하 여 가상 네트워크 및 서브넷 및 네트워크 보안 그룹 tooprotect hello 서브넷 있는 합니다. 이제이 기존 네트워크 인프라 내 hello VM을 배포할 수 있습니다.

[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. Hello에 대 한 자세한 내용은 전체 VM hello Azure CLI 2.0 toodeploy와 toouse를 플래그에 대 한 참조 [hello Azure CLI를 사용 하 여 완벽 한 Linux 환경을 만들](create-cli-complete.md)합니다.

다음 예제는 hello Azure 관리 되는 디스크를 사용 하는 VM을 만듭니다. 이러한 디스크 hello Azure 플랫폼에서 처리 되 고 모든 준비 단계 또는 위치 toostore 필요 하지 않은 하 합니다. 관리 디스크에 대한 자세한 내용은 [Azure Managed Disks 개요](../../storage/storage-managed-disks-overview.md)를 참조하세요. 관리 되지 않는 toouse 디스크 하려는 경우 아래 hello 추가 참고를 참조 하세요.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

관리 디스크를 사용하는 경우 이 단계를 건너뜁니다. 추가 매개 변수 toohello 계속 명령 toocreate 관리 되지 않는 디스크 라는 hello 저장소 계정에 따라 tooadd hello 필요 toouse 관리 되지 않는 디스크를 원하는 경우 `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

CLI 플래그는 hello를 사용 하 여 기존 리소스를 toocall hello 기존 네트워크 내부 Azure toodeploy hello VM을 지시 합니다. 가상 네트워크 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다. 이 예제에서는 않은 하지 만들고 할당 하려면 공용 IP 주소 toohello VNic hello 인터넷을 통해이 VM은 공개적으로 액세스할 수 있도록 합니다. 자세한 내용은 참조 [hello Azure CLI를 사용 하 여 고정 공용 ip는 VM 만들기](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md)합니다.

## <a name="next-steps"></a>다음 단계
Azure의 방법으로 toocreate 가상 컴퓨터에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.

* [Azure 리소스 관리자 템플릿 toocreate 특정 배포를 사용 하 여](../windows/cli-deploy-templates.md)
* [Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기](create-cli-complete.md)
* [템플릿을 사용하여 Azure에서 Linux VM 만들기](create-ssh-secured-vm-from-template.md)
