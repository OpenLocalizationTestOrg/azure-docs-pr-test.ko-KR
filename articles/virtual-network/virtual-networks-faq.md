---
title: "가상 네트워크 FAQ aaaAzure | Microsoft Docs"
description: "Microsoft Azure 가상 네트워크에 대 한 가장 자주 묻는 질문 답변 toohello 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Azure Virtual Network FAQ(질문과 대답)

## <a name="virtual-network-basics"></a>Virtual Network 기본 사항

### <a name="what-is-an-azure-virtual-network-vnet"></a>Azure VNet(Virtual Network)이란?
Azure 가상 네트워크 (VNet)는 hello 클라우드에서 사용자의 네트워크의 표현입니다. Azure 클라우드 전용 tooyour 구독 hello의 논리적 격리는 Vnet tooprovision를 사용 하 고 Azure 및 필요에 따라 링크 hello Azure의 다른 Vnet 또는 온-프레미스 Vnet에서 가상 사설망 (Vpn)을 관리할 수 있습니다 IT 인프라 toocreate 크로스-프레미스 또는 하이브리드 솔루션입니다. 각 VNet을 만들 자체 CIDR 블록 있으며 연결 된 tooother hello CIDR 블록 겹치지 않고으로 Vnet 및 온-프레미스 네트워크가 될 수 있습니다. 갖게 Vnet에 대 한 DNS 서버 설정의 제어 및 hello VNet 서브넷으로 구분 됩니다.

VNet을 다음에 사용합니다.

* 전용 사설 클라우드 전용 VNet을 만듭니다. 경우에 따라 솔루션에 대해 프레미스간 구성이 필요하지 않을 수 있습니다. VNet을 만들 때 서비스와 VNet 내의 Vm 수 직접 안전 하 게 서로 통신할 hello 클라우드에서 합니다. 이 트래픽을 hello VNet 내에서 안전 하 게 유지 하지만 여전히 hello Vm 및 솔루션의 일부로 인터넷 통신이 필요한 서비스에 대 한 tooconfigure 끝점 연결 합니다.
* 데이터 센터와 Vnet을 안전 하 게 확장, 기존의 사이트 간 (S2S) Vpn toosecurely 눈금의 데이터 센터 용량 빌드할 수 있습니다. S2S Vpn IPSEC tooprovide 여 회사 VPN 게이트웨이와 Azure 간 보안 연결을 사용합니다.
* 하이브리드 클라우드 시나리오 Vnet 제공 유연성 toosupport 다양 한 하이브리드 클라우드 시나리오를 hello를 사용 하도록 설정 합니다. 클라우드 기반 응용 프로그램 tooany 온-프레미스 시스템 유형 같은 메인프레임 및 Unix 시스템 안전 하 게 연결할 수 있습니다.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>VNet이 필요한 경우를 어떻게 알 수 있을까요?
hello [가상 네트워크 개요](virtual-networks-overview.md) 문서 hello 최적의 네트워크 디자인 옵션을 결정 하는 데 도움이 되는 의사 결정 테이블을 제공 합니다.

### <a name="how-do-i-get-started"></a>어떻게 시작하나요?
Hello 방문 [가상 네트워크 설명서](https://docs.microsoft.com/azure/virtual-network/) tooget 시작 합니다. 이 콘텐츠는 모든 hello VNet 기능에 대 한 개요 및 배포 정보를 제공합니다.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>크로스-프레미스 연결 없이 VNet을 사용할 수 있습니까?
예. 하이브리드 연결을 사용하지 않고 VNet을 사용할 수 있습니다. Toorun Microsoft Windows Server Active Directory 도메인 컨트롤러와 Azure에서 SharePoint 팜을 하려는 경우 특히 유용 합니다.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>VNet 간 또는 VNet과 온-프레미스 데이터 센터 간에 WAN 최적화를 수행할 수 있습니까?

예. 배포할 수는 [WAN 최적화 네트워크 가상 어플라이언스](https://azure.microsoft.com/marketplace/?term=wan+optimization) hello Azure 마켓플레이스를 통해 여러 공급 업체에서 합니다.

## <a name="configuration"></a>구성

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>도구 수행할 toocreate VNet을 사용 합니까?
다음 도구 toocreate hello를 사용 하 여 하거나 VNet을 구성할 수 있습니다.

* Azure 포털(클래식 및 리소스 관리자 VNet용)
* 네트워크 구성 파일(netcfg - 클래식 VNet 전용) Hello 참조 [네트워크 구성 파일을 사용 하 여 VNet 구성](virtual-networks-using-network-configuration-file.md) 문서.
* PowerShell(클래식 및 리소스 관리자 VNet용)
* Azure CLI(클래식 및 리소스 관리자 VNet용)

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>VNet 내에서 사용할 수 있는 주소 범위는 무엇입니까?
[RFC 1918](http://tools.ietf.org/html/rfc1918)에 정의되어 있는 모든 IP 주소 범위를 사용할 수 있습니다. 예를 들어 10.0.0.0/16을 사용할 수 있습니다.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>VNet 내에서 공용 IP 주소를 가질 수 있습니까?
예. 공용 IP 주소 범위에 대 한 자세한 내용은 참조 hello [가상 네트워크의 공용 IP 주소 공간](virtual-networks-public-ip-within-vnet.md) 문서. 공용 IP 주소는 hello 인터넷에서에서 직접 액세스할 수 있는 되지 않습니다.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>VNet 내에서 서브넷의 수는 제한 toohello 거기?
예. 읽기 hello [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 을 참조 합니다. 서브넷 주소 공간은 서로 겹칠 수 없습니다.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>이러한 서브넷 내에서 IP 주소를 사용하는데 제한 사항이 있습니까?
예. Azure는 각 서브넷 내의 일부 IP 주소를 예약합니다. hello hello 서브넷의 첫 번째 및 마지막 IP 주소가 예약 되어 Azure 서비스에 사용 되는 3 더 많은 주소와 함께 프로토콜 적합성을 위해 있습니다.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>VNet 및 서브넷은 얼마나 크고 얼마나 작을 수 있습니까?
지원 hello 가장 작은 서브넷은 / 29 및 hello 가장 큰 서브넷 은/8 (CIDR 서브넷 정의 사용).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>Vnet을 사용 하 여 내 Vlan tooAzure를 가져올 수 있습니까?
아니요. VNet은 계층 3 오버레이입니다. Azure는 모든 계층 2 의미 체계를 지원하지 않습니다.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>VNet 및 서브넷에 사용자 지정 라우팅 정책을 지정할 수 있습니까?
예. UDR(사용자 정의 라우팅)을 사용할 수 있습니다. UDR에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](virtual-networks-udr-overview.md)을 참조하세요.

### <a name="do-vnets-support-multicast-or-broadcast"></a>VNet은 멀티 캐스트 또는 브로드캐스트를 지원합니까?
아니요. 멀티 캐스트 또는 브로드캐스트는 지원하지 않습니다.

### <a name="what-protocols-can-i-use-within-vnets"></a>VNet 내에서 사용할 수 있는 프로토콜은 무엇입니까?
VNet 내에서 TCP, UDP 및 ICMP TCP/IP 프로토콜을 사용할 수 있습니다. 멀티 캐스트, 브로드캐스트, IP-IP 캡슐화 패킷 및 GRE(일반 라우팅 캡슐화) 패킷은 VNet 내에서 차단됩니다. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>내 기본 라우터를 VNet 내에서 ping할 수 있습니까?
아니요.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>Tracert toodiagnose 연결을 사용할 수 있습니까?
아니요.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>Hello VNet을 만든 후 서브넷을 추가할 수 있습니까?
예. 서브넷 추가할 수 있습니다 tooVNets 언제 든 지도 hello 서브넷 주소 hello VNet에 있는 다른 서브넷의 일부가 아닙니다.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>만들 I 후 내 서브넷의 hello 크기를 수정할 수 있습니까?
예. VNet 내에서 배포된 VM 또는 서비스가 없는 경우 서브넷을 추가, 제거, 확장 또는 축소할 수 있습니다.

### <a name="can-i-modify-subnets-after-i-created-them"></a>서브넷을 만든 후 수정할 수 있습니까?
예. 추가, 제거 하 고 VNet에서 사용 하는 hello CIDR 블록을 수정할 수 있습니다.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>에 연결할 수 있습니까 toohello 내 서비스 VNet에서 실행 하는 경우 인터넷?
예. VNet 내에 배포 된 모든 서비스 toohello 연결할 수 인터넷 합니다. Azure에 배포 된 모든 클라우드 서비스에는 공개적으로 주소 지정 가능한 VIP tooit 할당 되어 있습니다. 나면 toodefine PaaS 역할에 대 한 입력된 끝점 및 tooenable 가상 컴퓨터에 대 한 끝점 hello에서 이러한 서비스 tooaccept 연결 인터넷 합니다.

### <a name="do-vnets-support-ipv6"></a>VNet은 IPv6를 지원합니까?
아니요. VNet과 함께 IPv6를 사용할 수 없습니다.

### <a name="can-a-vnet-span-regions"></a>VNet을 사용하여 지역을 확장할 수 있습니까?
아니요. VNet은 제한 된 tooa 단일 영역.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>VNet tooanother Azure의 VNet에에서 연결할 수 있습니까?
예. VNet tooanother VNet를 수행 하 여 연결할 수 있습니다.
- Azure VPN Gateway. 읽기 hello [VNet 대 VNet 연결 구성](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 을 참조 합니다. 
- VNet 피어링. 읽기 hello [VNet 피어 링 개요](virtual-network-peering-overview.md) 을 참조 합니다.

## <a name="name-resolution-dns"></a>이름 확인(DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>VNet에 대한 DNS 옵션은 무엇입니까?
Hello에 사용 하 여 hello 의사 결정 테이블 [Vm 및 역할 인스턴스에 대 한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) DNS hello 모든 페이지 tooguide 사용할 수 있는 옵션이 있습니다.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>VNet에 대한 DNS 서버를 지정할 수 있습니까?
예. Hello VNet 설정에서 DNS 서버 IP 주소를 지정할 수 있습니다. 이것으로 적용 됩니다 hello 기본 DNS 서버 hello VNet에 있는 모든 Vm에 대 한 합니다.

### <a name="how-many-dns-servers-can-i-specify"></a>얼마나 많은 DNS 서버 수를 지정할 수 있습니까?
참조 hello [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 을 참조 합니다.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>Hello 네트워크 만든 후 내 DNS 서버를 수정할 수 있습니까?
예. 언제 든 지 VNet에 대 한 hello DNS 서버 목록을 변경할 수 있습니다. DNS 서버 목록을 변경 하면 toopick hello 새 DNS 서버를 위해에서 VNet에서 각 toorestart hello vm 해야 합니다.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Azure에서 제공하는 DNS란 무엇이며 VNet으로 작동합니까?
Azure에서 제공하는 DNS는 Microsoft에서 제공하는 다중 테넌트 DNS 서비스입니다. Azure는 이 서비스에 모든 VM 및 클라우드 서비스 역할 인스턴스를 등록합니다. 이 서비스 호스트 이름으로 Vm 및 클라우드 서비스를 동일 하 고 Vm 및 역할 인스턴스는 FQDN으로 hello 같은 hello 내에 포함 된 역할 인스턴스에 대 한 이름 확인을 제공 VNet입니다. 읽기 hello [Vm 및 역할 인스턴스에 대 한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) DNS에 대 한 자세한 문서 toolearn 합니다.

> [!NOTE]
> 에 없는 경우이 시간 toohello 제한 처음 100 개의 클라우드 서비스가 Azure 제공 DNS를 사용 하 여 테 넌 트 간 이름 확인을 위해 VNet 사용자 고유의 DNS 서버를 사용하는 경우 이러한 제한이 적용되지 않습니다.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>VM 당/서비스 단위로 DNS 설정을 재정의할 수 있습니까?
예. 클라우드 서비스 단위로 toooverride hello 기본 네트워크 설정에 DNS 서버를 설정할 수 있습니다. 그러나 가능한 한 네트워크 차원 DNS를 사용하는 것이 좋습니다.

### <a name="can-i-bring-my-own-dns-suffix"></a>고유한 DNS 접미사를 가져올 수 있습니까?
아니요. VNet에 대해 사용자 지정 DNS 접미사를 지정할 수 없습니다.

## <a name="connecting-virtual-machines"></a>가상 컴퓨터 연결

### <a name="can-i-deploy-vms-tooa-vnet"></a>Vm tooa VNet을 배포할 수 있습니까?
예. 모든 네트워크 인터페이스 (NIC) 연결 된 tooa hello 리소스 관리자 배포 모델을 통해 배포 된 VM에 연결 된 VNet tooa 이어야 합니다. Hello 클래식 배포 모델을 통해 배포 된 Vm에 연결 된 VNet tooa 선택적 될 수 있습니다.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Hello 다른 유형 이란 IP 주소의 tooVMs를 할당할 수 있습니까?
* **비공개:** tooeach 각 VM 내의 NIC를 할당 합니다. hello 정적 또는 동적 방법 중 하나를 사용 하 여 hello 주소가 할당 됩니다. 개인 IP 주소는 VNet의 hello 서브넷 설정에 지정 된 hello 범위에서 할당 됩니다. Hello 클래식 배포 모델을 통해 배포 된 리소스는 연결 되어 있지 않은 경우에 개인 IP 주소를 할당 된 VNet tooa 합니다. Hello 리소스 삭제 될 때까지 할당 hello 동적 메서드가 유지 된 개인 IP 주소 할당 tooa 리소스 (Vm 이나 클라우드 서비스 배포 슬롯). Hello에 된 (할당 취소) 상태를 중지 한 후에 VM이 다시 시작 하는 경우 hello 동적 메서드를 사용 하 여 할당할 개인 IP 주소가 변경 될 수 있습니다. Hello 리소스 삭제 될 때까지 hello 정적 메서드 할당 된 상태로 유지 됩니다. tooa 리소스를 사용 하 여 할당할 개인 IP 주소입니다. Tooensure 해야 할 경우 hello 리소스 삭제 될 때까지 해당 hello 개인 IP 주소 리소스를 변경 하지 않습니다, hello 정적 메서드로 개인 IP 주소를 할당 합니다.
* **공용:** 선택적으로 할당 된 tooNICs tooVMs hello Azure 리소스 관리자 배포 모델을 통해 배포를 연결 합니다. hello 정적 또는 동적 할당 방법으로 hello 주소를 할당할 수 있습니다. 지정 된 클라우드 서비스 내에 존재 hello 클래식 배포 모델을 통해 배포 된 모든 Vm 및 클라우드 서비스 역할 인스턴스는 *동적*, 공용 가상 IP (VIP) 주소입니다. [예약된 IP 주소](virtual-networks-reserved-public-ip.md)라고 하는 공용 *정적* IP 주소는 필요에 따라 VIP로 할당될 수 있습니다. 공용 IP 주소 tooindividual hello 클래식 배포 모델을 통해 배포 된 클라우드 서비스 또는 Vm 역할 인스턴스를 할당할 수 있습니다. 이러한 주소는 [ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소라고 하며 동적으로 할당될 수 있습니다.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>나중에 만들 VM에 대한 개인 IP 주소를 예약할 수 있습니까?
아니요. 개인 IP 주소를 예약할 수 없습니다. 개인 IP 주소를 사용할 수 있는 경우 할당 됩니다 tooa VM 또는 역할 인스턴스에 hello DHCP 서버에서 합니다. VM 이거나 아닐 수 hello 개인 IP 주소 toobe에 할당 하는 hello 합니다. 그러나 hello 개인 IP 주소는 이미 만들어진 VM tooany 사용 가능한 개인 IP 주소를 변경할 수 있습니다.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>VNet에서 VM에 대한 개인 IP 주소가 변경됩니까?
경우에 따라 다릅니다. 동적 개인 IP 주소는 중지(할당 취소) 또는 삭제될 때까지 VM과 함께 유지됩니다. 정적 개인 IP 주소는 삭제될 때까지 VM에서 해제되지 않습니다.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>수동으로 hello VM 운영 체제 내에서 IP 주소 tooNICs를 할당할 수 있습니까?
예, 하지만 권장되지 않습니다. Hello IP 주소 할당 hello Azure VM 내의 NIC tooa toochange 되었으면 VM의 운영 체제 내에서 NIC에 대 한 hello IP 주소를 수동으로 변경 toolosing 연결 toohello VM 잠재적으로 발생할 수 있습니다.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Toomy IP 주소는 클라우드 서비스 배포 슬롯 또는 종료 hello 운영 체제 내에서 VM 중지 하 게 하려면 어떻게 됩니까?
아무 일도 일어나지 않습니다. hello IP 주소 (공용 VIP를, 공용 및 개인) 클라우드 서비스 배포 슬롯을 할당된 toohello 또는 VM에 남아 있습니다. VM이 중지(할당 취소) 또는 삭제되거나 클라우드 서비스 배포 슬롯이 삭제되는 경우에만 동적 주소가 해제됩니다. 클릭 하 여 hello **중지** 해당 상태 tooStopped (할당 취소 됨)을 설정 하는 hello Azure 포털 내에서 VM에 대 한 단추입니다. 이 경우 hello VM의 IP 주소는 손실 됩니다.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>이동할 수 있습니까 Vm의 VNet 서브넷 tooanother 서브넷 1 개에서 다시 배포 하지 않고?
예. Hello에 자세한 정보를 찾을 수 [어떻게 toomove VM 또는 역할 인스턴스 tooa 다른 서브넷](virtual-networks-move-vm-role-to-subnet.md) 문서.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>VM에 대해 정적 MAC 주소를 구성할 수 있습니까?
아니요. MAC 주소를 정적으로 구성할 수 없습니다.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>MAC 주소 hello 남습니다 만든 후 같은 VM에 대 한 hello?
예, MAC 주소 hello hello 삭제 될 때까지 클래식 배포 모델 및 hello 리소스 관리자를 통해 배포 하는 VM에 대해 동일한 상태로 유지 됩니다. 이전에 MAC 주소 hello hello VM 중지 되었습니다 (할당 취소) 하지만 hello MAC 주소가 hello VM 상태를 할당 취소 하는 hello에 있을 경우에 그대로 유지 됩니다 이제 해제 되었습니다.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>에 연결할 수 있습니까 toohello VNet에 VM에서 인터넷?
예. VNet 내에 배포 된 모든 Vm 및 클라우드 서비스 역할 인스턴스 toohello 인터넷에 연결할 수 있습니다.

## <a name="azure-services-that-connect-toovnets"></a>TooVNets 연결 하는 azure 서비스

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>VNet에 Azure App Service Web Apps를 사용할 수 있습니까?
예. ASE(앱 서비스 환경)를 사용하여 VNet 내부에 Web Apps를 배포할 수 있습니다. VNet에 대해 지점 및 사이트 간 연결이 구성된 경우 Azure VNet에서 모든 Web Apps를 안전하게 연결하고 리소스에 액세스할 수 있습니다. 자세한 내용은 다음 문서는 hello 참조:

* [앱 서비스 환경에서 웹앱 만들기](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Azure Virtual Network에 앱 통합](../app-service-web/web-sites-integrate-with-vnet.md)
* [웹앱을 통해 VNet 통합 및 하이브리드 연결 사용](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>VNet에서 웹 및 작업자 역할(PaaS)을 사용하여 Cloud Services를 배포할 수 있습니까?
예. (선택 사항) VNet 내에서 Cloud Services 역할 인스턴스를 배포할 수 있습니다. toodo 따라서 hello 네트워크 구성 섹션 서비스 구성의 hello VNet 이름 및 hello 역할/서브넷 매핑을 지정 합니다. 않아도 tooupdate 이진 파일입니다.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>가상 컴퓨터 크기 조정 설정 (VMSS) tooa VNet에 연결할 수 있습니까?
예. VMSS tooa VNet를 연결 해야 합니다.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>서비스를 VNet 내부 및 외부로 이동할 수 있습니까?
아니요. 서비스를 VNet 내부 및 외부로 이동할 수 없습니다. Toodelete 있고 hello 서비스 toomove 재배포 됩니다 것 tooanother VNet입니다.

## <a name="security"></a>보안

### <a name="what-is-hello-security-model-for-vnets"></a>Vnet에 대 한 hello 보안 모델은 무엇입니까?
Vnet, 서로 완전히 격리 되며 Azure 인프라 hello에 다른 서비스 호스트. VNet은 트러스트 경계입니다.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>인바운드 또는 아웃 바운드 트래픽 흐름 tooVNet에 연결 된 리소스를 제한할 수 있습니까?
예. 적용할 수 있습니다 [네트워크 보안 그룹](virtual-networks-nsg.md) tooindividual 서브넷은 VNet 내의 Nic tooa VNet 또는 둘 다을 연결 합니다.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>VNet에 연결된 리소스 간에 방화벽을 구현할 수 있습니까?
예. 배포할 수는 [방화벽 네트워크 가상 어플라이언스](https://azure.microsoft.com/en-us/marketplace/?term=firewall) hello Azure 마켓플레이스를 통해 여러 공급 업체에서 합니다.

### <a name="is-there-information-available-about-securing-vnets"></a>VNet 보안에 사용 가능한 정보가 있습니까?
예. Hello 참조 [Azure 네트워크 보안 개요](../security/security-network-overview.md) 을 참조 합니다.

## <a name="apis-schemas-and-tools"></a>API, 스키마 및 도구

### <a name="can-i-manage-vnets-from-code"></a>코드에서 VNet을 관리할 수 있습니까?
예. Hello에 Vnet에 대 한 REST Api를 사용할 수 있습니다 [Azure 리소스 관리자](https://msdn.microsoft.com/library/mt163658.aspx) 및 [클래식 (서비스 관리)](http://go.microsoft.com/fwlink/?LinkId=296833)) 배포 모델입니다.

### <a name="is-there-tooling-support-for-vnets"></a>VNet에 대한 도구 지원이 있습니까?
예. 사용에 대한 자세한 정보:
- hello 통해 Azure 포털 toodeploy Vnet hello [Azure 리소스 관리자](virtual-networks-create-vnet-arm-pportal.md) 및 [클래식](virtual-networks-create-vnet-classic-pportal.md) 배포 모델입니다.
- Vnet hello를 통해 배포 PowerShell toomanage [리소스 관리자](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) 및 [클래식](/powershell/module/azure/?view=azuresmps-3.7.0) 배포 모델입니다.
- hello [Azure CLI (명령줄 인터페이스)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage Vnet 두 가지 경우 모두를 통해 배포 합니다.  
