---
title: "aaaUser 정의 된 경로 및 Azure의 IP 전달 | Microsoft Docs"
description: "Tooconfigure 사용자 정의 경로 (UDR) 및 IP 전달 tooforward Azure에서 가상 어플라이언스 toonetwork 트래픽 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>사용자 정의 경로 및 IP 전달

Azure에서 가상 컴퓨터 (Vm) tooa 가상 네트워크 (VNet)를 추가할 때 hello Vm은 서로 수 toocommunicate hello 네트워크를 통해 자동으로 확인할 수 있습니다. Hello Vm 서브넷이 서로 다른 경우에 게이트웨이 toospecify를 않아도 됩니다. hello 같은 기준이 hello Vm toohello에서 통신에 대 한 공용 인터넷 및 tooyour Azure에서 하이브리드 연결 데이터 센터를 사용할 수 있는지를 소유 하는 경우에 tooyour 온-프레미스 네트워크입니다.

통신의이 흐름은 Azure 일련의 시스템 경로 toodefine IP 트래픽이 흐르는 방법을 사용 하기 때문에 가능 합니다. Hello 흐름 hello 다음 시나리오에서에서이 통신을 제어 하는 시스템 경로:

* 내에서 동일한 서브넷을 hello 합니다.
* VNet 내의 서브넷 tooanother에서.
* Vm toohello 인터넷 합니다.
* VPN 게이트웨이 통해는 VNet tooanother VNet입니다.
* VNet tooanother VNet (서비스 연결) 피어 링을 통해 VNet에서
* VPN 게이트웨이 통해 VNet tooyour 온-프레미스 네트워크입니다.

아래 hello 그림 VNet, 2 서브넷 및 hello와 함께 몇 가지 Vm을 사용 하 여 간단한 설치 IP 트래픽이 tooflow 허용 하는 시스템 경로 보여 줍니다.

![Azure의 시스템 경로](./media/virtual-networks-udr-overview/Figure1.png)

시스템 경로 hello 사용을 자동으로 배포에 대 한 트래픽을 용이 하 게, 있지만 toocontrol hello 패킷을 라우팅할 가상 어플라이언스를 통해 만들려는 경우가 있습니다. 수행 하므로 사용자 정의 경로 만들어 지정 tooa 특정 서브넷 toogo tooyour 가상 어플라이언스를 대신 흐르는 패킷이 대 한 다음 홉 hello 하 고 IP를 사용 하도록 설정에 대 한 전달 hello hello 가상 어플라이언스를 실행 중인 VM입니다.

hello 아래 그림은 예의 사용자 정의 경로 및 IP tooforce 패킷을 전달 다른 toogo에서 세 번째 서브넷을 가상 어플라이언스를 통해 tooone 서브넷을 전송 합니다.

![Azure의 시스템 경로](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> 사용자 정의 경로를 그대로 유지 하면서 서브넷 리소스에서 (예: 네트워크 인터페이스 연결 tooVMs) hello 서브넷 적용된 tootraffic 됩니다. 경로 toospecify를 만들 수 없습니다 어떻게 트래픽이 수신 서브넷 hello 인터넷에서에서 예를 들어 있습니다. 트래픽 toocannot를 전달 하는 hello 기기 hello에 있을 동일한 서브넷 hello 트래픽이 발생 하는 위치입니다. 항상 기기를 위한 별도의 서브넷을 만드세요. 
> 
> 

## <a name="route-resource"></a>경로 리소스
패킷을은 hello 실제 네트워크에 각 노드에 정의 된 경로 테이블을 기반으로 하는 TCP/IP 네트워크를 통해 라우팅됩니다. 경로 테이블은 개별 경로의 컬렉션 toodecide 여기서 tooforward 패킷을에 따라 사용 hello 대상 IP 주소. 경로는 hello 다음 이루어져 있습니다.

| 속성 | 설명 | 제약 조건 | 고려 사항 |
| --- | --- | --- | --- |
| 주소 접두사 |hello 대상 CIDR toowhich hello 경로 10.1.0.0/16 등 적용 됩니다. |Hello에 주소를 나타내는 유효한 CIDR 범위 여야 합니다. 공용 인터넷, Azure 가상 네트워크 또는 온-프레미스 데이터 센터입니다. |있는지 hello 확인 **주소 접두사** hello에 대 한 hello 주소가 들어 있지 않으면 **다음 홉 주소**, 그렇지 않은 프로그램 패킷을 도달 하지 않고 hello 소스 toohello 다음 홉에서 이동 하는 루프에 입력 됩니다 hello 대상입니다. |
| 다음 홉 유형 |hello 종류의 Azure 홉 hello 패킷에 전송 되어야 합니다. |Hello 다음 값 중 하나 여야 합니다. <br/> **Virtual Network**. Hello 로컬 가상 네트워크를 나타냅니다. 예를 들어, 두 개의 서브넷이 있는 경우 10.1.0.0/16 및에서 10.2.0.0/16 hello 동일한 가상 네트워크, hello 경로 테이블의 각 서브넷에 대 한 hello 경로 다음 홉 값 *가상 네트워크*합니다. <br/> **Virtual Network 게이트웨이**. Azure S2S VPN Gateway를 나타냅니다. <br/> **인터넷**. Hello Azure 인프라에서 제공 하는 hello 기본 인터넷 게이트웨이 나타냅니다. <br/> **가상 어플라이언스**. Tooyour Azure 가상 네트워크를 추가 하는 가상 어플라이언스를 나타냅니다. <br/> **없음**. 블랙 홀을 나타냅니다. Tooa 블랙홀에 전달 된 패킷은 전혀 전달 되지 않습니다. |사용 하는 것이 좋습니다 **가상 어플라이언스** toodirect 트래픽 tooa VM 또는 Azure 부하 분산 장치 내부 IP 주소입니다.  이 형식은 아래 설명 된 대로 IP 주소의 hello 지정이 될 수 있습니다. 사용 하는 것이 좋습니다는 **None** toostop 패킷을 대상 지정 된 이동을 tooa에서를 입력 합니다. |
| 다음 홉 주소 |전달 해야 하는 패킷을 hello IP 주소를 포함 하는 hello 다음 홉 주소입니다. 다음 홉 값은 다음 홉 형식이 hello 인 경로 에서만 허용 *가상 어플라이언스*합니다. |Hello를 거치지 않고 사용자 정의 경로 hello 적용 하는 가상 네트워크 내에서 연결할 수 있는 IP 주소 여야 합니다는 **가상 네트워크 게이트웨이**합니다. hello IP 주소 또는 peered 가상 네트워크를 적용 하는 경우 동일한 가상 네트워크는 hello에 toobe에 있습니다. |Hello IP 주소는 VM을 나타내는 경우 사용 하도록 설정 하면 있는지 확인 [IP 전달을](#IP-forwarding) hello VM에 대 한 Azure에서. Hello IP 주소 나타냅니다 hello 내부 IP 주소를 Azure 부하 분산 장치 있어야 일치 하는 부하 분산 규칙 각 포트에 대해 원하는 tooload 분산 합니다.|

Azure PowerShell에서 일부 hello "NextHopType" 값 이름이 다릅니다.

* 가상 네트워크는 VnetLocal입니다.
* 가상 네트워크 게이트웨이는 VirtualNetworkGateway입니다.
* 가상 어플라이언스는 VirtualAppliance입니다.
* Internet은 인터넷입니다.
* None은 없음입니다.

### <a name="system-routes"></a>시스템 경로
가상 네트워크에서 만든 모든 서브넷 hello 시스템 경로 규칙을 포함 하는 경로 테이블 자동 연결 됩니다.

* **로컬 Vnet 규칙**:이 규칙은 가상 네트워크에 있는 모든 서브넷에 대해 자동으로 생성됩니다. Hello Vm hello VNet에에서 직접 연결 되어 있는 및는 중간 없는 다음 홉을 지정 합니다.
* **온-프레미스 규칙**:이 규칙 tooall 전송 트래픽을 toohello 온-프레미스 주소 범위를 적용 하 고 VPN 게이트웨이 사용 하 여 hello 다음 홉 대상으로 합니다.
* **인터넷 규칙**:이 규칙에는 모든 트래픽이 toohello 처리 공용 인터넷 (주소 접두사 0.0.0.0/0) 및 사용 하 여 hello 인프라 인터넷 게이트웨이 hello로 모든 트래픽이 toohello 인터넷에 대 한 다음 홉 합니다.

### <a name="user-defined-routes"></a>사용자 정의 경로
대부분의 환경에만 Azure에서 이미 정의 된 hello 시스템 경로 필요 합니다. 그러나와 같은 특정 경우에 하나 이상의 경로 추가 toocreate 경로 테이블을 할 수 있습니다.

* 온-프레미스 네트워크를 통해 터널링 toohello 인터넷 강제로 적용 합니다.
* Azure 환경에서 가상 어플라이언스를 사용하는 경우

위의 hello 시나리오에서는 toocreate 경로 테이블 및 사용자 정의 경로 tooit를 추가 합니다. 여러 경로 테이블을 포함할 수 있습니다 hello 동일한 경로 테이블 수 있으며 관련된 tooone 또는 서브넷을 더 합니다. 및 각 서브넷 연결된 tooa 단일 경로 테이블에만 될 수 있습니다. 모든 Vm 및 서브넷에 있는 클라우드 서비스는 hello 경로 연결 된 테이블 toothat 서브넷을 사용 합니다.

서브넷 경로 테이블 연결된 toohello 서브넷 될 때까지 시스템 경로에 의존 합니다. 연결이 설정되면 사용자 정의 경로 및 시스템 경로 간에 LPM(가장 긴 접두사 일치)을 기반으로 라우팅이 수행됩니다. 없을 경우 둘 이상의 경로가 동일한 LPM 경로 선택은 일치 하는 hello로 순서에 따라 hello에서 원본에 따라:

1. 사용자 정의 경로
2. BGP 경로(ExpressRoute를 사용하는 경우)
3. 시스템 경로

toolearn toocreate 사용자 경로 정의 하는 방법 참조 [tooCreate 라우팅합니다 하 고 Azure의 IP 전달을 사용 하도록 설정 하는 방법을](virtual-network-create-udr-arm-template.md)합니다.

> [!IMPORTANT]
> 사용자 정의 경로 적용 된 tooAzure Vm 및 클라우드 서비스입니다. 예를 들어, tooadd 온-프레미스 네트워크와 Azure 간의 방화벽 가상 어플라이언스를 원하는 경우 수 toocreate toohello 온-프레미스 주소 공간 toohello 가상 라인으로 전환 하는 모든 트래픽을 전달 하는 Azure 경로 테이블에 대 한 사용자 정의 경로 구성할 수 있습니다. 사용자 정의 경로 (UDR) toohello GatewaySubnet tooforward 모든 트래픽을 온-프레미스 tooAzure에서 hello 가상 어플라이언스를 통해 추가할 수 있습니다. 이 기능은 최근에 추가되었습니다.
> 
> 

### <a name="bgp-routes"></a>BGP 경로
ExpressRoute 연결 온-프레미스 네트워크와 Azure 간에 있는 경우에 온-프레미스 네트워크 tooAzure에서 BGP toopropagate 경로 사용할 수 있습니다. Hello에 이러한 BGP 경로 사용 하는 시스템 경로 및 사용자 같은 방식으로 각 Azure 서브넷에 경로 정의 합니다. 자세한 내용은 [ExpressRoute 소개](../expressroute/expressroute-introduction.md)를 참조하세요.

> [!IMPORTANT]
> 프로그램 Azure 환경 toouse 강제 hello 다음 홉으로 hello VPN 게이트웨이 사용 하는 서브넷 0.0.0.0/0에 대 한 사용자 정의 경로 만들어 온-프레미스 네트워크를 통해 터널링을 구성할 수 있습니다. 그러나 이 구성은 VPN Gateway를 사용하는 경우에만 작동하고 ExpressRoute를 사용하는 경우에는 작동하지 않습니다. ExpressRoute의 경우 강제 터널링은 BGP를 통해 구성됩니다.
> 
> 

## <a name="ip-forwarding"></a>IP 전달
Hello는 주요 이유 toocreate 중 하나 위에 설명 된 대로 사용자 정의 경로 tooforward 트래픽 tooa 가상 어플라이언스는. 가상 어플라이언스 방화벽이 나 NAT 장치 등의 방법으로 사용 되는 응용 프로그램 toohandle 네트워크 트래픽을 실행 하는 VM에 뿐입니다.

VM에 있는 수 tooreceive 들어오는 트래픽이 있어야 합니다.이 가상 어플라이언스 tooitself를 바람직하지 않습니다. VM tooreceive 트래픽이 tooallow 해결 tooother 대상, VM hello에 대 한 IP 전달 설정 해야 합니다. 이 Azure 설정 hello 게스트 운영 체제에서 설정이 아닙니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[hello 리소스 관리자 배포 모델에서 경로 만들어](virtual-network-create-udr-arm-template.md) toosubnets 연결 합니다. 
* 너무 방법에 대해 알아봅니다[hello 클래식 배포 모델에서 경로 만들어](virtual-network-create-udr-classic-ps.md) toosubnets 연결 합니다.

