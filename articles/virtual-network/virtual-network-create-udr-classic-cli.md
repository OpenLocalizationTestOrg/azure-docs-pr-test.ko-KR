---
title: "Azure 가상 네트워크-CLI-클래식에서 aaaControl 라우팅을 | Microsoft Docs"
description: "사용 하 여 Vnet에 라우팅 toocontrol Azure CLI hello 클래식 배포 모델에서 hello 하는 방법에 대해 알아봅니다"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>컨트롤에서 라우팅 및 사용 하 여 가상 어플라이언스 (클래식)를 사용 하 여 hello Azure CLI

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [템플릿](virtual-network-create-udr-arm-template.md)
> * [PowerShell(클래식)](virtual-network-create-udr-classic-ps.md)
> * [CLI(클래식)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [라우팅을 제어 하 고 가상 어플라이언스를 사용 하 여 hello 리소스 관리자 배포 모델에서](virtual-network-create-udr-arm-cli.md)합니다.

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다. 이 문서에 표시 된 대로 toorun hello 명령을 하려는 경우 만들 hello 환경에 표시 된 [hello Azure CLI를 사용 하 여 VNet (클래식)을 만들](virtual-networks-create-vnet-classic-cli.md)합니다.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기
toocreate hello 경로 테이블 및 필요한 위의 hello 시나리오에 따라 hello 프런트 엔드 서브넷에 대 한 경로 아래의 hello 단계를 수행 합니다.

1. 다음 명령 tooswitch tooclassic 모드 hello를 실행 합니다.

    ```azurecli
    azure config mode asm
    ```

    출력:

        info:    New mode is asm

2. 다음 명령은 toocreate hello hello 프런트 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    출력:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    매개 변수
   
   * **-l(또는 --location)**. Azure 지역 hello 새 NSG를 만들 위치입니다. 이 시나리오에서는 *westus*입니다.
   * **-n (or --name)**. Hello에 대 한 이름을 새 NSG 합니다. 이 시나리오에서는 *NSG-FrontEnd*입니다.
3. 모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    출력:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    매개 변수
   
   * **-r(또는 --route-table-name)**. Hello 경로 추가할 hello 경로 테이블의 이름입니다. 이 시나리오에서는 *UDR-FrontEnd*입니다.
   * **-a(또는 --address-prefix)**. Hello 서브넷에 패킷을 보내는 위치에 대 한 주소 접두사입니다. 이 시나리오에서는 *192.168.2.0/24*입니다.
   * **-t(또는 --next-hop-type)**. 전송할 개체 트래픽 유형입니다. 가능한 값은 *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* 또는 *None*입니다.
   * **-p(또는 --next-hop-ip-address**). 다음 홉에 대한 IP 주소입니다. 이 시나리오에서는 *192.168.0.4*입니다.
4. 실행된 hello 다음 명령은 hello를 사용 하 여 만든 tooassociate hello 경로 테이블 **프런트 엔드** 서브넷:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    출력:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    매개 변수
   
   * **-t(또는 --vnet-name)**. Hello hello 서브넷 위치한 VNet의 이름입니다. 이 시나리오에서는 *TestVNet*입니다.
   * **-n(또는 --subnet-name**). Hello 서브넷 hello 경로 테이블의 이름에 추가 됩니다. 이 시나리오에서는 *FrontEnd*입니다.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Hello UDR hello 백 엔드 서브넷에 대 한 만들기
toocreate hello 경로 테이블 및 hello 시나리오에서는 다음 단계 완료 hello에 따라 hello 백 엔드 서브넷에 필요한 경로:

1. 다음 명령은 toocreate hello hello 백 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. 모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. 실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **백 엔드** 서브넷:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

