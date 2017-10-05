---
title: "빠른 시작: MySQL용 Azure Database 서버 만들기 - Azure CLI | Microsoft Docs"
description: "이 빠른 시작에서는 Azure CLI를 사용하여 Azure 리소스 그룹에서 MySQL용 Azure Database 서버를 만드는 방법을 살펴봅니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 04fc441aee7a4c8adc4f02d5e51b2d9e64400f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="0cacd-103">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기 </span><span class="sxs-lookup"><span data-stu-id="0cacd-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="0cacd-104">이 빠른 시작에서는 약 5분 안에 Azure CLI를 사용하여 Azure 리소스 그룹에서 MySQL용 Azure Database 서버를 만드는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="0cacd-105">명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="0cacd-106">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0cacd-107">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0cacd-108">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="0cacd-109">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacd-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="0cacd-110">구독이 여러 개인 경우 리소스가 있거나 요금이 청구되는 적절한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="0cacd-111">[az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0cacd-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="0cacd-112">Create a resource group</span></span>
<span data-ttu-id="0cacd-113">[az group create](https://docs.microsoft.com/cli/azure/group#create) 명령을 사용하여 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="0cacd-114">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="0cacd-115">다음 예제는 `westus` 위치에 `myresourcegroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="0cacd-116">MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="0cacd-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="0cacd-117">**az mysql server create** 명령을 사용하여 MySQL용 Azure Database 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-117">Create an Azure Database for MySQL server with the **az mysql server create** command.</span></span> <span data-ttu-id="0cacd-118">서버는 여러 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-118">A server can manage multiple databases.</span></span> <span data-ttu-id="0cacd-119">일반적으로 각 프로젝트 또는 각 사용자에 대해 별도의 데이터베이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="0cacd-120">다음 예제에서는 `westus`에 있는 MySQL용 Azure Database 서버를 `myserver4demo`라는 이름으로 `myresourcegroup` 리소스 그룹에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-120">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="0cacd-121">서버에는 `myadmin` 이름과 `Password01!` 암호의 관리자 로그인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-121">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="0cacd-122">서버는 서버의 모든 데이터베이스 간에 공유되는 **기본** 성능 계층과 **50** 계산 단위로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-122">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="0cacd-123">응용 프로그램 요구 사항에 따라 계산과 저장소의 크기를 확장하거나 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-123">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="0cacd-124">방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="0cacd-124">Configure firewall rule</span></span>
<span data-ttu-id="0cacd-125">**az mysql server firewall-rule create** 명령을 사용하여 MySQL용 Azure Database 서버 수준 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-125">Create an Azure Database for MySQL server-level firewall rule using the **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="0cacd-126">서버 수준 방화벽 규칙을 사용하면 **mysql.exe** 명령줄 도구 또는 MySQL Workbench와 같은 외부 응용 프로그램에서 Azure MySQL 서비스 방화벽을 통해 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-126">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="0cacd-127">다음 예제에서는 미리 정의된 주소 범위(이 예제에서는 전체 가능한 IP 주소 범위)에 대해 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-127">The following example creates a firewall rule for a predefined address range, which in this example is the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="0cacd-128">SSL 설정 구성</span><span class="sxs-lookup"><span data-stu-id="0cacd-128">Configure SSL settings</span></span>
<span data-ttu-id="0cacd-129">기본적으로 서버와 클라이언트 응용 프로그램 간에 SSL 연결이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="0cacd-130">이렇게 하면 인터넷을 통해 데이터 스트림을 암호화하여 "이동 중"인 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-130">This ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span>  <span data-ttu-id="0cacd-131">이 빠른 시작을 간단하게 하기 위해 서버에 대해 SSL 연결을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-131">To make this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="0cacd-132">이런 설정은 프로덕션 서버에는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="0cacd-133">자세한 내용은 [MySQL용 Azure 데이터베이스에 안전하게 연결하기 위한 사용자 응용 프로그램의 SSL 연결 구성](./howto-configure-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacd-133">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="0cacd-134">다음 예에서는 MySQL 서버에 SSL을 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-134">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="0cacd-135">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="0cacd-135">Get the connection information</span></span>

<span data-ttu-id="0cacd-136">서버에 연결하려면 호스트 정보와 액세스 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-136">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="0cacd-137">결과는 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-137">The result is in JSON format.</span></span> <span data-ttu-id="0cacd-138">**fullyQualifiedDomainName** 및 **administratorLogin**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-138">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="0cacd-139">mysql.exe 명령줄 도구를 사용하여 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="0cacd-139">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="0cacd-140">**mysql.exe** 명령줄 도구를 사용하여 서버에 연결.</span><span class="sxs-lookup"><span data-stu-id="0cacd-140">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="0cacd-141">[여기](https://dev.mysql.com/downloads/)에서 MySQL을 다운로드하여 컴퓨터에 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="0cacd-142">대신 예제 코드에서 **시도** 단추를 클릭하거나 Azure Portal의 오른쪽 상단 도구 모음에서 `>_` 단추를 클릭하고 **Azure Cloud Shell**을 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-142">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="0cacd-143">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-143">Type the next commands:</span></span> 

1. <span data-ttu-id="0cacd-144">**mysql** 명령줄 도구를 사용하여 서버에 연결:</span><span class="sxs-lookup"><span data-stu-id="0cacd-144">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="0cacd-145">서버 상태 보기:</span><span class="sxs-lookup"><span data-stu-id="0cacd-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="0cacd-146">모든 작업이 제대로 진행되었다면 명령줄 도구에서 다음 텍스트가 출력될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-146">If everything goes well, the command-line tool should output the following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="0cacd-147">다른 명령은 [MySQL 5.7 참조 설명서 - 4.5.1장](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cacd-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="0cacd-148">MySQL Workbench GUI 도구로 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="0cacd-148">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="0cacd-149">클라이언트 컴퓨터에서 MySQL Workbench 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-149">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="0cacd-150">MySQL Workbench는 [여기](https://dev.mysql.com/downloads/workbench/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="0cacd-151">**새 연결 설정** 대화 상자의 **매개 변수** 탭에 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-151">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![새 연결 설정](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="0cacd-153">**설정**</span><span class="sxs-lookup"><span data-stu-id="0cacd-153">**Setting**</span></span> | <span data-ttu-id="0cacd-154">**제안 값**</span><span class="sxs-lookup"><span data-stu-id="0cacd-154">**Suggested Value**</span></span> | <span data-ttu-id="0cacd-155">**설명**</span><span class="sxs-lookup"><span data-stu-id="0cacd-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="0cacd-156">연결 이름</span><span class="sxs-lookup"><span data-stu-id="0cacd-156">Connection Name</span></span> | <span data-ttu-id="0cacd-157">내 연결</span><span class="sxs-lookup"><span data-stu-id="0cacd-157">My Connection</span></span> | <span data-ttu-id="0cacd-158">이 연결에 대한 레이블 지정(아무 이름이나 가능)</span><span class="sxs-lookup"><span data-stu-id="0cacd-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="0cacd-159">연결 방법</span><span class="sxs-lookup"><span data-stu-id="0cacd-159">Connection Method</span></span> | <span data-ttu-id="0cacd-160">표준(TCP/IP) 선택</span><span class="sxs-lookup"><span data-stu-id="0cacd-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="0cacd-161">TCP/IP 프로토콜을 사용하여 MySQL에 대한 Azure Database에 연결></span><span class="sxs-lookup"><span data-stu-id="0cacd-161">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="0cacd-162">호스트 이름</span><span class="sxs-lookup"><span data-stu-id="0cacd-162">Hostname</span></span> | <span data-ttu-id="0cacd-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="0cacd-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="0cacd-164">앞에서 기록한 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="0cacd-165">포트</span><span class="sxs-lookup"><span data-stu-id="0cacd-165">Port</span></span> | <span data-ttu-id="0cacd-166">3306</span><span class="sxs-lookup"><span data-stu-id="0cacd-166">3306</span></span> | <span data-ttu-id="0cacd-167">MySQL의 기본 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-167">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="0cacd-168">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="0cacd-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="0cacd-169">앞에서 기록한 서버 관리자 로그인</span><span class="sxs-lookup"><span data-stu-id="0cacd-169">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="0cacd-170">암호</span><span class="sxs-lookup"><span data-stu-id="0cacd-170">Password</span></span> | **** | <span data-ttu-id="0cacd-171">이전에 구성한 관리자 계정 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-171">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="0cacd-172">**연결 테스트**를 클릭하여 모든 매개 변수가 올바르게 구성되었는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-172">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="0cacd-173">이제 연결을 클릭하여 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-173">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0cacd-174">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="0cacd-174">Clean up resources</span></span>
<span data-ttu-id="0cacd-175">다른 빠른 시작/자습서에서 이러한 리소스가 필요하지 않으면 다음 명령을 수행하여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cacd-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="0cacd-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cacd-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cacd-177">Azure CLI로 MySQL 데이터베이스 디자인</span><span class="sxs-lookup"><span data-stu-id="0cacd-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
