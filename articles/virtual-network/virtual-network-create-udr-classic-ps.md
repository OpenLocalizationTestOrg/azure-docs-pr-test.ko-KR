---
title: "Azure 가상 네트워크-PowerShell-클래식에서 aaaControl 라우팅을 | Microsoft Docs"
description: "자세한 내용은 방법 toocontrol PowerShell을 사용 하 여 Vnet에 라우팅 | 클래식"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>PowerShell 사용하여 라우팅 제어 및 가상 어플라이언스(클래식) 사용

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [템플릿](virtual-network-create-udr-arm-template.md)
> * [PowerShell(클래식)](virtual-network-create-udr-classic-ps.md)
> * [CLI(클래식)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다. Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-resource-manager/resource-manager-deployment-model.md) 를 이해해야 합니다. 이 문서의 hello 위쪽에 옵션을 선택 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다. 이 문서에서는 hello 클래식 배포 모델에 설명 합니다.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

위의 hello 시나리오를 기반으로 hello 샘플 Azure PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다. 이 문서에 표시 된 대로 toorun hello 명령을 하려는 경우 만들 hello 환경에 표시 된 [PowerShell을 사용 하 여 VNet (클래식)을 만들](virtual-networks-create-vnet-classic-netcfg-ps.md)합니다.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기
toocreate hello 경로 테이블 및 필요한 위의 hello 시나리오에 따라 hello 프런트 엔드 서브넷에 대 한 경로 아래의 hello 단계를 수행 합니다.

1. 다음 명령은 toocreate hello hello 프런트 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. 모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. 실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **프런트 엔드** 서브넷:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Hello UDR hello 백 엔드 서브넷에 대 한 만들기
서브넷 hello 시나리오에 따라 종료 toocreate hello 경로 테이블 및 경로 hello 백에 필요한 단계를 수행 하는 hello를 완료 하십시오.

1. 다음 명령은 toocreate hello hello 백 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. 모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. 실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **백 엔드** 서브넷:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Hello FW1 VM에 IP 전달을 사용 하도록 설정

hello FW1 VM을 단계를 수행 하는 전체 hello에에서 tooenable IP 전달 합니다.

1. 다음의 IP 전달 명령 toocheck hello 상태 hello를 실행 합니다.

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. 실행된 hello 다음 명령은 hello에 대 한 IP 전달 tooenable *FW1* VM:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
