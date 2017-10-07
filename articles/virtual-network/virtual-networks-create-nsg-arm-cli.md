---
title: "aaaCreate 네트워크 보안 그룹-Azure CLI 2.0 | Microsoft Docs"
description: "자세한 방법을 toocreate hello Azure CLI 2.0을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>네트워크를 Azure CLI 2.0 hello를 사용 하 여 보안 그룹 만들기

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업 

Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다. 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

hello 샘플 Azure CLI 2.0 다음 이미 이전 hello 시나리오를 기반으로 만들어진 단순 환경 예상 되는 명령입니다. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Hello에 대 한 hello NSG 만들기 `FrontEnd` 서브넷

명명 된 NSG toocreate *NSG 프런트 엔드* hello 단계 다음에 따라 이전 hello 시나리오에 따라, 합니다.

1. 하지 않은 아직 설치 하 고 최신 hello 구성 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다. 

2. Hello를 사용 하 여 NSG 만들기 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create) 명령입니다. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    매개 변수
   
   * `--resource-group`: Hello NSG를 만들 위치 hello 리소스 그룹의 이름입니다. 이 시나리오에서는 *TestRG*입니다.
   * `--location`: Azure 영역 hello 새 NSG를 만들 위치입니다. 이 시나리오에서는 *westus*입니다.
   * `--name`: 이름 hello에 대 한 새 NSG 합니다. 이 시나리오에서는 *NSG-FrontEnd*입니다.

    hello 출력은 모든 hello 기본 규칙의 목록을 포함 하 여 정보의 다소 필요 합니다. hello 다음 예제에서는 hello로 JMESPATH 쿼리 필터를 사용 하 여 hello 기본 규칙 `table` 출력 형식:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   출력:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Hello로 hello 인터넷에서에서 액세스 tooport 3389 (RDP)를 허용 하는 규칙을 만들 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 명령입니다.

    > [!NOTE]
    > 사용 하는 hello 셸 따라 toomodify hello를 할 수 있습니다 `*` hello 인수를 실행 하기 전에 되지 않으므로 tooexpand hello 인수 뒤에 문자입니다.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    예상 출력:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    매개 변수

    * `--resource-group testrg`: 리소스 그룹 toouse hello 합니다. 대/소문자를 구분하지 않습니다.
    * `--nsg-name NSG-FrontEnd`: Hello NSG는 hello 규칙이 만들어질의 이름입니다.
    * `--name rdp-rule`: Hello 새 규칙의 이름입니다.
    * `--access Allow`: Hello 규칙 (Deny 또는 허용)에 대 한 액세스 수준입니다.
    * `--protocol Tcp`: 프로토콜(Tcp, Udp 또는 *)입니다.
    * `--direction Inbound`: Hello 연결 (인바운드 또는 아웃 바운드)의 방향입니다.
    * `--priority 100`: Hello 규칙에 대 한 우선 순위입니다.
    * `--source-address-prefix Internet`: CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.
    * `--source-port-range "*"`: 원본 포트 또는 포트 범위입니다. 포트 연결을 hello 연입니다.
    * `--destination-address-prefix "*"`: CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.
    * `--destination-port-range 3389`: 대상 포트 또는 포트 범위입니다. Hello 연결 요청을 수신 하는 포트입니다.



4. Hello 인터넷에서에서 액세스 tooport 80 (HTTP)를 허용 하는 규칙을 만들 **az 네트워크 nsg 규칙 만들기** 명령입니다.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    예상 출력:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. Hello NSG toohello 바인딩 **프런트 엔드** hello로 서브넷 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update) 명령입니다.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    예상 출력:
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Hello에 대 한 hello NSG 만들기 `BackEnd` 서브넷
명명 된 NSG toocreate *NSG 백 엔드* hello 단계 다음에 따라 이전 hello 시나리오에 따라, 합니다.

1. Hello 만들기 `NSG-BackEnd` 와 NSG **az 네트워크 nsg 만들기**합니다.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    앞, 2 단계에서 설명한 대로 hello 출력은 매우 클 기본 규칙을 포함 하 여 필요 합니다.
   
2. 액세스 tooport 1433 (SQL) hello에서 허용 하는 규칙을 만들 `FrontEnd` hello로 서브넷 **az 네트워크 nsg 규칙 만들기** 명령입니다.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    예상 출력:

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. 사용 하 여 액세스 toohello 인터넷 거부 하는 규칙을 만들 hello **az 네트워크 nsg 규칙 만들기** 명령입니다.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    예상 출력:
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. Hello NSG toohello 바인딩 `BackEnd` hello를 사용 하 여 서브넷 **az 네트워크 vnet 서브넷 집합** 명령입니다.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    예상 출력:
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
