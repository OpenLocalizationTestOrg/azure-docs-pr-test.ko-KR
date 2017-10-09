---
title: "DMZ 예 – aaaAzure 빌드 Nsg와 단순 DMZ | Microsoft Docs"
description: "NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>예제 1 – 클래식 PowerShell로 NSG를 사용하여 간단한 DMZ 빌드
[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager 템플릿](virtual-networks-dmz-nsg.md)
> * [클래식 - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

이 예에서는 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 기본 DMZ를 만듭니다. 이 예에서는 각 hello 관련 PowerShell 명령 tooprovide 각 단계에 대 한 깊은 이해가 설명합니다. 이기도 한 트래픽 시나리오 섹션 tooprovide 심층 분석 하는 단계별 트래픽 hello 계층의 철저 한 방어 기능을 통해 진행 방법 hello DMZ 합니다. 마지막으로 hello references 섹션에는 전체 코드 hello 및 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다. 

![NSG와 인바운드 DMZ][1]

## <a name="environment-description"></a>환경 설명
이 예에서 구독 리소스를 다음 hello를 포함 되어 있습니다.

* 두 클라우드 서비스: "FrontEnd001" 및 "BackEnd001"
* "FrontEnd" 및 "BackEnd"의 두 서브넷을 포함하는 가상 네트워크 "CorpNetwork"
* 적용 된 tooboth 서브넷은 네트워크 보안 그룹
* 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
* 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
* DNS 서버("DNS01")를 나타내는 Windows Server

Hello references 섹션에는 PowerShell 스크립트의이 예제에서 설명 하는 hello 환경 대부분 있습니다. 건물 hello Vm 및 가상 네트워크를 hello 예제 스크립트에 의해 수행 하지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다. 

toobuild hello 환경

1. Hello 네트워크 구성 xml 파일 (이름, 위치 및 IP 주소 toomatch hello 주어진 시나리오에 업데이트) hello references 섹션에 포함 된 저장
2. Hello 스크립트 toomatch hello 환경 hello 스크립트의 update hello 사용자 변수는 toobe (구독, 서비스 이름 등)에 대해 실행
3. PowerShell에서 hello 스크립트를 실행 합니다.

>[!Note]
>hello PowerShell 스크립트에서에서 표시 하는 hello 지역 hello 네트워크 구성 xml 파일에서 표시 하는 hello 지역을 일치 해야 합니다.
>
>

Hello 스크립트 실행이 성공적으로 추가 되 면 선택적 단계를 수행 합니다, 그리고 hello references 섹션에는 두 개의 스크립트 tooset hello 웹 서버와이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 응용 프로그램 서버.

hello 다음 섹션에서는 네트워크 보안 그룹 및이 예제에 대 한 키 줄의 hello PowerShell 스크립트를 통해 탐색 하 여 작동 방식을 자세히 설명 합니다.

## <a name="network-security-groups-nsg"></a>네트워크 보안 그룹(NSG)
이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다. 

> [!TIP]
> 일반적으로 특정 "Allow" 규칙을 먼저 만든 하 고 보다 일반적인 "거부" 규칙을 마지막 hello 안됩니다. 우선 순위가 할당 된 hello는 규칙이 먼저 평가 결정 합니다. 트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다. NSG 규칙의 hello에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향입니다.
> 
> 

선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:

1. 내부 DNS 트래픽(포트 53) 허용됨
2. RDP 트래픽 (포트 3389 hello 인터넷 tooany VM에서 에서) 허용 됩니다.
3. Hello 인터넷 tooweb 서버 (IIS01)에서 HTTP 트래픽 (포트 80)가 허용
4. (모든 포트) IIS01 tooAppVM1에서 모든 트래픽을 허용합니다
5. 전체 VNet (두 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)
6. Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.

이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청 hello 인터넷 toohello 웹 서버 로부터 언바운드 하지 않은 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것을 히 규칙 3 보다 우선 순위가 규칙 5는 하지 고려해 야 하 고 적용 됩니다. 따라서 toohello 웹 서버 hello HTTP 요청 허용 합니다. 동일한 트래픽이 해당 tooreach hello DNS01 서버를 시도 하 고, 규칙 5 (거부) hello 첫 번째 tooapply 및 hello 트래픽 toopass toohello 서버 허용 되지 않는 것입니다. 규칙 6 (거부) hello 프런트 엔드 서브넷 통하게 (규칙 1 및 4에서에서 허용 된 트래픽)를 제외한 toohello 백 엔드 서브넷의 차단,이 규칙 집합 hello 백 엔드 네트워크를 보호는 공격자가 손상 hello에서 웹 응용 프로그램 hello 프런트 엔드, hello 공격자가 경우 백 엔드 "보호" (만 hello AppVM01 서버에서 노출 tooresources) 네트워크 액세스 toohello를 제한 됩니다.

Toohello 아웃 트래픽을 허용 하는 기본 아웃 바운드 규칙이 인터넷 합니다. 이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다. 양방향에서 트래픽 아래로 toolock, 사용자 정의 된 라우팅 필수 이며 hello에 "예 3"에 대해서는 [보안 경계 모범 사례 페이지][HOME]합니다.

다음과 같이 각 규칙에서 자세히 설명 되어 (**참고**: hello 달러 기호로 시작 하는 목록 다음의 모든 항목 (예: $NSGName)는이 문서의 hello 참조 섹션에 hello 스크립트에서 사용자 정의 변수):

1. 먼저 네트워크 보안 그룹 toohold hello 규칙 작성 해야 합니다.

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. 이 예에서 첫 번째 규칙 hello hello 백 엔드 서브넷에 있는 모든 내부 네트워크 toohello DNS 서버 간의 DNS 트래픽을 허용합니다. hello 규칙에 몇 가지 중요 한 매개 변수:
   
   * "Type"은 이 규칙이 적용되는 트래픽 흐름의 방향을 나타냅니다. hello 방향은 (에 따라이 NSG 바인딩되는) hello 서브넷 또는 가상 컴퓨터의 hello 관점에서입니다. 따라서 경우 형식이 "Inbound" 및 트래픽 hello 서브넷을 시작 하는, hello 규칙이 적용 되 고이 규칙에 의해 내보내는 hello 서브넷을 받지 않습니다.
   * "Priority" 트래픽 흐름을 확인 하는 hello 순서를 설정 합니다. hello 낮은 hello 숫자 hello 더 높은 hello 우선 순위입니다. Tooa 특정 트래픽 흐름을 적용 하는 규칙을 더 이상 규칙이 처리 됩니다. 따라서 우선 순위 1의 규칙이 트래픽이 우선 순위가 2 인 규칙 트래픽을, 거부 및 규칙이 모두 적용 tootraffic 경우 hello 트래픽 tooflow 것은 허용 (규칙 1 한 우선 순위가 높은 이후 효과 데 걸린 및 적용 된 규칙이 더 이상 없음).
   * "Action"은 이 규칙의 영향을 받는 트래픽을 차단하거나 허용할지를 나타냅니다.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. 이 규칙은 모든 서버 hello에 hello toohello RDP 포트를 인터넷에서 RDP 트래픽 tooflow 바인딩된 서브넷 허용 됩니다. 이 규칙은 "VIRTUAL_NETWORK" 및 "INTERNET"이라는 두 가지 특별한 주소 접두사 형식을 사용합니다. 이러한 태그는 쉽게 tooaddress 주소 접두사의 더 큰 범주입니다.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. 이 규칙은 toohit hello 웹 서버에 대 한 인바운드의 인터넷 트래픽을 허용 합니다. 이 규칙 hello 라우팅 동작을 변경 하지 않습니다. hello 규칙 IIS01 toopass 향하는 트래픽을 허용 합니다. 따라서이 규칙은 허용 하 고 규칙은 추가 처리를 중지 대상으로 hello 인터넷 트래픽만 hello 웹 서버를 갖는 경우입니다. (우선 순위에서 hello 규칙에 140 모든 다른 인바운드 인터넷 트래픽을 차단). 이 규칙 HTTP 트래픽을 처리 하는 경우 추가 될 수 제한 tooonly 대상 포트 80을 허용 합니다.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. 이 규칙은 toohello AppVM01 서버 트래픽을 toopass hello IIS01 서버에서 허용, 이후 규칙은 다른 모든 프런트 엔드 tooBackend 트래픽을 차단 합니다. tooimprove hello 포트를 식별 하는 경우이 규칙을 추가 해야 합니다. 예를 들어 hello IIS 서버 AppVM01에 SQL Server 작업 부하는 hello 대상 포트 범위 변경 해야에서 "*" (모두) too1433 (hello SQL 포트) 되므로 AppVM01에서 더 작은 인바운드 공격 노출 해야 hello 웹 응용 프로그램 적이 손상 될 수 있습니다.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. 이 규칙 hello 인터넷 tooany 서버 hello 네트워크에서에서 트래픽을 거부합니다. 110 및 120 우선 순위에서 hello 규칙을 사용 hello 효과 tooallow만 인바운드 인터넷 트래픽 toohello 방화벽 및 서버 모두에서 RDP 포트 이며 다른 모든 것을 차단 합니다. 이 규칙은 "유사시 대기" 규칙 tooblock 모든 예기치 않은 흐름.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. hello 최종 규칙 hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 트래픽을 거부합니다. 이 규칙에만 인바운드 규칙 이므로 (hello 백 엔드 toohello 프런트 엔드)에서 역방향 트래픽이 허용 됩니다.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>트래픽 시나리오
#### <a name="allowed-internet-tooweb-server"></a>(*허용*) 인터넷 tooweb 서버
1. 인터넷 사용자가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 연결 클라우드 서비스).
2. 서비스 전달 트래픽을 IIS01 쪽으로 포트 80에 대 한 열린 끝점을 통해 클라우드 (hello 웹 서버)
3. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리
4. 트래픽 (10.0.1.5) hello 웹 서버의 IIS01 내부 IP 주소에 도달
5. IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다
6. IIS01 정보 AppVM01에 SQL Server hello를 요청
7. 프런트 엔드 서브넷에 아웃바운드 규칙이 없으므로 트래픽이 허용됩니다.
8. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다
   4. NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리
9. AppVM01 hello SQL 쿼리를 받아 응답
10. Hello 응답이 허용 hello 백 엔드 서브넷에 없는 아웃 바운드 규칙이 있을 경우
11. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
    1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
    2. 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.
12. hello IIS 서버 hello SQL 응답을 수신 하 고 hello HTTP 응답을 완료 및 toohello 요청자에 게 보냅니다.
13. 아웃 바운드 규칙 hello 프런트 엔드 서브넷에 있기 때문 hello 응답 허용 되 고 hello 인터넷 사용자에 게 요청 된 hello 웹 페이지입니다.

#### <a name="allowed-rdp-toobackend"></a>(*허용*) RDP toobackend
1. 인터넷에서 서버 관리자 요청 BackEnd001.CloudApp.Net:xxxxx 여기서 xxxxx는 RDP tooAppVM01 hello 임의로 할당 된 포트 번호에서 RDP 세션 tooAppVM01 (hello 할당 된 포트를 찾을 수 hello Azure 포털에서 또는 PowerShell을 통해)
2. 백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.
3. 아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.
4. RDP 세션이 사용하도록 설정됩니다.
5. Hello 사용자 이름 및 암호에 대 한 AppVM01 프롬프트

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*허용*) DNS 서버에서 웹 서버 DNS 조회
1. 웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.
2. hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01
3. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
4. 백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.
   * NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.
5. DNS 서버 hello 요청 수신
6. DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷
7. 백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
8. 이 세션은 내부적으로 시작 된 이후 인터넷 DNS 서버 응답을 hello 응답이 허용
9. DNS 서버 hello 응답을 캐시 및 toohello 초기 요청 백 tooIIS01 이벤트에 응답
10. 백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
11. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
    1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
    2. hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용
12. IIS01은 DNS01에서 hello 응답을 받습니다.

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*허용*) AppVM01에서 웹 서버가 파일 액세스
1. IIS01은 AppVM01에서 파일을 요청합니다.
2. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
3. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooIIS01) 적용 되지 않습니다
   4. NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리
4. AppVM01은 hello 요청을 받아 파일 (액세스 권한이 부여 가정)를 사용 하 여 응답
5. Hello 응답이 허용 hello 백 엔드 서브넷에 없는 아웃 바운드 규칙이 있을 경우
6. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
   1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
   2. 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.
7. hello IIS 서버 hello 파일 수신

#### <a name="denied-web-toobackend-server"></a>(*Denied*) 웹 toobackend 서버
1. 인터넷 사용자가 tooaccess hello BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에 있는 파일
2. 파일 공유에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 트래픽과 hello 서버에 도달 하지 않습니다.
3. NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 인 경우

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*거부*) DNS 서버에서 웹 DNS 조회
1. 인터넷 사용자 시도 하는 hello BackEnd001.CloudApp.Net 서비스를 통해 DNS01에 내부 DNS 레코드를 toolook
2. DNS에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 트래픽과 hello 서버에 도달 하지 않습니다.
3. NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 있던 경우 (참고: 규칙 1 (DNS) 같은 두 가지 이유로 적용 되지 않습니다, 첫 번째 hello 소스 주소는 인터넷을 hello,이 규칙은 toohello 적용 됩니다. 또한 지역 VNet으로 hello 원본 이 규칙 허용 규칙 이므로 트래픽을 거부 하지 않습니다 것)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Denied*) 웹 방화벽을 통해 tooSQL 액세스
1. 인터넷 사용자가 FrontEnd001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 연결 클라우드 서비스).
2. SQL에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 트래픽과 hello 방화벽에 도달 하지 않습니다.
3. 어떤 이유로 끝점 열려 있던 hello 프런트 엔드 서브넷 인바운드 규칙 처리를 시작 합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리
4. 트래픽 (10.0.1.5) hello IIS01의 내부 IP 주소에 도달
5. IIS01 하지 않게 응답 toohello 요청 포트 1433에서 수신 되지 않습니다.

## <a name="conclusion"></a>결론
이 예제는 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 쉽고 명확한 방법.

네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.

## <a name="references"></a>참조
### <a name="main-script-and-network-config"></a>기본 스크립트 및 네트워크 구성
PowerShell 스크립트 파일에 hello 전체 스크립트를 저장 합니다. Hello 네트워크 구성 "NetworkConf1.xml." 라는 파일에 저장 합니다.
필요 하 고 실행할 hello 스크립트로 hello 사용자 정의 변수를 수정 합니다.

#### <a name="full-script"></a>전체 스크립트
이 스크립트는 사용자 정의 변수를 hello; 기반

1. Tooan Azure 구독 연결
2. 저장소 계정 만들기
3. VNet 및 hello 네트워크 구성 파일에 정의 된 대로 두 서브넷 만들기
4. 4개의 Windows Server VM 빌드
5. 다음을 포함하여 NSG를 구성합니다.
   * NSG 만들기
   * 규칙으로 채우기
   * 바인딩 hello NSG toohello 적절 한 서브넷

이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.

> [!IMPORTANT]
> 이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다. 빨간색 오류 메시지만 심각한 문제입니다.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>네트워크 구성 파일
업데이트 된 위치와이 xml 파일을 저장 하 고 hello 스크립트 앞에 hello 링크 toothis 파일 toohello $NetworkConfigFile 변수를 추가 합니다.

```XML
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
```

#### <a name="sample-application-scripts"></a>샘플 응용 프로그램 스크립트
Hello 링크에 제공 된다는이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 원하면: [샘플 응용 프로그램 스크립트][SampleApp]

## <a name="next-steps"></a>다음 단계
* 업데이트 및 XML 파일 저장
* Hello PowerShell 스크립트 toobuild hello 환경 실행
* Hello 샘플 응용 프로그램 설치
* 이 DMZ를 통해 다양한 트래픽 흐름 테스트

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "NSG와 인바운드 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

