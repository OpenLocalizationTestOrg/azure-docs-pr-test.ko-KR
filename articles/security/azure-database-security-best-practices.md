---
title: "aaaAzure 데이터베이스 보안 모범 사례 | Microsoft Docs"
description: "이 문서에서는 Azure 데이터베이스 보안을 위한 일단의 모범 사례를 제공합니다."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Azure 데이터베이스 보안 모범 사례

보안은 데이터베이스 관리에서 가장 중요하며 항상 Azure SQL Database의 최우선 순위였습니다. 데이터베이스 수 밀접 하 게 보안된 toohelp 가장 규정 충족 또는 다른 규칙 으로부터 HIPAA, 27002/ISO 27001, PCI DSS 수준 1 등의 보안 요구 사항입니다. Hello에 사용할 수 있는 보안 규정 준수 인증의 최신 목록은 [Microsoft 보안 센터 사이트](http://azure.microsoft.com/support/trust-center/services/)합니다. Tooplace 규정 요구 사항에 따라 특정 Azure 데이터 센터에서 데이터베이스를 선택할 수도 있습니다.

이 문서에서는 Azure 네트워크 보안 모범 사례 모음에 대해 설명합니다. 이들 모범 사례는 경험상 Azure 데이터베이스 보안 및 고객의 hello 경험을와 같은 직접 합니다.

각 모범 사례에 대해 다음과 같이 설명합니다.

-   어떤 hello 것이 좋습니다.
-   이유는 tooenable 최선의 방법을
-   Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴
-   Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.

이 Azure 데이터베이스 보안 모범 사례 문서 합의 의견 및 Azure 플랫폼 기능에 기반 및이 문서가 작성 된 hello 시 존재 하므로 기능을 설정 합니다. 의견 및 기술 시간이 지남에 따라 변경 하 고이 문서 됩니다. 이러한 변경 내용을 정기적으로 tooreflect에서 업데이트 합니다.

이 문서에서 다루는 Azure 데이터베이스 보안 모범 사례는 다음과 같습니다.

-   방화벽 규칙 toorestrict 데이터베이스 액세스를 사용 하 여
-   데이터베이스 인증 사용
-   암호화를 사용하여 데이터 보호
-   전송 중인 데이터 보호
-   데이터베이스 감사 사용
-   데이터베이스 위협 검색 사용


## <a name="use-firewall-rules-toorestrict-database-access"></a>방화벽 규칙 toorestrict 데이터베이스 액세스를 사용 하 여

Microsoft Azure SQL Database는 Azure 및 기타 인터넷 기반 응용 프로그램의 관계형 데이터베이스 서비스를 제공합니다. tooprovide 액세스 보안, SQL 데이터베이스의 id 및 사용자가 toospecific 작업 및 데이터를 제한 하는 권한 부여 메커니즘 사용자 tooprove를 요구 하는 인증 메커니즘 IP 주소로 연결을 제한 하는 방화벽 규칙으로 액세스를 제어 합니다. 방화벽은 권한이 있는 컴퓨터를 지정할 때까지 모든 액세스 tooyour 데이터베이스 서버를 차단 합니다. hello 방화벽 액세스 toodatabases hello 시작 IP 주소를 각 요청에 따라 권한을 부여 합니다.

![방화벽 규칙](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

hello Azure SQL 데이터베이스 서비스 TCP 포트 1433 통해서만 제공 됩니다. 사용자의 컴퓨터에서 SQL 데이터베이스 tooaccess 클라이언트 컴퓨터 방화벽이 TCP 포트 1433에서 보내는 TCP 통신을 허용 하는지 확인 합니다. 다른 응용 프로그램에 필요하지 않은 경우 방화벽 규칙을 사용하여 1433 TCP 포트에서 인바운드 연결을 차단합니다.

Hello 연결 프로세스의 일환으로, Azure 가상 컴퓨터에서 연결은 리디렉션된 tooa 다른 IP 주소와 포트를 각 작업자 역할에 대해 고유 합니다. hello 포트 번호가 11000 too11999에서 hello 사이입니다. TCP 포트에 대한 자세한 내용은 [ADO.NET 4.5 및 SQL Database2에 대한 1433 이외의 포트](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12)를 참조하세요.

> [!Note]
> SQL Database의 방화벽 규칙에 대한 자세한 내용은 [SQL Database 방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)을 참조하세요.

## <a name="enable-database-authentication"></a>데이터베이스 인증 사용
SQL Database는 인증을 위해 두 가지 인증 유형, 즉 SQL 인증 및 Azure AD 인증(Azure Active Directory 인증)을 지원합니다.

**SQL 인증**은 다음과 같은 경우에 권장됩니다.

-   Windows 도메인으로 모든 사용자가 인증 되지 않은 혼합된 운영 체제를 사용 하 여 SQL Azure toosupport 환경이 있습니다.
-   SQL Azure toosupport 이전 응용 프로그램 및 SQL Server 인증을 필요로 하는 타사에서 제공 되는 응용 프로그램을 허용 합니다.
-   알 수 없거나 신뢰할 수 없는 도메인에서 사용자가 tooconnect을 수 있습니다. 예를 들어 기존된 고객이 연결할 응용 프로그램의 주문의 tooreceive hello 상태로 SQL Server 로그인을 할당 합니다.
-   허용 SQL Azure toosupport 웹 기반 응용 프로그램 사용자가 자신의 id를 만들 수 있는 합니다.
-   소프트웨어를 사용 하면 복잡 한 권한 계층 구조를 사용 하 여 응용 프로그램에 따라 개발자 toodistribute에 SQL Server 로그인이 사전 설정 알 수 있습니다.

> [!Note]
> 그러나 SQL Server 인증에서는 Kerberos 보안 프로토콜을 사용할 수 없습니다.

**SQL 인증**을 사용하는 경우 다음을 수행해야 합니다.

-   사용자가 직접 hello 강력한 자격 증명을 관리 합니다.
-   Hello 연결 문자열에 hello 자격 증명을 보호 합니다.
-   (잠재적으로) hello 웹 서버 toohello 데이터베이스에서 hello 네트워크를 통해 전달 되는 hello 자격 증명을 보호 합니다. 자세한 내용은 참조 [하는 방법: ASP.NET 2.0에서 서버를 사용 하 여 SQL 인증 tooSQL 연결](https://msdn.microsoft.com/library/ms998300.aspx)합니다.

**Azure Active Directory 인증** tooMicrosoft Azure SQL 데이터베이스를 연결 하는 메커니즘은 및 [SQL 데이터 웨어하우스](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) Azure Active Directory (Azure AD)에 id를 사용 하 여 합니다. Azure AD 인증을 사용 하면 데이터베이스 사용자의 신원을 hello 및 하나의 중앙 위치에서 다른 Microsoft 서비스를 중앙에서 관리할 수 있습니다. ID 관리를 중앙 toomanage 데이터베이스 사용자를 한 위치를 제공 하 고 사용 권한 관리를 간소화 합니다. Hello 다음을 이점입니다.

-   대체 tooSQL 서버 인증을 제공합니다.
-   사용 하면 데이터베이스 서버에 대해 hello 확산 됨에 따라 사용자 id를 중지합니다.
-   한 곳에서 암호를 회전할 수 있습니다.
-   고객이 외부(AAD) 그룹을 사용하여 데이터베이스 사용 권한을 관리할 수 있습니다.
-   Windows 통합 인증 또는 Azure Active Directory에서 지원하는 기타 인증을 사용하여 암호 저장을 제거할 수 있습니다.
-   Azure AD 인증 hello 데이터베이스 수준에서 포함 된 데이터베이스 사용자 tooauthenticate id를 사용합니다.
-   Azure AD 연결 tooSQL 데이터베이스 응용 프로그램에 대 한 토큰 기반 인증을 지원 합니다.
-   Azure AD 인증은 도메인 동기화 없이 로컬 Azure Active Directory에 대해 ADFS(도메인 페더레이션) 또는 기본 사용자/암호 인증을 지원합니다.
-   Azure AD는 MFA(Multi-Factor Authentication)를 포함하는 Active Directory 유니버설 인증을 사용하는 SQL Server Management Studio를 통해 연결하도록 지원합니다. MFA는 전화 통화, 문자 메시지, 모바일 앱 알림 등의 여러 가지 간편한 검증 옵션을 제공하는 강력한 인증을 포함합니다. 자세한 내용은 [SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 Azure AD MFA에 대한 SSMS 지원](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.

hello 구성 단계 hello 프로시저 tooconfigure 다음을 포함 하 고 Azure Active Directory 인증을 사용 합니다.

-   Azure AD를 만들고 채웁니다.
-   옵션: 연결 하거나 현재 Azure 구독과 연결 되어 있는 hello active directory 변경 합니다.
-   Azure SQL Server 또는 [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/)에 대한 Azure Active Directory 관리자를 만듭니다.
- 클라이언트 컴퓨터를 구성합니다.
-   AD id에 매핑된 데이터베이스 tooAzure 포함 된 데이터베이스 사용자를 만듭니다.
-   Azure AD id를 사용 하 여 tooyour 데이터베이스를 연결 합니다.

자세한 내용은 [여기](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)서 찾을 수 있습니다.

## <a name="protect-your-data-using-encryption"></a>암호화를 사용하여 데이터 보호

[Azure SQL 데이터베이스 투명 한 데이터 암호화 (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) 의 hello 데이터베이스에 연결 된 백업, 실시간 암호화 / 해독을 수행 하 여 악의적인 활동의 hello 취약점 으로부터 보호 하 고 트랜잭션 로그 파일 없이 미사용 필요한 변경 내용 toohello 응용 프로그램입니다. TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다.

Hello 전체 저장소를 암호화 한 경우에 반드시 tooalso 자체 데이터베이스를 암호화 합니다. Hello 철저 한 방어 데이터 보호 방법은의 구현입니다. Azure SQL 데이터베이스를 사용 하는 경우 신용 카드나 주민 등록 번호 같은 중요 한 데이터 tooprotect 보려면 FIPS 140-2의 유효성을 검사 256 비트 AES 암호화 (예: HIPAA, 많은 업계 표준의 hello 요구 사항을 충족 하는 데이터베이스를 암호화할 수 있습니다. PCI)입니다.

이 파일 toounderstand 너무 관련 중요[버퍼 풀 확장 (BPE)](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) TDE를 사용 하 여 데이터베이스를 암호화 하는 경우 암호화 하지 않습니다. 와 같은 파일 시스템 수준 암호화 도구를 사용 해야 [BitLocker](https://technet.microsoft.com/library/cc732774) 또는 hello [암호화 EFS (파일 시스템)](https://technet.microsoft.com/library/cc700811.aspx) BPE 관련 파일입니다.

이후 권한 있는 사용자는 보안 관리자 또는 데이터베이스 관리자가 hello 데이터베이스가 암호화 TDE를 사용 하는 경우에 hello 데이터를 액세스할 수와 같은 hello 권장 사항도 따라야 아래:

-   Hello 데이터베이스 수준에서 SQL 인증을 사용 하도록 설정 합니다.
-   [RBAC 역할](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)을 사용하는 Azure AD 인증을 사용해야 합니다.
-   사용자와 응용 프로그램에는 별도 계정을 tooauthenticate를 사용 해야 합니다. 이렇게 toousers 및 응용 프로그램에 부여 하는 hello 사용 권한을 제한 하 고 악의적인 활동의 hello 위험을 줄일 수 있습니다.
-   구현 데이터베이스 수준 보안 (예: db_datareader, db_datawriter) 고정된 데이터베이스 역할 또는 있습니다를 사용 하 여 응용 프로그램 toogrant에 대 한 사용자 지정 역할 명시적 사용 권한을 tooselected 데이터베이스 개체를 만들 수 있습니다.

다른 방법으로 tooencrypt 데이터를 고려해 보십시오.

-   [셀 수준 암호화](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt 특정 열 또는 다른 암호화 키를 사용 하 여 데이터의 셀도 합니다.
-   상시 암호화를 사용 하 여 사용 중인 암호화: [항상 암호화](https://msdn.microsoft.com/library/mt163865.aspx) 클라이언트 tooencrypt 중요 한 데이터 클라이언트 응용 프로그램 내부 및 하지 hello 암호화 키 toohello 데이터베이스 엔진 (SQL 데이터베이스 또는 SQL Server)를 표시할 수 있습니다. 결과적으로, 사용자에 게 소유 하는 hello 데이터 (및 대시보드를 볼 수)을 분리 상시 암호화는 고객과 구매할 hello 데이터 관리 (하지만 액세스 권한이 없어야).
-   행 수준 보안을 사용 하 여: 행 수준 보안을 사용 하면 쿼리 (예:: 그룹 멤버십 또는 실행 컨텍스트)를 실행 하는 hello 사용자의 hello 특성에 따라 데이터베이스 테이블에서 고객 toocontrol 액세스 toorows 합니다. 자세한 내용은 [행 수준 보안](https://msdn.microsoft.com/library/dn765131)을 참조하세요.

## <a name="protect-data-in-transit"></a>전송 중인 데이터 보호
전송 중인 데이터 보호는 데이터 보호 전략에서 절대 빠질 수 없는 핵심입니다. 데이터는 여러 위치에서 앞뒤로 이동 됩니다, hello 일반적인 권장 사항은 이므로 다른 위치에서 SSL/TLS 프로토콜 tooexchange 데이터 항상 사용. 일부 경우에 온-프레미스와 클라우드 간의 tooisolate hello 전체 통신 채널을 사용할 수 있습니다 가상 사설망 (VPN)을 사용 하 여 인프라입니다.

온-프레미스 인프라와 Azure 사이를 이동하는 데이터의 경우 HTTPS 또는 VPN처럼 적절한 안전 장치를 고려해야 합니다.

여러 워크스테이션 온-프레미스 tooAzure에서 toosecure 액세스 해야 하는 조직에서 사용 하 여 [Azure 사이트 간 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create)합니다.

사용 하는 것이 좋습니다, toosecure 필요한 조직을 위해 액세스 있는 개별 워크스테이션에서 온-프레미스 또는 오프-프레미스 tooAzure [지점 및 사이트 간 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create)합니다.

대용량 데이터 집합은 [Express 경로](https://azure.microsoft.com/services/expressroute/) 같은 전용 고속 WAN 링크를 통해 이동할 수 있습니다. 또한 사용 하 여 hello 응용 프로그램 수준에서 hello 데이터를 암호화할 수 toouse express 경로 선택 하면 [SSL/TLS](https://support.microsoft.com/kb/257591) 또는 추가적인된 보호를 위해 다른 프로토콜입니다.

Hello Azure 포털을 통해 Azure 저장소와 상호 작용 하는, 하는 경우 HTTPS를 통해 모든 트랜잭션이 발생 합니다. [저장소 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx) HTTPS를 통해 수도 있습니다를 사용 하는 toointeract [Azure 저장소](https://azure.microsoft.com/services/storage/) 및 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/)합니다.

Tooprotect 데이터 전송 중에 실패 하는 조직에 보다 민감한는 [중간자 개입 공격](https://technet.microsoft.com/library/gg195821.aspx), [도청](https://technet.microsoft.com/library/gg195641.aspx) 및 세션 하이재킹입니다. 이러한 공격은 tooconfidential 데이터에 액세스 하지 못하도록 hello 첫 번째 단계 수 있습니다.

hello 문서를 참조 하 여 Azure VPN 옵션에 대 한 자세한 toolearn [계획 및 디자인 VPN 게이트웨이에 대 한](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design)합니다.

## <a name="enable-database-auditing"></a>데이터베이스 감사 사용
SQL Server 데이터베이스 엔진 hello 또는 개별 데이터베이스 인스턴스의 감사 추적 및 로깅 이벤트가 hello 데이터베이스 엔진에서 발생 하는 작업이 포함 됩니다. SQL Server 감사를 사용하면 서버 수준 이벤트에 대한 서버 감사 사양과 데이터베이스 수준 이벤트에 대한 데이터베이스 감사 사양을 포함할 수 있는 서버 감사를 만들 수 있습니다. Toohello 이벤트 로그 또는 tooaudit 파일에 감사 된 이벤트를 작성할 수 있습니다.

설치에 대한 정부 또는 표준 요구 사항에 따라 SQL Server에 대한 여러 수준의 감사가 있습니다. SQL Server Audit hello 도구와 다양 한 서버 및 데이터베이스 개체에 tooenable, 저장소 및 보기 감사가 있어야 하는 프로세스를 제공 합니다.

[Azure SQL 데이터베이스 감사](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) 데이터베이스 이벤트를 추적 하 고 Azure 저장소 계정에 tooan 감사 로그를 기록 합니다.

감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.

감사 및 준수 toocompliance 표준을 용이 하 게 있지만 규정 준수를 보장 하지 않습니다.

데이터베이스 감사에 대 한 자세한 toolearn 어떻게 tooenable, 문서를 참조 하세요 hello 및 [Azure 보안 센터의 SQL server에 감사 및 위협 검색을 설정할](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers)합니다.

## <a name="enable-database-threat-detection"></a>데이터베이스 위협 검색 사용
SQL 위협 요소 탐지 toodetect 있으며 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답 합니다. 의심스러운 데이터베이스 활동, 잠재적 취약성 및 SQL 삽입 공격뿐만 아니라 비정상적인 데이터베이스 액세스 패턴에 대한 경고도 받을 수 있습니다. SQL 위협 요소 탐지 경고의 의심 스러운 활동 세부 정보를 제공 및 방법에 대 한 작업을 권장 tooinvestigate hello 위협을 완화 합니다.

예를 들어 SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다. 공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 응용 프로그램 입력 필드에 졌는 지 또는 hello 데이터베이스에서 데이터를 수정 합니다.

방법에 대 한 toolearn hello Azure 포털 참조에서에서 데이터베이스에 대 한 위협 요소 탐지를 tooset [SQL 데이터베이스 위협 검색](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)합니다.

또한 SQL 위협 검색에서는 경고를 [Azure Security Center](https://azure.microsoft.com/services/security-center/)와 통합합니다. Tootry 초대 아웃에 대 한 일 동안 무료로 합니다.

데이터베이스 위협 검색에 대 한 자세한 toolearn 어떻게 tooenable, 문서를 참조 하세요 hello 및 [Azure 보안 센터의 SQL server에 감사 및 위협 검색을 설정할](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers)합니다.

## <a name="conclusion"></a>결론
Azure 데이터베이스는 다양한 조직 및 규정 준수 요구 사항을 충족하는 모든 보안 기능을 갖춘 강력한 데이터베이스 플랫폼입니다. Hello 물리적 tooyour 데이터에 액세스를 제어 하 고 hello 파일, 열 또는 투명 한 데이터 암호화, 셀 수준 암호화 또는 행 수준 보안으로 행 수준에서 데이터 보안에 대 한 다양 한 옵션을 사용 하 여 데이터를 보호할 수 있습니다. 항상 암호화 해줍니다 암호화 된 데이터에 대 한 작업을 hello 프로세스 응용 프로그램 업데이트를 단순화 합니다. 차례로 SQL 데이터베이스 작업의 액세스 tooauditing 로그 tooknow 데이터 액세스 방법 및 시기를 허용 해야 하는 hello 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계
- 방화벽 규칙에 대해 자세히 toolearn 참조 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)합니다.
- 사용자와 로그인을 하는 방법에 대 한 toolearn 참조 [로그인 관리](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)합니다.
- 자습서는 [Azure SQL Database 보안](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial)을 참조하세요.
