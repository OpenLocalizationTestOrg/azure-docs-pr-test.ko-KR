---
title: "aaaAzure SQL 로그인 및 사용자 | Microsoft Docs"
description: "자세한 내용은 SQL 데이터베이스 보안 관리에 대 한 방법을 구체적으로 toomanage 데이터베이스 액세스 및 로그인 보안을 통해 hello 서버 수준 보안 주체입니다."
keywords: "sql 데이터베이스 보안,데이터베이스 보안 관리,로그인 보안,데이터베이스 보안,데이터베이스 액세스"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>데이터베이스 액세스 제어 및 권한 부여

방화벽 규칙 구성 된 경우에 사용자 hello 관리자 계정 중 하나로, hello 데이터베이스 소유자 또는 hello 데이터베이스에서 데이터베이스 사용자로 tooa SQL 데이터베이스에 연결할 수 있습니다.  

>  [!NOTE]  
>  이 항목 tooAzure SQL server 및 hello Azure SQL server에서 생성 된 tooboth SQL 데이터베이스 및 SQL 데이터 웨어하우스 데이터베이스에 적용 합니다. 간단히 하기 위해 SQL 데이터베이스 tooboth SQL 데이터베이스 및 SQL 데이터 웨어하우스를 참조할 때 사용 됩니다. 
>

> [!TIP]
> 자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.
>


## <a name="unrestricted-administrative-accounts"></a>무제한 관리 계정
관리자로 작동하는 두 가지 관리 계정(**서버 관리자** 및 **Active Directory 관리자**)이 있습니다. tooidentify 위해 SQL server의 관리자 계정은 이러한 열고 hello Azure 포털 및 SQL server의 toohello 속성을 탐색 합니다.

![SQL Server 관리자](./media/sql-database-manage-logins/sql-admins.png)

- **서버 관리자**   
Azure SQL 서버를 만들 때 **서버 관리자 로그인**을 지정해야 합니다. SQL server hello master 데이터베이스에 로그인 할 때 해당 계정을 만듭니다. 이 계정은 SQL Server 인증(사용자 이름 및 암호)을 사용하여 연결됩니다. 이러한 계정 중 하나만 존재할 수 있습니다.   
- **Azure Active Directory 관리자**   
하나의 Azure Active Directory 계정, 개인 또는 보안 그룹 계정을 관리자로 구성할 수도 있습니다. 선택적 tooconfigure Azure AD 관리자 이지만 toouse Azure AD 계정 tooconnect tooSQL 데이터베이스 하려는 경우 Azure AD 관리자를 구성 해야 합니다. Azure Active Directory 액세스를 구성 하는 방법에 대 한 자세한 내용은 참조 [연결 tooSQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여](sql-database-aad-authentication.md) 및 [SSMS SQL로 Azure AD MFA에 대 한 지원 데이터베이스 및 SQL 데이터 웨어하우스](sql-database-ssms-mfa-authentication.md)합니다.
 

hello **서버 관리자** 및 **Azure AD 관리자** 계정 hello 특성 뒤에:
- 이들은 hello hello 서버의 tooany SQL 데이터베이스를 자동으로 연결할 수 있는 유일한 계정입니다. (tooconnect tooa 사용자 데이터베이스를 다른 계정 이어야 합니다. hello의 hello 소유자, 데이터베이스 또는 hello 사용자 데이터베이스에 사용자 계정이 있어야 합니다.)
- 이러한 계정은 hello로 사용자 데이터베이스를 입력 `dbo` 사용자 고 hello 사용자 데이터베이스에서 모든 hello 권한을 보유 합니다. (사용자 데이터베이스의 소유자 hello도 hello 데이터베이스 자동으로 입력 hello `dbo` 사용자입니다.) 
- 이러한 계정은 hello를 입력 하지 않으면 `master` hello와 데이터베이스 `dbo` 사용자 있으며 master에 대 한 사용 권한을 제한 합니다. 
- 이러한 계정은 hello의 구성원이 아닌 표준 SQL Server `sysadmin` SQL 데이터베이스에서 사용할 수 없는 고정된 서버 역할을 합니다.  
- 이러한 계정은 데이터베이스, 로그인, master의 사용자 및 서버 수준 방화벽 규칙을 만들고 변경하고 삭제할 수 있습니다.
- 이러한 계정을 추가 하거나 제거 멤버 toohello `dbmanager` 및 `loginmanager` 역할입니다.
- 이러한 계정은 hello를 볼 수 `sys.sql_logins` 시스템 테이블입니다.

### <a name="configuring-hello-firewall"></a>Hello 방화벽 구성
를 개별 IP 주소 또는 범위에 대 한 hello 서버 수준 방화벽을 구성 된 경우 hello **SQL server 관리** 및 hello **Azure Active Directory 관리자** toohello master 데이터베이스 및 모든 hello 연결할 수 있습니다 사용자 데이터베이스입니다. hello 통해 hello 초기 서버 수준 방화벽을 구성할 수 있습니다 [Azure 포털](sql-database-get-started-portal.md)를 사용 하 여 [PowerShell](sql-database-get-started-powershell.md) hello를 사용 하 여 또는 [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx)합니다. 연결이 설정되면 [Transact-SQL](sql-database-configure-firewall-settings.md)을 사용하여 추가 서버 수준 방화벽 규칙도 구성할 수 있습니다.

### <a name="administrator-access-path"></a>관리자 액세스 경로
Hello 서버 수준 방화벽을 올바르게 구성한 경우 hello **SQL server 관리** 및 hello **Azure Active Directory 관리자** SQL Server Management Studio 또는 SQL과 같은 클라이언트 도구를 사용 하 여 연결 수 서버 데이터 도구입니다. Hello 최신 도구만 모든 hello 기능 및 기능을 제공 합니다. hello 다음 다이어그램에서는 hello에 대 한 일반적인 구성을 두 관리자 계정

![관리자 액세스 경로](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Hello 서버 수준 방화벽에서 열려 있는 포트를 사용할 경우 관리자는 tooany SQL 데이터베이스를 연결할 수 있습니다.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용 하 여 tooa 데이터베이스 연결
서버, 데이터베이스, 서버 수준 방화벽 규칙을 만들고 SQL Server Management Studio tooquery 데이터베이스를 사용 하는 연습을 참조 하세요. [hello Azure 포털을 사용 하 여 Azure SQL 데이터베이스 서버, 데이터베이스 및 방화벽 규칙 시작 및 SQL Server Management Studio](sql-database-get-started-portal.md)합니다.

> [!IMPORTANT]
> 항상 hello를 사용 하는 것이 좋습니다. 최신 버전 tooremain Management Studio의 Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다. [SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>추가 서버 수준 관리 역할
또한 앞에서 설명한 서버 수준 관리 역할을 toohello, SQL 데이터베이스는 tooeither 데이터베이스를 만들거나 관리 하는 사용 권한을 부여 하는 hello master 데이터베이스 toowhich 사용자 계정에는 두 가지 제한 된 관리 역할을 추가할 수 있습니다. 로그인 합니다.

### <a name="database-creators"></a>데이터베이스 작성자
이러한 관리자 역할 중 하나는 hello **dbmanager** 역할입니다. 이 역할의 멤버는 새 데이터베이스를 만들 수 있습니다. toouse hello에서 사용자를 만들고이 역할 `master` 데이터베이스에 있으며 다음 hello 사용자 toohello 추가 **dbmanager** 데이터베이스 역할입니다. 데이터베이스 toocreate 사용자 hello master 데이터베이스에는 SQL Server 로그인 또는 데이터베이스 사용자는 Azure Active Directory 사용자에 따라 포함 된 hello 사용자 여야 합니다.

1. Toohello master 데이터베이스를 연결 관리자 계정을 사용 합니다.
2. 선택적 단계: hello를 사용 하 여 SQL Server 인증 로그인 만들기 [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) 문. 샘플 문:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > 로그인 또는 포함된 데이터베이스 사용자를 만들 때는 강력한 암호를 사용합니다. 자세한 내용은 [강력한 암호](https://msdn.microsoft.com/library/ms161962.aspx)를 참조하십시오.
    
   tooimprove 성능 로그인 (서버 수준 보안 주체) hello 데이터베이스 수준에서 일시적으로 캐시 됩니다. toorefresh hello 인증 캐시 참조 [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx)합니다.

3. Hello master 데이터베이스에 hello를 사용 하 여 사용자를 만들 [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) 문. Azure Active Directory 인증 포함 된 데이터베이스 사용자 (Azure AD 인증에 대 한 환경을 구성한) 하는 경우, 또는 SQL Server 인증 포함 된 데이터베이스 사용자 또는 SQL에 따라 SQL Server 인증 사용자 hello 사용자 수 있습니다. 서버 인증 로그인 (hello 이전 단계에서 만든). 샘플 문:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Toohello hello 새 사용자 추가 **dbmanager** hello를 사용 하 여 데이터베이스 역할 [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) 문. 샘플 문:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > hello dbmanager는 데이터베이스 역할 master 데이터베이스에 있으므로 데이터베이스 사용자 toohello dbmanager 역할에만 추가할 수 있습니다. 서버 수준 로그인 toodatabase 수준 역할을 추가할 수 없습니다.
    
5. 필요한 경우에 방화벽 규칙 tooallow hello 새 사용자 tooconnect을 구성 합니다. (hello 새 사용자는 기존 방화벽 규칙으로 다룰 수 수 있습니다.)

이제 hello 사용자 toohello master 데이터베이스를 연결할 수 있습니다 및 새 데이터베이스를 만들 수 있습니다. hello 데이터베이스를 만드는 hello 계정이 hello hello 데이터베이스 소유자가 됩니다.

### <a name="login-managers"></a>로그인 관리자
hello 다른 관리 역할은 hello 로그인 관리자 역할입니다. 이 역할의 멤버 hello master 데이터베이스에 새 로그인을 만들 수 있습니다. 완료할 수를 동일한 단계를 hello (로그인 및 사용자를 만들고 사용자 toohello 추가 **loginmanager** 역할) tooenable 사용자 hello 마스터의 toocreate 새 로그인 합니다. 일반적으로 로그인으로 로그인을 기반으로 하는 사용자가 사용 하는 대신 권장 hello에 인증 하는 포함 된 데이터베이스 사용자를 사용 하 여 데이터베이스 수준 필요 하지 않습니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.

## <a name="non-administrator-users"></a>비관리자 사용자
일반적으로 관리자가 아닌 계정 액세스 하지 않습니다 필요 toohello master 데이터베이스. Hello를 사용 하 여 hello 데이터베이스 수준에서 포함 된 데이터베이스 사용자 만들기 [CREATE USER (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) 문. Azure Active Directory 인증 포함 된 데이터베이스 사용자 (Azure AD 인증에 대 한 환경을 구성한) 하는 경우, 또는 SQL Server 인증 포함 된 데이터베이스 사용자 또는 SQL에 따라 SQL Server 인증 사용자 hello 사용자 수 있습니다. 서버 인증 로그인 (hello 이전 단계에서 만든). 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요. 

toocreate 사용자 toohello 데이터베이스 연결 및 문 비슷한 toohello 예제 따르는 실행:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

처음에 hello 관리자나 hello 데이터베이스의 hello 소유자 중 하나에만 사용자를 만들 수 있습니다. tooauthorize 추가 사용자 toocreate 새 사용자를 해당 선택한 사용자 hello 부여 `ALTER ANY USER` 같은 문을 사용 하 여 사용 권한:

```
GRANT ALTER ANY USER tooMary;
```

toogive hello 데이터베이스의 추가 사용자에 게 모든 권한이 있도록 hello 소속 **db_owner** hello를 사용 하 여 고정된 데이터베이스 역할 `ALTER ROLE` 문.

> [!NOTE]
> hello, 로그인을 기반으로 가장 일반적인 이유 toocreate 데이터베이스 사용자는 경우에 toomultiple 데이터베이스에 액세스 해야 하는 SQL Server 인증 사용자입니다. 로그인을 기반으로 하는 사용자가 동률된 toohello 로그인 및 해당 로그인에 대해 유지 관리 되는 하나의 암호입니다. 개별 데이터베이스에 포함된 데이터베이스 사용자는 각 개별 엔터티이며 각각 고유한 암호를 유지 관리합니다. 사용자가 동일하게 암호를 유지 관리하지 않으면 포함된 데이터베이스 사용자를 혼동할 수 있습니다.

### <a name="configuring-hello-database-level-firewall"></a>Hello 데이터베이스 수준 방화벽 구성
모범 사례로, 관리자 이외의 사용자는 사용 하는 hello 방화벽 toohello 데이터베이스를 통한 액세스 하나만 있어야 합니다. 해당 IP 권한을 부여 하는 대신 서버 수준 hello 통해 주소 방화벽 및 hello를 사용 하 여 access tooall 데이터베이스 제공 [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) 문 tooconfigure hello 데이터베이스 수준 방화벽입니다. hello 포털을 사용 하 여 hello 데이터베이스 수준 방화벽을 구성할 수 없습니다.

### <a name="non-administrator-access-path"></a>비관리자 액세스 경로
Hello 데이터베이스 수준 방화벽이 올바르게 구성 하는 경우 SQL Server Management Studio와 같은 클라이언트 도구 또는 SQL Server Data Tools를 사용 하 여 hello 데이터베이스 사용자를 연결할 수 있습니다. Hello 최신 도구만 모든 hello 기능 및 기능을 제공 합니다. hello 다음 다이어그램에서는 일반적인 비관리자 액세스 경로를 보여 줍니다.

![비관리자 액세스 경로](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>그룹 및 역할
효율적으로 액세스 관리 toogroups 및 개별 사용자 대신 역할에 할당 된 사용 권한을 사용 합니다. 

- Azure Active Directory 인증을 사용하는 경우 Azure Active Directory 사용자를 Azure Active Directory 그룹에 배치합니다. Hello 그룹에 대 한 포함 된 데이터베이스 사용자를 만듭니다. 하나 이상의 데이터베이스 사용자로 배치는 [데이터베이스 역할](https://msdn.microsoft.com/library/ms189121) 후 할당 [권한을](https://msdn.microsoft.com/library/ms191291.aspx) toohello 데이터베이스 역할입니다.

- SQL Server 인증을 사용할 때는 hello 데이터베이스에 포함 된 데이터베이스 사용자를 만듭니다. 하나 이상의 데이터베이스 사용자로 배치는 [데이터베이스 역할](https://msdn.microsoft.com/library/ms189121) 후 할당 [권한을](https://msdn.microsoft.com/library/ms191291.aspx) toohello 데이터베이스 역할입니다.

데이터베이스 역할 hello hello 기본 제공 역할 같은 수 **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, 및 **db_denydatareader**합니다. **db_owner** toogrant 자주 사용 되는 모든 권한을 tooonly 몇 가지 사용자입니다. hello 다른 고정된 데이터베이스 역할 신속 하 게 개발에서 간단한 데이터베이스를 보는 데 유용 하지만 대부분의 프로덕션 데이터베이스에 적합 하지 않습니다. 예를 들어 hello **db_datareader** 고정된 데이터베이스 역할은 일반적으로 hello 데이터베이스에 대 한 읽기 액세스 tooevery 테이블 이상 반드시 필요한 것은 권한을 부여 합니다. 훨씬 더 낫습니다 toouse hello는 [역할 만들기](https://msdn.microsoft.com/library/ms187936.aspx) 문 toocreate 사용자 자신의 사용자 정의 데이터베이스 역할 및 각 역할 hello를 신중 하 게 hello 비즈니스 요구 사항에 필요한 최소 사용 권한을 부여 합니다. 사용자가 여러 역할의 구성원이, 모두의 hello 사용 권한의 집계 합니다.

## <a name="permissions"></a>권한
SQL 데이터베이스에는 개별적으로 부여하거나 거부할 수 있는 100개가 넘는 사용 권한이 있습니다. 이러한 사용 권한은 대부분 중첩됩니다. 예를 들어 hello `UPDATE` hello를 포함 하는 스키마에 대 한 권한이 `UPDATE` 해당 스키마 내에서 각 테이블에 대 한 권한이 있습니다. 대부분의 권한 시스템에서와 같이 hello 사용 권한 거부 권한 부여를 재정의합니다. 중첩 된 hello 특성과 권한의 hello 수 때문에 데이터베이스를 보호 하는 적절 한 사용 권한이 시스템 tooproperly 연구 toodesign 신중 하 게 걸릴 수 있습니다. 사용 권한 hello 목록과 함께 시작 [사용 권한 (데이터베이스 엔진)](https://msdn.microsoft.com/library/ms191291.aspx) hello 검토 [포스터 크기 그래픽](http://go.microsoft.com/fwlink/?LinkId=229142) hello 사용 권한.


### <a name="considerations-and-restrictions"></a>고려 사항 및 제한 사항
SQL 데이터베이스에서 로그인 및 사용자를 관리할 때는 hello 다음 사항을 고려 합니다.

* 연결 된 toohello 해야 **마스터** hello를 실행할 때 데이터베이스 `CREATE/ALTER/DROP DATABASE` 문.   
* 데이터베이스 사용자에 대 한 해당 toohello hello **서버 관리자** 로그인을 변경 또는 삭제할 수 없습니다. 
* 미국-영어는 hello 기본 언어의 hello **서버 관리자** 로그인 합니다.
* 관리자만 hello (**서버 관리자** 로그인 또는 Azure AD 관리자) hello의 구성원과 hello **dbmanager** 데이터베이스 역할에 hello **마스터** 데이터베이스에 적용 사용 권한 tooexecute hello `CREATE DATABASE` 및 `DROP DATABASE` 문.
* Hello를 실행 하는 경우 연결 된 toohello master 데이터베이스 해야 `CREATE/ALTER/DROP LOGIN` 문. 그러나 로그인 사용은 권장되지 않습니다. 대신에 포함된 데이터베이스 사용자를 사용합니다.
* tooconnect tooa 사용자 데이터베이스 hello hello 연결 문자열에는 데이터베이스의 hello 이름을 제공 해야 합니다.
* 서버 수준의 보안 주체 로그인과 hello 멤버 hello만 hello **loginmanager** hello의 데이터베이스 역할 **마스터** 데이터베이스 사용 권한 tooexecute hello가 `CREATE LOGIN`, `ALTER LOGIN`, 및 `DROP LOGIN` 문.
* Hello를 실행할 때 `CREATE/ALTER/DROP LOGIN` 및 `CREATE/ALTER/DROP DATABASE` ADO.NET 응용 프로그램에서 문을 매개 변수화 된 명령을 사용할 수 없습니다. 자세한 내용은 [명령 및 매개 변수](https://msdn.microsoft.com/library/ms254953.aspx)를 참조하세요.
* Hello를 실행할 때 `CREATE/ALTER/DROP DATABASE` 및 `CREATE/ALTER/DROP LOGIN` 문은, 해당 문만 있어야 TRANSACT-SQL 일괄 처리 내의 문만 hello 합니다. 그렇지 않은 경우 오류가 발생합니다. 다음 TRANSACT-SQL hello 데이터베이스의 존재 여부 확인 hello 예를 들어 있습니다. 이 특성이 있으면는 `DROP DATABASE` 문을 tooremove hello 데이터베이스 라고 합니다. 때문에 hello `DROP DATABASE` 문이 hello 일괄 처리에서 유일한 문 hello 않습니다, hello 다음 실행할 TRANSACT-SQL 문을 실행 하면 오류가 발생 합니다.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Hello를 실행할 때 `CREATE USER` hello 사용 하 여 문을 `FOR/FROM LOGIN` 옵션을 여야 TRANSACT-SQL 일괄 처리 내의 문만 hello 합니다.
* Hello를 실행할 때 `ALTER USER` hello 사용 하 여 문을 `WITH LOGIN` 옵션을 여야 TRANSACT-SQL 일괄 처리 내의 문만 hello 합니다.
* 너무`CREATE/ALTER/DROP` 사용자에 게 필요한 hello `ALTER ANY USER` hello 데이터베이스에 대 한 권한이 있습니다.
* 데이터베이스 역할의 소유자 hello tooadd 또는 데이터베이스 역할에서 다른 데이터베이스 사용자 tooor 제거를 시도할 때 hello 다음 오류가 발생할 수 있습니다: **사용자 또는 역할 'Name'이 데이터베이스에 존재 하지 않습니다.** 이 오류는 hello 사용자 표시 toohello 소유자 없기 때문에 발생 합니다. tooresolve이 문제를 부여 hello 역할 소유자 hello `VIEW DEFINITION` hello 사용자에 대 한 권한이 있습니다. 


## <a name="next-steps"></a>다음 단계

- 방화벽 규칙에 대해 자세히 toolearn 참조 [Azure SQL 데이터베이스 방화벽](sql-database-firewall-configure.md)합니다.
- 모든 hello SQL 데이터베이스 보안 기능 개요를 참조 하십시오. [SQL 보안 개요](sql-database-security-overview.md)합니다.
- 자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.
- 보기 및 저장 프로시저에 대한 자세한 내용은 [보기 및 저장 프로시저 만들기](https://msdn.microsoft.com/library/ms365311.aspx)를 참조하세요.
- Access tooa 데이터베이스 개체 권한을 부여 하는 방법에 대 한 정보를 참조 하세요. [액세스 부여 tooa 데이터베이스 개체](https://msdn.microsoft.com/library/ms365327.aspx)
