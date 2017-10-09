---
title: "aaaAvailability 및 Azure 리소스 관리자 템플릿을 배율이 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a>Windows VM용 Azure Resource Manager 템플릿의 가용성 및 크기 조정

가용성과 규모 toouptime / hello 기능 toomeet 요구를 참조 하십시오. 응용 프로그램 hello 시간의 99.9%를 차지 수 있어야 할 경우 여러 개의 동시 계산 리소스를 허용 하는 아키텍처 toohave가 필요 합니다. 예를 들어, 단일 웹 사이트를 설치 하는 대신 가용성의 높은 수준의 구성 hello 앞에 기술 분산 동일 사이트의 여러 인스턴스를 포함 합니다. 이 구성에서는 hello 응용 프로그램의 한 인스턴스를 중지할 수 유지 관리를 위해 남은 hello toofunction를 계속 합니다. 눈금 hello에 다른 손 tooan 응용 프로그램에서 기능 tooserve 요구를 참조 합니다. 부하 분산 된 응용 프로그램을 추가 하거나 hello 풀에서 인스턴스를 제거 하더라도 응용 프로그램 tooscale toomeet 요구가 있습니다.

이 문서 가용성과 규모에 대 한 hello Music Store 샘플 배포는 구성 하는 방법에 대해 자세히 설명 합니다. 모든 종속성 및 고유한 구성이 강조 표시됩니다. Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다. hello 완전 한 템플릿 여기 – 있습니다 [Windows에서 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

## <a name="availability-set"></a>가용성 집합
가용성 집합은 여러 물리적 호스트 및 기타 인프라 구성 요소(예: 전원 공급 장치 및 물리적 네트워킹 하드웨어)에 Azure 가상 컴퓨터를 논리적으로 분산합니다. 가용성 집합은 유지 관리, 장치 오류 또는 기타 가동 중단 시간 동안 모든 가상 컴퓨터가 영향을 받지는 않도록 합니다. 가용성 집합 tooan Azure 리소스 관리자 템플릿 hello Visual Studio 새 리소스 추가 마법사를 사용 하 여 서식 파일에 유효한 JSON을 삽입 또는 추가할 수 있습니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가용성 집합](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368)합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

가용성 집합은 가상 컴퓨터 리소스의 속성으로 선언됩니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터와 연결 가용성 집합](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302)합니다.

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
hello 가용성 hello Azure 포털에서에서와 같이 설정 합니다. 각 가상 컴퓨터 및 hello 구성에 대 한 세부 정보는 여기에서 자세히 설명 합니다.

![가용성 집합](./media/dotnet-core-4-availability-scale/ase-win.png)

가용성 집합에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요. 

## <a name="network-load-balancer"></a>네트워크 부하 분산 장치
가용성 집합에는 응용 프로그램에 대 한 내결함성을 제공, 반면 부하 분산 장치 하면 hello 응용 프로그램의 여러 인스턴스에서 사용할 수는 단일 네트워크 주소입니다. 응용 프로그램의 여러 인스턴스를 호스팅할 수 있습니다 tooa 부하 분산 장치를 연결 된 각 많은 가상 컴퓨터에서 합니다. Hello 응용 프로그램에 액세스 하는 대로 hello 부하 분산 장치 경로 hello 연결 된 멤버에서 들어오는 요청을 hello 합니다. 부하 분산 장치 또는 hello Visual Studio 새 리소스 추가 마법사를 사용 하 여 추가할 수 올바르게 삽입 하 여 JSON 리소스 hello Azure 리소스 관리자 템플릿으로 서식이 지정 합니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [네트워크 부하 분산 장치](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198)합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

Hello 샘플 응용 프로그램에 노출 된 toohello 이므로 공용 IP 주소를 사용 하 여 인터넷을이 주소는 부하 분산 장치 hello와 연결 합니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [공용 IP 주소와 네트워크 부하 분산 장치 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)합니다.

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

Hello Azure 포털에서에서 hello 네트워크 부하 분산 장치 개요 표시 hello 공용 IP 주소와 hello 연결 합니다.

![네트워크 부하 분산 장치](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a>부하 분산 장치 규칙
부하 분산 장치를 사용 하 여 의도 한 hello 리소스 간에 트래픽 균형 방법을 제어 하는 규칙이 구성 됩니다. Hello 예제 음악 스토어 응용 프로그램으로 트래픽 hello 공용 IP 주소의 포트 80에서 도착 하 고 모든 가상 컴퓨터의 포트 80에 분산 됩니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [부하 분산 장치 규칙](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226)합니다.

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

수준의 hello 네트워크 부하 분산 장치 규칙 hello 포털에서 사용 합니다.

![네트워크 부하 분산 장치 규칙](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a>부하 분산 장치 검색
부하 분산 장치 hello도 필요 toomonitor 각 가상 컴퓨터 요청은 toorunning 시스템만을 제공 합니다. 이 모니터링은 미리 정의된 포트를 지속적으로 검색하여 진행됩니다. hello Music Store 배포가 구성 된 tooprobe 포트 80에 모든 포함 된 가상 컴퓨터입니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [부하 분산 장치 검색](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247)합니다.

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

부하 분산 장치 프로브 hello hello Azure 포털에서에서 본 합니다.

![네트워크 부하 분산 장치 검색](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a>인바운드 NAT 규칙
규칙 toobe 필요한 부하 분산 장치를 사용할 때 비 부하 분산 된 액세스 tooeach 가상 컴퓨터를 제공 하는 위치에 배치 합니다. 예를 들어 각 가상 컴퓨터에 대한 RDP 연결을 만들 때 이 트래픽의 부하가 분산되지 않아야 하며, 미리 결정된 경로가 구성되어야 합니다. 미리 결정된 경로는 인바운드 NAT 규칙 리소스를 사용하여 구성됩니다. 이 리소스를 사용 하 여 인바운드 통신 매핑된 tooindividual 가상 컴퓨터를 수 있습니다. 

음악 스토어 응용 프로그램 hello로 매핑된 tooport 3389 각 가상 컴퓨터에 RDP 액세스를 위한가 5000에서 시작 포트입니다. hello `copyindex()` 함수는 사용 되는 tooincrement hello 수신 포트, 5001이 고 포트가 들어오는 받는 두 번째 가상 컴퓨터를 hello 등, 세 번째 5002 hello 및 등입니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [인바운드 NAT 규칙](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260)합니다. 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

Azure 포털에서 본 것된 hello로 인바운드 NAT 규칙을 한 가지 예입니다. RDP NAT 규칙 hello 배포의 각 가상 컴퓨터에 대해 만들어집니다.

![인바운드 NAT 규칙](./media/dotnet-core-4-availability-scale/natrule-win.png)

Hello Azure 네트워크 부하 분산 장치에 대 한 자세한 내용은 참조 하십시오. [부하 Azure 인프라 서비스에 대 한 분산](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="deploy-multiple-vms"></a>여러 VM 배포
마지막으로,에서 가용성 집합 또는 부하 분산 장치 tooeffectively 함수를 여러 가상 컴퓨터가 필요 합니다. Hello Azure 리소스 관리자 템플릿 복사 기능을 사용 하 여 여러 Vm은 배포할 수 있습니다. Hello 복사 기능을 사용 하 여, 없습니다. 필요한 toodefine 한정 된 수의 가상 컴퓨터 대신이 값 수 동적으로 제공할 수 hello 시 배포 합니다. hello 복사 기능 인스턴스 toobe 만든 hello 수 및 hello 적절 한 수의 가상 컴퓨터와 연결 된 리소스를 배포 하는 핸들을 사용 합니다.

Hello 음악 스토어 샘플 템플릿은 인스턴스 수는 수행 하는 매개 변수를 정의 합니다. 가상 컴퓨터 및 관련된 리소스를 만들 때이 수가 hello 템플릿 전체에서 사용 됩니다.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

Hello 가상 컴퓨터 리소스, hello 복사 루프는 이름이 지정 되며 있으며 toocontrol hello 매수 결과 사용 하는 hello 수가 인스턴스 매개 변수입니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 복사 기능](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290)합니다. 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

hello 복사 기능의 현재 반복 hello hello로 액세스할 수 `copyIndex()` 함수입니다. hello 복사 인덱스 함수 hello 값 tooname 사용 되는 가상 컴퓨터 및 기타 리소스를 수 있습니다. 예를 들어 가상 컴퓨터의 두 인스턴스가 배포된 경우 둘 다 이름이 달라야 합니다. hello `copyIndex()` hello 가상 컴퓨터의 부분 이름을 toocreate 고유 이름으로 함수를 사용할 수 있습니다. Hello의 예로 `copyindex()` hello 가상 컴퓨터 리소스에서에서 목적으로 이름 지정에 사용 되는 함수를 볼 수 있습니다. 여기서 hello 컴퓨터 이름은 hello의 연결을 `vmName` 매개 변수 및 hello `copyIndex()` 함수입니다. 

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [복사 인덱스 기능](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309)합니다. 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

hello `copyIndex` 함수가 hello Music Store 예제 서식 파일에서 여러 번 사용 합니다. 리소스 및 함수를 사용 하 여 `copyIndex` hello 가상 컴퓨터의 이러한 어느 것에 특정 tooa 단일 인스턴스 및 네트워크 인터페이스, 부하 분산 장치 규칙을 포함 하 고 모든 기능에 따라 달라 집니다. 

Hello 복사 기능에 대 한 자세한 내용은 참조 하십시오. [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](../../resource-group-create-multiple.md)합니다.

## <a name="next-step"></a>다음 단계
<hr>

[4단계 - Azure Resource Manager 템플릿을 사용한 응용 프로그램 배포](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

