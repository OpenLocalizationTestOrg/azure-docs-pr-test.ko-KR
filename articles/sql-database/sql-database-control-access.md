---
title: "SQL 데이터베이스 aaaGranting 액세스 tooAzure | Microsoft Docs"
description: "Azure SQL 데이터베이스 액세스 tooMicrosoft 권한을 부여 하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Azure SQL Database 액세스 제어
보안 tooprovide SQL 데이터베이스의 id 및 사용자가 toospecific 작업 및 데이터를 제한 하는 권한 부여 메커니즘 사용자 tooprove를 요구 하는 인증 메커니즘 IP 주소로 연결을 제한 하는 방화벽 규칙으로 액세스를 제어 합니다. 

> [!IMPORTANT]
> Hello SQL 데이터베이스 보안 기능 개요를 참조 하십시오. [SQL 보안 개요](sql-database-security-overview.md)합니다. 자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.

## <a name="firewall-and-firewall-rules"></a>방화벽 및 방화벽 규칙
Microsoft Azure SQL Database는 Azure 및 기타 인터넷 기반 응용 프로그램의 관계형 데이터베이스 서비스를 제공합니다. toohelp 데이터 보호, 방화벽 권한이 있는 컴퓨터를 지정할 때까지 모든 액세스 tooyour 데이터베이스 서버를 차단 합니다. hello 방화벽 액세스 toodatabases hello 시작 IP 주소를 각 요청에 따라 권한을 부여 합니다. 자세한 내용은 [Azure SQL Database 방화벽 규칙 개요](sql-database-firewall-configure.md)를 참조하세요.

hello Azure SQL 데이터베이스 서비스 TCP 포트 1433 통해서만 제공 됩니다. 사용자의 컴퓨터에서 SQL 데이터베이스 tooaccess 클라이언트 컴퓨터 방화벽이 TCP 포트 1433에서 보내는 TCP 통신을 허용 하는지 확인 합니다. 다른 응용 프로그램에 필요하지 않은 경우 TCP 포트 1433의 인바운드 연결을 차단합니다. 

Hello 연결 프로세스의 일환으로, Azure 가상 컴퓨터에서 연결은 리디렉션된 tooa 다른 IP 주소와 포트를 각 작업자 역할에 대해 고유 합니다. hello 포트 번호가 11000 too11999에서 hello 사이입니다. TCP 포트에 대한 자세한 내용은 [ADO.NET 4.5 및 SQL Database2에 대한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)를 참조하세요.

## <a name="authentication"></a>인증

SQL 데이터베이스는 두 가지 인증 유형을 지원합니다.

* **SQL 인증**은 사용자 이름과 암호를 사용합니다. 데이터베이스에 대 한 hello 논리 서버를 만들 때 "서버 관리자" 로그인 사용자 이름 및 암호를 지정 했습니다. 이러한 자격 증명을 사용 하 여 tooany 데이터베이스 hello 데이터베이스 소유자 또는 "dbo"로 해당 서버에 인증할 수 있습니다. 
* **Azure Active Directory 인증**은 Azure Active Directory에서 관리하는 ID를 사용하고 관리되고 통합된 도메인을 지원합니다. [가능한 경우](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) Active Directory 인증(통합 보안)을 사용합니다. Toouse Azure Active Directory 인증을 사용 하도록 하려는 경우 hello tooadminister Azure AD 사용자 및 그룹은 허용 "Azure AD 관리"를 호출 하는 다른 서버 관리자를 만들어야 합니다. 이 관리자는 일반 서버 관리자가 할 수 있는 모든 작업을 수행할 수도 있습니다. 참조 [데이터베이스를 사용 하 여 Azure Active Directory 인증 여 tooSQL 연결](sql-database-aad-authentication.md) 방법의 연습은 toocreate Azure AD 관리자 tooenable Azure Active Directory 인증 합니다.

데이터베이스 엔진 hello 30 분 이상 유휴 상태로 유지 하는 연결을 닫습니다. 연결 hello 사용 하려면 먼저 다시 로그인 해야 합니다. 활성 연결 tooSQL 데이터베이스 권한을 다시 부여할 (hello 데이터베이스 엔진에 의해 수행 됨)을 필요로 하는 지속적으로 10 시간 이상 마다. hello 데이터베이스 엔진 재인증 hello 제출 된 원래 암호를 사용 하 고 없는 사용자 입력이 필요 합니다. 성능상의 이유로 SQL 데이터베이스에서 암호가 재설정 될 때 hello 연결 없으면 tooconnection 풀링 인해 hello 연결이 다시 설정 하는 경우에 다시 인증할 수 있습니다. 이 온-프레미스 SQL Server의 hello 동작과에서 다릅니다. Hello 연결은 초기 인증 후 hello 암호가 변경 된 hello 연결을 종료 해야 하 고 hello 새 암호를 사용 하 여 새 연결 합니다. Hello로 사용자 `KILL DATABASE CONNECTION` hello를 사용 하 여 사용 권한을 연결 tooSQL 데이터베이스를 명시적으로 종료할 수 [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) 명령입니다.

사용자 계정을 hello master 데이터베이스에 만들 수 있으며 hello 서버의 모든 데이터베이스에서 사용 권한을 부여할 수 있습니다 또는 hello 데이터베이스 자체 (포함 된 사용자 라고 함)에서 만들 수 있습니다. 로그인 만들기 및 관리에 대한 자세한 내용은 [로그인 관리](sql-database-manage-logins.md)를 참조하세요. tooenhance 이식성 및 scalabilty, 포함 된 데이터베이스 사용자가 tooenhance 확장성을 사용 합니다. 포함된 사용자에 대한 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [사용자 만들기(Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) 및 [포함된 데이터베이스](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases)를 참조하세요.

가장 좋은 방법은 응용 프로그램 사용 해야 전용된 계정 tooauthenticate-toohello 응용 프로그램을 부여 하는 hello 사용 권한을 제한 하 고 응용 프로그램 코드는 취약 한 tooa SQL 주입 하는 경우 악의적인 활동의 hello 위험을 줄일 수 있습니다 이러한 방식으로 공격입니다. hello 권장 방법은 toocreate는 [포함 된 데이터베이스 사용자](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), 앱 tooauthenticate을 허용 하는 직접 toohello 데이터베이스입니다. 

## <a name="authorization"></a>권한 부여

권한 부여 toowhat는 사용자는 Azure SQL 데이터베이스 내에서 수행할 수 있는 사용자 계정의 데이터베이스에 의해 제어 됩니다 및 [역할 멤버 자격](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) 및 [개체 수준 사용 권한](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)합니다. 모범 사례로, 사용자가 hello를 필요한 최소한의 권한만 부여 해야 합니다. hello 서버 관리자 계정으로 연결 하는 hello 데이터베이스 내의 모든 기관 toodo가 db_owner의 멤버인 합니다. 스키마 업그레이드 및 기타 관리 작업을 배포하기 위해서는 이 계정을 저장합니다. Hello로 응용 프로그램 toohello 데이터베이스에서 좀 더 제한적된 사용 권한 tooconnect hello "ApplicationUser" 계정을 사용 응용 프로그램에 필요한 최소 권한입니다. 자세한 내용은 [로그인 관리](sql-database-manage-logins.md)를 참조하세요.

일반적으로 관리자만 toohello에 액세스할 필요 `master` 데이터베이스입니다. 각 데이터베이스에서 만든 관리자가 아닌 포함 된 데이터베이스 사용자가 통해 일상적인 액세스 tooeach 사용자 데이터베이스 여야 합니다. 포함 된 데이터베이스 사용자를 사용 하면 hello에서 toocreate 로그인 불필요 `master` 데이터베이스입니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable)를 참조하세요.

사용 되는 toolimit 하거나 권한을 높일 수 있는 기능을 수행 하는 hello를 잘 이해 해야 합니다.   
* [가장](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) 및 [모듈 서명](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) 수 수 사용된 toosecurely 권한 상승을 일시적으로 합니다.
* [행 수준 보안](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) 은 사용자가 액세스할 수 있는 행을 제한하는 데 사용할 수 있습니다.
* [데이터 마스킹](sql-database-dynamic-data-masking-get-started.md) 중요 한 데이터의 사용된 toolimit 노출 될 수 있습니다.
* [저장 프로시저](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) 사용된 toolimit hello 데이터베이스에서 수행할 수 있는 hello 동작 일 수 있습니다.

## <a name="next-steps"></a>다음 단계

- Hello SQL 데이터베이스 보안 기능 개요를 참조 하십시오. [SQL 보안 개요](sql-database-security-overview.md)합니다.
- 방화벽 규칙에 대해 자세히 toolearn 참조 [방화벽 규칙](sql-database-firewall-configure.md)합니다.
- 사용자와 로그인을 하는 방법에 대 한 toolearn 참조 [로그인 관리](sql-database-manage-logins.md)합니다. 
- 사전 모니터링에 대한 설명은 [데이터베이스 감사](sql-database-auditing.md) 및 [SQL Database 위협 검색](sql-database-threat-detection.md)을 참조하세요.
- 자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.
