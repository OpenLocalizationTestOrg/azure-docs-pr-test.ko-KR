---
title: "PostgreSQL hello Azure CLI를 사용 하 여에 대 한 Azure 데이터베이스 만들기 | Microsoft Docs"
description: "빠른 시작 가이드 toocreate 하 고 Azure CLI (명령줄 인터페이스)를 사용 하 여 PostgreSQL 서버에 대 한 Azure 데이터베이스를 관리 합니다."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="49f7b-103">PostgreSQL hello Azure CLI를 사용 하 여에 대 한 Azure 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="49f7b-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="49f7b-104">Azure에 대 한 PostgreSQL 데이터베이스가 toorun 수 있는 관리 되는 서비스, 관리 하 고 hello 클라우드에서 항상 사용 가능한 PostgreSQL 데이터베이스의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="49f7b-105">hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="49f7b-106">이 빠른 시작에서는 toocreate Azure 데이터베이스 방법 PostgreSQL 서버에 대 한 프로그램 [Azure 리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) Azure CLI hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="49f7b-107">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49f7b-108">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="49f7b-109">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49f7b-110">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="49f7b-111">다중 구독인 경우 hello 리소스는 지불 hello 적절 한 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="49f7b-112">[az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="49f7b-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="49f7b-113">Create a resource group</span></span>

<span data-ttu-id="49f7b-114">만들기는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello를 사용 하 여 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="49f7b-115">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="49f7b-116">hello 다음 예제에서는 명명 된 리소스 그룹 `myresourcegroup` hello에 `westus` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="49f7b-117">PostgreSQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="49f7b-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="49f7b-118">만들기는 [PostgreSQL 서버에 대 한 Azure 데이터베이스](overview.md) hello를 사용 하 여 [az postgres 서버 만들](/cli/azure/postgres/server#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="49f7b-119">서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="49f7b-120">hello 다음 예제에서는 이라는 서버 `mypgserver-20170401` 리소스 그룹에서 `myresourcegroup` 서버 관리자 로그인과 `mylogin`합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="49f7b-121">서버 hello 이름을 tooDNS 이름을 매핑하고 필요한 toobe Azure에서 전역적으로 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="49f7b-122">대체 hello `<server_admin_password>` 고유한 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="49f7b-123">여기서 지정 하는 hello 서버 관리자 로그인 및 암호는 toohello 서버에서 필요한 toolog와이 빠른 시작의 뒷부분에 나오는 해당 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="49f7b-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="49f7b-124">나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="49f7b-125">기본적으로 **postgres** 데이터베이스가 서버 아래에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="49f7b-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 데이터베이스는 사용자, 유틸리티 및 타사 응용 프로그램에서 사용 하기 위해 의미 하는 기본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="49f7b-127">서버 수준 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="49f7b-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="49f7b-128">Hello로 Azure PostgreSQL 서버 수준 방화벽 규칙 만들기 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="49f7b-129">와 같은 외부 응용 프로그램 서버 수준 방화벽 규칙을 허용 [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 또는 [PgAdmin](https://www.pgadmin.org/) hello PostgreSQL Azure 서비스 방화벽을 통해 tooconnect tooyour 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="49f7b-130">IP 범위 toobe 수 tooconnect 네트워크에서에 대해 설명 하는 방화벽 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="49f7b-131">hello 다음 예제에서는 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) toocreate 방화벽 규칙 `AllowAllIps` 는 ip 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="49f7b-132">tooopen 모든 IP 주소를 IP 주소와 255.255.255.255 끝 주소 hello로 시작 하는 hello로 0.0.0.0를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="49f7b-133">Azure PostgreSQL 서버는 5432 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="49f7b-134">회사 네트워크 내에서 연결하려는 경우 5432 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="49f7b-135">IT 부서 포트 5432 tooconnect tooyour Azure SQL 데이터베이스 서버를 열고 있으며</span><span class="sxs-lookup"><span data-stu-id="49f7b-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="49f7b-136">Hello 연결 정보를 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="49f7b-136">Get hello connection information</span></span>

<span data-ttu-id="49f7b-137">tooconnect tooyour 서버 tooprovide 호스트 정보 및 액세스 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="49f7b-138">hello 결과 JSON 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-138">hello result is in JSON format.</span></span> <span data-ttu-id="49f7b-139">Hello 메모 **administratorLogin** 및 **fullyQualifiedDomainName**합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="49f7b-140">Psql를 사용 하 여 tooPostgreSQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="49f7b-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="49f7b-141">클라이언트 컴퓨터에 설치 된 PostgreSQL의 로컬 인스턴스를 사용할 수 있습니다 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="49f7b-142">이제 hello psql 명령줄 유틸리티 tooconnect toohello Azure PostgreSQL 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="49f7b-143">Hello psql 명령 tooconnect tooan Azure 데이터베이스 PostgreSQL 서버에 대 한 다음 실행</span><span class="sxs-lookup"><span data-stu-id="49f7b-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="49f7b-144">다음 명령을 hello 라는 toohello 기본 데이터베이스를 연결 하는 예를 들어 **postgres** PostgreSQL 서버의 **mypgserver 20170401.postgres.database.azure.com** 액세스 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="49f7b-145">Hello 입력 `<server_admin_password>` 암호를 묻는 메시지가 나타나면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="49f7b-146">연결 된 toohello 서버 되 면 hello 프롬프트에서 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="49f7b-147">Hello 프롬프트에서 실행 명령을 tooswitch 연결 toohello 새로 만든 데이터베이스를 다음 hello **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="49f7b-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="49f7b-148">PgAdmin를 사용 하 여 tooPostgreSQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="49f7b-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="49f7b-149">hello GUI 도구를 사용 하 여 tooconnect tooAzure PostgreSQL 서버 _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="49f7b-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="49f7b-150">Hello 시작 _pgAdmin_ 클라이언트 컴퓨터에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="49f7b-151">_pgAdmin_은 http://www.pgadmin.org/에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="49f7b-152">선택 **새 서버 추가** hello에서 **빠른 링크** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="49f7b-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="49f7b-153">Hello에 **서버 만들기-** 대화 상자 **일반** 탭에서 서버 hello에 대 한 고유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="49f7b-154">**Azure PostgreSQL 서버**라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="49f7b-155">![pgAdmin 도구 - 만들기 - 서버](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="49f7b-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="49f7b-156">Hello에 **서버 만들기-** 대화 상자, **연결** 탭:</span><span class="sxs-lookup"><span data-stu-id="49f7b-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="49f7b-157">Hello 정규화 된 서버 이름을 입력 하십시오 (예를 들어 **mypgserver 20170401.postgres.database.azure.com**) hello에 **호스트 이름 / 주소** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="49f7b-158">Hello에 포트 5432 입력 **포트** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="49f7b-159">Hello 입력 **서버 관리자 로그인 (user@mypgserver)** 의 앞부분에 나오는이 빠른 시작 및 hello에 hello 서버를 만들 때 입력 한 암호가 얻은 **Username** 및 **암호** 상자에 각각 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="49f7b-160">**SSL 모드**를 **필수**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="49f7b-161">기본적으로 모든 Azure PostgreSQL 서버는 SSL을 실행한 상태에서 만들어집니다. </span><span class="sxs-lookup"><span data-stu-id="49f7b-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="49f7b-162">SSL 적용 해제 tooturn 세부 사항을 볼 [적용 SSL](./concepts-ssl-connection-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - 만들기 - 서버](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="49f7b-164">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-164">Click **Save**.</span></span>
6.  <span data-ttu-id="49f7b-165">Hello 브라우저 왼쪽된 창에서 확장 hello **서버 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="49f7b-166">**Azure PostgreSQL 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="49f7b-167">Hello 선택 **서버** 에 연결 하 고 눌러 **데이터베이스** 그 아래에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="49f7b-168">마우스 오른쪽 단추로 클릭 **데이터베이스** tooCreate 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="49f7b-169">데이터베이스 이름을 선택 **mypgsqldb** 및 서버 관리자 로그인에 대 한 hello 소유자가 **mylogin**합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="49f7b-170">클릭 **저장** toocreate 빈 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="49f7b-171">Hello에 **브라우저**, hello 확장 **서버** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="49f7b-172">Hello 사용자가 만든 서버를 확장 하 고 hello 데이터베이스 참조 **mypgsqldb** 그 아래에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="49f7b-173">![pgAdmin - 만들기 - 데이터베이스](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="49f7b-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="49f7b-174">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="49f7b-174">Clean up resources</span></span>

<span data-ttu-id="49f7b-175">Hello를 삭제 하 여 hello 빠른 시작에서 만든 모든 리소스를 정리 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="49f7b-176">이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="49f7b-177">Toocontinue toowork 후속 사용 하려는 경우 퀵 스타트를 정리 하지 않습니다는이 빠른 시작에서 만든 리소스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="49f7b-178">Toocontinue 않으려는 경우 다음 단계 toodelete hello이 퀵이 스타트의 hello Azure CLI에에서 의해 생성 된 모든 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="49f7b-179">실행할 수만 toodelete hello 하나의 새로 만든된 서버 싶으면, [az postgres 서버 삭제](/cli/azure/postgres/server#delete) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="49f7b-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="49f7b-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49f7b-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="49f7b-181">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="49f7b-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
