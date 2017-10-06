---
title: "연결 확인: Azure ExpressRoute 문제 해결 가이드 | Microsoft Docs"
description: "이 페이지는 ExpressRoute 회로의 최종 tooend 연결 유효성 검사 및 문제 해결에 지침을 제공 합니다."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>ExpressRoute 연결 확인
ExpressRoute 연결 공급자를 통해 이루어집니다 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장 하는 hello 다음 3 개의 고유한 네트워크 영역에 포함 됩니다.

-   고객 네트워크
-   공급자 네트워크
-   Microsoft 데이터 센터

이 문서의 hello 목적은 toohelp 사용자 tooidentify 위치 (또는 경우에) 연결 문제가 존재 하 고, 영역 내에서 tooseek 쉽게에서 적합 한 팀 tooresolve hello 문제입니다. Microsoft 지원에 필요한 tooresolve 문제 이면와 지원 티켓을 개설할 [Microsoft 지원][Support]합니다.

> [!IMPORTANT]
> 이 문서가 의도 한 toohelp 진단 및 간단한 문제를 해결 합니다. 의도 한 toobe Microsoft 지원에 대 한 대체 하지 않습니다. 지원 티켓을 열고 [Microsoft 지원] [ Support] 제공 하는 hello 지침을 사용 하 여 없습니다 toosolve hello 문제가 있다면 합니다.
>
>

## <a name="overview"></a>개요
hello 다음 그림에 hello ExpressRoute를 사용 하는 고객 네트워크 tooMicrosoft 네트워크의 논리적 연결 합니다.
[![1]][1]

Hello 다이어그램 앞, hello 숫자 키 네트워크 지점을 나타냅니다. hello 네트워크 지점 관련 번호로이 문서를 통해 자주 참조 됩니다.

Hello ExpressRoute 연결에 따라 모델 (클라우드 Exchange 공동 배치, 지점 간 이더넷 연결 또는 Any-에-any (IPVPN)) hello 네트워크 지점 3과 4 (계층 2 장치) 스위치를 수 있습니다. hello 키 네트워크 지점 예시는 다음과 같습니다.

1.  고객 계산 장치(예: 서버 또는 PC)
2.  CE: 고객 에지 라우터 
3.  PE(CE 연결): 고객 에지 라우터에 연결되는 공급자 에지 라우터/스위치입니다. 이 문서에서 PE CEs tooas를 라고합니다.
4.  PE(MSEE 연결): MSEE에 연결되는 공급자 에지 라우터/스위치입니다. 이 문서에서 PE MSEEs tooas를 라고합니다.
5.  MSEE: MSEE(Microsoft Enterprise Edge) ExpressRoute 라우터
6.  VNet(가상 네트워크) 게이트웨이
7.  Hello Azure VNet에서 장치를 계산 합니다.

Hello 클라우드 교환 공동 배치 또는 이더넷 연결 지점 간 연결 모델을 사용 하는 경우 hello 고객에 지 라우터가 (2)는 MSEEs (5)와 피어 링 BGP를 설정 합니다. 네트워크 지점 3과 4는 여전히 존재하지만 계층 2 장치로 다소 투명하게 됩니다.

Hello Any-에-any (IPVPN) 연결 모델을 사용 하는 경우에 pes가 있습니다 (연결 된 MSEE) hello (4) MSEEs (5)와 피어 링 BGP를 설정 합니다. 다음 경로 hello IPVPN 서비스 공급자 네트워크를 통해 백 toohello 고객 네트워크를 전파 합니다.

>[!NOTE]
>ExpressRoute 고가용성을 위해 MSEE(5)와 PE-MSEE(4) 간에 중복 쌍의 BGP 세션이 필요합니다. 고객 네트워크와 PE-CE 간에도 중복 쌍의 네트워크 경로를 사용하는 것이 좋습니다. 그러나 Any-에-any (IPVPN) 연결 모델에서 단일 CE 장치 (2) 연결 된 tooone 또는 자세한에 pes가 있습니다 (3) 수 있습니다.
>
>

ExpressRoute 회로 단계를 수행 하는 hello toovalidate (지점과 hello 네트워크에 연결 하는 hello 수로 표시 된) 다룹니다.
1. [회로 프로비전 및 상태 확인 유효성 검사(5)](#validate-circuit-provisioning-and-state)
2. [하나 이상의 ExpressRoute 피어링이 구성되었는지 확인(5)](#validate-peering-configuration)
3. [Microsoft 및 hello 서비스 공급자 (4와 5 사이의 링크) 간의 ARP 유효성 검사](#validate-arp-between-microsoft-and-the-service-provider)
4. [BGP 및 hello MSEE (BGP 4 too5 사이의 5 too6 VNet 연결 되어 있는 경우)에서 경로 유효성 검사](#validate-bgp-and-routes-on-the-msee)
5. [Hello 트래픽 통계 (5 전달 되는 트래픽에)를 확인 합니다.](#check-the-traffic-statistics)

유효성 검사 및 검사를 더 추가 될 예정 hello 미래 다시 확인 매월!

##<a name="validate-circuit-provisioning-and-state"></a>회로 프로비전 및 상태 유효성 검사
Hello 연결 모델에 관계 없이 ExpressRoute 회로 만든 toobe 및 서비스 회로 프로 비전 하기 위해 생성 된 키입니다. ExpressRoute 회로를 프로비전하면 PE-MSEE(4)와 MSEE(5) 간에 계층 2 중복 연결이 설정됩니다. Toocreate를 수정, 프로 비전, 고 ExpressRoute 회로 확인 방법에 대 한 자세한 내용은 hello 문서 참조 [만들기 ExpressRoute 회로 수정 하 고][CreateCircuit]합니다.

>[!TIP]
>서비스 키는 ExpressRoute 회로를 고유하게 식별합니다. 이 키는이 문서에 언급 된 hello powershell 명령의 대부분에 필요 합니다. 또한 필요한 경우에 지원 Microsoft 또는 express 경로 파트너 tootroubleshoot ExpressRoute 문제에서 hello 서비스 제공 키 tooreadily hello 회로 식별 합니다.
>
>

###<a name="verification-via-hello-azure-portal"></a>Hello Azure 포털을 통해 확인
Azure 포털 hello, hello 상태 ExpressRoute 회로를 선택 하 여 확인할 수 있습니다 ![2][2] 사이드바 왼쪽 메뉴에서 다음 hello ExpressRoute 회로 hello에 있습니다. Express 경로 선택 하면 "모든 리소스" 아래에 나열 하는 회로 hello ExpressRoute 회로 블레이드를 엽니다. Hello에 ![3][3] hello 블레이드에서 hello essentials hello 스크린 샷 뒤에 표시 된 것으로 나열 된 ExpressRoute의 섹션:

![4][4]    

ExpressRoute Essentials hello에 *상태 회로* hello 회로 hello Microsoft 쪽에서의 hello 상태를 나타냅니다. *공급자 상태* hello 회로 되었음을 나타냅니다 *프로 비전 됨/Not 프로 비전* hello 서비스 공급자 쪽에 있습니다. 

Operational ExpressRoute 회로 toobe는, hello *상태 회로* 여야 *Enabled* 및 hello *공급자 상태* 이어야 합니다 *프로비전됨*.

>[!NOTE]
>경우 hello *상태 회로* 는 문의 사용할 수 없는 [Microsoft 지원][Support]합니다. 경우 hello *공급자 상태* 은 서비스 공급자에 게 문의 프로 비전 되지 않습니다.
>
>

###<a name="verification-via-powershell"></a>PowerShell을 통한 확인
toolist은 리소스 그룹의 ExpressRoute 회로 hello 모두, 다음 명령을 hello를 사용 하 여:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>리소스 그룹 이름은 Azure 포털 hello를 통해 얻을 수 있습니다. 이 문서의 이전 섹션에 있는 hello 참조 및 해당 hello 리소스 그룹 이름은 hello 예제에서는 화면에 표시 됩니다.
>
>

리소스 그룹에서 다음 명령을 사용 하 여 hello 특정 ExpressRoute 회로 tooselect:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

샘플 응답은 다음과 같습니다.

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm은 ExpressRoute 회로 작동 하는 경우에 특히 주의 toohello 필드 뒤 지불:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>경우 hello *CircuitProvisioningState* 는 문의 사용할 수 없는 [Microsoft 지원][Support]합니다. 경우 hello *ServiceProviderProvisioningState* 은 서비스 공급자에 게 문의 프로 비전 되지 않습니다.
>
>

###<a name="verification-via-powershell-classic"></a>PowerShell(클래식)을 통한 확인
toolist 구독에서 ExpressRoute 회로 hello 모두, 다음 명령을 hello를 사용 하 여:

    Get-AzureDedicatedCircuit

tooselect 특정 ExpressRoute 회로 다음 명령을 사용 하 여 hello:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

샘플 응답은 다음과 같습니다.

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm ExpressRoute 회로 작동 하는 경우 지불 필드를 수행 하는 특별 한 주의 toohello: ServiceProviderProvisioningState: 사용자를 프로 비전 상태: 사용 하도록 설정

>[!NOTE]
>경우 hello *상태* 는 문의 사용할 수 없는 [Microsoft 지원][Support]합니다. 경우 hello *ServiceProviderProvisioningState* 은 서비스 공급자에 게 문의 프로 비전 되지 않습니다.
>
>

##<a name="validate-peering-configuration"></a>피어링 구성 유효성 검사
Hello 서비스 공급자가 완료 된 hello hello ExpressRoute 회로 프로 비전 한 후에 라우팅 구성은 hello MSEE-Pr (4)와 (5) MSEEs 간의 ExpressRoute 회로 통해 만들 수 있습니다. 각 ExpressRoute 회로 하나, 두 개 또는 세 개의 라우팅 컨텍스트에 사용할 수 있을 수 있습니다: Azure 개인 피어 링 (트래픽 tooprivate Azure에서 가상 네트워크), Azure 공용 피어 링 (트래픽 toopublic IP 주소 Azure의) 및 Microsoft (트래픽 tooOffice 365 피어 링 및 Dynamics 365)입니다. 방법에 대 한 자세한 내용은 toocreate 라우팅 구성을 수정 하 고 hello 문서를 참조 하십시오 [만들기 및 수정 ExpressRoute 회로 대 한 라우팅][CreatePeering]합니다.

###<a name="verification-via-hello-azure-portal"></a>Hello Azure 포털을 통해 확인
>[!IMPORTANT]
>Hello에 express 경로 피어 링은 Azure 포털의 알려진된 버그가 있습니다 *하지* hello 포털 hello 서비스 공급자가 구성 된 경우에 표시 합니다. Express 경로 피어 링 hello 포털 또는 PowerShell을 통해 추가 *hello 서비스 공급자 설정을 덮어씁니다*합니다. 이 작업 hello hello ExpressRoute 회로 대해 라우팅 및 hello 서비스 공급자 toorestore hello 설정의 hello 지원이 필요로 끊어지고 일반 라우팅 다시 설정 합니다. 것이 확실 hello 서비스 공급자에는 계층 2 서비스에만 제공 하는 경우에 hello express 경로 피어 링을 수정!
>
>

<p/>
>[!NOTE]
>계층 3 제공 서비스 공급자 및 hello 피어 링 hello 하 여 hello 포털에서 비어 있는 경우 PowerShell 사용된 toosee hello 서비스 공급자 구성 설정 될 수 있습니다.
>
>

Azure 포털 hello, 상태 ExpressRoute 회로를 선택 하 여 확인할 수 있습니다 ![2][2] 사이드바 왼쪽 메뉴에서 다음 hello ExpressRoute 회로 hello에 있습니다. Express 경로 선택 하면 "모든 리소스" 아래에 나열 하는 회로 hello ExpressRoute 회로 블레이드를 점 열립니다. Hello에 ![3][3] hello 블레이드에서 hello essentials는 hello 스크린 샷 뒤에 표시 된 대로 표시 되는 ExpressRoute의 섹션:

![5][5]

앞 예제는 hello에 명시 된 Azure로 개인 피어 링 라우팅 컨텍스트를 사용할 수, 공용 Azure 및 Microsoft 피어 링 라우팅 컨텍스트를 사용할 수 있지만 합니다. 성공적으로 활성화 된 피어 링 컨텍스트 hello (BGP에 필요) 하는 기본 및 보조 지점 간 서브넷 나열 해야 합니다. hello/30 서브넷의 hello MSEEs hello 인터페이스 IP 주소 및 PE MSEEs에 사용 됩니다. 

>[!NOTE]
>피어 링을 사용 하지 않는 경우 할당 된 hello 기본 및 보조 서브넷와 일치 하는 경우 확인 PE MSEEs에 hello 구성 합니다. 하는 경우 not, toochange hello 구성 MSEE 라우터에서 너무 참조[만들기 및 수정 ExpressRoute 회로 대 한 라우팅][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>PowerShell을 통한 확인
tooget hello 개인 Azure hello 다음 명령을 사용 하 여 구성 세부 정보를 피어 링:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

성공적으로 구성된 개인 피어링에 대한 샘플 응답은 다음과 같습니다.

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 성공적으로 활성화 된 피어 링 컨텍스트 hello 기본 및 보조 주소 접두사를 나열 해야 합니다. hello/30 서브넷의 hello MSEEs hello 인터페이스 IP 주소 및 PE MSEEs에 사용 됩니다.

tooget hello Azure 공용 구성 세부 정보를 피어 링 명령 뒤 hello를 사용 합니다.

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello 한 Microsoft 피어 링 구성 세부 정보를 다음 명령 hello를 사용 합니다.

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

피어링이 구성되어 있지 않으면 오류 메시지가 표시됩니다. Hello 피어 링 (Azure 공용이 예에서 피어 링) 될 때 샘플 응답 hello 회로 내의 구성 되어 있지 않습니다.

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>피어 링을 사용 하지 않는 경우에 PE MSEE hello hello에 할당 된 기본 및 보조 서브넷 일치 hello 구성에 연결 된 경우를 확인 합니다. 있는지 확인 합니다. hello 올바른 *VlanId*, *AzureASN*, 및 *PeerASN* MSEEs에서 사용 되 고 이러한 값 매핑되 toohello hello에는 데 사용 되는 경우 PE MSEE 연결 합니다. MD5 해시를 선택한 경우 공유 키 hello MSEE 및 PE MSEE 쌍에서 동일 해야 합니다. hello MSEE 라우터에서 toochange hello 구성 참조 너무 [만들기 및 수정 ExpressRoute 회로 대 한 라우팅] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>PowerShell(클래식)을 통한 확인
tooget hello 개인 Azure hello 다음 명령을 사용 하 여 구성 세부 정보를 피어 링:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

성공적으로 구성된 개인 피어링에 대한 샘플 응답은 다음과 같습니다.

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

A가 성공적으로 활성화 피어 링 상황에 맞는 나열 된 hello 기본 및 보조 피어 서브넷이 있는 것입니다. hello/30 서브넷의 hello MSEEs hello 인터페이스 IP 주소 및 PE MSEEs에 사용 됩니다.

tooget hello Azure 공용 구성 세부 정보를 피어 링 명령 뒤 hello를 사용 합니다.

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello 한 Microsoft 피어 링 구성 세부 정보를 다음 명령 hello를 사용 합니다.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>3 계층 피어 링 hello 서비스 공급자가로 설정 된 hello 포털 또는 PowerShell을 통해 hello express 경로 피어 링 설정 hello 서비스 공급자 설정을 덮어씁니다. Hello 서비스 공급자의 hello 지원이 필요 hello 공급자 측에 대 한 피어 링 설정을 다시 설정 합니다. 것이 확실 hello 서비스 공급자에는 계층 2 서비스에만 제공 하는 경우에 hello express 경로 피어 링을 수정!
>
>

<p/>
>[!NOTE]
>피어 링을 사용 하지 않는 경우에 PE MSEE hello에 hello 기본 및 보조 피어 서브넷 할당 일치 hello 구성에 연결 된 경우를 확인 합니다. 있는지 확인 합니다. hello 올바른 *VlanId*, *AzureAsn*, 및 *PeerAsn* MSEEs에서 사용 되 고 이러한 값 매핑되 toohello hello에는 데 사용 되는 경우 PE MSEE 연결 합니다. hello MSEE 라우터에서 toochange hello 구성 참조 너무 [만들기 및 수정 ExpressRoute 회로 대 한 라우팅] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Microsoft 및 hello 서비스 공급자 간의 ARP 유효성 검사
이 섹션에서는 PowerShell(클래식) 명령을 사용합니다. Azure 리소스 관리자 PowerShell 명령을 사용 하는 경우 확인을 통해 관리자/공동 관리자 액세스 toohello 구독이 있는지 [Azure 클래식 포털][OldPortal]합니다. Azure 리소스 관리자를 사용 하 여 문제 해결에 대 한 명령을 참조 하십시오 toohello [hello 리소스 관리자 배포 모델에서 가져오기 ARP 테이블] [ ARP] 문서.

>[!NOTE]
>tooget ARP를 hello Azure 포털 및 Azure 리소스 관리자 PowerShell 명령을 둘 다 사용할 수 있습니다. Hello Azure 리소스 관리자 PowerShell 명령을 사용 하 여 오류가 발생 하는 경우 클래식 PowerShell 명령의 명령을 Azure 리소스 관리자 ExpressRoute 회로를 사용할 수도 클래식 PowerShell로 작동 해야 합니다.
>
>

tooget hello hello hello 개인 피어 링에 대 한 기본 MSEE 라우터의 ARP 테이블, 다음 명령을 hello를 사용 하 여:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

성공 시나리오 hello hello 명령에 대 한 예제 응답:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

마찬가지로, hello ARP 테이블 hello에 MSEE hello에서 확인할 수 있습니다 *기본*/*보조* 경로 대 한 *개인* /  *공용*/*Microsoft* 피어 링입니다.

hello 다음 예제에서는 피어 링에 대 한 hello 명령의 응답 hello 존재 하지 않습니다.

    ARP Info:
       
>[!NOTE]
>Hello ARP 테이블에 없는 경우 다음 정보 검토 hello tooMAC 주소 hello 인터페이스의 IP 주소에 매핑됩니다.
>1. Hello hello/30 서브넷의 첫 번째 IP 주소 간의 hello 링크에 대 한 할당 된 경우 hello MSEE PR 및 MSEE MSEE 프로의 hello 인터페이스에서 사용 됩니다. Azure는 항상 MSEEs에 대 한 hello 두 번째 IP 주소를 사용합니다.
>2. Hello 고객 (C 태그)와 서비스 (S 태그) VLAN 태그 일치 모두 MSEE PR 및 MSEE 쌍에서 확인 하십시오.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>BGP 및 hello MSEE에서 경로 유효성 검사
이 섹션에서는 PowerShell(클래식) 명령을 사용합니다. Azure 리소스 관리자 PowerShell 명령을 사용 하는 경우 확인을 통해 관리자/공동 관리자 액세스 toohello 구독이 있는지 [Azure 클래식 포털][OldPortal]

>[!NOTE]
>tooget BGP 정보를 모두 hello Azure 포털 및 Azure 리소스 관리자 PowerShell 명령을 사용할 수 있습니다. Hello Azure 리소스 관리자 PowerShell 명령을 사용 하 여 오류가 발생 하는 경우 클래식 PowerShell 명령의 명령을 Azure 리소스 관리자 ExpressRoute 회로를 사용할 수도 클래식 PowerShell로 작동 해야 합니다.
>
>

tooget hello 라우팅 테이블 (BGP 인접 한 항목)는 특정 라우팅 컨텍스트에 대 한 요약, hello 다음 명령을 사용 하 여:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

예제 응답은 다음과 같습니다.

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Hello 이전 예제와 같이 hello 명령 hello 라우팅 컨텍스트가 설정 기간에 대 한 유용한 toodetermine입니다. 또한 hello 피어 링 라우터에서 보급 된 경로 접두사의 수를 나타냅니다.

>[!NOTE]
>Hello 상태 이면 정상 또는 유휴 hello에 hello 기본 및 보조 피어 서브넷 할당 일치 hello 구성 PE MSEE 하는 경우 연결을 확인 합니다. 있는지 확인 합니다. hello 올바른 *VlanId*, *AzureAsn*, 및 *PeerAsn* MSEEs에서 사용 되 고 이러한 값 매핑되 toohello hello에는 데 사용 되는 경우 PE MSEE 연결 합니다. MD5 해시를 선택한 경우 공유 키 hello MSEE 및 PE MSEE 쌍에서 동일 해야 합니다. hello MSEE 라우터에서 toochange hello 구성 참조 너무[만들기 및 수정 ExpressRoute 회로 대 한 라우팅][CreatePeering]합니다.
>
>

<p/>
>[!NOTE]
>특정 피어 링을 통해 특정 대상을 연결할 수 없는 경우 toohello 특정 피어 링 컨텍스트에 속하는 hello MSEEs의 hello 경로 테이블을 확인 합니다. 일치 하는 접두사 (NATed IP 수 있음)가 hello 라우팅 테이블에 있는 경우에 hello 경로에 방화벽/NSG Acl이 있는 경우 고 hello 트래픽을 허용 확인 합니다.
>
>

tooget hello 전체 라우팅 테이블에서 MSEE hello *기본* 특정 hello에 대 한 경로 *개인* 라우팅 컨텍스트, 다음 명령을 사용 하 여 hello:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

다음은 hello 명령에 대 한 예제 성공적인 결과가입니다.

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

마찬가지로, hello hello에 MSEE hello에서 라우팅 테이블을 확인할 수 있습니다 *기본*/*보조* 경로 대 한 *개인* / *공용*/*Microsoft* 피어 링 컨텍스트.

hello 다음 예제에서는 피어 링에 대 한 hello 명령의 응답 hello 없습니다.

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Hello 트래픽 통계를 확인 합니다.
tooget hello에 따라 다음 명령을 사용 하 여 hello 피어 링 컨텍스트의 기본 및 보조 경로 트래픽 통계-바이트 결합 하는 및 축소.

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Hello 명령의 예제 출력은입니다.

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

존재 하지 않는 피어 링에 대 한 hello 명령의 예제 출력은입니다.

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>다음 단계
자세한 정보나 도움말에 대 한 링크를 따라 hello 확인해 보세요.

- [Microsoft 지원][Support]
- [ExpressRoute 회로 만들기 및 수정][CreateCircuit]
- [ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "논리 ExpressRoute 연결"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "모든 리소스 아이콘"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "개요 아이콘"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials 샘플 스크린샷"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials 샘플 스크린샷"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






