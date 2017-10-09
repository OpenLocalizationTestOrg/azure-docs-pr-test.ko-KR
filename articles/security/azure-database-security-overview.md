---
title: "aaaAzure 데이터베이스 보안 개요 | Microsoft Docs"
description: "이 문서에서는 hello Azure 데이터베이스 보안 기능의 개요를 제공 합니다."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Azure 데이터베이스 보안 개요

보안은 데이터베이스 관리에서 가장 중요하며 항상 Azure SQL Database의 최우선 순위였습니다. Azure SQL Database는 방화벽 규칙과 연결 암호화를 통해 연결 보안을 지원합니다. 사용자 이름과 암호를 사용한 인증과, Azure Active Directory에서 관리하는 Azure Active Directory Authentication을 지원합니다. 권한 부여는 역할 기반 액세스 제어를 사용합니다.

Azure SQL 데이터베이스 변경 내용을 toohello 응용 프로그램 필요 없이 실시간 암호화 및 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에 대 한 암호 해독을 수행 하 여 암호화를 지원 합니다.

Microsoft는 추가 방법을 알아볼 tooencrypt 엔터프라이즈 데이터를 제공합니다.

-   셀 수준 암호화 tooencrypt 특정 열 또는 셀의 데이터도 다른 암호화 키를 사용 합니다.
-   하드웨어 보안 모듈 또는 암호화 키 계층의 중앙 관리가 필요한 경우 Azure VM에서 SQL Server와 함께 Azure Key Vault 사용을 고려합니다.
-   항상 암호화 (현재 미리 보기)에 암호화 투명 tooapplications 만들고 SQL 데이터베이스를 사용한 hello 암호화 키를 공유 하지 않고 클라이언트가 클라이언트 응용 프로그램 내 tooencrypt 중요 한 데이터를 허용 합니다.

Azure SQL 데이터베이스 감사 기업 toorecord 이벤트 tooan 감사 로그인을 Azure 저장소 수 있습니다. 또한 SQL 데이터베이스 감사 Microsoft Power BI toofacilitate 드릴 다운 보고서 및 분석에 통합합니다.

 SQL Azure 데이터베이스 규정 가장 밀접 하 게 보안된 toosatisfy 또는 다른 규칙 으로부터 HIPAA, 27002/ISO 27001, PCI DSS 수준 1 등의 보안 요구 사항 수 있습니다. Hello에 사용할 수 있는 보안 규정 준수 인증의 최신 목록은 [Microsoft Azure 보안 센터 사이트](http://azure.microsoft.com/support/trust-center/services/)합니다.

이 문서는 구조적, 테이블 형식 및 관계형 데이터에 대 한 Microsoft Azure SQL 데이터베이스 보안의 hello 기초 안내 합니다. 특히 이 문서에서는 데이터 보호, 액세스 제어 및 사전 모니터링을 위한 리소스로 시작합니다.

이 Azure 데이터베이스 보안 개요 문서 hello 영역을 다음에 중점을 둡니다.

-   데이터 보호
-   Access Control
-   사전 모니터링
-   중앙 집중식 보안 관리 
-   Azure 마켓플레이스

## <a name="protect-data"></a>데이터 보호

SQL Database는 이동 중인 데이터의 경우 [전송 계층 보안](https://support.microsoft.com/kb/3135244), 미사용 데이터의 경우 [투명한 데이터 암호화](http://go.microsoft.com/fwlink/?LinkId=526242) 및 사용 중인 데이터의 경우 [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)를 제공하여 데이터를 보호합니다.

이 섹션에서는 다음에 대해 설명합니다.

-   진행 중인 암호화
-   휴지 상태의 암호화
-   암호화 사용(클라이언트)

다른 방법으로 tooencrypt 데이터를 고려해 보십시오.

-   [셀 수준 암호화](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt 특정 열 또는 다른 암호화 키를 사용 하 여 데이터의 셀도 합니다.
-   하드웨어 보안 모듈 또는 암호화 키 계층의 중앙 관리가 필요한 경우 [Azure VM에서 SQL Server와 함께 Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)를 사용하는 것을 고려해 보세요.

### <a name="encryption-in-motion"></a>진행 중인 암호화

모든 클라이언트/서버 응용 프로그램에 대 한 일반적인 문제는 개인 정보 보호 hello 필요가 공용 및 개인 네트워크를 통해 데이터를 이동할 때. 네트워크를 통해 이동 하는 데이터 암호화 되지 않은 경우 수 수 캡처된를 권한이 없는 사용자가 도난 hello 가능성이 높습니다. 데이터베이스 서비스를 처리할 때 toomake 있는지 그리고 데이터베이스 서버 간에 통신 하는 통신과 중간 계층 응용 프로그램을 hello 데이터베이스 클라이언트와 서버 간에 데이터를 암호화 해야 합니다.

네트워크를 관리할 때의 한 가지 문제는 신뢰할 수 없는 네트워크를 통해 응용 프로그램 간에 전송되는 데이터를 보호하는 것입니다. 사용할 수 있습니다 [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate 서버와 클라이언트 hello 인증 된 당사자 간에 메시지 tooencrypt 사용 합니다.

Hello 인증 프로세스에서 TLS/SSL 클라이언트 메시지 tooa TLS/SSL 서버에 보내고 hello 서버 hello 서버 자체 tooauthenticate 필요한 hello 정보로 응답 합니다. hello 클라이언트와 서버 세션 키 교환을 추가로 수행 하 고 인증 대화 종료 hello 합니다. 인증이 완료 되 면 hello 서버와 hello 인증 프로세스 중에 설정 된 hello 대칭 암호화 키를 사용 하 여 hello 클라이언트 간에 SSL 보안 통신 시작 될 수 있습니다.

모든 연결 tooAzure SQL 데이터베이스 암호화 필요 (SSL/TLS)에서 모든 시간 데이터는 전송 중""에 tooand hello 데이터베이스에서. SQL Azure는 TLS/SSL tooauthenticate 서버와 클라이언트를 사용 하 여 및 hello 인증 된 당사자 간에 메시지 tooencrypt 사용 합니다. 응용 프로그램의 연결 문자열에 매개 변수 tooencrypt hello 연결 및 인증서를 지정 하지 tootrust hello 서버 (이렇게 하면 hello Azure 클래식 포털에서 연결 문자열을 복사 하는 경우), 그렇지 않으면 연결은 hello 해야 합니다. hello 서버 hello 신원을 확인 하지 하 고 취약 너무 "man-에-가로채기" 공격 됩니다. Hello ADO.NET 드라이버, 예를 들어, 이러한 연결 문자열 매개 변수는 Encrypt = True 및 TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>휴지 상태의 암호화
보안 시스템 디자인, 중요 한 자산 암호화 및 데이터베이스 서버 hello 한 방화벽 구축과 같은 여러 가지 toohelp 보안 hello 데이터베이스 예방 조치를 취할 수 있습니다. 그러나 hello 물리적 미디어 (예: 드라이브 또는 백업 테이프)를 도난 당한 경우에서 악의적인 사용자만 복원 또는 hello 데이터베이스에 연결 하 고 수 hello 데이터를 검색 합니다.

한 가지 해결 tooencrypt hello hello 데이터베이스의 중요 한 데이터는 고 hello는 키가 인증서를 사용 하 여 사용 되는 tooencrypt hello 데이터를 보호 합니다. 이 없으면 누구도 hello 키 hello 데이터를 사용 하 여 하지만 이러한 종류의 보호를 계획 해야 합니다.

이 문제를 SQL Server 및 Azure SQL 지원 toosolve [투명 한 데이터 암호화 (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde)합니다. TDE는 SQL Server 및 Azure SQL Database 데이터 파일을 암호화합니다. 이를 미사용 데이터 암호화라고 합니다.

Azure SQL 데이터베이스 투명 한 데이터 암호화는 변경 하지 않고도 실시간 암호화 및 hello 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에 대 한 암호 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 toohello 응용 프로그램입니다.  

TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다. SQL 데이터베이스의 hello 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호 됩니다. hello 기본 제공 서버 인증서는 각 SQL 데이터베이스 서버에 대해 고유 합니다.

데이터베이스가 GeoDR 관계에 있는 경우 각 서버에서 서로 다른 키로 보호됩니다. 두 데이터베이스는 연결 된 toohello 경우 공유 같은 서버에 동일한 기본 제공 인증서 hello 합니다. Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다. TDE에 대한 일반적인 설명은 [투명한 데이터 암호화(TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde)를 참조하세요.

### <a name="encryption-in-use-client"></a>암호화 사용(클라이언트)

대부분 데이터 침해 개인 식별이 가능한 정보 또는 신용 카드 번호 등의 중요 데이터의 hello 도용 작업이 포함 됩니다. 데이터베이스는 중요 정보를 담고 있을 수 있습니다. 여기에 고객의 개인 데이터, 기밀 경쟁 정보, 지적 재산 등이 포함될 수 있습니다. 특히 고객 데이터의 손실이나 도난은 브랜드 평판 손상, 경쟁력 상실, 소송까지 초래하는 심각한 벌금을 초래할 수 있습니다.

![상시 암호화](./media/azure-databse-security-overview/azure-database-fig1.png)

[항상 암호화](https://msdn.microsoft.com/library/mt163865.aspx) 은 설계 된 기능 tooprotect 중요 한 데이터, 신용 카드 번호나 주민 등록 번호 (예를 들어 미국 사회 보장 번호)와 같은 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스에 저장 합니다. 항상 암호화 된 클라이언트 tooencrypt 중요 한 클라이언트 응용 프로그램 데이터를 허용 하 고 hello 암호화 키 toohello 데이터베이스 엔진 (SQL 데이터베이스 또는 SQL Server)를 표시 하지 않을 합니다.

암호화 된 사용자에 게 소유 하는 hello 데이터 (및 대시보드를 볼 수)을 분리를 제공 하는 항상 고객과 구매할 hello 데이터 관리 (하지만 액세스 권한이 없어야). 온-프레미스 데이터베이스 관리자가 함으로써 클라우드 데이터베이스 관리자 또는 기타 높은 권한을 있지만 인증 되지 않은 사용자가 암호화 된 hello 데이터에 액세스할 수 없습니다

또한 항상 암호화 암호화 투명 tooapplications를 만듭니다. 자동으로 암호화 및 hello 클라이언트 응용 프로그램의 중요 한 데이터를 해독할 수 있도록 hello 클라이언트 컴퓨터에 설치 된 상시 암호화 지원 드라이버입니다. hello 드라이버 hello 데이터 toohello 데이터베이스 엔진에 전달 하기 전에 hello 중요 한 열의 데이터를 암호화 하 고 hello 의미 체계 toohello 응용 프로그램 유지 되도록 쿼리를 자동으로 다시 작성 합니다. 마찬가지로, hello 드라이버는 쿼리 결과에 포함 되는 암호화 된 데이터베이스 열에 저장 된 데이터를 투명 하 게 해독 합니다.

## <a name="access-control"></a>Access Control
보안 tooprovide SQL 데이터베이스의 id 및 사용자가 toospecific 작업 및 데이터를 제한 하는 권한 부여 메커니즘 사용자 tooprove를 요구 하는 인증 메커니즘 IP 주소로 연결을 제한 하는 방화벽 규칙으로 액세스를 제어 합니다.

### <a name="database-access"></a>데이터베이스 액세스

데이터 보호 tooyour 데이터 액세스 제어로 시작 합니다. 데이터를 호스트 하는 hello 데이터 센터가 hello 네트워크 계층에서 방화벽 toomanage 보안을 구성할 수도 있지만 물리적 액세스를 관리 합니다. 또한 인증에 대한 로그인을 구성하고 서버 및 데이터베이스 역할의 권한을 정의하여 액세스를 제어할 수도 있습니다.

이 섹션에서는 다음에 대해 설명합니다.

-   방화벽 및 방화벽 규칙
-   인증
-   권한 부여

#### <a name="firewall-and-firewall-rules"></a>방화벽 및 방화벽 규칙

Microsoft Azure SQL Database는 Azure 및 기타 인터넷 기반 응용 프로그램의 관계형 데이터베이스 서비스를 제공합니다. toohelp 데이터 보호, 방화벽 권한이 있는 컴퓨터를 지정할 때까지 모든 액세스 tooyour 데이터베이스 서버를 차단 합니다. hello 방화벽 액세스 toodatabases hello 시작 IP 주소를 각 요청에 따라 권한을 부여 합니다. 자세한 내용은 [Azure SQL Database 방화벽 규칙 개요](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)를 참조하세요.

hello [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) 서비스 TCP 포트 1433 통해서만 제공 됩니다. 사용자의 컴퓨터에서 SQL 데이터베이스 tooaccess 클라이언트 컴퓨터 방화벽이 TCP 포트 1433에서 보내는 TCP 통신을 허용 하는지 확인 합니다. 다른 응용 프로그램에 필요하지 않은 경우 TCP 포트 1433의 인바운드 연결을 차단합니다.

#### <a name="authentication"></a>인증

SQL 데이터베이스 인증 참조 toohow toohello 데이터베이스를 연결할 때 사용자의 신원을 증명 합니다. SQL 데이터베이스는 두 가지 인증 유형을 지원합니다.

-   **SQL 인증:** 단일 로그인 계정이 hello 라는 SQL 데이터베이스의 구독자 계정 이름의 논리 SQL 인스턴스를 만들 때 만들어집니다. 이 계정은 [SQL Server 인증](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)(사용자 이름 및 암호)을 사용하여 연결됩니다. 이 계정은 hello 논리 서버 인스턴스 및 모든 사용자 데이터베이스에서 관리자로 toothat 인스턴스 연결입니다. hello 구독자 계정을의 hello 권한을 제한할 수 없습니다. 이러한 계정 중 하나만 존재할 수 있습니다.
-   **Azure Active Directory 인증:** [Azure Active Directory 인증](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) 장치가 Azure Active Directory (에서 id를 사용 하 여 연결 tooMicrosoft Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스 Azure AD)입니다. 이에서는 데이터베이스 사용자의 id를 관리 하는 toocentrally 있습니다.

![인증](./media/azure-databse-security-overview/azure-database-fig2.png)

 Azure Active Directory 인증에는 다음과 같은 장점이 있습니다.
  - 대체 tooSQL 서버 인증을 제공합니다.
  - 또한 데이터베이스 서버에 대해 사용자 id의 hello 급증을 막는 데도 도움이 됩니다 &를 한 위치에서 암호 교체를 허용 합니다.
  - 외부(Azure Active Directory) 그룹을 사용하여 데이터베이스 권한을 관리할 수 있습니다.
  - Windows 통합 인증 또는 Azure Active Directory에서 지원하는 기타 인증을 사용하여 암호 저장을 제거할 수 있습니다.

#### <a name="authorization"></a>권한 부여
[권한 부여](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) toowhat 참조는 사용자는 Azure SQL 데이터베이스 내에서 수행할 수 있는 사용자 계정의 데이터베이스에 의해 제어 됩니다 및 [역할 멤버 자격](https://msdn.microsoft.com/library/ms189121) 및 [개체 수준 사용 권한](https://msdn.microsoft.com/library/ms191291.aspx)합니다. 권한 부여는 이러한 리소스에 대 한 보안 주체에서 액세스할 수 있는 보안 리소스 및 작업은 사용할 수를 결정 하는 hello 프로세스입니다.

### <a name="application-access"></a>응용 프로그램 액세스

이 섹션에서는 다음에 대해 설명합니다.

-   동적 데이터 마스킹
-   행 수준 보안

#### <a name="dynamic-data-masking"></a>동적 데이터 마스킹
콜 센터 서비스 담당자는 사회 보장 번호 또는 신용 카드 번호의 여러 숫자로 발신자를 식별할 수 있지만 해당 데이터 항목 완벽 하 게 되지 않아야 toohello 서비스 담당자를 노출 합니다.

hello 제외 하 고 모두 마스킹 하도록의 마지막 4 자리 사회 보장 번호 또는 신용 카드 번호 쿼리의 hello 결과 집합의 모든 마스킹 규칙을 정의할 수 있습니다.

![동적 데이터 마스킹](./media/azure-databse-security-overview/azure-database-fig3.png)

또 다른 예로, 개발자는 적합성 규정 준수 규칙을 위반 하지 않고 문제 해결을 위해 프로덕션 환경을 쿼리할 수 있도록 적절 한 데이터 마스크 정의 tooprotect 개인 식별이 가능한 정보 (PII) 데이터를 수 있습니다.

[SQL 데이터베이스 동적 데이터 마스킹](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) toonon 권한이 사용자에 게 마스킹하 여 중요 한 데이터 노출을 제한 합니다. Azure SQL 데이터베이스의 V12 버전 hello에 대 한 동적 데이터 마스킹은 지원 됩니다.

[동적 데이터 마스킹](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) toodesignate를 사용 하 여 무단된 액세스 toosensitive 데이터 것을 방지할 수 어느 정도의 hello 중요 한 데이터 tooreveal hello 응용 프로그램 계층에 미치는 영향을 최소화 합니다. hello 데이터베이스의 hello 데이터는 변경 되지 않으면 지정 된 데이터베이스 필드를 통해 hello hello 쿼리 결과 집합에서 중요 한 데이터를 숨기는 정책 기반 보안 기능.


> [!Note]
> 동적 데이터 마스킹 Azure 데이터베이스 admin 님 안녕하세요, 서버 관리자 또는 보안 책임자 역할에서 구성할 수 있습니다.

#### <a name="row-level-security"></a>행 수준 보안
다중 테넌트 데이터베이스에 대한 또 다른 공통 보안 요구 사항은 [행 수준 보안](https://msdn.microsoft.com/library/dn765131.aspx)입니다. 이 기능을 통해 toocontrol 액세스 toorows 쿼리 (예:: 그룹 멤버십 또는 실행 컨텍스트)를 실행 하는 hello 사용자의 hello 특성에 따라 데이터베이스 테이블에 있습니다.

![행 수준 보안](./media/azure-databse-security-overview/azure-database-fig4.png)

hello 액세스 제한 논리는 hello 데이터베이스 계층에서 다소 떨어진 위치에서 다른 응용 프로그램 계층의 hello 데이터는 합니다. hello 데이터베이스 시스템은 모든 계층에서 데이터 액세스를 시도할 때마다 hello 액세스를 제한 합니다. 그러면 보안 시스템이 더 안정적이 고 강력한 보안 시스템의 hello 노출 영역 줄이기 합니다.

행 수준 보안에서는 조건자 기반 액세스 제어를 도입합니다. 적절 하 게 고려 메타 데이터 또는 관리자에 게 판단한 기타 기준을 사용할 수 있는 유연한, 중앙 집중적 이며, 조건자 기반 평가 제공 합니다. hello 사용자에 게 사용자 특성을 기반으로 하는 hello 적절 한 액세스 toohello 데이터 여부 hello 조건자 조건 toodetermine로 사용 됩니다. 레이블 기반 액세스 제어는 조건자 기준 액세스 제어를 사용하여 구현할 수 있습니다.

## <a name="proactive-monitoring"></a>사전 모니터링
SQL Database는 **감사** 및 **위협 검색** 기능을 제공하여 데이터를 보호합니다.

### <a name="auditing"></a>감사
SQL 데이터베이스 감사 프로그램 기능 toogain에 대 한 정보 이벤트 및 업데이트 및 hello 데이터에 대 한 쿼리를 포함 하 여 hello 데이터베이스 내에서 발생 한 변경 내용을 증가 합니다.

[Azure SQL 데이터베이스 감사](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) 데이터베이스 이벤트를 추적 하 고 Azure 저장소 계정에 tooan 감사 로그를 기록 합니다. 감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다. 감사 및 준수 toocompliance 표준을 용이 하 게 있지만 규정 준수를 보장 하지 않습니다.

SQL 데이터베이스 감사를 사용하여 다음을 수행할 수 있습니다.

-   **유지** 합니다. 감사 데이터베이스 작업 toobe의 범주를 정의할 수 있습니다.
-   **보고** 합니다. 미리 구성 된 보고서 및 활동 및 이벤트 보고 신속 하 게 시작 하는 대시보드 tooget를 사용할 수 있습니다.
-   **분석** 합니다. 의심스러운 이벤트, 특별한 활동 및 추세를 찾을 수 있습니다.

두 가지 감사 방법이 있습니다.

-   **Blob 감사** -로그가 tooAzure Blob 저장소에 기록 됩니다. 이 방법은 고성능을 제공하고, 보다 세밀한 개체 수준 감사를 지원하고, 보다 비용 효율적인 새로운 감사 방법입니다.
-   **테이블 감사** -로그가 tooAzure 테이블 저장소에 기록 됩니다.

### <a name="threat-detection"></a>위협 감지
[Azure SQL Database 위협 검색](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)은 보안 위협의 가능성이 있는 의심스러운 활동을 검색합니다. 위협 검색 하면 SQL 삽입 같은 hello 데이터베이스에서 toorespond toosuspicious 이벤트 나타나는 순서 대로 있습니다. 경고를 제공 하 고 의심 스러운 이벤트 hello Azure SQL 데이터베이스 감사 tooexplore hello 사용을 허용 합니다.

![위협 검색](./media/azure-databse-security-overview/azure-database-fig5.jpg)

예를 들어 SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다. 공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 응용 프로그램 입력 필드에 졌는 지 또는 hello 데이터베이스에서 데이터를 수정 합니다.

보안 책임자 또는 지정된 다른 관리자는 의심스러운 데이터베이스 활동이 발생하는 즉시 알림을 받을 수 있습니다. 각 알림에 hello 의심 스러운 활동의 세부 정보를 제공 하 고 toofurther 조사 하 고 hello 위협을 완화 하는 방법을 제시 합니다.        

## <a name="centralized-security-management"></a>중앙 집중식 보안 관리 

[Azure 보안 센터](https://azure.microsoft.com/documentation/services/security-center/) 하면 방지, 검색 및 toothreats 응답 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

[보안 센터](https://docs.microsoft.com/azure/security-center/security-center-sql-database) 모든 서버 및 데이터베이스의 보안을 hello에 대 한 가시성을 제공 하 여 SQL 데이터베이스의에서 데이터를 보호 하는 데 도움이 됩니다. 보안 센터를 사용하면 다음과 같은 작업을 수행할 수 있습니다.

-   SQL Database 암호화 및 감사를 위한 정책을 정의합니다.
-   모든 구독에서 SQL 데이터베이스 리소스의 보안을 hello를 모니터링 합니다.
-   보안 문제를 신속하게 파악하고 해결합니다.
-   [Azure SQL Database 위협 감지](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)에 대한 경고를 통합합니다.
-   보안 센터는 역할 기반 액세스를 지원합니다.

## <a name="azure-marketplace"></a>Azure 마켓플레이스

Azure 마켓플레이스 hello 수 있도록 해 주는 업체 독립 소프트웨어 공급 업체 (Isv) toooffer hello 전 세계 솔루션 tooAzure 고객에 게는 온라인 응용 프로그램 및 서비스 마켓플레이스입니다.
hello Azure 마켓플레이스 결합 하나의 통합 된 플랫폼 toobetter에 파트너 에코 시스템을 Microsoft Azure는 고객 및 파트너를 제공 합니다. 클릭 [여기](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance 데이터베이스 보안 제품 Azure 마켓플레이스에에서 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Azure SQL Database 보호](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial)에 대한 자세한 정보
- [Azure Security Center 및 Azure SQL Database 서비스](https://docs.microsoft.com/azure/security-center/security-center-sql-database)에 대한 자세한 정보
- 위협 검색에 대해 자세히 toolearn 참조 [SQL 데이터베이스 위협 검색](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)합니다.
- toolearn 더 참조 [개선 SQL 데이터베이스 성능](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial)합니다. 
