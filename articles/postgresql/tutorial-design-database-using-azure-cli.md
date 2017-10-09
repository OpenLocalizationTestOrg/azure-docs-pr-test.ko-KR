---
title: "Azure CLI를 사용하여 첫 번째 Azure Database for PostgreSQL 디자인 | Microsoft Docs"
description: "이 자습서에서는 Azure CLI를 사용 하 여 tooDesign 첫 번째 Azure 데이터베이스에 대 한 PostgreSQL 보여 줍니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="5ce33-103">Azure CLI를 사용하여 Azure Database for PostgreSQL을 디자인합니다</span><span class="sxs-lookup"><span data-stu-id="5ce33-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="5ce33-104">이 자습서를 사용 하 여 Azure CLI (명령줄 인터페이스) 및 기타 유틸리티 toolearn 어떻게에:</span><span class="sxs-lookup"><span data-stu-id="5ce33-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="5ce33-105">PostgreSQL용 Azure Database 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce33-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="5ce33-106">Hello 서버 방화벽을 구성</span><span class="sxs-lookup"><span data-stu-id="5ce33-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="5ce33-107">사용 하 여 [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티 toocreate 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="5ce33-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="5ce33-108">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="5ce33-108">Load sample data</span></span>
> * <span data-ttu-id="5ce33-109">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="5ce33-109">Query data</span></span>
> * <span data-ttu-id="5ce33-110">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ce33-110">Update data</span></span>
> * <span data-ttu-id="5ce33-111">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="5ce33-111">Restore data</span></span>

<span data-ttu-id="5ce33-112">Hello 브라우저에서 Azure 클라우드 셸 hello를 사용할 수 있습니다 또는 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli) 이 자습서에서 자신의 컴퓨터 toorun hello 코드 블록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5ce33-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5ce33-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5ce33-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="5ce33-116">여러 구독이 있는 경우 hello 리소스 존재 하거나에 대 한 청구 hello 적절 한 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="5ce33-117">[az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="5ce33-118">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce33-118">Create a resource group</span></span>
<span data-ttu-id="5ce33-119">만들기는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello를 사용 하 여 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5ce33-120">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="5ce33-121">hello 다음 예제에서는 명명 된 리소스 그룹 `myresourcegroup` hello에 `westus` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="5ce33-122">PostgreSQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce33-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="5ce33-123">만들기는 [PostgreSQL 서버에 대 한 Azure 데이터베이스](overview.md) hello를 사용 하 여 [az postgres 서버 만들](/cli/azure/postgres/server#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="5ce33-124">서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="5ce33-125">hello 다음 예제에서는 라고 하는 서버 `mypgserver-20170401` 리소스 그룹에서 `myresourcegroup` 서버 관리자 로그인과 `mylogin`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="5ce33-126">서버 이름을 tooDNS 이름을 매핑하고 필요한 toobe Azure에서 전역적으로 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="5ce33-127">대체 hello `<server_admin_password>` 고유한 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="5ce33-128">여기서 지정 하는 hello 서버 관리자 로그인 및 암호는 toohello 서버에서 필요한 toolog와이 빠른 시작의 뒷부분에 나오는 해당 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="5ce33-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="5ce33-129">나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="5ce33-130">기본적으로 **postgres** 데이터베이스가 서버 아래에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="5ce33-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 데이터베이스는 사용자, 유틸리티 및 타사 응용 프로그램에서 사용 하기 위해 의미 하는 기본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="5ce33-132">서버 수준 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5ce33-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="5ce33-133">Hello로 Azure PostgreSQL 서버 수준 방화벽 규칙 만들기 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="5ce33-134">와 같은 외부 응용 프로그램 서버 수준 방화벽 규칙을 허용 [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 또는 [PgAdmin](https://www.pgadmin.org/) hello PostgreSQL Azure 서비스 방화벽을 통해 tooconnect tooyour 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="5ce33-135">IP 범위 toobe 수 tooconnect 네트워크에서에 대해 설명 하는 방화벽 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="5ce33-136">hello 다음 예제에서는 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) toocreate 방화벽 규칙 `AllowAllIps` 는 ip 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="5ce33-137">tooopen 모든 IP 주소를 IP 주소와 255.255.255.255 끝 주소 hello로 시작 하는 hello로 0.0.0.0를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="5ce33-138">Azure PostgreSQL 서버는 5432 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="5ce33-139">회사 네트워크 내에서 연결하려는 경우 5432 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5ce33-140">IT 부서 포트 5432 tooconnect tooyour Azure SQL 데이터베이스 서버를 열고 있으며</span><span class="sxs-lookup"><span data-stu-id="5ce33-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="5ce33-141">Hello 연결 정보를 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="5ce33-141">Get hello connection information</span></span>

<span data-ttu-id="5ce33-142">tooconnect tooyour 서버 tooprovide 호스트 정보 및 액세스 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="5ce33-143">hello 결과 JSON 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-143">hello result is in JSON format.</span></span> <span data-ttu-id="5ce33-144">Hello 메모 **administratorLogin** 및 **fullyQualifiedDomainName**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="5ce33-145">TooAzure 데이터베이스 psql를 사용 하 여 PostgreSQL 데이터베이스에 대 한 연결</span><span class="sxs-lookup"><span data-stu-id="5ce33-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="5ce33-146">클라이언트 컴퓨터에 설치 된 PostgreSQL의 로컬 인스턴스를 사용할 수 있습니다 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), 또는 hello Azure 클라우드 콘솔 tooconnect tooan Azure PostgreSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="5ce33-147">PostgreSQL 서버에 대 한 hello psql 명령줄 유틸리티 tooconnect toohello Azure 데이터베이스를 지금 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="5ce33-148">Hello psql 명령 tooconnect tooan Azure 데이터베이스 PostgreSQL 서버에 대 한 다음 실행</span><span class="sxs-lookup"><span data-stu-id="5ce33-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="5ce33-149">다음 명령을 hello 라는 toohello 기본 데이터베이스를 연결 하는 예를 들어 **postgres** PostgreSQL 서버의 **mypgserver 20170401.postgres.database.azure.com** 액세스 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="5ce33-150">Hello 입력 `<server_admin_password>` 암호를 묻는 메시지가 나타나면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="5ce33-151">연결 된 toohello 서버 되 면 hello 프롬프트에서 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="5ce33-152">Hello 프롬프트에서 실행 명령을 tooswitch 연결 toohello 새로 만든 데이터베이스를 다음 hello **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="5ce33-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="5ce33-153">Hello 데이터베이스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce33-153">Create tables in hello database</span></span>
<span data-ttu-id="5ce33-154">배웠으므로 어떻게 tooconnect toohello Azure PostgreSQL 데이터베이스 해 볼 수 있습니다 방법을 보다 toocomplete 몇 가지 기본적인 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="5ce33-155">먼저 테이블을 만들고 일부 데이터와 함께 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="5ce33-156">인벤토리 정보를 추적하는 테이블을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="5ce33-157">새로 만든 테이블의 테이블 목록이 hello 지금 입력 하 여 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="5ce33-158">Hello 테이블로 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-158">Load data into hello tables</span></span>
<span data-ttu-id="5ce33-159">이제 테이블을 만들었으므로 이 테이블에 일부 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="5ce33-160">Hello open 명령 프롬프트 창에서 실행 hello 쿼리 tooinsert 다음 데이터의 일부 행</span><span class="sxs-lookup"><span data-stu-id="5ce33-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="5ce33-161">이제 두 개의 행 앞에서 만든 hello 테이블에 샘플 데이터의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="5ce33-162">Hello 테이블의 hello 데이터 쿼리 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ce33-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="5ce33-163">Hello 쿼리 tooretrieve 정보 hello 데이터베이스 테이블에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="5ce33-164">Hello 테이블의 hello 데이터를 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="5ce33-165">hello 행이 데이터를 검색 하는 경우 그에 따라 업데이트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="5ce33-166">데이터베이스 tooa 이전 시점으로 복원</span><span class="sxs-lookup"><span data-stu-id="5ce33-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="5ce33-167">실수로 테이블을 삭제한 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="5ce33-168">이런 경우는 쉽게 복구할 수 없는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="5ce33-169">PostgreSQL에 대 한 azure 데이터베이스 toogo 백 tooany-시점 (마지막 too7 일 (기본) 위쪽과 35 일 (표준) hello)에 있으며이 시점에서 tooa 새 서버를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="5ce33-170">이 새 서버 toorecover 삭제 된 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="5ce33-171">hello 표를 추가 하기 전에 단계 복원 hello 샘플 서버 tooa 지점 뒤 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="5ce33-172">hello `az postgres server restore` 명령 hello 매개 변수 뒤에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="5ce33-173">설정</span><span class="sxs-lookup"><span data-stu-id="5ce33-173">Setting</span></span> | <span data-ttu-id="5ce33-174">제안 값</span><span class="sxs-lookup"><span data-stu-id="5ce33-174">Suggested value</span></span> | <span data-ttu-id="5ce33-175">설명</span><span class="sxs-lookup"><span data-stu-id="5ce33-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="5ce33-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="5ce33-176">--resource-group</span></span> |  <span data-ttu-id="5ce33-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5ce33-177">myResourceGroup</span></span> |  <span data-ttu-id="5ce33-178">원본 서버가 있는 hello에 있는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="5ce33-179">--name</span><span class="sxs-lookup"><span data-stu-id="5ce33-179">--name</span></span> | <span data-ttu-id="5ce33-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="5ce33-180">mypgserver-restored</span></span> | <span data-ttu-id="5ce33-181">hello restore 명령에 의해 만들어진 hello 새 서버의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="5ce33-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="5ce33-182">restore-point-in-time</span></span> | <span data-ttu-id="5ce33-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="5ce33-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="5ce33-184">지정 시간 toorestore를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="5ce33-185">이 날짜 및 시간 hello 원본 서버 백업 보존 기간 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="5ce33-186">ISO8601 날자 및 시간 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="5ce33-187">예를 들어 `2017-04-13T05:59:00-08:00`과 같은 고유한 현지 표준 시간대 또는 UTC Zulu 형식 `2017-04-13T13:59:00Z`를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="5ce33-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="5ce33-188">--source-server</span></span> | <span data-ttu-id="5ce33-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="5ce33-189">mypgserver-20170401</span></span> | <span data-ttu-id="5ce33-190">hello 이름 또는에서 원본 서버 toorestore hello의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="5ce33-191">복원 하는 서버 tooa-시점 hello 시점의 hello 원래 서버로 복사 하 여 지정한 시간에 새 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="5ce33-192">hello 위치 및 복원 하는 hello 서버에 대 한 계층 값 가격 hello 원본 서버와 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="5ce33-193">hello 명령을 동기적 이므로 hello 서버 복원 된 후에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="5ce33-194">Hello 복원이 완료 되 면 생성 된 hello 새 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="5ce33-195">Hello 데이터가 예상 대로 복원 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce33-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ce33-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ce33-196">Next steps</span></span>
<span data-ttu-id="5ce33-197">이 자습서에서는 방법에 대해 배웠습니다 toouse Azure CLI (명령줄 인터페이스) 및 기타 유틸리티를:</span><span class="sxs-lookup"><span data-stu-id="5ce33-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="5ce33-198">PostgreSQL용 Azure Database 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce33-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="5ce33-199">Hello 서버 방화벽을 구성</span><span class="sxs-lookup"><span data-stu-id="5ce33-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="5ce33-200">사용 하 여 [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티 toocreate 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="5ce33-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="5ce33-201">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="5ce33-201">Load sample data</span></span>
> * <span data-ttu-id="5ce33-202">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="5ce33-202">Query data</span></span>
> * <span data-ttu-id="5ce33-203">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ce33-203">Update data</span></span>
> * <span data-ttu-id="5ce33-204">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="5ce33-204">Restore data</span></span>

<span data-ttu-id="5ce33-205">그 다음, 자세한 방법을 toouse hello Azure 포털 toodo 유사한 작업을이 자습서를 검토: [PostgreSQL를 사용 하 여 Azure 포털을 hello에 대 한 첫 번째 Azure 데이터베이스 디자인](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5ce33-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
