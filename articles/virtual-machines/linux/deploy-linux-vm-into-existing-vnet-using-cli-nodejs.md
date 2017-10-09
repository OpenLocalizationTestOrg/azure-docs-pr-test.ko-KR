---
title: "Linux Vm의 경우 Azure CLI 1.0을 사용 하 여 기존 네트워크에 aaaDeploy | Microsoft Docs"
description: "어떻게 사용 하 여 기존 가상 네트워크에 Linux VM toodeploy hello Azure CLI 1.0"
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
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>어떻게 toodeploy hello Azure CLI 1.0로 기존 Azure 가상 네트워크로 Linux 가상 컴퓨터

이 문서에서는 Azure CLI 1.0 toouse toodeploy 기존 가상 네트워크 (VNet)로 가상 컴퓨터 (VM). hello 요구 사항은 같습니다.

- [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)
- [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="quick-commands"></a>빠른 명령

Hello 작업을 수행를 tooquickly가 필요한 경우 다음 단원을 hello 필요한 hello 명령에 자세히 설명 합니다. 각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough)합니다.

필수 구성 요소: SSH 인바운드를 사용하는 NSG, 리소스 그룹, VNet, 서브넷. 모든 예제를 고유한 설정으로 바꿉니다.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hello VM hello 가상 네트워크 인프라에 배포

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>자세한 연습

Azure 자산의 hello Vnet 및 같은 네트워크 보안 그룹 정적 이어야 하며 긴 동안 거의 배포 된 리소스를 활성 상태로 유지 합니다. VNet에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 새 배포 재사용할 수 있습니다. VNet를 기존 하드웨어 네트워크 스위치로 생각해 보세요. 각 배포와 새로운 하드웨어 전환 tooconfigure가 필요는 없습니다. 올바르게 구성 된 VNet에 계속할 수 있습니다 toodeploy 새 서버 해당 VNet에 반복 해 hello VNet의 hello 수명 기간 동안 필요한 경우에 자주 변경.

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

먼저 만듭니다 리소스 그룹 tooorganize이이 연습에서 만드는 모든 항목입니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Hello VNet 만들기

hello 첫 번째 단계는 VNet toolaunch hello에 대 한 Vm toobuild입니다. hello VNet이 연습에서는 한 서브넷을 포함합니다. Azure Vnet에 대 한 자세한 내용은 참조 하세요. [hello Azure CLI를 사용 하 여 가상 네트워크 만들기](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Hello 네트워크 보안 그룹 만들기

기존 네트워크 보안 그룹 뒤 hello 서브넷 빌드될 하므로 hello 서브넷 하기 전에 hello 네트워크 보안 그룹을 작성 합니다. Azure 네트워크 보안 그룹은 hello 네트워크 계층에서 해당 tooa 방화벽입니다. Azure 네트워크 보안 그룹에 대 한 자세한 내용은 참조 하십시오. [toocreate 네트워크 보안 hello Azure CLI에에서 그룹화 하는 방법](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>인바운드 SSH 허용 규칙 추가

hello VM 인터넷 트래픽을 toobe 인바운드 포트 22 허용 하는 규칙 hello VM hello 네트워크 tooport 22 통해 전달 되므로 필요한 hello에서 액세스를 해야 합니다.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>서브넷 toohello VNet 추가

Hello VNet 내에서 Vm 서브넷에 있어야 합니다. 각 VNet에는 여러 개의 서브넷이 있을 수 있습니다. Hello 서브넷을 만들고 hello 네트워크 보안 그룹과 연결 합니다.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

이제 hello 서브넷 hello VNet 내 추가 되 고 hello 네트워크 보안 그룹 및 규칙 연관 됩니다.


## <a name="add-a-vnic-toohello-subnet"></a>VNic toohello 서브넷 추가

가상 네트워크 카드 (VNics)는 중요 toodifferent Vm을 연결 하 여 다시 사용할 수 있습니다. 이 방법은 hello Vm 말할 수 하는 동안 정적 리소스로 hello VNic를 유지 합니다. VNic 만들고 hello 이전 단계에서 만든 hello 서브넷과 연결 합니다.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Hello VNet에 VM hello 및 NSG를 배포 합니다.

이제 VNet과 tooprotect hello 서브넷 SSH에 대 한 포트 22 제외한 모든 인바운드 트래픽 차단 하 여 역할을 하는 네트워크 보안 그룹 및 해당 VNet 내의 서브넷 만들어졌습니다. 이제이 기존 네트워크 인프라 내 hello VM을 배포할 수 있습니다.

Hello Azure CLI 및 hello를 사용 하 여 `azure vm create` hello Linux VM은 Azure 리소스 그룹, VNet, 서브넷 및 VNic 기존 배포 toohello 명령입니다. Hello CLI toodeploy 전체 VM 사용에 대 한 자세한 내용은 참조 하세요. [hello Azure CLI를 사용 하 여 완벽 한 Linux 환경을 만들](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

CLI 플래그는 hello를 사용 하 여 기존 리소스를 toocall hello 기존 네트워크 내부 Azure toodeploy hello VM을 지시 합니다. VNet 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.  

## <a name="next-steps"></a>다음 단계

* [Azure 리소스 관리자 템플릿 toocreate 특정 배포를 사용 하 여](../windows/cli-deploy-templates.md)
* [Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기](create-cli-complete.md)
* [템플릿을 사용하여 Azure에서 Linux VM 만들기](create-ssh-secured-vm-from-template.md)
