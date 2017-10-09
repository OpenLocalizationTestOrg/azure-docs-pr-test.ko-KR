---
title: "aaaOpen 포트 tooa Azure CLI 1.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Linux VM 만들기 / hello Azure 리소스 관리자 배포를 사용 하 여 모델을 hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>여는 포트와 끝점 tooa Linux VM에서 사용 하 여 Azure hello Azure CLI 1.0
포트를 열거나 끝점을 만들 tooa (VM) Azure에서 가상 컴퓨터는 서브넷 또는 VM 네트워크 인터페이스에 네트워크 필터를 만들어 합니다. Hello 트래픽을 수신 하는 연결 된 네트워크 보안 그룹 toohello 리소스에서 인바운드 및 아웃 바운드 트래픽을 제어 하는 데 이러한 필터를 배치 합니다. 포트 80에서 웹 트래픽의 일반적인 예제를 사용해 보겠습니다. 이 문서에 사용 하 여 포트 tooa VM tooopen Azure CLI 1.0 hello 하는 방법을 보여줍니다.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](nsg-quickstart.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="quick-commands"></a>빠른 명령
toocreate 네트워크 보안 그룹 규칙 필요 하 고 [Azure CLI 1.0 hello](../../cli-install-nodejs.md) 설치 및 사용 하 여 리소스 관리자 모드:

```azurecli
azure config mode arm
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.

고유한 이름 및 위치를 적절히 입력하여 네트워크 보안 그룹을 만듭니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup* hello에 *eastus* 위치:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

규칙 tooallow HTTP 트래픽 tooyour 웹 서버를 추가 합니다 (또는 SSH 액세스 또는 데이터베이스 연결 등의 고유한 시나리오에 대 한 조정). hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRule* tooallow TCP 포트 80에서 트래픽을:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

VM의 네트워크 인터페이스 (NIC) hello 네트워크 보안 그룹을 연결 합니다. hello 다음 예제에서는 연결 라는 기존 NIC *myNic* hello 라는 네트워크 보안 그룹으로 *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

또는 바로 toohello 네트워크 인터페이스에는 단일 VM 대신 가상 네트워크 서브넷 네트워크 보안 그룹을 연결할 수 있습니다. hello 다음 예제에서는 연결 라는 기존 서브넷 *mySubnet* hello에 *myVnet* hello 라는 네트워크 보안 그룹을 사용 하 여 가상 네트워크 *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>네트워크 보안 그룹에 대한 자세한 정보
빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다. 네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다. [여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)에 대해 자세히 읽어보세요.

네트워크 보안 그룹 및 ACL 규칙을 Azure Resource Manager 템플릿의 일부로 정의할 수도 있습니다. [템플릿을 사용하여 네트워크 보안 그룹 만들기](../../virtual-network/virtual-networks-create-nsg-arm-template.md)에 대해 자세히 읽어보세요.

VM에 toouse 포트 전달을 toomap 고유한 외부 포트 tooan 내부 포트를 필요한 경우 부하 분산 장치 및 네트워크 주소 변환 (NAT) 규칙을 사용 합니다. 예를 들어 수 tooexpose TCP 포트 8080 외부에서 VM에 보내지는 트래픽을 tooTCP 포트 80입니다. [인터넷 연결 부하 분산 장치 만들기](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)에 대해 자세히 알아볼 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다. Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.

* [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)
* [NSG(네트워크 보안 그룹)란?](../../virtual-network/virtual-networks-nsg.md)
* [부하 분산 장치에 대한 Azure Resource Manager 개요](../../load-balancer/load-balancer-arm.md)

