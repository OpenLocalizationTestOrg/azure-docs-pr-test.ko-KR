---
title: "Azure (클래식)에서 주소 형식을 aaaIP | Microsoft Docs"
description: "Azure에서 공용 및 개인 IP 주소(기본)에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Azure의 IP 주소 유형 및 할당 방법
온-프레미스 네트워크를 다른 Azure 리소스와 IP 주소 tooAzure 리소스 toocommunicate를 할당할 수 있으며 인터넷 hello 있습니다. Azure에서 사용할 수 있는 IP 주소는 공용 및 개인의 두 종류가 있습니다.

공용 IP 주소는 인터넷, Azure 공용 웹 서비스를 포함 하 여 hello와의 통신에 사용 됩니다.

사용 하는 경우 VPN 게이트웨이 또는 express 경로 회로 tooextend 네트워크 tooAzure 개인 IP 주소는 Azure 가상 네트워크 (VNet), 클라우드 서비스 및 온-프레미스 네트워크 내에서 통신에 사용 됩니다.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 새로운 배포는 대부분 리소스 관리자를 사용하는 것이 좋습니다. 읽는 hello 여 리소스 관리자의 IP 주소에 대 한 자세한 내용은 [IP 주소](virtual-network-ip-addresses-overview-arm.md) 문서.

## <a name="public-ip-addresses"></a>공용 IP 주소
공용 IP 주소와 같은 인터넷 및 Azure 공용 웹 서비스와 Azure 리소스 toocommunicate를 허용 [Azure Redis Cache](https://azure.microsoft.com/services/cache/), [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/), [SQL 데이터베이스](../sql-database/sql-database-technical-overview.md), 및 [Azure 저장소](../storage/common/storage-introduction.md)합니다.

공용 IP 주소 리소스 유형에 따라 hello와 연관 되어 있습니다.

* 클라우드 서비스
* IaaS VM(가상 컴퓨터)
* PaaS 역할 인스턴스
* VPN 게이트웨이
* 응용 프로그램 게이트웨이

### <a name="allocation-method"></a>할당 방법
이 공용 IP 주소를 toobe tooan Azure 리소스를 할당 하면 *동적으로* 할당 된 풀의 사용 가능한 공용 IP 주소 hello 위치 hello 리소스 내에서 만들어집니다. 이 IP 주소는 hello 리소스 중지 될 때 해제 됩니다. 클라우드 서비스의 이러한 모든 hello 역할 인스턴스가 중지 되 면 하는 경우를 방지할 수 있습니다를 사용 하 여 한 *정적* (예약 된) IP 주소 (참조 [클라우드 서비스](#Cloud-services)).

> [!NOTE]
> 에 있는 공용 IP 주소 리소스가 할당 됩니다. tooAzure IP 범위 목록이 hello를 게시 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.
> 
> 

### <a name="dns-hostname-resolution"></a>DNS 호스트 이름 확인
클라우드 서비스 또는 IaaS VM을 만들 tooprovide은 Azure에서 모든 리소스에서 고유 클라우드 서비스 DNS 이름을 필요 합니다. 그러면 매핑이 만들어집니다 hello에 Azure 관리 되는 DNS 서버에 대 한 *dnsname*. hello 리소스의 cloudapp.net toohello 공용 IP 주소입니다. 예를 들어, 만들 때 클라우드 서비스의 클라우드 서비스 DNS 이름을 가진 **contoso**, hello 정규화 된 도메인 이름 (FQDN) **contoso.cloudapp.net** tooa의 공용 IP 주소 (VIP)를 확인 하 되 hello 클라우드 서비스입니다. 이 FQDN toocreate Azure에서 toohello 공용 IP 주소를 가리키는 사용자 지정 도메인 CNAME 레코드를 사용할 수 있습니다.

### <a name="cloud-services"></a>클라우드 서비스
클라우드 서비스는 항상 된 공용 IP 주소 참조 tooas 가상 IP 주소 (VIP)를 가집니다. 클라우드 서비스 tooassociate 서로 다른 포트에서 Vm 및 역할 인스턴스 hello 클라우드 서비스 내에서 hello VIP toointernal 포트의 끝점을 만들 수 있습니다. 

클라우드 서비스에 여러 IaaS Vm이 포함 될 수 있습니다 또는 PaaS 역할 인스턴스를 통해 노출 된 모든 hello 동일한 클라우드 서비스 VIP 합니다. 할당할 수도 있습니다 [여러 Vip tooa 클라우드 서비스](../load-balancer/load-balancer-multivip.md)는 다중 테 넌 트 환경 SSL 기반 웹 사이트와 다중 VIP 시나리오를 사용 합니다.

클라우드 서비스의 공용 IP 주소 hello hello를 사용 하 여 역할 인스턴스를 hello 모든 경우에 동일가 중지 된 상태로 유지 됩니다 되도록 할 수 있습니다는 *정적* 공용 IP 주소, 참조 tooas [예약 된 IP](virtual-networks-reserved-public-ip.md)합니다. 특정 위치에 (예약 됨된) 정적 IP 리소스를 만들고 해당 위치에 클라우드 서비스 tooany 할당할 수 있습니다. Hello 예약 된 IP에 대 한 hello 실제 IP 주소를 지정할 수 없습니다, 그리고 만들어질 hello 위치에 사용 가능한 IP 주소 풀에서 할당 됩니다. 이 IP 주소는 명시적으로 삭제될 때까지 해제되지 않습니다.

여기서는 클라우드 서비스 (예약 됨된) 고정 공용 IP 주소는 hello 시나리오에서 일반적으로 사용 됩니다.

* 방화벽 규칙 toobe 설치 프로그램을 최종 사용자가 필요합니다.
* 외부 DNS 이름 확인에 따라 달라지며, 동적 IP를 위해 A 레코드 업데이트가 필요한 경우
* IP 기반 보안 모델을 사용하는 외부 웹 서비스를 사용하는 경우
* SSL 인증서 tooan 연결 된 IP 주소를 사용 합니다.

> [!NOTE]
> 클래식 VM을 만들 때 컨테이너 *클라우드 서비스* 가 Azure에 의해 만들어지며 VIP(가상 IP 주소)를 포함합니다. RDP 또는 SSH 기본 포털을 통해 hello 만들기를 수행 하는 경우 *끝점* toohello VM 클라우드 서비스 VIP hello 통해 연결할 수 있도록 hello 포털에서 구성 됩니다. 예약 된 IP 주소 tooconnect toohello VM을 효과적으로 제공 하는이 클라우드 서비스 VIP은 예약할 수 있는 합니다. 더 많은 끝점을 구성하여 추가 포트를 열 수 있습니다.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>IaaS VM 및 PaaS 역할 인스턴스
공용을 할당할 수 IP 주소 직접 tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 클라우드 서비스 내에서 PaaS 역할 인스턴스. 이 참조 된 tooas 인스턴스 수준 공용 IP 주소 ([ILPIP](virtual-networks-instance-level-public-ip.md)). 이 공용 IP 주소는 동적 방식만 가능합니다.

> [!NOTE]
> 이 PaaS 또는 IaaS Vm 역할 인스턴스에 대 한 컨테이너 역할 hello 클라우드 서비스의 VIP hello 다릅니다, 동일한 클라우드 서비스 VIP는 클라우드 서비스에는 여러 IaaS Vm 또는 PaaS 역할 인스턴스를 모두 노출된 hello를 통해 포함 될 수 있으므로 합니다.
> 
> 

### <a name="vpn-gateways"></a>VPN 게이트웨이
A [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md) 사용된 tooconnect Azure VNet tooother Azure Vnet 또는 온-프레미스 네트워크가 될 수 있습니다. VPN 게이트웨이 공용 IP 주소를 할당 된 *동적으로*, hello 원격 네트워크와 통신할 수 있도록입니다.

### <a name="application-gateways"></a>응용 프로그램 게이트웨이
Azure [응용 프로그램 게이트웨이](../application-gateway/application-gateway-introduction.md) Layer7 HTTP에 따라 tooroute 네트워크 트래픽 부하 분산에 사용할 수 있습니다. 응용 프로그램 게이트웨이 공용 IP 주소를 할당 된 *동적으로*, 하는 해당 역할을 부하 분산 된 VIP hello 합니다.

### <a name="at-a-glance"></a>개요
hello 아래 표에 hello 할당 메서드 (동적/정적) 및 기능 tooassign와 각 리소스 유형에 여러 공용 IP 주소가 있습니다.

| 리소스 | 동적 | 정적 | 여러 IP 주소 |
| --- | --- | --- | --- |
| 클라우드 서비스 |예 |예 |예 |
| IaaS VM 또는 PaaS 역할 인스턴스 |예 |아니요 |아니요 |
| VPN 게이트웨이 |예 |아니요 |아니요 |
| 응용 프로그램 게이트웨이 |예 |아니요 |아니요 |

## <a name="private-ip-addresses"></a>개인 IP 주소
클라우드 서비스에서 다른 리소스와 Azure 리소스 toocommunicate를 허용 하는 개인 IP 주소가 또는 [가상 네트워크](virtual-networks-overview.md)(VNet) 또는 사용 하지 않고 VPN 게이트웨이 또는 express 경로 회로) (통해 tooon 온-프레미스 네트워크는 인터넷 연결 가능한 IP 주소입니다.

Azure 클래식 배포 모델에서 개인 IP 주소가 Azure 리소스를 따라 toohello를 할당할 수 있습니다.

* IaaS VM 및 PaaS 역할 인스턴스
* 내부 부하 분산 장치
* 응용 프로그램 게이트웨이

### <a name="iaas-vms-and-paas-role-instances"></a>IaaS VM 및 PaaS 역할 인스턴스
Hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터 (Vm)은 항상 유사한 tooPaaS 역할 인스턴스가 클라우드 서비스에 저장 됩니다. 개인 IP 주소의 hello 동작 하므로 이러한 리소스에 대 한 비슷합니다.

클라우드 서비스 일 수 있는 중요 한 toonote는 두 가지 방법으로 배포 합니다.

* 가상 네트워크 내에 있지 않은 *독립 실행형* 클라우드 서비스로 배포
* 가상 네트워크의 일부로 배포

#### <a name="allocation-method"></a>할당 방법
경우에 *독립 실행형* 클라우드 서비스, 개인 IP 주소를 할당 하는 리소스 가져오기 *동적으로* hello Azure 데이터 센터의 개인 IP 주소 범위입니다. 사용할 수 있도록 동일한 클라우드 서비스 hello 내 다른 Vm과 통신에만 합니다. 이 IP 주소는 hello 리소스 중지 되 고 시작 하는 경우 변경할 수 있습니다.

리소스 가져오기 개인 가상 네트워크 내에 배포 된 클라우드 서비스의 경우 hello의 hello 주소 범위에서 할당 된 IP 주소 서브넷 (지정 된 대로 네트워크 구성에서) 연결입니다. 이 개인 IP 주소 hello VNet 내의 모든 Vm 간의 통신에 사용할 수 있습니다.

또한 VNet 내 클라우드 서비스의 경우 기본적으로 개인 IP 주소가 (DHCP를 사용하여) *동적으로* 할당됩니다. Hello 리소스 중지 되 고 시작 하는 경우 변경할 수는 있습니다. 동일한 tooensure hello IP 주소 남아 hello, 너무 tooset hello 할당 방법을 사용 해야*정적*, hello 해당 주소 범위 내 올바른 IP 주소를 제공 합니다.

정적 개인 IP 주소가 일반적으로 사용되는 대상은 다음과 같습니다.

* 도메인 컨트롤러 또는 DNS 서버 역할을 하는 VM
* IP 주소를 사용하는 방화벽 규칙이 필요한 VM
* IP 주소를 통해 다른 앱에서 액세스하는 서비스를 실행 중인 VM

#### <a name="internal-dns-hostname-resolution"></a>내부 DNS 호스트 이름 확인
모든 Azure VM 및 PaaS 역할 인스턴스는 명시적으로 사용자 지정 DNS 서버를 구성하지 않으면 기본적으로 [Azure 관리 DNS 서버](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) 로 구성됩니다. 역할 인스턴스 내에 있는 hello 동일한 VNet 또는 클라우드 서비스 및 이러한 DNS 서버 Vm에 대 한 내부 이름 확인을 제공 합니다.

VM을 만들 때 hello hostname tooits 개인 IP 주소에 대 한 매핑은 toohello Azure 관리 되는 DNS 서버 추가 됩니다. 다중 NIC VM의 경우 hello hostname 매핑된 toohello hello 기본 NIC.의 개인 IP 주소 그러나이 매핑 정보는 제한 된 tooresources 동일한 hello 내에서 클라우드 서비스 또는 VNet 합니다.

경우에 *독립 실행형* 클라우드 서비스, 수 tooresolve hostnames 됩니다 hello 내에서 모든 Vm/역할 인스턴스의 동일한 클라우드 서비스에만 해당 합니다. VNet 내에서 클라우드 서비스의 경우 hello VNet 내의 모든 hello Vm/역할 인스턴스 수 tooresolve 호스트 이름이 됩니다.

### <a name="internal-load-balancers-ilb--application-gateways"></a>ILB(내부 부하 분산 장치) 및 응용 프로그램 게이트웨이
개인 IP 주소 toohello를 할당할 수 **프런트 엔드** 의 구성을 [Azure 내부 부하 분산 장치](../load-balancer/load-balancer-internal-overview.md) (ILB) 또는 [Azure 응용 프로그램 게이트웨이](../application-gateway/application-gateway-introduction.md)합니다. 이 개인 IP 주소가 역할의 내부 끝점을, 해당 가상 네트워크 (VNet) 및 hello 원격 네트워크에 액세스할 수 있는 유일한 toohello 리소스 toohello VNet를 연결 합니다. 동적 또는 정적 개인 IP 주소 toohello 프런트 엔드 구성 중 하나를 지정할 수 있습니다. 또한 여러 개인 IP 주소 tooenable 다중 vip 시나리오를 할당할 수 있습니다.

### <a name="at-a-glance"></a>개요
hello 표에서 hello 할당 메서드 (동적/정적) 및 기능 tooassign와 각 리소스 유형에 여러 개인 IP 주소를 보여 줍니다.

| 리소스 | 동적 | 정적 | 여러 IP 주소 |
| --- | --- | --- | --- |
| VM( *독립 실행형* 클라우드 서비스 내) |예 |예 |예 |
| PaaS 역할 인스턴스( *독립 실행형* 클라우드 서비스 내) |예 |아니요 |예 |
| VM 또는 PaaS 역할 인스턴스(VNet 내) |예 |예 |예 |
| 내부 부하 분산 장치 프런트 엔드 |예 |예 |예 |
| 응용 프로그램 게이트웨이 프런트 엔드 |예 |예 |예 |

## <a name="limits"></a>제한
hello 아래 표에 IP에서 부과 하는 hello 제한은 구독 당 Azure에서 주소를 지정 합니다. 할 수 있습니다 [지원에 문의](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 비즈니스 요구 사항에 따라 toohello 최대 한도를 tooincrease hello 기본 제한 값입니다.

|  | 기본 제한 | 최대 제한 |
| --- | --- | --- |
| 공용 IP 주소(동적) |5 |지원에 문의 |
| 예약된 공용 IP 주소 |20 |지원에 문의 |
| 배포당 공용 VIP(클라우드 서비스) |5 |지원에 문의 |
| 배포당 개인 VIP(ILB)(클라우드 서비스) |1 |1 |

Hello 전체 집합을 읽어야 [네트워킹에 대 한 제한](../azure-subscription-service-limits.md#networking-limits) Azure에서.

## <a name="pricing"></a>가격
대부분의 경우에 공용 IP 주소는 무료입니다. Toouse 추가 및/또는 고정 공용 IP 주소 명목 요금이 청구가 않습니다. Hello 이해 [공용 Ip에 대 한 가격 구조](https://azure.microsoft.com/pricing/details/ip-addresses/)합니다.

## <a name="differences-between-resource-manager-and-classic-deployments"></a>리소스 관리자와 클래식 배포 간 차이점
다음은 리소스 관리자 및 hello 클래식 배포 모델의 IP 주소 지정 기능 비교입니다.

|  | 리소스 | 클래식 | 리소스 관리자 |
| --- | --- | --- | --- |
| **공용 IP 주소** |***VM*** |참조 된 tooas는 ILPIP (동적에만 해당) |참조 tooas 된 공용 IP (동적 또는 정적) |
|  ||할당 된 tooan IaaS VM 또는 PaaS 역할 인스턴스 |연결 된 toohello VM NIC | |
|  |***인터넷 연결 부하 분산 장치*** |Tooas 또는 예약 된 IP (정적)의 VIP (동적)를 참조합니다. |참조 tooas 된 공용 IP (동적 또는 정적) | |
|  ||할당 된 tooa 클라우드 서비스 |연결 된 toohello 부하 분산 장치의 프런트 엔드 구성 | |
|  | | | |
| **개인 IP 주소** |***VM*** |DIP는 참조 된 tooas |Tooas 개인 IP 주소를 참조합니다. |
|  ||할당 된 tooan IaaS VM 또는 PaaS 역할 인스턴스 |할당 된 toohello VM NIC | |
|  |***ILB(내부 부하 분산 장치)*** |할당 된 toohello ILB (동적 또는 정적) |할당 된 toohello ILB 프런트 엔드 구성 (동적 또는 정적) | |

## <a name="next-steps"></a>다음 단계
* [개인 고정 IP 주소를 사용 하 여 VM 배포](virtual-networks-static-private-ip-classic-pportal.md) Azure 포털 hello를 사용 하 여 합니다.

