---
title: "예 – aaaDMZ 빌드 DMZ tooProtect 네트워크 방화벽과 UDR, NSG를 | Microsoft Docs"
description: "방화벽, UDR(사용자 정의 라우팅), NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>예제 3 – 빌드 DMZ tooProtect 네트워크 방화벽과 UDR, NSG를
[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]

이 예제에서는 방화벽이 포함된 DMZ, 4개의 Windows Server, 사용자 정의 라우팅, IP 전달, 네트워크 보안 그룹을 만듭니다. 그는 또한 안내 각각 hello 관련 명령 tooprovide의 각 단계에 대 한 깊은 이해가. 이기도 한 트래픽 시나리오 섹션 tooprovide 심층 분석 하는 단계별 트래픽 hello 계층의 철저 한 방어 기능을 통해 진행 방법 hello DMZ 합니다. 마지막으로 hello references 섹션에는 전체 코드 hello 및 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다. 

![NVA, NSG, UDR을 사용하는 양방향 DMZ][1]

## <a name="environment-setup"></a>환경 설정
이 예제는 hello 다음을 포함 하는 구독:

* 세 클라우드 서비스: "SecSvc001", "FrontEnd001", "BackEnd001"
* "SecNet", "FrontEnd", "BackEnd"의 세 서브넷을 포함하는 가상 네트워크 "CorpNetwork"
* 이 예제는 방화벽에서 네트워크 가상 어플라이언스 toohello SecNet 서브넷 연결
* 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
* 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
* DNS 서버("DNS01")를 나타내는 Windows Server

아래 hello references 섹션에는 PowerShell 스크립트를 위에서 설명한 hello 환경의 대부분 빌드됩니다 있습니다. 건물 hello Vm 및 가상 네트워크를 hello 예제 스크립트에 의해 수행 하지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다.

toobuild hello 환경:

1. Hello 네트워크 구성 xml 파일 (이름, 위치 및 IP 주소 toomatch hello 주어진 시나리오에 업데이트) hello references 섹션에 포함 된 저장
2. Hello 스크립트 toomatch hello 환경 hello 스크립트의 update hello 사용자 변수는 toobe (구독, 서비스 이름 등)에 대해 실행
3. PowerShell에서 hello 스크립트를 실행 합니다.

**참고**: hello PowerShell 스크립트에서에서 표시 하는 hello 지역 hello 네트워크 구성 xml 파일에서 표시 하는 hello 지역 일치 해야 합니다.

Hello 스크립트가 성공적으로 실행 되 면 이후 스크립트 단계를 수행 하는 hello는 사용할 수 있습니다.

1. 이 이라는 hello 섹션에서 설명 되 hello 방화벽 규칙을 설정,: 방화벽 규칙을 설명 합니다.
2. 필요에 따라 hello references 섹션에는 두 개의 스크립트 tooset hello 웹 서버와이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 응용 프로그램 서버.

Hello 스크립트가 성공적으로 실행 되 면 hello 방화벽 규칙 toobe 완료 해야 합니다,이 내용은 hello 섹션에서 설명: 방화벽 규칙입니다.

## <a name="user-defined-routing-udr"></a>UDR(사용자 정의 라우팅)
기본적으로 시스템 경로 따라 hello로 정의 됩니다.

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

hello VNETLocal는 항상 정의 된 hello 주소 접두사가 (ie 것에서 변경 됩니다. 각 특정 VNet을 정의 하는 방법을 따라 VNet tooVNet) 해당 특정 네트워크에 대 한 hello VNet의입니다. 이 정적이 고 위와 같은 기본 hello 나머지 시스템 경로입니다.

우선 순위와 hello 가장 긴 접두사 일치 (LPM) 메서드를 통해 처리 되는 경로, 따라서 hello hello 테이블에 가장 적합 한 경로 적용할 tooa 대상 주소를 제공 합니다.

따라서 hello 로컬 네트워크 (10.0.0.0/16) 하기 위한 트래픽 (예: toohello DNS01 서버를 10.0.2.4)는 toohello 10.0.0.0/16 경로 인해 hello VNet tooits 대상 간에 라우팅됩니다. 즉, 10.0.2.4에 대 한 hello 10.0.0.0/16 경로가 hello 가장 구체적인 경로 hello 10.0.0.0/8 및 0.0.0.0/0도 적용할 수, 하지만이 트래픽을 영향을 하지 않는 덜 구체적인 되므로 경우에 합니다. 따라서 hello 트래픽 too10.0.2.4 다음 홉의 지역 VNet hello 및 단순히 toohello 대상 라우팅하는 것입니다.

위한 트래픽이 10.1.1.1 예를 들어, hello 10.0.0.0/16 경로가 적용 하지 않지만 hello 10.0.0.0/8 hello 가장 구체적인 것이 hello 트래픽을 개이고 경우 hello 다음 홉은 Null ("블랙 숨어")는 삭제 합니다. 

Hello 대상 tooany hello Null 접두사 또는 hello VNETLocal 접두사를 적용 하지 않은 경우 hello 구체적인 따라가는, 0.0.0.0/0 라우팅하고 toohello hello 다음 홉으로 인터넷 아웃와 Azure의 인터넷 가장자리 아웃 라우팅할 수 있습니다.

Hello 경로 테이블에 두 개의 동일한 접두사 인 hello 다음은 hello 경로 "source" 특성에 따라 기본 설정의 hello 순서입니다.

1. "Virtualappliance 인" = 사용자 정의 경로 수동으로 추가한 toohello 테이블
2. "VPNGateway" (BGP 하이브리드 네트워크와 함께 사용할 경우)에 대 한 동적 경로 = 동적 네트워크 프로토콜에 의해 추가, 이러한 경로로 변경 될 수 있습니다 시간이 지남에 따라 겹치기 네트워크의 변경 내용이 자동으로 반영 되 hello 동적 프로토콜
3. "Default" hello 시스템 경로 = 위의 hello 경로 테이블에 표시 된 대로 로컬 VNet과 hello 정적 항목 hello 합니다.

> [!NOTE]
> 이제 ExpressRoute와 VPN 게이트웨이 tooforce 아웃 바운드 된 사용자 정의 라우팅 (UDR)를 사용할 수 있습니다 및 크로스-프레미스 인바운드 트래픽을 toobe 라우트된 tooa 네트워크 가상 어플라이언스 (NVA).
> 
> 

#### <a name="creating-hello-local-routes"></a>Hello 로컬 경로 만들기
이 예제에서는 두 개의 라우팅 테이블 필요한 마다 하나씩 hello 프런트 엔드 및 백 엔드 서브넷에 대 한 합니다. 각 테이블은 서브넷을 지정 하는 hello에 대 한 적절 한 고정 경로로 로드 됩니다. 이 예의 hello 목적으로 각 테이블에는 세 가지 경로:

1. 정의 된 다음 홉 tooallow 로컬 서브넷 트래픽 toobypass hello 방화벽이 없는 로컬 서브넷 트래픽
2. 지역 VNet 트래픽이 tooroute를 직접 허용 하는 hello 기본 규칙 재정의 한 다음 홉 방화벽으로 정의 된 가상 네트워크 트래픽
3. 다음 홉 방화벽 hello로 정의 된 나머지 모든 트래픽 (0/0)

Hello 라우팅 테이블을 만들 바인딩된 tootheir 서브넷 않습니다. Hello 프런트 엔드 서브넷 라우팅 테이블을 만든 후에 바인딩된 toohello 서브넷이 다음과 같이 표시 됩니다.

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


예를 들어 hello 다음 명령을 사용 하는 toobuild hello 경로 테이블은 사용자 정의 경로 추가 하 고 다음 hello 경로 테이블 tooa 서브넷을 바인딩합니다 (참고; 달러 기호로 시작 아래의 모든 항목 (예:: $BESubnet)는 hello 스크립트에서 사용자 정의 변수 hello 참조가 문서의 섹션):

1. 첫 번째 hello 기본 라우팅 테이블을 만들어야 합니다. 이 코드 조각 hello 백 엔드 서브넷에 대 한 hello 테이블 hello 만드는 방법을 보여 줍니다. Hello 스크립트에는 해당 테이블이 만들어집니다 hello 프런트 엔드 서브넷에 대 한 합니다.
   
     New-AzureRouteTable -Name $BERouteTableName `
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Hello 경로 테이블을 만든 후에 특정 사용자 정의 경로 추가할 수 있습니다. 이 조각에서 모든 트래픽 (0.0.0.0/0) hello ($VMIP [0], 변수는 hello 가상 어플라이언스 hello 스크립트의 앞부분에 나오는 만들 떄 할당 hello IP 주소에 사용 되는 toopass은)는 가상 어플라이언스를 통해 라우팅됩니다. Hello 스크립트에는 해당 규칙에에서도 만들어지는 hello 프런트 엔드 테이블입니다.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. 경로 항목 위에 hello 덮어씁니다 hello 기본 "0.0.0.0/0" 경로 하지만 여전히 있게 기존 hello 기본 10.0.0.0/16 규칙 트래픽 hello VNet tooroute 내에서 직접 toohello 대상과 toohello 네트워크 가상 어플라이언스 되지 않습니다. toocorrect이 동작 hello에 따라 규칙을 추가 해야 합니다.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. 이 시점에서 내용을 선택 toobe입니다. 두 경로 위에 hello로 모든 트래픽이 평가는 단일 서브넷 내에 트래픽에 대 한 toohello 방화벽을 라우팅합니다. 하지만이 세 번째, 특정 규칙을 추가할 수 있습니다 hello 방화벽의 개입 하지 않고 로컬 서브넷 tooroute 내에서 트래픽을 tooallow 권장 될 수도 있습니다. 이 경로의 모든 주소 destine hello 로컬 서브넷 just 수에 대 한 상태 라우팅할 있습니다 직접 (NextHopType VNETLocal =) 합니다.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. 마지막으로 hello 라우팅 테이블과 함께 사용자 정의 경로가 채웁니다 hello 테이블 이제 해야 바인딩된 tooa 서브넷입니다. Hello 스크립트 hello 프런트 엔드 경로 테이블도 바인딩된 toohello 프런트 엔드 서브넷이입니다. Hello 백 엔드 서브넷에 대 한 hello 바인딩 스크립트는 다음과 같습니다.
   
     Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>IP 전달
도우미 기능 tooUDR IP 전달 됩니다. 이 트래픽을 허용 하 고 tooreceive 특별히 가상 기기에서 설정을 toohello 기기 해결은 선택한 후 해당 트래픽을 tooits 최종 대상을 전달 합니다.

예를 들어 AppVM01 트래픽만 인해 요청 toohello DNS01 서버, UDR 라우팅합니다이 toohello 방화벽을입니다. IP 전달을 사용 하도록 설정와 hello DNS01 대상 (10.0.2.4)에 대 한 hello 트래픽은 hello 기기 (10.0.0.4)에서 허용 되며 tooits 최종 대상 (10.0.2.4)를 전달 합니다. 없이 IP 전달 hello 방화벽에서 사용 하도록 설정, 트래픽 것에서 허용 되지 hello 기기 hello 경로 테이블에 hello 다음 홉으로 hello 방화벽이 있는 경우에 합니다. 

> [!IMPORTANT]
> 것이 사용자 정의 된 라우팅을와 함께에서 중요 한 tooremember tooenable IP 전달 합니다.
> 
> 

IP 전달 설정은 단일 명령이며 VM을 만들 때 지정할 수 있습니다. Hello에 대 한이 예제에서는 hello 코드 조각의 흐름 hello hello 스크립트 끝에 반영 하 고 hello UDR 명령으로 그룹화:

1. Hello VM 인스턴스 가상 어플라이언스를 호출,이 경우 방화벽 hello 및 IP 전달 설정 (참고; 달러 기호로 시작 하는 빨간색의 모든 항목 (예:: $VMName[0]) hello이 문서의 hello 참조 섹션에는 스크립트에서 사용자 정의 변수입니다. [0] 대괄호로 0 hello, 나타냅니다 hello 수정 하지 않고 예제 스크립트 toowork hello에 대 한 Vm의 hello 배열에서 첫 번째 VM, 첫 번째 VM (VM 0) 해야 하는 hello hello 방화벽):
   
     Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>네트워크 보안 그룹(NSG)
이 예제에서는 NSG 그룹을 빌드한 후 단일 규칙을 로드합니다. 이 그룹은 다음 toohello 프런트 엔드 및 백 엔드 서브넷만 (하지 SecNet hello)를 연결 합니다. 선언적 규칙을 따르는 hello 작성 중인:

1. 전체 VNet (모든 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)

이 예제에서 NSG를 사용했지만 기본 목적은 수동 구성 시 실수가 발생할 경우를 대비하여 두 번째 방어 계층을 만드는 것입니다. 프런트 엔드 hello 인터넷 tooeither hello에서 모든 인바운드 트래픽을 tooblock 원하는 또는 hello SecNet 서브넷 toohello 방화벽을 통해 백 엔드 서브넷 트래픽 흐름만 (및 서브넷 toohello 프런트 엔드 또는 백 엔드에 적절 한 경우). 또한 장소에 hello UDR 규칙과 함께 않은 쉽게 변환할 hello 프런트 엔드 또는 백 엔드 서브넷 하는 모든 트래픽은 전송 toohello 방화벽 (감사 tooUDR) 초과 합니다. hello 표시 되는 것이 비대칭 흐름으로 방화벽과 hello 아웃 바운드 트래픽을 삭제 합니다. 있다는 3 계층의 보안 보호 hello 프런트 엔드 및 백 엔드 서브넷; 1) BackEnd001 클라우드 서비스, 2) Nsg 거부 없고 FrontEnd001 hello open 끝점에서 트래픽을 인터넷, 3) hello 방화벽 비대칭 트래픽을 삭제 hello 합니다.

이 예에서 hello 네트워크 보안 그룹에 대 한 흥미로운 사항이 하나 포함 한다는 것입니다 아래 표시 된 규칙이 하나만 있는 toodeny 인터넷 트래픽을 toohello 전체 가상 네트워크에 있는 hello 보안 서브넷을 포함 합니다. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

그러나 toohello 프런트 엔드 및 백 엔드 서브넷 hello NSG는만 바인딩되어 있으므로 hello 규칙 되지에서 처리 트래픽 인바운드 toohello 보안 서브넷입니다. 결과적으로, hello NSG 규칙 처음이 NSG hello toohello 보안 서브넷 바인딩되기 때문에 인터넷 트래픽을 tooany 주소가 없습니다. VNet hello에 라는, 경우에 트래픽 toohello 보안 서브넷을 흐릅니다.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>방화벽 규칙
Hello 방화벽에서 전달 규칙 toobe 생성 해야 합니다. Hello 방화벽 차단 또는 모든 인바운드, 아웃 바운드 전달 및 VNet 내 트래픽 이므로 많은 방화벽 규칙이 필요 합니다. 또한 모든 인바운드 트래픽 hello 보안 서비스 공용 IP 주소를 적중지 것입니다 (서로 다른 포트의 경우)에서 toobe hello 방화벽에 의해 처리 됩니다. 가장 좋은 방법은 나중에 hello 서브넷 및 방화벽 규칙 tooavoid 재작업을 설정 하기 전에 toodiagram hello 논리 흐름입니다. hello 다음 그림은이 예제에 대 한 hello 방화벽 규칙의 논리적 보기:

![Hello 방화벽 규칙의 논리적 보기][2]

> [!NOTE]
> Hello 관리 포트에 사용 되는 네트워크 가상 어플라이언스 hello에 따라 달라 집니다. 이 예제에서는 포트 22, 801, 807을 사용하는 Barracuda NextGen 방화벽을 참조합니다. Hello 어플라이언스 공급 업체 설명서 toofind hello 정확 하 게 사용 되는 포트를 사용 중인 hello 장치 관리를 참조 하십시오.
> 
> 

### <a name="logical-rule-description"></a>논리적 규칙 설명
Hello 논리 위의 다이어그램에서 hello 방화벽 hello 해당 서브넷에만 리소스가 고 hello 방화벽 규칙 및 방법은 논리적으로 허용 하거나 거부할 트래픽 흐름이 고 hello 실제 라우트된 경로가 아닌이 다이어그램에 표시 되므로 hello 보안 서브넷 표시 되지 않습니다. 또한 hello RDP 트래픽이 높은 범위가 지정 된 포트 (8014 – 8026) 되며 hello로 정렬 된 선택한 toosomewhat에 대해 선택 하는 hello 외부 포트 마지막 두 개 8 진수가 동일한 hello 쉽게 가독성을 위해 로컬 IP 주소 (예: 로컬 서버 주소 10.0.1.4 연결 된 그러나 외부 포트 8014) 더 높은 모든 충돌 하지 않는 포트를 사용할 수 없습니다.

이 예제에서는 7가지 유형의 규칙이 필요하며 아래에서 이러한 규칙 유형에 대해 설명합니다.

* 외부 규칙(인바운드 트래픽용):
  1. 방화벽 관리 규칙:이 앱의 리디렉션 규칙 hello 네트워크 가상 어플라이언스의 트래픽이 toopass toohello 관리 포트를 허용 합니다.
  2. (각 windows server) 용 RDP 규칙: (각 서버 마다 하나씩) 이러한 4 가지 규칙의 hello 관리 RDP 통해 개별 서버를 허용 합니다. Hello 사용 중인 네트워크 가상 어플라이언스의 hello 기능에 따라 하나의 규칙으로도 제공 수 없습니다.
  3. 응용 프로그램 트래픽 규칙: 두 응용 프로그램 트래픽 규칙을 hello 프런트 엔드 웹 트래픽에 대해 먼저 hello hello 백 엔드 트래픽 (예: 웹 서버 toodata 계층)에 대 한 두 번째 hello 가지 합니다. 이러한 규칙의 hello 구성 (서버 배치) hello 네트워크 아키텍처 및 트래픽 흐름 (어떤 방향이 hello 트래픽 흐름 및 사용 되는 포트)에 따라 달라 집니다.
     * 첫 번째 규칙의 hello hello 실제 응용 프로그램 트래픽 tooreach hello 응용 프로그램 서버를 허용 합니다. Hello 다른 규칙 보안, 관리, 등을 허용 하는 동안 응용 프로그램 규칙 hello (가) 외부 사용자 또는 서비스 tooaccess 허용 작업은입니다. 이 예에서는 포트 80에서 단일 웹 서버인는, 따라서 단일 방화벽 응용 프로그램 규칙은 인바운드 트래픽을 toohello 외부 IP toohello 웹 서버의 내부 IP 주소를 리디렉션합니다. hello 리디렉션 트래픽 세션은 NAT 미치지 않을 toohello 내부 서버입니다.
     * 두 번째 응용 프로그램 트래픽 규칙은 hello 모든 포트를 통해 백 엔드 규칙 tooallow hello 웹 서버 tootalk toohello AppVM01 서버 (않음 하지 AppVM02) hello 합니다.
* 내부 규칙(인트라-VNet 트래픽용)
  1. 아웃 바운드 tooInternet 규칙:이 규칙을 사용 하면 모든 네트워크에서 트래픽을 toopass toohello 선택한 네트워크입니다. 이 규칙은 일반적으로 기본 규칙 요소가 hello 방화벽에 있지만 사용할 수 없는 상태에 있습니다. 이 예제에서는 이 규칙을 사용하도록 설정해야 합니다.
  2. DNS 규칙:이 규칙에는 DNS (포트 53) 트래픽 toopass toohello DNS 서버 에서만 허용 됩니다. Hello 프런트 엔드 toohello 백 엔드에서에서 대부분 트래픽을 차단 하는이 환경에 대 한이 규칙은 특히 DNS 모든 로컬 서브넷에서 허용 합니다.
  3. 서브넷 tooSubnet 규칙:이 규칙은 tooallow hello 프런트 엔드 서브넷에 서브넷 tooconnect tooany 서버 종료 (하지만 하지 역방향 hello)의 모든 서버 hello 백에서 합니다.
* 유사 시 대기 (트래픽에 대 한 규칙 hello 위의 중 하나를 만족 하지 않는):
  1. 모든 트래픽 규칙 거부:이 hello 최종 규칙 (측면에서 우선 순위)은 항상 고 따라서 트래픽이 이동 하면 실패 toomatch hello 앞에이 규칙에 의해 삭제 됩니다 규칙의 합니다. 이 규칙은 기본 규칙으로 일반적으로 활성화되어 있으며 수정이 필요하지 않는 경우가 대부분입니다.

> [!TIP]
> Hello 두 번째 응용 프로그램 트래픽 규칙 모든 포트가이 예제의 쉽게에 대 한 허용 됩니다에서 실제 시나리오 hello 가장 구체적인 포트와 주소 범위입니다.이 규칙의 사용된 tooreduce hello 공격 노출 영역 이어야 합니다.
> 
> 

<br />

> [!IMPORTANT]
> 모든 규칙 위에 hello를 만든 후에 tooreview hello 각 규칙 tooensure 트래픽의 우선 순위 허용 하거나 필요에 따라 거부 중요 합니다. 예를 들어 hello 규칙은 우선 순위에 따라입니다. 쉽게 toobe toomis 정렬 규칙 기한 hello 방화벽 잠긴 경우 여기에 최소한 자체 hello 방화벽에 대 한 hello 관리는 항상 hello 절대 가장 높은 우선 순위 규칙을 확인 합니다.
> 
> 

### <a name="rule-prerequisites"></a>규칙 필수 조건
Hello 가상 컴퓨터가 실행 중인 hello 방화벽에 대 한 필수 구성 요소 하나은 공용 끝점입니다. Hello 방화벽 tooprocess 트래픽에 대 한 적절 한 공용 끝점 hello 열려 있어야 합니다. 세 가지 방법으로이 예에서; 트래픽 1) 관리 트래픽 toocontrol hello 방화벽 및 방화벽 규칙, 2) RDP 트래픽 toocontrol hello windows 서버 및 3) 응용 프로그램 트래픽이 합니다. 이들은 hello 위쪽에 있는 트래픽 형식의 hello 세 개의 열 위에 hello 방화벽 규칙의 논리 보기의 절반입니다.

> [!IMPORTANT]
> 키 takeway 여기는 tooremember 하 **모든** 트래픽이 hello 방화벽을 통해 시작 됩니다. 따라서 tooremote 데스크톱 toohello IIS01 서버 라고 하더라도 hello 프런트 엔드 서브넷에 tooaccess와 hello 프런트 엔드 클라우드 서비스에에서이 서버 tooRDP toohello 방화벽에 필요한 포트 8014, 사용 되 고 hello 방화벽 tooroute hello RDP 요청을 내부적으로 허용 toohello IIS01 RDP 포트입니다. hello Azure 포털의 "연결" 단추 (관련해 서 hello 포털 참조 수) 없는 직접 RDP 경로 tooIIS01 있기 때문에 작동 하지 않습니다. 즉, 모든 연결 hello에서 toohello 보안 서비스 및 포트, secscv001.cloudapp.net:xxxx (외부 포트 및 내부 ip 주소 및 포트 매핑 hello에 대 한 다이어그램 위에서 참조 hello) 예: 인터넷 여야 합니다.
> 
> 

끝점 hello VM 생성 시 열 수 있습니다 또는 hello 예제 스크립트에서 수행 되며이 코드 조각에서는 아래 표시 된 대로 빌드를 게시할 (참고; 모든 항목 시작 부분에 달러 기호 (예:: $VMName[$i])는 hello referen의 hello 스크립트에서 사용자 정의 변수 이 문서의 섹션 ce입니다. 대괄호로 [$i] "$i" hello 나타내는 Vm의 배열에서 특정 VM의 hello 배열 번호):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

하지 명확 하 게 여기에 표시 된 기한 않지만 변수 하지만 끝점의 toohello 사용은 **만** hello 보안 클라우드 서비스에서 열. 이 모든 인바운드 트래픽을 처리 하는 tooensure 라우팅되면 NAT를 생략 된 hello 방화벽에 의해 합니다.

관리 클라이언트에서는 toobe PC toomanage hello 방화벽에 설치 되어 있어야 하 고 필요한 hello 구성을 만듭니다. 어떻게 toomanage hello 장치에 hello 설명서 방화벽 (또는 다른 NVA)에서 공급 업체를 참조 하십시오. 이 섹션 및 방화벽 규칙 만들기 hello 다음 섹션의 나머지 부분에서는 hello hello 공급 업체 관리 클라이언트 (즉, 하지 hello Azure 포털 또는 PowerShell)를 통해 자체 hello 방화벽의 hello 구성에 설명 합니다.

클라이언트 다운로드 및 연결 toohello Barracuda이 예에서 사용에 대 한 지침은 여기: [Barracuda NG 관리자](https://techlib.barracuda.com/NG61/NGAdmin)

hello 규칙을 만들; 보다 쉽게 만들 수 있는 두 가지 필수 구성 요소 개체 클래스가 hello 방화벽에 있지만 방화벽 규칙을 만들기 전에 로그에 기록 되 면 네트워크 및 서비스 개체입니다.

이 예제에서는 세 개의 명명 된 네트워크 개체 정의 (hello 프런트 엔드 서브넷 및 hello 백 엔드 서브넷에도 hello hello DNS 서버의 IP 주소에 대 한 네트워크 개체에 대해 각각 하나씩) 이어야 합니다. 명명 된 네트워크; toocreate hello Barracuda NG 관리자 클라이언트 대시보드에서 부터는 toohello 구성 탭 이동, hello Operational 구성 섹션에서에서 규칙 집합을 클릭, 클릭 한 후 "네트워크" hello 방화벽 객체 메뉴에서 고 hello 네트워크 편집 메뉴에서 새로 만들기를 클릭 합니다. hello 네트워크 개체 hello 이름과 hello 접두사를 추가 하 여 만들 이제 있습니다.

![프런트 엔드 네트워크 개체 만들기][3]

이렇게 하면 hello 프런트 엔드 서브넷에 대 한 명명 된 네트워크 만들어집니다, 그리고 hello 백 엔드 서브넷에도 비슷한 개체를 작성 해야 합니다. 이제 hello 서브넷 hello 방화벽 규칙에 대 한 이름으로 보다 쉽게 참조할 수 있습니다.

에 대 한 DNS 서버 개체를 hello:

![DNS 서버 개체 만들기][4]

이 단일 IP 주소 참조가 hello 문서의 뒷부분에 나오는 DNS 규칙에 사용 됩니다.

hello 두 번째 필수 구성 요소 개체는 서비스 개체입니다. 이 각 서버에 대 한 hello RDP 연결 포트를 나타냅니다. Hello 기존 RDP 서비스 개체에 바인딩된 toohello 기본 RDP 포트 이므로 3389 새로운 서비스에서에서 만들 수 있습니다 tooallow 트래픽은 hello 외부 포트 (8014 8026). hello 새 포트 toohello 기존 RDP 서비스를 추가할 수도 있지만 설명의 편의 각 서버에 대해 개별 규칙을 만들 수 있습니다. toocreate 서버;에 대 한 새 RDP 규칙 toohello 구성 탭을 탐색 hello Barracuda NG 관리 클라이언트 대시보드에서 시작, hello Operational 구성에서에서 섹션 클릭 규칙 집합을 다음 hello 서비스 hello 목록 아래로 스크롤하여 방화벽 개체 메뉴에서 "서비스"를 클릭 하 고 선택 hello "RDP" 서비스입니다. 마우스 오른쪽 단추로 복사를 클릭하여 선택한 다음 마우스 오른쪽 단추로 붙여넣기를 클릭하여 선택합니다. 이제 RDP-Copy1 서비스 개체를 편집할 수 있습니다. RDP Copy1를 마우스 오른쪽 단추로 클릭 하 고 편집을 선택, 서비스 개체 편집 다음과 같이 창이 팝업 됩니다 hello:

![기본 RDP 규칙 복사본][5]

hello 값 편집된 toorepresent hello 특정 서버에 대 한 RDP 서비스 수 있습니다. 기본 위에 AppVM01 hello에 대 한 RDP 규칙에는 수정 된 tooreflect 새 서비스 이름, 설명, 되어야 할지와 그림 8 다이어그램 hello에 외부 RDP 포트 사용 (참고: hello 포트가 hello RDP toohello 외부 포트 3389를 사용 하는이 기본값에서에서 변경 된 특정 서버 AppVM01 hello 외부 포트의 hello 경우에는 8025) hello 수정 된 서비스는 다음과 같습니다.

![AppVM01 규칙][6]

이 프로세스 반복된 toocreate 서버; 남은 hello에 대 한 RDP 서비스 여야 합니다. AppVM02, DNS01, 및 IIS01 합니다. 이러한 서비스의 hello 생성을 하면 hello 규칙을 만드는 간단 하 고 더욱 명확 하 게 hello 다음 섹션에 있습니다.

> [!NOTE]
> 두 가지 이유로; hello 방화벽에 대 한는 RDP 서비스가 필요 하지 않습니다. 1) 첫 번째 hello 방화벽 VM은 Linux 기반 이미지 SSH 포트는 RDP, 2) 포트 22 대신 VM 관리에 대 한 22에서 사용 된 것과 다른 두 개의 관리 포트 관리 연결에 대 한 tooallow 아래에 설명 된 hello 첫 번째 관리 규칙 사용할 수 있도록 합니다.
> 
> 

### <a name="firewall-rules-creation"></a>방화벽 규칙 만들기
이 예제에는 세 가지 유형의 방화벽 규칙을 사용하며 각각 고유한 아이콘이 있습니다.

응용 프로그램 리디렉션 규칙이 hello: ![응용 프로그램 리디렉션 아이콘][7]

hello 대상 NAT 규칙: ![대상 NAT 아이콘][8]

hello 통과 규칙: ![전달 아이콘][9]

이러한 규칙에 대 한 자세한 내용은 hello Barracuda 웹 사이트에서 찾을 수 있습니다.

toocreate 규칙에 따라 hello (또는 기존 기본 규칙 확인) hello Operational 구성 섹션에서 규칙 집합을 toohello 구성 탭 이동 hello Barracuda NG 관리 클라이언트 대시보드를 시작 합니다. 표 호출 하 여 "Main 규칙" hello이이 방화벽에 대 한 규칙 활성화 및 비활성화 된 기존 표시 됩니다. Hello 오른쪽 상단의이 눈금은 작은 녹색 "+" 단추를 클릭이 toocreate 새 규칙 (참고: 표시 단추에 "Lock"으로 표시는 없습니다 toocreate 또는 규칙을 편집,이 단추를 클릭 하는 경우 너무 "잠금 해제" hello 규칙 se, 방화벽 "잠겨" 변경에 대 한 t 편집). 기존 규칙 tooedit을 원한다 해당 규칙을 선택, 마우스 오른쪽 단추로 클릭 하 고 편집할 규칙을 선택 합니다.

규칙은 생성 및/또는 수정, 일단 해야만 해당 toohello 방화벽 푸시되 며 다음 처리 되 고 활성화, 이렇게 하지 않으면 hello 규칙 변경 내용이 적용 되지 것입니다. hello 세부 정보 규칙 설명은 아래 hello 푸시 및 활성화 프로세스에 설명 합니다.

각 규칙의 hello 비슷하므로이 예제는 다음과 같이 설명 toocomplete가 필요 합니다.

* **관리 규칙을 방화벽**:이 응용 프로그램 리디렉션 규칙이 toopass toohello 관리 포트가이 예에서 Barracuda NextGen 방화벽 hello 네트워크 가상 어플라이언스로의 트래픽을 허용 합니다. hello 관리는 801, 807 필요에 따라 22입니다. hello 외부 및 내부 포트 동일 (예: 포트 변환) hello 됩니다. SETUP-MGMT-ACCESS가 기본 규칙이며 기본적으로 사용하도록 설정되어 있습니다(Barracuda NextGen Firewall 버전 6.1).
  
    ![방화벽 관리 규칙][10]

> [!TIP]
> hello 소스 주소 공간이이 규칙에는 임의의 경우 hello 알려진 관리 IP 주소 범위,이 범위를 줄이는 hello 공격 노출 toohello 관리 포트가 줄일 수 있습니다.
> 
> 

* **RDP 규칙**: 이러한 대상 NAT 규칙의 hello 관리 RDP 통해 개별 서버를 허용 합니다.
  이 규칙은 4 개의 필요한 중요 한 필드 toocreate:
  
  1. 소스 hello 원본 필드에 사용 되는 "Any" hello 참조 어디에서 든 RDP tooallow입니다.
  2. Hello 외부 포트 리디렉션 toohello 서버 로컬 IP 주소와 tooport 3386 (hello 기본 RDP 포트)를 서비스 – 적절 한 서비스 개체는이 경우 "AppVM01 RDP" 앞에서 만든 hello를 사용 합니다. 이 특정 규칙 RDP 액세스 tooAppVM01입니다.
  3. 대상-hello 해야 *hello 방화벽에 로컬 포트*, "DCHP 1 로컬 IP" 또는 t h 0 고정 Ip를 사용 하는 경우. hello 서 수 (eth0, e t h 1 등)는 네트워크 어플라이언스에 여러 로컬 인터페이스가 포함 하는 경우 달라질 수 있습니다. 이 hello 포트 hello 방화벽에서를 전송 (포트를 수신 하는 hello로 hello 동일)을 수 hello 실제 라우팅된 대상을 hello 대상 목록 필드에이 합니다.
  4. 리디렉션 –이 섹션에서는 설명 hello 가상 어플라이언스 tooultimately이이 트래픽을 리디렉션해야 하는 위치입니다. hello 가장 간단한 리디렉션은 tooplace hello IP 및 hello 대상 목록 필드에 지정 된 포트 (선택 사항)입니다. 대상 포트 hello 인바운드 요청에 사용 되는 hello 포트가 없는 경우 됩니다 (ie 변환 없음), 포트 hello 포트를 지정 된 경우 사용 됩니다 NAT 함께 hello IP 주소를 지정 합니다.
     
     ![방화벽 RDP 규칙][11]
     
     환경에서는 총 4 개의 RDP 규칙의 toobe 만든이 필요 합니다. 
     
     | 규칙 이름 | 서버 | 부여 | 대상 목록 |
     | --- | --- | --- | --- |
     | RDP-to-IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP-to-DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP-to-AppVM01 |AppVM01 |AppVM01 RDP |10.0.2.5:3389 |
     | RDP-to-AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> Hello hello 소스 범위의 키와 서비스 필드 범위를 좁혀 hello 공격 노출 영역이 감소 합니다. 기능을 사용 하면 hello 가장 제한 된 범위를 사용 해야 합니다.
> 
> 

* **응용 프로그램 트래픽 규칙**: 두 개의 응용 프로그램 트래픽 규칙, hello 프런트 엔드 웹 트래픽에 대해 먼저 hello 및 hello 백 엔드 트래픽 (예: 웹 서버 toodata 계층)에 대 한 두 번째 hello 없는 합니다. 이러한 규칙은 hello 네트워크 아키텍처 (위해 서버를 배치 하는 위치) 및 트래픽 흐름 (어떤 방향이 hello 트래픽 흐름 및 사용 되는 포트)에 따라 달라 집니다.
  
    먼저 설명 하는 것은 웹 트래픽에 대해 hello 프런트 엔드 규칙입니다.
  
    ![방화벽 웹 규칙][12]
  
    이 대상 NAT 규칙 hello 실제 응용 프로그램 트래픽 tooreach hello 응용 프로그램 서버를 수 있습니다. Hello 다른 규칙 보안, 관리, 등을 허용 하는 동안 응용 프로그램 규칙 hello (가) 외부 사용자 또는 서비스 tooaccess 허용 작업은입니다. 이 예에서는 포트 80 켜져 단일 웹 서버, 따라서 hello 단일 방화벽 응용 프로그램 규칙은 인바운드 트래픽을 toohello 외부 IP toohello 웹 서버의 내부 IP 주소를 리디렉션합니다.
  
    **참고**: hello 대상 목록 필드에 할당 된 포트는, 따라서 hello 인바운드 포트 80 (또는 hello 선택 되어 있는 서비스의 경우 443)에 사용할 hello 웹 서버의 hello 리디렉션. Hello 웹 서버를 다른 포트에서 수신 하는 경우 예를 들어: 포트 8080, hello 대상 목록 필드도 hello 포트 리디렉션에 대 한 업데이트 된 too10.0.1.4:8080 tooallow 수 있습니다.
  
    hello 다음 응용 프로그램 트래픽 규칙은 모든 서비스를 통해 백 엔드 규칙 tooallow hello 웹 서버 tootalk toohello AppVM01 서버 (않음 하지 AppVM02) hello:
  
    ![방화벽 AppVM01 규칙][13]
  
    이 통과 규칙은 모든 IIS 서버에서 hello 프런트 엔드 서브넷 tooreach hello AppVM01 (IP 주소 10.0.2.5) 모든 포트에서 hello 웹 응용 프로그램에 필요한 프로토콜 tooaccess 데이터를 사용 하 여 허용 합니다.
  
    이 화면에는 "\<명시적-dest\>" hello 대상 필드 toosignify 10.0.2.5에에서 hello 대상으로 사용 됩니다. 일 수 명시적 표시 된 것 처럼 또는 명명 된 네트워크 개체 (값으로 DNS 서버 hello에 대 한 필수 구성 요소 hello에에서). 이 hello 방화벽의 toohello 관리자를 toowhich 메서드가 사용 됩니다. Explict Desitnation,으로 10.0.2.5 tooadd hello 아래의 첫 번째 빈 행을 두 번 클릭 \<명시적-dest\> 팝업 되 hello 창의 hello 주소를 입력 합니다.
  
    없는 NAT 때문에이 내부 트래픽이 너무 hello 연결 방법을 설정할 수 있도록이 전달 규칙을 사용 하면 필요한 "No SNAT"입니다.
  
    **참고**:이 규칙에 hello 원본 네트워크는 모든 리소스 hello 프런트 엔드 서브넷에만, 또는 되기 알려진된 특정 수의 웹 서버, 리소스일 수 네트워크 개체를 만들 toobe 보다 구체적인 toothose 정확 하 게 IP 주소 대신 하는 경우 hello 전체 프런트 엔드 서브넷입니다.

> [!TIP]
> 이 규칙에 "임의" toomake 샘플 응용 프로그램 보다 쉽게 toosetup hello 및 사용 하 여 hello 서비스 사용 하 여, 또한 이렇게 하면 ICMPv4 단일 규칙에서 (ping). 하지만 권장되는 방식은 아닙니다. hello 포트 및 프로토콜 ("서비스")이이 경계를 넘어 응용 프로그램 작업 tooreduce hello 공격 노출 영역을 허용 하는 좁은 범위의 toohello 최소 가능 해야 합니다.
> 
> 

<br />

> [!TIP]
> 이 규칙을 사용 하 고는 dest 명시적 참조를 표시 하지만 전체 hello 방화벽 구성 일관적인 접근 방식을 사용 해야 합니다. 명명 된 네트워크 개체는 hello 쉽게 가독성 및 지원 가능성에 대 한 전체에서 사용 될 것이 좋습니다. 안녕하세요 명시적-dest 여기 사용 되는 유일한 tooshow 대체 참조 메서드이고 (특히 복잡 한 구성의 경우)에 일반적으로 권장 되지 않습니다.
> 
> 

* **아웃 바운드 tooInternet 규칙**:이 전달 규칙에는 모든 원본 네트워크 toopass toohello 선택한 대상 네트워크의 트래픽을 허용 됩니다. 이 규칙은 hello Barracuda NextGen 방화벽을 이미 일반적으로 기본 규칙을 않으며 사용할 수 없는 상태입니다. 이 규칙을 마우스 오른쪽 단추로 클릭 hello 규칙 활성화 명령에 액세스할 수 있습니다. 여기에 표시 된 hello 규칙 수정된 tooadd hello 로컬 서브넷인 hello이이 규칙의이 문서 toohello 원본 특성의 필수 구성 요소 섹션에 참조로 생성 된 되었습니다.
  
    ![방화벽 아웃바운드 규칙][14]
* **DNS 규칙**: 전달이 규칙은 DNS (포트 53) 트래픽 toopass toohello DNS 서버 에서만 허용 됩니다. Hello 프런트 엔드 toohello 백 엔드에서에서 대부분 트래픽을 차단 하는이 환경에 대 한이 규칙은 특히 DNS 허용 됩니다.
  
    ![방화벽 DNS 규칙][15]
  
    **참고**:이 화면에서 발된 hello 라이선스 서버의 연결 방법이 포함 됩니다. 내부 IP toointernal IP 주소 트래픽에 대 한이 규칙 이기 때문에 없는 NATing가 필요 합니다이 hello이 연결 방법은 너무 설정 되어이 통과 규칙에 대 한 "No SNAT"입니다.
* **서브넷 tooSubnet 규칙**: 전달이 규칙은 활성화 된 기본 규칙 및의 모든 서버에서 다시 hello에 서브넷 tooconnect tooany 서버를 종료 하는 수정 된 tooallow hello 프런트 엔드 서브넷입니다. 이 규칙에는 모든 내부 트래픽 하므로 hello 라이선스 서버의 연결 방법이 tooNo SNAT를 설정할 수 있습니다.
  
    ![방화벽 인트라-VNet 규칙][16]
  
    **참고**: hello 양방향 확인란을 선택 하지 않으면 (아닙니다 대부분의 규칙에서 확인),이 기능은 "하나 방향" 규칙이 있다는 점에서이 규칙에 대 한 중요, hello 백 엔드 서브넷 toohello 프런트 엔드 네트워크에 대 한 연결을 시작할 수 있습니다 하지만 하지 역방향 hello 합니다. 이 확인란을 선택할 경우 이 규칙에서 양방향 트래픽이 허용되며 논리적 다이어그램에 따라 바람직하지 않습니다.
* **모든 트래픽 규칙 거부**: hello 최종 규칙 (측면에서 우선 순위)와 항상를 이어야 하며 따라서 트래픽이 이동 실패 toomatch hello 규칙 앞에 하면 삭제 됩니다이 규칙에 의해 합니다. 이 규칙은 기본 규칙으로 일반적으로 활성화되어 있으며 수정이 필요하지 않는 경우가 대부분입니다. 
  
    ![방화벽 거부 규칙][17]

> [!IMPORTANT]
> 모든 규칙 위에 hello를 만든 후에 tooreview hello 각 규칙 tooensure 트래픽의 우선 순위 허용 하거나 필요에 따라 거부 중요 합니다. 예를 들어 hello 규칙 hello 전달 규칙 hello Barracuda 관리 클라이언트에서에서 주 눈금에에서 표시 되어야 하는 hello 순서로 표시 됩니다.
> 
> 

## <a name="rule-activation"></a>규칙 활성화
Hello 논리 다이어그램의 수정 된 ruleset toohello 사양 hello hello ruleset 이어야 toohello 방화벽을 업로드 하 고 활성화 합니다.

![방화벽 규칙 활성화][18]

Hello 관리 클라이언트의 오른쪽 상단 모서리 hello 단추의 클러스터가 됩니다. Hello "보낼 변경" 단추 toosend hello 수정 규칙 toohello 방화벽 클릭 hello "활성화" 단추를 클릭 합니다.

이 예에서는 환경 구축 hello 방화벽 규칙 집합의 정품 인증의 hello 완료 되었습니다.

## <a name="traffic-scenarios"></a>트래픽 시나리오
> [!IMPORTANT]
> 키 takeway은 tooremember 하 **모든** 트래픽이 hello 방화벽을 통해 시작 됩니다. 따라서 tooremote 데스크톱 toohello IIS01 서버 라고 하더라도 hello 프런트 엔드 서브넷에 tooaccess와 hello 프런트 엔드 클라우드 서비스에에서이 서버 tooRDP toohello 방화벽에 필요한 포트 8014, 사용 되 고 hello 방화벽 tooroute hello RDP 요청을 내부적으로 허용 toohello IIS01 RDP 포트입니다. hello Azure 포털의 "연결" 단추 (관련해 서 hello 포털 참조 수) 없는 직접 RDP 경로 tooIIS01 있기 때문에 작동 하지 않습니다. 즉, 모든 연결 hello에서 toohello 보안 서비스 및 포트, secscv001.cloudapp.net:xxxx 예: 인터넷 여야 합니다.
> 
> 

이러한 시나리오에 대 한 방화벽 규칙에 따라 hello 위치 여야 합니다.

1. 방화벽 관리
2. RDP tooIIS01
3. RDP tooDNS01
4. RDP tooAppVM01
5. RDP tooAppVM02
6. 웹 앱 트래픽 toohello
7. 앱 트래픽 tooAppVM01
8. 아웃 바운드 toohello 인터넷
9. 프런트 엔드 tooDNS01
10. 내 서브넷 간의 트래픽은 (백 엔드 toofront 끝에만 해당)
11. 모두 거부

hello 실제 방화벽 규칙 집합 또한 toothese에서 여러 가지 규칙 줄 가능성이 큽니다, 지정 된 모든 방화벽 규칙 hello 서로 다른 우선 순위는 hello 여기에 나열 된 것 보다 합니다. 이 목록 및 연결 된 번호는 이러한 11 개의 규칙 및 적용 hello 상대적 우선 순위만 간의 tooprovide 관련성입니다. 즉; hello 실제 방화벽 "RDP tooIIS01" hello 규칙 번호 5, 수 있지만이 목록의 hello 의도가 맞게 hello "RDP tooDNS01" 규칙 이상 hello "방화벽 관리" 규칙 아래를 될 수 있습니다. hello 목록 아래 시나리오를 간단 하 게 나타내기; 허용 hello에도 도움이 될 예: "FW Rule 9 (DNS)". 간단한 설명을 위해 네 개의 RDP 규칙 통칭 됩니다 hello 라고도 함, "hello RDP 규칙" hello 트래픽 시나리오 관련 없는 tooRDP를가 하는 경우.

또한 네트워크 보안 그룹은 hello 프런트 엔드에 인바운드 인터넷 트래픽에 대해와 백 엔드 서브넷 점에 유의 하세요.

#### <a name="allowed-internet-tooweb-server"></a>(사용 가능) 인터넷 tooWeb 서버
1. 인터넷 사용자가 SecSvc001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 클라우드 서비스).
2. 10.0.0.4:80에 포트 80 toofirewall 인터페이스에 대 한 열린 끝점을 통해 클라우드 서비스 전달 트래픽
3. 없음 NSG tooSecurity 서브넷에 할당 하는 시스템 NSG 규칙에서 트래픽을 toofirewall 허용 되므로
4. 트래픽은 hello 방화벽 (10.0.1.4)의 내부 IP 주소에 도달
5. 방화벽에서 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
   2. FW 규칙 2-5 (RDP 규칙), 적용 하지 않는 toonext 규칙 이동
   3. FW 규칙 6 (응용 프로그램: 웹), 해당 방화벽 Nat 트래픽이 허용 것 too10.0.1.4 (IIS01)
6. 인바운드 규칙 처리를 시작 하는 hello 프런트 엔드 서브넷:
   1. NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다 (이 트래픽은 NAT가 hello 방화벽에 의해 것, 따라서 hello 소스 주소는 이제 hello 보안 서브넷에는 hello 방화벽 NSG toobe "local" 트래픽 hello 프런트 엔드 서브넷에는 표시 있고 따라서 허용), toonext 규칙 이동
   2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
7. IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다
8. IIS01 백 엔드 서브넷에 FTP 세션 tooAppVM01 tooinitiates 시도
9. hello UDR 프런트 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉
10. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
11. 방화벽에서 규칙 처리를 시작합니다.
    1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
    2. Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.
    3. FW 규칙 6 (응용 프로그램: 웹) toonext 규칙을 이동, 적용 하지 않습니다
    4. FW 규칙 7 (응용 프로그램: 백 엔드)를 적용 하는 트래픽을 허용, 방화벽 전달 트래픽 too10.0.2.5 (AppVM01)
12. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
    1. Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다
    2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
13. AppVM01은 hello 요청을 수신 하 고 hello 세션 시작 및 응답
14. hello UDR 백 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉
15. 이어서 hello 백 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù
16. 연결된 세션 hello 방화벽 hello 응답 백 toohello 웹 서버 (IIS01) 트래픽에서 반환이 때문에 통과
17. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
    1. Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다
    2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
18. 이 HTTP 응답은 toohello 요청자에 게 전송 hello IIS 서버 hello 응답을 받은 AppVM01를 사용 하 여 hello 트랜잭션을 완료 하 고 건물 hello HTTP 응답을 요청한 후,
19. 이어서 hello 프런트 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù
20. HTTP 응답 적중 hello 방화벽 hello 하며 NAT 세션은 hello 방화벽에 의해 허용 되는이 항목은 hello 응답 tooan 설정
21. hello 방화벽이 리디렉션합니다 hello 응답 백 toohello를 인터넷 사용자
22. 아웃 바운드 NSG 규칙 또는 UDR 홉 없는지 이후 hello 프런트 엔드 서브넷에 hello 응답 허용 되 고 hello 인터넷 사용자 hello 웹 페이지 요청을 받습니다.

#### <a name="allowed-internet-rdp-toobackend"></a>(사용 가능) 인터넷 RDP tooBackend
1. 인터넷에서 서버 관리자 RDP 세션 tooAppVM01 SecSvc001.CloudApp.Net:8025, 8025 hello hello "RDP tooAppVM01" 방화벽 규칙에 대 한 포트 번호를 할당 하는 사용자가을 통해 요청
2. hello 클라우드 서비스 10.0.0.4:8025 8025 toofirewall 인터페이스 포트에 hello 열린 끝점을 통해 트래픽을 전달합니다
3. 없음 NSG tooSecurity 서브넷에 할당 하는 시스템 NSG 규칙에서 트래픽을 toofirewall 허용 되므로
4. 방화벽에서 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
   2. Toonext 규칙 이동 FW 규칙 2 (RDP IIS) 적용 되지 않습니다
   3. Toonext 규칙 이동 FW 규칙 3 (RDP DNS01) 적용 되지 않습니다
   4. FW 규칙 4 (RDP AppVM01)은 적용, 방화벽 Nat 트래픽을 허용 하기 too10.0.2.5:3386 (AppVM01 RDP 포트)
5. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
   1. NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다 (이 트래픽은 NAT가 hello 방화벽에 의해 것, 따라서 hello 소스 주소는 이제 hello 보안 서브넷에는 hello 방화벽 NSG toobe "local" 트래픽 hello 백 엔드 서브넷에는 표시 있고 따라서 허용), toonext 규칙 이동
   2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
6. AppVM01이 RDP 트래픽을 수신 대기하다 응답합니다.
7. 아웃바운드 NSG 규칙이 없으므로 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.
8. Hello 다음 홉으로 UDR 경로 아웃 바운드 트래픽 toohello 방화벽
9. 연결된 세션 hello 방화벽 hello 응답 백 toohello 인터넷 사용자 트래픽을에서 반환이 때문에 통과
10. RDP 세션이 사용하도록 설정됩니다.
11. AppVM01에서 사용자 이름과 암호를 묻습니다.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(허용) DNS 서버에서 웹 서버 DNS 조회
1. 웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.
2. hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01
3. Hello 다음 홉으로 UDR 경로 아웃 바운드 트래픽 toohello 방화벽
4. 아웃 바운드 NSG 규칙이 바인딩된 toohello 프런트 엔드 서브넷은, 트래픽이 허용 됩니다.
5. 방화벽에서 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
   2. Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.
   3. FW 규칙 6 및 7 (앱 규칙) 적용 안 함, toonext 규칙 이동
   4. Toonext 규칙 이동 FW 규칙 8 (tooInternet) 적용 되지 않습니다
   5. FW 규칙 9 (DNS)은 적용, 트래픽을 허용, 방화벽 전달 트래픽 too10.0.2.4 (DNS01)
6. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
   1. Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다
   2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
7. DNS 서버 hello 요청 수신
8. DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷
9. Hello 다음 홉으로 UDR 경로 아웃 바운드 트래픽 toohello 방화벽
10. 백 엔드 서브넷에 아웃바운드 NSG 규칙이 없고 트래픽이 허용됩니다.
11. 방화벽에서 규칙 처리를 시작합니다.
    1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
    2. Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.
    3. FW 규칙 6 및 7 (앱 규칙) 적용 안 함, toonext 규칙 이동
    4. FW 규칙 8 (tooInternet)은 적용, 트래픽을 허용, 세션 hello 인터넷의 DNS 서버 tooroot 아웃 SNAT은
12. 인터넷 DNS 서버 응답 hello 방화벽에서이 세션이 시작 된, 때문 hello 응답 수락한 경우 hello 방화벽
13. Hello 방화벽 전달 hello 응답 toohello DNS01 서버를 시작 합니다. 지금은 연결된 된 세션 이기
14. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
    1. Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다
    2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
15. hello DNS 서버 hello 응답을 캐시 받아서 toohello 초기 요청 백 tooIIS01 응답
16. hello UDR 백 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉
17. 아웃 바운드 NSG 규칙이 hello 백 엔드 서브넷에 있는 트래픽이 허용 됩니다.
18. 이 hello 방화벽에서 연결된 된 세션, hello 응답 hello 방화벽 백 toohello IIS 서버에 의해 전달 됩니다.
19. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
    1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
    2. hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용
20. IIS01은 DNS01에서 hello 응답을 받습니다.

#### <a name="allowed-backend-server-toofrontend-server"></a>(사용 가능) 백 엔드 서버 tooFrontend 서버
1. 로그온 한 tooAppVM02 RDP 통해 관리자는 파일 서버에서 직접 요청 hello IIS01 windows 파일 탐색기를 통해
2. hello UDR 백 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉
3. 이어서 hello 백 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù
4. 방화벽에서 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
   2. Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.
   3. FW 규칙 6 및 7 (앱 규칙) 적용 안 함, toonext 규칙 이동
   4. Toonext 규칙 이동 FW 규칙 8 (tooInternet) 적용 되지 않습니다
   5. Toonext 규칙 이동 FW 규칙 9 (DNS)를 적용 하지 않습니다.
   6. FW 규칙 10 (내 서브넷)은 적용, 트래픽을 허용, 방화벽 전달 트래픽 too10.0.1.4 (IIS01)
5. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다
   2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
6. 적절 한 인증 및 권한 부여 라고 가정할 경우 IIS01 hello 요청을 수락 및 응답
7. hello UDR 프런트 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉
8. 이어서 hello 프런트 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù
9. Hello 방화벽에서 기존 세션의 경우 이것이이 응답이 허용 하 고 hello 방화벽 hello 응답 tooAppVM02를 반환 합니다.
10. 백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.
    1. Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다
    2. 서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.
11. AppVM02는 hello 응답 수신

#### <a name="denied-internet-direct-tooweb-server"></a>(거부 됨) 인터넷 직접 tooWeb 서버
1. 인터넷 사용자가 tooaccess hello 웹 IIS01를 통해 서버 hello FrontEnd001.CloudApp.Net 서비스
2. HTTP 트래픽에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스를 통과 하지는 및 hello 서버에 도달 하지 않습니다.
3. 어떤 이유로 hello 끝점 열려 있던 경우 hello 프런트 엔드 서브넷에 NSG (블록 인터넷) hello를이 트래픽 차단
4. 마지막으로, hello 프런트 엔드 서브넷 UDR 경로 hello 다음 홉으로 IIS01 toohello 방화벽에서 모든 아웃 바운드 트래픽을 보내는 것과 및 hello 방화벽은 비대칭 트래픽으로 표시 되는이 놓습니다 hello 아웃 바운드 응답의 3 개 이상 독립적인 층 따라서 방어 hello 간의 인터넷 및 IIS01 권한이 없음/부적절 한 액세스를 방지 하는 클라우드 서비스를 통해 합니다.

#### <a name="denied-internet-toobackend-server"></a>(거부 됨) 인터넷 tooBackend 서버
1. 인터넷 사용자가 tooaccess hello BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에 있는 파일
2. 파일 공유에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 한 hello 서버에 도달 하지
3. 어떤 이유로 hello 끝점 열려 있던 경우 hello NSG (블록 인터넷)를이 트래픽 차단
4. 마지막으로, hello UDR 경로 hello 다음 홉으로 AppVM01 toohello 방화벽에서 모든 아웃 바운드 트래픽을 보내는 것과 및 hello 방화벽은 비대칭 트래픽으로 표시 되는이 놓습니다 hello 아웃 바운드 응답 따라서 방어 사이의 세 개 이상의 독립 층 권한이 없음/부적절 한 액세스를 방지 하는 클라우드 서비스를 통해 인터넷 및 AppVM01 hello 합니다.

#### <a name="denied-frontend-server-toobackend-server"></a>(거부 됨) 프런트 엔드 서버 tooBackend 서버
1. IIS01 보안이 손상 되 고 서버가 tooscan hello 백 엔드 서브넷을 시도 하는 악성 코드를 실행 중인 것으로 가정 합니다.
2. hello 프런트 엔드 서브넷 UDR 경로 hello 다음 홉으로 IIS01 toohello 방화벽에서 아웃 바운드 트래픽을 보낼 것입니다. 이것이 하 여 변경할 수 있는 hello VM을 노출 합니다.
3. hello 방화벽 hello 요청이 tooAppVM01, 또는 트래픽 수 tooFW 규칙 7-9) (인해 hello 방화벽에 의해 잠재적으로 허용 되는 DNS 조회에 대 한 DNS 서버 toohello 경우 hello 트래픽을 처리 합니다. 기타 트래픽은 FW 규칙 11(모두 거부)에서 차단합니다.
4. Hello 방화벽에서 이동 하는 위협 검색을 사용할 수 (이 문서에서는 다루지 않습니다, 고급 위협 기능이 특정 네트워크 장치에 대 한 hello 공급 업체 설명서를 참조)를 포함 하 여 전달 규칙 기본 hello에서 허용 되는 트래픽 이 항목에 설명 된 hello 트래픽 알려진된 서명이 나 고급 위협 규칙 플래그를 지정 하는 패턴을 포함 하는 경우 문서 되지 않을 수 있습니다.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(거부) DNS 서버에서 인터넷 DNS 조회
1. 인터넷 사용자가 toolookup BackEnd001.CloudApp.Net 서비스를 통해 DNS01에 내부 DNS 레코드 
2. DNS 트래픽에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스를 통과 하지는 및 hello 서버에 도달 하지 않습니다.
3. Hello hello 프런트 엔드 서브넷에 NSG 규칙 (블록 인터넷)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 인 경우
4. 마지막으로, hello 백 엔드 서브넷 UDR 경로 hello 다음 홉으로 DNS01 toohello 방화벽에서 모든 아웃 바운드 트래픽을 보내는 것과 및 hello 방화벽은 비대칭 트래픽으로 표시 되는이 놓습니다 hello 아웃 바운드 응답의 3 개 이상 독립적인 층 따라서 방어 hello 간의 인터넷 및 DNS01 권한이 없음/부적절 한 액세스를 방지 하는 클라우드 서비스를 통해 합니다.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(거부 됨) 방화벽을 통해 인터넷 tooSQL 액세스
1. 인터넷 사용자가 SecSvc001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 클라우드 서비스).
2. SQL에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 고 hello 방화벽에 도달 하지 않습니다.
3. 어떤 이유로 SQL 끝점 열려 있던 hello 방화벽 규칙을 처리를 시작 합니다.
   1. Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다
   2. FW 규칙 2-5 (RDP 규칙), 적용 하지 않는 toonext 규칙 이동
   3. FW 규칙 6 및 7 (응용 프로그램 규칙) 적용 안 함, toonext 규칙 이동
   4. Toonext 규칙 이동 FW 규칙 8 (tooInternet) 적용 되지 않습니다
   5. Toonext 규칙 이동 FW 규칙 9 (DNS)를 적용 하지 않습니다.
   6. Toonext 규칙 이동 FW 규칙 10 (내 서브넷) 적용 되지 않습니다
   7. FW 규칙 11(모두 거부)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.

## <a name="references"></a>참조
### <a name="main-script-and-network-config"></a>기본 스크립트 및 네트워크 구성
PowerShell 스크립트 파일에 hello 전체 스크립트를 저장 합니다. Hello 네트워크 구성 "NetworkConf2.xml" 라는 파일에 저장 합니다.
필요에 따라 hello 사용자 정의 변수를 수정 합니다. Hello 스크립트를 실행 한 다음 위의 hello 방화벽 규칙 설정 지침을 따릅니다.

#### <a name="full-script"></a>전체 스크립트
이 스크립트는 hello 사용자 정의 변수를 기반 합니다.

1. Tooan Azure 구독 연결
2. 새 저장소 계정 만들기
3. VNet을 새로 만들고 hello 네트워크 구성 파일에 정의 된 대로 세 개의 서브넷
4. 5개의 가상 머신(1개 방화벽, 4개 Windows Server VM)을 빌드합니다.
5. 다음을 포함하여 UDR을 구성합니다.
   1. 2개의 새 경로 테이블 만들기
   2. 경로 toohello 테이블 추가
   3. 바인딩할 테이블 tooappropriate 서브넷
6. IP 전달은 hello NVA에서 사용 하도록 설정
7. 다음을 포함하여 NSG를 구성합니다.
   1. NSG 만들기
   2. 규칙 추가
   3. 바인딩 hello NSG toohello 적절 한 서브넷

이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.

> [!IMPORTANT]
> 이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다. 빨간색 오류 메시지만 심각한 문제입니다.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>네트워크 구성 파일
업데이트 된 위치와이 xml 파일을 저장 하 고 hello 링크 toothis toohello $NetworkConfigFile 변수 위의 hello 스크립트에서 파일을 추가 합니다.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>샘플 응용 프로그램 스크립트
Hello 링크에 제공 된다는이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 원하면: [샘플 응용 프로그램 스크립트][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "NVA, NSG, UDR을 사용하는 양방향 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Hello 방화벽 규칙의 논리적 보기"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "프런트 엔드 네트워크 개체 만들기"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "DNS 서버 개체 만들기"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "기본 RDP 규칙의 복사본"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 규칙"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "응용 프로그램 리디렉션 아이콘"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "대상 NAT 아이콘"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "전달 아이콘"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "방화벽 관리 규칙"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "방화벽 RDP 규칙"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "방화벽 웹 규칙"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "방화벽 AppVM01 규칙"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "방화벽 아웃바운드 규칙"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "방화벽 DNS 규칙"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "VNet 내 방화벽 규칙"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "방화벽 거부 규칙"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "방화벽 규칙 활성화"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
