---
title: "Vm 및 역할 인스턴스에 대 한 aaaResolution"
description: "Azure IaaS, 하이브리드 솔루션, 서로 다른 클라우드 서비스, Active Directory, 자체 DNS 서버 사용 시의 이름 확인 시나리오  "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>VM 및 역할 인스턴스에 대한 이름 확인
사용 방법에 따라 사용자 Azure toohost IaaS, PaaS 및 하이브리드 솔루션을 tooallow hello Vm 및 역할 인스턴스를 서로 toocommunicate 만들어야 할 수 있습니다. IP 주소를 사용 하 여이 통신을 수행할 수 있습니다, 이지만 보다 간단 하 게 toouse 이름의 기억 하기 쉬운 변경 되지 않습니다. 

역할 인스턴스 및 Azure에서 호스팅되는 Vm tooresolve 도메인 이름을 toointernal IP 주소를 할 때 두 가지 방법 중 하나를 사용할 수 있습니다.

* [Azure에서 제공하는 이름 확인](#azure-provided-name-resolution)
* [자체 DNS 서버를 사용 하 여 이름 확인](#name-resolution-using-your-own-dns-server) (있는 전달 될 수 있습니다 쿼리 toohello Azure 제공 DNS 서버) 

hello 종류의 이름 확인 사용 어떻게 Vm 및 역할 인스턴스는 서로 toocommunicate 필요에 따라 달라 집니다.

**hello 다음 표에 나와 시나리오와 해당 이름 확인 솔루션이 있습니다.**

| **시나리오** | **솔루션** | **접미사** |
| --- | --- | --- |
| 역할 인스턴스 또는 Vm 간의 이름 확인에 hello 동일한 클라우드 서비스 또는 가상 네트워크 |[Azure에서 제공하는 이름 확인](#azure-provided-name-resolution) |호스트 이름 또는 FQDN |
| 서로 다른 네트워크에 위치한 역할 인스턴스 또는 VM 간 이름 확인 |고객이 관리하는 DNS 서버가 Azure(DNS 프록시)에서 확인을 위해 vnet 간의 쿼리를 전달합니다.  [자체 DNS 서버를 이용한 이름 확인](#name-resolution-using-your-own-dns-server) |FQDN만 |
| Azure의 VM 또는 역할 인스턴스에서 온-프레미스 컴퓨터와 서비스 이름 확인 |고객이 관리하는 DNS 서버(예: 온-프레미스 도메인 컨트롤러, 로컬 읽기 전용 도메인 컨트롤러 또는 영역 전송을 사용하여 동기화된 DNS 보조)입니다.  See [자체 DNS 서버를 이용한 이름 확인](#name-resolution-using-your-own-dns-server) |FQDN만 |
| 온-프레미스 컴퓨터에서 Azure 호스트 이름 확인 |쿼리 전달 tooa 고객이 관리 하는 DNS에서에서 프록시 서버 hello 해당 vnet hello 프록시 서버는 확인을 위해 쿼리 tooAzure 전달합니다. See [자체 DNS 서버를 사용한 이름 확인](#name-resolution-using-your-own-dns-server) |FQDN만 |
| 내부 IP에 대한 역방향 DNS |[자체 DNS 서버를 사용한 이름 확인](#name-resolution-using-your-own-dns-server) |해당 없음 |
| 서로 다른 클라우드 서비스에 위치하며 가상 네트워크에 존재하지 않는 VM 또는 역할 인스턴스 간 이름 확인 |사용할 수 없습니다. 가상 네트워크 외부에 있는 VM과 역할 인스턴스가 서로 다른 클라우드 서비스에 위치한 경우에는 연결을 지원하지 않습니다. |해당 없음 |

## <a name="azure-provided-name-resolution"></a>Azure에서 제공하는 이름 확인
공용 DNS 이름 확인와 Azure Vm에 대 한 내부 이름 확인을 제공 하 고, 역할 인스턴스 내에 있는 동일한 가상 네트워크 또는 클라우드 서비스 hello 합니다.  Vm/클라우드 서비스의 인스턴스는 동일한 DNS 접미사 (충분 한 hello 호스트 이름 만으로는 이므로) 그러나 클래식 가상 네트워크 서로 다른 클라우드 서비스는 서로 다른 DNS 접미사 hello FQDN은 서로 다른 클라우드 서비스 간에 필요한 tooresolve 이름을 hello를 공유 합니다.  Hello 리소스 관리자 배포 모델의 가상 네트워크에 DNS 접미사 hello 일관적 hello 가상 네트워크를 통해 (있으므로 hello FQDN 필요 하지 않습니다) 이며 tooboth Nic 및 Vm에는 DNS 이름을 지정할 수 있습니다. 하지만 Azure 제공 이름 확인에는 구성이 필요 하지 않지만 하지 hello 적절 한 선택은 모든 배포 시나리오에 대 한 위의 hello 테이블에 표시 된 것과 같이 합니다.

> [!NOTE]
> 웹 및 작업자 역할의 경우 hello hello hello 역할 이름 및 인스턴스 번호 hello Azure 서비스 관리 REST API를 사용 하 여를 기반으로 역할 인스턴스의 내부 IP 주소를 액세스할 수 있습니다. 자세한 내용은 [서비스 관리 REST API 참조](https://msdn.microsoft.com/library/azure/ee460799.aspx)를 참조하세요.
> 
> 

### <a name="features-and-considerations"></a>기능 및 고려 사항
**기능:**

* 사용 편의성: 순서 toouse Azure 제공 이름 확인에에서 필요한 구성이 없습니다.
* hello Azure 제공 이름 확인 서비스는 항상 사용 가능을 저장 하면 hello toocreate 필요한 사용자 고유의 DNS 서버 클러스터를 관리 합니다.
* 사용자 고유의 DNS 서버 tooresolve와 함께에서 사용할 수 있습니다 온-프레미스와 Azure 호스트 이름입니다.
* 이름 확인에는 동일한 클라우드 서비스 FQDN에 대 한 필요 없이 역할 인스턴스/hello Vm 간에 제공 됩니다.
* 이름 확인은 hello FQDN에 대 한 필요 없이 hello 리소스 관리자 배포 모델을 사용 하는 가상 네트워크의 Vm 간에 제공 됩니다. Hello 클래식 배포 모델에서 가상 네트워크는 서로 다른 클라우드 서비스의 이름을 확인할 때 hello FQDN 필요 합니다. 
* 자동 생성되는 이름 대신에 배포를 가장 잘 설명해주는 호스트 이름을 사용할 수 있습니다.

**고려 사항:**

* hello Azure에서 만든 DNS 접미사를 수정할 수 없습니다.
* 사용자 고유의 레코드를 수동으로 등록할 수 없습니다.
* WINS 및 NetBIOS는 지원되지 않습니다. (Windows 탐색기에 VM은 표시되지 않습니다.)
* 호스트 이름이 DNS와 호환될 수 있어야 합니다. (0-9, a-z 및 '-'만 사용이 가능하며, '-'로 시작하거나 끝날 수 없습니다. RFC 3696 섹션을 2를 참조하세요.)
* DNS 쿼리 트래픽은 각 VM에 대해 제한됩니다. 이 대부분의 응용 프로그램에 영향을 주지 않아야 합니다.  요청 제한이 확인되는 경우 클라이언트쪽 캐싱이 사용하도록 설정되었는지 확인합니다.  자세한 내용은 참조 하십시오. [hello Azure 제공 이름 확인 대부분 가져오는](#Getting-the-most-from-Azure-provided-name-resolution)합니다.
* 클래식 배포 모델에서 각 가상 네트워크에 대 한 hello 처음 180 개의 클라우드 서비스 내의 Vm만 등록 됩니다. Toovirtual 네트워크 리소스 관리자 배포 모델에는 적용 되지 않습니다.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Hello Azure 제공 이름 확인 대부분 가져오기
**클라이언트쪽 캐싱:**

모든 DNS 쿼리 toobe hello 네트워크를 통해 전송 해야 합니다.  클라이언트 쪽 캐싱 대기 시간을 줄이고 로컬 캐시에서 되풀이 DNS 쿼리를 확인 하 여 복원 력을 toonetwork 탐사를 향상 시킬 수 있습니다.  DNS 레코드는 활성 시간 (TTL) 하므로 대부분의 경우에 적합 한 클라이언트 쪽 캐싱 레코드 freshness, 영향을 주지 않고 가능한 한 오랫동안에 대 한 hello 캐시 toostore hello 레코드 수를 포함 합니다.

hello 기본 Windows DNS 클라이언트는 기본 제공 되는 DNS 캐시를 있습니다.  일부 Linux 배포판에 기본적으로 캐싱을 포함 되지 않습니다 (아님을 로컬 캐시 이미 확인) 한 후 tooeach Linux VM을 추가할 수 하나 것이 좋습니다.

제공 되는 다른 DNS 캐싱 패키지, 예: dnsmasq 여러 가지, hello 가장 일반적인 배포판에 hello 단계 tooinstall dnsmasq 다음과 같습니다.

* **Ubuntu(resolvconf 사용)**:
  * 방금 hello dnsmasq 패키지 ("sudo apt get 설치 dnsmasq")를 설치 합니다.
* **SUSE(netconf 사용)**:
  * hello dnsmasq 패키지 ("sudo zypper 설치 dnsmasq")를 설치 합니다. 
  * hello dnsmasq 서비스 ("systemctl enable dnsmasq.service")를 사용 하도록 설정 
  * hello dnsmasq 서비스 ("systemctl 시작 dnsmasq.service")를 시작 합니다. 
  * 편집 "/ 등/sysconfig/네트워크/config" NETCONFIG_DNS_FORWARDER 변경 = "" 너무 "dnsmasq"
  * 로컬 DNS 확인자 hello 대로 resolv.conf ("다음과 같은 netconfig 업데이트") tooset hello 캐시 업데이트
* **OpenLogic(NetworkManager 사용)**:
  * hello dnsmasq 패키지 ("sudo yum 설치 dnsmasq")를 설치 합니다.
  * hello dnsmasq 서비스 ("systemctl enable dnsmasq.service")를 사용 하도록 설정
  * hello dnsmasq 서비스 ("systemctl 시작 dnsmasq.service")를 시작 합니다.
  * "도메인 이름 서버 127.0.0.1; 앞에 추가" 추가 too"/etc/dhclient-eth0.conf"
  * 로컬 DNS 확인자 hello 대로 hello 네트워크 서비스 ("서비스 네트워크를 다시 시작") tooset hello 캐시를 다시 시작

> [!NOTE]
> hello 'dnsmasq' 패키지 많은 DNS 캐시를 사용할 수 있는 Linux 용는 hello 중 하나입니다.  사용하기 전에 특정 요구 사항에 대한 적합성을 확인하고 다른 캐시가 설치되어 있지 않은지 확인합니다.
> 
> 

**클라이언트쪽 재시도:**

DNS는 주로 UDP 프로토콜입니다.  UDP 프로토콜 hello 메시지 배달을 보장 하지 않습니다, 처럼 재시도 논리 hello DNS 프로토콜 자체에서 처리 됩니다.  각 DNS 클라이언트 (운영 체제) hello 작성자가 기본 설정에 따라 다시 시도 논리를 나타낼 수 있습니다.

* Windows 운영 체제는 1초 후 재시도한 후 2초, 4초 후 다시 재시도하고 또 다시 4초 후 재시도합니다. 
* hello 기본 Linux 설치 후에 다시 시도 5 초입니다.  5 번 1 초 간격이 tooretry toochange을 것이 좋습니다.  

toocheck hello 'cat /etc/resolv.conf' Linux VM의 현재 설정 하 고 예를 들어 hello '옵션' 줄 확인:

    options timeout:1 attempts:5

hello resolv.conf 파일은 일반적으로 자동 생성 및 편집할 수 없습니다.  옵션' hello' 줄을 추가 하기 위한 구체적인 단계 hello distro로 다릅니다.

* **Ubuntu** (resolvconf 사용):
  * hello 옵션 선 too'/etc/resolveconf/resolv.conf.d/head 추가 ' 
  * ' resolvconf u' tooupdate 실행
* **SUSE** (netconf 사용):
  * ' timeout:1 시도 횟수: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS 추가 = ""에 '/ 등/sysconfig/네트워크/config' 매개 변수 
  * '다음과 같은 netconfig 업데이트' tooupdate 실행
* **OpenLogic** (NetworkManager 사용):
  * 추가 too'/etc/NetworkManager/dispatcher.d/11-dhclient '에코 "옵션 timeout:1 시도 횟수: 5" ' ' 
  * 서비스가 네트워크 다시 시작' tooupdate 실행

## <a name="name-resolution-using-your-own-dns-server"></a>자체 DNS 서버를 이용한 이름 확인
이름 확인 요구 될 수 있습니다 이동 hello 기능 Azure에서 제공 예를 들어 경우 초과 사용 하 여 Active Directory 도메인 또는 가상 네트워크 (vnet) 간의 DNS 확인을 요구 하는 경우 다양 한 상황이 있습니다.  toocover 이러한 시나리오에서는 Azure 기능을 제공 hello toouse 있습니다에 대 한 사용자 고유 DNS 서버입니다.  

가상 네트워크 내에서 DNS 서버는 해당 가상 네트워크 내에서 tooresolve 호스트 이름이 DNS 쿼리 tooAzure 재귀 확인자 전달할 수 있습니다.  예를 들어 도메인 컨트롤러 (DC) Azure에서 실행 중인 tooDNS 쿼리 해당 도메인에 대 한 응답을 다른 모든 쿼리 tooAzure 전달 됩니다.  이렇게 하면 Vm toosee (DC hello)를 통해 온-프레미스 리소스와 (hello 전달자)를 통해 Azure에서 제공 호스트 이름입니다.  액세스 tooAzure 재귀 확인자 hello 가상 IP 168.63.129.16 통해 제공 됩니다.

또한 DNS 전달 간 vnet DNS 확인 있으며 온-프레미스 컴퓨터 tooresolve Azure에서 제공 되는 호스트 이름이 있습니다.  주문 tooresolve VM의 호스트 이름, VM hello DNS 서버에에서 있어야 hello 동일한 가상 네트워크 및 구성 된 tooforward hostname 쿼리 tooAzure 수 있습니다.  조건부 전달 hello DNS 접미사 각 vnet에 다른 그대로 사용할 수 있습니다 toosend DNS 쿼리 toohello 규칙 확인용 vnet을 해결 합니다.  다음 이미지는 hello 두 vnet 및이 메서드를 사용 하 여 vnet 간 DNS 확인을 수행 하는 온-프레미스 네트워크를 보여 줍니다.  예제 DNS 전달자는 hello 영어로 [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) 및 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder)합니다.

![Vnet 간 DNS](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Azure 제공 이름 확인이 내부 DNS 접미사를 사용 하는 경우 (*. internal.cloudapp.net) DHCP를 사용 하 여 제공 된 tooeach VM 됩니다.  이 통해 레코드 hello internal.cloudapp.net 영역에는 hello 호스트 이름으로 호스트 이름 확인 합니다.  사용자 고유의 이름 확인 솔루션을 사용 하는 경우 다른 DNS 아키텍처 (예: 도메인에 가입 된 시나리오) 충돌 하므로 IDN 접미사가 않습니다 hello tooVMs를 제공 합니다.  대신 작동하지 않는 자리 표시자(reddog.microsoft.com)가 제공됩니다.  

필요한 경우 PowerShell 또는 hello API를 사용 하 여 hello 내부 DNS 접미사를 확인할 수 있습니다.

* 리소스 관리자 배포 모델에서 가상 네트워크에 대 한 hello 접미사는 hello를 통해 사용할 수 있는 [네트워크 인터페이스 카드](https://msdn.microsoft.com/library/azure/mt163668.aspx) 리소스 또는 hello를 통해 [Get AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet.    
* 클래식 배포 모델에서 hello 접미사는 hello를 통해 사용할 수 있는 [배포 API 가져오기](https://msdn.microsoft.com/library/azure/ee460804.aspx) 호출 또는 hello를 통해 [Get-azurevm-디버그](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet.

TooAzure 요구 사항에 적합 하지 않습니다는 쿼리를 전달 하는 경우 자체 DNS 솔루션 tooprovide 해야 합니다.  DNS 솔루션은 다음을 수행해야 합니다:

* 예를 들어 [DDNS](virtual-networks-name-resolution-ddns.md)를 통해 적절한 호스트 이름 확인을 제공해야 합니다.  Note. DDNS toodisable DNS 레코드 청소 Azure의 DHCP 임대 매우 긴 하 여 청소 DNS 제거 될 수 있습니다를 할 수 있습니다를 사용 하 여 중간 기록 하는 경우. 
* 외부 도메인 이름의 적절 한 재귀 해상도 tooallow 확인을 제공 합니다.
* 액세스할 수 있는 (TCP 및 UDP 포트 53) 사용 되 고 수 tooaccess 수 hello 클라이언트에서 인터넷 hello 수 있습니다.
* Hello에서 액세스 로부터 보호 인터넷, 외부 에이전트에서 발생할 수 있는 toomitigate 위험 합니다.

> [!NOTE]
> 최상의 성능을 위해 DNS 서버와 Azure Vm을 사용 하는 경우, i p v 6을 비활성화 해야 및 [인스턴스 수준 공용 IP](virtual-networks-instance-level-public-ip.md) tooeach DNS 서버 VM을 할당 해야 합니다.  DNS 서버로 toouse Windows 서버를 선택 하면 [이 여기서](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) 추가적인 성능 분석과 최적화를 제공 합니다.
> 
> 

### <a name="specifying-dns-servers"></a>DNS 서버 지정
사용자 고유의 DNS 서버를 사용할 때 Azure 가상 네트워크 당 여러 DNS 서버 hello 기능 toospecify 제공 하나의 네트워크 인터페이스 (리소스 관리자) / 또는 클라우드 서비스 (클래식).  클라우드 서비스/네트워크 인터페이스에 대 한 지정 된 DNS 서버 hello 가상 네트워크에 대해 지정 된 조치 우선 순위를 가져옵니다.

> [!NOTE]
> 네트워크 연결 속성, 서비스 하는 동안 지워질 가져올 있습니다 대로 DNS 서버 Ip을 Windows Vm 내에서 직접 편집할 수와 같은 치료 hello 가상 네트워크 어댑터 바꾸면 가져옵니다. 
> 
> 

Hello 리소스 관리자 배포 모델을 사용할 때는 hello 포털, API/템플릿에에서 DNS 서버를 지정할 수 있습니다 ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) 또는 PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Hello 클래식 배포 모델을 사용할 때는 DNS 서버 hello 가상 네트워크에 지정할 수 있습니다에 대 한 hello 포털 또는 [hello *네트워크 구성* 파일](https://msdn.microsoft.com/library/azure/jj157100)합니다.  클라우드 서비스에 대 한 hello DNS 서버를 통해 지정 [hello *서비스 구성* 파일](https://msdn.microsoft.com/library/azure/ee758710) 또는 PowerShell ([New-azurevm](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> 이미 배포 된 가상 네트워크/가상 컴퓨터에 대 한 hello DNS 설정을 변경 하면 toorestart 영향을 받는 각 VM에 필요한 hello 변경 tootake 효과입니다.
> 
> 

## <a name="next-steps"></a>다음 단계
리소스 관리자 배포 모델:

* [가상 네트워크 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [네트워크 인터페이스 카드 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [새-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [새-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

클래식 배포 모델:

* [Azure 서비스 구성 스키마](https://msdn.microsoft.com/library/azure/ee758710)
* [가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100)
* [네트워크 구성 파일을 사용하여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md) 

