---
title: "Microsoft Azure 보안 aaaGetting 시작 | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure 보안 기능 및 자산 tooa 클라우드 공급자에 게 마이그레이션하는 조직에 대 한 일반적인 고려 사항에 대 한 개요를 제공 합니다."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Microsoft Azure 보안 시작
를 작성 하거나 IT 자산 tooa 클라우드 공급자를 마이그레이션할 때 응용 프로그램 및 서비스 hello 및 클라우드 기반 자산의 toomanage hello 보안을 제공 하는 hello 컨트롤을 사용 하 여 데이터 해당 조직의 능력 tooprotect에 의존 하 고 있습니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고 비즈니스는 고유한 보안 요구를 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 다양 한 구성 가능한 보안 옵션 및 hello 기능 toocontrol와 보안 toomeet hello 하면 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다.

Azure 보안에 있는 이 개요 문서에서 다음 사항을 살펴봅니다.

* Azure 서비스 및 toohelp를 사용할 수 있는 기능 서비스와 Azure 내에서 데이터를 보호 합니다.
* Microsoft Azure 인프라 toohelp hello를 보호 하는 방법, 데이터 및 응용 프로그램을 보호 합니다.

## <a name="identity-and-access-management"></a>ID 및 액세스 관리
액세스 tooIT 인프라, 데이터 및 응용 프로그램을 제어 하는 것이 중요 합니다. Microsoft Azure는 Azure AD(Azure Active Directory), Azure Storage, 수많은 표준 및 API에 대한 지원과 같은 서비스를 통해 이러한 기능을 제공합니다.

[Azure AD](../active-directory/active-directory-whatis.md)는 조직의 사용자, 그룹 및 개체에 대한 인증, 권한 부여 및 액세스 제어를 제공하는 ID 리포지토리 및 엔진입니다. Azure AD는 또한 개발자는 효과적인 방법은 toointegrate id 관리 응용 프로그램에 제공합니다. [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx) 및 [OpenID 연결](http://openid.net/connect/)과 같은 산업 표준 프로토콜을 통해 .NET, Java, Node.js 및 PHP와 같은 플랫폼에서 로그인 기능을 설정할 수 있습니다.

Graph API REST 기반 hello 모든 플랫폼의 개발자 tooread 및 쓰기 toohello 디렉터리를 수 있습니다. [OAuth 2.0](http://oauth.net/2/) 지원을 통해 개발자는 Microsoft 및 타사 웹 API와 통합되는 모바일 및 웹 응용 프로그램을 빌드하고 사용자 고유의 보안 웹 API를 빌드할 수 있습니다. 개발 중인 추가 라이브러리와 함께 오픈 소스 클라이언트 라이브러리를 .Net, Windows Store, iOS 및 Android에서 사용할 수 있습니다.

### <a name="how-azure-enables-identity-and-access-management"></a>Azure가 ID 및 액세스 관리를 사용하는 방법
Azure AD는 조직의 독립 실행형 클라우드 디렉터리 또는 기존 온-프레미스 Active Directory와 통합된 솔루션으로 사용될 수 있습니다. 일부 통합 기능은 디렉터리 동기화 및 Single Sign-On(SSO)을 포함합니다. 이러한 hello 클라우드로 기존 온-프레미스 id의 hello 도달 범위를 확장 하 고 hello 관리자 및 사용자 환경을 개선 합니다.

ID 및 액세스 관리에 대한 기타 기능은 다음과 같습니다.

* Azure AD 사용 [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) 호스팅되는 위치에 관계 없이 tooSaaS 응용 프로그램입니다. 응용 프로그램 일부는 Azure AD를 사용하여 페더레이션되고 나머지는 암호 SSO를 사용합니다. 또한 페더레이션된 응용 프로그램은 사용자 프로비전 및 암호 보관을 지원할 수 있습니다.
* 에 대 한 액세스 toodata [Azure 저장소](https://azure.microsoft.com/services/storage/) 인증을 통해 제어 됩니다. 각 저장소 계정에 기본 키 ([저장소 계정 키](https://msdn.microsoft.com/library/azure/ee460785.aspx), 또는 SAK)와 보조 비밀 키 (hello 공유 액세스 서명, 또는 SAS).
* Azure AD는 온-프레미스 디렉터리와 함께 [Active Directory Federation Services](../active-directory/fundamentals-identity.md), 동기화 및 복제를 사용하여 페더레이션을 통해 IaaS(Identity as a Service)를 제공합니다.
* [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) hello 다단계 인증 서비스 모바일 앱, 전화 통화 또는 문자 메시지를 사용 하 여 사용자가 tooverify 로그인입니다. Hello Azure Multi-factor Authentication 서버 및 사용자 지정 응용 프로그램 및 디렉터리 hello SDK를 사용 하 여과 Azure AD toohelp 안전한 온-프레미스 리소스와 사용할 수 있습니다.
* [Azure AD 도메인 서비스](https://azure.microsoft.com/services/active-directory-ds/) 도메인 컨트롤러를 배포 하지 않고 Azure 가상 컴퓨터 tooa 도메인에 가입할 수 있습니다. 회사 Active Directory 자격 증명으로 toothese 가상 컴퓨터에 로그인 하 고 모든 Azure 가상 컴퓨터에 그룹 정책 tooenforce 보안 기준을 사용 하 여 도메인에 가입 된 가상 컴퓨터를 관리할 수 있습니다.
* [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) toohundreds 수백만 id의 크기를 조정 하는 소비자 용 응용 프로그램에 대해 항상 사용 가능한 글로벌 id 관리 서비스를 제공 합니다. 이 서비스는 모바일 및 웹 플랫폼에 통합될 수 있습니다. 소비자 또는 서명할 수 tooall에 사용자 지정 가능한 환경을 통해 응용 프로그램는 기존 소셜 계정을 사용 하 여 새 자격 증명을 만들어.

## <a name="data-access-control-and-encryption"></a>데이터 액세스 제어 및 암호화
의무 분리 hello 원칙을 사용 하는 Microsoft 및 [최소 권한](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 전체 Azure 운영 합니다. Azure 지원 담당자가 액세스 toodata 명시적 사용 권한을 차지 하며가 부여 기록 되 고 감사 하는 "just in time" 별로 다음 해지 hello engagement 완료 된 후 합니다.

Azure는 전송 중인 데이터와 미사용 데이터 보호를 위한 다수의 기능도 제공합니다. 여기에는 데이터, 파일, 응용 프로그램, 서비스, 통신, 장치에 대한 암호화가 포함됩니다. 정보를 Azure에 배치하기 전에 암호화할 수 있고 온-프레미스 데이터 센터에 키를 저장할 수도 있습니다.

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Azure 암호화 기술
사용 하 여 관리자 액세스 tooyour 구독 환경에 대 한 세부 정보를 수집할 수 [Azure AD 보고](../active-directory/active-directory-reporting-audit-events.md)합니다. Azure의 중요한 정보를 포함하는 VHD에서 [BitLocker 드라이브 암호화](https://technet.microsoft.com/library/cc732774.aspx)를 구성할 수 있습니다.

데이터 보안 tookeep 도움이 되는 Azure의 다른 기능 포함 됩니다.

* 응용 프로그램 개발자가 Windows hello를 사용 하 여 Azure에 배포할 hello 응용 프로그램에 암호화를 빌드할 수 [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) 및.NET Framework입니다.
* Azure Blob 저장소에 대 한 클라이언트 쪽 암호화와 함께 hello 키를 완전히 제어 합니다. hello 저장소 서비스 되지 hello 키 하 고 hello 데이터를 암호 해독 수 없는 경우에 합니다.
* [Azure 권한 관리 (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (hello로 [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) 파일 및 액세스 정책 기반 관리를 통해 데이터 수준의 암호화 및 데이터 누수 방지를 제공 합니다.
* Azure는 SQL Server 가상 컴퓨터에서 [테이블 수준 및 열 수준 암호화(TDE/CLE)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx)를 지원하고 데이터 센터에서 타사 온-프레미스 키 관리 서버를 지원합니다.
* 저장소 계정 키, 공유 액세스 서명, 관리 인증서와 다른 키가 고유 tooeach Azure 테 넌 트입니다.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) 하이브리드 저장소 tooAzure 저장소를 업로드 하기 전에 128 비트 공개/개인 키 쌍을 통해 데이터를 암호화 합니다.
* Azure 지원 하 고 hello 데이터 형식, 컨테이너 및 전송에 따라 SSL/TLS, IPsec 및 AES를 비롯 한 다양 한 암호화 메커니즘을 사용 합니다.

## <a name="virtualization"></a>가상화
hello Azure 플랫폼에는 가상화 된 환경을 사용합니다. 사용자 인스턴스 액세스 tooa 물리적 호스트 서버를 갖지 않는 독립 실행형 가상 컴퓨터와 작동 되지 않으며이 격리 물리적를 사용 하 여 적용 [프로세서 (링-0/링-3) 권한 수준](https://en.wikipedia.org/wiki/Protection_ring)합니다.

링 0은 가장 권한이 있는 고 3 hello hello 이상입니다. hello 게스트 OS는 낮은 권한의 링 1에서 실행 하 고 응용 프로그램에서 실행 hello 최소 권한이 지정 된 링 3 키를 누릅니다. 물리적 리소스의이 가상화 게스트 OS와 하이퍼바이저, 결과적으로 두 hello 간의 추가 보안 분리 간의 tooa 명확 하 게 분리를 안내 합니다.

hello Azure 하이퍼바이저 마이크로 커널 처럼 작동 및 VMBus를 호출 하는 공유 메모리 인터페이스를 사용 하 여 처리를 위해 게스트 가상 컴퓨터 toohello 호스트에서 모든 하드웨어 액세스 요청을 전달 합니다. 사용자가 원시 읽기/쓰기/실행 액세스 toohello 시스템 하지 못하도록 방지 하 고 hello의 시스템 리소스를 공유 하는 위험을 완화 합니다.

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Azure가 가상화를 구현하는 방법
Azure는 hello 하이퍼바이저에서 구현 되며 패브릭 컨트롤러 에이전트에서 구성 하는 하이퍼바이저 방화벽 (패킷 필터)를 사용 합니다. 이렇게 하면 무단 액세스로부터 테넌트를 보호할 수 있습니다. 모든 트래픽이 hello 패브릭 컨트롤러 에이전트가 hello 패킷 필터 tooadd를 구성 하는 다음 가상 컴퓨터를 만들 때 기본적으로 차단 *규칙 및 예외* tooallow 트래픽 권한을 부여 합니다.

프로그래밍하는 규칙에는 다음과 같은 두 가지 범주가 있습니다.

* **컴퓨터 구성 또는 인프라 규칙**: 기본적으로 모든 통신이 차단됩니다. 있습니다 예외 tooallow 가상 컴퓨터 toosend 되며 DHCP 및 DNS 트래픽을 수신 합니다. 가상 컴퓨터 트래픽 toohello "public" 인터넷 및 송신 트래픽 tooother 가상 컴퓨터 운영 체제 정품 인증 서버 hello hello 클러스터 내에서 보낼 수도 있습니다. 허용 된 보내는 대상 hello 가상 컴퓨터 목록이 Azure 라우터 서브넷을 포함 하지 않습니다, 그리고 Azure 관리 백업 끝점 및 기타 Microsoft 속성입니다.
* **역할 구성 파일**: hello hello 테 넌 트의 서비스 모델에 따라 인바운드 액세스 제어 목록 (Acl)을 정의 합니다. 예를 들어 테 넌 트에 웹 프런트 엔드를 특정 가상 컴퓨터에서 포트 80에서, 다음 Azure 열립니다 TCP 포트 80 tooall Ip hello에 끝점을 구성 하는 경우 [Azure 클래식 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md)합니다. Hello 작업자 역할만 toohello 내에서 가상 컴퓨터 hello 엽니다 hello 가상 컴퓨터에를 실행 하는 백 엔드 또는 작업자 역할 경우 동일한 테 넌 트.

## <a name="isolation"></a>격리
또 다른 중요 한 클라우드 보안 요구 사항은 분리 tooprevent 공유 다중 테 넌 트 아키텍처에서 배포 간에 정보의 무단 및 의도 하지 않은 전송 합니다.

Azure는 VLAN 격리, ACL, 부하 분산 장치 및 IP 필터를 통해 [네트워크 액세스 제어](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) 및 분리를 구현합니다. 외부 트래픽이 제한 인바운드 tooports 및 정의 하는 가상 컴퓨터에는 프로토콜입니다. 네트워크의 스푸핑 공격을 tooprevent 트래픽을 필터링 하 고 들어오고 나가는 트래픽을 tootrusted 플랫폼 구성 요소를 제한 하는 azure 구현 합니다. 트래픽 흐름 정책은 기본적으로 트래픽을 거부하는 경계 보호 장치에서 구현됩니다.

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-getting-started/sec-azgsfig3.PNG)

네트워크 주소 변환 (NAT) 사용 되는 외부 트래픽에서 tooseparate 내부 네트워크 트래픽이 있습니다. 내부 트래픽은 외부에서 라우팅할 수 없습니다. 외부에서 라우팅할 수 있는 [가상 IP 주소](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx)는 Azure 내에서만 라우팅할 수 있는 [내부 동적 IP](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) 주소로 변환됩니다.

외부 트래픽이 tooAzure 가상 컴퓨터 방화벽을 라우터, 부하 분산 장치 및 계층 3 스위치에 Acl을 통해 사용 합니다. 알려진 특정 프로토콜에만 허용됩니다. Acl 위치 toolimit 트래픽이 tooother Vlan 관리에 사용 되는 게스트 가상 컴퓨터에서 시작 되었습니다. 또한 트래픽 hello 호스트 운영 체제 추가 제한 hello에서 트래픽 모두 데이터 연결 및 네트워크 계층에서 IP 필터를 통해 필터링 됩니다.

### <a name="how-azure-implements-isolation"></a>Azure가 격리를 구현하는 방법
hello Azure 패브릭 컨트롤러는 tootenant 작업 인프라 리소스를 할당 해야 하 고 toovirtual 컴퓨터를 호스트 하는 hello에서 단방향 통신을 관리 합니다. hello Azure 하이퍼바이저 메모리를 적용 하 고 프로세스 구분 하며 가상 컴퓨터 네트워크 트래픽 tooguest OS 테 넌 트를 안전 하 게 라우팅합니다. 또한 Azure는 테넌트, 저장소 및 가상 네트워크에 대한 격리를 구현합니다.

* 각 Azure AD 테넌트는 보안 경계를 사용하여 논리적으로 분리됩니다.
* Azure 저장소 계정의 고유한 tooeach 구독 되며 저장소 계정 키를 사용 하 여 액세스를 인증 합니다.
* 가상 네트워크는 고유한 개인 IP 주소, 방화벽 및 IP ACL의 조합을 통해 논리적으로 격리됩니다. 부하 분산 장치에는 트래픽을 toohello 적절 한 테 넌 트를 끝점 정의에 따라 라우팅합니다.

## <a name="virtual-networks-and-firewalls"></a>가상 네트워크 및 방화벽
hello [분산 및 가상 네트워크를](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) Azure 도움말의 개인 네트워크 트래픽이 다른 Azure 가상 네트워크에서 트래픽을 논리적으로 격리 인지를 확인 합니다.

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-getting-started/sec-azgsfig4.PNG)

구독에는 다수의 격리된 개인 네트워크가 포함될 수 있습니다(방화벽, 부하 분산 및 네트워크 주소 변환 포함).

Azure는 세 가지 기본 수준의 각 Azure의 네트워크 분리 toologically segregate 트래픽 클러스터를 제공 합니다. [가상 local area network](https://azure.microsoft.com/services/virtual-network/) (Vlan)을 사용 하는 hello Azure 네트워크 hello 나머지에서 tooseparate 고객 트래픽이 합니다. 액세스 toohello 외부 hello 클러스터에서 Azure 네트워크 부하 분산 장치를 통해 사용할 수 없습니다.

가상 컴퓨터에서 네트워크 트래픽을 tooand hello 하이퍼바이저 가상 스위치를 통과 해야 합니다. hello 루트 OS에서에서 hello IP 필터 구성 요소는 hello 게스트 가상 컴퓨터 및 다른 hello 게스트 가상 컴퓨터에서 hello 루트 가상 컴퓨터를 격리합니다. 테 넌 트의 노드와 hello 간의 트래픽 toorestrict 통신의 필터링을 수행할 공용 인터넷 (hello 고객의 서비스 구성에 따라)을 다른 테 넌 트에서에 따로 저장 합니다.

hello IP 필터를 사용 하면에서 게스트 가상 컴퓨터를 방지할 수 있습니다.

* 스푸핑된 트래픽 생성.
* 트래픽을 받는 toothem을 해결 했습니다.
* 트래픽 tooprotected 인프라 끝점을 전달 합니다.
* 부적절한 브로드캐스트 트래픽 송신 및 수신.

가상 컴퓨터를 [Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/)에 배치할 수 있습니다. 이러한 가상 네트워크는 온-프레미스 환경에서 구성 하는 비슷한 toohello 네트워크는 일반적으로 가상 스위치에 연결 합니다. 가상 컴퓨터 추가 구성 없이 서로 toohello 동일한 가상 네트워크에서 통신할 수를 연결 합니다. 가상 네트워크 내에 다른 서브넷을 구성할 수도 있습니다.

가상 네트워크에서 Azure 가상 네트워크 기술 toohelp 보안 통신을 수행 하는 hello를 사용할 수 있습니다.

* [**NSG(네트워크 보안 그룹)**](../virtual-network/virtual-networks-nsg.md). 가상 네트워크에 NSG toocontrol 트래픽 tooone 또는 더 많은 가상 컴퓨터 인스턴스를 사용할 수 있습니다. NSG에는 트래픽 방향, 프로토콜, 원본 주소 및 포트, 대상 주소 및 포트에 따라 트래픽을 허용하거나 거부하는 액세스 제어 규칙이 포함되어 있습니다.
* [**사용자 정의 라우팅**](../virtual-network/virtual-networks-udr-overview.md). Hello 패킷을 라우팅할 가상 어플라이언스를 통해 hello tooa 특정 서브넷 toogo tooa 가상 네트워크 보안 어플라이언스 흐르는 패킷이 대 한 다음 홉을 지정 하는 사용자 정의 경로 만들어 제어할 수 있습니다.
* [**IP 전달**](../virtual-network/virtual-networks-udr-overview.md). 가상 네트워크 보안 어플라이언스 tooitself 주소가 지정된 되지 않은 들어오는 트래픽을 tooreceive 수 있어야 합니다. 가상 컴퓨터 tooreceive 트래픽 tooallow tooother 대상 해결, hello 가상 컴퓨터에 대 한 IP 전달 설정 합니다.
* [**강제 터널링**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). 강제 터널링 사용 하면 검사 및 감사용 사이트 간 VPN 터널을 통해 가상 네트워크 백 tooyour 온-프레미스 위치에 가상 컴퓨터에 의해 생성 된 모든 인터넷 바인딩된 트래픽이 "강제" 또는 리디렉션
* [**끝점 ACL**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). 컴퓨터에는 사용할 수 hello 인터넷 tooa 가상 컴퓨터의 인바운드 연결을 가상 네트워크 끝점 Acl을 정의 하 여 제어할 수 있습니다.
* [**파트너 네트워크 보안 솔루션**](https://azure.microsoft.com/marketplace/). Hello Azure Marketplace에서에서 액세스할 수 있는 파트너 네트워크 보안 솔루션의 여러 가지가 있습니다.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Azure가 가상 네트워크 및 방화벽을 구현하는 방법
Azure에서는 기본적으로 모든 호스트 및 게스트 가상 컴퓨터에 패킷 필터링 방화벽을 구현합니다. Hello Azure Marketplace에서 Windows 운영 체제 이미지에는 또한 Windows 방화벽이 기본적으로 활성화 되어 있으며 Azure 공용 네트워크 제어 통신의 hello 경계에서 부하 분산 장치 고객 관리자가 관리 하는 IP Acl에 기반 합니다.

Azure가 정상적인 작업의 일부로 서 또는 재해 발생 중에 고객의 데이터를 이동하면 개인의 암호화된 통신 채널을 통해 수행합니다. 가상 네트워크 및 방화벽에서 Azure toouse에서 사용 되는 다른 기능이 됩니다.

* **네이티브 호스트 방화벽**: Azure Service Fabric 및 Azure Storage는 하이퍼바이저가 없는 네이티브 OS에서 실행됩니다. 따라서 hello 이전 두 규칙 집합이 hello windows 방화벽 구성 됩니다. 저장소 네이티브 toooptimize 성능을 실행합니다.
* **호스트 방화벽**: hello 호스트 방화벽은 hello 하이퍼바이저를 실행 하 tooprotect hello 호스트 운영 체제. hello 규칙 프로그래밍 된 tooallow 전용 hello 서비스 패브릭 컨트롤러는 하 고 특정 포트에서 상자 tootalk toohello 호스트 OS. hello 다른 예외는 tooallow DHCP 응답 및 DNS 회신입니다. Azure에 hello 호스트 운영 체제에 대 한 방화벽 규칙의 hello 템플릿 컴퓨터 구성 파일을 사용 합니다. hello 호스트 자체 알려진, 인증 된 출처에서 Windows 방화벽 구성 toopermit 통신 외부 공격 으로부터 보호 됩니다.
* **게스트 방화벽**: 하지만 다른 소프트웨어 (예: hello 게스트 OS의 hello Windows 방화벽 부분)에 프로그래밍 된 hello 스위치 패킷 필터를 가상 컴퓨터의 hello 규칙을 복제 합니다. hello 게스트 가상 컴퓨터 방화벽에서 hello 호스트 IP 필터 구성에 의해 허용 되는 hello 통신 하는 경우에 hello 게스트 가상 컴퓨터에서 구성 된 toorestrict 통신 tooor 수 있습니다. Toouse hello 게스트 가상 컴퓨터 방화벽 toorestrict 통신 된 Vnet 간 구성 tooconnect tooone 시켜야 하는 예를 들어 다른 합니다.
* **저장소 방화벽 (FW)**: hello 저장소 프런트 엔드에 hello 방화벽에서 포트 80/443 및 기타 필요한 유틸리티 포트에 대해서만 트래픽 toobe 필터링 합니다. hello 저장소 백 엔드에서 hello 방화벽 저장소 프런트 엔드 서버를 통해서만 통신 toocome를 제한합니다.
* **가상 네트워크 게이트웨이**: hello [Azure 가상 네트워크 게이트웨이](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) 는 역할을 Azure 가상 네트워크 tooyour에서 작업을 연결 하는 hello 크로스-프레미스 게이트웨이 온-프레미스 사이트입니다. 필요한 tooconnect tooon 온-프레미스 사이트를 통해는 [IPsec 사이트 간 VPN 터널](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), 또는 [ExpressRoute](../expressroute/expressroute-introduction.md) 회로 합니다. IPsec/IKE VPN 터널에 대 한 hello 게이트웨이 IKE 핸드셰이크가 수행 하 고 hello 가상 네트워크와 온-프레미스 사이트 간에 hello IPsec S2S VPN 터널을 설정 합니다. 또한 가상 네트워크 게이트웨이는 [지점 및 사이트 간 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)을 종료합니다.

## <a name="secure-remote-access"></a>안전한 원격 액세스
Hello 클라우드에 저장 된 데이터 충분 한 보호 기능이 사용 하도록 설정 tooprevent 악용 권한과 기밀성과 무결성에 전송 하는 동안 유지 합니다. 여기에는 조직의 정책 기반, 감사 가능한 ID 및 액세스 관리 메커니즘을 사용하여 연결된 네트워크 제어가 포함됩니다.

기본 제공 암호화 기술을 사용 하면 프로젝트 내부 및 배포의 경우 Azure 지역 및 Azure tooon 온-프레미스 데이터 센터에서 간의 tooencrypt 통신 합니다. 통해 시스템 관리자 액세스 toovirtual [원격 데스크톱 세션](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [원격 Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), hello Azure 포털 항상 암호화 됩니다.

toosecurely 확장 온-프레미스 데이터 센터 toohello 클라우드, Azure 둘 다 제공 [사이트 간 VPN](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) 및 [지점-사이트 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md), 전용된 링크를 더한 [ExpressRoute](../expressroute/expressroute-introduction.md)(가상 네트워크 VPN 통해 암호화 된 연결 tooAzure).

### <a name="how-azure-implements-secure-remote-access"></a>Azure가 안전한 원격 액세스를 구현하는 방법
Azure 포털 연결 toohello는 항상 인증 해야 하며 SSL/TLS 필요 합니다. 관리 인증서 tooenable 보안 관리를 구성할 수 있습니다. [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) 및 [IPsec](https://en.wikipedia.org/wiki/IPsec)과 같은 보안 업계 표준 프로토콜은 완벽하게 지원됩니다.

[Azure ExpressRoute](../expressroute/expressroute-introduction.md)를 사용하면 온-프레미스 또는 공동 배치 환경의 인프라와 Azure 데이터 센터 간에 개인 연결을 만들 수 있습니다. ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 일반적인 인터넷 기반 연결보다 안정성, 빠른 속도, 짧은 대기 시간 및 높은 보안성을 제공합니다. 경우에 따라 ExpressRoute 연결을 사용하여 온-프레미스 위치와 Azure 간에 데이터를 전송하면 상당한 비용 혜택을 얻을 수 있습니다.

## <a name="logging-and-monitoring"></a>로깅 및 모니터링
Azure의 보안 관련 이벤트는 감사 추적을 생성 하는 인증 된 로깅을 제공 되며 엔지니어링된 toobe 안전 tootampering 있습니다. Azure 인프라 가상 컴퓨터 및 Azure AD에서 보안 이벤트 로그와 같은 시스템 정보가 포함됩니다. DHCP 또는 DNS 서버 IP 주소가;으로 변경 하는 이벤트를 수집 하는 포함 되어 보안 이벤트 모니터링 액세스 시도 tooports, 프로토콜, 또는 디자인; 의해 차단 되는 IP 주소 보안 정책 또는 방화벽 설정;의 변경 내용 계정 또는 그룹 생성 및 예기치 않은 프로세스 또는 드라이버를 설치 합니다.

![Azure의 Microsoft 맬웨어 방지](./media/azure-security-getting-started/sec-azgsfig5.PNG)

감사는 권한 있는 사용자 액세스 및 활동, 권한이 부여되거나 무단인 액세스 시도, 시스템 예외 및 보안 이벤트가 설정된 시간 동안 보관되는 정보를 기록합니다. 로그의 hello 보존 판단에 따라 되므로 로그 수집 및 보존 tooyour 고유의 요구 사항을 구성 합니다.

### <a name="how-azure-implements-logging-and-monitoring"></a>Azure가 로깅 및 모니터링을 구현하는 방법
Azure 네이티브 또는 가상 관리 에이전트 (MA) 및 Azure 보안 모니터 (ASM) 에이전트 tooeach 계산, 저장소 또는 관리에서 패브릭 노드를 배포 합니다. 각 관리 에이전트 및 앞으로 미리 구성 된 진단 hello Azure 인증서 저장소에서 가져온 인증서로 구성 된 tooauthenticate tooa 서비스 팀 저장소 계정 및 이벤트 데이터 toohello 저장소 계정에는 합니다. 이러한 에이전트 배포 toocustomers 가상 컴퓨터 않습니다.

Azure 관리자가 인증 되 고 제어 된 액세스 toohello 로그에 대 한 웹 포털을 통해 로그에 액세스 합니다. 관리자는 로그의 구문을 분석하고 필터링하며 상호 연결 및 분석합니다. hello Azure 서비스 팀 저장소 계정 로그에서 직접 관리자 액세스 toohelp 보호에 대 한 로그 변조 방지 합니다.

Microsoft 및 Microsoft 서비스 ACS (Audit Collection)를 사용 하 여 호스트 서버 hello Syslog 프로토콜을 사용 하는 네트워크 장치에서 로그를 수집 합니다. 이러한 로그는 로그 데이터베이스에 배치되고 이를 통해 의심스러운 이벤트에 대한 경고가 생성됩니다. 관리자에 게 액세스 하 고 이러한 로그를 분석할 수 있습니다.

[Azure 진단](https://msdn.microsoft.com/library/azure/gg433048.aspx) toocollect 진단 데이터를 Azure에서 실행 중인 응용 프로그램에서 사용 하면 Azure의 기능입니다. 디버깅 및 문제 해결, 성능 측정, 리소스 사용 모니터링, 트래픽 분석 및 용량 계획, 감사 등에 사용할 수 있는 진단 데이터입니다. Hello 진단 데이터를 수집한 후 전송된 tooan 지 속성에 대 한 Azure 저장소 계정 수 있습니다. 전송은 예약되거나 요청 시에 가능합니다.

## <a name="threat-mitigation"></a>위협 해결 방법
또한 tooisolation, 암호화 및 필터링에 Azure에서는 다양 한 위협 완화 메커니즘 및 프로세스 tooprotect 인프라 및 서비스를 사용합니다. 이러한 내부 제어 및 사용 되는 기술 toodetect 포함 및 DDoS, 권한 상승 및 hello 등과 같은 고급 위협 재구성 [OWASP 상위 10 개](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)합니다.

Microsoft는 클라우드 인프라 줄일 위치 toosecure에 hello 보안 컨트롤 및 위험 관리 프로세스 hello 보안 문제에 대 한 위험 합니다. 인시던트 이벤트 발생을 hello에 hello 보안 인시던트 관리 (SIM) 팀 hello Microsoft 온라인 보안 서비스 및 규정 준수 (OSSC) 팀 내에서 언제 든 지 준비 toorespond은 합니다.

### <a name="how-azure-implements-threat-mitigation"></a>Azure가 위협 해결 방법을 구현하는 방법
Azure 전체 tooimplement 위협 요소 완화에서 보안 제어 않았으며 toohelp 고객 환경에서 잠재적인 위협을 완화 하는 또한 됩니다. hello 다음 사항은 Azure에서 제공 하는 hello 위협 완화 기능:

* [Azure 맬웨어 방지](azure-security-antimalware.md)는 모든 인프라 서버에서 기본적으로 사용됩니다. 필요에 따라 사용자 고유의 가상 컴퓨터 내에서 사용할 수 있습니다.
* Microsoft은 toodetect 위협 서버, 네트워크 및 응용 프로그램 간 모니터링 지속적인 유지 관리 및 악용을 방지 합니다. 자동화 된 알림 내부 및 외부 위협에 tootake 수정 동작을 있도록 비정상적인 동작의 관리자를 게 알립니다.
* 구독 내에서 [Barracuda](https://techlib.barracuda.com/ng54/deployonazure)의 웹 응용 프로그램 방화벽과 같은 타사 보안 솔루션을 배포할 수 있습니다.
* Microsoft의 접근 방식을 toopenetration 테스트 포함 "[빨간색 팀](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)," Microsoft 보안 전문가 들에 실제 세계에 대 한 Azure tootest 방어 (비-고객) 라이브 프로덕션 시스템을 공격 포함 됩니다는 고급 지속 위협입니다.
* 통합된 배포 시스템 hello Azure 플랫폼에서 hello 배포 및 보안 패치 설치를 관리 합니다.

## <a name="next-steps"></a>다음 단계
[Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)

[Azure 보안 팀 블로그](http://blogs.msdn.com/b/azuresecurity/)

[Microsoft 보안 대응 센터](https://technet.microsoft.com/library/dn440717.aspx)

[Active Directory 블로그](http://blogs.technet.com/b/ad/)
