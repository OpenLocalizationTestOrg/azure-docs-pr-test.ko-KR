---
title: "Azure Service Fabric에 대 한 aaaNetworking 패턴 | Microsoft Docs"
description: "서비스 패브릭에 대 한 일반적인 네트워킹 패턴에 설명 하 고 어떻게 toocreate Azure 네트워킹 기능을 사용 하 여 클러스터 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Service Fabric 네트워킹 패턴
다른 Azure 네트워킹 기능으로 Azure Service Fabric 클러스터를 통합할 수 있습니다. 이 문서에서는 보여줍니다 어떻게 toocreate 클러스터를 사용 하 여 hello 같은 기능:

- [기존 가상 네트워크 또는 서브넷](#existingvnet)
- [고정 공용 IP 주소](#staticpublicip)
- [내부 전용 부하 분산 장치](#internallb)
- [내부 및 외부 부하 분산 장치](#internalexternallb)

Service Fabric은 표준 가상 컴퓨터 확장 집합에서 실행됩니다. 가상 컴퓨터 확장 집합에서 사용할 수 있는 모든 기능을 Service Fabric 클러스터에서 사용할 수 있습니다. 서비스 패브릭 및 가상 컴퓨터 크기 집합에 대 한 hello Azure 리소스 관리자 템플릿의 네트워킹 섹션 hello와 동일합니다. 다른 쉽게 tooincorporate tooan 기존 가상 네트워크를 배포한 후에 네트워킹 Azure express 경로, Azure VPN 게이트웨이, 네트워크 보안 그룹 및 가상 네트워크 피어 링 같은 기능을 합니다.

Service Fabric은 한 가지 측면에서 다른 네트워킹 기능과 다릅니다. hello [Azure 포털](https://portal.azure.com) 내부적으로 사용 하 여 hello 서비스 패브릭 리소스 공급자 toocall tooa 클러스터 tooget 정보 노드 및 응용 프로그램에 대 한 합니다. 서비스 패브릭 리소스 공급자 hello hello 관리 끝점에 대 한 인바운드 액세스 공개적으로 액세스할 수 있는 toohello HTTP 게이트웨이 포트 (포트 19080, 기본적으로) 필요합니다. [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 사용 하 여 hello 관리 끝점 toomanage 클러스터입니다. 또한 hello 서비스 패브릭 리소스 공급자 toodisplay hello Azure 포털에서에서 클러스터에 대 한이 포트 tooquery 정보를 사용합니다. 

메시지와 같은 포트 19080 hello 서비스 패브릭 리소스 공급자에서 액세스할 수 없는 경우 *노드를 찾을 수 없습니다* hello 포털에 표시 및 노드 및 응용 프로그램 목록을 빈 상태로 나타납니다. Toosee hello Azure 포털에서에서 클러스터를, 부하 분산 장치는 공용 IP 주소를 노출 해야 하 고 네트워크 보안 그룹에는 들어오는 포트 19080 트래픽을 허용 해야 합니다. 설치 프로그램에서 이러한 요구 사항에 맞지 않으면 hello Azure 포털 클러스터의 hello 상태를 표시 하지 않습니다.

## <a name="templates"></a>템플릿

모든 Service Fabric 템플릿은 [하나의 다운로드 파일](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip)에 있습니다. 있어야 수 toodeploy hello 템플릿을으로-hello 다음 PowerShell 명령을 사용 하는 것입니다. Hello를 먼저 읽어 기존 Azure 가상 네트워크 템플릿이나 hello 고정 공용 IP 서식 파일을 배포 하는 경우 hello [설치 초기](#initialsetup) 이 문서의 섹션.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>초기 설치

### <a name="existing-virtual-network"></a>기존 가상 네트워크

다음 예제는 hello에서 hello에 ExistingRG vnet을 명명 된 기존 가상 네트워크와 시작 **ExistingRG** 리소스 그룹입니다. hello 서브넷의 기본을 이름은입니다. 이러한 기본 리소스는 hello Azure 포털 toocreate 표준 가상 컴퓨터 (VM)를 사용 하는 경우에 생성 됩니다. Hello VM을 만들지 않고 hello 가상 네트워크 및 서브넷을 만들 수 있지만 클러스터 tooan 기존 가상 네트워크를 추가 하는 hello 주요 목표는 tooprovide 네트워크 연결 tooother Vm입니다. VM 만들기 hello 기존 가상 네트워크는 일반적으로 사용 방법의 좋은 예를 제공 합니다. 서비스 패브릭 클러스터를만 내부 부하 분산 장치, 없이 공용 IP 주소를 사용 하는 경우 사용할 수 있습니다 VM과 해당 공용 IP는 보안으로 hello *상자 점프*합니다.

### <a name="static-public-ip-address"></a>고정 공용 IP 주소

고정 공용 IP 주소는 일반적으로 VM 또는 Vm에 할당 된 hello에서 별도로 관리 되는 전용된 리소스입니다. (것과 반대로 tooin hello 서비스 패브릭 클러스터 리소스 그룹으로 자체) 전용된 네트워킹 리소스 그룹에 프로 비전 됩니다. Hello에 staticIP1 라는 고정 공용 IP 주소 만들기 같은 ExistingRG 리소스 그룹 hello Azure 포털에서에서 또는 PowerShell을 사용 하 여:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Service Fabric 템플릿

이 문서의 예제 hello 사용 하 여 hello 서비스 패브릭 template.json 합니다. 클러스터를 만들기 전에 hello 표준 포털 마법사 toodownload hello hello 포털에서 템플릿을 사용할 수 있습니다. 사용할 수도 있습니다 hello 템플릿 중 하나에 hello [템플릿 갤러리](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), hello 같은 [다섯 개 노드 서비스 패브릭 클러스터](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/)합니다.

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>기존 가상 네트워크 또는 서브넷

1. 다음 두 개의 새 매개 변수 tooreference hello 기존 가상 네트워크를 추가 하 고 hello 기존 서브넷의 hello 서브넷 매개 변수 toohello 이름을 변경 합니다.

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. 변경 hello `vnetID` 변수 toopoint toohello 기존 가상 네트워크:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Azure에서 새 가상 네트워크를 만들지 않도록 리소스에서 `Microsoft.Network/virtualNetworks`를 제거합니다.

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Hello에서 가상 네트워크의 hello 주석 `dependsOn` 특성 `Microsoft.Compute/virtualMachineScaleSets`새 가상 네트워크를 만드는 방법에 의존 하지 않으므로:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Hello 템플릿을 배포 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    배포 후 가상 네트워크가 포함 되어야 hello 새 크기 집합 Vm입니다. hello 기존 가상 네트워크 및 서브넷 hello 가상 컴퓨터 조정 집합 노드 유형이 표시 됩니다. 또한 프로토콜 RDP (원격 데스크톱) tooaccess hello hello 가상 네트워크에 이미 있던 VM을 사용할 수 있으며 tooping hello에 대 한 새 크기 집합 Vm:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

또 다른 예에 대 한 참조 [이름이 아닌 특정 tooService 패브릭](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet)합니다.


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>고정 공용 IP 주소

1. 고정 IP 리소스 그룹, 이름 및 정규화 된 도메인 이름 (FQDN)을 기존 hello hello 이름에 대 한 매개 변수를 추가 합니다.

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Hello 제거 `dnsName` 매개 변수입니다. (hello 고정 IP 주소에 이미 하나 있습니다.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. 변수 tooreference hello 기존의 고정 IP 주소를 추가 합니다.

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Azure에서 새 IP 주소를 만들지 않도록 리소스에서 `Microsoft.Network/publicIPAddresses`를 제거합니다.

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Hello에서 IP 주소 hello 주석 `dependsOn` 특성 `Microsoft.Network/loadBalancers`새 IP 주소를 만드는 방법에 의존 하지 않으므로:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. Hello에 `Microsoft.Network/loadBalancers` 리소스, 변경 hello `publicIPAddress` 요소의 `frontendIPConfigurations` tooreference hello 새로 만든 대신 기존의 고정 IP 주소:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. Hello에 `Microsoft.ServiceFabric/clusters` 리소스를 변경 `managementEndpoint` toohello DNS FQDN hello 고정 IP 주소입니다. 보안 클러스터를 사용 하는 경우 반드시 변경 해야 *http://* 너무*https://*합니다. (Note는이 단계는 tooService 패브릭 클러스터에만 적용 됩니다. 가상 컴퓨터 확장 집합을 사용하는 경우에는 이 단계를 건너뜁니다.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Hello 템플릿을 배포 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

배포 후 볼 수 있습니다 프로그램 부하 분산 장치가 바인딩된 toohello 공용 정적 IP 주소를 hello 있는 다른 리소스 그룹입니다. 서비스 패브릭 클라이언트 연결 끝점 hello 및 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 끝점 지점 toohello DNS FQDN hello 고정 IP 주소입니다.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>내부 전용 부하 분산 장치

이 시나리오는 내부 전용 부하 분산 장치 hello 기본 서비스 패브릭 템플릿 hello 외부 부하 분산 장치를 대체합니다. Hello 서비스 패브릭 리소스 공급자 및 hello Azure 포털에 대 한 의미를 hello 앞 섹션을 참조 하십시오.

1. Hello 제거 `dnsName` 매개 변수입니다. (필수는 아닙니다.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. 경우에 따라 고정 할당 방법을 사용할 때 고정 IP 주소 매개 변수를 추가할 수 있습니다. 동적 할당 방법을 사용 하는 경우 불필요 toodo이이 단계입니다.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Azure에서 새 IP 주소를 만들지 않도록 리소스에서 `Microsoft.Network/publicIPAddresses`를 제거합니다.

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Hello IP 주소를 제거 `dependsOn` 특성 `Microsoft.Network/loadBalancers`새 IP 주소를 만드는 방법에 의존 하지 않으므로 합니다. Hello 가상 네트워크 추가 `dependsOn` hello 부하 분산 장치는 이제 hello 가상 네트워크에서 서브넷 hello에 의존 하기 때문에 특성:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Hello 부하 분산 장치의 변경 `frontendIPConfigurations` 사용 하 여 설정 된 `publicIPAddress`, toousing 서브넷 및 `privateIPAddress`합니다. `privateIPAddress`에서는 미리 정의된 고정 내부 IP 주소를 사용합니다. 동적 IP 주소를 toouse 제거 hello `privateIPAddress` 요소를 한 다음 `privateIPAllocationMethod` 너무**동적**합니다.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. Hello에 `Microsoft.ServiceFabric/clusters` 리소스를 변경 `managementEndpoint` toopoint toohello 내부 부하 분산 장치 주소입니다. 보안 클러스터를 사용 하는 경우 반드시 변경 해야 *http://* 너무*https://*합니다. (Note는이 단계는 tooService 패브릭 클러스터에만 적용 됩니다. 가상 컴퓨터 확장 집합을 사용하는 경우에는 이 단계를 건너뜁니다.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Hello 템플릿을 배포 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

부하 분산 장치 배포 후 hello 정적 10.0.0.250 개인 IP 주소를 사용 합니다. 동일한 가상 네트워크의 다른 컴퓨터가 있는 경우에 내부 toohello을 이동할 수 있습니다 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 끝점입니다. Tooone hello 부하 분산 장치 뒤 hello 노드를 연결 되는지 확인 합니다.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>내부 및 외부 부하 분산 장치

이 시나리오에서는 시작 hello 기존 단일 노드 형식 외부 부하 분산 장치를 추가 하는 hello에 대 한 내부 부하 분산 장치는 형식이 동일 합니다. 연결 하는 백 엔드 포트 tooa 백 엔드 주소 풀만 tooa 단일 부하 분산 장치를 할당할 수 있습니다. 응용 프로그램 포트를 포함할 부하 분산 장치 및 관리 끝점을 포함할 부하 분산 장치를 선택합니다(포트 19000 및 19080). Hello 내부 부하 분산 장치에 hello 관리 끝점을 설정 하는 경우 유의 hello에 서비스 패브릭 리소스 공급자 제한은 유지 hello 문서의 앞부분에서 설명 합니다. 예에서 hello 사용 하 여 hello 관리 끝점 hello 외부 부하 분산 장치에 유지 됩니다. 또한 포트 80 응용 프로그램 포트를 추가 하 고 hello 내부 부하 분산 장치에 배치 합니다.

노드 형식 두 클러스터의 노드 유형의 hello 외부 부하 분산 장치에 만들어집니다. hello 다른 노드 형식에 있는 경우 hello 내부 부하 분산 장치 hello 포털에서 만든 두 노드 형식 서식 파일 (이 두 가지 부하 분산 장치 함께 제공)에 있는 두 노드 형식 클러스터 toouse hello 두 번째 부하 분산 장치 tooan 내부 부하 분산 장치를 전환 합니다. 자세한 내용은 참조 hello [내부 전용 부하 분산 장치](#internallb) 섹션.

1. Hello 정적 내부 부하 분산 장치 IP 주소 매개 변수를 추가 합니다. (Toousing 동적 IP 주소를 관련된 정보,이 문서의 이전 섹션 참조).

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. 응용 프로그램 포트 80 매개 변수를 추가합니다.

3. hello 기존 tooadd 내부 버전 복사 하 고, 붙여 넣고, 추가 변수 네트워킹 "-Int" toohello 이름:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. AppPort1 hello 기본 포털 템플릿을 추가 하는 응용 프로그램 포트 80을 사용 하는 hello 포털에서 생성 된 템플릿을 사용 하 여 시작 하는 경우 (포트 80) hello 외부 부하 분산 장치에 있습니다. 이 경우 AppPort1 hello 외부 부하 분산 장치에서 제거 `loadBalancingRules` 및 프로브를 있으므로 toohello 내부 부하 분산 장치를 추가할 수 있습니다.

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. 두 번째 `Microsoft.Network/loadBalancers` 리소스를 추가합니다. Hello에 생성 된 유사한 toohello 내부 부하 분산 장치 검색 [내부 전용 부하 분산 장치](#internallb) hello를 사용 하 여 하지만 섹션 "-Int" 부하 분산 장치 변수 및 구현만 hello 응용 프로그램 포트 80입니다. 이 제거 `inboundNatPools`, hello 공용 부하 분산 장치에 tookeep RDP 끝점입니다. Hello 내부 부하 분산 장치에 RDP 하려는 경우 이동 `inboundNatPools` hello 외부 부하 분산 장치 toothis 내부에서 부하 분산 장치:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. `networkProfile` hello에 대 한 `Microsoft.Compute/virtualMachineScaleSets` 리소스를 hello 내부 백 엔드 주소 풀을 추가 합니다.

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Hello 템플릿을 배포 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

배포 후 hello 리소스 그룹에 두 개의 부하 분산 장치를 볼 수 있습니다. Hello 부하 분산 장치를 찾을 때는 hello 공용 IP 주소 및 관리 끝점 (포트 19000 및 19080) 할당 toohello 공용 IP 주소를 볼 수 있습니다. Hello 정적 내부 IP 주소와 응용 프로그램 끝점 (포트 80)가 할당 된 toohello 내부 볼 수 부하 분산 장치입니다. 부하 분산 장치 사용 하 여 hello 동일한 가상 컴퓨터 크기 집합 백 엔드 풀입니다.

## <a name="next-steps"></a>다음 단계
[클러스터 만들기](service-fabric-cluster-creation-via-arm.md)
