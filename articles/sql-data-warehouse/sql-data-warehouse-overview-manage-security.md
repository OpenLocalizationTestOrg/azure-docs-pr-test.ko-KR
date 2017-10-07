---
title: "SQL 데이터 웨어하우스의 데이터베이스 aaaSecure | Microsoft Docs"
description: "솔루션 개발을 위해 Azure SQL 데이터 웨어하우스에서 데이터베이스를 보호하는 팁"
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 데이터베이스 보호
> [!div class="op_single_selector"]
> * [보안 개요](sql-data-warehouse-overview-manage-security.md)
> * [인증](sql-data-warehouse-authentication.md)
> * [암호화(포털)](sql-data-warehouse-encryption-tde.md)
> * [암호화(T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

이 문서는 Azure SQL 데이터 웨어하우스 데이터베이스를 보호의 hello 기초 안내 합니다. 특히, 이 문서는 데이터베이스에서 액세스 제한, 데이터 보호 및 작업 모니터링을 위한 리소스로 시작할 수 있습니다.

## <a name="connection-security"></a>연결 보안
연결 보안 참조 toohow 제한 하 고 방화벽 규칙 및 연결 암호화를 사용 하 여 연결 tooyour 데이터베이스 보안을 설정 합니다.

방화벽 규칙은 모두 hello 서버와 hello 데이터베이스 tooreject의에서 연결 시도 되지 않은 명시적으로 허용 목록 IP 주소에서 사용 됩니다. 응용 프로그램 또는 클라이언트 컴퓨터의 공용 IP 주소에서 tooallow 연결을 먼저 만들어야 합니다 hello Azure 포털, REST API 또는 PowerShell을 사용 하 여 서버 수준 방화벽 규칙입니다. 모범 사례로, 가능한 한 서버 방화벽을 통해 허용 hello IP 주소 범위를 제한 해야 합니다.  로컬 컴퓨터에서 Azure SQL 데이터 웨어하우스 tooaccess 확인 hello 방화벽 네트워크와 로컬 컴퓨터에서 TCP 포트 1433에서 나가는 통신을 허용 합니다.  자세한 내용은 [Azure SQL Database 방화벽][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] 및 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]을 참조하세요.

연결 tooyour SQL 데이터 웨어하우스는 기본적으로 암호화 됩니다.  연결 설정 toodisable 수정 암호화는 무시 됩니다.

## <a name="authentication"></a>인증
인증 참조 toohow toohello 데이터베이스를 연결할 때 사용자의 신원을 증명 합니다. SQL Data Warehouse는 현재 Azure Active Directory뿐 아니라 사용자 이름 및 암호를 사용하는 SQL Server 인증도 지원합니다. 

데이터베이스에 대 한 hello 논리 서버를 만들 때 "서버 관리자" 로그인 사용자 이름 및 암호를 지정 했습니다. 이러한 자격 증명을 사용 하 여 tooany 데이터베이스 hello 데이터베이스 소유자 또는 SQL Server 인증을 통해 "dbo"로 해당 서버에 인증할 수 있습니다.

그러나 모범 사례로, 조직의 사용자가 다른 계정 tooauthenticate를 사용 해야 합니다. 이렇게 toohello 응용 프로그램을 부여 하는 hello 사용 권한을 제한 하 고 응용 프로그램 코드는 취약 한 tooa SQL 주입 공격 하는 경우 악의적인 활동의 hello 위험을 줄일 수 있습니다. 

SQL Server 인증 사용자를 toocreate 연결 toohello **마스터** 데이터베이스 서버를 서버 관리자 로그인 하 고 새 서버 로그인을 만듭니다.  또한 Azure SQL 데이터 웨어하우스 사용자에 대 한 hello master 데이터베이스에서 좋습니다 toocreate 사용자 않습니다. Master에 사용자를 만들면 SSMS와 같은 도구를 사용 하 여 데이터베이스 이름을 지정 하지 않고 사용자 toologin이 있습니다.  또한 있게 toouse hello 개체 탐색기 tooview에 모든 데이터베이스를 SQL server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

그런 다음 tooyour 연결 **SQL 데이터 웨어하우스 데이터베이스** 서버 관리자 로그인과 방금 만든 hello server 로그인 기반 데이터베이스 사용자를 만듭니다.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

사용자는 로그인 만들기 또는 새 데이터베이스 만들기 등의 추가 작업을 수행 하는 경우 할당 된 toobe toohello 해야 됩니다 `Loginmanager` 및 `dbmanager` hello master 데이터베이스의 역할을 합니다. 이러한 추가 역할 및 인증 tooa SQL 데이터베이스에 대 한 자세한 내용은 참조 하십시오. [Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리][Managing databases and logins in Azure SQL Database]합니다.  SQL 데이터 웨어하우스에 대 한 Azure AD에 대 한 자세한 내용은 참조 하십시오. [데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여 tooSQL 연결][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]합니다.

## <a name="authorization"></a>권한 부여
권한 부여 toowhat는 Azure SQL 데이터 웨어하우스 데이터베이스 내에서 수행할 수 있습니다 및이 사용자 계정의 역할 멤버 자격과 권한에 의해 제어 됩니다. 모범 사례로, 사용자가 hello를 필요한 최소한의 권한만 부여 해야 합니다. Azure SQL 데이터 웨어하우스 T-SQL에서이 쉽게 toomanage 역할과 함께 사용 하면:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

hello 서버 관리자 계정으로 연결 하는 hello 데이터베이스 내의 모든 기관 toodo가 db_owner의 멤버인 합니다. 스키마 업그레이드 및 기타 관리 작업을 배포하기 위해서는 이 계정을 저장합니다. Hello로 응용 프로그램 toohello 데이터베이스에서 좀 더 제한적된 사용 권한 tooconnect hello "ApplicationUser" 계정을 사용 응용 프로그램에 필요한 최소 권한입니다.

toofurther도 같은 방법으로 사용자가 Azure SQL 데이터베이스와 함께 수행할 수 있는 작업

* 세분화 된 [권한을] [ Permissions] 제어 작업을 수행할 수 있습니다 수행에 개별 열, 테이블, 뷰, 프로시저 및 hello 데이터베이스에서 다른 개체를 사용 합니다. 사용 하 여 세분화 된 사용 권한 toohave 대부분 제어 hello 및 hello 필요한 최소한의 권한을 부여 합니다. hello 세분화 된 권한 시스템은 다소 복잡 하 고 일부 연구 toouse를 효과적으로 필요 합니다.
* [데이터베이스 역할] [ Database roles] db_datareader 및 db_datawriter 사용된 toocreate 수 이외의 보다 강력한 응용 프로그램 사용자 계정 또는 성능이 낮은 관리 계정. hello 기본 제공 고정된 데이터베이스 역할을 쉽게 toogrant 사용 권한을 제공 하지만 필요한 것 보다 많은 권한이 부여 될 수 있습니다.
* [저장 프로시저] [ Stored procedures] 사용된 toolimit hello 데이터베이스에서 수행할 수 있는 hello 동작 일 수 있습니다.

Hello Azure 클래식 포털에서에서 데이터베이스 및 논리 서버를 관리 하거나 hello Azure 리소스 관리자 API를 사용 하 여 포털 사용자 계정의 역할 할당에 의해 제어 됩니다. 이 항목에 대한 자세한 내용은 [Azure Portal의 역할 기반 액세스 제어][Role-based access control in Azure Portal]를 참조하세요.

## <a name="encryption"></a>암호화
Azure SQL 데이터 웨어하우스 투명 한 데이터 암호화 (TDE)는 실시간 암호화 및 미사용 데이터의 암호 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 하는 데 도움이 됩니다.  데이터베이스를 암호화 하는 경우 모든 변경 내용을 tooyour 응용 프로그램을 요구 하지 않고 연결 된 백업 및 트랜잭션 로그 파일 암호화 됩니다. TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다. SQL 데이터베이스의 hello 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호 됩니다. hello 기본 제공 서버 인증서는 각 SQL 데이터베이스 서버에 대해 고유 합니다. Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다. SQL 데이터 웨어하우스 사용 되는 hello 암호화 알고리즘은 AES 256입니다. TDE에 대한 일반적인 설명은 [투명한 데이터 암호화][Transparent Data Encryption]를 참조하세요.

Hello를 사용 하 여 데이터베이스를 암호화할 수 [Azure 포털] [ Encryption with Portal] 또는 [T-SQL][Encryption with TSQL]합니다.

## <a name="next-steps"></a>다음 단계
세부 정보 및 서로 다른 프로토콜을 사용 하 여 SQL 데이터 웨어하우스 tooyour 연결에 대 한 예제를 참조 하세요. [tooSQL 데이터 웨어하우스 연결][Connect tooSQL Data Warehouse]합니다.

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
