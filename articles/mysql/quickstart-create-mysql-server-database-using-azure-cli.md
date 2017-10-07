---
title: "빠른 시작: MySQL용 Azure Database 서버 만들기 - Azure CLI | Microsoft Docs"
description: "이 퀵 스타트의 방법을 toouse hello Azure CLI toocreate Azure 리소스 그룹에 MySQL 서버에 대 한 Azure 데이터베이스를 설명 합니다."
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
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="93e1a-103">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기 </span><span class="sxs-lookup"><span data-stu-id="93e1a-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="93e1a-104">이 퀵 스타트의 방법을 toouse hello Azure CLI toocreate Azure 리소스 그룹에 MySQL 서버에 대 한 Azure 데이터베이스 약 5 분 후에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="93e1a-105">hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="93e1a-106">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="93e1a-107">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="93e1a-108">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="93e1a-109">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="93e1a-110">여러 구독이 있는 경우 hello 리소스 존재 하거나에 대 한 청구 hello 적절 한 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="93e1a-111">[az account set](/cli/azure/account#set) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="93e1a-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="93e1a-112">Create a resource group</span></span>
<span data-ttu-id="93e1a-113">만들기는 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) hello를 사용 하 여 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="93e1a-114">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="93e1a-115">hello 다음 예제에서는 명명 된 리소스 그룹 `myresourcegroup` hello에 `westus` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="93e1a-116">Azure Database for MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="93e1a-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="93e1a-117">Hello로 MySQL server 용 Azure 데이터베이스 만들기 **az mysql server 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="93e1a-118">서버는 여러 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-118">A server can manage multiple databases.</span></span> <span data-ttu-id="93e1a-119">일반적으로 각 프로젝트 또는 각 사용자에 대해 별도의 데이터베이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="93e1a-120">hello 다음 예제에서는 Azure 데이터베이스에 있는 MySQL 서버에 대 한 `westus` hello 리소스 그룹에 `myresourcegroup` 이름의 `myserver4demo`합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="93e1a-121">hello 서버에 관리자 로그에 명명 된 `myadmin` 및 암호 `Password01!`합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="93e1a-122">hello 생성 되 **기본** 성능 계층 및 **50** hello 서버에서 모든 hello 데이터베이스 간에 공유 되는 단위를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="93e1a-123">확장할 수 있습니다 계산 및 저장소 위나 아래로 hello 응용 프로그램 요구에 따라.</span><span class="sxs-lookup"><span data-stu-id="93e1a-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="93e1a-124">방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="93e1a-124">Configure firewall rule</span></span>
<span data-ttu-id="93e1a-125">Hello를 사용 하 여 MySQL 서버 수준 방화벽 규칙에 대 한 Azure 데이터베이스 만들기 **az mysql 서버 방화벽 규칙 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="93e1a-126">서버 수준 방화벽 규칙은 hello와 같은 외부 응용 프로그램 허용 **mysql.exe** 명령줄 도구 또는 MySQL 워크 벤치 tooconnect tooyour 서버 hello Azure MySQL 서비스 방화벽을 통해.</span><span class="sxs-lookup"><span data-stu-id="93e1a-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="93e1a-127">hello 다음 예제에서는 미리 정의 된 주소 범위는이 예제는 hello 전체 가능한 IP 주소 범위에 대 한 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="93e1a-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="93e1a-128">SSL 설정 구성</span><span class="sxs-lookup"><span data-stu-id="93e1a-128">Configure SSL settings</span></span>
<span data-ttu-id="93e1a-129">기본적으로 서버와 클라이언트 응용 프로그램 간에 SSL 연결이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="93e1a-130">이렇게 하면 "동작에서"의 보안을 통해 hello 데이터 스트림을 암호화 하 여 데이터 hello 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="93e1a-131">이 빠른 시작 쉽게 toomake, 서버에 대 한 SSL 연결 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="93e1a-132">이런 설정은 프로덕션 서버에는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="93e1a-133">자세한 내용은 참조 [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](./howto-configure-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="93e1a-134">hello 다음 예제에서는 비활성화 MySQL 서버에서 SSL을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="93e1a-135">Hello 연결 정보를 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="93e1a-135">Get hello connection information</span></span>

<span data-ttu-id="93e1a-136">tooconnect tooyour 서버 tooprovide 호스트 정보 및 액세스 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="93e1a-137">hello 결과 JSON 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-137">hello result is in JSON format.</span></span> <span data-ttu-id="93e1a-138">Hello 메모 **fullyQualifiedDomainName** 및 **administratorLogin**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="93e1a-139">Toohello 서버 hello mysql.exe 명령줄 도구를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="93e1a-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="93e1a-140">Tooyour 서버 hello를 사용 하 여 연결 **mysql.exe** 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="93e1a-141">[여기](https://dev.mysql.com/downloads/)에서 MySQL을 다운로드하여 컴퓨터에 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="93e1a-142">대신 클릭 수도 있습니다 hello **시도** 코드 샘플 단추 또는 환영 `>_` hello 상단 오른쪽에 도구 모음에서 Azure 포털 hello 및 시작 hello 단추 **Azure 클라우드 셸**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="93e1a-143">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="93e1a-144">사용 하 여 toohello 서버 연결 **mysql** 명령줄 도구:</span><span class="sxs-lookup"><span data-stu-id="93e1a-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="93e1a-145">서버 상태 보기:</span><span class="sxs-lookup"><span data-stu-id="93e1a-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="93e1a-146">모든 코드가 정상적으로 작동 하는 경우 hello 명령줄 도구 hello 텍스트 다음 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

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
> <span data-ttu-id="93e1a-147">다른 명령은 [MySQL 5.7 참조 설명서 - 4.5.1장](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93e1a-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="93e1a-148">Toohello 서버 hello MySQL 워크 벤치 GUI 도구를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="93e1a-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="93e1a-149">Hello 클라이언트 컴퓨터에서 MySQL 워크 벤치 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="93e1a-150">MySQL Workbench는 [여기](https://dev.mysql.com/downloads/workbench/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="93e1a-151">Hello에 **새 연결을 설정** 대화 상자에 입력 다음 정보는 hello **매개 변수** 탭:</span><span class="sxs-lookup"><span data-stu-id="93e1a-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![새 연결 설정](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="93e1a-153">**설정**</span><span class="sxs-lookup"><span data-stu-id="93e1a-153">**Setting**</span></span> | <span data-ttu-id="93e1a-154">**제안 값**</span><span class="sxs-lookup"><span data-stu-id="93e1a-154">**Suggested Value**</span></span> | <span data-ttu-id="93e1a-155">**설명**</span><span class="sxs-lookup"><span data-stu-id="93e1a-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="93e1a-156">연결 이름</span><span class="sxs-lookup"><span data-stu-id="93e1a-156">Connection Name</span></span> | <span data-ttu-id="93e1a-157">내 연결</span><span class="sxs-lookup"><span data-stu-id="93e1a-157">My Connection</span></span> | <span data-ttu-id="93e1a-158">이 연결에 대한 레이블 지정(아무 이름이나 가능)</span><span class="sxs-lookup"><span data-stu-id="93e1a-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="93e1a-159">연결 방법</span><span class="sxs-lookup"><span data-stu-id="93e1a-159">Connection Method</span></span> | <span data-ttu-id="93e1a-160">표준(TCP/IP) 선택</span><span class="sxs-lookup"><span data-stu-id="93e1a-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="93e1a-161">MySQL에 대 한 TCP/IP 프로토콜 tooconnect tooAzure 데이터베이스를 사용 하 여 ></span><span class="sxs-lookup"><span data-stu-id="93e1a-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="93e1a-162">호스트 이름</span><span class="sxs-lookup"><span data-stu-id="93e1a-162">Hostname</span></span> | <span data-ttu-id="93e1a-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="93e1a-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="93e1a-164">앞에서 기록한 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="93e1a-165">포트</span><span class="sxs-lookup"><span data-stu-id="93e1a-165">Port</span></span> | <span data-ttu-id="93e1a-166">3306</span><span class="sxs-lookup"><span data-stu-id="93e1a-166">3306</span></span> | <span data-ttu-id="93e1a-167">MySQL 용 hello 기본 포트가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="93e1a-168">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="93e1a-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="93e1a-169">이전에 기록한 hello 서버 관리자 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="93e1a-170">암호</span><span class="sxs-lookup"><span data-stu-id="93e1a-170">Password</span></span> | **** | <span data-ttu-id="93e1a-171">이전에 구성한 hello 관리자 계정 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="93e1a-172">클릭 **연결 테스트** tootest 모든 매개 변수가 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="93e1a-173">를 클릭 하 여 hello 연결 toosuccessfully toohello 서버에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="93e1a-174">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="93e1a-174">Clean up resources</span></span>
<span data-ttu-id="93e1a-175">빠른 시작/자습서에 대 한 이러한 리소스 필요가 없는 경우에 hello 다음 명령을 실행 하 여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e1a-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="93e1a-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93e1a-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="93e1a-177">Azure CLI로 MySQL 데이터베이스 디자인</span><span class="sxs-lookup"><span data-stu-id="93e1a-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
