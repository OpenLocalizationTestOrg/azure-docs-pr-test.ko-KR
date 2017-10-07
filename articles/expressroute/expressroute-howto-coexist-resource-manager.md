---
title: "공존할 수 있는 ExpressRoute 및 사이트 간 VPN 연결 구성: Resource Manager: Azure | Microsoft Docs"
description: "이 문서에서는 Resource Manager 모델에 대해 공존할 수 있는 ExpressRoute와 사이트 간 VPN 연결을 구성하는 과정을 안내합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>ExpressRoute 및 사이트 간 공존 연결 구성
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - 클래식](expressroute-howto-coexist-classic.md)
> 
> 

사이트 간 VPN과 ExpressRoute가 공존하는 연결을 구성하면 여러 장점이 있습니다. ExressRoute에 대 한 보안 장애 조치 경로와 사이트 간 VPN을 구성할 수도 있고 ExpressRoute를 통해 연결 되어 있지 않은 사이트 간 Vpn tooconnect toosites를 사용할 수 있습니다. 두 시나리오 모두이 문서의 단계 tooconfigure hello을 다룹니다. 이 문서 toohello 리소스 관리자 배포 모델을 적용 하 고는 PowerShell을 사용 합니다. 이 구성은 hello Azure 포털에서에서 사용할 수 없습니다.

> [!IMPORTANT]
> ExpressRoute 회로 아래 hello 지침을 따르기 전에 미리 구성 해야 합니다. Hello 가이드 너무 수행 되었는지 확인[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 및 [라우팅 구성](expressroute-howto-routing-arm.md) 계속 진행 하기 전에.
> 
> 

## <a name="limits-and-limitations"></a>제한 및 제한 사항
* **통과 라우팅이 지원되지 않습니다.** 사이트 간 VPN을 통해 연결된 로컬 네트워크와 ExpressRoute를 통해 연결된 로컬 네트워크 사이는 Azure를 통해 라우팅할 수 없습니다.
* **기본 SKU 게이트웨이는 지원되지 않습니다.** 두 hello에 대 한 기본 SKU가 아닌 게이트웨이 사용 해야 [express 경로 게이트웨이](expressroute-about-virtual-network-gateways.md) 및 hello [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다.
* **경로 기반 VPN Gateway만 지원됩니다.** 경로 기반 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)를 사용해야 합니다.
* **VPN Gateway에 고정 경로를 구성해야 합니다.** 로컬 네트워크 연결된 tooboth ExpressRoute 이며는-사이트 VPN, 있어야 로컬 네트워크 tooroute hello 사이트 간 VPN 연결 toohello에 구성 된 고정 경로 경우 공용 인터넷 합니다.
* **Express 경로 게이트웨이 먼저 구성 해야 하며 tooa 회로 연결 합니다.** Hello express 경로 게이트웨이 먼저 만든 및 hello 사이트 간 VPN 게이트웨이 추가 하기 전에 tooa 회로 연결 해야 합니다.

## <a name="configuration-designs"></a>구성 디자인
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>사이트 간 VPN을 ExpressRoute에 대한 장애 조치(failover) 경로로 구성
ExpressRoute에 대한 백업으로 사이트 간 VPN 연결을 구성할 수 있습니다. 이 toovirtual 네트워크 연결 된 toohello Azure 개인 피어 링 경로 적용 됩니다. 공용 Azure 및 Microsoft 피어링을 통해 액세스할 수 있는 서비스에 대한 VPN 기반 장애 조치 솔루션은 없습니다. hello ExpressRoute 회로 항상 hello 기본 링크입니다. ExpressRoute 회로 hello 실패할 경우에 데이터 hello 사이트 간 VPN 경로 통해 이동 합니다.

> [!NOTE]
> ExpressRoute 회로 상태인 동안 기본 사이트 간 VPN을 통해 두 경로가 동일한 hello 되는 경우 Azure hello 패킷 대상 쪽으로 hello 가장 긴 접두사 일치 toochoose hello 경로 사용 합니다.
> 
> 

![공존](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>ExpressRoute를 통해 연결 되어 있지는 사이트 간 VPN tooconnect toosites 구성
여기서 일부 사이트 직접 tooAzure 사이트 간 VPN을 통해 연결 하 고 연결 일부 사이트 ExpressRoute를 통해 네트워크를 구성할 수 있습니다. 

![공존](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> 가상 네트워크를 중계 라우터로 구성할 수 없습니다.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Hello 단계 toouse 선택
프로시저 toochoose의 서로 다른 두 가지가 있습니다. 선택 하는 hello 구성 프로시저는 기존 가상 네트워크, tooconnect 하거나 toocreate 새 가상 네트워크를 원하는 있는지 여부에 따라 달라 집니다.

* VNet 했으며 toocreate 하나 필요 하지 않습니다.
  
    가상 네트워크가 아직 없는 경우 이 절차에서는 Resource Manager 배포 모델을 사용하여 새 가상 네트워크를 만들고 새 ExpressRoute 및 사이트 간 VPN 연결을 만드는 과정을 안내합니다. 가상 네트워크 tooconfigure hello 단계에 따라 [toocreate 새 가상 네트워크 및 공존할 연결](#new)합니다.
* 이미 Resource Manager 배포 모델 VNet이 있는 경우
  
    기존 사이트 간 VPN 또는 ExpressRoute에 연결된 가상 네트워크가 이미 있을 수 있습니다. hello [이미 기존 VNet에 대 한 tooconfigure 공존할 연결](#add) 섹션을 단계별로 hello 게이트웨이 삭제 한 후 새 ExpressRoute 및 사이트 간 VPN 연결을 만들어야 합니다. Hello 새 연결을 만들 때에 특정 순서로 hello 단계를 완료 해야 합니다. 게이트웨이 및 연결에는 기타 기사 toocreate의 hello 지침을 사용 하지 마십시오.
  
    이 절차에서는 공존할 수 있는 연결을 만드는 있습니다 toodelete 게이트웨이 차지 하며 다음 새 게이트웨이 구성 합니다. 생깁니다 크로스-프레미스 연결에 대 한 가동 중지 시간 toomigrate 필요는 없지만 하지만 삭제 하 고 게이트웨이 및 연결을 다시 Vm 또는 서비스 tooa 새로운 가상 네트워크 중 하나. Vm 및 서비스가 hello 부하 분산 장치를 통해 아웃 수 toocommunicate 있더라도 구성된 toodo 있으므로 게이트웨이 구성 하는 동안 합니다.

## <a name="new"></a>새 가상 네트워크를 toocreate 및 공존할 연결
이 절차에서는 공존하는 VNet 연결과 사이트 간 및 ExpressRoute 연결을 만드는 방법을 안내합니다.

1. Hello hello Azure PowerShell cmdlet의 최신 버전을 설치 합니다. Hello cmdlet을 설치 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 이 구성에 사용 하는 hello cmdlet 무엇 친숙할 수 있지만와 약간 다를 수 있습니다. 있는지 toouse hello cmdlet이이 지침에 지정 합니다.
2. Tooyour 계정을 로그인 하 고 hello 환경을 설정 합니다.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. 게이트웨이 서브넷을 포함하여 가상 네트워크를 만듭니다. Hello 가상 네트워크 구성에 대 한 자세한 내용은 참조 [Azure 가상 네트워크 구성](../virtual-network/virtual-networks-create-vnet-arm-ps.md)합니다.
   
   > [!IMPORTANT]
   > hello 게이트웨이 서브넷은 / 27 또는 짧은 접두사 (예: /26 또는 /25) 이어야 합니다.
   > 
   > 
   
    새 VNet을 만듭니다.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    서브넷을 추가합니다.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Hello VNet 구성을 저장 합니다.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>ExpressRoute 게이트웨이를 만듭니다. Hello express 경로 게이트웨이 구성에 대 한 자세한 내용은 참조 [express 경로 게이트웨이 구성](expressroute-howto-add-gateway-resource-manager.md)합니다. hello GatewaySKU 해야 *표준*, *HighPerformance*, 또는 *UltraPerformance*합니다.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Hello express 경로 게이트웨이 toohello ExpressRoute 회로 연결 합니다. 이 단계를 완료 한 후 온-프레미스 네트워크와 Azure ExpressRoute 통해 hello 연결이 설정 됩니다. Hello 링크 작업에 대 한 자세한 내용은 참조 [링크 Vnet tooExpressRoute](expressroute-howto-linkvnet-arm.md)합니다.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>그런 다음 사이트 간 VPN Gateway를 만듭니다. Hello VPN 게이트웨이 구성에 대 한 자세한 내용은 참조 [사이트 간 연결을 사용 하 여 VNet 구성](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)합니다. hello GatewaySKU 해야 *표준*, *HighPerformance*, 또는 *UltraPerformance*합니다. hello VpnType 해야 *RouteBased*합니다.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Azure VPN Gateway는 BGP 라우팅 프로토콜을 지원합니다. 다음 명령을 hello에 hello-Asn 스위치를 추가 하 여 해당 가상 네트워크에 대 한 ASN (AS 번호)을 지정할 수 있습니다. 해당 매개 변수를 지정 하지 않으면 됩니다 기본 tooAS 번호 65515입니다.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    BGP 피어 링이 IP hello 및 $azureVpn.BgpSettings.BgpPeeringAddress 및 $azureVpn.BgpSettings.Asn hello VPN 게이트웨이에 대 한 Azure를 사용 하는 숫자로 hello 찾을 수 있습니다. 자세한 내용은 Azure VPN Gateway에 대한 [BGP 구성](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.
7. 로컬 사이트 VPN Gateway 엔터티를 만듭니다. 이 명령은 온-프레미스 VPN Gateway를 구성하지 않습니다. 대신, tooprovide hello 로컬 게이트웨이 설정 hello 공용 IP와 같은 허용 및 hello 온-프레미스 주소 공간을 hello Azure VPN 게이트웨이에 연결할 수 있도록 tooit 합니다.
   
    로컬 VPN 장치만을 지 원하는 경우 고정 라우팅은 hello 방식으로 다음의 hello 고정 경로 구성할 수 있습니다.

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Tooknow hello BGP 로컬 VPN 장치 지원 hello BGP tooenable 동적 라우팅 원하는 경우 해야 IP 및 로컬 VPN 번호 처럼 hello 피어 링 장치에서 사용 합니다.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. 로컬 VPN 장치 tooconnect toohello 새 Azure VPN 게이트웨이 구성 합니다. VPN 장치 구성에 대한 자세한 내용은 [VPN 장치 구성](../vpn-gateway/vpn-gateway-about-vpn-devices.md)을 참조하세요.
9. Azure toohello 로컬 게이트웨이에 사이트 간 VPN 게이트웨이 hello 하는 링크입니다.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>기존 VNet에 대 한 tooconfigure 공존할 연결
기존 가상 네트워크를 사용 하도록 설정한 경우 hello 게이트웨이 서브넷 크기를 확인 합니다. Hello 게이트웨이 서브넷이 / 28 또는/29 일 경우 먼저 hello 가상 네트워크 게이트웨이 삭제 하며 hello 게이트웨이 서브넷 크기를 늘리세요. hello이 섹션의 단계 방법을 보여 줍니다 toodo입니다.

Hello 게이트웨이 서브넷이 / 27 이상의 및 hello 가상 네트워크는 ExpressRoute를 통해 연결 되어, 다음 hello 단계를 건너뛰고 너무 진행할 수 있습니다["6 단계-사이트 간 VPN 게이트웨이 만들기"](#vpngw) hello 이전 섹션에서. 

> [!NOTE]
> Hello 기존 게이트웨이 삭제 하면이 구성에서 작업 하는 동안 로컬 프레미스 hello 연결 tooyour 가상 네트워크는 손실 됩니다. 
> 
> 

1. Tooinstall hello 최신 버전의 hello Azure PowerShell cmdlet 필요 합니다. Cmdlet을 설치 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 이 구성에 사용 하는 hello cmdlet 무엇 친숙할 수 있지만와 약간 다를 수 있습니다. 있는지 toouse hello cmdlet이이 지침에 지정 합니다. 
2. Hello 기존 express 경로 또는 사이트 간 VPN 게이트웨이 삭제 합니다.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. 게이트웨이 서브넷을 삭제합니다.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. /27 이상인 게이트웨이 서브넷을 추가합니다.
   
   > [!NOTE]
   > 가상 네트워크 tooincrease hello 게이트웨이 서브넷 크기에 남아 있는 충분 한 IP 주소를 설정 하지 않은 경우 tooadd IP 주소 공간이 더 필요한 합니다.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Hello VNet 구성을 저장 합니다.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. 이제 게이트웨이 없는 VNet이 생겼습니다. toocreate 새 게이트웨이 연결을 완료 하 고, 계속 진행할 수 [4 단계-express 경로 게이트웨이 만들기](#gw)hello 앞 단계에서에서 발견 되었습니다.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>tooadd 지점-사이트 구성 toohello VPN 게이트웨이
동시 설치 프로그램에서 tooadd 지점-사이트 tooyour VPN 게이트웨이 구성 하는 다음 hello 단계를 따를 수 있습니다.

1. VPN 클라이언트 주소 풀을 추가합니다.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. VPN 게이트웨이에 대 한 VPN 루트 인증서 tooAzure hello를 업로드 합니다. 이 예제에서는 해당 hello 루트 인증서는 PowerShell cmdlet을 다음 hello는 실행 되는 hello 로컬 컴퓨터에 저장 가정 합니다.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

지점 및 사이트 간 VPN에 대한 자세한 내용은 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.
