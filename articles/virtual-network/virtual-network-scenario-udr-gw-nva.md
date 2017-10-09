---
title: "2 계층 응용 프로그램과 aaaHybrid 연결 | Microsoft Docs"
description: "자세한 내용은 방법 toodeploy UDR toocreate Azure의 다중 계층 응용 프로그램 환경 및 가상 어플라이언스"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>가상 어플라이언스 시나리오
더 큰 Azure 고객 간의 일반적인 시나리오는 온-프레미스 데이터 센터에서 toohello 백 계층 액세스를 허용 하면서 hello 필요 tooprovide 노출 된 2 계층 응용 프로그램 toohello 인터넷입니다. 이 문서는 사용자 정의 경로 (UDR), VPN 게이트웨이 및 네트워크 가상 어플라이언스 toodeploy를 사용 하 여 시나리오를 통해 hello 요구 사항을 준수를 충족 하는 2 계층 환경:

* 웹 응용 프로그램에서 액세스할 수 있어야 hello 공용 인터넷만 합니다.
* 웹 서버 호스팅 hello 응용 프로그램 수 tooaccess 백 엔드 응용 프로그램 서버 여야 합니다.
* Hello 인터넷 toohello 웹 응용 프로그램의에서 모든 트래픽이 방화벽 가상 어플라이언스를 통해 이동 해야 합니다. 이 가상 어플라이언스는 인터넷 트래픽에 대해서만 사용됩니다.
* 모든 트래픽이 toohello 응용 프로그램 서버는 방화벽 가상 어플라이언스를 통해 이동 해야 합니다. 이 가상 어플라이언스에 액세스 toohello 백 엔드 서버 및 VPN 게이트웨이 통해 hello 온-프레미스 네트워크에서 들어오는 액세스에 대 한 사용 됩니다.
* 사용 하 여 세 번째는 관리 목적을 위해 배타적으로 사용 되는 가상 어플라이언스를 방화벽을 관리자가 자신의 온-프레미스 컴퓨터에서 수 toomanage hello 방화벽 가상 어플라이언스를 여야 합니다.

이는 DMZ 및 보호된 네트워크를 사용한 표준 DMZ 시나리오입니다. NSG, 방화벽 가상 어플라이언스 또는 둘의 조합을 사용하여 Azure에서 이러한 시나리오를 생성할 수 있습니다. hello 표에서 hello 장점 및 단점 Nsg 사이의 방화벽 가상 어플라이언스의 일부를 보여 줍니다.

|  | 장점 | 단점 |
| --- | --- | --- |
| NSG |무료입니다. <br/>Azure RBAC에 통합됩니다. <br/>ARM 템플릿에서 규칙을 만들 수 있습니다. |대규모 환경에서 복잡성이 달라질 수 있습니다. |
| 방화벽 |데이터 평면을 완벽히 제어합니다. <br/>방화벽 콘솔을 통해 중앙에서 관리합니다. |방화벽 어플라이언스의 비용이 듭니다. <br/>Azure RBAC와 통합되지 않습니다. |

hello 솔루션 아래 방화벽 가상 어플라이언스 tooimplement DMZ/보호 네트워크 시나리오를 사용합니다.

## <a name="considerations"></a>고려 사항
오늘, 다음과 같이 사용할 수 있는 다양 한 기능을 사용 하 여 Azure에서 위에서 설명한 hello 환경에 배포할 수 있습니다.

* **가상 네트워크(VNet)**. Azure VNet 비슷한 방식으로 tooan 온-프레미스 네트워크 내에서 작동 하 고 하나 이상의 서브넷 tooprovide 트래픽 격리 및 문제의 분리로 나눌 수 있습니다.
* **가상 어플라이언스**. 여러 파트너 hello 위에서 설명한 hello 3 개의 방화벽에 사용할 수 있는 Azure Marketplace의에서 가상 어플라이언스를 제공 합니다. 
* **UDR(사용자 정의 경로)**. 경로 테이블 UDRs Azure 네트워킹 toocontrol hello 패킷 흐름이 VNet 내에서 사용 하는 포함 될 수 있습니다. 이러한 경로 테이블에 적용 된 toosubnets 수 있습니다. Azure의 hello 최신 기능 중 하나에 hello 기능 tooapply 경로 테이블 toohello hello 기능 tooforward hello Azure VNet으로 하이브리드 연결 tooa 가상 기기에서 들어오는 모든 트래픽을 제공 GatewaySubnet입니다.
* **IP 전달**. 기본적으로 Azure 네트워킹 엔진 hello 패킷을 전달할 toovirtual 네트워크 인터페이스 카드 (Nic) hello 패킷의 대상 IP 주소 hello NIC IP 주소와 일치 하는 경우에입니다. 따라서 한 UDR 패킷을 보내야 한다고 가상 어플라이언스를 제공 하는 tooa 정의 Azure 네트워킹 엔진 hello 패킷이 마 합니다. tooensure hello 패킷 배달 tooa hello 패킷에 대 한 실제 대상 hello 없는에 (이 경우 가상 어플라이언스) VM 가상 어플라이언스 hello에 대 한 IP 전달 tooenable를 해야 합니다.
* **NSG(네트워크 보안 그룹)**. 아래 예제에서는 hello는의 Nsg를 사용 하 여 수행 하는이 솔루션 toofurther hello 트래픽을 필터링 및 해당 서브넷과 Nic에 적용할 Nsg toohello 서브넷 및/또는 Nic를 사용할 수 있습니다.

![IPv6 연결](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

이 예제는 hello 다음을 포함 하는 구독:

* 2 리소스 그룹을 hello 다이어그램에 표시 되지 않습니다. 
  * **ONPREMRG**. 모든 리소스 필요한 toosimulate 온-프레미스 네트워크를 포함합니다.
  * **AZURERG**. Hello Azure 가상 네트워크 환경에 필요한 모든 리소스를 포함 합니다. 
* 명명 된 VNet **onpremvnet** toomimic 아래와 같은 온-프레미스 데이터 센터는 분할을 사용 합니다.
  * **onpremsn1**. Ubuntu toomimic 온-프레미스 서버를 실행 하는 가상 컴퓨터 (VM)를 포함 하는 서브넷입니다.
  * **onpremsn2**. Ubuntu toomimic 관리자에서 사용 되는 온-프레미스 컴퓨터를 실행 하는 VM을 포함 하는 서브넷입니다.
* 라는 하나의 방화벽 가상 어플라이언스는 **OPFW** 에 **onpremvnet** toomaintain 터널 너무 사용**azurevnet**합니다.
* 아래 나열된 대로 분할된 **azurevnet** 이라는 VNet
  * **azsn1**. 외부 방화벽 서브넷 hello 외부 방화벽에 독점적으로 사용 합니다. 모든 인터넷 트래픽이 이 서브넷을 통해 들어옵니다. 이 서브넷이 NIC 연결 toohello 외부 방화벽을 포함 해야 합니다.
  * **azsn2**. Hello 인터넷에서에서 액세스할 수 있는 웹 서버로 실행 하는 VM을 호스팅하는 프런트 엔드 서브넷입니다.
  * **azsn3**. Hello 프런트 엔드 웹 서버에서 액세스할 수 있는 백 엔드 응용 프로그램 서버를 실행 하는 VM을 호스팅하는 백 엔드 서브넷입니다.
  * **azsn4**. 관리 서브넷만 tooprovide 관리 액세스 tooall 방화벽 가상 어플라이언스를 사용 합니다. 이 서브넷만 hello 솔루션에서 사용 되는 각 방화벽 가상 어플라이언스에는 NIC를 포함 합니다.
  * **GatewaySubnet**. Azure Vnet 및 다른 네트워크 간의 VPN 게이트웨이 및 express 경로 tooprovide 연결에 필요한 azure 하이브리드 연결 서브넷입니다. 
* Hello에 방화벽 가상 어플라이언스 3 가지 **azurevnet** 네트워크입니다. 
  * **AZF1**. 노출 된 외부 방화벽 toohello Azure에서 공용 IP 주소 리소스를 사용 하 여 공용 인터넷 합니다. 사용자에 게 템플릿이 hello Marketplace 또는 해당 프로 비전 기기 공급 업체에서 직접 3-NIC 가상 어플라이언스 tooensure가 필요 합니다.
  * **AZF2**. 내부 방화벽 간의 트래픽을 toocontrol 사용 **azsn2** 및 **azsn3**합니다. 또한 3-NIC 가상 어플라이언스입니다.
  * **AZF3**. 방화벽 관리 hello에서 액세스할 수 있는 tooadministrators 온-프레미스 데이터 센터 및 연결 된 tooa 관리 서브넷 toomanage 모든 방화벽 어플라이언스를 사용 합니다. Hello Marketplace에서에서 2-NIC는 가상 어플라이언스 템플릿이 하거나 기기 공급 업체에서 직접 요청할 수 있습니다.

## <a name="user-defined-routing-udr"></a>UDR(사용자 정의 라우팅)
각 Azure 서브넷에에서 연결 된 tooa UDR 사용 되는 테이블 toodefine 해당 서브넷에서 시작 된 트래픽의 경우 라우팅됩니다 어떻게 될 수 있습니다. 없는 UDRs 정의 된 경우 Azure 서브넷 tooanother 하나에서 기본 경로 tooallow 트래픽 tooflow를 사용 합니다. toobetter UDRs 이해, 방문 [사용자 정의 경로 및 IP 전달](virtual-networks-udr-overview.md#ip-forwarding)합니다.

tooensure 통신 hello 마지막 요구 사항을 위의 기반 hello 적절 한 방화벽 어플라이언스를 통해 수행 됩니다, toocreate hello 다음 필요한 UDRs에 포함 된 경로 테이블 **azurevnet**합니다.

### <a name="azgwudr"></a>azgwudr
이 시나리오에서는 트래픽 흐름에서 온-프레미스 tooAzure 너무 연결 하 여 사용 되는 toomanage hello 방화벽 수 hello**AZF3**, 트래픽이 hello 내부 방화벽을 통해 전달 해야 하 고 **AZF2**합니다. 따라서 하나의 경로 hello에 반드시 필요한 **GatewaySubnet** 다음과 같이 합니다.

| 대상 | 다음 홉 | 설명 |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |온-프레미스 방화벽 관리 트래픽을 tooreach 허용 **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| 대상 | 다음 홉 | 설명 |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |트래픽 toohello 백 엔드 서브넷을 통해 응용 프로그램 서버 hello 호스팅 허용 **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |통해 라우팅될 모든 트래픽 toobe 허용 **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| 대상 | 다음 홉 | 설명 |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |너무 트래픽이**azsn2** 를 통해 응용 프로그램 서버 toohello 웹 서버에서 tooflow **AZF2** |

또한의 hello 서브넷 toocreate 경로 테이블을 해야 **onpremvnet** toomimic hello 온-프레미스 데이터 센터입니다.

### <a name="onpremsn1udr"></a>onpremsn1udr
| 대상 | 다음 홉 | 설명 |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |너무 트래픽이**onpremsn2** 통해 **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| 대상 | 다음 홉 | 설명 |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |통해 Azure에 백업 toohello 트래픽 서브넷 허용 **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |너무 트래픽이**onpremsn1** 통해 **OPFW** |

## <a name="ip-forwarding"></a>IP 전달
UDR 및 IP 전달는 Azure VNet 조합 tooallow 가상 어플라이언스 사용 toobe toocontrol 트래픽 흐름에 사용할 수 있는 기능입니다.  가상 어플라이언스 방화벽이 나 NAT 장치 등의 방법으로 사용 되는 응용 프로그램 toohandle 네트워크 트래픽을 실행 하는 VM에 뿐입니다.

VM에 있는 수 tooreceive 들어오는 트래픽이 있어야 합니다.이 가상 어플라이언스 tooitself를 바람직하지 않습니다. VM tooreceive 트래픽이 tooallow 해결 tooother 대상, VM hello에 대 한 IP 전달 설정 해야 합니다. 이 Azure 설정 hello 게스트 운영 체제에서 설정이 아닙니다. Toohandle 응용 프로그램의 일부 형식에 가상 어플라이언스 여전히 요구 toorun 들어오는 트래픽을 hello 및 적절 하 게 전달 합니다.

IP 전달에 대 한 자세한 toolearn 방문 [사용자 정의 경로 및 IP 전달](virtual-networks-udr-overview.md#ip-forwarding)합니다.

예를 들어, 다음과 같은 Azure vnet의 설정이 hello 있다고 가정해 봅니다.

* 서브넷 **onpremsn1**은 **onpremvm1**이라는 VM을 포함합니다.
* 서브넷 **onpremsn2**은 **onpremvm2**이라는 VM을 포함합니다.
* 라는 가상 어플라이언스 **OPFW** 너무 연결 되어**onpremsn1** 및 **onpremsn2**합니다.
* 사용자 정의 경로 너무 연결**onpremsn1** 모든 너무 트래픽을 지정**onpremsn2** 너무 보내야**OPFW**합니다.

에이 가리키는 경우 **onpremvm1** tooestablish와의 연결을 시도 **onpremvm2**, hello UDR 사용 되 고 트래픽이 너무 전송**OPFW** hello 다음 홉으로 합니다. 실제 패킷의 대상 hello 있음을 명심 변경 되지 않으면 여전히 표시 **onpremvm2** hello 대상이 있습니다. 

IP 전달에 대 한 기능을 사용 하지 않고 **OPFW**, Azure 가상 네트워크 논리 hello hello 패킷에 짧아집니다, VM의 IP 주소는 hello 패킷에 대 한 hello 대상 이후 경우 hello 패킷 전송 toobe tooa VM만 허용 합니다.

IP 전달은와 hello Azure 가상 네트워크 논리는 원래 대상 주소를 변경 하지 않고 hello 패킷에 tooOPFW를 전달 합니다. **OPFW** hello 패킷을 처리 하 고 이러한 어떤 toodo 결정 해야 합니다.

에 대 한 hello Nic의 IP 전달 설정 해야 toowork 위에 hello 시나리오용 **OPFW**, **AZF1**, **AZF2**, 및 **AZF3** 에 사용 되는 라우팅 (연결 된 toohello 관리 서브넷 hello 것을 제외한 모든 Nic). 

## <a name="firewall-rules"></a>방화벽 규칙
위에서 설명한 대로 패킷이 가상 어플라이언스 toohello 전송 되도록 IP만 전달 합니다. 어플라이언스는 여전히 toodecide 패킷과와 어떤 toodo가 필요합니다. 위의 hello 시나리오에서는 toocreate hello 기기가에서 규칙에 따라이 필요 합니다.

### <a name="opfw"></a>onpremsn2
OPFW는 hello 규칙을 포함 하는 온-프레미스 장치를 나타냅니다.

* **경로**: 모든 트래픽을 too10.0.0.0/16 (**azurevnet**) 터널을 통해 전송 해야 **ONPREMAZURE**합니다.
* **정책**: **포트2** 및 **ONPREMAZURE** 간의 모든 양방향 트래픽을 허용합니다.

### <a name="azf1"></a>AZF1
AZF1은 hello 규칙에 포함 된 Azure 가상 어플라이언스를 나타냅니다.

* **정책**: **port1** 및 **port2** 간의 모든 양방향 트래픽을 허용합니다.

### <a name="azf2"></a>AZF2
AZF2는 hello 규칙에 포함 된 Azure 가상 어플라이언스를 나타냅니다.

* **경로**: 모든 트래픽을 too10.0.0.0/16 (**onpremvnet**)를 통해 toohello Azure 게이트웨이 IP 주소 (예: 10.0.0.1)를 전송 해야 **포트 1**합니다.
* **정책**: **port1** 및 **port2** 간의 모든 양방향 트래픽을 허용합니다.

## <a name="network-security-groups-nsgs"></a>NSG(네트워크 보안 그룹)
이 시나리오에서 NSG는 사용되지 않습니다. 그러나 Nsg는 tooeach 서브넷 toorestrict 들어오고 나가는 트래픽을 적용할 수 있습니다. 예를 들어, 다음 NSG 규칙 toohello 외부 FW 서브넷 hello를 적용할 수 있습니다.

**수신**

* Hello 서브넷의 모든 VM에 인터넷 tooport hello 80의에서 모든 TCP 트래픽이 허용 합니다.
* Hello 인터넷에서에서 다른 모든 트래픽이 거부 합니다.

**발신**

* 모든 트래픽 toohello 인터넷을 거부 합니다.

## <a name="high-level-steps"></a>대략적인 단계
toodeploy hello 상위 수준 단계 수행 아래이 시나리오에서는 합니다.

1. 로그인 tooyour Azure 구독입니다.
2. VNet toomimic hello toodeploy 온-프레미스 네트워크를 사용할 경우의 일부인 hello 리소스를 프로 비전 **ONPREMRG**합니다.
3. 일부인 hello 리소스를 프로 비전 **AZURERG**합니다.
4. 프로 비전 hello 터널 **onpremvnet** 너무**azurevnet**합니다.
5. 모든 리소스는 프로 비전 되 면 로그 너무**onpremvm2** 간의 ping 10.0.3.101 tootest 연결성 **onpremsn2** 및 **azsn3**합니다.

