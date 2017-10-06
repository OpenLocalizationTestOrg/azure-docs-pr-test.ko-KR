---
title: "aaaAzure SQL 데이터베이스 방화벽 규칙 | Microsoft Docs"
description: "Tooconfigure SQL 데이터베이스 서버 수준 및 데이터베이스 수준 방화벽 규칙 toomanage 액세스할 수 있는 방화벽에 알아봅니다."
keywords: "데이터베이스 방화벽"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 

Microsoft Azure SQL Database는 Azure 및 기타 인터넷 기반 응용 프로그램의 관계형 데이터베이스 서비스를 제공합니다. toohelp 데이터 보호, 방화벽 권한이 있는 컴퓨터를 지정할 때까지 모든 액세스 tooyour 데이터베이스 서버를 차단 합니다. hello 방화벽 액세스 toodatabases hello 시작 IP 주소를 각 요청에 따라 권한을 부여 합니다.

## <a name="overview"></a>개요

처음에 모든 TRANSACT-SQL tooyour Azure의 SQL server 액세스 hello 방화벽으로 차단 됩니다. Azure SQL server를 사용 하 여 toobegin tooyour Azure SQL server 액세스를 사용할 수 있는 하나 이상의 서버 수준 방화벽 규칙을 지정 해야 합니다. 방화벽 규칙 toospecify hello를 사용 하 여 인터넷 허용 hello에서 어떤 IP 주소 범위 및 Azure 응용 프로그램 tooconnect tooyour Azure SQL server를 시작할 수 있는지 여부.

hello Azure SQL server 데이터베이스 중 하나 tooselectively grant 액세스 toojust, hello 필요한 데이터베이스에 대 한 데이터베이스 수준 규칙을 만들어야 합니다. IP 주소 hello 서버 수준 방화벽 규칙에 지정 된 범위 및 hello 클라이언트의 IP 주소 hello hello 데이터베이스 수준 규칙에 지정 된 hello 범위에 속하는지 확인 hello 벗어납니다 hello 데이터베이스 방화벽 규칙에 대 한 IP 주소 범위를 지정 합니다.

연결 시도 hello 인터넷 및 Azure 통과 해야 hello 방화벽을 통해 Azure SQL server 또는 SQL 데이터베이스에 영향을 미칠 수 전에 hello 다음 다이어그램에에서 나와 있는 것 처럼:

   ![방화벽 구성을 설명하는 다이어그램입니다.][1]

* **서버 수준 방화벽 규칙:** 이러한 규칙을 통해 클라이언트 tooaccess 전체 Azure SQL server, 즉, 모든 hello 데이터베이스 내에서 hello 동일한 논리 서버입니다. 이러한 규칙은 hello **마스터** 데이터베이스입니다. Hello 포털을 사용 하 여 또는 TRANSACT-SQL 문을 사용 하 여 서버 수준 방화벽 규칙을 구성할 수 있습니다. toocreate 서버 수준 방화벽 규칙 hello Azure 포털 또는 PowerShell을 사용 하 여 hello 구독 소유자 또는 구독 참가자 여야 합니다. TRANSACT-SQL을 사용 하 여 서버 수준 방화벽 규칙 toocreate hello 서버 수준 보안 주체 로그인 또는 hello Azure Active Directory 관리자 (즉, 서버 수준 방화벽 규칙을 먼저 만들어야 함을 toohello SQL 데이터베이스 인스턴스 연결 해야 합니다. 사용자가 Azure 수준 권한).
* **데이터베이스 수준 방화벽 규칙:** 이러한 규칙을 통해 클라이언트 tooaccess 특정 (보안) 데이터베이스 hello 내에서 동일한 논리 서버입니다. 각 데이터베이스에 대 한 이러한 규칙을 만들 수 있습니다 (hello를 포함 하 여 **마스터** database0) hello 개별 데이터베이스에 저장 됩니다. 데이터베이스 수준 방화벽 규칙 TRANSACT-SQL 문을 사용 하 여 구성할 수 있습니다 및 구성한 후에 첫 번째 서버 수준 방화벽 hello 합니다. Hello 서버 수준 방화벽 규칙에 지정 된 외부 hello 범위는 hello 데이터베이스 수준 방화벽 규칙의 IP 주소 범위를 지정 하는 경우 hello 데이터베이스 수준 범위의 IP 주소를가지고 있는 클라이언트에만 hello 데이터베이스에 액세스할 수 있습니다. 데이터베이스에 대해 최대 128개의 데이터베이스 수준 방화벽 규칙을 가질 수 있습니다. master 및 사용자 데이터베이스에 대한 데이터베이스 수준 방화벽 규칙은 Transact-SQL을 통해서만 만들고 관리할 수 있습니다. 데이터베이스 수준 방화벽 규칙 구성에 대 한 자세한 내용은 뒷부분에서는이 문서와 참조 hello 예제를 참조 하십시오. [sp_set_database_firewall_rule (Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/dn270010.aspx)합니다.

**권장 사항:** 데이터베이스 수준 방화벽 규칙을 사용 하는 것이 좋습니다 때마다 가능한 tooenhance 보안과 toomake 데이터베이스 이식성이 향상 됩니다. 관리자에 대 한 서버 수준 방화벽 규칙을 사용 하 여 및 hello가 많은 데이터베이스가 있는 경우 같은 액세스 요구 사항을 않게 toospend 시간 각 데이터베이스를 개별적으로 구성 합니다.

> [!Note]
> 비즈니스 연속성의 hello 컨텍스트에서 이식 가능한 데이터베이스에 대 한 정보를 참조 하십시오. [재해 복구를 위한 인증 요구 사항](sql-database-geo-replication-security-config.md)합니다.
>

### <a name="connecting-from-hello-internet"></a>Hello 인터넷에서 연결

Hello 인터넷에서에서 tooconnect tooyour 데이터베이스 서버를 시도 하는 컴퓨터 hello 방화벽 시작 IP 주소를 hello 연결을 요청 하는 hello 데이터베이스에 대 한 hello 데이터베이스 수준 방화벽 규칙에 대해 hello 요청의 hello를 먼저 확인 합니다.

* Hello 요청의 hello IP 주소 내 hello 데이터베이스 수준 방화벽 규칙에 지정 된 hello 범위 중 하나에 있으면 hello 연결 toohello hello 규칙을 포함 하는 SQL 데이터베이스 권한이 부여 됩니다.
* Hello 요청의 hello IP 주소 hello 데이터베이스 수준 방화벽 규칙에 지정 된 hello 범위 중 하나에 없으면 hello 서버 수준 방화벽 규칙이 확인 됩니다. Hello 요청의 hello IP 주소 중 한 hello 서버 수준 방화벽 규칙에 지정 된 hello 범위 내에 있으면 hello 연결이 승인 됩니다. 서버 수준 방화벽 규칙은 tooall SQL 데이터베이스 hello Azure SQL server에 적용 됩니다.  
* 내에 없으면 hello 요청의 hello IP 주소 hello 데이터베이스 수준 중 하나에 지정 된 hello 범위 또는 서버 수준 방화벽 규칙의 경우, hello 연결 요청이 실패 합니다.

> [!NOTE]
> 로컬 컴퓨터에서 Azure SQL 데이터베이스 tooaccess 확인 hello 방화벽 네트워크와 로컬 컴퓨터에서 TCP 포트 1433에서 나가는 통신을 허용 합니다.
> 

### <a name="connecting-from-azure"></a>Azure에서 연결
Azure tooconnect tooyour Azure SQL server, Azure 연결이에서 tooallow 응용 프로그램을 사용 하도록 설정 합니다. Azure에서 응용 프로그램 tooconnect tooyour 데이터베이스 서버와 시도 hello 방화벽 Azure 연결이 허용 되는지 확인 합니다. 방화벽 설정에서 시작 주소와 끝 주소와 같으면 too0.0.0.0 허용 되는 이러한 연결을 나타냅니다. Hello 연결 시도가 허용 되지 않는 경우 hello 요청 hello Azure SQL 데이터베이스 서버에 도달 하지 않습니다.

> [!IMPORTANT]
> 이 옵션 hello 방화벽 tooallow 다른 고객의 hello 구독에서 Azure 포함 하 여 연결에서 모든 연결을 구성합니다. 권한 있는 사용자 때이 옵션을 선택 하면 있는지 확인 하 여 로그인 하 고 사용자 권한을 tooonly 액세스를 제한 합니다.
> 

## <a name="creating-and-managing-firewall-rules"></a>방화벽 규칙 만들기 및 관리
hello를 사용 하 여 hello 첫 번째 서버 수준 방화벽 설정을 만들 수 있습니다 [Azure 포털](https://portal.azure.com/) 프로그래밍 방식으로 사용 하 여 [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [Azure CLI](/cli/azure/sql/server/firewall-rule#create), 또는 hello [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx)합니다. 후속 서버 수준 방화벽 규칙은 이러한 방법과 Transact-SQL을 사용하여 만들고 관리 할 수 있습니다. 

> [!IMPORTANT]
> 데이터베이스 수준 방화벽 규칙은 Transact-SQL을 사용해야만 만들고 관리할 수 있습니다. 
>

tooimprove 성능, 서버 수준 방화벽 규칙 hello 데이터베이스 수준에서 일시적으로 캐시 됩니다. toorefresh hello 캐시 참조 [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx)합니다. 

> [!TIP]
> 사용할 수 있습니다 [SQL 데이터베이스 감사](sql-database-auditing.md) tooaudit 서버 수준과 데이터베이스 수준의 방화벽 변경 내용이 있습니다.
>

### <a name="azure-portal"></a>Azure portal

tooset hello Azure 포털에서에서 서버 수준 방화벽 규칙을 이동할 수 있습니다 하거나 toohello 개요 페이지 Azure SQL 데이터베이스 또는 hello 개요 페이지에 대 한 Azure 데이터베이스 논리 서버에 대 한 합니다.

> [!TIP]
> 자습서를 참조 하십시오. [만들기는 DB를 사용 하 여 Azure 포털을 hello](sql-database-get-started-portal.md)합니다.
>

**데이터베이스 개요 페이지에서**

1. hello 데이터베이스 개요 페이지에서 서버 수준 방화벽 규칙 tooset 클릭 **서버 방화벽 설정** hello 다음 이미지와 같이 hello 도구 모음에서: hello **방화벽 설정** SQL hello에 대 한 페이지 데이터베이스 서버를 엽니다.

      ![서버 방화벽 규칙](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. 클릭 **클라이언트 IP 추가** hello 컴퓨터의 hello 도구 모음 tooadd hello IP 주소에 현재 사용 하 고이 클릭 한 다음 **저장**합니다. 현재 IP 주소에 대한 서버 수준 방화벽 규칙이 생성됩니다.

      ![set server firewall rule](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**서버 개요 페이지에서**

hello 완벽 하 게 hello 보여 주는 서버 열리면 프로그램에 대 한 개요 페이지에 정규화 된 서버 이름 (예: **mynewserver20170403.database.windows.net**) 하 고 더 이상의 구성에 대 한 옵션을 제공 합니다.

1. 서버 개요 페이지에서 서버 수준 규칙 tooset 클릭 **방화벽** hello hello 다음 이미지에에서 표시 된 대로 설정에서 왼쪽 메뉴에서: 

     ![논리 서버 개요](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. 클릭 **클라이언트 IP 추가** hello 컴퓨터의 hello 도구 모음 tooadd hello IP 주소에 현재 사용 하 고이 클릭 한 다음 **저장**합니다. 현재 IP 주소에 대한 서버 수준 방화벽 규칙이 생성됩니다.

     ![set server firewall rule](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| 카탈로그 뷰 또는 저장된 프로시저 | 수준 | 설명 |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |서버 |Hello 현재 서버 수준 방화벽 규칙을 표시합니다. |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |서버 |서버 수준 방화벽 규칙 생성 및 업데이트 |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |서버 |서버 수준 방화벽 규칙 제거 |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |데이터베이스 |Hello 현재 데이터베이스 수준 방화벽 규칙을 표시합니다. |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |데이터베이스 |만들거나 hello 데이터베이스 수준 방화벽 규칙을 업데이트 합니다. |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |데이터베이스 |데이터베이스 수준 방화벽 규칙 제거 |


hello 다음 예제에서는 hello 기존 규칙을 검토, Contoso, hello 서버의 IP 주소를 사용 하도록 설정 및 방화벽 규칙을 삭제 합니다.
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
그런 다음 방화벽 규칙을 추가합니다.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

서버 수준 방화벽 규칙을 toodelete hello sp_delete_firewall_rule 저장 프로시저를 실행 합니다. hello 다음 예에서는 삭제 contosofirewallrule hello 규칙:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | 수준 | 설명 |
| --- | --- | --- |
| [AzureSqlDatabaseServerFirewallRule가져오기](https://msdn.microsoft.com/library/azure/dn546731.aspx) |서버 |Hello 현재 서버 수준 방화벽 규칙을 반환합니다. |
| [신규 AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |서버 |새 서버 수준 방화벽 규칙 만들기 |
| [AzureSqlDatabaseServerFirewallRule집합](https://msdn.microsoft.com/library/azure/dn546739.aspx) |서버 |기존 서버 수준 방화벽 규칙의 hello 속성 업데이트 |
| [AzureSqlDatabaseServerFirewallRule삭제](https://msdn.microsoft.com/library/azure/dn546727.aspx) |서버 |서버 수준 방화벽 규칙 제거 |


다음 예제는 hello PowerShell을 사용 하는 서버 수준 방화벽 규칙을 설정 합니다.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> 빠른 시작의 hello 컨텍스트에서 PowerShell 예제를 보려면 [DB 만들기-PowerShell](sql-database-get-started-powershell.md) 및 [단일 데이터베이스를 만들고 PowerShell을 사용 하는 방화벽 규칙 구성](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>Azure CLI
| Cmdlet | 수준 | 설명 |
| --- | --- | --- |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) | Hello 입력 한 IP 주소 범위에서 hello 서버의 방화벽 규칙 tooallow 액세스 tooall SQL 데이터베이스를 만듭니다.|
| [az sql server firewall delete](/cli/azure/sql/server/firewall-rule#delete)| 방화벽 규칙을 삭제합니다.|
| [az sql server firewall list](/cli/azure/sql/server/firewall-rule#list)| Hello 방화벽 규칙을 나열합니다.|
| [az sql server firewall rule show](/cli/azure/sql/server/firewall-rule#show)| 방화벽 규칙의 hello 세부 정보를 표시 합니다.|
| [ax sql server firewall rule update](/cli/azure/sql/server/firewall-rule#update)| 방화벽 규칙을 업데이트합니다.

다음 예제는 hello hello Azure CLI를 사용 하 여 서버 수준 방화벽 규칙을 설정 합니다. 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> 빠른 시작의 hello 컨텍스트에서 Azure CLI 예제를 보려면 [DDB 만들기-Azure CLI](sql-database-get-started-cli.md) 및 [단일 데이터베이스를 만들고 hello Azure CLI를 사용 하는 방화벽 규칙 구성](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>REST API
| API | 수준 | 설명 |
| --- | --- | --- |
| [방화벽 규칙 나열](https://msdn.microsoft.com/library/azure/dn505715.aspx) |서버 |Hello 현재 서버 수준 방화벽 규칙을 표시합니다. |
| [방화벽 규칙 만들기](https://msdn.microsoft.com/library/azure/dn505712.aspx) |서버 |서버 수준 방화벽 규칙 생성 및 업데이트 |
| [방화벽 규칙 설정](https://msdn.microsoft.com/library/azure/dn505707.aspx) |서버 |기존 서버 수준 방화벽 규칙의 hello 속성 업데이트 |
| [방화벽 규칙 삭제](https://msdn.microsoft.com/library/azure/dn505706.aspx) |서버 |서버 수준 방화벽 규칙 제거 |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>서버 수준 방화벽 규칙 및 데이터베이스 수준 방화벽 규칙
Q. 한 데이터베이스의 사용자가 다른 데이터베이스에서 완전히 분리되어야 하나요?   
  그렇다면 데이터베이스 수준 방화벽 규칙을 사용하여 액세스 권한을 부여하세요. 이렇게 하면 데이터베이스 tooall 여 방어의 hello 깊이 줄여 hello 방화벽을 통해 액세스를 허용 하는 서버 수준 방화벽 규칙을 사용 하 여 없습니다.   
 
Q. Hello IP 주소에서 사용자가 필요에 액세스 하려면 tooall 데이터베이스?   
  사용 하 여 서버 수준 방화벽 규칙 tooreduce hello 횟수 방화벽 규칙을 구성 해야 합니다.   

Q. Hello 개인 이나 팀만 hello 방화벽 규칙 구성 액세스 권한이 통해 hello Azure 포털, PowerShell 또는 REST API hello?   
  서버 수준 방화벽 규칙을 사용해야 합니다. 데이터베이스 수준 방화벽 규칙은 Transact-SQL을 사용해야만 구성할 수 있습니다.  

Q. hello 개인 이나 팀 hello 방화벽 규칙 구성 금지 hello 데이터베이스 수준에서 수 있는 높은 수준의 권한을 가진에서?   
  서버 수준 방화벽 규칙을 사용하세요. TRANSACT-SQL을 사용 하 여 데이터베이스 수준 방화벽 규칙을 구성 하려면 최소한 `CONTROL DATABASE` hello 데이터베이스 수준에서 권한이 있습니다.  

Q. 대부분에 대 한 방화벽 규칙을 중앙에서 관리는 hello 개인 이나 팀 구성 또는 hello 방화벽 규칙, 감사 (아마도 단위: 100) 데이터베이스의?   
  이 선택은 사용자의 필요 및 환경에 따라 달라집니다. 서버 수준 방화벽 규칙 보다 쉽게 tooconfigure 있지만 스크립팅 hello 데이터베이스 수준에서 규칙을 구성할 수 있습니다. 경우 tooaudit hello 데이터베이스 방화벽 규칙을 toosee 서버 수준 방화벽 규칙을 사용 하는 경우에 할 수 있습니다 및 있는 사용자 `CONTROL` hello 데이터베이스에 대 한 권한이 데이터베이스 수준 방화벽 규칙을 만들었습니다.   

Q. 서버 수준 및 데이터베이스 수준 방화벽 규칙을 함께 사용할 수 있나요?   
  예. 관리자와 같은 일부 사용자는 서버 수준 방화벽 규칙이 필요할 수 있습니다. 데이터베이스 응용 프로그램 사용자와 같은 경우는 데이터베이스 수준 방화벽 규칙이 필요할 수 있습니다.   

## <a name="troubleshooting-hello-database-firewall"></a>Hello 데이터베이스 방화벽 문제 해결
Hello 포인트 액세스 toohello Microsoft Azure SQL 데이터베이스 서비스에는 예상 대로 작동 하지 않는 경우 다음을 고려 합니다.

* **로컬 방화벽 구성:** TCP 포트 1433에 대 한 컴퓨터에 방화벽 예외를 toocreate 컴퓨터에서 Azure SQL 데이터베이스에 액세스 하기 전에 할 수 있습니다. Hello Azure 클라우드 경계 내에서 연결 작업을 수행 하려면 tooopen 추가 포트를 할 수 있습니다. 자세한 내용은 참조 hello **SQL 데이터베이스: 내부 및 외부** 의 섹션 [ADO.NET 4.5 및 SQL 데이터베이스에 대 한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)합니다.
* **네트워크 주소 변환 (NAT):** 기한 tooNAT, hello IP 주소에서 사용자 컴퓨터 tooconnect tooAzure SQL 데이터베이스 컴퓨터의 IP 구성 설정에 표시 된 hello IP 주소와 다를 수 있습니다. 컴퓨터가 tooview hello IP 주소 toohello 포털에 로그인 하 고 toohello 이동 tooconnect tooAzure를 사용 하 여 **구성** hello 서버 데이터베이스를 호스팅하는 탭 합니다. Hello에서 **허용 IP 주소** 섹션 hello **현재 클라이언트 IP 주소** 표시 됩니다. 클릭 **추가** toohello **허용 IP 주소** tooallow이 컴퓨터 tooaccess hello 서버입니다.
* **변경 내용을 toohello 허용 목록이 아직 적용 되지 않음:** 하는 데 5 분 지연 toohello Azure SQL 데이터베이스 방화벽 구성 tootake 효과 변경 하는 만큼 있을 수 있습니다.
* **hello 로그인 권한이 없거나 잘못 된 암호를 사용한:** hello Azure SQL 데이터베이스 서버에 대 한 사용 권한이 로그인 하지 않거나 사용 되는 hello 암호가 올바르지 않습니다, toohello Azure SQL 데이터베이스 서버에 연결할 hello 거부 되었습니다. Tooyour 서버;에 연결 하는 기회 tooattempt 클라이언트 제공 방화벽 설정 각 클라이언트 hello 필요한 보안 자격 증명을 제공 해야 합니다. 로그인 준비에 대한 자세한 내용은 Azure SQL Database에서 데이터베이스, 로그인, 사용자 관리를 참조하세요. 
* **동적 IP 주소:** 동적 IP 주소로 사용 하는 인터넷 연결이 있는 hello 방화벽을 통과 하는 데 문제가 있는 경우 hello 솔루션을 다음 중 하나를 시도할 수 있습니다.
  
  * 인터넷 서비스 공급자 (ISP) hello IP 주소 범위에 대 한 할당 tooyour 클라이언트 컴퓨터 액세스 hello Azure SQL 데이터베이스 서버를 게 문의 하 고 방화벽 규칙으로 hello IP 주소 범위를 추가 합니다.
  * 고정 IP 주소를 대신 클라이언트 컴퓨터에 대 한 가져오고 방화벽 규칙으로 hello IP 주소를 추가 합니다.

## <a name="next-steps"></a>다음 단계

- 데이터베이스 및 서버 수준 방화벽 규칙 만들기에 대한 빠른 시작은 [Azure SQL Database 만들기](sql-database-get-started-portal.md)를 참조하세요.
- 오픈 소스 또는 타사 응용 프로그램에서 연결 tooan Azure SQL 데이터베이스에서 도움말을 참조 하십시오. [클라이언트 빠른 시작 코드 샘플 데이터베이스 tooSQL](https://msdn.microsoft.com/library/azure/ee336282.aspx)합니다.
- 추가 포트를 tooopen 할 수 있습니다, 참조 hello **SQL 데이터베이스: 내부 및 외부** 의 섹션 [ADO.NET 4.5 및 SQL 데이터베이스에 대 한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)
- Azure SQL Database 보안 개요는 [데이터베이스 보안 설정](sql-database-security-overview.md)을 참조하세요.

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
