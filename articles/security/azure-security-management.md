---
title: "Azure에서 원격 관리 보안 aaaEnhance | Microsoft Docs"
description: "이 문서에서는 클라우드 서비스, Virtual Machines 및 사용자 지정 응용 프로그램 등 Microsoft Azure 환경을 관리하면서 원격 관리 보안을 향상하는 단계를 설명합니다."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Azure의 보안 관리
Azure 구독자는 관리 워크스테이션, 개발자 PC, 심지어 작업별 사용 권한을 가진 최종 사용자 장치 등 여러 장치에서 자신의 클라우드 환경을 관리할 수 있습니다. 경우에 따라 관리 기능 hello와 같은 웹 기반 콘솔을 통해 수행 됩니다 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다. 다른 경우, 가상 사설망 (Vpn), 터미널 서비스, 클라이언트 응용 프로그램 프로토콜, 또는 (프로그래밍 방식) hello Azure 서비스 관리 API SMAPI ()를 통해 온-프레미스 시스템에서 직접 연결 tooAzure 수 있습니다. 또한 클라이언트 끝점은 태블릿이나 스마트폰 같이 조인 또는 격리되고 관리되지 않는 도메인이 될 수 있습니다.

액세스 및 관리 기능을 여러 다양 한 옵션을 제공 하지만이 가변성 상당한 위험 tooa 클라우드 배포를 추가할 수 있습니다. 것이 어려운 toomanage 추적 및 관리 작업을 감사 합니다. 이 가변성 클라우드 서비스 관리에 사용 되는 비조절형된 액세스 tooclient 끝점을 통해 보안 위협 사용할 수 있습니다. 인프라를 개발 및 관리하기 위한 일반 또는 개인 워크스테이션을 사용 하면 웹 검색(예: 워터링 홀 공격) 또는 전자 메일(예: 소셜 엔지니어링 및 피싱 공격)와 같이 예측할 수 없는 위협 벡터를 열게 됩니다.

![][1]

hello 잠재적인 공격에 대 한 것이 어려운 tooconstruct 보안 정책 및 메커니즘 tooappropriately 광범위 하 게 다양 한 끝점에서 액세스 tooAzure 인터페이스 (예: SMAPI)을 관리 하기 때문에이 유형의 환경에서 증가 합니다.

### <a name="remote-management-threats"></a>원격 관리 위협
공격자는 종종 toogain 권한 있는 액세스를 시도 (예를 들어 암호 무차별 암호 강제 적용, 피싱, 및 자격 증명 수집)를 통해 계정 자격 증명을 손상 시 키 지 또는 사용자가 손상 코드 (예:로 유해한 웹 사이트에서에서 실행 되는로 속이는 행위 드라이브에서 다운로드 또는 유해한 전자 메일 첨부 파일에서). 계정 위반 tooan 발생할 수 있습니다를 원격으로 관리 되는 클라우드 환경에서 위험을 증가 due tooanywhere, 언제 든 지 액세스 합니다.

기본 관리자 계정에 엄격 하 게 제어 된 경우에 하위 수준의 사용자 계정에 보안 전략에 사용 되는 tooexploit 약점 수 있습니다. 적절 한 보안 교육 부족 toobreaches 통해 계정 정보가 노출 되거나 실수로 노출 될 수도 있습니다.

관리 작업에 사용자 워크스테이션도 필요한 경우, 많은 여러 지점에서 손상될 수 있습니다. 사용자 hello 웹 탐색, 타사 및 오픈 소스 도구를 사용 하 여 또는 유해한 문서 파일을 열 하는 트로이 목마 포함 됩니다.

일반적으로 데이터 침해 될 수 있는 가장에 목표 공격에 악용 toobrowser, (예: Flash, PDF, Java) 플러그 인 및 데스크톱 컴퓨터에서 스피어 피싱 (전자 메일) 추적 됩니다. 이러한 컴퓨터에 관리자 수준의 있을 수 있습니다 또는 서비스 수준 권한 tooaccess 라이브 서버 또는 네트워크 장치 개발 또는 다른 자산 관리에 사용 되는 경우 작업에 대 한 합니다.

### <a name="operational-security-fundamentals"></a>작업 보안 기본 사항
보다 안전한 관리 및 작업에 대 한 가능한 진입점의 hello 수를 줄여 클라이언트의 공격을 최소화할 수 있습니다. 이러한 작업은 "의무 분리" 및 "환경의 분리" 보안 원칙을 통해 수행할 수 있습니다.

다른 toodecrease hello 가능성 한 수준에서 실수로 다른 tooa 위반을 leads에서 중요 한 기능을 격리 합니다. 예제:

* 관리 작업 (예를 들어, 인프라 서버를 감염 시킨 다음 관리자의 전자 메일에서 맬웨어) tooa 손상 될 수 있는 작업을 결합 하지 않도록 합니다.
* 높은 민감도 작업에 사용 하는 워크스테이션 hello 같은 시스템 검색 hello 인터넷 위험 수준이 높은 용도 대해 사용할 수 없습니다.

불필요 한 소프트웨어를 제거 하 여 hello 시스템의 공격 노출 영역을 줄입니다. 예제:

* 표준 관리, 지원 또는 개발 워크스테이션 hello 장치의 주요 목적은 toomanage 클라우드 서비스를이 전자 메일 클라이언트 또는 기타 생산성 응용 프로그램의 설치가 필요 하지 않습니다.

클라이언트 시스템 관리자 액세스 tooinfrastructure 구성 요소가 해야 있는 toohello 가장 엄격한 정책 가능한 tooreduce 보안 위험을 거쳐야 합니다. 예제:

* 보안 정책을 hello 장치 및 제한적인 방화벽 구성의 사용에서 인터넷에 대 한 개방형 액세스를 거부 하는 그룹 정책 설정을 포함할 수 있습니다.
* 직접 액세스가 필요한 경우 인터넷 프로토콜 보안(IPsec) VPN을 사용합니다.
* Active Directory 도메인의 관리 및 개발을 별도로 구성합니다.
* 관리 워크스테이션 네트워크 트래픽을 격리 및 필터링합니다.
* 맬웨어 방지 소프트웨어를 사용합니다.
* Multi-factor authentication tooreduce hello 위험 훔친된 자격 증명을 구현 합니다.

또한 액세스 리소스를 통합하고 관리되지 않는 끝점을 제거하면 관리 작업을 단순화할 수 있습니다.

### <a name="providing-security-for-azure-remote-management"></a>Azure의 원격 관리를 위한 보안 제공
Azure는 Azure 클라우드 서비스 및 가상 컴퓨터를 관리 하는 메커니즘 tooaid 관리자 보안을 제공 합니다. 이러한 메커니즘은 다음을 포함합니다.

* 인증 및 [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md).
* 모니터링, 로깅 및 보고.
* 인증서 및 암호화된 통신.
* 웹 관리 포털.
* 네트워크 패킷 필터링.

클라이언트 쪽 보안 구성 및 관리 게이트웨이의 데이터 센터 배포를 사용 가능한 toorestrict 및 모니터 관리자 액세스 toocloud 응용 프로그램 및 데이터 않습니다.

> [!NOTE]
> 이 문서의 특정 권장 사항으로 인해 데이터, 네트워크 또는 계산 리소스 사용량이 증가할 수 있으며 이로 인해 라이선스 또는 구독 비용이 증가할 수 있습니다.
>
>

## <a name="hardened-workstation-for-management"></a>관리용 워크스테이션 강화
워크스테이션 보안 강화의 hello 목표는 모든 tooeliminate 이지만 hello 가장 중요 한 기능에서 필요한 hello 잠재적인 공격 취약 부분을 가능한 한 작게 만드는 toooperate 합니다. 시스템 보안 강화에 설치 된 서비스 및 네트워크 액세스 tooonly 필요한 것을 제한 하는 응용 프로그램 실행을 제한 하는 응용 프로그램의 hello 수를 최소화 하 고 항상 hello 시스템 toodate 가동 포함 되어 있습니다. 또한 관리용 강화 워크스테이션을 사용하면 다른 최종 사용자 작업으로부터 관리 도구 및 활동을 분리합니다.

온-프레미스 엔터프라이즈 환경 내에서 전용된 관리 네트워크, 카드 액세스할 수 있는 서버 룸 및 hello 네트워크의 보호 된 영역에서 실행 되는 워크스테이션 통해 실제 인프라의 hello 공격 노출 영역을 제한할 수 있습니다. 클라우드 또는 하이브리드 IT 모델에서는 보안 관리 서비스에 대 한 효과적인 되 고 더 복잡할 수 있습니다 hello 물리적으로 액세스 tooIT 리소스 부족으로 인해 합니다. 보호 솔루션을 구현하면 세심한 소프트웨어 구성, 보안에 중점을 둔 프로세스, 포괄적인 정책이 필요합니다.

잠금 워크스테이션에 최소 권한 최소화 된 소프트웨어 사용 공간을 사용 하 여 클라우드 관리를 위한-및 응용 프로그램 개발에 대 한-표준화 hello 원격 관리 / 개발 환경에서 보안 문제의 hello 위험을 줄일 수 있습니다. 강화 된 워크스테이션 구성 맬웨어 및 악용에서 사용 하는 많은 일반적인 수단을 닫아 toomanage 사용 되는 중요 한 클라우드 리소스 되는 계정 hello 손상을 방지할 수 있습니다. 사용할 수는 특히, [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) 및 Hyper-v 기술 toocontrol 클라이언트 시스템 동작을 격리 하 고 전자 메일 또는 인터넷 검색을 포함 하는 위협을 완화 합니다.

강화 된 워크스테이션에서 관리자에 게는 표준 사용자 계정 (관리자 수준의 실행을 차단)를 실행 하 고 관련된 응용 프로그램 허용 목록에 의해 제어 됩니다. 강화 된 워크스테이션의 hello 기본 요소는 다음과 같습니다.

* 활성 검색 및 패치. 맬웨어 방지 프로그램 소프트웨어를 배포 하 고, 일반 취약점 검색을 수행 시기 적절 하 게에서 hello 최신 보안 업데이트를 사용 하 여 모든 워크스테이션을 업데이트 합니다.
* 제한된 기능. 필요하지 않은 모든 응용 프로그램을 제거하고 불필요한 (시작) 서비스를 사용하지 않습니다.
* 네트워크 강화. Windows 방화벽 규칙 tooallow만 유효한 IP 주소, 포트 및 Url 관련된 tooAzure 관리를 사용 합니다. 해당 인바운드 원격 연결 toohello 워크스테이션도 차단 됩니다 확인 합니다.
* 실행 제한. 관리 toorun에 필요한 미리 정의 된 실행 파일의 하위 집합만 허용 ("기본 거부" tooas 함). 기본적으로 사용자가 거부 되도록 할지 권한 toorun hello에 명시적으로 정의 하지 않는 한 프로그램이 허용 목록입니다.
* 최소 권한. Hello 자체 로컬 컴퓨터에서 관리 워크스테이션 사용자는 관리 권한이 없어야 합니다. 이러한 방식으로 이러한 또는 변경할 수 없습니다 hello 시스템 구성 hello 시스템 파일을 의도적으로 또는 실수로 합니다.

사용 하 여 이러한 작업을 적용할 수 있습니다 [그룹 정책 개체](https://www.microsoft.com/download/details.aspx?id=2612) (Gpo)에서 Active Directory 도메인 서비스 (AD DS) 및 사용자 (로컬) 관리 도메인 tooall 관리 계정을 통해이 적용 합니다.

### <a name="managing-services-applications-and-data"></a>서비스, 응용 프로그램 및 데이터 관리
Azure 클라우드 서비스 구성은 hello Windows PowerShell 명령줄 인터페이스 또는 RESTful 이러한 인터페이스를 활용 하는 사용자가 작성 한 응용 프로그램을 통해 hello Azure 포털 또는 SMAPI를 통해 수행 됩니다. 이러한 메커니즘을 사용하여 서비스에는 Azure Active Directory(Azure AD), Azure 저장소, Azure 웹 사이트 및 Azure 가상 네트워크 등이 있습니다.

가상 컴퓨터 – 배포할 응용 프로그램 자체 클라이언트 도구 및 필요에 따라, 같은 hello 콘솔 MMC (Microsoft Management), (예: Microsoft System Center 또는 Windows Intune) 엔터프라이즈 관리 콘솔 또는 다른 관리 인터페이스 제공 응용 프로그램-예를 들어 Microsoft SQL Server Management Studio 합니다. 이러한 도구는 일반적으로 엔터프라이즈 환경 또는 클라이언트 네트워크에 상주합니다. 이는 직접적이며 상태 저장 연결이 필요한 RDP(원격 데스크톱 프로토콜)와 같은 특정 네트워크 프로토콜에 따라 다를 수 있습니다. 일부 하지 않아야 하는 공개적으로 게시 되거나 hello 인터넷을 통해 액세스할 수 있는 웹 기반 인터페이스 있을 수 있습니다.

사용 하 여 Azure에서 액세스 tooinfrastructure 및 플랫폼 서비스 관리를 제한할 수 있습니다 [multi-factor authentication](../multi-factor-authentication/multi-factor-authentication.md), [X.509 관리 인증서](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/), 및 방화벽 규칙입니다. Azure 포털 hello 및 SMAPI 보안 TLS (전송 계층) 필요합니다. 그러나 서비스 및 Azure에 배포 하는 응용 프로그램 해야 tootake 보호 되는 측정값 적절 한 응용 프로그램에 따라 합니다. 이러한 메커니즘은 강화된 워크스테이션 구성을 표준화하여 보다 쉽게 자주 사용할 수 있습니다.

### <a name="management-gateway"></a>관리 게이트웨이
모든 관리 toocentralize에 액세스 하 고 모니터링 및 로깅 단순화, 전용 배포할 수 있습니다 [원격 데스크톱 게이트웨이](https://technet.microsoft.com/library/dd560672) RD 게이트웨이 () 서버에 온-프레미스 네트워크에 연결 된 tooyour Azure 환경입니다.

원격 데스크톱 게이트웨이 는 보안 요구 사항을 적용하는 정책 기반 RDP 프록시 서비스입니다. Windows 서버 네트워크 액세스 보호(NAP)와 함께 RD 게이트웨이를 구현하면 Active Directory 도메인 서비스(AD DS) 그룹 정책 개체(GPO)에 의해 설정된 특정 보안 상태 조건을 충족하는 클라이언트만 연결할 수 있는지 확인할 수 있습니다. 또한,

* 프로 비전 한 [Azure 관리 인증서](http://msdn.microsoft.com/library/azure/gg551722.aspx) RD 게이트웨이 hello에 hello 전용 호스트를 사용할 수 있도록 tooaccess hello Azure 포털입니다.
* Hello RD 게이트웨이 toohello 가입 동일한 [관리 도메인](http://technet.microsoft.com/library/bb727085.aspx) hello 관리자 워크스테이션으로 합니다. 이 작업은 필요 단방향 트러스트 tooAzure 광고를 맺고 있는 도메인 내의 사이트 간 IPsec VPN 또는 express 경로 사용 하는 경우 또는 온-프레미스 간의 자격 증명을 페더레이션 하는 경우 AD DS 인스턴스 및 Azure AD.
* 구성 된 [클라이언트 연결 권한 부여 정책](http://technet.microsoft.com/library/cc753324.aspx) toolet hello RD 게이트웨이 hello 클라이언트 컴퓨터 이름이 유효한 (도메인에 가입)를 허용된 tooaccess hello Azure 포털을 확인 합니다.
* 에 대 한 IPsec을 사용 하 여 [Azure VPN](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther 도청 및 토큰을 도용에서 관리 트래픽을 보호 하거나 격리 된 인터넷 링크를 통해 [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/)합니다.
* Multi-Factor Authentication([Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)을 통해) 또는 RD 게이트웨이를 통해 로그인하는 관리자를 위한 스마트 카드 인증을 사용합니다.
* 원본 구성 [IP 주소 제한을](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) 또는 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) Azure toominimize hello 수가 허용 된 관리 끝점에 있습니다.

## <a name="security-guidelines"></a>보안 지침
일반적으로 사용 hello 클라우드로 모든 워크스테이션 온-프레미스에 사용 되는 비슷한 toohello 환경을 위해 toosecure 관리자 워크스테이션을 지원-예를 들어, 빌드 및 제한적인 사용 권한을 최소화 합니다. 클라우드 관리의 몇 가지 고유한 요소는 더 김 윤 식 tooremote 또는 엔터프라이즈 대역외 관리입니다. 여기에 자격 증명, 원격 액세스 보안 및 위협 요소 탐지 및 응답에 대 한 감사 및 hello 사용 됩니다.

### <a name="authentication"></a>인증
관리 도구에 액세스 하기 위한 Azure 로그온 제한을 tooconstrain 원본 IP 주소를 사용 하 고 액세스 요청을 감사할 수 있습니다. Azure toohelp SMAPI (고객 개발 도구를 통해 Windows PowerShell cmdlet 등)와 hello Azure 포털 toorequire 클라이언트 관리 인증서 toobe 구성할 수 있습니다 관리 클라이언트 (워크스테이션 또는 응용 프로그램)를 식별 합니다. 또한 tooSSL 인증서를 설치 합니다. 또한 관리자 액세스에 대해 다단계 인증을 요구하는 것이 좋습니다.

Azure에 배포하는 일부 응용 프로그램 또는 서비스는 최종 사용자와 관리자 액세스를 위한 자체 인증 메커니즘이 있을 수 있지만, 다른 것들은 Azure AD를 최대한 활용합니다. 디렉터리 동기화를 사용 하 여 hello에서 전적으로 사용자 계정 유지 관리 또는 Active Directory Federation Services (AD FS)을 통해 자격 증명을 페더레이션는 여부에 따라 클라우드를 사용 하 여 [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (의 일부로 Azure AD Premium) hello 리소스 간의 identity 주기를 관리할 수 있습니다.

### <a name="connectivity"></a>연결
몇 가지 메커니즘은 사용 가능한 toohelp 보안 클라이언트 연결 tooyour Azure 가상 네트워크입니다. 이러한 메커니즘 중 두 [사이트 간 VPN](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) 및 [지점-사이트 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) 업계의 hello 사용을 활성화 하는 (P2S) 표준 IPsec (S2S) 또는 hello [Secure Socket Tunneling Protocol](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) 암호화 및 터널링 합니다. Azure는 Azure 포털 hello 같은 toopublic 용 Azure 서비스 관리에 연결할 때 Azure 하이퍼텍스트 전송 프로토콜 보안 (HTTPS) 필요 합니다.

독립 실행형 강화 된 워크스테이션의 tooAzure RD 게이트웨이 통해 연결 되지 않은 사용 하 여 hello SSTP 기반 지점-사이트 VPN toocreate hello 초기 연결 toohello Azure 가상 네트워크를 설정 해야 RDP 연결 tooindividual 가상 hello VPN 터널에서 컴퓨터를 설정 합니다.

### <a name="management-auditing-vs-policy-enforcement"></a>감사 관리 및 정책 적용
일반적으로 두 가지가 toosecure 관리 프로세스에 도움이 되: 감사 및 정책 적용 합니다. 두 방식 다 포괄적으로 제어하지만, 모든 상황에서 가능하지 않을 수도 있습니다. 또한 각 방법에는 서로 다른 수준의 비용, 위험과 특히 한 관계로 toohello 개인과 시스템 아키텍처에 배치 하는 신뢰 수준의 보안을 관리와 관련 된 활동에 있습니다.

모니터링, 로깅 및 감사 추적 및 관리 작업을 이해 하는 것에 대 한 기초를 제공 하지만에서 작업을 모두 완료 인해 생성 된 데이터 양 toohello 세부 불가능 tooaudit 항상 아닐 수 있습니다. 그러나 Hello 관리 정책의 hello 효율성을 감사는는 것이 좋습니다.

엄격한 액세스 제어를 포함하는 정책은 프로그래밍 방식 메커니즘을 관리자 작업을 관리할 수 있는 장소에 적용하고 모든 가능한 보호 조치가 사용되도록 합니다. 로깅 누가 무엇을 했는지에, 위치 및 시기에서 추가 tooa 레코드에 적용의 증거를 제공 합니다. 또한 로깅 사용 하면 관리자가 정책을 지키는 방법에 대 한 tooaudit 및 상호 검사가 정보 및 활동의 증거를 제공

## <a name="client-configuration"></a>클라이언트 구성
강화된 워크스테이션에 대한 세 가지 기본 구성을 지정하는 것이 좋습니다. hello 가장 큰 차이점으로 모든 옵션 전체에서 유사한 보안 프로필을 유지 하면서 비용, 효용성 및 내게 필요한 옵션을 됩니다. 다음 표에서 hello hello 이점과 위험 평가 tooeach의 짧은 분석을 제공 합니다. (참고 "회사 PC" 역할에 관계 없이 모든 도메인 사용자가 tooa 표준 데스크톱 PC 구성이 배포는 참조 합니다.)

| 구성 | 이점 | 단점 |
| --- | --- | --- |
| 독립 실행형 강화된 워크스테이션 |밀접하게 제어된 워크스테이션 |전용 데스크톱의 비용 증가 |
| - | 응용 프로그램 악용 위험성 감소 |관리 노력 감소 |
| - | 업무의 명확한 분할 | - |
| 회사 PC의 가상 컴퓨터화 |하드웨어 비용 감소 | - |
| - | 역할 및 응용 프로그램의 분리 | - |
| BitLocker 드라이브 암호화와 함께 Windows toogo |대부분의 PC와의 호환성 |자산 추적 |
| - | 비용 효율성 및 이식성 | - |
| - | 격리된 관리 환경 |- |

Hello 강화 된 워크스테이션 호스트인 hello 및 hello hello 간의 아무 것도 없으면 게스트 호스팅하지 운영 체제 및 hello 하드웨어 유용 합니다. "클린 소스 원칙" hello (라고도 "보안 원점") 의미 hello 호스트 하는 hello 가장 강화 해야 합니다. 그렇지 않으면 hello 강화 된 워크스테이션 (게스트)은 주체 tooattacks 호스팅되어 있는 hello 시스템에 있습니다.

Hello 도구만 있는 각 강화 된 워크스테이션에 대 한 전용된 시스템 이미지를 통한 관리 기능을 더 세분 수 및 필요한 관리 하기 위한 Azure 선택 권한과 클라우드 hello에 대 한 특정 로컬 AD DS Gpo와 응용 프로그램 필요한 작업입니다.

없는 온-프레미스 인프라 (예를 들어 없습니다 액세스 tooa hello 클라우드에 있는 모든 서버가 로컬 AD DS 인스턴스 Gpo에 대 한), 설치 된 IT 환경에 대 한 서비스와 같은 [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) 배포 및 유지 관리를 간소화할 수 워크스테이션 구성 합니다.

### <a name="stand-alone-hardened-workstation-for-management"></a>관리를 위한 독립 실행형 강화된 워크스테이션
독립 실행형 강화된 워크스테이션에서 관리자는 관리 작업에 PC나 랩톱을 사용하고, 비 관리 작업에는 다른 별도의 PC 또는 랩톱을 사용합니다. 전용 워크스테이션 toomanaging Azure 서비스는 다른 응용 프로그램이 설치 필요 하지 않습니다. 또한 TPM([신뢰할 수 있는 플랫폼 모듈](https://technet.microsoft.com/library/cc766159)) 또는 유사한 하드웨어 수준 암호화 기술을 지원하는 워크스테이션을 사용하면 장치를 인증하고 특정 공격을 방지할 수 있습니다. TPM hello 시스템 드라이브의 전체 볼륨 보호를 사용 하 여도 지원할 수 있습니다 [BitLocker 드라이브 암호화](https://technet.microsoft.com/library/cc732774.aspx)합니다.

Hello 독립 실행형 강화 된 워크스테이션 시나리오 (아래 참조), Windows 방화벽 (또는 Microsoft 이외의 클라이언트 방화벽) hello 로컬 인스턴스는 구성 된 tooblock 인바운드 RDP와 같은 연결 합니다. 관리자에 게 toohello 로그온 할 수 워크스테이션을 확정 강화 된 워크스테이션 및 tooAzure 설정한 VPN은 Azure 가상 네트워크를 사용 하 여 연결 하지만 tooa 회사 PC 및 사용 하 여 RDP tooconnect toohello가 로그온 후에 연결 하는 RDP 세션 시작 자체입니다.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>회사 PC의 가상 컴퓨터화
별도 독립 실행형 강화 된 워크스테이션 제한 된다는 가정 때나 hello 비용 있는 경우에 강화 된 워크스테이션 가상 컴퓨터 tooperform 비 관리 작업을 호스트할 수 있습니다.

![][3]

tooavoid 워크스테이션 1 대를 사용 하 여 시스템 관리 및 기타 일상적인 작업 작업에 대 한에서 발생할 수 있는 몇 가지 보안 위험을 배포할 수 있습니다 Windows Hyper-v 가상 컴퓨터 toohello 워크스테이션을 강화 합니다. 이 가상 컴퓨터는 회사 PC hello으로 사용할 수 있습니다. hello 회사 PC 환경 hello 공격 노출 줄어들고 (예: 전자 메일) hello 사용자의 일별 활동을 함께 사용 되는 민감한 관리 작업에서 제거 하는 호스트에서에서 분리 되어 수 있습니다.

hello 회사 PC 가상 컴퓨터는 보호 된 공간에서 실행 하 고 사용자가 응용 프로그램을 제공 합니다. hello 호스트 남습니다 "정리" 하 고 hello 루트 운영 체제 (예를 들어 차단에서 RDP에 액세스할 hello 가상 컴퓨터)에서 엄격한 네트워크 정책을 적용 합니다.

### <a name="windows-toogo"></a>Windows tooGo
다른 대체 toorequiring 독립 실행형 강화 된 워크스테이션은 toouse는 [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx) 드라이브, USB 부팅 하는 클라이언트 쪽 기능 지원 기능을 합니다. Windows tooGo 암호화 된 USB 플래시 드라이브에서 실행 하는 사용자가 tooboot 호환 PC tooan 격리 시스템 이미지를 수 있습니다. 최소 OS 빌드, 엄격한 보안 정책 사용 하 여 회사 IT 그룹에 의해 hello 이미지를 완전히 관리 하려면 TPM을 지원 하기 때문에 원격 관리 끝점에 대 한 추가 제어 기능을 제공 합니다.

아래 그림 hello에서 hello 이식 가능 이미지는 미리 구성 된 tooconnect만 tooAzure은 multi-factor authentication을 하며 모든 비 관리 트래픽을 차단 하는 도메인에 가입 된 시스템. 사용자 부팅 동일한 PC toohello 표준 회사 이미지와 Azure 관리 도구에 대 한 RD 게이트웨이 액세스 시도 hello, hello 세션 차단 됩니다. Windows tooGo hello 루트 수준의 운영 체제 되며 없는 추가 계층은 필요한 (호스트 운영 체제, 하이퍼바이저, 가상 컴퓨터) toooutside 공격 으로부터 더 취약 있을 수 있습니다.

![][4]

USB 플래시 드라이브는 보다 쉽게 손실 된 평균 데스크톱 PC 보다 중요 한 toonote 것 합니다. BitLocker tooencrypt hello 전체 볼륨, 강력한 암호를 함께 사용 하면 공격자가 유해한 용도로 hello 드라이브 이미지를 사용할 수 가능성이 더 낮아집니다. 또한 hello USB 플래시 드라이브를 분실 한 경우 취소 및 [새 관리 인증서를 발급](https://technet.microsoft.com/library/hh831574.aspx) 빠른 암호와 함께 재설정 노출을 줄일 수 있습니다. 관리 감사 로그 상주할 Azure 내에서 하지 hello 클라이언트에 데이터 손실의 더욱 줄입니다.

## <a name="best-practices"></a>모범 사례
Hello를 응용 프로그램 및 Azure에서 데이터를 관리 하는 경우 추가 지침을 따르는 것이 좋습니다.

### <a name="dos-and-donts"></a>실행 사항 및 금지 사항
워크스테이션 잠겨 있기 때문에 다른 일반적인 보안 요구 사항이 필요로 하지 않는다는 사실을 충족 toobe 가정 하지 마십시오. hello에 대 한 위험이 정보는 관리자 계정을 일반적으로 소유 하는 상승 된 액세스 수준 때문에 더 빨라집니다. 위험 및 대체는 안전 하 게 보호 방법의 예는 hello 테이블 아래에 표시 됩니다.

| 금지 사항 | 실행 사항 |
| --- | --- |
| 관리자 액세스 또는 기타 암호(예: SSL 또는 관리 인증서)에 대한 자격 증명을 전자 메일로 보내지 마세요. |계정 이름 및 음성 암호(음성 메일에는 저장되지 않음)를 제공하여 기밀성을 유지하거나, 클라이언트/서버 인증서의 원격 설치를 수행하거나(암호화된 세션을 통해), 보호된 네트워크 공유에서 다운로드하거나, 이동식 미디어를 통해 직접 배포합니다. |
| - | 관리 인증서 수명 주기를 사전 관리합니다. |
| 암호화되지 않았거나 해시되지 않은 응용 프로그램 저장소(스프레드시트, SharePoint 사이트 또는 파일 공유 등)에 계정 암호를 저장하지 마세요. |보안 관리 원칙 및 시스템 정책, 강화 설정 하 고 tooyour 개발 환경에 적용 합니다. |
| - | 사용 하 여 [고급 완화 경험 도구 키트 5.5](https://technet.microsoft.com/security/jj653751) tooensure 적절 한 액세스 tooAzure SSL/TLS 사이트 규칙 인증서 고정 합니다. |
| 관리자 간 계정 및 암호를 공유하거나, 여러 사용자 계정 또는 서비스, 특히 소셜 미디어 또는 기타 비 관리 작업에 암호를 다시 사용하지 마세요. |Azure 구독 전용된 Microsoft 계정 toomanage 만들기-개인 전자 메일에 대 한 사용 되지 않는 계정. |
| 구성 파일을 전자 메일로 보내지 마세요. |구성 파일 및 프로필은 전자 메일 등 쉽게 손상될 수 있는 메커니즘이 아닌 신뢰할 수 있는 소스(예: 암호화된 USB 플래시 드라이브)로부터 설치해야 합니다. |
| 약하거나 단순한 로그온 암호를 사용하지 마세요. |강력한 암호 정책, 만료 주기(changeon-first-use), 콘솔 시간 제한, 자동 계정 잠금 등을 적용합니다. 암호 자격 증명 모음 액세스용 다단계 인증으로 클라이언트 암호 관리 시스템을 사용합니다. |
| 관리 포트 toohello 인터넷을 제공 하지 마십시오. |Azure 포트 및 IP 주소 toorestrict 관리 액세스를 잠금. 자세한 내용은 참조 hello [Azure 네트워크 보안](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) 백서에 나와 있습니다. |
| - | 모든 관리 연결에 대한 방화벽, VPN 및 NAP를 사용합니다. |

## <a name="azure-operations"></a>Azure 작업
Microsoft의 Azure 작업 내에서, Azure의 프로덕션 시스템에 액세스하는 작업 엔지니어 및 고객 지원 담당자는 회사 내부 네트워크 액세스 및 응용 프로그램(예: 전자 메일, 인트라넷 등)을 위해 프로비전되고 [VM으로 강화된 워크스테이션 PC](#stand-alone-hardened-workstation-for-management)를 사용합니다. 일부 관리 워크스테이션 컴퓨터에 Tpm, hello 호스트 부팅 드라이브를 BitLocker로 암호화 되어 있고 조인된 tooa 특별 한 조직 구성 단위 (OU)에서 Microsoft의 기본 회사 도메인.

중앙 집중화된 소프트웨어 업데이트와 함께 그룹 정책을 통해 시스템 강화가 적용됩니다. 감사 및 분석을 위해 (예: 보안 및 AppLocker) 이벤트 로그 관리 워크스테이션에서 수집 되며 tooa 중앙 위치에 저장 됩니다.

또한 전용된 점프-상자 Microsoft의 네트워크에서 2 단계 인증을 요구 하는 사용 되는 tooconnect tooAzure 프로덕션 네트워크.

## <a name="azure-security-checklist"></a>Azure 보안 검사 목록
Hello 강화 된 워크스테이션에서 관리자가 수행할 수 있는 작업 수를 최소화 개발 및 관리 환경에서 hello 공격 노출 영역을 최소화 하는 데 도움이 됩니다. 다음 기술 toohelp 사용 하 여 hello 강화 된 워크스테이션을 보호 합니다.

* IE 보안 강화. hello Internet Explorer 브라우저 (또는 해당 문제에 대 한 모든 웹 브라우저)은 외부 서버와 광범위 한 상호 작용 tooits 인해 손상 코드에 대 한 주요 진입점입니다. 클라이언트 정책을 검토하고 보호 모드에서 실행, 추가 기능 사용 안 함, 파일 다운로드 사용 안 함, [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx) 필터링 사용 등을 적용합니다. 보안 경고가 표시되는지 확인 합니다. 인터넷 영역을 활용하고 적절한 강화를 구성한 신뢰할 수 있는 사이트의 목록을 만듭니다. 다른 모든 사이트 및 ActiveX 및 Java와 같은 브라우저 내 코드를 차단합니다.
* 표준 사용자. 표준 사용자는 다양 한 이점이 실행, hello는 가장 큰 하 맬웨어를 통해 관리자 자격 증명을 도용 하기가 더 어려워집니다입니다. 그리고 표준 사용자 계정에 없는 상승 된 권한 hello 루트 운영 체제에서 많은 구성 옵션 및 Api가 잠겨 기본적으로 합니다.
* AppLocker. 사용할 수 있습니다 [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict hello 프로그램 및 사용자가 실행할 수 있는 스크립트입니다. 감사 또는 적용 모드에서 AppLocker를 실행할 수 있습니다. AppLocker는 기본적으로 hello 클라이언트에서 모든 코드 관리 토큰 toorun 권한이 있는 사용자가 수 있는 허용 규칙을 있습니다. 이 규칙은 out, 자신을 잠그지에서 tooprevent 관리자 있으며 tooelevated 토큰에만 적용 됩니다. 또한 Windows Server [핵심 보안](http://technet.microsoft.com/library/dd348705.aspx)의 일부인 코드 무결성도 참조하세요.
* 코드 서명. 관리자가 사용하는 모든 도구와 스크립트를 코드 서명하면 응용 프로그램 잠금 정책을 배포하기 위한 관리 가능형 메커니즘을 제공합니다. 해시 신속 하 게 변경 내용 toohello 코드로 비율이 조정 되지 않음 및 파일 경로 높은 수준의 보안을 제공 하지 않습니다. PowerShell을 사용 하 여 AppLocker 규칙을 관찰 해야 [실행 정책을](http://technet.microsoft.com/library/ee176961.aspx) 하는 특정 서명 된 코드와 toobe 스크립트 [실행](http://technet.microsoft.com/library/hh849812.aspx)합니다.
* 그룹 정책. 전역 관리자 정책 만들기 관리 (및 다른 모든에서 액세스 차단)에 사용 되는 적용 된 tooany 도메인 워크스테이션 이며 해당 워크스테이션에서 toouser 계정을 인증 합니다.
* 보안이 강화된 프로비전. 초기 강화 된 워크스테이션 이미지를 보호 toohelp 변조 방지 합니다. 암호화 및 격리 toostore 이미지, 가상 컴퓨터 및 스크립트와 같은 보안 조치를 사용 하 고 (아마도 감사 가능한 체크 인/체크 아웃을 사용 하 여 프로세스) 액세스를 제한 합니다.
* 패치 일관성 있는 빌드를 유지 관리 (했거나 개발, 작업 및 기타 관리 작업에 대해 별도 이미지)를 변경 하 고 맬웨어 정기적으로, hello 쌓이게 toodate 유지 하 고 필요할 때에 컴퓨터를 정품 인증에 대 한 검색 합니다.
* 암호화. 관리 워크스테이션 안전 하 게 사용 되는 TPM toomore 갖도록 [파일 시스템 암호화](https://technet.microsoft.com/library/cc700811.aspx) (EFS) 및 BitLocker 합니다. Windows tooGo를 사용 하는 경우 BitLocker와 함께 암호화 된 USB 키를 사용 합니다.
* 관리 AD DS Gpo toocontrol 파일 공유와 같은 모든 hello 관리자의 Windows 인터페이스를 사용 합니다. 감사, 모니터링 및 로깅 프로세스에 관리 워크스테이션을 포함합니다. 모든 관리자 및 개발자 액세스 및 사용을 추적합니다.

## <a name="summary"></a>요약
Azure 클라우드 서비스, 가상 컴퓨터 및 응용 프로그램을 관리하기 위해 강화된 워크스테이션 구성을 사용하면 중요한 IT 인프라를 원격으로 관리함으로써 발생할 수 있는 다양한 위험 및 위협을 방지할 수 있습니다. Azure와 Windows 보호 하 고 통신, 인증 및 클라이언트 동작을 제어 하는 toohelp를 사용할 수 있는 메커니즘을 제공 합니다.

## <a name="next-steps"></a>다음 단계
hello 다음 리소스를 사용할 수 있는 tooprovide Azure에 대 한 자세한 내용은 관련 Microsoft 서비스,이 문서에서 참조 하는 추가 toospecific 항목 및:

* [권한 있는 액세스 보안](https://technet.microsoft.com/library/mt631194.aspx) – 디자인 및 Azure 관리에 대 한 보안 관리 워크스테이션을 빌드하기 위한 hello 기술 세부 정보 가져오기
* [Microsoft 보안 센터](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) -Azure 패브릭이 hello를 보호 하는 Azure 플랫폼 기능에 대 한 자세한 내용은 및 작업에서 실행된 Azure hello
* [Microsoft 보안 대응 센터](http://www.microsoft.com/security/msrc/default.aspx) -Microsoft 보안 취약점을 azure에 대 한 문제를 포함 하는 보고 될 수 없거나 전자 메일을 통해 너무[secure@microsoft.com](mailto:secure@microsoft.com)
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) – Azure 보안에 최신 hello에 toodate 계속 확인

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
