---
title: "사용 하 여 가상 네트워크 aaaCreate hello Azure CLI 1.0 | Microsoft Docs"
description: "사용 하 여 가상 네트워크 toocreate Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 가상 네트워크 만들기

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다. Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다. hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한
- [Azure CLI 1.0](#create-a-virtual-network) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기

사용 하 여 가상 네트워크 toocreate hello Azure CLI, 단계를 수행 하는 전체 hello:

1. 에서 설치 및 구성 단계를 다음 hello 하 여 Azure CLI hello hello [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) 문서.

2. VNet 및 서브넷을 만듭니다.

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    예상 출력:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    사용된 매개 변수:

   * **--vnet**. 만든 hello VNet toobe의 이름입니다. 이 시나리오에서는 *TestVNet*
   * **-e(또는 --address-space)**. VNet 주소 공간입니다. 이 시나리오에서는 *192.168.0.0*
   * **-i(또는 -cidr)**. CIDR 형식의 네트워크 마스크입니다. 이 시나리오에서는 *16*입니다.
   * **-n(또는 --subnet-name**). Hello 첫 번째 서브넷의 이름입니다. 이 시나리오에서는 *FrontEnd*입니다.
   * **-p(또는 --subnet-start-ip)**. 서브넷 또는 서브넷 주소 공간의 시작 IP 주소입니다. 이 시나리오에서는 *192.168.1.0*입니다.
   * **-r(또는 --subnet-cidr)**. 서브넷에 대한 CIDR 형식의 네트워크 마스크입니다. 이 시나리오에서는 *24*입니다.
   * **-l(또는 --location)**. Azure 지역 VNet hello 생성 됩니다. 이 시나리오에서는 *Central US*입니다.

3. 서브넷을 만듭니다.

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    예상 출력:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    사용된 매개 변수:

   * **-t(또는 --vnet-name)**. Hello hello 서브넷을 만들 수는 VNet의 이름입니다. 이 시나리오에서는 *TestVNet*입니다.
   * **-n (or --name)**. Hello 새 서브넷의 이름입니다. 이 시나리오에서는 *BackEnd*입니다.
   * **-a(또는 --address-prefix)**. 서브넷 CIDR 블록입니다. 이 시나리오에서는 *192.168.2.0/24*입니다.
   
4. tooview hello 속성을 새 VNet을 hello:

    ```azurecli
    azure network vnet show
    ```
   
    예상 출력:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooconnect:

- Hello를 참조 하 여 가상 컴퓨터 (VM) tooa 가상 네트워크 [Linux VM을 만들](../virtual-machines/linux/quick-create-cli.md) 문서. Hello 아티클의 hello 단계에서 VNet 및 서브넷을 만드는 대신 및 선택할 수 있습니다는 기존 VNet 서브넷 tooconnect VM을 합니다.
- hello를 참조 하 여 가상 네트워크 tooother 가상 네트워크를 hello [Vnet 연결](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 문서.
- 가상 네트워크 tooan hello 온-프레미스 사이트 간 가상 사설망 (VPN) 또는 express 경로 회로 사용 하 여 네트워크. 자세한 방법은 hello [사이트 간 VPN을 사용 하 여 VNet tooan 온-프레미스 네트워크 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet tooan ExpressRoute 회로 연결](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)합니다.
