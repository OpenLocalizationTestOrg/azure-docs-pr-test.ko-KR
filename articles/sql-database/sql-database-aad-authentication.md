---
title: "aaaAzure Active Directory 인증-Azure SQL (개요) | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 인증을 위해 Azure Active Directory toouse"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>SQL Database 및 SQL Data Warehouse에서 인증을 위해 Azure Active Directory 인증 사용
Azure Active Directory 인증은 tooMicrosoft Azure SQL 데이터베이스를 연결 하는 메커니즘 및 [SQL 데이터 웨어하우스](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) Azure Active Directory (Azure AD)에 id를 사용 하 여 합니다. Azure AD 인증을 사용 하면 데이터베이스 사용자의 신원을 hello 및 하나의 중앙 위치에서 다른 Microsoft 서비스를 중앙에서 관리할 수 있습니다. ID 관리를 중앙 toomanage 데이터베이스 사용자를 한 위치를 제공 하 고 사용 권한 관리를 간소화 합니다. Hello 다음을 이점입니다.

* 대체 tooSQL 서버 인증을 제공합니다.
* 사용 하면 데이터베이스 서버에 대해 hello 확산 됨에 따라 사용자 id를 중지합니다.
* 한 위치에서의 암호 회전이 가능합니다.
* 고객이 외부(AAD) 그룹을 사용하여 데이터베이스 사용 권한을 관리할 수 있습니다.
* Windows 통합 인증 또는 Azure Active Directory에서 지원하는 기타 인증을 사용하여 암호 저장을 제거할 수 있습니다.
* Azure AD 인증 hello 데이터베이스 수준에서 포함 된 데이터베이스 사용자 tooauthenticate id를 사용합니다.
* Azure AD 연결 tooSQL 데이터베이스 응용 프로그램에 대 한 토큰 기반 인증을 지원 합니다.
* Azure AD 인증은 도메인 동기화 없이 로컬 Azure Active Directory에 대해 ADFS(도메인 페더레이션) 또는 기본 사용자/암호 인증을 지원합니다.  
* Azure AD는 MFA(Multi-Factor Authentication)를 포함하는 Active Directory 유니버설 인증을 사용하는 SQL Server Management Studio를 통해 연결하도록 지원합니다.  MFA는 전화 통화, 문자 메시지, 모바일 앱 알림 등의 여러 가지 간편한 검증 옵션을 제공하는 강력한 인증을 포함합니다. 자세한 내용은 [SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 Azure AD MFA에 대한 SSMS 지원](sql-database-ssms-mfa-authentication.md)을 참조하세요.  

>  [!NOTE]  
>  Azure VM에서 실행 중인 서버에 Azure Active Directory 계정을 사용 하 여 지원 되지 않습니다 tooSQL를 연결 합니다. 대신 도메인 Active Directory 계정을 사용합니다.  

hello 구성 단계 hello 프로시저 tooconfigure 다음을 포함 하 고 Azure Active Directory 인증을 사용 합니다.

1. Azure AD를 만들고 채웁니다.
2. 옵션: 연결 하거나 현재 Azure 구독과 연결 되어 있는 hello active directory 변경 합니다.
3. Azure SQL Server 또는 [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/)에 대한 Azure Active Directory 관리자를 만듭니다.
4. 클라이언트 컴퓨터를 구성합니다.
5. AD id에 매핑된 데이터베이스 tooAzure 포함 된 데이터베이스 사용자를 만듭니다.
6. Azure AD id를 사용 하 여 tooyour 데이터베이스를 연결 합니다.

> [!NOTE]
> toolearn 어떻게 toocreate 및 Azure AD를 채우는 및 Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스를 Azure AD를 구성 하 고, 참조 [Azure AD와 Azure SQL 데이터베이스 구성](sql-database-aad-authentication-configure.md)합니다.
>

## <a name="trust-architecture"></a>트러스트 아키텍처
hello 대략적인 다이어그램을 다음에 Azure AD 인증을 사용 하 여 Azure SQL 데이터베이스의 hello 솔루션 아키텍처 요약 되어 있습니다. hello 같은 개념이 적용 tooSQL 데이터 웨어하우스 합니다. Azure AD 기본 사용자 암호를 Azure AD/Azure SQL 데이터베이스 및 hello 클라우드 부분 toosupport 간주 됩니다. toosupport 페더레이션 인증 (또는 Windows 자격 증명에 대 한 사용자/암호), ADFS 블록와 hello 통신 합니다. hello 화살표 통신 경로 나타냅니다.

![aad auth 다이어그램][1]

hello 다음 다이어그램이 나타냅니다 hello 페더레이션, 신뢰 및 호스팅 토큰을 제출 하 여 클라이언트 tooconnect tooa 데이터베이스를 허용 하는 관계입니다. hello 토큰 Azure AD를 통해 인증 되 고 hello 데이터베이스에서 신뢰할 수 있습니다. 고객 1은 기본 사용자가 있는 Azure Active Directory 또는 페더레이션된 사용자가 있는 Azure AD를 나타낼 수 있습니다. 고객 2는 가져온 사용자를 포함하는 가능한 해결 방법을 나타냅니다. 이 예에서는 Azure Active Directory와 동기화되는 ADFS로 페더레이션된 Azure Active Directory에서 가져옵니다. toounderstand Azure AD 인증을 사용 하 여 tooa 데이터베이스에 액세스 하는 구독을 호스팅 해당 hello 관련된 toohello Azure AD가 필요 합니다. hello 동일한 구독은 있어야 사용된 toocreate hello SQL Server 호스팅 hello Azure SQL 데이터베이스 또는 SQL 데이터 웨어하우스 합니다.

![구독 관계][2]

## <a name="administrator-structure"></a>관리자 구조
Azure AD 인증을 사용할 때는 두 가지 관리자 계정을 hello SQL 데이터베이스 서버에 대 한 원래 SQL Server 관리자 및 관리자에 게 Azure AD hello 합니다. hello 같은 개념이 적용 tooSQL 데이터 웨어하우스 합니다. Hello 관리자만 Azure AD 계정에 따라 사용자 데이터베이스에서 hello 첫 번째 Azure AD에 포함 된 데이터베이스 사용자를 만들 수 있습니다. Azure AD 사용자 또는 Azure AD 그룹 hello Azure AD 관리자 로그인 수 있습니다. 관리자에 게 그룹 계정을 이면 hello SQL Server 인스턴스에 대 한 여러 Azure AD 관리자를 사용 하면 모든 그룹 구성원이 사용할 수 있습니다. 관리자 관리 효율성 toocentrally를 허용 하 여 그룹 계정을 사용 하 여 추가 하 고 hello 사용자 또는 SQL 데이터베이스의 사용 권한을 변경 하지 않고 Azure AD에서 그룹 구성원을 제거 합니다. 한 번에 하나의 Azure AD 관리자(그룹 또는 사용자)를 구성할 수 있습니다.

![관리자 구조][3]

## <a name="permissions"></a>권한
사용자가 새 toocreate 있어야 hello `ALTER ANY USER` hello 데이터베이스에 대 한 사용 권한입니다. hello `ALTER ANY USER` 권한을 tooany 데이터베이스 사용자를 부여할 수 있습니다. hello `ALTER ANY USER` hello 서버 관리자 계정 및 hello로 데이터베이스 사용자가 권한을 보유도 `CONTROL ON DATABASE` 또는 `ALTER ON DATABASE` hello의 멤버 및 해당 데이터베이스에 대 한 사용 권한을 `db_owner` 데이터베이스 역할입니다.

toocreate SQL 데이터 웨어하우스 또는 Azure SQL 데이터베이스의 포함 된 데이터베이스 사용자를 Azure AD id를 사용 하 여 toohello 데이터베이스를 연결 해야 합니다. toocreate hello 첫 번째 포함 된 데이터베이스 사용자 (hello의 소유자 인 데이터베이스 hello) Azure AD 관리자를 사용 하 여 toohello 데이터베이스를 연결 해야 합니다. 이에 대해서는 아래 4, 5단계에서 설명합니다. 모든 Azure AD 인증은 Azure SQL 데이터베이스 또는 SQL 데이터 웨어하우스 서버에 대 한 Azure AD admin 님 안녕하세요 만들어진 경우에 있습니다. Azure Active Directory admin 님 안녕하세요 hello 서버에서 제거 되었으면, SQL Server 내부 이전에 만든 기존 Azure Active Directory 사용자가 Azure Active Directory 자격 증명을 사용 하 여 toohello 데이터베이스를 더 이상 연결할 수 없습니다.

## <a name="azure-ad-features-and-limitations"></a>Azure AD 기능 및 제한 사항
Azure AD의 멤버를 다음 hello Azure SQL server 또는 SQL 데이터 웨어하우스에서 프로 비전 할 수 있습니다.:

* 네이티브 멤버: hello 관리 되는 도메인 또는 고객 도메인에 Azure AD에서 만든 멤버입니다. 자세한 내용은 참조 [고유한 도메인 이름을 tooAzure AD 추가](../active-directory/active-directory-add-domain.md)합니다.
* 도메인 구성원 멤버: 페더레이션 도메인으로 Azure AD에 만들어진 멤버입니다. 자세한 내용은 [Microsoft Azure는 이제 Windows Server Active Directory와의 페더레이션 지원](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)을 참조하세요.
* 네이티브 또는 페더레이션 도메인 멤버인 다른 Azure AD에서 가져온 멤버입니다.
* 보안 그룹으로 만들어진 Active Directory 그룹.

Microsoft 계정(예: outlook.com, hotmail.com, live.com) 또는 다른 게스트 계정(예: gmail.com, yahoo.com)은 지원되지 않습니다. 너무에 로그인 하는 경우[https://login.live.com](https://login.live.com) Microsoft 계정을 사용 하 고 다음 hello 계정 및 암호를 사용 하 여, 지원 되지 않는 Azure SQL 데이터 웨어하우스 또는 Azure SQL 데이터베이스에 대 한 Azure AD 인증에 대 한 합니다.

## <a name="connecting-using-azure-ad-identities"></a>Azure AD ID를 사용하여 연결

Azure Active Directory 인증 hello 다음 Azure AD id를 사용 하 여 연결 tooa 데이터베이스의 메서드를 지원 합니다.

* 통합 Windows 인증 사용
* Azure AD 사용자 이름 및 암호 사용
* 응용 프로그램 토큰 인증 사용

### <a name="additional-considerations"></a>추가 고려 사항

* tooenhance 관리 효율성은 권장 되는 전용된 Azure AD를 프로 비전 관리자 권한으로 그룹화 합니다.   
* Azure SQL Server 또는 Azure SQL Data Warehouse에 대해 한 번에 하나의 Azure AD 관리자(그룹 또는 사용자)만 구성할 수 있습니다.   
* SQL Server 용 Azure AD 관리자만 toohello Azure SQL server 또는 Azure Active Directory 계정을 사용 하 여 Azure SQL 데이터 웨어하우스에 처음 연결할 수 있습니다. Active Directory 관리자에 게 다음 Azure AD를 구성할 수 데이터베이스 사용자입니다.   
* Hello 연결 제한 시간 too30 초를 설정 하는 것이 좋습니다.   
* SQL Server 2016 Management Studio 및 Visual Studio 2015용 SQL Server Data Tools(버전 14.0.60311.1 2016년 4월 이상)는 Azure Active Directory 인증을 지원합니다. (Azure AD 인증 hello에서 지원 되며 **.NET Framework Data Provider for SqlServer**; 이상 버전.NET Framework 4.6). 따라서 이러한 도구의 최신 버전을 hello 및 데이터 계층 응용 프로그램 (DAC 및.bacpac)는 Azure AD 인증을 사용할 수 있습니다.   
* [ODBC version 13.1](https://www.microsoft.com/download/details.aspx?id=53339)은 Azure Active Directory 인증을 지원하지만 `bcp.exe`는 구형 ODBC 공급자를 사용하기 때문에 Azure Active Directory 인증을 사용하여 연결할 수 없습니다.   
* `sqlcmd`13.1 hello에서 사용할 수 있는 버전으로 Azure Active Directory 인증을 시작 지원 [다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=825643)합니다.   
* SQL Server Data Tools for Visual Studio 2015 이상이 필요 hello 2016 년 4 월 버전의 hello Data Tools (버전 14.0.60311.1). 현재 Azure AD 사용자는 SSDT 개체 탐색기에 표시되지 않습니다. 이 문제를 해결에 hello 사용자 보기 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)합니다.   
* [SQL Server용 Microsoft JDBC 드라이버 6.0](https://www.microsoft.com/download/details.aspx?id=11774)은 Azure AD 인증을 지원합니다. 참고: [hello 연결 속성을 설정할](https://msdn.microsoft.com/library/ms378988.aspx)합니다.   
* PolyBase는 Azure AD 인증을 사용하여 인증할 수 없습니다.   
* Azure AD 인증 hello Azure 포털에서 SQL 데이터베이스에 대해 지원 되며 **가져오기 데이터베이스** 및 **데이터베이스 내보내기** 블레이드입니다. 가져오기 및 내보내기 Azure AD 인증을 사용 하 여 hello PowerShell 명령에서에서 지원 됩니다.   
* Azure AD 인증은 CLI를 사용하여 SQL Database 및 SQL Data Warehouse에 대해 지원됩니다. 자세한 내용은 [SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리](sql-database-aad-authentication-configure.md) 및 [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server)를 참조하세요.

## <a name="next-steps"></a>다음 단계
- toolearn 어떻게 toocreate 및 Azure AD를 채우는 및 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스를 Azure AD를 구성 하 고, 참조 [구성 및 Azure Active Directory 인증을 SQL 데이터베이스 또는 SQL 데이터 웨어하우스 관리](sql-database-aad-authentication-configure.md)합니다.
- SQL Database의 액세스 및 제어에 대한 개요는 [SQL Database 액세스 및 제어](sql-database-control-access.md)를 참조하세요.
- SQL Database의 로그인, 사용자 및 데이터베이스 역할에 대한 개요는 [로그인, 사용자 및 데이터베이스 역할](sql-database-manage-logins.md)을 참조하세요.
- 데이터베이스 보안 주체에 대한 자세한 내용은 [보안 주체](https://msdn.microsoft.com/library/ms181127.aspx)를 참조하세요.
- 데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 역할](https://msdn.microsoft.com/library/ms189121.aspx)을 참조하세요.
- SQL Database의 방화벽 규칙에 대한 자세한 내용은 [SQL Database 방화벽 규칙](sql-database-firewall-configure.md)을 참조하세요.

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

