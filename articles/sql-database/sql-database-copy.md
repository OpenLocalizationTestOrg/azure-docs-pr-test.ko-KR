---
title: "Azure SQL 데이터베이스 aaaCopy | Microsoft Docs"
description: "Azure SQL 데이터베이스 사본 만들기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Azure SQL 데이터베이스 복사

Azure SQL 데이터베이스 제공 동일 하거나 hello에 기존 Azure SQL의 일관성이 복사본을 만드는 여러 가지 방법을 데이터베이스 서버나 다른 서버입니다. Hello Azure 포털, PowerShell 또는 T-SQL을 사용 하 여 SQL 데이터베이스를 복사할 수 있습니다. 

## <a name="overview"></a>개요

데이터베이스 복사본은 복사 요청 hello hello 시간을 기준으로 hello 원본 데이터베이스의 스냅숏입니다. 선택할 수 있습니다 동일한 서버 또는 다른 서버, 서비스 계층과 성능 수준이, 또는 hello 내에서 다른 성능 수준 hello 동일한 서비스 계층 (버전). Hello 복사가 완료 된 후에 완벽 하 게 작동 되는, 독립적인 데이터베이스 있게 됩니다. 이 시점에서 업그레이드 하거나 tooany 버전 다운 그레이드할 수 있습니다. hello 로그인, 사용자 및 사용 권한 수 독립적으로 관리 합니다.  

## <a name="logins-in-hello-database-copy"></a>Hello 데이터베이스 복사본의 로그인

데이터베이스 toohello를 복사 하는 경우 동일한 논리 서버, hello 두 데이터베이스 모두에 동일한 로그인을 사용할 수 있습니다. hello 보안 toocopy hello 데이터베이스를 사용 하 여 사용자에 hello 새 데이터베이스에 hello 데이터베이스 소유자가 됩니다. 모든 데이터베이스 사용자, 해당 사용 권한 및의 보안 식별자 (Sid)가 toohello 데이터베이스 복사본을 복사 합니다.  

데이터베이스 tooa 다른 논리 서버로 복사할 때 hello 보안 hello 새 서버에서 사용자에 hello 새 데이터베이스에 hello 데이터베이스 소유자가 됩니다. 사용 하는 경우 [포함 된 데이터베이스 사용자](sql-database-manage-logins.md) 데이터 액세스를 위해 다음과 같이 모두 hello 기본 및 보조 데이터베이스는 항상 hello 하는 hello 복사 된 후 완료 하면 되므로 동일한 사용자 자격 증명에 즉시 액세스할 수 있는 동일한 hello 사용 하 여 자격 증명입니다. 

사용 하는 경우 [Azure Active Directory](../active-directory/active-directory-whatis.md), hello 복사본에 대 한 자격 증명을 관리 하기 위한 hello 요구를 완전히 제거할 수 있습니다. 그러나 hello 데이터베이스 tooa 새 서버를 복사할 때 hello 로그인 기반 액세스 수 없으므로 작동 되지, hello 로그인 hello 새 서버에 존재 하지 않습니다. toolearn 데이터베이스 tooa 다른 논리 서버를 복사 하는 경우 로그인을 관리 하는 방법에 대 한 참조 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다. 

Hello 복사 성공 후 및 다른 사용자가 다시 매핑하기 전에 hello hello 데이터베이스 소유자 hello 복사를 시작한 로그인 로그인 수 toohello 새 데이터베이스. tooresolve 로그인 hello 복사 작업을 완료 한 후 참조 [로그인을 해결](#resolve-logins)합니다.

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 데이터베이스를 복사 합니다.

데이터베이스를 사용 하 여 Azure 포털에서 데이터베이스 열기 hello 페이지 hello 및 클릭 toocopy **복사**합니다. 

   ![데이터베이스 복사](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>PowerShell을 사용하여 데이터베이스 복사

PowerShell을 사용 하 여 hello를 사용 하 여 데이터베이스 toocopy [새로 AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

전체 샘플 스크립트에 대 한 참조 [데이터베이스 tooa 새 서버에 복사](scripts/sql-database-copy-database-to-new-server-powershell.md)합니다.

## <a name="copy-a-database-by-using-transact-sql"></a>Transact-SQL을 사용하여 데이터베이스 복사

Hello 서버 수준 보안 주체 로그인 이나 toocopy hello 데이터베이스를 만든 사람의 로그인 정보 hello와 데이터베이스 toohello 마스터에 로그인 합니다. Toosucceed를 복사 하는 데이터베이스에 대 한 hello 서버 수준 보안 주체가 없는 로그인 hello dbmanager 역할의 구성원 이어야 합니다. 로그인과 연결 toohello 서버에 대 한 자세한 내용은 참조 [로그인 관리](sql-database-manage-logins.md)합니다.

Hello hello 원본 데이터베이스 복사를 시작 [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) 문. 이 문을 실행 hello 데이터베이스 복사 프로세스가 시작 됩니다. 데이터베이스 복사는 비동기 프로세스 이므로 hello 데이터베이스 복사가 완료 되기 전에 hello CREATE DATABASE 문을 반환 합니다.

### <a name="copy-a-sql-database-toohello-same-server"></a>SQL 데이터베이스 toohello 복사 동일한 서버
Hello 서버 수준 보안 주체 로그인 이나 toocopy hello 데이터베이스를 만든 사람의 로그인 정보 hello와 데이터베이스 toohello 마스터에 로그인 합니다. Toosucceed를 복사 하는 데이터베이스에 대 한 hello 서버 수준 보안 주체가 없는 로그인 hello dbmanager 역할의 구성원 이어야 합니다.

이 명령은 복사 Database1 tooa 새 데이터베이스 Database2 hello에 이름이 표시 된 같은 서버. 데이터베이스의 hello 크기에 따라 작업을 복사 하는 hello 일부 시간 toocomplete를 걸릴 수 있습니다.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>SQL 데이터베이스 tooa 다른 서버에 복사

여기서 hello 새 데이터베이스는 만든 toobe hello SQL 데이터베이스 서버 hello 대상 서버의 데이터베이스 toohello 마스터에 로그인 합니다. Hello 원본 SQL 데이터베이스 서버에서 hello 원본 데이터베이스의 데이터베이스 소유자 hello로 동일한 이름 및 암호 hello에 있는 로그인을 사용 합니다. 또한 hello 대상 서버에서 로그인의 hello hello dbmanager 역할의 멤버 여야 하거나 hello 서버 수준 보안 주체 로그인 해야 합니다.

이 명령은 2에 Database2 라는 server1 tooa 새 데이터베이스에 Database1를 복사 합니다. 데이터베이스의 hello 크기에 따라 작업을 복사 하는 hello 일부 시간 toocomplete를 걸릴 수 있습니다.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>작업을 복사 하는 hello hello 진행률 모니터링

Hello sys.databases 및 sys.dm_database_copies 뷰를 쿼리하여 hello 복사 프로세스를 모니터링 합니다. 진행 중인 hello 복사, 동안 hello **state_desc** hello 새 데이터베이스에 대 한 hello sys.databases 뷰의 열이 너무 설정 되어**COPYING**합니다.

* Hello 복사에 실패할 경우 hello **state_desc** hello 새 데이터베이스에 대 한 hello sys.databases 뷰의 열이 너무 설정 되어**의심**합니다. Hello 새로운 데이터베이스에서 DROP 문을 hello 실행과 나중에 다시 시도 합니다.
* Hello 복사 성공 하면 hello **state_desc** hello 새 데이터베이스에 대 한 hello sys.databases 뷰의 열이 너무 설정 되어**온라인**합니다. hello 복사가 완료 되며 hello 새 데이터베이스는 hello 원본 데이터베이스와 독립적으로 변경 될 수 있는 일반 데이터베이스입니다.

> [!NOTE]
> 진행 중인 동안 toocancel hello 복사 기능을 결정 하는 경우 실행 hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) hello 새 데이터베이스에서 문입니다. 또는 hello 복사 프로세스가 취소도 hello 원본 데이터베이스에서 hello DROP DATABASE 문을 실행 합니다.
> 

## <a name="resolve-logins"></a>로그인 확인

Hello를 사용 하 여 새 데이터베이스 hello hello 대상 서버에서 온라인 상태 이면 후 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) hello에서 문을 tooremap hello 사용자는 새 toologins hello 대상 서버의 데이터베이스입니다. tooresolve 분리 된 사용자에 게 표시 [분리 된 사용자 문제 해결](https://msdn.microsoft.com/library/ms175475.aspx)합니다. 참고 항목 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.

Hello 원본 데이터베이스에서 가졌던 hello 사용 권한을 유지 하는 hello 새 데이터베이스의 모든 사용자. hello 데이터베이스 복사본을 시작한 hello 사용자 hello 새 데이터베이스의 데이터베이스 소유자 hello 되며 새 보안 식별자 (SID)를 할당 됩니다. Hello 복사 성공 후 및 다른 사용자가 다시 매핑하기 전에 hello hello 데이터베이스 소유자 hello 복사를 시작한 로그인 로그인 수 toohello 새 데이터베이스.

toolearn 데이터베이스 tooa 다른 논리 서버를 복사할 때 사용자와 로그인을 관리 하는 방법에 대 한 참조 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.

## <a name="next-steps"></a>다음 단계

* 로그인에 대 한 정보를 참조 하십시오. [로그인 관리](sql-database-manage-logins.md) 및 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.
* tooexport 데이터베이스 참조 [hello 데이터베이스 tooa BACPAC 내보내기](sql-database-export.md)합니다.
