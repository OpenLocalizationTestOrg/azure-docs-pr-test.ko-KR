---
title: "Azure에서 PaaS 데이터베이스 aaaSecuring | Microsoft Docs"
description: " PaaS 웹 및 모바일 응용 프로그램 보안을 위한 Azure SQL Database 및 SQL Data Warehouse 보안 모범 사례에 대해 자세히 알아봅니다. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Azure에서 PaaS 데이터베이스 보안 유지

이 문서에서는 PaaS 웹 및 모바일 응용 프로그램 보안을 위한 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) 및 [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) 보안 모범 사례에 대해 설명합니다. 이들 모범 사례는 Azure에 대 한 경험 및 고객의 hello 경험을와 같은 직접 합니다.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Azure SQL Database 및 SQL Data Warehouse
[Azure SQL Database](../sql-database/sql-database-technical-overview.md) 및 [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)는 인터넷 기반 응용 프로그램에 관계형 데이터베이스 서비스를 제공합니다. PaaS 배포에서 Azure SQL Database 및 SQL Data Warehouse를 사용할 때 응용 프로그램과 데이터를 보호하는 데 도움이 되는 서비스를 살펴보겠습니다.

- Azure Active Directory 인증(SQL Server 인증 대신)
- Azure SQL 방화벽
- TDE(투명한 데이터 암호화)

## <a name="best-practices"></a>모범 사례

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>중앙 집중식 ID 리포지토리를 사용하여 인증 및 권한 부여

Azure SQL 데이터베이스에 구성 된 toouse 인증의 두 가지 유형 중 하나일 수 있습니다.

- **SQL 인증**은 사용자 이름과 암호를 사용합니다. 데이터베이스에 대 한 hello 논리 서버를 만들 때 "서버 관리자" 로그인 사용자 이름 및 암호를 지정 했습니다. 이러한 자격 증명을 사용 하 여 해당 서버의 tooany 데이터베이스 hello 데이터베이스 소유자에 인증할 수 있습니다.

- **Azure Active Directory 인증**은 Azure Active Directory에서 관리하는 ID를 사용하며, 관리되는 도메인과 통합된 도메인에서 지원됩니다. Azure Active Directory 인증 toouse hello tooadminister Azure AD 사용자 및 그룹은 허용 "Azure AD 관리"를 호출 하는 다른 서버 관리자를 만들어야 합니다. 이 관리자는 일반 서버 관리자가 할 수 있는 모든 작업을 수행할 수도 있습니다.

[Azure Active Directory 인증](../active-directory/develop/active-directory-authentication-scenarios.md) 에 Azure AD (Active Directory) id를 사용 하 여 tooAzure SQL 데이터베이스 및 SQL 데이터 웨어하우스에 연결 하는 메커니즘입니다. Azure AD 사용자 id의 hello 급증을 중지 하려면 데이터베이스 서버에 대해 대체 tooSQL 서버 인증을 제공 합니다. Azure AD 인증 사용 하면 toocentrally 데이터베이스 사용자와 하나의 중앙 위치에서 다른 Microsoft 서비스의 hello id를 관리 합니다. ID 관리를 중앙 toomanage 데이터베이스 사용자를 한 위치를 제공 하 고 사용 권한 관리를 간소화 합니다.  

SQL 인증 대신 Azure AD 인증을 사용하는 이점은 다음과 같습니다.

- 한 곳에서 암호를 회전할 수 있습니다.
- 외부 Azure AD 그룹을 사용하여 데이터베이스 권한을 관리합니다.
- Azure AD에서 지원하는 통합 Windows 인증 및 다른 인증 유형을 사용하여 저장 중인 암호를 제거합니다.
- 사용 하 여 hello 데이터베이스 수준에서 데이터베이스 사용자 tooauthenticate id를 포함 합니다.
- TooSQL 데이터베이스 연결 응용 프로그램에 대 한 토큰 기반 인증을 지원 합니다.
- 도메인 동기화 없이 로컬 Azure AD에 대해 ADFS(도메인 페더레이션) 또는 기본 사용자/암호 인증을 지원합니다.
- Azure AD는 [MFA(Multi-Factor Authentication)](../multi-factor-authentication/multi-factor-authentication.md)를 포함하는 Active Directory 유니버설 인증을 사용하는 SQL Server Management Studio를 통해 연결하도록 지원합니다. MFA는 전화 통화, 문자 메시지, 모바일 앱 알림 등의 여러 가지 간편한 검증 옵션을 제공하는 강력한 인증을 포함합니다. 자세한 내용은 [SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 Azure AD MFA에 대한 SSMS 지원](../sql-database/sql-database-ssms-mfa-authentication.md)을 참조하세요.

Azure AD 인증에 대해 자세히 toolearn 참조:

- [TooSQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여 연결](../sql-database/sql-database-aad-authentication.md)
- [인증 tooAzure SQL 데이터 웨어하우스](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Azure AD 인증을 사용하는 Azure SQL DB에 대한 토큰 기반 인증 지원](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)(영문)

> [!NOTE]
> Azure Active Directory에 사용자 환경에 가장 잘 맞는 tooensure 참조 [Azure AD 기능 및 제한 사항](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), 특히 hello 추가로 고려해 야 합니다.
>
>

### <a name="restrict-access-based-on-ip-address"></a>IP 주소 기반 액세스 제한
허용 가능한 IP 주소의 범위를 지정하는 방화벽 규칙을 만들 수 있습니다. Hello 서버와 데이터베이스 수준에서 이러한 규칙을 지정할 수 있습니다. 데이터베이스 수준 방화벽 규칙을 사용 하는 것이 좋습니다 때마다 가능한 tooenhance 보안과 toomake 데이터베이스 이식성이 향상 됩니다. 하지만 같은 액세스 요구 사항을 toospend 시간 각 데이터베이스를 개별적으로 구성를 사용 하지 hello가 많은 데이터베이스가 있는 경우을 서버 수준 방화벽 규칙은 관리자가 가장 적합 합니다.

SQL Database의 기본 원본 IP 주소를 제한하면 Azure 주소(다른 구독 및 테넌트 포함)에서 액세스할 수 있습니다. 이 tooonly 제한할 수 있습니다 IP 주소 tooaccess hello 인스턴스를 허용 합니다. SQL 방화벽과 IP 주소 제한이 있더라도 강력한 인증이 여전히 필요합니다. 이 문서의 앞부분에서 만든 hello 권장을 참조 하십시오.

Azure SQL 방화벽 및 IP 제한 사항에 대해 자세히 toolearn 참조:

- [Azure SQL Database 액세스 제어](../sql-database/sql-database-control-access.md)
- [Azure SQL Database 방화벽 규칙 구성 - 개요](../sql-database/sql-database-firewall-configure.md)
- [Hello Azure 포털을 사용 하 여 Azure SQL 데이터베이스 서버 수준 방화벽 규칙을 구성](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>미사용 데이터 암호화
[TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/azure/bb934049)는 기본적으로 사용되도록 설정됩니다. TDE는 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse 데이터 및 로그 파일을 암호화합니다. TDE는 toohello 파일에 직접 액세스 하거나 자신의 백업 손상 으로부터 보호합니다. 이렇게 하면 저장 된 상태의 데이터 tooencrypt 기존 응용 프로그램을 변경 하지 않고 있습니다. TDE 항상 상태를 유지 해야 사용할 수 있습니다. 그러나 hello 일반 액세스 경로 사용 하는 공격자가 중지 되지 않습니다. TDE는 hello 기능 toocomply 된 법, 규정 및 다양 한 업계에서 확립 된 지침을 제공 합니다.

Azure SQL은 TDE와 관련된 주요 문제를 관리합니다. TDE와 온-프레미스에서 특별 한 주의 해야 tooensure 복구 기능 하 고 데이터베이스를 이동할 경우 합니다. 더 복잡 한 시나리오 hello 키 명시적으로 관리 Azure 키 자격 증명 모음의 확장 가능 키 관리를 통해 (참조 [SQL Server를 사용 하 여 EKM에서 TDE를 사용 하도록 설정](/security/encryption/enable-tde-on-sql-server-using-ekm)). 이 경우 Azure Key Vault를 통한 BYOK(Bring Your Own Key)도 허용됩니다.

Azure SQL은 [Always Encrypted](/sql/relational-databases/security/encryption/always-encrypted-database-engine)를 통해 열에 대한 암호화를 제공합니다. 이렇게 하면 승인 된 응용 프로그램만 액세스 toosensitive 열. 이러한 종류의 암호화를 사용 하 여 암호화 된 열 tooequality 기반 값에 대 한 SQL 쿼리를 제한 합니다.

선택적 데이터에는 응용 프로그램 수준 암호화도 사용해야 합니다. 경우에 따라 올바른 국가 hello에 유지 되는 키로 데이터를 암호화 하 여 데이터 sovereignty 문제를 완화할 수 있습니다. 이렇게 하면도 실수로 인 한 데이터 전송을 (예: AES 256) 강력한 알고리즘을 가정 하는 hello 키가 없는 데이터를 사용 불가능 한 toodecrypt hello에 있기 때문에 문제를 발생 시킨에서 않습니다.

보안 시스템 디자인, 중요 한 자산 암호화 및 데이터베이스 서버 hello 한 방화벽 구축과 같은 예방 조치를 추가로 toohelp 보안 hello 데이터베이스를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 SQL 데이터베이스 및 SQL 데이터 웨어하우스 PaaS 웹 및 모바일 응용 프로그램 보안에 대 한 보안 모범 사례의 한 있습니다 tooa 컬렉션을 도입 되었습니다. PaaS 배포의 경우 보안에 대 한 더 toolearn 참조:

- [PaaS 배포 보안](security-paas-deployments.md)
- [Azure App Services를 사용하여 PaaS 웹 및 모바일 응용 프로그램 보안](security-paas-applications-using-app-services.md)
