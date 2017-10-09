---
title: "Azure 사이트 간 연결의 강제 터널링 구성: Resource Manager | Microsoft Docs"
description: "어떻게 tooredirect 또는 'force' 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 위치 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>강제 터널링을 사용 하 여 구성 hello Azure 리소스 관리자 배포 모델

강제 터널링 리디렉션 또는 "강제" 검사 및 감사용 사이트 간 VPN 터널을 통해 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 위치로 사용 하면 됩니다. 대부분의 엔터프라이즈 IT 정책에 있어서 중요한 보안 요구 사항입니다. 강제 터널링 기능이 없으면 Azure 내 Vm의에서 인터넷 바인딩된 트래픽이 항상 통과 hello 옵션 tooallow 없이 toohello 인터넷 아웃 직접 Azure 네트워크 인프라에서 있습니다 tooinspect 또는 감사 hello 트래픽을 합니다. 인터넷에 대 한 무단된 액세스 tooinformation 노출 또는 기타 유형의 보안 위반을 일으킬 수 있습니다.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

이 문서에서는 구성 강제 hello 리소스 관리자 배포 모델을 사용 하 여 만든 가상 네트워크에 대 한 터널링 하는 과정을 안내 합니다. 강제 터널링 되지 hello 포털을 통해 PowerShell을 사용 하 여 구성할 수 있습니다. 강제 터널링 hello 클래식 배포 모델에 대 한 tooconfigure hello 다음 드롭다운 목록에서에서 클래식 문서를 선택 합니다.

> [!div class="op_single_selector"]
> * [PowerShell - 클래식](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>강제 터널링 정보

다음 다이어그램 hello 방법을 강제 터널링의 작동을 보여 줍니다. 

![강제 터널링](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

Hello 위의 hello 예제 프런트 엔드 서브넷은 강제 되지 터널링 합니다. hello 프런트 엔드 서브넷에 hello 작업 tooaccept 계속 한 hello 인터넷에서에서 직접 toocustomer 요청에 응답 합니다. hello 중간 계층 및 백 엔드 서브넷은 강제 터널링 합니다. 이러한 두 서브넷 toohello 인터넷의에서 모든 아웃 바운드 연결에는 hello S2S VPN 터널 중 하나를 통해 강제 또는 다시 리디렉션된 tooan 온-프레미스 사이트가 됩니다.

이 toorestrict 있습니다 및 가상 컴퓨터에서 인터넷 액세스를 검사 또는 tooenable 필요한 다중 계층 서비스 아키텍처를 계속 하면서 클라우드 azure에서 서비스. 가상 네트워크에 없는 인터넷 연결 작업이 있는 경우 강제 터널링 toohello 전체 가상 네트워크도 적용할 수 있습니다.

## <a name="requirements-and-considerations"></a>요구 사항 및 고려 사항

Azure에서 강제 터널링은 가상 네트워크 사용자 정의 경로를 통해 구성됩니다. 트래픽 tooan 리디렉션 온-프레미스 사이트는 기본 경로 toohello Azure VPN 게이트웨이로 표시 됩니다. 사용자 정의 경로 및 가상 네트워크에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.

* 각 가상 네트워크 서브넷에는 기본 제공 시스템 라우팅 테이블이 있습니다. hello 시스템에 대 한 라우팅 테이블에는 3 개의 그룹의 경로 따라 hello에 있습니다.
  
  * **지역 VNet 경로:** 직접 toohello의에서 대상 Vm hello 동일한 가상 네트워크입니다.
  * **온-프레미스 경로:** toohello Azure VPN 게이트웨이 합니다.
  * **기본 경로:** toohello 인터넷 직접 합니다. 패킷을 toohello 개인 IP 주소 hello 이전 두 경로에서 포함 하지 않는 삭제 됩니다.
* 이 절차는 사용자 정의 경로 (UDR) toocreate 라우팅 테이블 tooadd 기본 경로 사용 하 고 hello 라우팅 테이블 tooyour VNet 서브넷 tooenable 강제 터널링 이러한 서브넷에 연결 하 여.
* 강제 터널링은 경로 기반 VPN 게이트웨이가 있는 VNet에 연결되어야 합니다. Hello 크로스-프레미스 로컬 사이트 toohello 연결 된 가상 네트워크 간에 tooset "기본 사이트" 해야합니다. 또한 hello 온-프레미스 VPN 장치 0.0.0.0/0을 사용 하 여 트래픽 선택기로 구성 해야 합니다. 
* Express 경로 강제 터널링이 메커니즘을 통해 구성 되지 않은 하지만 대신 hello ExpressRoute BGP를 통해 기본 경로으로 활성화 되어 피어 링 세션입니다. 자세한 내용은 참조 hello [express 경로 설명서](https://azure.microsoft.com/documentation/services/expressroute/)합니다.

## <a name="configuration-overview"></a>구성 개요

hello 절차 다음에 리소스 그룹과 VNet을 만들 수 있습니다. 그런 다음 VPN Gateway를 만들고 강제 터널링을 구성합니다. 이 절차에서는 ' Multitier-vnet ' hello 가상 네트워크에 서브넷이 3 개의: '프런트 엔드', 'Midtier' 및 '백 엔드' 네 개로 크로스-프레미스 연결: 'DefaultSiteHQ' 및 3 개 분기 합니다.

hello 절차의 단계에 대 한 hello 기본 사이트 연결 강제 터널링, 및 hello 'Midtier' 및 '백 엔드' 서브넷 toouse 강제 터널링을 구성할 때 'DefaultSiteHQ' hello를 설정 합니다.

## <a name="before-you-begin"></a>시작하기 전에

Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.

### <a name="toolog-in"></a>toolog

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>강제 터널링 구성

1. 리소스 그룹을 만듭니다.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. 가상 네트워크를 만들고 서브넷을 지정합니다.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Hello 로컬 네트워크 게이트웨이 만듭니다.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Hello 경로 테이블 및 경로 규칙을 만듭니다.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Hello 경로 테이블 toohello Midtier 및 Backend 서브넷에 연결 합니다.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. 기본 사이트와 hello 게이트웨이 만듭니다. 이 단계는 만들고 hello 게이트웨이 구성 때문에 일부 시간 toocomplete, 때로는 45 분 이상, 됩니다.<br> hello **-GatewayDefaultSite** hello 강제 라우팅 구성 toowork 수 있는 cmdlet 매개 변수도 hello 되 고 있으므로 보험 tooconfigure이 올바르게 설정 됩니다. 이 매개 변수는 PowerShell 1.0 이상에서 사용할 수 있습니다.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Hello 사이트 간 VPN 연결을 설정 합니다.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```