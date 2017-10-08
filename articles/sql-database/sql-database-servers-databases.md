---
title: "aaaCreate & SQL Azure 서버 및 데이터베이스 관리 | Microsoft Docs"
description: "만들기 및 Azure SQL 데이터베이스 서버 및 데이터베이스 개념에 대 한 자세한 내용은 및 관리 서버와 데이터베이스를 사용 하 여 hello Azure 포털, PowerShell, hello Azure CLI, TRANSACT-SQL 및 hello REST API입니다."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Azure SQL Database 서버 및 데이터베이스 만들기 및 관리

Azure SQL Database는 [다양한 워크로드에 대한 계산 및 저장소 리소스](sql-database-service-tiers.md)를 정의한 집합을 사용하여 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 내에서 만든 Microsoft Azure의 관리되는 데이터베이스입니다. Azure SQL Database는 Azure SQL Database 논리 서버와 연결되어 있으며 특정 Azure 지역에서 만들어집니다. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Azure SQL Database는 풀되거나 분할된 단일 데이터베이스일 수 있습니다.

Azure SQL Database는 다음과 같을 수 있습니다.

- [고유한 리소스 집합](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus)(DTU)이 있는 단일 데이터베이스
- [리소스 집합을 공유](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus)(eDTU)하는 [SQL 탄력적 풀](sql-database-elastic-pool.md)의 일부
- 일부 [분할 데이터베이스의 확장된 집합](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling)은 단일 또는 풀링된 데이터베이스
- [다중 테넌트 SaaS 디자인 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)에 속한 데이터베이스 집합의 일부 및 해당 데이터베이스는 단일 또는 풀링된 데이터베이스 또는 둘 다일 수 있습니다. 

> [!TIP]
> 유효한 데이터베이스 이름은 [데이터베이스 식별자](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers)를 참조하세요. 
>
 
- hello 기본 데이터베이스 데이터 정렬이 Microsoft Azure SQL 데이터베이스에서 사용 하는 **SQL_LATIN1_GENERAL_CP1_CI_AS**여기서 **LATIN1_GENERAL** 영어 (미국) **CP1** 코드 페이지 1252 **CI** 대/소문자가 및 **AS** 사전이 악센트를 구분 합니다. 어떻게 tooset hello 데이터 정렬에 대 한 자세한 내용은 참조 [COLLATE (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms184391.aspx)합니다.
- Microsoft Azure SQL 데이터베이스는 TDS(Tabular Data Stream) 프로토콜 클라이언트 버전 7.3 이상을 지원합니다.
- TCP/IP 연결만 허용됩니다.

## <a name="what-is-an-azure-sql-logical-server"></a>Azure SQL 논리 서버란?

논리 서버는 [SQL 탄력적 풀](sql-database-elastic-pool.md) [로그인](sql-database-manage-logins.md), [방화벽 규칙](sql-database-firewall-configure.md), [감사 규칙](sql-database-auditing.md), [위협 검색 정책](sql-database-threat-detection.md) 및 [장애 조치 그룹](sql-database-geo-replication-overview.md)을 포함하여 여러 데이터베이스에 대한 중앙 관리 지점의 역할을 담당합니다. 논리 서버는 리소스 그룹과 다른 지역에 위치할 수 있습니다. hello 논리 서버 hello Azure SQL 데이터베이스를 만들려면 먼저 존재 해야 합니다. 서버에 있는 모든 데이터베이스 내에서 만들어집니다 hello 동일한 논리 서버 hello와 지역입니다. 


> [!IMPORTANT]
> SQL 데이터베이스에는 서버는 수에 대해 잘 알고 hello 온-프레미스 환경에서 SQL Server 인스턴스를 구별 되는 논리적 구문입니다. 특히, hello SQL 데이터베이스 서비스 hello 데이터베이스의 위치에 대 한 보장은 없습니다 관계에서 tootheir 논리 서버를 만들고 없는 인스턴스 수준의 액세스 나 기능을 노출 합니다.
> 

논리 서버를 만들 때 로그인 계정 및 암호에 해당 서버에 대 한 관리 권한 toohello master 데이터베이스와 해당 서버에서 생성 된 모든 데이터베이스 서버를 제공 합니다. 이 초기 계정이 SQL 로그인 계정입니다. Azure SQL Database는 인증을 위해 SQL 인증 및 Azure Active Directory 인증을 지원합니다. 로그인 및 인증에 대한 내용은 [Azure SQL Database에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요. Windows 인증은 지원되지 않습니다. 

> [!TIP]
> 유효한 리소스 그룹 및 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.
>

Azure 데이터베이스 논리 서버는 다음과 같습니다.

- Azure 구독 내에서 생성 되지만 해당 포함 된 리소스 tooanother 구독과 이동할 수 있습니다
- 데이터베이스, 탄력적 풀, 및 데이터 웨어하우스에 hello 부모 리소스
- 데이터베이스, 탄력적 풀 및 데이터 웨어하우스의 네임스페이스를 제공합니다.
- 강력한 수명 의미 체계가-하며 서버를 삭제 하는 delete 있는 논리적 컨테이너 hello 포함 된 데이터베이스, 탄력적 풀, 및 데이터 웨어하우스
- 에 참여 [Azure 역할 기반 액세스 제어 (RBAC)](/active-directory/role-based-access-control-what-is) -데이터베이스, 탄력적 풀, 및 데이터 웨어하우스 서버 내에서 액세스 권한을 hello 서버에서 상속
- 데이터베이스, 탄력적 풀 및 Azure 리소스에 대 한 데이터 웨어하우스 hello id의 상위 요소 관리 목적으로 (hello URL 참조 데이터베이스 및 풀에 대 한 구성표)
- 지역에 리소스 배치
- 데이터베이스 액세스에 대한 연결 끝점을 제공합니다(<serverName>.database.windows.net).
- Tooa master 데이터베이스를 연결 하 여 Dmv 통해 포함 된 리소스에 대 한 액세스 toometadata를 제공합니다. 
- Tooits 데이터베이스-로그인 적용, 방화벽, 감사, 검색 등을 위협 하는 관리 정책에 대 한 hello 범위를 제공 합니다. 
- Hello 부모 구독 내에서 할당량으로 제한 됩니다 (기본적으로-는 구독 당 6 대의 서버 [구독 제한 여기 참조](../azure-subscription-service-limits.md))
- (예: 45,000 DTU) 포함 된 hello 리소스에 대 한 데이터베이스 할당량 및 DTU 할당량에 대 한 hello 범위를 제공 합니다.
- 포함 된 리소스에서 사용 하도록 설정 하는 기능에 대 한 hello 버전 관리 범위는 
- 서버 수준 주체 로그인은 서버에 있는 모든 데이터베이스를 관리할 수 있습니다.
- 로그인을 포함할 수 제한 된 관리 권한만 부여 된 액세스 tooone 또는 hello 서버에 데이터베이스를 추가로 허용 되는 수 귀하의 구내 SQL Server 인스턴스에 있는 비슷한 toothose 합니다. 자세한 내용은 [로그인](sql-database-manage-logins.md)을 참조하세요.

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>Azure SQL Database는 SQL Database 방화벽으로 보호됩니다.

toohelp 데이터를 보호 한 [SQL 데이터베이스 방화벽](sql-database-firewall-configure.md) 모든 액세스 tooyour 데이터베이스 서버 또는 Azure 구독 연결을 통해 직접 연결 toohello 서버 외부에서 데이터베이스를 방지 합니다. tooenable 추가 연결을 수행 해야 [하나 이상의 방화벽 규칙을 만들](sql-database-firewall-configure.md#creating-and-managing-firewall-rules)합니다. SQL 탄력적 풀 만들기 및 관리에 대해서는 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Azure SQL 서버, 데이터베이스 그리고 hello Azure 포털을 사용 하는 방화벽 관리

Hello 서버 자체를 만드는 동안 또는 미리 hello Azure SQL 데이터베이스의 리소스 그룹을 만들 수 있습니다. 새 SQL server를 만들어 또는 새 데이터베이스 만들기의 일부로 tooa 새 SQL server 폼을 가져오기 위한는 방법은 여러 가지가 있습니다. 

### <a name="create-a-blank-sql-server-logical-server"></a>비어 있는 SQL Server(논리 서버) 만들기

사용 하 여 Azure SQL 데이터베이스 서버 (데이터베이스) 없음 toocreate hello [Azure 포털](https://portal.azure.com), tooa 빈 SQL server (논리 서버) 양식 이동 합니다. hello 다음 스크린샷은 폼 toocreate를 열기 위한 한 가지 방법은 빈 논리 SQL server. 

   ![논리 서버 만들기 양식 완료](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

다른 방법을 사용 하 여 toothis 형식 발생 하는 경우에 hello 양식의 hello 정보는 동일 합니다.

### <a name="create-a-blank-or-sample-sql-database"></a>비어 있거나 샘플인 SQL Database 만들기

사용 하 여 Azure SQL 데이터베이스 toocreate hello [Azure 포털](https://portal.azure.com)tooa 빈 SQL 데이터베이스 폼을 탐색 하 고, 요청 된 정보를 hello 합니다. Hello Azure SQL 데이터베이스의 리소스 그룹 및 논리 서버 hello 데이터베이스 자체를 만드는 동안 또는 미리 만들 수 있습니다. 비어 있는 데이터베이스를 만들거나 Adventure Works LT에 따라 샘플 데이터베이스를 만들 수 있습니다. 

  ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

> [중요] 가격 책정 계층 데이터베이스에 대 한 hello 선택에 대 한 자세한 내용은 참조 하십시오. [서비스 계층](sql-database-service-tiers.md)합니다.
>

### <a name="manage-an-existing-sql-server"></a>기존 SQL Server 관리

toomanage는 기존 서버를 사용 하 여 다양 한 메서드-특정 SQL 데이터베이스 페이지와 같은 hello toohello 서버 이동 **SQL server** 페이지 또는 hello **모든 리소스** 페이지. 스크린 샷에 표시 방법을 따르는 hello hello에서 서버 수준 방화벽 설정 toobegin **개요** 는 서버에 대 한 페이지입니다. 

   ![논리 서버 개요](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

toomanage 기존 데이터베이스를 이동 toohello **SQL 데이터베이스** 페이지 고 toomanage hello 데이터베이스를 클릭 합니다. 스크린 샷에 표시 방법을 따르는 hello hello에서 데이터베이스에 대 한 서버 수준 방화벽 설정 toobegin **개요** 데이터베이스에 대 한 페이지입니다. 

   ![서버 방화벽 규칙](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> 데이터베이스에 대 한 성능 속성 tooconfigure 참조 [서비스 계층](sql-database-service-tiers.md)합니다.
>

> [!TIP]
> Azure 포털 빠른 시작 자습서를 참조 하십시오. [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](sql-database-get-started-portal.md)합니다.
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>PowerShell을 사용하여 Azure SQL Server, 데이터베이스 및 방화벽 관리

toocreate 및 Azure SQL server, 데이터베이스 및 Azure PowerShell을 사용한 방화벽을 관리, PowerShell cmdlet을 다음 hello를 사용 합니다. PowerShell을 업그레이드 하거나 tooinstall를 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다. SQL 탄력적 풀 만들기 및 관리에 대해서는 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.

| Cmdlet | 설명 |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|데이터베이스 만들기 |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|하나 이상의 데이터베이스 가져오기|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|데이터베이스의 속성 설정 또는 기존 데이터베이스를 탄력적 풀로 이동|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|데이터베이스 제거|
|[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|리소스 그룹 만들기]
|[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|서버 만들기|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|서버에 대한 정보 반환|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|서버의 속성 수정|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|서버 제거|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|서버 수준 방화벽 규칙 만들기 |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|서버의 방화벽 규칙 가져오기|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|서버에서 방화벽 규칙 수정|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|서버에서 방화벽 규칙 삭제|

> [!TIP]
> PowerShell 빠른 시작 자습서는 [PowerShell을 사용하여 단일 Azure SQL Database 만들기](sql-database-get-started-portal.md)를 참조하세요. PowerShell 예제 스크립트를 참조 하십시오. [PowerShell 사용 하 여 toocreate 단일 Azure SQL 데이터베이스 방화벽 규칙을 구성 및](scripts/sql-database-create-and-configure-database-powershell.md) 및 [모니터 및 배율 단일 SQL 데이터베이스 PowerShell을 사용 하 여](scripts/sql-database-monitor-and-scale-database-powershell.md)합니다.
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Azure SQL 서버, 데이터베이스 및 Azure CLI hello를 사용 하는 방화벽 관리

toocreate 및 Azure SQL server, 데이터베이스 및 hello로 방화벽 관리 [Azure CLI](/cli/azure/overview), hello 다음 이름을 사용해 서 [Azure CLI SQL 데이터베이스](/cli/azure/sql/db) 명령입니다. 사용 하 여 hello [클라우드 셸](/azure/cloud-shell/overview) 브라우저에서 toorun hello CLI 또는 [설치](/cli/azure/install-azure-cli) macOS, Linux 또는 Windows에 있습니다. SQL 탄력적 풀 만들기 및 관리에 대해서는 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.

| Cmdlet | 설명 |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |데이터베이스 만들기|
|[az sql db list](/cli/azure/sql/db#list)|서버의 모든 데이터베이스 및 데이터 웨어하우스 또는 탄력적 풀의 모든 데이터베이스 나열|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|사용 가능한 서비스 목표 및 저장소 용량 제한 나열|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|데이터베이스 사용 정보 반환|
|[az sql db show](/cli/azure/sql/db#show)|데이터베이스 또는 데이터 웨어하우스 가져오기|
|[az sql db update](/cli/azure/sql/db#update)|데이터베이스 업데이트|
|[az sql db delete](/cli/azure/sql/db#delete)|데이터베이스 제거|
|[az group create](/cli/azure/group#create)|리소스 그룹 만들기|
|[az sql server create](/cli/azure/sql/server#create)|서버 만들기|
|[az sql server list](/cli/azure/sql/server#list)|서버 나열|
|[az sql server list-usages](/cli/azure/sql/server#list-usages)|서버 사용 반환|
|[az sql server show](/cli/azure/sql/server#show)|서버 가져오기|
|[az sql server update](/cli/azure/sql/server#update)|서버 업데이트|
|[az sql server delete](/cli/azure/sql/server#delete)|서버를 삭제합니다.|
|[az sql server firewall-rule create](/cli/azure/sql/server/firewall-rule#create)|서버 방화벽 규칙 만들기|
|[az sql server firewall-rule list](/cli/azure/sql/server/firewall-rule#list)|서버 hello 방화벽 규칙을 나열합니다.|
|[az sql server firewall-rule show](/cli/azure/sql/server/firewall-rule#show)|방화벽 규칙의 hello 세부 정보를 보여 줍니다.|
|[az sql server firewall-rule update](/cli/azure/sql/server/firewall-rule#update)|방화벽 규칙 업데이트|
|[az sql server firewall-rule delete](/cli/azure/sql/server/firewall-rule#delete)|방화벽 규칙 삭제|

> [!TIP]
> Azure CLI 빠른 시작 자습서를 참조 하십시오. [hello Azure CLI를 사용 하 여 단일 Azure SQL 데이터베이스 만들기](sql-database-get-started-cli.md)합니다. Azure CLI 예제 스크립트에 대 한 참조 [사용 CLI toocreate 단일 Azure SQL 데이터베이스 방화벽 규칙을 구성 및](scripts/sql-database-create-and-configure-database-cli.md) 및 [사용 CLI toomonitor 및 소수 자릿수는 단일 SQL 데이터베이스](scripts/sql-database-monitor-and-scale-database-cli.md)합니다.
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Transact-SQL을 사용하여 Azure SQL Server, 데이터베이스 및 방화벽 관리

toocreate 및 Azure SQL server, 데이터베이스 및 Transact sql 방화벽을 관리, T-SQL 명령을 수행 하는 hello를 사용 합니다. Hello Azure 포털을 사용 하 여 이러한 명령을 실행할 수 있습니다 [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), 또는 tooan Azure SQL 데이터베이스 서버를 연결 하 고 TRANSACT-SQL 전달할 수 있는 다른 프로그램 명령입니다. SQL 탄력적 관리에 대해서는 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.

> [!IMPORTANT]
> Transact-SQL을 사용하여 서버를 만들거나 삭제할 수 없습니다.
>

| 명령 | 설명 |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|새 데이터베이스를 만듭니다. 연결 된 toohello master 데이터베이스 toocreate 새 데이터베이스 여야 합니다.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Azure SQL 데이터베이스를 수정합니다. |
|[ALTER DATABASE(Azure SQL Data Warehouse)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Azure SQL Data Warehouse를 수정합니다.|
|[DROP DATABASE(Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|데이터베이스를 삭제합니다.|
|[sys.database_service_objectives(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에 대 한 반환 hello edition (서비스 계층), (가격 책정 계층), 서비스 목표 및 탄력적인 풀 이름입니다. Azure SQL 데이터베이스 서버에서 toohello master 데이터베이스에 로그온 하는 경우 모든 데이터베이스에서 정보를 반환 합니다. Azure SQL 데이터 웨어하우스에 대 한 연결 된 toohello master 데이터베이스 여야 합니다.|
|[sys.dm_db_resource_stats(Azure SQL Database)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Azure SQL Database 데이터베이스에 대한 CPU, I/O 및 메모리 소비량을 반환합니다. Hello 데이터베이스에 작업이 수행 되지 않은 경우에 15 초 마다 한 행이 있습니다.|
|[sys.resource_stats(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Azure SQL Database에 대한 CPU 사용량 및 저장소 데이터를 반환합니다. hello 데이터 수집 되 고 5 분 간격 내에서 집계 됩니다.|
|[sys.database_connection_stats(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|SQL Database 데이터베이스 연결 이벤트에 대한 통계를 포함하며 데이터베이스 연결 성공 및 실패에 대한 개요를 제공합니다. |
|[sys.event_log(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|성공적인 Azure SQL Database 데이터베이스 연결, 연결 실패 및 교착 상태를 반환합니다. 이 정보 tootrack를 사용 하거나 SQL 데이터베이스와 데이터베이스 작업 문제 해결 수 있습니다.|
|[sp_set_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|만들거나 SQL 데이터베이스 서버에 대 한 hello 서버 수준 방화벽 설정을 업데이트 합니다. 이 저장된 프로시저는 hello master 데이터베이스 toohello 서버 수준 보안 주체 로그인에 사용할 수만 있습니다. 서버 수준 방화벽 규칙을 다시 만들 hello 첫 번째 서버 수준 방화벽 규칙이 Azure 수준 사용 권한 가진 사용자가 만들어진 후 TRANSACT-SQL을 사용 하 여|
|[sys.firewall_rules(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Microsoft Azure SQL 데이터베이스와 관련 된 hello 서버 수준 방화벽 설정에 대 한 정보를 반환 합니다.|
|[sp_delete_firewall_rule(Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|SQL Database 서버에서 서버 수준 방화벽 설정을 제거합니다. 이 저장된 프로시저는 hello master 데이터베이스 toohello 서버 수준 보안 주체 로그인에 사용할 수만 있습니다.|
|[sp_set_database_firewall_rule(Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|만들거나 Azure SQL 데이터베이스 또는 SQL 데이터 웨어하우스에 대 한 hello 데이터베이스 수준 방화벽 규칙을 업데이트 합니다. SQL 데이터베이스에서 사용자 데이터베이스와 hello master 데이터베이스에 대해 데이터베이스 방화벽 규칙을 구성할 수 있습니다. 데이터베이스 방화벽 규칙은 포함된 데이터베이스 사용자를 사용하는 경우에 유용합니다. |
|[sys.database_firewall_rules(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Microsoft Azure SQL 데이터베이스와 관련 된 hello 데이터베이스 수준 방화벽 설정에 대 한 정보를 반환 합니다. |
|[sp_delete_database_firewall_rule(Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Azure SQL Database 또는 SQL Data Warehouse에서 데이터베이스 수준 방화벽 설정을 제거합니다. |


> [!TIP]
> Microsoft Windows에서 SQL Server Management Studio를 사용 하 여 빠른 시작 자습서를 참조 하십시오. [Azure SQL 데이터베이스: SQL Server Management Studio를 사용 하 여 tooconnect 및 쿼리 데이터](sql-database-connect-query-ssms.md)합니다. Visual Studio 코드를 사용 하 여 hello macOS, Linux 또는 Windows에는 빠른 시작 자습서를 참조 하십시오. [Azure SQL 데이터베이스: 사용 가능한 Visual Studio 코드 tooconnect 및 쿼리 데이터](sql-database-connect-query-vscode.md)합니다.

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Azure SQL 서버, 데이터베이스 그리고 hello REST API를 사용 하는 방화벽 관리

toocreate 및 Azure SQL server, 데이터베이스 및 hello REST API를 사용 하 여 방화벽을 관리, 참조 [Azure SQL 데이터베이스 REST API](/rest/api/sql/)합니다.

## <a name="next-steps"></a>다음 단계

- SQL 탄력적인 풀을 사용 하 여 데이터베이스를 풀링 하는 방법에 대 한 toolearn 참조 [탄력적 풀](sql-database-elastic-pool.md)합니다.
- Azure SQL 데이터베이스 서비스 hello에 대 한 정보를 참조 하십시오. [SQL 데이터베이스 란?](sql-database-technical-overview.md)합니다.
- SQL Server 데이터베이스 tooAzure 마이그레이션에 대 한 toolearn 참조 [tooAzure SQL 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다.
- 지원되는 기능에 대한 자세한 내용은 [기능](sql-database-features.md)을 참조하세요.
