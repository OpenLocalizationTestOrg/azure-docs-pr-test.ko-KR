---
title: "Windows Azure 리소스 관리자 템플릿으로 계산 리소스 aaaDeploying | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Windows VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 아키텍처

Azure 리소스 관리자 배포를 개발할 때 계산 매핑된 toobe tooAzure 리소스 및 서비스 요구 사항 필요 합니다. 응용 프로그램으로 구성 된 경우 여러 http 끝점, 데이터베이스 및 서비스 캐싱 데이터 hello 이러한 각 구성이 요소를 호스트 하는 Azure 리소스 필요 toobe 합리화 합니다. 예를 들어, hello 샘플 음악 스토어 응용 프로그램에 가상 컴퓨터에서 호스팅되는 웹 응용 프로그램 및 Azure SQL 데이터베이스에서 호스트 되는 SQL 데이터베이스에 포함 됩니다. 

이 문서 hello 샘플 Azure 리소스 관리자 템플릿 hello Music Store 계산 리소스 구성 방법에 대해 자세히 설명 합니다. 모든 종속성 및 고유한 구성이 강조 표시됩니다. Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다. hello 완전 한 템플릿 여기 – 있습니다 [Windows에서 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

## <a name="virtual-machine"></a>가상 컴퓨터
hello 음악 스토어 응용 프로그램에 고객 찾아볼 수도 있고 음악 구매 웹 응용 프로그램에 포함 됩니다. 웹 응용 프로그램을 호스트할 수 있는 여러 Azure 서비스가 있지만 이 예제에서는 가상 컴퓨터가 사용됩니다. Hello 샘플 음악 스토어 템플릿을 사용 하 여, 가상 컴퓨터가 배포 된, 웹 서버 설치 및 hello 음악 스토어 웹 사이트 설치 및 구성 합니다. 이 문서의 hello 위해서만 hello 가상 컴퓨터 배포에 자세히 설명 되어 있습니다. 웹 서버 hello 및 hello 응용 프로그램의 hello 구성 이후 문서에 자세히 나와 있습니다.

가상 컴퓨터에 Visual Studio 새 리소스 추가 마법사를 사용 하거나 hello 배포 템플릿을에 유효한 JSON을 삽입 하 여 hello를 사용 하 여 tooa 템플릿을 추가할 수 있습니다. 가상 컴퓨터를 배포할 때는 몇 가지 관련 리소스도 필요합니다. Visual Studio toocreate hello 템플릿을 사용 하는 경우 이러한 리소스 생성 됩니다. Hello 서식 파일을 수동으로 생성할 하는 경우 이러한 리소스 toobe 삽입 하 고 구성 해야 합니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285)합니다.

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

배포 된 후 가상 컴퓨터 속성 hello hello Azure 포털에서에서 볼 수 있습니다.

![가상 컴퓨터](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>저장소 계정
저장소 계정에는 많은 저장소 옵션과 기능이 있습니다. Azure 가상 컴퓨터의 컨텍스트에 hello에 대 한 저장소 계정을 hello 가상 컴퓨터의 가상 하드 드라이브를 hello 및 모든 추가 데이터 디스크를 보유합니다. hello Music Store 샘플 hello 배포에 하나의 저장소 계정 toohold hello 가상 하드 드라이브의 각 가상 컴퓨터를 포함합니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [저장소 계정](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98)합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

저장소 계정은 hello 가상 컴퓨터의 hello 리소스 관리자 템플릿 선언 내에 있는 가상 컴퓨터와 연결입니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 및 저장소 계정 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321)합니다.

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

배포 후 hello 저장소 계정 hello Azure 포털에서에서 볼 수 있습니다.

![저장소 계정](./media/dotnet-core-2-architecture/storacct-win.png)

Hello 저장소 계정 blob 컨테이너를 클릭 하면, hello 템플릿을 사용 하 여 배포 된 각 가상 컴퓨터에 대 한 가상 하드 드라이브 파일 hello 볼 수 있습니다.

![가상 하드 드라이브](./media/dotnet-core-2-architecture/vhd-win.png)

Azure 저장소에 대한 자세한 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)를 참조하세요.

## <a name="virtual-network"></a>가상 네트워크
가상 컴퓨터를 다른 가상 컴퓨터 및 Azure 리소스와 hello 기능 toocommunicate 같은 내부 네트워킹을 필요한 경우에 Azure 가상 네트워크 필요 합니다.  가상 네트워크를 만들지 않습니다 hello 가상 컴퓨터를 통해 액세스할 수 있는 인터넷 hello 합니다. 공용 연결에는 공용 IP 주소가 필요합니다. 이 내용은 이 시리즈의 뒷부분에서 자세히 설명합니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 네트워크 및 서브넷](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126)합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

Hello Azure 포털에서에서 가상 네트워크 hello hello 다음 이미지 처럼 보입니다. 가상 네트워크에 연결 된 toohello hello 템플릿을 사용 하 여 배포한 모든 가상 컴퓨터 인지를 확인 합니다.

![가상 네트워크](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>네트워크 인터페이스
 네트워크 인터페이스에는 가상 컴퓨터 tooa 가상 네트워크, 가상 네트워크 hello에에서 정의 된 tooa 서브넷 좀 더 구체적으로 연결 합니다. 

 Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [네트워크 인터페이스](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156)합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

각 가상 컴퓨터 리소스에는 네트워크 프로필이 포함됩니다. hello 네트워크 인터페이스는이 프로필에 hello 가상 컴퓨터와 연결 합니다.  

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 네트워크 프로필](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330)합니다.

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

Hello Azure 포털에서에서 네트워크 인터페이스 hello hello 다음 이미지 처럼 보입니다. hello 네트워크 인터페이스 리소스에 hello 내부 IP 주소 및 hello 가상 컴퓨터 연결을 볼 수 있습니다.

![네트워크 인터페이스](./media/dotnet-core-2-architecture/nic-win.png)

Azure 가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 설명서](https://azure.microsoft.com/documentation/services/virtual-network/)를 참조하세요.

## <a name="azure-sql-database"></a>Azure SQL Database
또한 hello 음악 스토어 웹 사이트, Azure SQL 데이터베이스를 호스팅하는 tooa 가상 컴퓨터는 배포 된 toohost hello Music Store 데이터베이스입니다. 여기 Azure SQL 데이터베이스를 사용 하 여 hello 장점은 가상 컴퓨터의 두 번째 집합은 필요 하지 확장성 및 가용성 변환은 hello 서비스에입니다.

Visual Studio 새 리소스 추가 마법사를 사용 하거나 유효한 JSON 서식 파일에 삽입 하 여 hello를 사용 하 여 Azure SQL 데이터베이스를 추가할 수 있습니다. SQL Server 리소스 hello 사용자 이름 및 hello SQL 인스턴스에 대해 관리 권한이 부여 되는 암호를 포함 합니다. 또한 SQL 방화벽 리소스도 추가됩니다. 기본적으로 Azure에서 호스팅되는 응용 프로그램 수 tooconnect hello SQL 인스턴스와 됩니다. tooallow 외부 응용 프로그램 같은 SQL Server Management studio tooconnect toohello SQL 인스턴스 hello 방화벽 toobe 구성 해야 합니다. Hello Music Store 데모 hello 위해서 hello 기본 구성은 문제가 없습니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379)합니다.

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Hello SQL server 및 MusicStore 데이터베이스 hello Azure 포털에에서 표시 되는 보기입니다.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Azure SQL Database 배포에 대한 자세한 내용은 [Azure SQL Database 설명서](https://azure.microsoft.com/documentation/services/sql-database/)를 참조하세요.

## <a name="next-step"></a>다음 단계
<hr>

[2단계 - Azure Resource Manager 템플릿의 액세스 및 보안](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

