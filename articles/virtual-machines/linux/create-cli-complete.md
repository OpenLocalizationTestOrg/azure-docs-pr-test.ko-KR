---
title: "aaaCreate Azure CLI 2.0 hello로 Linux 환경 | Microsoft Docs"
description: "Hello Azure CLI 2.0을 사용 하 여 접지 hello 모두에서 저장소, Linux VM, 가상 네트워크 및 서브넷, 부하 분산 장치, NIC를, 공용 IP 및 네트워크 보안 그룹을 만듭니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI가 있는 완벽 한 Linux 가상 컴퓨터 만들기
모든 필수 리소스를 지 원하는 기본 값 toocreate를 사용 하는 단일 Azure CLI 명령을 사용할 수 있습니다, tooquickly Azure에서 가상 컴퓨터 (VM)를 만듭니다. 가상 네트워크, 공용 IP 주소 및 네트워크 보안 그룹 규칙 등의 리소스는 자동으로 생성됩니다. 프로덕션 환경에서 사용자 환경의 자세한 컨트롤에 대 한 사용, 이러한 리소스 보다 앞선 시간을 만들고 Vm toothem 추가 될 수 있습니다. 이 문서 어떻게 toocreate VM 및 각 hello 하나씩 지원 리소스에 설명 합니다.

Hello 최신 설치 되어 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 에 있는 계정입니다. 기록 된 tooan Azure 및 [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.

## <a name="create-resource-group"></a>리소스 그룹 만들기
Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 리소스 그룹은 가상 컴퓨터와 지원하는 가상 네트워크 리소스에 앞서 만들어져야 합니다. Hello 리소스 그룹을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

기본적으로 Azure CLI 명령을 hello 출력은 JSON (JavaScript Object Notation). 예를 들어 사용 toochange hello 기본 출력 tooa 목록 또는 테이블을 [az 구성-출력](/cli/azure/#configure)합니다. 추가할 수도 있습니다 `--output` tooany 명령을 한 번에 대 한 출력 형식으로 변경 합니다. hello 다음 예제에서는 hello JSON 출력을에서 보여 줍니다 hello `az group create` 명령:

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>가상 네트워크 및 서브넷 만들기
그런 다음 Azure에서 가상 네트워크를 만드는 경우 및 toowhich의 서브넷을 Vm을 만들 수 있습니다. 사용 하 여 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create) toocreate 이라는 가상 네트워크 *myVnet* hello로 *192.168.0.0/16* 주소 접두사입니다. 이라는 서브넷을 추가할 수도 *mySubnet* hello 주소 접두사와 *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

hello 출력 hello 서브넷을 hello 가상 네트워크 내에 만들어진 논리적으로 보여 줍니다.

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>공용 IP 주소 만들기
이제 [az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP 주소를 만듭니다. 이 공용 IP 주소가 있습니다 tooconnect tooyour를 Vm hello 인터넷에서에서 수 있습니다. Hello로 명명 된 DNS 항목 hello 기본 주소는 동적도 생성 `--domain-name-label` 옵션입니다. hello 다음 예제에서는 명명 된 공용 IP *myPublicIP* 의 hello DNS 이름을 가진 *mypublicdns*합니다. Hello DNS 이름은 고유 해야 하기 때문에 고유한 DNS 이름을 제공 합니다.

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

출력:

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>네트워크 보안 그룹 만들기
toocontrol hello 트래픽 흐름을 Vm에 내부 및 외부 네트워크 보안 그룹을 만듭니다. 네트워크 보안 그룹에 적용 된 tooa NIC 또는 서브넷 수 있습니다. hello 다음 예제에서는 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create) 네트워크 보안 그룹 이라는 toocreate *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

Hello 특정 트래픽을 허용 하거나 거부 하는 규칙을 정의 합니다. tooallow 22 (toosupport SSH) 포트에서 인바운드 연결 네트워크 보안 그룹을 hello에 대 한 인바운드 규칙을 만듭니다 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create)합니다. hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow 다른 네트워크 보안 그룹 규칙을 추가 하는 포트 80 (toosupport 웹 트래픽)에 대 한 인바운드 연결 합니다. hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

Hello 네트워크 보안 그룹 및 규칙을 검사 하 여 [az 네트워크 nsg 쇼](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

출력:

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>가상 NIC 만들기
가상 네트워크 인터페이스 카드 (Nic)은 tootheir 사용 규칙을 적용할 수 있으므로 프로그래밍 방식으로 사용할 수 있습니다. 2개 이상 있을 수도 있습니다. Hello 다음과에서 [az 네트워크 nic 만들](/cli/azure/network/nic#create) 명령, 명명 된 NIC를 만들고 *myNic* hello 네트워크 보안 그룹에 연결 합니다. 공용 IP 주소를 hello *myPublicIP* hello 가상 NIC.과 관련 되어

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

출력:

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>가용성 집합 만들기
가용성 집합은 장애 도메인 및 업데이트 도메인에 걸쳐 VM을 분산하는 데 유용합니다. 모범 사례 toouse 가용성 집합 toomake는만 하나의 VM 지금 바로 만들 경우에 해당 hello 향후에 더 쉽게 tooexpand 합니다. 

장애 도메인은 공통의 전원 및 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다. 기본적으로 가용성 집합 내에서 구성 된 가상 컴퓨터를 hello toothree 오류 도메인을 걸쳐 분리 되어 있습니다. 이러한 장애 도메인 중 하나에서 발생한 하드웨어 문제가 앱을 실행 중인 모든 VM에 영향을 미치지 않습니다.

업데이트 도메인 hello에서 다시 부팅 해야 하는 기본 실제 하드웨어와 가상 컴퓨터 그룹을 나타내는 동시 합니다. 계획 된 유지 관리 하는 동안 업데이트 도메인 재부팅 됩니다 hello 순서 순차적, 않을 수 있지만 한 번에 하나의 업데이트 도메인을 다시 부팅 합니다.

Azure 자동으로 Vm hello 장애 도메인과 업데이트 도메인에 걸쳐 때 배포 가용성 집합에 배치 합니다. 자세한 내용은 참조 [Vm의 가용성을 hello 관리](manage-availability.md)합니다.

[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 VM에 대한 가용성 집합을 만듭니다. hello 다음 예제에서는 가용성 명명 된 집합 *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

출력 메모 오류 도메인 hello 하 고 도메인을 업데이트 합니다.

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>Hello Linux Vm 만들기
Hello 네트워크 리소스 toosupport를 인터넷에서 액세스할 수 있는 Vm 만들었습니다. 이제 VM을 만들어 SSH 키로 보호합니다. 이 예에서 여기 toocreate Ubuntu VM hello에 따라 가장 최근의 LTS 합니다. [Azure VM 이미지 찾기](cli-ps-findimage.md)에서 설명한 대로 [az vm image list](/cli/azure/vm/image#list)를 통해 추가적인 이미지를 찾을 수 있습니다.

또한 인증을 위해 SSH 키 toouse를 지정합니다. SSH 공개 키 쌍이 없는 경우 다음을 할 수 있습니다 [만들](mac-create-ssh-keys.md) hello를 사용 하 여 또는 `--generate-ssh-keys` 매개 변수 toocreate ç 있습니다. 키 쌍이 있으면 이 매개 변수는 `~/.ssh`의 기존 키를 사용합니다.

모든 리소스와 정보를 hello 함께 전환 하 여 hello VM 만들기 [az vm 만들기](/cli/azure/vm#create) 명령입니다. hello 다음 예제에서는 V *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Hello 공용 IP 주소를 만들 때 제공한 DNS 항목 hello로 SSH tooyour VM입니다. 이 `fqdn` VM을 만드는 것 만큼 hello 출력에 표시 됩니다.

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

출력:

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

NGINX를 설치 하 고 hello 트래픽 흐름 toohello VM을 확인할 수 있습니다. 다음과 같이 NGINX를 설치합니다.

```bash
sudo apt-get install -y nginx
```

toosee hello 기본 NGINX 사이트 작업에서 웹 브라우저를 열고에 FQDN을 입력 합니다.

![VM의 기본 NGINX 사이트](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>템플릿으로 내보내기
이제 toocreate hello로 추가 개발 환경을 원하는 경우 동일한 매개 변수 또는 일치 하는 프로덕션 환경? 리소스 관리자는 사용자 환경에 대 한 모든 hello 매개 변수를 정의 하는 JSON 템플릿을 사용 합니다. 이 JSON 템플릿을 참조하여 전체 환경을 빌드합니다. 할 수 있습니다 [JSON 서식 파일을 수동으로 빌드할](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 기존 환경 toocreate hello JSON 템플릿을 내보냅니다. 사용 하 여 [az 그룹 내보내기](/cli/azure/group#export) tooexport 리소스 그룹 다음과 같습니다.

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

이 명령은 만듭니다 hello `myResourceGroup.json` 현재 작업 디렉터리에 파일입니다. 이 템플릿에서 환경을 만들 때 모든 hello 리소스 이름을 하 라는 메시지가 표시 됩니다. Hello를 추가 하 여 템플릿 파일에 이러한 이름을 채울 수 있습니다 `--include-parameter-default-value` 매개 변수 toohello `az group export` 명령입니다. JSON 템플릿 toospecify hello 리소스 이름의 편집 또는 [parameters.json 파일을 만들](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello 리소스 이름을 지정 하는 합니다.

서식 파일을 사용 하 여 환경 toocreate [az 그룹 배포 만들기](/cli/azure/group/deployment#create) 다음과 같습니다:

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

Tooread 경우가 [방법에 대 한 자세한 템플릿에서 toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. Tooincrementally 업데이트 환경 hello 매개 변수 파일을 사용 하 고 단일 저장소 위치에서 서식 파일에 액세스 하는 방법에 대해 알아봅니다.

## <a name="next-steps"></a>다음 단계
이제 준비 toobegin 여러 네트워킹 구성 요소 및 Vm을 사용 합니다. 여기 도입 hello 핵심 구성 요소를 사용 하 여이 샘플 환경 toobuild 응용 프로그램에 사용할 수 있습니다.
