---
title: "Azure에서 aaaIP 주소 유형을 | Microsoft Docs"
description: "Azure의 공용 및 개인 IP 주소에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>IP 주소 유형 및 Azure에서 할당 메서드
온-프레미스 네트워크를 다른 Azure 리소스와 IP 주소 tooAzure 리소스 toocommunicate를 할당할 수 있으며 인터넷 hello 있습니다. Azure에서 두 가지 유형의 IP 주소를 사용할 수 있습니다.

* **공용 IP 주소**: hello Azure 공용 웹 서비스를 포함 하 여 인터넷와의 통신에 사용 되는
* **개인 IP 주소**: Azure 가상 네트워크 (VNet) 내에서 통신에 사용 되 고 사용 하는 경우 VPN 게이트웨이 또는 express 경로 회로 tooextend 네트워크 tooAzure 온-프레미스 네트워크입니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](virtual-network-ip-addresses-overview-classic.md)합니다.
> 

Hello 클래식 배포 모델에 익숙한 경우 확인 hello [클래식 사이의 주소를 지정 하는 IP의 차이 및 리소스 관리자](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments)합니다.

## <a name="public-ip-addresses"></a>공용 IP 주소
공용 IP 주소와 같은 인터넷 및 Azure 공용 웹 서비스와 Azure 리소스 toocommunicate를 허용 [Azure Redis Cache](https://azure.microsoft.com/services/cache/), [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/), [SQL 데이터베이스](../sql-database/sql-database-technical-overview.md), 및 [Azure 저장소](../storage/common/storage-introduction.md)합니다.

Azure 리소스 관리자에서 [공용 IP](resource-groups-networking.md#public-ip-address) 주소는 고유 속성을 가진 리소스입니다. 다음 리소스는 hello를 사용 하 여 공용 IP 주소 리소스를 연결할 수 있습니다.

* VM(가상 컴퓨터)
* 인터넷 연결 부하 분산 장치
* VPN 게이트웨이
* 응용 프로그램 게이트웨이

### <a name="allocation-method"></a>할당 방법
IP 주소는 tooa을 할당 하는 데는 두 가지가 있습니다 *공용* IP 리소스- *동적* 또는 *정적*합니다. hello 기본 할당 메서드는 *동적*, 여기서 IP 주소는 **하지** hello 생성할 때 해당에 할당 합니다. 대신, 시작 (하거나 만들 때)에 연결 하는 hello 리소스 (예: VM 또는 부하 분산) hello 공용 IP 주소가 할당 됩니다. 중지 (또는 삭제) hello 리소스 hello IP 주소가 해제 됩니다. 이렇게 지정 하면 중지 하 고 리소스를 시작할 때 hello IP 주소 toochange 합니다.

tooensure hello IP 주소 hello 관련된 리소스 유지 hello 동일을 설정할 수 있습니다 hello 할당 방법을 명시적으로 너무*정적*합니다. 이 경우 IP 주소가 즉시 할당됩니다. Hello 리소스를 삭제 하거나도 해당 할당 방법 변경 하는 경우에 놓을 때*동적*합니다.

> [!NOTE]
> 도 설정한 경우 hello 할당 방법 너무*정적*, 실제 IP 주소 할당 toohello hello를 지정할 수 없습니다 *공용 IP 리소스*합니다. 할당 되는 대신, hello Azure 위치에에서 사용 가능한 IP 주소 풀에서 hello 리소스가에 만들어집니다.
>

고정 공용 IP 주소는 hello 다음 시나리오에서에서 일반적으로 사용 됩니다.

* 최종 사용자로 Azure 리소스 tooupdate 방화벽 규칙 toocommunicate가 필요합니다.
* DNS 이름을 확인, IP 주소를 변경하려면 A 레코드를 업데이트해야 하는 경우
* Azure 리소스가 IP 기반 보안 모델을 사용하는 다른 앱 또는 서비스와 통신하는 경우
* SSL 인증서 tooan 연결 된 IP 주소를 사용 합니다.

> [!NOTE]
> 에 있는 공용 IP 주소 (정적/동적) tooAzure 리소스가 할당 됩니다 하는 IP 범위 목록이 hello를 게시 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.
>

### <a name="dns-hostname-resolution"></a>DNS 호스트 이름 확인
에 대 한 매핑을 만듭니다 공용 IP 리소스에 대 한 DNS 도메인 이름 레이블을 지정할 수 있습니다 *domainnamelabel*. *위치*. hello Azure 관리 되는 DNS 서버에서 cloudapp.azure.com toohello 공용 IP 주소입니다. 예를 들어 있는 공용 IP 리소스를 만드는 경우 **contoso** 로 *domainnamelabel* hello에 **West US** Azure *위치*, hello 정규화 된 도메인 이름 (FQDN) **contoso.westus.cloudapp.azure.com** toohello hello 리소스 공용 IP 주소를 확인 합니다. 이 FQDN toocreate Azure에서 toohello 공용 IP 주소를 가리키는 사용자 지정 도메인 CNAME 레코드를 사용할 수 있습니다.

> [!IMPORTANT]
> 생성된 각 도메인 이름은 Azure 위치 내에서 고유해야 합니다.  
>

### <a name="virtual-machines"></a>가상 컴퓨터
공용 IP 주소와 연결할 수 있습니다는 [Windows](../virtual-machines/windows/overview.md) 또는 [Linux](../virtual-machines/virtual-machines-linux-about.md) tooits 할당 하 여 VM **네트워크 인터페이스**합니다. 여러 네트워크 인터페이스가 있는 VM의 경우 hello에에서 할당할 수 있습니다 toohello *기본* 네트워크 인터페이스에만 해당 합니다. 동적 또는 고정 공용 IP 주소 tooa VM 할당할 수 있습니다.

### <a name="internet-facing-load-balancers"></a>인터넷 연결 부하 분산 장치
공용 IP 주소와 연결할 수 있습니다는 [Azure 부하 분산 장치](../load-balancer/load-balancer-overview.md), toohello 할당 하 여 부하 분산 장치 **프런트 엔드** 구성 합니다. 이 공용 IP 주소는 부하 분산 VIP(가상 IP 주소)로 사용됩니다. 동적 또는 고정 공용 IP 주소 tooa 부하 분산 장치 프런트 엔드를 할당할 수 있습니다. 여러 공용 IP 주소 tooa 부하 분산 장치 프런트 엔드를 매핑함으로써를 지정할 수 있습니다 [다중 VIP](../load-balancer/load-balancer-multivip.md) 시나리오 같은 SSL 기반 웹 사이트를 사용 하 여 다중 테 넌 트 환경입니다.

### <a name="vpn-gateways"></a>VPN 게이트웨이
[Azure VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md) tooconnect 사용된 하는 Azure 가상 네트워크 (VNet) tooother Azure Vnet 또는 tooan 온-프레미스 네트워크입니다. 공용 IP 주소 tooits tooassign 필요한 **IP 구성** tooenable 것 hello 원격 네트워크와 toocommunicate 합니다. 현재만 할당할 수 있습니다는 *동적* 공용 IP 주소 tooa VPN 게이트웨이 합니다.

### <a name="application-gateways"></a>응용 프로그램 게이트웨이
Azure는 공용 IP 주소를 연결할 수 있는 [응용 프로그램 게이트웨이](../application-gateway/application-gateway-introduction.md), toohello 게이트웨이 할당 하 여 **프런트 엔드** 구성 합니다. 이 공용 IP 주소는 부하 분산 VIP로 사용됩니다. 현재만 할당할 수 있습니다는 *동적* 공용 IP 주소 tooan 응용 프로그램 게이트웨이 프런트 엔드 구성 합니다.

### <a name="at-a-glance"></a>요약
hello 표에서 관련된 tooa 최상위 리소스 및 hello 할당 방법 (동적 또는 정적 사용할 수 있는) 공용 IP 주소 수는 hello 특정 속성을 보여 줍니다.

| 최상위 리소스 | IP 주소 연결 | 않는 | 공용 |
| --- | --- | --- | --- |
| 가상 컴퓨터 |Linux |예 |예 |
| 부하 분산 장치 |프런트 엔드 구성 |예 |예 |
| VPN 게이트웨이 |게이트웨이 IP 구성 |예 |아니요 |
| 프런트 엔드 |프런트 엔드 구성 |예 |아니요 |

## <a name="private-ip-addresses"></a>개인 IP 주소
다른 리소스와 Azure 리소스 toocommunicate를 허용 하는 개인 IP 주소가 한 [가상 네트워크](virtual-networks-overview.md) 또는 VPN 게이트웨이 또는 인터넷 연결 가능한 IP 주소를 사용 하지 않고 ExpressRoute 회로 통해 온-프레미스 네트워크입니다.

Hello Azure 리소스 관리자 배포 모델 개인 IP 주소는 Azure 리소스의 종류에 따라 관련된 toohello입니다.

* VM
* 내부 부하 분산 장치(ILB)
* 응용 프로그램 게이트웨이

### <a name="allocation-method"></a>할당 방법
개인 IP 주소가 할당 된 hello 주소에서 연결 된 hello 서브넷 toowhich hello 리소스의 범위. 자체 hello 서브넷의 주소 범위 hello hello VNet의 주소 범위에 포함 됩니다.

개인 IP 주소를 할당하는 방법으로 *동적* 또는 *정적*이라는 두 가지 방법이 있습니다. hello 기본 할당 메서드는 *동적*, 여기서 hello IP 주소 (DHCP를 사용 하 여) hello 리소스의 서브넷에서 자동으로 할당 됩니다. 이 IP 주소 중지 하 고 hello 리소스를 시작할 때 변경할 수 있습니다.

너무 hello 할당 방법을 설정할 수 있습니다*정적* tooensure hello IP 주소 남아 hello 동일 합니다. 이 경우 tooprovide hello 리소스의 서브넷의 일부인 올바른 IP 주소 해야 있습니다.

정적 개인 IP 주소가 일반적으로 사용되는 대상은 다음과 같습니다.

* 도메인 컨트롤러 또는 DNS 서버 역할을 하는 VM
* IP 주소를 사용하는 방화벽 규칙이 필요한 리소스
* IP 주소를 통해 다른 앱/리소스에서 액세스하는 리소스

### <a name="virtual-machines"></a>가상 컴퓨터
개인 IP 주소 할당 toohello **네트워크 인터페이스** 의 [Windows](../virtual-machines/windows/overview.md) 또는 [Linux](../virtual-machines/virtual-machines-linux-about.md) VM입니다. 다중 네트워크 인터페이스 VM의 경우 각 인터페이스에 개인 IP 주소가 할당됩니다. 네트워크 인터페이스에 대 한 정적 또는 동적으로 hello 할당 방법을 지정할 수 있습니다.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>내부 DNS 호스트 이름 확인(VM)
모든 Azure VM은 명시적으로 사용자 지정 DNS 서버를 구성하지 않으면 기본적으로 [Azure 관리 DNS 서버](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) 로 구성됩니다. 이러한 DNS 서버 내에 있는 hello 같은 Vm에 대 한 내부 이름 확인을 제공 VNet 합니다.

VM을 만들 때 hello hostname tooits 개인 IP 주소에 대 한 매핑은 toohello Azure 관리 되는 DNS 서버 추가 됩니다. VM에는 여러 네트워크 인터페이스의 경우 hello hostname 매핑된 toohello hello 주 네트워크 인터페이스의 개인 IP 주소입니다.

Azure 관리 되는 DNS 서버와 구성 된 Vm에는 VNet tootheir 개인 IP 주소 내에서 모든 Vm의 수 tooresolve hello 호스트 이름이 됩니다.

### <a name="internal-load-balancers-ilb--application-gateways"></a>ILB(내부 부하 분산 장치) 및 응용 프로그램 게이트웨이
개인 IP 주소 toohello를 할당할 수 **프런트 엔드** 의 구성을 [Azure 내부 부하 분산 장치](../load-balancer/load-balancer-internal-overview.md) (ILB) 또는 [Azure 응용 프로그램 게이트웨이](../application-gateway/application-gateway-introduction.md)합니다. 이 개인 IP 주소가 역할의 내부 끝점을, 해당 가상 네트워크 (VNet) 및 hello 원격 네트워크에 액세스할 수 있는 유일한 toohello 리소스 toohello VNet를 연결 합니다. 동적 또는 정적 개인 IP 주소 toohello 프런트 엔드 구성 중 하나를 지정할 수 있습니다.

### <a name="at-a-glance"></a>요약
hello 표에서 관련된 tooa 최상위 리소스 및 hello 할당 방법 (동적 또는 정적 사용할 수 있는) 개인 IP 주소 수는 hello 특정 속성을 보여 줍니다.

| 최상위 리소스 | IP 주소 연결 | 않는 | 공용 |
| --- | --- | --- | --- |
| 가상 컴퓨터 |Linux |예 |예 |
| 부하 분산 장치 |프런트 엔드 구성 |예 |예 |
| 프런트 엔드 |프런트 엔드 구성 |예 |예 |

## <a name="limits"></a>제한
hello IP 주소 지정에 부과 된 제한에에서 표시 된 hello 전체 집합을 [네트워킹에 대 한 제한](../azure-subscription-service-limits.md#networking-limits) Azure에서. 이러한 제한은 지역별, 구독별로 적용됩니다. 할 수 있습니다 [지원에 문의](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 비즈니스 요구 사항에 따라 toohello 최대 한도를 tooincrease hello 기본 제한 값입니다.

## <a name="pricing"></a>가격
공용 IP 주소에는 명목 요금이 부과될 수 있습니다. azure에서 검토 hello 가격 toolearn IP에 대 한 주소 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지.

## <a name="next-steps"></a>다음 단계
* [Hello Azure 포털을 사용 하 여 고정 공용 IP 사용 하 여 VM 배포](virtual-network-deploy-static-pip-arm-portal.md)
* [템플릿을 사용하여 고정 공용 IP를 사용하는 VM 배포](virtual-network-deploy-static-pip-arm-template.md)
* [정적 개인 IP 주소로 hello Azure 포털을 사용 하 여 VM 배포](virtual-networks-static-private-ip-arm-pportal.md)
