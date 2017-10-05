---
title: "첫 번째 Azure Database for MySQL 데이터베이스 디자인 - Azure CLI | Microsoft Docs"
description: "이 자습서에서는 명령줄에서 Azure CLI 2.0을 사용하여 MySQL용 Azure Database 서버 및 데이터베이스를 만들고 관리하는 방법을 설명합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="9efac-103">첫 번째 Azure Database for MySQL 데이터베이스 디자인</span><span class="sxs-lookup"><span data-stu-id="9efac-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="9efac-104">Azure Database for MySQL은 MySQL Community Edition 데이터베이스 엔진을 기반으로 한 Microsoft 클라우드의 관계형 데이터베이스 서비스입니다</span><span class="sxs-lookup"><span data-stu-id="9efac-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="9efac-105">이 자습서에서는 Azure CLI(명령줄 인터페이스) 및 기타 유틸리티를 사용하여 다음을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9efac-106">Azure Database for MySQL 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="9efac-107">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="9efac-107">Configure the server firewall</span></span>
> * <span data-ttu-id="9efac-108">[mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="9efac-109">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9efac-109">Load sample data</span></span>
> * <span data-ttu-id="9efac-110">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="9efac-110">Query data</span></span>
> * <span data-ttu-id="9efac-111">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="9efac-111">Update data</span></span>
> * <span data-ttu-id="9efac-112">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="9efac-112">Restore data</span></span>

<span data-ttu-id="9efac-113">브라우저에서 Azure Cloud Shell을 사용하거나 컴퓨터에 [Azure CLI 2.0을 설치]( /cli/azure/install-azure-cli)하여 이 자습서의 코드 블록을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9efac-114">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9efac-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="9efac-116">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9efac-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="9efac-117">구독이 여러 개인 경우 리소스가 있거나 요금이 청구되는 적절한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="9efac-118">[az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="9efac-119">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-119">Create a resource group</span></span>
<span data-ttu-id="9efac-120">[az group create](https://docs.microsoft.com/cli/azure/group#create) 명령을 사용하여 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="9efac-121">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="9efac-122">다음 예제는 `westus` 위치에 `mycliresource`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="9efac-123">Azure Database for MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="9efac-124">az mysql server create 명령을 사용하여 Azure Database for MySQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="9efac-125">서버는 여러 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-125">A server can manage multiple databases.</span></span> <span data-ttu-id="9efac-126">일반적으로 각 프로젝트 또는 각 사용자에 대해 별도의 데이터베이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="9efac-127">다음 예제에서는 `westus`에 있는 MySQL용 Azure Database 서버를 `mycliserver`라는 이름으로 `mycliresource` 리소스 그룹에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="9efac-128">서버에는 `myadmin` 이름과 `Password01!` 암호의 관리자 로그인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="9efac-129">서버는 서버의 모든 데이터베이스 간에 공유되는 **기본** 성능 계층과 **50** 계산 단위로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="9efac-130">응용 프로그램 요구 사항에 따라 계산과 저장소의 크기를 확장하거나 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="9efac-131">방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="9efac-131">Configure firewall rule</span></span>
<span data-ttu-id="9efac-132">az mysql server firewall-rule create 명령을 사용하여 Azure Database for MySQL 서버 수준 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="9efac-133">서버 수준 방화벽 규칙을 사용하면 **mysql** 명령줄 도구 또는 MySQL Workbench와 같은 외부 응용 프로그램에서 Azure MySQL 서비스 방화벽을 통해 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="9efac-134">다음 예제에서는 미리 정의된 주소 범위에 대한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="9efac-135">이 예제에서는 가능한 IP 주소 범위 전체를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="9efac-136">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="9efac-136">Get the connection information</span></span>

<span data-ttu-id="9efac-137">서버에 연결하려면 호스트 정보와 액세스 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="9efac-138">결과는 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-138">The result is in JSON format.</span></span> <span data-ttu-id="9efac-139">**fullyQualifiedDomainName** 및 **administratorLogin**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="9efac-140">mysql을 사용하여 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="9efac-140">Connect to the server using mysql</span></span>
<span data-ttu-id="9efac-141">[mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)를 사용하여 Azure Database for MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="9efac-142">이 예제에서 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="9efac-143">빈 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-143">Create a blank database</span></span>
<span data-ttu-id="9efac-144">서버에 연결되면 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="9efac-145">프롬프트에서 다음 명령을 실행하여 새로 만든 이 데이터베이스에 대한 연결로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="9efac-146">데이터베이스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-146">Create tables in the database</span></span>
<span data-ttu-id="9efac-147">이제 Azure Database for MySQL 데이터베이스에 연결하는 방법을 알았으므로 몇 가지 기본 작업을 수행하는 방법을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="9efac-148">먼저 테이블을 만들고 일부 데이터와 함께 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="9efac-149">인벤토리 정보를 저장하는 테이블을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="9efac-150">테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9efac-150">Load data into the tables</span></span>
<span data-ttu-id="9efac-151">이제 테이블을 만들었으므로 이 테이블에 일부 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="9efac-152">열린 명령 프롬프트 창에서 다음 쿼리를 실행하여 데이터 행을 일부 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="9efac-153">이제 앞에서 만든 테이블에 두 개의 샘플 데이터 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="9efac-154">테이블의 데이터 쿼리 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="9efac-154">Query and update the data in the tables</span></span>
<span data-ttu-id="9efac-155">다음 쿼리를 실행하여 데이터베이스 테이블에서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="9efac-156">또한 테이블의 데이터를 업데이트할 수도 있습니다</span><span class="sxs-lookup"><span data-stu-id="9efac-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="9efac-157">이에 따라 데이터를 검색할 때 해당 행이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="9efac-158">이전 시점으로 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="9efac-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="9efac-159">실수로 이 테이블을 삭제했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="9efac-160">이런 경우는 쉽게 복구할 수 없는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="9efac-161">Azure Database for MySQL을 사용하면 마지막 시점에서 최대 35일 전의 특정 시점으로 되돌아가 이 시점의 새 서버로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="9efac-162">이 새 서버를 사용하여 삭제된 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="9efac-163">다음 단계에서는 테이블이 추가되기 이전 시점으로 샘플 서버를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="9efac-164">복원에는 다음 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="9efac-165">복원 지점: 데이터베이스를 변경하기 전의 특정 시점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="9efac-166">원본 데이터베이스의 가장 오래된 백업 값보다 크거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="9efac-167">대상 서버: 복원해 두려는 새 서버의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="9efac-168">원본 서버: 복원해 오려는 서버의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="9efac-169">위치: 지역은 선택할 수 없으며, 기본적으로 원본 서버와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="9efac-170">서버를 테이블 삭제 이전의 [특정 시점으로 복원](./howto-restore-server-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="9efac-171">다른 특정 시점으로 서버를 복원하는 경우 [서비스 계층](./concepts-service-tiers.md)에 대한 보존 기간 내에 있다면 중복된 새 서버를 지정한 시점의 원본 서버로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9efac-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9efac-172">Next Steps</span></span>
<span data-ttu-id="9efac-173">이 자습서에서는 다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9efac-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9efac-174">Azure Database for MySQL 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="9efac-175">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="9efac-175">Configure the server firewall</span></span>
> * <span data-ttu-id="9efac-176">[mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9efac-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="9efac-177">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9efac-177">Load sample data</span></span>
> * <span data-ttu-id="9efac-178">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="9efac-178">Query data</span></span>
> * <span data-ttu-id="9efac-179">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="9efac-179">Update data</span></span>
> * <span data-ttu-id="9efac-180">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="9efac-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9efac-181">Azure Database for MySQL - Azure CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="9efac-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
