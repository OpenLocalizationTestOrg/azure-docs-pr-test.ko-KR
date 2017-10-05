---
title: "Azure CLI를 사용하여 PostgreSQL용  Azure Database 만들기 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스)를 통해 Azure Database for PostgreSQL 서버를 만들고 관리하기 위한 빠른 시작 가이드입니다."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: d78243abc140c7b3f0b99bdf56821b7920568550
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-using-the-azure-cli"></a><span data-ttu-id="c9354-103">Azure CLI를 사용하여 PostgreSQL용  Azure Database 만들기</span><span class="sxs-lookup"><span data-stu-id="c9354-103">Create an Azure Database for PostgreSQL using the Azure CLI</span></span>
<span data-ttu-id="c9354-104">PostgreSQL용  Azure Database는 클라우드에서 항상 사용 가능한 PostgreSQL 데이터베이스를 실행, 관리 및 크기 조정할 수 있게 하는 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="c9354-105">명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="c9354-106">이 빠른 시작에서는 Azure CLI를 사용하여 [Azure 리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)에서 PostgreSQL용 Azure Database 서버를 만드는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-106">This quickstart shows you how to create an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the Azure CLI.</span></span>

<span data-ttu-id="c9354-107">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c9354-108">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c9354-109">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="c9354-110">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9354-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="c9354-111">구독이 여러 개인 경우 리소스가 과금될 적절한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-111">If you have multiple subscriptions, choose the appropriate subscription in which the resource will be billed.</span></span> <span data-ttu-id="c9354-112">[az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="c9354-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c9354-113">Create a resource group</span></span>

<span data-ttu-id="c9354-114">[az group create](/cli/azure/group#create) 명령을 사용하여 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c9354-115">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="c9354-116">다음 예제는 `westus` 위치에 `myresourcegroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-116">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="c9354-117">PostgreSQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="c9354-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="c9354-118">[az postgres server create](/cli/azure/postgres/server#create) 명령을 사용하여 [PostgreSQL용 Azure Database 서버](overview.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-118">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="c9354-119">서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="c9354-120">다음 예제에서는 `mylogin` 서버 관리자 로그인을 사용하여 `myresourcegroup` 리소스 그룹에 이름이 `mypgserver-20170401`인 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-120">The following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="c9354-121">서버 이름은 DNS 이름에 매핑되므로 Azure에서 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-121">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="c9354-122">`<server_admin_password>`를 자신의 고유한 값으로 직접 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-122">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="c9354-123">여기에 지정한 서버 관리자 로그인 및 암호는 이 빠른 시작의 뒷부분에 나오는 서버 및 데이터베이스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-123">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="c9354-124">나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="c9354-125">기본적으로 **postgres** 데이터베이스가 서버 아래에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="c9354-126">[postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 데이터베이스는 사용자, 유틸리티 및 타사 응용 프로그램에서 사용하는 기본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-126">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="c9354-127">서버 수준 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="c9354-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="c9354-128">[az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 명령을 사용하여 Azure PostgreSQL 서버 수준 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-128">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="c9354-129">서버 수준 방화벽 규칙을 사용하면 [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 또는 [PgAdmin](https://www.pgadmin.org/)과 같은 외부 응용 프로그램에서 Azure PostgreSQL 서비스 방화벽을 통해 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="c9354-130">IP 범위를 적용하는 방화벽 규칙을 설정하여 네트워크에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-130">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="c9354-131">다음 예제에서는 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create)를 사용하여 IP 주소 범위에 대한 `AllowAllIps` 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-131">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="c9354-132">모든 IP 주소를 열려면 시작 IP 주소로 0.0.0.0을, 끝나는 IP 주소로 255.255.255.255를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-132">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="c9354-133">Azure PostgreSQL 서버는 5432 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="c9354-134">회사 네트워크 내에서 연결하려는 경우 5432 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c9354-135">IT 부서에서 포트 5432를 열어 Azure SQL Database 서버에 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-135">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>

## <a name="get-the-connection-information"></a><span data-ttu-id="c9354-136">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c9354-136">Get the connection information</span></span>

<span data-ttu-id="c9354-137">서버에 연결하려면 호스트 정보와 액세스 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="c9354-138">결과는 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-138">The result is in JSON format.</span></span> <span data-ttu-id="c9354-139">**administratorLogin** 및 **fullyQualifiedDomainName**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-139">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-postgresql-database-using-psql"></a><span data-ttu-id="c9354-140">psql을 사용하여 PostgreSQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="c9354-140">Connect to PostgreSQL database using psql</span></span>

<span data-ttu-id="c9354-141">클라이언트 컴퓨터에 PostgreSQL이 설치되어 있는 경우 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 로컬 인스턴스를 사용하여 Azure PostgreSQL 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="c9354-142">이제 psql 명령줄 유틸리티를 사용하여 Azure PostgreSQL 서버에 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-142">Let's now use the psql command-line utility to connect to the Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="c9354-143">다음 psql 명령을 실행하여 Azure Database for PostgreSQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-143">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="c9354-144">예를 들어 다음 명령은 액세스 자격 증명을 사용하여 **mypgserver-20170401.postgres.database.azure.com** PostgreSQL 서버의 **postgres**라는 기본 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-144">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="c9354-145">암호를 묻는 메시지가 표시되면 선택한 `<server_admin_password>`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-145">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="c9354-146">서버에 연결되면 프롬프트에서 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-146">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="c9354-147">프롬프트에서 다음 명령을 실행하여 새로 만든 **mypgsqldb** 데이터베이스에 대한 연결로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-147">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-to-postgresql-database-using-pgadmin"></a><span data-ttu-id="c9354-148">pgAdmin을 사용하여 PostgreSQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="c9354-148">Connect to PostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="c9354-149">GUI 도구 _pgAdmin_을 사용하여 Azure PostgreSQL 서버에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="c9354-149">To connect to Azure PostgreSQL server using the GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="c9354-150">클라이언트 컴퓨터에서 _pgAdmin_ 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-150">Launch the _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="c9354-151">_pgAdmin_은 http://www.pgadmin.org/에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="c9354-152">**빠른 링크** 메뉴에서 **새 서버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-152">Choose **Add New Server** from the **Quick Links** menu.</span></span>
3.  <span data-ttu-id="c9354-153">**만들기-서버** 대화 상자의 **일반** 탭에서서버에 대해 고유하면서 익숙한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-153">In the **Create - Server** dialog box **General** tab, enter a unique friendly Name for the server.</span></span> <span data-ttu-id="c9354-154">**Azure PostgreSQL 서버**라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="c9354-155">![pgAdmin 도구 - 만들기 - 서버](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="c9354-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="c9354-156">**만들기 - 서버** 대화 상자의 **연결** 탭에서 </span><span class="sxs-lookup"><span data-stu-id="c9354-156">In the **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="c9354-157">**호스트 이름/주소** 상자에 정규화된 서버 이름(예: **mypgserver 20170401.postgres.database.azure.com**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-157">Enter the fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in the **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="c9354-158">**포트** 상자에 포트 5432를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-158">Enter port 5432 into the **Port** box.</span></span> 
    - <span data-ttu-id="c9354-159">이 빠른 시작의 앞 부분에서 구한 **서버 관리자 로그인(user@mypgserver)**과, 서버를 만들 때 입력한 암호를 각각 **사용자 이름**과 **암호**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-159">Enter the **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created the server into the **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="c9354-160">**SSL 모드**를 **필수**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="c9354-161">기본적으로 모든 Azure PostgreSQL 서버는 SSL을 실행한 상태에서 만들어집니다. </span><span class="sxs-lookup"><span data-stu-id="c9354-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="c9354-162">SSL 실행을 해제하려면 [SSL 적용](./concepts-ssl-connection-security.md)에서 세부 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9354-162">To turn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - 만들기 - 서버](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="c9354-164">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-164">Click **Save**.</span></span>
6.  <span data-ttu-id="c9354-165">브라우저 왼쪽 창에서 **서버 그룹**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-165">In the Browser left pane, expand the **Server Groups**.</span></span> <span data-ttu-id="c9354-166">**Azure PostgreSQL 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="c9354-167">연결된 **서버**를 선택한 다음 그 아래의 **데이터베이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-167">Choose the **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="c9354-168">**데이터베이스**를 마우스 오른쪽 단추로 클릭하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-168">Right-click on **Databases** to Create a Database.</span></span>
9.  <span data-ttu-id="c9354-169">데이터베이스 이름 **mypgsqldb**를 선택하고 그에 대한 소유자를 서버 관리자 로그인 **mylogin**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-169">Choose a database name **mypgsqldb** and the owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="c9354-170">**저장**을 클릭하여 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-170">Click **Save** to create a blank database.</span></span>
11. <span data-ttu-id="c9354-171">**브라우저**에서 **서버** 그룹을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-171">In the **Browser**, expand the **Servers** group.</span></span> <span data-ttu-id="c9354-172">만든 서버를 확장하고 그 아래에서 **mypgsqldb** 데이터베이스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-172">Expand the server you created, and see the database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="c9354-173">![pgAdmin - 만들기 - 데이터베이스](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="c9354-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="c9354-174">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="c9354-174">Clean up resources</span></span>

<span data-ttu-id="c9354-175">[Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 삭제하여 이 빠른 시작에서 만든 모든 리소스를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-175">Clean up all resources you created in the quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="c9354-176">이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="c9354-177">다음 빠른 시작을 계속 진행하려는 경우 이 빠른 시작에서 만든 리소스를 정리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-177">If you plan to continue on to work with subsequent quickstarts, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="c9354-178">계속하지 않으려는 경우 다음 단계에 따라 이 빠른 시작에서 만든 모든 리소스를 Azure CLI에서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-178">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="c9354-179">새로 만든 서버만 삭제하려면 [az postgres server delete](/cli/azure/postgres/server#delete) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9354-179">If you just would like to delete the one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="c9354-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9354-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c9354-181">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="c9354-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
