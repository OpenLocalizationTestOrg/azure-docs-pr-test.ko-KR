---
title: "aaaOpen 포트 tooa Azure CLI 2.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Linux VM 만들기 / hello Azure 리소스 관리자 배포를 사용 하 여 모델을 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Hello Azure CLI가 있는 포트와 끝점 tooa Linux VM을 열려면
포트를 열거나 끝점을 만들 tooa (VM) Azure에서 가상 컴퓨터는 서브넷 또는 VM 네트워크 인터페이스에 네트워크 필터를 만들어 합니다. Hello 트래픽을 수신 하는 연결 된 네트워크 보안 그룹 toohello 리소스에서 인바운드 및 아웃 바운드 트래픽을 제어 하는 데 이러한 필터를 배치 합니다. 포트 80에서 웹 트래픽의 일반적인 예제를 사용해 보겠습니다. 이 문서에서는 Azure CLI 2.0 hello로 포트 tooa VM tooopen 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](nsg-quickstart-nodejs.md)합니다.


## <a name="quick-commands"></a>빠른 명령
toocreate 네트워크 보안 그룹 및 규칙 필요한 최신 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.

Hello 네트워크 보안 그룹을 만들 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup* hello에 *eastus* 위치:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

사용 하 여 규칙을 추가할 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 트래픽 tooyour 웹 서버 (또는 SSH 액세스 또는 데이터베이스 연결 등의 고유한 시나리오에 대 한 조정) tooallow HTTP입니다. hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRule* tooallow TCP 포트 80에서 트래픽을:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

VM의 네트워크 인터페이스 (NIC)와 hello 네트워크 보안 그룹 연결 [az 네트워크 nic 업데이트](/cli/azure/network/nic#update)합니다. hello 다음 예제에서는 연결 라는 기존 NIC *myNic* hello 라는 네트워크 보안 그룹으로 *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

또는 네트워크 보안 그룹 사용 하 여 가상 네트워크 서브넷과 연결할 수 있습니다 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update) 방금 toohello 네트워크 인터페이스에는 단일 VM 대신 합니다. hello 다음 예제에서는 연결 라는 기존 서브넷 *mySubnet* hello에 *myVnet* hello 라는 네트워크 보안 그룹을 사용 하 여 가상 네트워크 *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>네트워크 보안 그룹에 대한 자세한 정보
빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다. 네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다. [여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](tutorial-virtual-network.md#secure-network-traffic)에 대해 자세히 읽어보세요.

고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다. hello 부하 분산 장치 트래픽 tooVMs 트래픽 필터링이 제공 하는 네트워크 보안 그룹에 배포 합니다. 자세한 내용은 참조 [어떻게 tooload 균형 Linux 가상 컴퓨터에서 Azure toocreate 항상 사용 가능한 응용 프로그램](tutorial-load-balancer.md)합니다.

## <a name="next-steps"></a>다음 단계
이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다. Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.

* [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)
* [NSG(네트워크 보안 그룹)란?](../../virtual-network/virtual-networks-nsg.md)
