---
title: "SQL 데이터베이스 보안 개요 aaaAzure | Microsoft Docs"
description: "Tooauthentication, 권한 부여, 연결 보안, 암호화 및 규정 준수 상태가 되 면 hello 클라우드 및 온-프레미스 SQL 서버 hello 차이점을 비롯 한 Azure SQL 데이터베이스 및 SQL Server 보안에 알아봅니다."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>SQL 데이터베이스 보안 설정

이 문서는 Azure SQL 데이터베이스를 사용 하 여 응용 프로그램의 hello 데이터 계층을 보안 설정의 hello 기초 안내 합니다. 특히 이 문서에서는 데이터 보호, 액세스 제어 및 사전 모니터링을 위한 리소스로 시작합니다. 

SQL의 모든 버전에서 사용할 수 있는 보안 기능의 전체 개요를 참조 hello [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대 한 보안 센터](https://msdn.microsoft.com/library/bb510589)합니다. 자세한 내용은 hello 제공 됩니다. [보안 및 Azure SQL 데이터베이스 기술 백서](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>데이터 보호
SQL Database는 이동 중인 데이터의 경우 [전송 계층 보안](https://support.microsoft.com/kb/3135244), 미사용 데이터의 경우 [투명한 데이터 암호화](http://go.microsoft.com/fwlink/?LinkId=526242) 및 사용 중인 데이터의 경우 [상시 암호화](https://msdn.microsoft.com/library/mt163865.aspx)를 제공하여 데이터를 보호합니다. 

> [!IMPORTANT]
>모든 연결 tooAzure SQL 데이터베이스 암호화 필요 (SSL/TLS)에서 모든 시간 데이터는 전송 중""에 tooand hello 데이터베이스에서. 응용 프로그램의 연결 문자열에 매개 변수 tooencrypt hello 연결을 지정 해야 하 고 *하지* tootrust hello 서버 인증서 (이렇게 하면의 연결 문자열을 복사 하는 경우 hello Azure 클래식 포털에 대 한), 그렇지 않으면 hello 연결 hello hello 서버의 id를 확인 하지 않습니다 고 취약 너무 "man-에-가로채기" 공격 됩니다. 이러한 연결 문자열 매개 변수는 예를 들어 hello ADO.NET 드라이버에 대 한 **Encrypt = True** 및 **TrustServerCertificate = False**합니다. 

다른 방법으로 tooencrypt 데이터를 고려해 보십시오.

* [셀 수준 암호화](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt 특정 열 또는 다른 암호화 키를 사용 하 여 데이터의 셀도 합니다.
* 하드웨어 보안 모듈 또는 암호화 키 계층의 중앙 관리가 필요한 경우 [Azure VM에서 SQL Server와 함께 Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)를 사용하는 것을 고려해 보세요.

## <a name="control-access"></a>액세스 제어
SQL 데이터베이스에서 방화벽 규칙, id 및 권한 부여 toodata 역할 기반 구성원 자격 및 권한을 통해 통해서도 사용자 tooprove 하도록 하는 인증 메커니즘을 사용 하 여 액세스 tooyour 데이터베이스를 제한 하 여 데이터를 보호 행 수준 보안 및 동적 데이터 마스킹입니다. SQL 데이터베이스에 대 한 액세스 제어 기능을 사용 하 여 hello의 논의 알려면 [액세스 제어](sql-database-control-access.md)합니다.

> [!IMPORTANT]
> Azure에서 데이터베이스와 논리 서버를 관리할 경우 포털 사용자 계정의 역할 할당으로 제어합니다. 이 항목에 대한 자세한 내용은 [Azure 포털의 역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)를 참조하세요.
>

### <a name="firewall-and-firewall-rules"></a>방화벽 및 방화벽 규칙
toohelp 데이터 보호, 방화벽은 모든 액세스 tooyour 데이터베이스 서버를 사용 하 여 권한을 갖는 컴퓨터를 지정할 때까지 차단 [방화벽 규칙](sql-database-firewall-configure.md)합니다. hello 방화벽 액세스 toodatabases hello 시작 IP 주소를 각 요청에 따라 권한을 부여 합니다.

### <a name="authentication"></a>인증
SQL 데이터베이스 인증 참조 toohow toohello 데이터베이스를 연결할 때 사용자의 신원을 증명 합니다. SQL 데이터베이스는 두 가지 인증 유형을 지원합니다.

* **SQL 인증**은 사용자 이름과 암호를 사용합니다. 데이터베이스에 대 한 hello 논리 서버를 만들 때 "서버 관리자" 로그인 사용자 이름 및 암호를 지정 했습니다. 이러한 자격 증명을 사용 하 여 tooany 데이터베이스 hello 데이터베이스 소유자 또는 "dbo"로 해당 서버에 인증할 수 있습니다. 
* **Azure Active Directory 인증**은 Azure Active Directory에서 관리하는 ID를 사용하고 관리되고 통합된 도메인을 지원합니다. [가능한 경우](https://msdn.microsoft.com/library/ms144284.aspx) Active Directory 인증(통합 보안)을 사용합니다. Toouse Azure Active Directory 인증을 사용 하도록 하려는 경우 hello tooadminister Azure AD 사용자 및 그룹은 허용 "Azure AD 관리"를 호출 하는 다른 서버 관리자를 만들어야 합니다. 이 관리자는 일반 서버 관리자가 할 수 있는 모든 작업을 수행할 수도 있습니다. 참조 [데이터베이스를 사용 하 여 Azure Active Directory 인증 여 tooSQL 연결](sql-database-aad-authentication.md) 방법의 연습은 toocreate Azure AD 관리자 tooenable Azure Active Directory 인증 합니다.

### <a name="authorization"></a>권한 부여
권한 부여는 사용자는 Azure SQL 데이터베이스 내에서 수행할 수 있는 toowhat 있으며이 사용자 계정의 데이터베이스 역할 멤버 자격에 의해 제어 되 고 개체 수준 사용 권한. 모범 사례로, 사용자가 hello를 필요한 최소한의 권한만 부여 해야 합니다. hello 서버 관리자 계정으로 연결 하는 hello 데이터베이스 내의 모든 기관 toodo가 db_owner의 멤버인 합니다. 스키마 업그레이드 및 기타 관리 작업을 배포하기 위해서는 이 계정을 저장합니다. Hello로 응용 프로그램 toohello 데이터베이스에서 좀 더 제한적된 사용 권한 tooconnect hello "ApplicationUser" 계정을 사용 응용 프로그램에 필요한 최소 권한입니다.

### <a name="row-level-security"></a>행 수준 보안
행 수준 보안 (예:: 그룹 멤버십 또는 실행 컨텍스트) 쿼리를 실행 하는 hello 사용자의 hello 특성에 따라 데이터베이스 테이블에서 고객 toocontrol 액세스 toorows를 수 있습니다. 자세한 내용은 [행 수준 보안](https://msdn.microsoft.com/library/dn765131)을 참조하세요.

### <a name="data-masking"></a>데이터 마스킹 
SQL 데이터베이스 동적 데이터 마스킹 toonon 권한이 사용자에 게 마스킹하 여 중요 한 데이터 노출을 제한 합니다. 동적 데이터 마스킹 자동으로 Azure SQL 데이터베이스에서 잠재적으로 중요 한 데이터를 검색 하 고 hello 응용 프로그램 계층에 미치는 영향을 최소화 하면서 권장 toomask 이러한 필드를 제공 합니다. Hello 데이터베이스의 hello 데이터는 변경 되지 않으면 지정 된 데이터베이스 필드를 통해 hello hello 쿼리 결과 집합에서 중요 한 데이터를 난독 처리 하 여 작동 합니다. 자세한 내용은 참조 [SQL 데이터베이스 동적 데이터 마스킹 시작](sql-database-dynamic-data-masking-get-started.md) 중요 한 데이터의 사용된 toolimit 노출 될 수 있습니다.

## <a name="proactive-monitoring"></a>사전 모니터링
SQL Database는 감사 및 위협 검색 기능을 제공하여 데이터를 보호합니다. 

### <a name="auditing"></a>감사
SQL 데이터베이스 감사 데이터베이스 작업을 추적 하 고 Azure 저장소 계정에 데이터베이스 이벤트 tooan 감사 로그를 기록 하 여 toomaintain 규정 준수를 지원 합니다. 감사 toounderstand 진행 중인 데이터베이스 활동을 사용 하면 분석 및으로 이전 활동 tooidentify 잠재적 위협 또는 의심 되는 남용 및 보안 위반을 조사 합니다. 자세한 내용은 [SQL Database 감사 시작](sql-database-auditing.md)을 참조하세요.  

### <a name="threat-detection"></a>위협 감지
위협 요소 탐지 한 잠재적으로 위험한 시도 tooaccess 또는 악용 데이터베이스를 검색 하는 hello Azure SQL 데이터베이스 서비스에 기본 제공 보안 인텔리전스 추가 계층을 제공 하 여 감사를 보완 합니다. 의심스러운 활동, 잠재적 취약성 및 SQL 삽입 공격은 물론 비정상적인 데이터베이스 액세스 패턴에 대해 경고합니다. 위협 요소 탐지 경고에서 확인할 수 있습니다 [Azure 보안 센터](https://azure.microsoft.com/services/security-center/) 의심 스러운 활동의 세부 정보를 제공 하 고는 방법에 대 한 작업을 권장 tooinvestigate hello 위협을 완화 하 고 있습니다. 위협 감지 비용은 $15/서버/월입니다. 됩니다 hello에 대 한 사용 가능한 첫 번째 60 일입니다. 자세한 내용은 [SQL 데이터베이스 위협 감지 시작](sql-database-threat-detection.md)을 참조하세요.
 
### <a name="data-masking"></a>데이터 마스킹 
SQL 데이터베이스 동적 데이터 마스킹 toonon 권한이 사용자에 게 마스킹하 여 중요 한 데이터 노출을 제한 합니다. 동적 데이터 마스킹 자동으로 Azure SQL 데이터베이스에서 잠재적으로 중요 한 데이터를 검색 하 고 hello 응용 프로그램 계층에 미치는 영향을 최소화 하면서 권장 toomask 이러한 필드를 제공 합니다. Hello 데이터베이스의 hello 데이터는 변경 되지 않으면 지정 된 데이터베이스 필드를 통해 hello hello 쿼리 결과 집합에서 중요 한 데이터를 난독 처리 하 여 작동 합니다. 자세한 내용은 [Azure SQL Database 동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started.md) 시작을 참조하세요.
 
## <a name="compliance"></a>규정 준수
또한 다양 한 보안 요구 사항, Azure SQL 데이터베이스도 충족 하는 응용 프로그램 수 있는 특성과 기능 위에 toohello 정기적 감사에 참가 하 고 규정 준수 표준의 수와 인증 합니다. 자세한 내용은 참조 hello [Microsoft Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)여기서 hello의 최신 목록을 찾을 수 있습니다 [SQL 데이터베이스 규정 준수 인증](https://azure.microsoft.com/support/trust-center/services/)합니다.

## <a name="next-steps"></a>다음 단계

- SQL 데이터베이스에 대 한 액세스 제어 기능을 사용 하 여 hello의 논의 알려면 [액세스 제어](sql-database-control-access.md)합니다.
- 데이터베이스 감사 내용은 [SQL Database 감사](sql-database-auditing.md)를 참조하세요.
- 위협 요소 탐지 내용은 [SQL Database 위협 요소 탐지](sql-database-threat-detection.md)를 참조하세요.
