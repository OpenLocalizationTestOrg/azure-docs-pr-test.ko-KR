---
title: "aaaAccess Windows Vm에 대 한 Azure 템플릿에서 및 보안 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Windows VM용 Azure Resource Manager 템플릿의 액세스 및 보안

응용 프로그램에서 Azure 할 가능성이 toobe 액세스를 통해 호스트 되 hello 인터넷 또는 VPN / azure Express 경로 연결 합니다. Hello 음악 스토어 응용 프로그램 샘플에서와 hello 웹 사이트에서 사용할 수는 공용 IP 주소로 인터넷 hello 합니다. 설정에 연결 된 연결 toohello 응용 프로그램 리소스를 액세스할 toohello 가상 컴퓨터 자체를 보호 해야 합니다. 이 액세스 보안은 네트워크 보안 그룹을 통해 제공됩니다. 

이 문서에 hello 샘플 Azure 리소스 관리자 템플릿 hello 음악 스토어 응용 프로그램 보호 되는 방식을 자세히 설명 합니다. 모든 종속성 및 고유한 구성이 강조 표시됩니다. Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다. hello 완전 한 템플릿 여기 – 있습니다 [Windows에서 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

## <a name="public-ip-address"></a>공용 IP 주소
tooprovide 공용 액세스 tooan Azure 리소스, 공용 IP 주소 리소스를 사용할 수 있습니다. 정적 또는 동적 IP 주소로 공용 IP 주소를 구성할 수 있습니다. 동적 주소를 사용 하 고 hello 가상 컴퓨터를 중지 하 고 할당 취소 hello 주소 제거 됩니다. Hello 컴퓨터 다시 시작 되 면 다른 공용 IP 주소를 할당할 수 있습니다. 가 변경할 tooprevent는 IP 주소, 예약된 된 IP 주소를 사용할 수 있습니다. 

공용 IP 주소는 Visual Studio 새 리소스 추가 마법사, hello를 사용 하 여 tooan Azure 리소스 관리자 템플릿을 추가할 수 있습니다 또는 서식 파일에 유효한 JSON을 삽입 하 여 합니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [공용 IP 주소](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110)합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

공용 IP 주소를 가상 네트워크 어댑터 또는 부하 분산 장치에 연결할 수 있습니다. 이 예제에서는 hello 음악 스토어 웹 사이트는 여러 가상 컴퓨터에서 부하 분산 때문에 hello 공용 IP 주소에는 연결 된 toohello 부하 분산 장치는 합니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [부하 분산 된 공용 IP 주소 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)합니다.

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

hello와 공용 IP 주소에서에서 본 hello Azure 포털입니다. 관련된 tooa 부하 분산 장치 및 가상 컴퓨터가 아닌 hello 공용 IP 주소 인지 확인 합니다. 네트워크 부하 분산 장치 hello이이 시리즈의 다음 문서에 자세히 설명 합니다.

![공용 IP 주소](./media/dotnet-core-3-access-security/pubip-win.png)

Azure 공용 IP 주소에 대한 자세한 내용은 [Azure의 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)를 참조하세요.

## <a name="network-security-group"></a>네트워크 보안 그룹
액세스에 설정 된 tooAzure 리소스를 수행한 후에이 액세스 제한 되어야 합니다. Azure 가상 컴퓨터의 경우 네트워크 보안 그룹을 사용하여 보안 액세스가 설정됩니다. Hello 음악 스토어 응용 프로그램 샘플에서와 모든 액세스 toohello 가상 컴퓨터는 http 액세스에 대 한 포트 80 및 포트 3389 RDP 액세스를 통해 제외 하 고 제한. 네트워크 보안 그룹은 Visual Studio 새 리소스 추가 마법사, hello를 사용 하 여 tooan Azure 리소스 관리자 템플릿을 추가할 수 있습니다 또는 서식 파일에 유효한 JSON을 삽입 하 여 합니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [네트워크 보안 그룹](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57)합니다.

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

이 예제에서는 hello 네트워크 보안 그룹 hello 가상 네트워크 리소스에 선언 된 hello 서브넷 개체와 연결 됩니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 네트워크와 네트워크 보안 그룹 연결이](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143)합니다.

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

다음은 어떤 hello 네트워크 보안 그룹 모양 hello에서 Azure 포털입니다. NSG는 서브넷 및/또는 네트워크 인터페이스와 연결될 수 있습니다. 이 경우 hello NSG에는 관련된 tooa 서브넷입니다. 이 구성에서는 hello 인바운드 규칙을 적용 tooall 연결 된 가상 컴퓨터 toohello 서브넷입니다.

![네트워크 보안 그룹](./media/dotnet-core-3-access-security/nsg-win.png)

네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹이란?](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)을 참조하세요.

## <a name="next-step"></a>다음 단계
<hr>

[3단계 - Azure Resource Manager 템플릿의 가용성 및 크기 조정](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

