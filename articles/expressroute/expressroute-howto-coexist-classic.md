---
title: "공존할 수 있는 ExpressRoute 및 사이트 간 VPN 연결 구성: 클래식: Azure | Microsoft Docs"
description: "이 문서에서는 express 경로 hello 클래식 배포 모델에 대 한 공존할 수 있는 사이트 간 VPN 연결을 구성 하는 과정을 안내 합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>ExpressRoute 및 사이트 간 공존 연결 구성(클래식)
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - 클래식](expressroute-howto-coexist-classic.md)
> 
> 

Hello 기능 tooconfigure 사이트 간 VPN 및 express 경로 여러 가지 장점이 있습니다. ExressRoute에 대 한 보안 장애 조치 경로와 사이트 간 VPN을 구성 하거나 ExpressRoute를 통해 연결 되어 있지 않은 사이트 간 Vpn tooconnect toosites를 사용할 수 있습니다. Hello 단계 tooconfigure 두 시나리오 모두이 문서에서 설명 합니다. 이 문서는 toohello 클래식 배포 모델을 적용합니다. 이 구성은 hello 포털에서 사용할 수 없습니다.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> ExpressRoute 회로 아래 hello 지침을 따르기 전에 미리 구성 해야 합니다. Hello 가이드 너무 수행 되었는지 확인[ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 및 [라우팅 구성](expressroute-howto-routing-classic.md) 아래 hello 단계를 수행 하기 전에.
> 
> 

## <a name="limits-and-limitations"></a>제한 및 제한 사항
* **통과 라우팅이 지원되지 않습니다.** 사이트 간 VPN을 통해 연결된 로컬 네트워크와 ExpressRoute를 통해 연결된 로컬 네트워크 사이는 Azure를 통해 라우팅할 수 없습니다.
* **지점 및 사이트 간 라우팅이 지원되지 않습니다.** 지점-사이트 VPN 연결 toohello를 설정할 수 없는 연결 된 tooExpressRoute 동일한 VNet입니다. 지점-사이트 VPN 및 express 경로 공존할 수 없으며 hello에 대 한 동일한 VNet입니다.
* **사이트 간 VPN 게이트웨이 hello에 강제 터널링을 사용할 수 없습니다.** 만 ExpressRoute 통해 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 네트워크를 "강제 적용" 수 있습니다.
* **기본 SKU 게이트웨이는 지원되지 않습니다.** 두 hello에 대 한 기본 SKU가 아닌 게이트웨이 사용 해야 [express 경로 게이트웨이](expressroute-about-virtual-network-gateways.md) 및 hello [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다.
* **경로 기반 VPN Gateway만 지원됩니다.** 경로 기반 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)를 사용해야 합니다.
* **VPN Gateway에 고정 경로를 구성해야 합니다.** 로컬 네트워크 연결된 tooboth ExpressRoute 이며는-사이트 VPN, 있어야 로컬 네트워크 tooroute hello 사이트 간 VPN 연결 toohello에 구성 된 고정 경로 경우 공용 인터넷 합니다.
* **ExpressRoute 게이트웨이를 먼저 구성해야 합니다.** Hello 사이트 간 VPN 게이트웨이 추가 하기 전에 hello express 경로 게이트웨이 먼저 만들어야 합니다.

## <a name="configuration-designs"></a>구성 디자인
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>사이트 간 VPN을 ExpressRoute에 대한 장애 조치(failover) 경로로 구성
ExpressRoute에 대한 백업으로 사이트 간 VPN 연결을 구성할 수 있습니다. 이 toovirtual 네트워크 연결 된 toohello Azure 개인 피어 링 경로 적용 됩니다. 공용 Azure 및 Microsoft 피어링을 통해 액세스할 수 있는 서비스에 대한 VPN 기반 장애 조치 솔루션은 없습니다. hello ExpressRoute 회로 항상 hello 기본 링크입니다. ExpressRoute 회로 hello 실패할 경우에 데이터 hello 사이트 간 VPN 경로 통해 전송 됩니다. 

> [!NOTE]
> ExpressRoute 회로 상태인 동안 기본 사이트 간 VPN을 통해 두 경로가 동일한 hello 되는 경우 Azure hello 패킷 대상 쪽으로 hello 가장 긴 접두사 일치 toochoose hello 경로 사용 합니다.
> 
> 

![공존](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>ExpressRoute를 통해 연결 되어 있지는 사이트 간 VPN tooconnect toosites 구성
여기서 일부 사이트 직접 tooAzure 사이트 간 VPN을 통해 연결 하 고 연결 일부 사이트 ExpressRoute를 통해 네트워크를 구성할 수 있습니다. 

![공존](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> 가상 네트워크를 통과 라우터로 구성할 수 없습니다.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Hello 단계 toouse 선택
공존할 수 있는 순서 tooconfigure 연결에서 프로시저 toochoose의 서로 다른 두 가지가 있습니다. 선택 하는 hello 구성 프로시저는 기존 가상 네트워크, tooconnect 하거나 toocreate 새 가상 네트워크를 원하는 있는지 여부에 따라 달라 집니다.

* VNet 했으며 toocreate 하나 필요 하지 않습니다.
  
    가상 네트워크를 아직 없는 경우이 절차는 과정을 단계별로 hello 클래식 배포 모델을 사용 하 고 새 ExpressRoute 및 사이트 간 VPN 연결을 만드는 새 가상 네트워크를 만드는 합니다. tooconfigure, hello 문서 섹션의 hello 단계 수행 [toocreate 새 가상 네트워크 및 공존할 연결](#new)합니다.
* 이미 클래식 배포 모델 VNet이 있는 경우
  
    기존 사이트 간 VPN 또는 ExpressRoute에 연결된 가상 네트워크가 이미 있을 수 있습니다. 문서 섹션 hello [이미 기존 VNet에 대 한 tooconfigure coexsiting 연결](#add) hello 게이트웨이 삭제 하 고 다음 ExpressRoute 및 사이트 간 VPN에 대 한 새 연결을 만드는 과정을 안내 합니다. Note hello 새 연결을 만들 때 hello 단계에 따라 매우 구체적인 순서를 완료 해야 합니다. 게이트웨이 및 연결에는 기타 기사 toocreate의 hello 지침을 사용 하지 마십시오.
  
    이 절차에서는 공존할 수 있는 연결을 만드는 및 필요 합니다. 있습니다 toodelete 게이트웨이 새 게이트웨이 구성 합니다. 이 해야 의미 크로스-프레미스 연결에 대 한 가동 중지 시간 toomigrate 필요는 없지만 하지만 삭제 하 고 게이트웨이 및 연결을 다시 만들 Vm 또는 서비스 tooa 새로운 가상 네트워크 중 하나입니다. Vm 및 서비스가 hello 부하 분산 장치를 통해 아웃 수 toocommunicate 있더라도 구성된 toodo 있으므로 게이트웨이 구성 하는 동안 합니다.

## <a name="new"></a>새 가상 네트워크를 toocreate 및 공존할 연결
이 절차는 VNet 만들기를 안내하고 함께 사용하는 사이트 간 및 Express 경로 연결을 만듭니다.

1. Tooinstall hello 최신 버전의 hello Azure PowerShell cmdlet 필요 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다. Note hello cmdlet는이 구성에 사용할 내용을 저장할 수와 약간 다 수 있습니다. 있는지 toouse hello cmdlet이이 지침에 지정 합니다. 
2. 가상 네트워크의 스키마를 만듭니다. Hello 구성 스키마에 대 한 자세한 내용은 참조 [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.
   
    스키마를 만들 때 다음 값에는 hello를 사용 해야 합니다.
   
   * hello 가상 네트워크에 대 한 hello 게이트웨이 서브넷은 / 27 또는 짧은 접두사 (예: /26 또는 /25) 이어야 합니다.
   * hello 게이트웨이 연결 유형은 "전용".
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. 를 만들고 xml 스키마 파일을 구성 후 hello 파일을 업로드 합니다. 그러면 가상 네트워크가 만들어집니다.
   
    다음 cmdlet tooupload hello 자신의 hello 값을 대체 하 여 파일을 사용 합니다.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>ExpressRoute 게이트웨이를 만듭니다. 있는지 toospecify 수로 GatewaySKU hello *표준*, *HighPerformance*, 또는 *UltraPerformance* 으로 GatewayType hello 및 *DynamicRouting*.
   
    다음 샘플, 사용자 고유의 대 한 hello 값으로 대체 hello를 사용 합니다.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Hello express 경로 게이트웨이 toohello ExpressRoute 회로 연결 합니다. 이 단계를 완료 한 후 온-프레미스 네트워크와 Azure ExpressRoute 통해 hello 연결이 설정 됩니다.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>그런 다음 사이트 간 VPN Gateway를 만듭니다. hello GatewaySKU 해야 *표준*, *HighPerformance*, 또는 *UltraPerformance* hello GatewayType 해야 *DynamicRouting*합니다.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    tooretrieve hello 가상 네트워크 게이트웨이 등의 설정을 hello 게이트웨이 ID와 hello 공용 IP를 사용 하 여 hello `Get-AzureVirtualNetworkGateway` cmdlet.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. 로컬 사이트 VPN Gateway 엔터티를 만듭니다. 이 명령은 온-프레미스 VPN Gateway를 구성하지 않습니다. 대신, tooprovide hello 로컬 게이트웨이 설정 hello 공용 IP와 같은 허용 및 hello 온-프레미스 주소 공간을 hello Azure VPN 게이트웨이에 연결할 수 있도록 tooit 합니다.
   
   > [!IMPORTANT]
   > 사이트 간 VPN hello에 대 한 로컬 사이트 hello hello netcfg에서 정의 되지 않았습니다. 대신,이 cmdlet toospecify hello 로컬 사이트 매개 변수를 사용 해야 합니다. 포털 또는 hello netcfg 파일 중 하나를 사용 하 여 정의할 수 없습니다.
   > 
   > 
   
    다음 샘플, 자신의 hello 값 대체 hello를 사용 합니다.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > 로컬 네트워크에 여러 경로가 있는 경우 모두 배열로 전달할 수 있습니다.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    tooretrieve hello 가상 네트워크 게이트웨이 등의 설정을 hello 게이트웨이 ID와 hello 공용 IP를 사용 하 여 hello `Get-AzureVirtualNetworkGateway` cmdlet. 다음 예제는 hello를 참조 하십시오.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. 로컬 VPN 장치 tooconnect toohello 새 게이트웨이 구성 합니다. VPN 장치를 구성 하는 경우 6 단계에서 검색 된 hello 정보를 사용 합니다. VPN 장치 구성에 대한 자세한 내용은 [VPN 장치 구성](../vpn-gateway/vpn-gateway-about-vpn-devices.md)을 참조하세요.
2. Azure toohello 로컬 게이트웨이에 사이트 간 VPN 게이트웨이 hello 하는 링크입니다.
   
    이 예제에서는 connectedEntityId는를 실행 하 여 찾을 수 있는 hello 로컬 게이트웨이 ID `Get-AzureLocalNetworkGateway`합니다. Hello를 사용 하 여 virtualNetworkGatewayId를 찾을 수 있습니다 `Get-AzureVirtualNetworkGateway` cmdlet. 이 단계를 hello 사이트 간 VPN 연결을 통해 로컬 네트워크와 Azure 간의 hello 연결이 설정 됩니다.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>기존 VNet에 대 한 tooconfigure coexsiting 연결
기존 가상 네트워크를 사용 하도록 설정한 경우 hello 게이트웨이 서브넷 크기를 확인 합니다. Hello 게이트웨이 서브넷이 / 28 또는/29 일 경우 먼저 hello 가상 네트워크 게이트웨이 삭제 하며 hello 게이트웨이 서브넷 크기를 늘리세요. hello이 섹션의 단계 방법을 살펴보겠습니다 toodo입니다.

Hello 게이트웨이 서브넷이 / 27 이상의 및 hello 가상 네트워크는 ExpressRoute를 통해 연결 되어, 다음 hello 단계를 건너뛰고 너무 진행할 수 있습니다["6 단계-사이트 간 VPN 게이트웨이 만들기"](#vpngw) hello 이전 섹션에서.

> [!NOTE]
> Hello 기존 게이트웨이 삭제 하면이 구성에서 작업 하는 동안 로컬 프레미스 hello 연결 tooyour 가상 네트워크는 손실 됩니다.
> 
> 

1. Tooinstall hello 최신 버전의 hello Azure 리소스 관리자 PowerShell cmdlet 필요 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다. Note hello cmdlet는이 구성에 사용할 내용을 저장할 수와 약간 다 수 있습니다. 있는지 toouse hello cmdlet이이 지침에 지정 합니다. 
2. Hello 기존 express 경로 또는 사이트 간 VPN 게이트웨이 삭제 합니다. 다음 cmdlet, 사용자의 정보로 hello 값 대체 hello를 사용 합니다.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Hello 가상 네트워크 스키마를 내보냅니다. 다음 PowerShell cmdlet, 사용자의 정보로 hello 값 대체 hello를 사용 합니다.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Hello 게이트웨이 서브넷이 / 27 또는 짧은 접두사 (예: /26 또는 /25) 있도록 hello 네트워크 구성 파일 스키마를 편집 합니다. 다음 예제는 hello를 참조 하십시오. 
   
   > [!NOTE]
   > 가상 네트워크 tooincrease hello 게이트웨이 서브넷 크기에 남아 있는 충분 한 IP 주소를 설정 하지 않은 경우 tooadd IP 주소 공간이 더 필요한 합니다. Hello 구성 스키마에 대 한 자세한 내용은 참조 [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. 이전 게이트웨이 사이트 간 VPN 경우도 변경 해야 hello 연결 유형 너무**전용**합니다.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. 이제 게이트웨이가 없는 VNet이 설정됩니다. toocreate 새 게이트웨이 연결을 완료 하 고, 계속 진행할 수 [4 단계-express 경로 게이트웨이 만들기](#gw)hello 앞 단계에서에서 발견 되었습니다.

## <a name="next-steps"></a>다음 단계
ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)

