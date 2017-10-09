---
title: "가상 네트워크 (VNet) aaaAzure 계획 및 디자인 가이드 | Microsoft Docs"
description: "Azure에서 가상 네트워크 tooplan 및 디자인 격리, 연결 및 위치 요구 사항에 따라 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Azure 가상 네트워크 계획 및 디자인
충분히 쉽게와 VNet tooexperiment를 만들 수 있지만 그럴 경우 조직의 시간 toosupport hello 프로덕션 요구를 통해 여러 Vnet을 배포 합니다. 몇 가지 계획 및 디자인을 있습니다 수 toodeploy Vnet 되며 hello 필요한 리소스를 보다 효율적으로 연결 합니다. Vnet 모르는 경우는 것이 좋습니다는 하면 [Vnet에 대 한 자세한 내용은](virtual-networks-overview.md) 및 [어떻게 toodeploy](virtual-networks-create-vnet-arm-pportal.md) 진행 하기 전에.

## <a name="plan"></a>계획
성공을 위해서는 Azure 구독, 하위 지역 및 네트워크 리소스를 충분히 이해하는 것이 중요합니다. Hello 아래 고려 사항 목록을 시작 지점으로 사용할 수 있습니다. 이러한 고려 사항을 이해 하 고 나면 네트워크 디자인에 대 한 hello 요구 사항을 정의할 수 있습니다.

### <a name="considerations"></a>고려 사항
계획 관련 질문 아래 hello를 응답 하기 전에 hello 다음을 고려 합니다.

* Azure에서 만드는 모든 항목은 하나 이상의 리소스로 구성됩니다. 가상 컴퓨터 (VM)는 리소스 hello 네트워크 어댑터 (NIC) 사용 하는 인터페이스는 VM은 리소스 hello NIC에서 사용 되는 공용 IP 주소는 리소스, hello VNet hello NIC가 연결 된 toois 리소스입니다.
* [Azure 지역](https://azure.microsoft.com/regions/#services) 및 구독 내에서 리소스를 만듭니다. 리소스에 연결 된 tooa 가상 네트워크 hello에 있는 동일한 지역 및 구독 hello 리소스에는 수만 있습니다.
* 사용 하 여 다른 가상 네트워크 tooeach를 연결할 수 있습니다.
    * **[가상 네트워크 피어 링](virtual-network-peering-overview.md)**: hello 가상 네트워크에에서 존재 해야 hello 동일한 Azure 지역입니다. 가상 네트워크 겹치기의 리소스 간에 대역폭 하면 hello 리소스에 연결 된 toohello 것 처럼 동일 hello은 동일한 가상 네트워크입니다.
    * **Azure [VPN 게이트웨이](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: hello 가상 네트워크에에서 존재할 수 hello 동일 하거나 서로 다른 Azure 지역입니다. VPN 게이트웨이 통해 연결 된 가상 네트워크의 리소스 간에 대역폭의 hello VPN 게이트웨이 hello 대역폭으로 제한 됩니다.
* Hello 중 하나를 사용 하 여 Vnet tooyour 온-프레미스 네트워크를 연결할 수 있습니다 [연결 옵션](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) Azure에서 사용할 수 있습니다.
* 다양 한 리소스를 함께 그룹화 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups), 하나의 단위로 쉽게 toomanage hello 리소스 만들기. 리소스 그룹으로 hello 리소스가 속해야 toohello 여러 지역에서 리소스를 포함할 수 있습니다 동일한 구독 합니다.

### <a name="define-requirements"></a>요구 사항 정의
Azure 네트워크 디자인에 대 한 시작 점으로 아래 hello 질문을 사용 합니다.    

1. 어떤 Azure 위치 하나요 toohost Vnet을 사용 하 여?
2. 이러한 Azure 위치 간의 tooprovide 통신 필요 한가요?
3. Azure VNet(s)와 온-프레미스 센터 간의 tooprovide 통신 필요 한가요?
4. 솔루션에 얼마나 많은 IaaS(Infrastructure as a Service) VM, 클라우드 서비스 역할 및 웹앱이 필요합니까?
5. Vm (즉, 프런트 엔드 웹 서버와 백 엔드 데이터베이스 서버)의 그룹에 따라 tooisolate 트래픽의 필요 한가요?
6. 가상 어플라이언스를 사용 하 여 toocontrol 트래픽 흐름 필요 한가요?
7. 사용자가 필요한 상이한 권한 toodifferent Azure 리소스 합니까?

### <a name="understand-vnet-and-subnet-properties"></a>VNet 및 서브넷 속성 이해
VNet과 서브넷 리소스를 사용하여 Azure에서 실행 중인 워크로드에 대한 보안 경계를 정의할 수 있습니다. VNet은 주소 공간의 모임(CIDR 블록으로 정의됨)으로 특징지을 수 있습니다.

> [!NOTE]
> 네트워크 관리자는 CIDR 표기법에 익숙합니다. CIDR을 잘 모르는 경우 [자세히 알아보세요](http://whatismyipaddress.com/cidr).
>
>

Vnet hello 다음과 같은 속성을 포함 합니다.

| 속성 | 설명 | 제약 조건 |
| --- | --- | --- |
| **name** |VNet 이름 |Too80 문자를 문자열입니다. 문자, 숫자, 밑줄, 마침표 또는 하이픈을 포함할 수 있습니다. 문자 또는 숫자로 시작해야 합니다. 문자, 숫자 또는 밑줄로 끝나야 합니다. 대문자 또는 소문자를 포함할 수 있습니다. |
| **위치** |(또한 참조 tooas 지역)는 azure 위치입니다. |중 하나 여야 합니다 hello 유효한 Azure 위치입니다. |
| **addressSpace** |CIDR 표기법에 hello VNet 구성 하는 주소 접두사의 컬렉션입니다. |공용 IP 주소 범위를 포함하여 올바른 CIDR 주소 블록의 배열이어야 합니다. |
| **서브넷** |서브넷 hello VNet 구성 하는 컬렉션입니다. |아래 hello 서브넷 속성 표를 참조 합니다. |
| **dhcpOptions** |**dnsServers**로 명명된 단일 필수 속성을 포함하는 개체입니다. | |
| **dnsServers** |DNS 서버 hello VNet에서 사용 하는 배열입니다. 서버를 지정하지 않은 경우 Azure 내부 이름 확인이 사용됩니다. |IP 주소로 too10 DNS 서버를 배열 이어야 합니다. |

서브넷은 VNet의 자식 리소스이며, IP 주소 접두사를 사용하여 CIDR 블록 내의 주소 공간 세그먼트를 정의하는 데 도움이 됩니다. Nic는 toosubnets, 및 다양 한 작업에 대 한 연결을 제공 하는 연결 된 tooVMs를 추가할 수 있습니다.

서브넷 hello 다음과 같은 속성을 포함 합니다.

| 속성 | 설명 | 제약 조건 |
| --- | --- | --- |
| **name** |서브넷 이름 |Too80 문자를 문자열입니다. 문자, 숫자, 밑줄, 마침표 또는 하이픈을 포함할 수 있습니다. 문자 또는 숫자로 시작해야 합니다. 문자, 숫자 또는 밑줄로 끝나야 합니다. 대문자 또는 소문자를 포함할 수 있습니다. |
| **위치** |(또한 참조 tooas 지역)는 azure 위치입니다. |중 하나 여야 합니다 hello 유효한 Azure 위치입니다. |
| **addressPrefix** |CIDR 표기법에서 hello 서브넷 구성 하는 단일 주소 접두사 |Hello VNet 주소 공간 중 하나에 포함 된 단일 CIDR 블록 이어야 합니다. |
| **networkSecurityGroup** |NSG 적용 toohello 서브넷 | |
| **routeTable** |경로 테이블 toohello 서브넷 적용 | |
| **ipConfigurations** |Nic 연결 된 toohello 서브넷에서 사용 하는 IP 구성 개체의 컬렉션 | |

### <a name="name-resolution"></a>이름 확인
기본적으로 VNet 사용 [Azure 제공 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve 이름을 hello VNet 내의 공용 인터넷 hello 합니다. 그러나 Vnet tooyour 온-프레미스 데이터 센터를 연결 하는 경우 필요한 tooprovide [자체 DNS 서버](virtual-networks-name-resolution-for-vms-and-role-instances.md) 네트워크 간 tooresolve 이름입니다.  

### <a name="limits"></a>제한
Hello에 hello 네트워킹 제한 검토 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서 tooensure 디자인 hello 한계를 사용 하 여 충돌 하지 않습니다. 일부 제한은 지원 티켓을 열어 늘릴 수 있습니다.

### <a name="role-based-access-control-rbac"></a>역할 기반 액세스 제어(RBAC)
사용할 수 있습니다 [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) toocontrol hello 수준의 액세스를 다른 사용자가 Azure에서 toodifferent 리소스 있을 수 있습니다. 이런 방식으로 요구에 따라 팀에서 수행 하는 hello 작업을 구분할 수 있습니다.

Hello에 대 한 사용자가 가상 네트워크는 먼 우려 **네트워크 참가자** 역할 Azure 리소스 관리자 가상 네트워크 리소스에 대해 모든 권한을 갖고 있습니다. 마찬가지로, 사용자 hello에 **클래식 네트워크 참가자** 역할 클래식 가상 네트워크 리소스에 대해 모든 권한을 갖고 있습니다.

> [!NOTE]
> 수도 있습니다 [자신의 역할을 만들](../active-directory/role-based-access-control-configure.md) tooseparate 관리 요구 사항입니다.
>
>

## <a name="design"></a>디자인
Hello에 toohello 질문 hello 답변을 알고 있다면 [계획](#Plan) 섹션에서 Vnet을 정의 하기 전에 hello 다음을 검토 합니다.

### <a name="number-of-subscriptions-and-vnets"></a>구독 및 VNet의 수
Hello 다음 시나리오에서에서 여러 Vnet을 작성 하는 것이 좋습니다.

* **Toobe 서로 다른 Azure 위치에 배치 해야 하는 Vm**합니다. Azure에서 VNet은 지역적입니다. 여러 위치에 걸쳐 있지 않습니다. 따라서 toohost Vm에서 원하는 각 Azure 위치에 대해 하나 이상의 VNet이 필요 합니다.
* **Toobe 서로 완전히 분리 해야 하는 워크 로드**합니다. 동일한 IP 주소 공간이 서로 tooisolate 다양 한 작업이 해당도 사용 하 여 hello 별도 Vnet을 만들 수 있습니다.

Hello 위의 참조 제한은 구독 당 지역당 염두에 둬야 합니다. 즉, 여러 구독 tooincrease hello 제한인 리소스 Azure에서 유지 관리할 수 있습니다 사용할 수 있습니다. 사이트 간 VPN 또는 다른 구독의 Vnet tooconnect ExpressRoute 회로 사용할 수 있습니다.

### <a name="subscription-and-vnet-design-patterns"></a>구독 및 VNet 디자인 패턴
hello 표에서 구독 및 Vnet을 사용 하기 위한 몇 가지 일반적인 디자인 패턴을 보여 줍니다.

| 시나리오 | 다이어그램 | 장점 | 단점 |
| --- | --- | --- | --- |
| 단일 구독, 앱당 두 VNet |![단일 구독](./media/virtual-network-vnet-plan-design-arm/figure1.png) |하나의 구독 에서만 toomanage 합니다. |Azure 지역당 최대 Vnet 수입니다. 이후에 구독이 더 필요합니다. 검토 hello [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 을 참조 합니다. |
| 앱당 1개 구독, 앱당 두 VNet |![단일 구독](./media/virtual-network-vnet-plan-design-arm/figure2.png) |구독당 두 개의 VNet만 사용합니다. |앱이 너무 많은 경우 쉽다는 점 toomanage 합니다. |
| 사업부당 1개 구독, 앱당 두 VNet |![단일 구독](./media/virtual-network-vnet-plan-design-arm/figure3.png) |구독 및 VNet 수 간에 균형을 유지합니다. |사업부(구독)당 최대 VNet 수입니다. 검토 hello [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 을 참조 합니다. |
| 사업부당 1개 구독, 앱 그룹당 두 VNet |![단일 구독](./media/virtual-network-vnet-plan-design-arm/figure4.png) |구독 및 VNet 수 간에 균형을 유지합니다. |서브넷과 NSG를 사용하여 앱을 격리해야 합니다. |

### <a name="number-of-subnets"></a>서브넷 수
다음 시나리오는 hello에 VNet에 여러 서브넷을 좋습니다.

* **서브넷에 있는 모든 NIC에 대해 개인 IP 주소가 부족**. 서브넷 주소 공간에 IP 주소 개수가 충분 없으면 hello 서브넷의 Nic hello 수에 대 한 여러 서브넷 toocreate 할 수 있습니다. Azure에서 사용할 수 없는 각 서브넷의에서 개인 IP 주소를 5 예약을 염두에서에 둬야: 먼저 hello 및 연결 (멀티 캐스트 hello 서브넷 주소에 대해) hello 주소 공간 및 사용 되는 내부적으로 (목적) DHCP 및 DNS 주소를 3 toobe의 주소를 지속 합니다.
* **보안**. 다중 계층 구조, 다른 적용 하 고 있는 작업을 위해 다른 Vm의 서브넷 tooseparate 그룹을 사용할 수 있습니다 [네트워크 보안 그룹 (Nsg)](virtual-networks-nsg.md#subnets) 이러한 서브넷에 대 한 합니다.
* **하이브리드 연결**. VPN 게이트웨이 및 express 경로 회로도 사용할 수[연결](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) Vnet tooone 다른, 및 tooyour 온-프레미스 데이터 센터입니다. VPN 게이트웨이 및 express 경로 회로 만든 자신의 toobe의 서브넷이 필요 합니다.
* **가상 어플라이언스**. Azure VNet에서 방화벽, WAN 가속기 또는 VPN 게이트웨이 같은 가상 어플라이언스를 사용할 수 있습니다. 이렇게 하면 해야 너무[트래픽을 라우팅할](virtual-networks-udr-overview.md) toothose 어플라이언스 자체의 서브넷에서 격리 하 고 있습니다.

### <a name="subnet-and-nsg-design-patterns"></a>서브넷 및 NSG 디자인 패턴
hello 표에서 서브넷을 사용 하기 위한 몇 가지 일반적인 디자인 패턴을 보여 줍니다.

| 시나리오 | 다이어그램 | 장점 | 단점 |
| --- | --- | --- | --- |
| 단일 서브넷, 앱당 응용 프로그램 계층당 여러 NSG |![단일 서브넷](./media/virtual-network-vnet-plan-design-arm/figure5.png) |하나의 서브넷 toomanage 합니다. |여러 Nsg 필요한 tooisolate 각 응용 프로그램입니다. |
| 앱당 1개 서브넷, 응용 프로그램 계층당 여러 NSG |![앱당 서브넷](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Nsg toomanage 적습니다. |여러 서브넷 toomanage 합니다. |
| 응용 프로그램 계층당 1개 서브넷, 앱당 여러 NSG |![계층당 서브넷](./media/virtual-network-vnet-plan-design-arm/figure7.png) |서브넷 및 NSG 수 간에 균형을 유지합니다. |구독당 최대 NSG 수입니다. 검토 hello [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 을 참조 합니다. |
| 앱당, 응용 프로그램 계층당 1개 서브넷, 서브넷당 여러 NSG |![앱당 계층당 서브넷](./media/virtual-network-vnet-plan-design-arm/figure8.png) |가능하면 NSG 수가 더 적습니다. |여러 서브넷 toomanage 합니다. |

## <a name="sample-design"></a>샘플 디자인
이 문서에서는 hello 정보의 tooillustrate hello 적용 hello를 시나리오를 따르는 것이 좋습니다.

여러분은 데이터 센터가 북아메리카에 2개, 유럽에 2개 있는 회사에서 일합니다. 6 식별 toomigrate tooAzure 파일럿으로 원하는 2 다른 비즈니스 단위에서 연결 된 응용 프로그램과 다른 고객 유지 관리 합니다. hello hello 응용 프로그램에 대 한 기본 아키텍처는 다음과 같습니다.

* App1, App2, App3 및 App4는 Ubuntu를 실행하는 Linux 서버에서 호스트되는 웹 응용 프로그램입니다. Linux 서버에 RESTful 서비스를 호스팅하는 각 응용 프로그램 tooa 별도 응용 프로그램 서버에 연결 합니다. hello RESTful 서비스 tooa 백 엔드 MySQL 데이터베이스를 연결합니다.
* App5 및 App6은 Windows Server 2012 R2를 실행하는 Windows 서버에서 호스트되는 웹 응용 프로그램입니다. 각 응용 프로그램 tooa 백 엔드 SQL Server 데이터베이스를 연결합니다.
* 모든 앱은 현재 북미 지역에 hello 회사의 데이터 센터 중 하나에서 호스트 됩니다.
* hello 온-프레미스 데이터 센터 hello 10.0.0.0/8 주소 공간을 사용합니다.

Hello 요구 사항을 준수를 충족 하는 가상 네트워크 솔루션 toodesign이 필요 합니다.

* 각 사업부는 다른 사업부의 리소스 사용량에 영향을 받아서는 안 됩니다.
* Vnet 및 서브넷 toomake 관리를 보다 쉽게 hello 양을 최소화 해야 합니다.
* 각 사업부에는 모든 응용 프로그램에 사용되는 단일 테스트/개발 VNet이 있어야 합니다.
* 각 응용 프로그램은 대륙당(북아메리카 및 유럽) 서로 다른 2개의 Azure 데이터 센터에서 호스트됩니다.
* 각 응용 프로그램은 서로 완전히 격리됩니다.
* 각 응용 프로그램 hello 인터넷을 통해 고객에 의해 액세스할 수 HTTP를 사용 합니다.
* 각 응용 프로그램은 암호화 된 터널을 사용 하 여 사용자가 연결 된 toohello 온-프레미스 데이터 센터에서 액세스할 수 있습니다.
* 연결 tooon 온-프레미스 데이터 센터는 기존의 VPN 장치를 사용 해야 합니다.
* hello 회사의 네트워킹 그룹 있어야 hello VNet 구성에 대 한 모든 권한을 합니다.
* 각 사업부의 개발자 수 toodeploy Vm tooexisting 서브넷만 있어야 합니다.
* 모든 응용 프로그램 (리프트 시프트) tooAzure 멤버인 마이그레이션됩니다.
* 각 위치에서 hello 데이터베이스 tooother Azure에 복제 해야 하루에 한 번에 위치 합니다.
* 각 응용 프로그램은 5개의 프런트 엔드 웹 서버, 2개의 응용 프로그램 서버(필요한 경우) 및 2개의 데이터베이스 서버를 사용합니다.

### <a name="plan"></a>계획
Hello에 hello 질문에 응답 하 여 계획 설계를 시작 해야 [요구 사항을 정의](#Define-requirements) 아래 표시 된 대로 합니다.

1. 어떤 Azure 위치 하나요 toohost Vnet을 사용 하 여?

    북아메리카에 2곳, 유럽에 2곳입니다. 기존 온-프레미스 데이터 센터의 실제 위치 hello에 기반한 선택 해야 합니다. 이런 방식으로 물리적 위치 tooAzure에서 연결 대기 시간: 더 나은 갖습니다.
2. 이러한 Azure 위치 간의 tooprovide 통신 필요 한가요?

    예. 이후 hello 데이터베이스가 복제 된 tooall 위치 여야 합니다.
3. Azure VNet(s)와 온-프레미스 데이터 센터 간의 tooprovide 통신 필요 한가요?

    예. 사용자가 연결 되기 때문 toohello 온-프레미스 데이터 센터에는 암호화 된 터널을 통해 수 tooaccess hello 응용 프로그램 이어야 합니다.
4. 솔루션에 IaaS VM이 얼마나 필요합니까?

    200개의 IaaS VM입니다. App1, App2, App3 및 App4에는 각각 5개의 웹 서버, 각각 2개의 응용 프로그램 서버, 각각 2개의 데이터베이스 서버가 필요합니다. 응용 프로그램당 총 9개의 IaaS VM 또는 36개의 IaaS VM입니다. App5 및 App6에는 5개의 웹 서버와 각각 2개의 데이터베이스 서버가 필요합니다. 응용 프로그램당 총 7개의 IaaS VM 또는 14개의 IaaS VM입니다. 따라서 각 Azure 지역에 있는 모든 응용 프로그램에 대해 50개의 IaaS VM이 필요합니다. 4 toouse 영역, 필요 하므로 IaaS Vm 200 됩니다 수 있습니다.

    Azure IaaS Vm 및 온-프레미스 네트워크 간에 또는 온-프레미스 데이터 센터 tooresolve 이름이 각 VNet에 tooprovide DNS 서버도 할 수 있습니다.
5. Vm (즉, 프런트 엔드 웹 서버와 백 엔드 데이터베이스 서버)의 그룹에 따라 tooisolate 트래픽의 필요 한가요?

    예. 각 응용 프로그램은 서로 완전히 격리되어야 하고 각 응용 프로그램 계층도 격리되어야 합니다.
6. 가상 어플라이언스를 사용 하 여 toocontrol 트래픽 흐름 필요 한가요?

    아니요. 가상 어플라이언스 사용된 tooprovide 보다 자세한 데이터 평면 로깅을 포함 하 되는 트래픽 흐름을 보다 자세히 제어할 수 있습니다.
7. 사용자가 필요한 상이한 권한 toodifferent Azure 리소스 합니까?

    예. hello 네트워킹 팀 해야 hello 가상 네트워킹 설정에 대해 모든 권한을 개발자 toodeploy 수 있어야 하는 동안 Vm toopre 기존 서브넷 합니다.

### <a name="design"></a>디자인
구독, Vnet, 서브넷 및 Nsg를 지정 하는 hello 디자인을 따라야 합니다. 여기서는 NSG를 설명하지만 디자인을 완료하기 전에 [NSG](virtual-networks-nsg.md) 에 대해 자세히 알아보아야 합니다.

**구독 및 VNet의 수**

요구 사항을 준수 하는 hello은 관련된 toosubscriptions과 Vnet입니다.

* 각 사업부는 다른 사업부의 리소스 사용량에 영향을 받아서는 안 됩니다.
* Vnet 및 서브넷의 hello 양을 최소화 해야 합니다.
* 각 사업부에는 모든 응용 프로그램에 사용되는 단일 테스트/개발 VNet이 있어야 합니다.
* 각 응용 프로그램은 대륙당(북아메리카 및 유럽) 서로 다른 2개의 Azure 데이터 센터에서 호스트됩니다.

이러한 요구에 따라 각 사업부에 대한 구독이 필요합니다. 이런 방식으로 사업부의 리소스 사용량은 다른 사업부에 대한 제한에 포함되지 않습니다. toominimize hello 수가 Vnet 지정할 것 이므로 hello를 사용 하 여 고려해 야 할 **사업부, 앱의 그룹 마다 두 개의 Vnet 파티션당 하나의 구독이** 아래 그림 처럼 패턴을 사용 합니다.

![단일 구독](./media/virtual-network-vnet-plan-design-arm/figure9.png)

또한 각 VNet에 대 한 toospecify hello 주소 공간에 필요 합니다. 하므로 hello 간의 연결 온-프레미스 데이터 센터 및 hello Azure 지역 Azure Vnet에 사용 된 hello 주소 공간은 없습니다 충돌 hello 온-프레미스 네트워크와 다른 기존 Vnet 각 VNet에서 사용 하는 hello 주소 공간 충돌 하지 해야 합니다. 이러한 요구 사항을 toosatisfy 아래 hello 표에 hello 주소 공간을 사용할 수 있습니다.  

| **구독** | **VNet** | **Azure 지역** | **주소 공간** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |미국 서부 |172.16.0.0/16 |
| BU1 |ProdBU1US2 |미국 동부 |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |북유럽 |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |서유럽 |172.19.0.0/16 |
| BU1 |TestDevBU1 |미국 서부 |172.20.0.0/16 |
| BU2 |TestDevBU2 |미국 서부 |172.21.0.0/16 |
| BU2 |ProdBU2US1 |미국 서부 |172.22.0.0/16 |
| BU2 |ProdBU2US2 |미국 동부 |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |북유럽 |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |서유럽 |172.25.0.0/16 |

**서브넷 및 NSG 수**

요구 사항을 준수 하는 hello은 관련된 toosubnets과 Nsg입니다.

* Vnet 및 서브넷의 hello 양을 최소화 해야 합니다.
* 각 응용 프로그램은 서로 완전히 격리됩니다.
* 각 응용 프로그램 hello 인터넷을 통해 고객에 의해 액세스할 수 HTTP를 사용 합니다.
* 각 응용 프로그램은 암호화 된 터널을 사용 하 여 사용자가 연결 된 toohello 온-프레미스 데이터 센터에서 액세스할 수 있습니다.
* 연결 tooon 온-프레미스 데이터 센터는 기존의 VPN 장치를 사용 해야 합니다.
* 각 위치에서 hello 데이터베이스 tooother Azure에 복제 해야 하루에 한 번에 위치 합니다.

이러한 요구 사항에 따라, 응용 프로그램 계층 마다 하나의 서브넷을 사용 하 여 및 응용 프로그램별 toofilter 트래픽 Nsg를 사용 하 여 수 있습니다. 이런 방식으로 각 VNet에 3개의 서브넷(프런트 엔드, 응용 프로그램 계층 및 데이터 센터) 및 서브넷당 응용 프로그램당 1개 NSG만 포함합니다. Hello를 사용 해야 하는 경우에 **앱 당 Nsg 응용 프로그램 계층당 하나의 서브넷** 디자인 패턴. hello 아래 그림 hello 디자인 패턴을 나타내는 hello hello 사용 **ProdBU1US1** VNet입니다.

![계층당 1개 서브넷, 계층당 응용 프로그램당 1개 NSG](./media/virtual-network-vnet-plan-design-arm/figure11.png)

그러나 있어야 toocreate 추가 서브넷 hello Vnet 및 온-프레미스 데이터 센터 간에 VPN 연결 hello에 대 한 합니다. 및 각 서브넷에 대 한 toospecify hello 주소 공간이 필요 합니다. hello 아래 그림에 대 한 샘플 솔루션 **ProdBU1US1** VNet입니다. 각 VNet에 대해 이 시나리오를 복제합니다. 각 색상은 서로 다른 응용 프로그램을 나타냅니다.

![샘플 VNet](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**액세스 제어**

hello 다음 요구 사항은 관련된 tooaccess 제어:

* hello 회사의 네트워킹 그룹 있어야 hello VNet 구성에 대 한 모든 권한을 합니다.
* 각 사업부의 개발자 수 toodeploy Vm tooexisting 서브넷만 있어야 합니다.

이러한 요구 사항에 따라, 있습니다 수에서 사용자를 추가할 기본 제공 팀 toohello 네트워킹 hello **네트워크 참가자** ; 각 구독에 대 한 역할을 만들고 hello에 대 한 사용자 지정 역할 응용 프로그램 개발자가 제공 하는 각 구독에 이러한 권한 tooadd Vm tooexisting 서브넷입니다.

## <a name="next-steps"></a>다음 단계
* [가상 네트워크를 배포](virtual-networks-create-vnet-arm-template-click.md) 합니다.
* 너무 방법을 이해[부하를 분산](../load-balancer/load-balancer-overview.md) IaaS Vm 및 [여러 Azure 지역에 대 한 라우팅을 관리](../traffic-manager/traffic-manager-overview.md)합니다.
* 에 대 한 자세한 내용은 [Nsg 방법과 tooplan 및 디자인](virtual-networks-nsg.md) NSG 솔루션입니다.
* [크로스-프레미스 및 VNet 연결 옵션](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)에 대해 알아봅니다.
