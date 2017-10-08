---
title: "어떻게 tooconfigure (피어 링)에 대 한 라우팅 ExpressRoute 회로: Azure: 클래식 | Microsoft Docs"
description: "이 문서를 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>ExpressRoute 회로의 피어링 만들기 및 수정(클래식)
> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [비디오 - 개인 피어링](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [비디오 - 공용 피어링](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [비디오 - Microsoft 피어링](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-routing-classic.md)
> 

이 문서는 hello 단계 toocreate 안내 하 고 PowerShell 및 hello 클래식 배포 모델을 사용 하 여 ExpressRoute 회로 대 한 라우팅 구성을 관리 합니다. 다음 hello 단계도 안내해 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, 피어 링 express 경로 회로 대 한 프로 비전 해제.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>필수 구성 요소
* Hello 최신 버전의 hello Azure 서비스 관리 (SM) PowerShell cmdlet 필요 합니다. 자세한 내용은 [Azure PowerShell cmdlet 시작](/powershell/azure/overview)을 참조하세요.  
* Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 페이지 hello [라우팅 요구 사항](expressroute-routing.md) 페이지 및 hello [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.
* 활성화된 Express 경로 회로가 있어야 합니다. 너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다. ExpressRoute 회로 hello 하면 아래에 설명 된 toobe 수 toorun hello cmdlet에 대 한 가능 하 고 프로 비전 된 상태에 있어야 합니다.

> [!IMPORTANT]
> 이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.
> 
> 

Express 경로 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft) 선택한 순서로 피어링을 구성할 수 있습니다. 그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Tooyour Azure 계정에에서 로그인을 구독 선택
1. 관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

        Login-AzureRmAccount

2. Hello 계정에 대 한 hello 구독을 확인 합니다.

        Get-AzureRmSubscription

3. 둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. 를 사용 하 여 다음 cmdlet tooadd hello Azure 구독 tooPowerShell hello 클래식 배포 모델에 대 한 합니다.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Azure 개인 피어링
이 섹션 toocreate를 가져오고, 업데이트, 고 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 삭제 방법에 지침을 제공 합니다. 

### <a name="toocreate-azure-private-peering"></a>Azure 개인 피어 링 toocreate
1. **ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.**
   
    Hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 hello Azure 및 ExpressRoute 모듈을 가져와야 합니다. 실행된 hello 다음 hello PowerShell 세션으로 tooimport hello Azure 및 ExpressRoute 모듈은 명령입니다.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Express 경로 회로를 만듭니다.**
   
    Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-classic.md) hello 연결 공급자가 사용자를 프로 비전 있습니다. 관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 아래 hello 지침을 따릅니다. 
3. **Hello ExpressRoute 회로 tooensure은 프로 비전을 확인 합니다.**
   
    Hello ExpressRoute 회로 프로 비전 하 고도 사용 하도록 설정 하는 경우에 먼저 toosee를 확인 해야 합니다. 아래 hello 예제를 참조 하십시오.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Hello 회로가 프로 비전 됨과 Enabled로 표시 되는지 확인 합니다. 그렇지 않으면 작업할 연결 공급자 tooget 회로 toohello 필요한 상황 및 상태입니다.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Azure 개인 피어 링 hello 회로 대 한 구성 합니다.**
   
    Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.
   
   * / 30 서브넷 hello 기본 링크에 대 한 합니다. 가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.
   * / 30 서브넷 hello 보조 링크에 대 한 합니다. 가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.
   * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
   * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다. 이 피어링에 개인 AS 숫자를 사용할 수 있습니다. 65515를 사용하지 않는지 확인합니다.
   * MD5 해시 toouse 하나를 선택 하는 경우입니다. **선택 사항입니다**.
     
    Azure 개인 피어 링 회로 대 한 cmdlet tooconfigure 다음 hello를 실행할 수 있습니다.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    Toouse MD5 해시를 선택 하는 경우 아래의 hello cmdlet을 사용할 수 있습니다.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > 고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>세부 정보를 피어 링 개인 Azure tooview
Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 개인 피어 링 구성
Hello 다음 cmdlet을 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다. Hello 아래 예제에서는 100 too500에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>Azure 개인 피어 링 toodelete
Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.

> [!WARNING]
> 모든 가상 네트워크 없는지 hello ExpressRoute 회로에서 연결 된이 cmdlet을 실행 하기 전에 확인 해야 합니다. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Azure 공용 피어링
이 섹션 toocreate를 get, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성 방법에 지침을 제공 합니다.

### <a name="toocreate-azure-public-peering"></a>Azure 공용 피어 링 toocreate
1. **ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.**
   
    Hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 hello Azure 및 ExpressRoute 모듈을 가져와야 합니다. 실행된 hello 다음 hello PowerShell 세션으로 tooimport hello Azure 및 ExpressRoute 모듈은 명령입니다. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **ExpressRoute 회로 만들기**
   
    Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-classic.md) hello 연결 공급자가 사용자를 프로 비전 있습니다. 관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable Azure 사용자에 대 한 피어 링 공용를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 아래 hello 지침을 따릅니다.
3. **Express 경로 회로 tooensure은 프로 비전 확인**
   
    Hello ExpressRoute 회로 프로 비전 하 고도 사용 하도록 설정 하는 경우에 먼저 toosee를 확인 해야 합니다. 아래 hello 예제를 참조 하십시오.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Hello 회로가 프로 비전 됨과 Enabled로 표시 되는지 확인 합니다. 그렇지 않으면 작업할 연결 공급자 tooget 회로 toohello 필요한 상황 및 상태입니다.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Azure 공용 피어 링 hello 회로 대 한 구성**
   
    다음 정보를 계속 진행 하기 전에 hello 가졌는지 확인 합니다.
   
   * / 30 서브넷 hello 기본 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
   * / 30 서브넷 hello 보조 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
   * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
   * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
   * MD5 해시 toouse 하나를 선택 하는 경우입니다. **선택 사항입니다**.
     
    다음 cmdlet tooconfigure Azure 공용 피어 링 회로 대 한 hello를 실행할 수 있습니다.
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    Toouse MD5 해시를 선택 하는 경우 아래의 hello cmdlet을 사용할 수 있습니다.
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > 고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>세부 정보를 피어 링 공용 Azure tooview
Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 공용 피어 링 구성
Hello 다음 cmdlet을 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

위 예제는 hello에 200 too600에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.

### <a name="toodelete-azure-public-peering"></a>Azure 공용 피어 링 toodelete
Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Microsoft 피어링
이 섹션, toocreate를 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성 방법에 지침을 제공 합니다. 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 피어 링
1. **ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.**
   
    Hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 hello Azure 및 ExpressRoute 모듈을 가져와야 합니다. 실행된 hello 다음 hello PowerShell 세션으로 tooimport hello Azure 및 ExpressRoute 모듈은 명령입니다.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **ExpressRoute 회로 만들기**
   
    Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-classic.md) hello 연결 공급자가 사용자를 프로 비전 있습니다. 관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 아래 hello 지침을 따릅니다.
3. **Express 경로 회로 tooensure은 프로 비전 확인**
   
    먼저 hello ExpressRoute 회로 사용 및 프로 비전 됨 상태 이면 toosee를 확인 해야 합니다.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Hello 회로가 프로 비전 됨과 Enabled로 표시 되는지 확인 합니다. 그렇지 않으면 작업할 연결 공급자 tooget 회로 toohello 필요한 상황 및 상태입니다.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Microsoft hello 회로 대 한 피어 링 구성**
   
    계속 하기 전에 정보 다음 hello 했는지 확인 합니다.
   
   * / 30 서브넷 hello 기본 링크에 대 한 합니다. 사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.
   * / 30 서브넷 hello 보조 링크에 대 한 합니다. 사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.
   * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
   * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
   * 접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다. 공용 IP 주소 접두사만 수락됩니다. Toosend 접두사를 계획 하는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다. 이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.
   * 고객 ASN: 등록 된 toohello 숫자로 피어 링 되지 않은 접두사를 배포 하는 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다. **선택 사항입니다**.
   * 라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.
   * MD5 해시를 toouse 하나를 선택 하는 경우. **선택 사항입니다.**
     
    회로 대 한 cmdlet tooconfigure Microsoft pering 다음 hello를 실행할 수 있습니다.
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>tooview Microsoft 피어 링 세부 정보
Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 피어 링 구성
Hello 다음 cmdlet을 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 피어 링
Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>다음 단계
그런 다음, [연결할 ExpressRoute 회로 VNet tooan](expressroute-howto-linkvnet-classic.md)합니다.

* 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.
* 회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.

