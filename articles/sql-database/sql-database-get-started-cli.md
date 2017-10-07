---
title: "Azure CLI: SQL Database 만들기 | Microsoft Docs"
description: "어떻게 toocreate SQL 데이터베이스 논리 서버, 서버 수준 방화벽 규칙 및 데이터베이스를 사용 하 여 hello Azure CLI에 알아봅니다."
keywords: "SQL 데이터베이스 자습서, SQL 데이터베이스 만들기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 단일 Azure SQL 데이터베이스 만들기

hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. 이 가이드 hello Azure CLI toodeploy를 사용 하 여 정보에 Azure SQL 데이터베이스는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 에 [Azure SQL 데이터베이스 논리 서버](sql-database-features.md)합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

이 항목 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="define-variables"></a>변수 정의

이 빠른 시작의 hello 스크립트에서 사용할 변수를 정의 합니다.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

만들기는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello를 사용 하 여 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. 리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westeurope` 위치 합니다.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>논리 서버 만들기

만들기는 [Azure SQL 데이터베이스 논리 서버](sql-database-features.md) hello를 사용 하 여 [az sql server 만들](/cli/azure/sql/server#create) 명령입니다. 논리 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다. hello 다음 예제에서는 만듭니다 임의로 지정 된 서버 리소스 그룹에 라는 관리자 로그인과 `ServerAdmin` 이 고 암호가 `ChangeYourAdminPassword1`합니다. 이러한 미리 정의된 값은 필요에 따라 바꿉니다.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>서버 방화벽 규칙 구성

만들기는 [Azure SQL 데이터베이스 서버 수준 방화벽 규칙](sql-database-firewall-configure.md) hello를 사용 하 여 [az sql server 방화벽 만들](/cli/azure/sql/server/firewall-rule#create) 명령입니다. 서버 수준 방화벽 규칙에는 SQL Server Management Studio 또는 hello SQLCMD 유틸리티 tooconnect tooa SQL 데이터베이스 같은 hello SQL 데이터베이스 서비스 방화벽을 통해 외부 응용을 프로그램 수 있습니다. 다음 예제는 hello,에서는 hello 방화벽은 다른 Azure 리소스에 대 한 열만. tooenable 외부 연결을 변경 hello IP 주소 tooan 사용자 환경에 대 한 적절 한 주소입니다. tooopen 모든 IP 주소를 IP 주소와 255.255.255.255 끝 주소 hello로 시작 하는 hello로 0.0.0.0를 사용 합니다.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Database는 포트 1433을 통해 통신합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우 됩니다 수 tooconnect tooyour Azure SQL 데이터베이스 서버 않으면 IT 부서는 포트 1433을 엽니다.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>샘플 데이터로 hello 서버에서 데이터베이스 만들기

사용 하 여 데이터베이스를 만들기는 [S0 성능 수준이](sql-database-service-tiers.md) hello를 사용 하 여 hello 서버에서 [az sql db 만들기](/cli/azure/sql/db#create) 명령입니다. hello 다음 예에서는 라는 데이터베이스를 만드는 `mySampleDatabase` 로드 AdventureWorksLT 샘플 데이터를이 데이터베이스에 hello 및 합니다. 이러한 미리 정의 된 대체 값 (hello 값이 빠른 시작에서에이 컬렉션 빌드에서 다른 빠른 시작)이 원하는 대로 합니다.

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>리소스 정리

이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 합니다. 

> [!TIP]
> 후속 빠른 시작으로 toowork toocontinue 하려는 경우이 빠른에서 만든 hello 리소스를 정리 실행할 수 없습니다. Toocontinue 않으려는 경우 모든 리소스를 만들 단계 toodelete hello Azure 포털에서에서이 빠른 시작에서 다음 hello를 사용 합니다.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>다음 단계

이제 데이터베이스가 생겼으니 자주 사용하는 도구를 사용하여 데이터베이스에 연결하고 쿼리할 수 있습니다. 아래에서 도구를 선택하여 자세한 내용을 알아보세요.

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Contact.java](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.JS](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

