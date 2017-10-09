---
title: "인프라 지침-Windows 네트워킹 aaaAzure | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure 인프라 서비스에서 가상 네트워킹을 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e2d45973-5eba-4904-8ba0-1821f64feed7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 64c288957e7c7b89578d871a74ff45ce470ed922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-windows-vms"></a>Windows VM에 대한 Azure 네트워킹 인프라 지침 

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

이 문서 기존 온-프레미스 환경 간에 Azure 내에서 가상 네트워킹 및 연결에 대 한 단계를 계획 하는 데 필요한 이해 hello에 중점을 둡니다.

## <a name="implementation-guidelines-for-virtual-networks"></a>가상 네트워크에 대한 구현 지침
의사 결정:

* 어떤 종류의 가상 네트워크 필요 한가요 toohost IT 작업 또는 인프라 (클라우드 전용 또는 크로스-프레미스)?
* 주소 공간 얼마나 크로스-프레미스 가상 네트워크에 대 한 필요 한가요 toohost hello 서브넷 및 Vm 이제 및 hello에 적절 한 확장에 대 한 향후?
* 가상 네트워크의 중앙 집중식 toocreate 알아볼 수 또는 각 리소스 그룹에 대 한 개별 가상 네트워크를 만들?

작업:

* Hello 가상 네트워크 toobe 생성에 대 한 hello 주소 공간을 정의 합니다.
* 각 서브넷 및 hello 주소 공간의 hello 집합을 정의 합니다.
* 크로스-프레미스 가상 네트워크에 Vm 가상 네트워크 필요 tooreach hello에에서 hello hello 온-프레미스 위치에 대 한 로컬 네트워크 주소 공간 hello 집합을 정의 합니다.
* 온-프레미스 네트워킹 팀 tooensure hello 적절 한 라우팅을 구성할 때 만드는 크로스-프레미스 가상 네트워크를 사용 합니다.
* 명명 규칙을 사용 하 여 hello 가상 네트워크를 만듭니다.

## <a name="virtual-networks"></a>가상 네트워크
가상 네트워크는 가상 컴퓨터 (Vm) 간의 필요한 toosupport 통신 합니다. 물리적 네트워크의 경우와 마찬가지로 서브넷, 사용자 지정 IP 주소, DNS 설정, 보안 필터링 및 부하 분산을 정의할 수 있습니다. 사용 하 여 한 [VPN 게이트웨이](../../vpn-gateway/vpn-gateway-about-vpngateways.md) 또는 [Express 경로 회로](../../expressroute/expressroute-introduction.md), Azure 가상 네트워크 tooyour 온-프레미스 네트워크에 연결할 수 있습니다. [가상 네트워크 및 해당 구성 요소](../../virtual-network/virtual-networks-overview.md)에 대해 자세히 읽어보세요.

리소스 그룹을 사용하여 보다 유연하게 가상 네트워킹 구성 요소를 디자인할 수 있습니다. Vm은 리소스 그룹 자신의 외부 toovirtual 네트워크를 연결할 수 있습니다. 일반적인 디자인 방법은 일반적인 팀에서 관리 될 수 있는 핵심 네트워킹 인프라를 포함 하는 중앙 집중식 toocreate 리소스 그룹와 다음 Vm 및 해당 응용 프로그램 tooseparate 리소스 그룹 배포 합니다. 이 방법을 사용 하면 응용 프로그램 소유자 액세스 액세스 toohello 구성 hello 넓어짐 가상 네트워킹 리소스를 열지 않고도 해당 Vm이 포함 된 toohello 리소스 그룹입니다.

## <a name="site-connectivity"></a>사이트 연결
### <a name="cloud-only-virtual-networks"></a>클라우드 전용 가상 네트워크
온-프레미스 사용자 및 컴퓨터 필요가 없는 경우 Azure 가상 네트워크에 대 한 지속적인 연결 tooVMs, 가상 네트워크 디자인 매우 간단 합니다.

![기본 클라우드 전용 가상 네트워크 다이어그램](./media/infrastructure-networking-guidelines/vnet01.png)

이 방법은 일반적으로 인터넷 기반 웹 서버와 같은 인터넷 연결 작업을 위한 것입니다. RDP 또는 지점-사이트 간 VPN 연결을 사용하여 이러한 VM을 관리할 수 있습니다.

Tooyour 온-프레미스 네트워크를 연결 되지 않기 때문에 Azure 전용 가상 네트워크 hello 동일한 개인 공간에는 온-프레미스를 사용 하는 경우에 hello 개인 IP 주소 공간 일부를 사용할 수 있습니다.

### <a name="cross-premises-virtual-networks"></a>크로스-프레미스 가상 네트워크
온-프레미스 사용자 및 컴퓨터는 Azure 가상 네트워크에 대 한 지속적인 연결 tooVMs를 요구 하는 경우 크로스-프레미스 가상 네트워크를 만듭니다.  Tooyour 온-프레미스 네트워크로 연결 ExpressRoute 또는 사이트 간 VPN 연결 합니다.

![프레미스 간 가상 네트워크 다이어그램](./media/infrastructure-networking-guidelines/vnet02.png)

이 구성에서는 hello Azure 가상 네트워크는 기본적으로 온-프레미스 네트워크는 클라우드 기반 확장입니다.

연결 때문에 tooyour 온-프레미스 네트워크에서 크로스-프레미스 가상 네트워크의 고유한 조직에서 사용 하는 hello 주소 공간 일부를 사용 해야 합니다. 에 hello 동일한 방식으로 해당 다른 회사의 위치 할당 된 특정 IP 서브넷, Azure 네트워크를 확장 하는 대로 다른 위치가 됩니다.

tooallow 크로스-프레미스 가상 네트워크 tooyour 온-프레미스 네트워크에서 패킷을 tootravel, hello 가상 네트워크에 대 한 hello 로컬 네트워크 정의의 일부로 hello 관련 온-프레미스 주소 접두사 집합을 구성 해야 합니다. Hello 주소에 따라 공간 hello 가상 네트워크 및 hello 집합이 관련의 온-프레미스 위치, hello 로컬 네트워크에 많은 주소 접두사 수 있습니다.

클라우드 전용 가상 네트워크 tooa 크로스-프레미스 가상 네트워크를 변환할 수 이지만 가장 가능성이 높은 필요 하면 toore IP 가상 네트워크 주소 공간 및 Azure 리소스. 따라서 IP 서브넷을 할당할 때 가상 네트워크 toobe tooyour 연결 된 온-프레미스 네트워크에 필요한 경우 주의 합니다.

## <a name="subnets"></a>서브넷
서브넷 허용은 서로 관련 되어 있거나 논리적으로 tooorganize 리소스 (Vm에 대 한 하나의 서브넷 toohello를 연결 하는 예를 들어 동일한 응용 프로그램), 또는 물리적으로 (예: 리소스 그룹당 서브넷 1 개). 또한 보안 강화를 위해 서브넷 격리 기술을 이용할 수도 있습니다.

크로스-프레미스 가상 네트워크 서브넷 hello로 디자인 해야 온-프레미스 리소스에 대 한 사용 하는 동일한 규칙입니다. **Azure에서는 각 서브넷에 대 한 hello 주소 공간의 처음 3 개의 IP 주소를 hello 항상**합니다. toodetermine hello 번호 주소의 hello 서브넷에 대 한 필요한 hello 이제 해야 하는 Vm 수를 계산 하 여 시작 합니다. 이후 성장을 예측 하 고 테이블 toodetermine hello hello 서브넷 크기를 다음 hello를 사용 하 여 키를 누릅니다.

| 필요한 VM 수 | 필요한 호스트 비트 수 | Hello 서브넷의 크기 |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> 기본 온-프레미스 서브넷에 대 한 hello 최대 n 호스트 bits 사용 하 여 서브넷에 대 한 호스트 주소 수는 2<sup> n </sup> 2 – 합니다. Azure 서브넷에 대 한 hello 최대 n 호스트 bits 사용 하 여 서브넷에 대 한 호스트 주소 수는 2<sup> n </sup> -5 (2 + Azure 각 서브넷에 사용 하는 hello 주소에 대해 3).
> 
> 

너무 작으면 서브넷 크기를 선택 하면 toore IP에 있고 hello 서브넷에서 hello Vm을 다시 배포 합니다.

## <a name="network-security-groups"></a>네트워크 보안 그룹
네트워크 보안 그룹을 사용 하 여 가상 네트워크를 통해 이동 하는 필터링 규칙 toohello 트래픽을 적용할 수 있습니다. 빌드할 수 세분화 된 필터링 규칙 toosecure 가상 네트워킹 환경, 인바운드 및 아웃 바운드 트래픽, 소스 및 대상 IP 범위, 포트 등을 사용할 수를 제어 합니다. 네트워크 보안 그룹에 가상 네트워크 또는 직접 가상 네트워크 인터페이스를 제공 하는 tooa 내에서 적용 된 toosubnets 수 있습니다. 몇 가지 수준의 네트워크 보안 그룹을 가상 네트워크에서 트래픽을 필터링 toohave 것이 좋습니다. [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md)에 대해 자세히 읽어보세요.

## <a name="additional-network-components"></a>네트워크 구성 요소 추가
온-프레미스 물리적 네트워킹 인프라의 경우와 마찬가지로, Azure 가상 네트워킹에는 서브넷 및 IP 주소 지정 이상의 기능이 포함될 수 있습니다. Tooincorporate 경우가 응용 프로그램 인프라를 디자인할 때 이러한 추가 구성 요소 중 일부:

* [VPN 게이트웨이](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -연결 tooother Azure 가상 네트워크가 Azure 가상 네트워크, 또는 사이트 간 VPN 연결을 통해 tooon 온-프레미스 네트워크에 연결 합니다. 전용, 보안 연결을 위해 Express 경로 연결을 구현합니다. 지점 및 사이트 간 VPN 연결로 사용자 직접 액세스를 제공할 수도 있습니다.
* [부하 분산 장치](../../load-balancer/load-balancer-overview.md) - 필요에 따라 외부 및 내부 트래픽에 대한 부하 분산을 제공합니다.
* [응용 프로그램 게이트웨이](../../application-gateway/application-gateway-introduction.md) -HTTP hello 응용 프로그램 계층에서 부하 분산, 웹 응용 프로그램에 대 한 몇 가지 추가 혜택을 제공 하는 대신 hello Azure 부하 분산 장치를 배포 합니다.
* [트래픽 관리자](../../traffic-manager/traffic-manager-overview.md) DNS 기반-다른 지역에서 Azure 데이터 센터에서 응용 프로그램 배포 toodirect 최종 사용자에 게 toohello 가장 가까운 사용할 수 있는 응용 프로그램 끝점, 가능 하면 toohost 트래픽입니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

