---
title: "Azure 가상 컴퓨터 크기 집합에 대 한 aaaNetworking | Microsoft Docs"
description: "Azure 가상 컴퓨터 확장 집합에 대한 네트워킹 구성 속성을 설명합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Azure 가상 컴퓨터 확장 집합에 대한 네트워킹

Hello 포털을 통해 설정 하는 Azure 가상 컴퓨터 크기를 배포할 때 특정 네트워크 속성은 기본적으로, 예를 들어 있는 Azure 부하 분산 장치 인바운드 NAT 규칙입니다. 이 문서에서는 더 높은 수준의 일부 hello 눈금으로 구성할 수 있는 네트워킹 기능 toouse 설정 하는 방법을 설명 합니다.

모든 Azure 리소스 관리자 템플릿을 사용 하 여이 문서에서 다루는 hello 기능을 구성할 수 있습니다. Azure CLI 및 PowerShell 예제도 선택한 기능에 포함되어 있습니다. CLI 2.10 및 PowerShell 4.2.0 이상을 사용합니다.

## <a name="accelerated-networking"></a>가속 네트워킹
Azure [네트워킹 Accelerated](../virtual-network/virtual-network-create-vm-accelerated-networking.md) 단일 루트 I/O 가상화 (SR-IOV) tooa 가상 컴퓨터를 사용 하 여 네트워크 성능을 개선 합니다. toouse accelerated 크기 집합와 네트워킹, 너무 enableAcceleratedNetworking 설정**true** 에 크기 집합 Networkinterfaceconfiguration 설정에서 합니다. 예:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>기존 Azure Load Balancer를 참조하는 확장 집합 만들기
크기 집합 hello Azure 포털을 사용 하 여 만들어지면 새 부하 분산 장치는 대부분의 구성 옵션에 대 한 생성 됩니다. 기존 부하 분산 장치는 tooreference 크기 집합을 만들면 이렇게 하려면 CLI를 사용 하 여 합니다. hello 다음 스크립트 예에서는 다음 부하 분산 장치를 만들고 참조 하는 확장 집합을 만듭니다.
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>구성 가능한 DNS 설정
기본적으로 크기 집합의 hello VNET 서브넷에서 생성 된 hello 특정 DNS 설정에서 수행 합니다. 그러나 수 크기 직접 집합에 대 한 hello DNS 설정을 구성 합니다.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>구성 가능한 DNS 서버가 포함된 확장 집합 만들기
눈금 설정 CLI 2.0을 사용 하 여 사용자 지정 DNS 구성을 toocreate 추가 hello **-dns 서버** 인수 toohello **vmss 만들** 서버 ip 주소를 구분 하는 명령, 공간입니다. 예:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
Azure 템플릿에서 tooconfigure 사용자 지정 DNS 서버는 dnsSettings 속성 toohello 크기 집합 Networkinterfaceconfiguration 섹션을 추가 합니다. 예:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>구성 가능한 가상 컴퓨터 도메인 이름이 포함된 확장 집합 만들기
소수 CLI 2.0을 사용 하 여 가상 컴퓨터에 대 한 사용자 지정 DNS 이름으로 설정 하는 toocreate 추가 hello **도메인 이름-vm** 인수 toohello **vmss 만들** 명령, hello 도메인 이름을 나타내는 문자열입니다.

Azure 템플릿에서 tooset hello 도메인 이름을 추가 **dnsSettings** 속성 toohello 크기 집합 **networkInterfaceConfigurations** 섹션. 예:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

hello 폼을 다음에 개별 가상 컴퓨터 dns 이름에 대 한 hello 출력이 합니다. 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>가상 컴퓨터당 공용 IPv4
일반적으로 Azure 확장 집합 가상 컴퓨터에는 자체의 공용 IP 주소가 필요하지 않습니다. 대부분의 시나리오에 대 한 경제적이 고 안전한 tooassociate 공용 IP 주소 tooa 부하 분산 장치 또는 tooan 개별 가상 컴퓨터 (즉, jumpbox) (예: 전자 필요에 따라 들어오는 tooscale 집합 가상 컴퓨터 연결을 라우팅합니다 되었기 인바운드 NAT 규칙)입니다.

그러나 일부 시나리오 필요가 크기 집합 가상 컴퓨터 toohave 자신의 공용 IP 주소입니다. 예로 게임, 콘솔 게임 물리 처리를 수행 하는 직접 연결 tooa 클라우드 가상 컴퓨터 toomake 필요한 부분입니다. 또 다른 예로 가상 컴퓨터 toomake 외부 연결 tooone 이곳 다른 지역에 배포 된 데이터베이스에 걸쳐 있습니다.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>가상 컴퓨터별 공용 IP가 포함된 확장 집합 만들기
CLI 2.0는 공용 IP 주소 tooeach 가상 컴퓨터를 할당 하는 크기 집합 toocreate 추가 hello **-vm 당 공용 ip** 매개 변수 toohello **vmss 만들** 명령입니다. 

크기는 Azure 템플릿을 사용 하 여 집합 toocreate hello Microsoft.Compute/virtualMachineScaleSets 리소스의 hello API 버전 이상 인지 확인 **2017-03-30**를 추가 하 고는 **publicIpAddressConfiguration**JSON 속성 toohello 비율이 ipConfigurations 섹션을 설정 합니다. 예:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
템플릿 예제: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>눈금의 hello 가상 컴퓨터의 주소 집합을 쿼리 하는 hello 공용 IP
toolist hello 공용 IP 주소 할당 tooscale CLI 2.0을 사용 하 여 집합 가상 컴퓨터, hello를 사용 하 여 **az vmss 목록-인스턴스-공용-ip** 명령입니다.

toolist 크기 PowerShell을 사용 하 여 공용 IP 주소 집합, hello를 사용 하 여 _Get AzureRmPublicIpAddress_ 명령입니다. 예:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Hello 공용 IP 주소 구성의 hello 리소스 id를 직접 참조 하 여 쿼리 hello 공용 IP 주소 수도 있습니다. 예:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

tooquery hello 공용 IP 주소 할당 tooscale hello를 사용 하 여 집합 가상 컴퓨터 [Azure 리소스 탐색기](https://resources.azure.com), Azure REST API 버전으로 hello 또는 **2017-03-30** 이상.

hello tooview 크기 hello 리소스 탐색기를 사용 하 여 집합에 대 한 공용 IP 주소 확인 **publicipaddresses** 크기 집합 섹션. 예: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

예제 출력:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>NIC당 여러 IP 주소
모든 NIC 연결 tooa VM 크기 집합의 연결 된 하나 이상의 IP 구성을 가질 수 있습니다. 각 구성에는 하나의 개인 IP 주소가 할당됩니다. 각 구성에는 연결된 하나의 공용 IP 주소 리소스가 있을 수도 있습니다. toounderstand IP 주소 수 tooa NIC를 할당할 수는 Azure 구독에서 사용할 수 있습니다 하는 공용 IP 주소 수가 너무 참조[Azure 제한을](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)합니다.

## <a name="multiple-nics-per-virtual-machine"></a>가상 컴퓨터당 여러 NIC
컴퓨터 크기에 따라 가상 컴퓨터당 too8 Nic를 만들 수 있습니다. 컴퓨터당 Nic의 hello 최대 수는 hello에서 사용할 수 있는 [VM 크기 문서](../virtual-machines/windows/sizes.md)합니다. hello 다음 예제는 여러 NIC 항목 및 가상 컴퓨터 마다 여러 공용 Ip를 보여 주는 네트워크 프로필을 설정 하는 소수 자릿수:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>확장 집합당 NSG
네트워크 보안 그룹 tooa 크기 집합 hello 눈금의 참조 toohello 네트워크 인터페이스 구성 섹션을 추가 하 여 가상 컴퓨터 속성을 설정 하는 직접 적용할 수 있습니다.

예: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>다음 단계
Azure 가상 네트워크에 대 한 자세한 내용은 참조 너무[이 설명서](../virtual-network/virtual-networks-overview.md)합니다.
