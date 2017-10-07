---
title: "DMZ 예 – aaaAzure 빌드 Nsg와 단순 DMZ | Microsoft Docs"
description: "NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>예 1 – Azure Resource Manager 템플릿으로 NSG를 사용하여 간단한 DMZ 빌드
[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager 템플릿](virtual-networks-dmz-nsg.md)
> * [클래식 - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

이 예에서는 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 기본 DMZ를 만듭니다. 이 예에서는 각 hello 관련 템플릿 섹션 tooprovide 각 단계에 대 한 깊은 이해가 설명합니다. 이기도 트래픽 시나리오 섹션 tooprovide 단계별 자세히 배우려면 hello DMZ에에서는 심층적인 방어의 hello 계층을 통해 트래픽을 처리할 방법을 합니다. 마지막으로 hello references 섹션에는 hello 완전 한 템플릿 코드와 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![NSG와 인바운드 DMZ][1]

## <a name="environment-description"></a>환경 설명
이 예에서 구독 리소스를 다음 hello를 포함 되어 있습니다.

* 단일 리소스 그룹
* 두 서브넷 “프런트 엔드” 및 “백 엔드”를 사용하는 가상 네트워크
* 적용 된 tooboth 서브넷은 네트워크 보안 그룹
* 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
* 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
* DNS 서버("DNS01")를 나타내는 Windows Server
* Hello 응용 프로그램 웹 서버와 관련 된 공용 IP 주소

Hello references 섹션에는이 예제에서 설명 하는 hello 환경 구축 하 링크 tooan Azure 리소스 관리자 템플릿입니다. 건물 hello Vm 및 가상 네트워크를 hello 예제 서식 파일에서 수행 되지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다. 

**toobuild이이 환경** (자세한 지침은이 문서의 hello references 섹션에는);

1. 배포 시 Azure 리소스 관리자 템플릿을 hello: [Azure 빠른 시작 템플릿][Template]
2. 시 hello 샘플 응용 프로그램 설치: [샘플 응용 프로그램 스크립트][SampleApp]

>[!NOTE]
>이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다. 첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다. 또는 공용 IP는 보다 쉬운 RDP를 위해 각 서버 NIC와 연결할 수 있습니다.
> 
>

hello 다음 섹션에서는 hello 네트워크 보안 그룹 및 Azure 리소스 관리자 템플릿을 hello 키 줄을 살펴보는 방법으로이 예제에 대 한 작동 방식이 자세히 설명 합니다.

## <a name="network-security-groups-nsg"></a>네트워크 보안 그룹(NSG)
이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다. 

>[!TIP]
>일반적으로 특정 "Allow" 규칙을 먼저 만든 하 고 보다 일반적인 "거부" 규칙을 마지막 hello 안됩니다. 우선 순위가 할당 된 hello는 규칙이 먼저 평가 결정 합니다. 트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다. NSG 규칙의 hello에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향입니다.
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

Toohello 아웃 트래픽을 허용 하는 기본 아웃 바운드 규칙이 인터넷 합니다. 이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다. 양방향에서 tooapply 보안 정책 tootraffic, 사용자 정의 된 라우팅 필수 이며 hello에 "예 3"에 대해서는 [보안 경계 모범 사례 페이지][HOME]합니다.

각 규칙은 다음과 같이 더 자세히 설명되어 있습니다.

1. 네트워크 보안 그룹 리소스 인스턴스화된 toohold hello 규칙 해야 합니다.

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. 이 예에서 첫 번째 규칙 hello hello 백 엔드 서브넷에 있는 모든 내부 네트워크 toohello DNS 서버 간의 DNS 트래픽을 허용합니다. hello 규칙에 몇 가지 중요 한 매개 변수:
  * 이러한 태그는 쉽게 tooaddress 주소 접두사의 더 큰 범주를 허용 하는 시스템 제공 식별자를 "destinationAddressPrefix"-규칙 주소 접두사 "기본 태그" 라는 특수 한 유형의 사용할 수 있습니다. 이 규칙을 사용 하 여 기본 태그 "Internet" hello toosignify hello VNet 외부에서 모두 해결 합니다. 다른 접두사 레이블은 VirtualNetwork 및 AzureLoadBalancer입니다.
  * "Direction"은 이 규칙이 적용되는 트래픽 흐름의 방향을 나타냅니다. hello 방향은 (에 따라이 NSG 바인딩되는) hello 서브넷 또는 가상 컴퓨터의 hello 관점에서입니다. 따라서 경우 방향은 "Inbound" 및 트래픽 hello 서브넷을 시작 하는, hello 규칙 적용 및이 규칙에 의해 내보내는 hello 서브넷을 받지 않습니다.
  * "Priority" 트래픽 흐름을 확인 하는 hello 순서를 설정 합니다. hello 낮은 hello 숫자 hello 더 높은 hello 우선 순위입니다. Tooa 특정 트래픽 흐름을 적용 하는 규칙을 더 이상 규칙이 처리 됩니다. 따라서 우선 순위 1의 규칙이 트래픽이 우선 순위가 2 인 규칙 트래픽을, 거부 및 규칙이 모두 적용 tootraffic 경우 hello 트래픽 tooflow 것은 허용 (규칙 1 한 우선 순위가 높은 이후 효과 데 걸린 및 적용 된 규칙이 더 이상 없음).
  * "Access"는 이 규칙의 영향을 받는 트래픽을 차단("Deny")하거나 허용("Allow")할지를 나타냅니다.

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. 이 규칙은 모든 서버 hello에 hello toohello RDP 포트를 인터넷에서 RDP 트래픽 tooflow 바인딩된 서브넷 허용 됩니다. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. 이 규칙은 toohit hello 웹 서버에 대 한 인바운드의 인터넷 트래픽을 허용 합니다. 이 규칙 hello 라우팅 동작을 변경 하지 않습니다. hello 규칙 IIS01 toopass 향하는 트래픽을 허용 합니다. 따라서이 규칙은 허용 하 고 규칙은 추가 처리를 중지 대상으로 hello 인터넷 트래픽만 hello 웹 서버를 갖는 경우입니다. (우선 순위에서 hello 규칙에 140 모든 다른 인바운드 인터넷 트래픽을 차단). 이 규칙 HTTP 트래픽을 처리 하는 경우 추가 될 수 제한 tooonly 대상 포트 80을 허용 합니다.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. 이 규칙은 toohello AppVM01 서버 트래픽을 toopass hello IIS01 서버에서 허용, 이후 규칙은 다른 모든 프런트 엔드 tooBackend 트래픽을 차단 합니다. tooimprove hello 포트를 식별 하는 경우이 규칙을 추가 해야 합니다. 예를 들어 hello IIS 서버 AppVM01에 SQL Server 작업 부하는 hello 대상 포트 범위 변경 해야에서 "*" (모두) too1433 (hello SQL 포트) 되므로 AppVM01에서 더 작은 인바운드 공격 노출 해야 hello 웹 응용 프로그램 적이 손상 될 수 있습니다.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. 이 규칙 hello 인터넷 tooany 서버 hello 네트워크에서에서 트래픽을 거부합니다. 110 및 120 우선 순위에서 hello 규칙을 사용 hello 효과 tooallow만 인바운드 인터넷 트래픽 toohello 방화벽 및 서버 모두에서 RDP 포트 이며 다른 모든 것을 차단 합니다. 이 규칙은 "유사시 대기" 규칙 tooblock 모든 예기치 않은 흐름.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. hello 최종 규칙 hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 트래픽을 거부합니다. 이 규칙에만 인바운드 규칙 이므로 (hello 백 엔드 toohello 프런트 엔드)에서 역방향 트래픽이 허용 됩니다.

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>트래픽 시나리오
#### <a name="allowed-internet-tooweb-server"></a>(*허용*) 인터넷 tooweb 서버
1. 인터넷 사용자 hello hello IIS01 NIC와 관련 된 NIC의 hello 공용 IP 주소에서 HTTP 페이지 요청
2. 공용 IP 주소 hello 전달 트래픽 toohello IIS01 쪽으로 VNet (hello 웹 서버)
3. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
  1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
  2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
  3. NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리
4. 트래픽 (10.0.1.5) hello 웹 서버의 IIS01 내부 IP 주소에 도달
5. IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다
6. IIS01 정보 AppVM01에 SQL Server hello를 요청
7. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
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
12. hello IIS 서버 hello SQL 응답 및 hello HTTP 응답을 완료를 주고받는 toohello 요청자
13. Hello 프런트 엔드 서브넷에 아웃 바운드 규칙이 있기 때문에 hello 응답이 허용 하 고 hello 인터넷 사용자 hello 웹 페이지 요청을 받습니다.

#### <a name="allowed-rdp-tooiis-server"></a>(*허용*) RDP tooIIS 서버
1. 인터넷에서 서버 관리자는 RDP 세션 tooIIS01 hello hello IIS01 NIC (이 공용 IP 주소 hello 포털 또는 PowerShell을 통해 찾을 수 있습니다)와 연결 된 NIC는 hello 공용 IP 주소에서 요청
2. 공용 IP 주소 hello 전달 트래픽 toohello IIS01 쪽으로 VNet (hello 웹 서버)
3. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
  1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
  2. NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.
4. 아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.
5. RDP 세션이 사용하도록 설정됩니다.
6. Hello 사용자 이름 및 암호에 대 한 IIS01 프롬프트

>[!NOTE]
>이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다. 첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.
>
>

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

#### <a name="denied-rdp-toobackend"></a>(*Denied*) RDP toobackend
1. 인터넷 사용자가 tooRDP tooserver AppVM01
2. 이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.
3. 그러나 어떤 이유로 공용 IP 주소가 활성화된 경우 NSG 규칙 2(RP)는 이 트래픽을 허용합니다.

>[!NOTE]
>이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다. 첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Denied*) 웹 toobackend 서버
1. 인터넷 사용자가 tooaccess AppVM01에 있는 파일
2. 이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.
3. NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 공용 IP 주소를 사용 하는 경우

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*거부*) DNS 서버에서 웹 DNS 조회
1. 인터넷 사용자가 toolook DNS01에는 내부 DNS 레코드를
2. 이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.
3. NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 공용 IP 주소를 사용 하는 경우 (참고: 인터넷 hello 및 toohello 규칙 1에만 적용 됩니다는 규칙 1 (DNS) hello 소스 주소를 요청 하기 때문에 적용 되지 않습니다 hello 소스로 지역 VNet)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Denied*) hello 웹 서버에 대 한 SQL 액세스
1. 인터넷 사용자가 IIS01에서 SQL 데이터를 요청합니다.
2. 이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.
3. 몇 가지 이유로 공용 IP 주소를 사용 하는 경우 hello 프런트 엔드 서브넷 인바운드 규칙 처리를 시작 합니다.
  1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
  2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
  3. NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리
4. 트래픽 (10.0.1.5) hello IIS01의 내부 IP 주소에 도달
5. IIS01 하지 않게 응답 toohello 요청 포트 1433에서 수신 되지 않습니다.

## <a name="conclusion"></a>결론
이 예제는 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 쉽고 명확한 방법.

네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.

## <a name="references"></a>참조
### <a name="azure-resource-manager-template"></a>Azure Resource Manager 템플릿
이 예제는 Microsoft에서 관리 하는 GitHub 리포지토리에 미리 정의 된 Azure 리소스 관리자 템플릿을 사용 하 고 toohello 커뮤니티를 엽니다. 이 템플릿은 GitHub에서 배포할 수 있습니다 또는 다운로드 하 고 toofit 요구에 맞게 수정 합니다. 

hello 기본 서식 파일은 "azuredeploy.json." 라는 hello 파일에 이 서식 파일 (hello 관련된 "azuredeploy.parameters.json" 파일)와 PowerShell 또는 CLI를 통해 제출할 수 toodeploy이 서식이 파일입니다. I 찾을 hello 가장 쉬운 방법은 toouse hello GitHub에서 hello README.md 페이지에서 "배포 tooAzure" 단추 합니다.

toodeploy hello 템플릿을 GitHub 및 hello Azure 포털에서이 예제를 작성 하는 다음이 단계를 따르십시오.

1. 브라우저에서 탐색 toohello [서식 파일][Template]
2. Hello "배포 tooAzure" 단추 (또는 hello "시각화" 단추 toosee이 서식이 파일의 그래픽 표현)를 클릭 합니다.
3. Hello 매개 변수 블레이드에서 hello 저장소 계정, 사용자 이름 및 암호를 입력 한 다음 클릭 **확인**
5. 이 배포에 대한 리소스 그룹을 만듭니다.(기존 것을 사용할 수 있지만 최상의 결과를 위해 새 것을 권장합니다.)
6. 필요한 경우 VNet에 대 한 hello 구독 및 위치 설정을 변경 합니다.
7. 클릭 **약관을 검토**hello 조건을 읽고 클릭 **구매** tooagree 합니다.
8. 클릭 **만들기** 이 서식 파일의 toobegin hello 배포 합니다.
9. Hello 배포 성공적으로 완료 되 면 리소스 그룹 내에 구성할이 배포 toosee hello 리소스에 대해 생성 toohello를 이동 합니다.

>[!NOTE]
>이 템플릿을 사용 하 여 RDP toohello IIS01 서버만 (찾기 hello IIS01에 대 한 공용 IP hello 포털에). 이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다. 첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.
>
>

tooremove 배포, delete hello이 리소스 그룹 및 모든 자식 리소스가 삭제 됩니다.

#### <a name="sample-application-scripts"></a>샘플 응용 프로그램 스크립트
Hello 템플릿을 성공적으로 실행 되 면이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 hello 웹 서버 및 응용 프로그램 서버를 설정할 수 있습니다. 이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 제공 된다는 링크 hello에: [샘플 응용 프로그램 스크립트][SampleApp]

## <a name="next-steps"></a>다음 단계

* 이 예제 배포
* Hello 샘플 응용 프로그램 빌드
* 이 DMZ를 통해 다양한 트래픽 흐름 테스트

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "NSG와 인바운드 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md