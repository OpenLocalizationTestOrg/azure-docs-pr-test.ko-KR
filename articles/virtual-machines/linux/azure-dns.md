---
title: "aaaDNS Azure에서 Linux 가상 컴퓨터에 대 한 이름 확인 옵션"
description: "Azure IaaS의 Linux 가상 컴퓨터에 대한 이름 확인 시나리오(제공된 DNS 서비스, 하이브리드 외부 DNS 및 사용자 고유의 DNS 서버 포함)입니다."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Azure의 Linux 가상 컴퓨터에 대한 DNS 이름 확인 옵션
Azure는 단일 가상 네트워크 내에 포함된 모든 가상 컴퓨터에 대해 기본적으로 DNS 이름 확인을 제공합니다. Azure에서 호스트하는 가상 컴퓨터에서 자체 DNS 서비스를 구성하여 사용자 고유의 DNS 이름 확인 솔루션을 구현할 수 있습니다. hello 다음과 같은 시나리오 있습니다 hello 상황에 맞는 하나를 선택 합니다.

* [Azure에서 제공하는 이름 확인](#azure-provided-name-resolution)
* [자체 DNS 서버를 사용한 이름 확인](#name-resolution-using-your-own-dns-server)

hello 종류의 사용 하는 이름 확인 방법을 가상 컴퓨터와 역할 인스턴스는 서로 toocommunicate 필요에 따라 달라 집니다.

hello 다음 표에 나와 시나리오와 해당 이름 확인 솔루션이 있습니다.

| **시나리오** | **솔루션** | **접미사** |
| --- | --- | --- |
| 이름 확인 역할 인스턴스 또는 hello에서 가상 컴퓨터 간의 동일한 가상 네트워크 |[Azure에서 제공하는 이름 확인](#azure-provided-name-resolution) |호스트 이름 또는 FQDN(정규화된 도메인 이름) |
| 서로 다른 네트워크에 있는 역할 인스턴스 또는 가상 컴퓨터 간 이름 확인 |Azure(DNS 프록시)에서 이름을 확인할 수 있도록 가상 컴퓨터 간에 쿼리를 전달하는 고객이 관리하는 DNS 서버. [자체 DNS 서버를 이용한 이름 확인](#name-resolution-using-your-own-dns-server). |FQDN만 |
| Azure의 역할 인스턴스 또는 가상 컴퓨터에서 온-프레미스 컴퓨터와 서비스 이름 확인 |고객이 관리하는 DNS 서버(예: 온-프레미스 도메인 컨트롤러, 로컬 읽기 전용 도메인 컨트롤러 또는 영역 전송을 사용하여 동기화된 DNS 보조). [자체 DNS 서버를 이용한 이름 확인](#name-resolution-using-your-own-dns-server). |FQDN만 |
| 온-프레미스 컴퓨터에서 Azure 호스트 이름 확인 |쿼리 tooa 고객이 관리 하는 DNS에서에서 프록시 서버 hello 해당 가상 네트워크를 전달 합니다. hello 프록시 서버는 확인을 위해 쿼리 tooAzure를 전달합니다. [자체 DNS 서버를 이용한 이름 확인](#name-resolution-using-your-own-dns-server). |FQDN만 |
| 내부 IP에 대한 역방향 DNS |[자체 DNS 서버를 사용한 이름 확인](#name-resolution-using-your-own-dns-server) |해당 없음 |

## <a name="name-resolution-that-azure-provides"></a>Azure에서 제공하는 이름 확인
공용 DNS 이름 확인와 Azure 가상 컴퓨터에 대 한 내부 이름 확인을 제공 하 고,에 있는 역할 인스턴스 hello 동일한 가상 네트워크입니다. Azure 리소스 관리자에 기반 하는 가상 네트워크에서 DNS 접미사 hello 전체에서 일관 된 hello 가상 네트워크입니다. hello FQDN이 필요 하지 않습니다. DNS 이름 (Nic) tooboth 네트워크 인터페이스 카드 및 가상 컴퓨터에 할당할 수 있습니다. 하지만 Azure에서 제공 하는 hello 이름 확인에는 구성이 필요 하지 않습니다, 하지 hello 적절 한 선택은 모든 배포 시나리오에 대 한 hello 테이블 앞에 표시 된 것과 같이 합니다.

### <a name="features-and-considerations"></a>기능 및 고려 사항
**기능:**

* 구성이 Azure에서 제공 하는 필수 toouse 이름 확인 합니다.
* Azure에서 제공 하는 hello 이름 확인 서비스는 항상 사용 가능 합니다. Toocreate 필요 하 고 사용자 고유의 DNS 서버 클러스터를 관리 하지 않습니다.
* 사용자 고유의 DNS 서버 tooresolve 함께 Azure에서 제공 하는 hello 이름 확인 서비스를 표시할 수 있습니다 온-프레미스와 Azure 호스트 이름입니다.
* 이름 확인 hello FQDN에 대 한 필요 없이 가상 네트워크의 가상 컴퓨터 간에 제공 됩니다.
* 자동으로 생성되는 이름 대신 배포를 가장 잘 설명해주는 호스트 이름을 사용할 수 있습니다.

**고려 사항:**

* Azure에서 만들어지는 hello DNS 접미사를 수정할 수 없습니다.
* 사용자 고유의 레코드를 수동으로 등록할 수 없습니다.
* WINS 및 NetBIOS는 지원되지 않습니다.
* 호스트 이름은 DNS와 호환되어야 합니다.
    이름에는 0-9, a-z 및 '-'만 사용이 가능하며, '-'로 시작하거나 끝날 수 없습니다. RFC 3696 섹션을 2를 참조하세요.
* DNS 쿼리 트래픽은 각 가상 컴퓨터에 대해 제한됩니다. 이 제한은 대부분의 응용 프로그램에 영향을 주지 않아야 합니다.  요청 제한이 확인되는 경우 클라이언트쪽 캐싱이 사용하도록 설정되었는지 확인합니다.  자세한 내용은 참조 [hello Azure 제공 이름 확인 대부분 가져오는](#getting-the-most-from-name-resolution-that-azure-provides)합니다.

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Hello Azure 제공 이름 확인 대부분 가져오기
**클라이언트쪽 캐싱:**

일부 DNS 쿼리 hello 네트워크를 통해 전송 되지 않습니다. 클라이언트 쪽 캐싱 대기 시간을 줄이고 로컬 캐시에서 되풀이 DNS 쿼리를 확인 하 여 복원 력을 toonetwork 불일치를 향상 시킬 수 있습니다. DNS 레코드는 활성 시간 (TTL) 레코드 새로 고침에 영향을 주지 않고 가능한 한 오랫동안에 대 한 hello 캐시 toostore hello 레코드를 매핑함으로써 포함 됩니다. 결과적으로 클라이언트쪽 캐싱은 대부분의 상황에 적합합니다.

일부 Linux 배포판은 기본적으로 캐싱이 포함되지 않습니다. 이 아님을 로컬 캐시 이미 확인 한 후 캐시 tooeach Linux 가상 컴퓨터를 추가 하는 것이 좋습니다.

dnsmasq 같은 여러 가지 DNS 캐싱 패키지를 사용할 수 있습니다. 가장 일반적인 배포 hello hello 단계 tooinstall dnsmasq 다음과 같습니다.

**Ubuntu(resolvconf 사용)**
  * Hello dnsmasq 패키지 ("sudo apt get 설치 dnsmasq")를 설치 합니다.

**SUSE(netconf 사용)**:
1. Hello dnsmasq 패키지 ("sudo zypper 설치 dnsmasq")를 설치 합니다.
2. Hello dnsmasq 서비스 ("systemctl enable dnsmasq.service")를 사용 하도록 설정 합니다.
3. Hello dnsmasq 서비스 ("systemctl 시작 dnsmasq.service")를 시작 합니다.
4. 편집 "/ 등/sysconfig/네트워크/config" NETCONFIG_DNS_FORWARDER 변경 = "" 너무 "dnsmasq"입니다.
5. 로컬 DNS 확인자 hello 대로 resolv.conf ("다음과 같은 netconfig 업데이트") tooset hello 캐시를 업데이트 합니다.

**Rogue Wave Software의 CentOS(이전의 OpenLogic. NetworkManager 사용)**
1. Hello dnsmasq 패키지 ("sudo yum 설치 dnsmasq")를 설치 합니다.
2. Hello dnsmasq 서비스 ("systemctl enable dnsmasq.service")를 사용 하도록 설정 합니다.
3. Hello dnsmasq 서비스 ("systemctl 시작 dnsmasq.service")를 시작 합니다.
4. "도메인 이름 서버 127.0.0.1; 앞에 추가" 추가 too"/etc/dhclient-eth0.conf"입니다.
5. 로컬 DNS 확인자 hello 대로 hello 네트워크 서비스 ("서비스 네트워크를 다시 시작") tooset hello 캐시를 다시 시작

> [!NOTE]
> : hello 'dnsmasq' 패키지는 Linux에 사용할 수 있는 많은 DNS 캐시 hello 중 하나입니다. 사용하기 전에 본인의 요구 사항에 적합한지 확인하고 다른 캐시가 설치되어 있지 않은지 확인합니다.
>
>

**클라이언트쪽 재시도**

DNS는 주로 UDP 프로토콜입니다. UDP 프로토콜 hello 메시지 배달을 보장 하지 않습니다, 때문에 자체 DNS 프로토콜 hello 재시도 논리를 처리 합니다. 각 DNS 클라이언트 (운영 체제) hello 작성자의 기본 설정에 따라 다시 시도 논리를 나타낼 수 있습니다.

* Windows 운영 체제는 1초 후 재시도한 후 2초, 4초 후 다시 재시도하고 또 다시 4초 후 재시도합니다.
* hello 기본 Linux 설치 후에 다시 시도 5 초입니다.  이 tooretry 1 초 간격에 따라 5 번 변경 해야 합니다.  

toocheck 'cat /etc/resolv.conf' Linux 가상 컴퓨터의 현재 설정을 hello 하 고 예를 들어 hello '옵션' 선 확인:

    options timeout:1 attempts:5

hello resolv.conf 파일은 자동으로 생성 및 편집할 수 없습니다. hello '옵션' 배포에 따라 다른 줄을 추가 하는 특정 단계 hello:

**Ubuntu**(resolvconf 사용)
1. Hello 옵션 선 too'/etc/resolveconf/resolv.conf.d/head 추가 '.
2. ' Resolvconf u' tooupdate를 실행 합니다.

**SUSE**(netconf 사용)
1. ' Timeout:1 시도 횟수: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS 추가 = ""에 '/ 등/sysconfig/네트워크/config' 매개 변수입니다.
2. Tooupdate '다음과 같은 netconfig 업데이트'를 실행 합니다.

**Rogue Wave Software의 CentOS(이전의 OpenLogic)**(NetworkManager 사용)
1. 추가 too'/etc/NetworkManager/dispatcher.d/11-dhclient '에코 "옵션 timeout:1 시도 횟수: 5" ' '.
2. 서비스가 네트워크 다시 시작' tooupdate를 실행 합니다.

## <a name="name-resolution-using-your-own-dns-server"></a>자체 DNS 서버를 이용한 이름 확인
사용자 이름 확인 요구 사항을 Azure에서 제공 하는 hello 기능 넘지 수 있습니다. 예를 들어 가상 네트워크 간 DNS 확인이 필요할 수 있습니다. toocover이이 시나리오에서는 사용자 고유의 DNS 서버를 사용할 수 있습니다.  

DNS 서버에 있는 가상 네트워크 캔 정방향 DNS를 Azure tooresolve 호스트 이름 확인 자의 toorecursive 쿼리 내에서 동일한 가상 네트워크를 hello 합니다. 예를 들어 Azure에서 실행 되는 DNS 서버 tooDNS 쿼리 자체 dns 영역 파일 및 다른 모든 쿼리 tooAzure 전달 응답할 수 있습니다. 이 기능을 사용 하면 가상 컴퓨터 toosee 모두에 있는 항목의 영역 파일 및 (hello 전달자)를 통해 Azure에서 제공 하는 호스트 이름입니다. Azure의 액세스 toohello 재귀 확인자 hello 가상 IP 168.63.129.16 통해 제공 됩니다.

또한 DNS 전달 가상 네트워크 간의 DNS 확인을 사용 하도록 설정 하 고 Azure에서 제공 하 여 온-프레미스 컴퓨터 tooresolve 호스트 이름을 사용 하도록 설정 합니다. tooresolve hello DNS 서버 가상 컴퓨터에 상주해 야 가상 컴퓨터의 호스트 이름에 동일한 가상 네트워크를 hello 및 구성 된 tooforward hostname 쿼리 tooAzure 수 있습니다. 조건부 전달 hello DNS 접미사에서에서 다르기 때문에 각 가상 네트워크를 사용할 수 있습니다 toosend DNS 쿼리 toohello 규칙 확인을 위해 가상 네트워크를 수정 합니다. hello 다음 이미지는 두 개의 가상 네트워크와이 방법을 사용 하 여 가상 네트워크 간의 DNS 확인을 수행 하는 온-프레미스 네트워크

![가상 네트워크 간의 DNS 확인](./media/azure-dns/inter-vnet-dns.png)

Azure에서 제공 하는 이름 확인을 사용 하는 경우 DHCP를 사용 하 여 hello 내부 DNS 접미사 tooeach 가상 컴퓨터를 제공 됩니다. 이름 확인 솔루션을 사용 하면이 접미사는 제공 된 toovirtual 컴퓨터 hello 접미사 다른 DNS 아키텍처를 방해 하므로 합니다. 가상 컴퓨터의 FQDN 또는 tooconfigure hello 접미사로 toorefer toomachines, PowerShell 또는 hello API toodetermine hello 접미사를 사용할 수 있습니다.

* Azure 리소스 관리자에서 관리 되는 가상 네트워크에 대 한 hello 접미사는 hello를 통해 사용할 수 있는 [네트워크 인터페이스 카드](https://msdn.microsoft.com/library/azure/mt163668.aspx) 리소스입니다. Hello를 실행할 수도 있습니다 `azure network public-ip show <resource group> <pip name>` 명령을 포함 하 여 공용 IP의 toodisplay hello 세부 정보 hello hello NIC.의 FQDN

TooAzure 요구 사항에 적합 하지 않습니다는 쿼리를 전달, 자체 DNS 솔루션 tooprovide 필요.  DNS 솔루션은 다음을 수행해야 합니다:

* 예를 들어 [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md)를 통해 적절한 호스트 이름 확인을 제공해야 합니다. DDNS을 사용 하는 경우 toodisable DNS 레코드 청소를 할 수 있습니다. Azure의 DHCP 임대는 기간이 매우 길며 청소를 통해 DNS 레코드가 완전히 제거될 수 있습니다.
* 외부 도메인 이름의 적절 한 재귀 해상도 tooallow 확인을 제공 합니다.
* 액세스할 수 있는 (TCP 및 UDP 포트 53) hello 클라이언트 역할에서 인터넷 수 tooaccess hello 되어야 합니다.
* 외부 에이전트에서 발생 하는 hello 인터넷 toomitigate 위협은에서 액세스 로부터 보호 합니다.

> [!NOTE]
> 최상의 성능을 위해 때는 가상 컴퓨터를 사용 하 여 Azure DNS 서버에 i p v 6을 사용 하지 않도록 설정 하 고 할당 한 [인스턴스 수준 공용 IP](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS 서버 가상 컴퓨터.  
>
>
