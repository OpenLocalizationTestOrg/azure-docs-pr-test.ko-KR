---
title: "aaaCreate 및 Azure CLI를 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 및 Azure CLI 명령줄을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스를 관리 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="268dc-103">Azure CLI를 사용한 MySQL용 Azure Database 방화벽 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="268dc-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="268dc-104">특정 IP 주소 또는 IP 주소 범위에서 MySQL Server에 대 한 관리자 toomanage 액세스 tooan Azure 데이터베이스를 사용 하는 서버 수준 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="268dc-105">편리 하 게 Azure CLI 명령을 사용 하 여, 수를 만들고 업데이트, 삭제, 목록, 서버 방화벽 규칙 toomanage를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="268dc-106">MySQL용 Azure Database 방화벽에 대한 개요는 [MySQL용 Azure Database 서버 방화벽 규칙](./concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="268dc-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="268dc-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="268dc-107">Prerequisites</span></span>
* [<span data-ttu-id="268dc-108">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="268dc-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="268dc-109">PostgreSQL 및 MySQL용 Azure Python SDK 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="268dc-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="268dc-110">PostgreSQL 및 MySQL 서비스에 대 한 hello Azure CLI 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="268dc-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="268dc-111">Azure Database for MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="268dc-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="268dc-112">방화벽 규칙 명령:</span><span class="sxs-lookup"><span data-stu-id="268dc-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="268dc-113">hello **az mysql 서버 방화벽 규칙** Azure CLI toocreate에서 명령을 사용 하는, 삭제, 나열, 표시 및 방화벽 규칙을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="268dc-114">명령:</span><span class="sxs-lookup"><span data-stu-id="268dc-114">Commands:</span></span>
- <span data-ttu-id="268dc-115">**create**: Azure MySQL 서버 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="268dc-116">**delete**: Azure MySQL 서버 방화벽 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="268dc-117">**목록** : hello Azure MySQL 서버 방화벽 규칙을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="268dc-118">**표시** : 방화벽 규칙의 Azure의 MySQL server hello 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="268dc-119">**update**: Azure MySQL 서버 방화벽 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="268dc-120">로그인 tooAzure 및 MySQL Server에 대 한 Azure 데이터베이스 목록</span><span class="sxs-lookup"><span data-stu-id="268dc-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="268dc-121">Azure 계정으로 Azure CLI를 안전하게 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="268dc-122">사용 하 여 hello **az 로그인** toodo이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="268dc-123">Hello hello 명령줄에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="268dc-124">이 명령은 hello 다음 단계에서 코드 toouse를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="268dc-125">웹 브라우저 tooopen hello 페이지를 사용 하 여 [https://aka.ms/devicelogin](https://aka.ms/devicelogin) hello 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="268dc-126">Hello 프롬프트에서 Azure 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="268dc-127">사용자의 로그인에 게 권한이 부여 되 면 hello 콘솔에서 구독 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="268dc-128">원하는 hello 구독 tooset hello 현재 구독 toobe 사용 일경의 hello id를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="268dc-129">Hello 이름의 확실 하지 않은 경우에 구독 및 리소스 그룹에 대 한 MySQL server에 대 한 hello Azure 데이터베이스를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="268dc-130">Hello 사용된 toospecify 됩니다 목록은 hello에 name 특성에는 MySQL server toowork를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="268dc-131">필요한 경우 해당 서버 toousing hello 이름 특성 tooconfirm 이름 형식이 hello 세부 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="268dc-132">MySQL용 Azure Database 서버에서 방화벽 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="268dc-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="268dc-133">Hello 서버 이름 및 hello 리소스 그룹 이름 목록 hello 기존 서버 방화벽 규칙 hello 서버에서 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="268dc-134">Hello에 해당 hello 서버 이름 특성에 지정 됩니다 **-서버** 전환한 하지 hello **-이름** 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="268dc-135">hello 출력은 JSON에서 기본적으로 모든 형식 hello 규칙을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="268dc-136">Hello 스위치를 사용할 수 있습니다 **-출력 테이블** hello 출력으로 더 읽기 쉬운 테이블 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="268dc-137">MySQL용 Azure Database 서버에서 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="268dc-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="268dc-138">Hello Azure MySQL 서버 이름 및 hello 리소스 그룹 이름을 사용 하 여, hello 서버에 새 방화벽 규칙을 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="268dc-139">Hello 규칙 toocover 범위의 IP 주소 tooallow 액세스에 대 한 hello 규칙, hello 시작 IP 및 끝 IP에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="268dc-140">단일 IP 주소에 대 대 한 액세스가 허용 toobe, 제공 IP 시작 및 끝 IP 다음이 예제와 같이 hello 처럼 동일한 주소 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="268dc-141">요청이 성공 하면 hello 명령 출력은 JSON 형식에서 기본적으로 만든 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="268dc-142">오류가 있으면 hello 출력 대신 오류 메시지 텍스트로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="268dc-143">MySQL용 Azure Database 서버에서 방화벽 규칙 업데이트</span><span class="sxs-lookup"><span data-stu-id="268dc-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="268dc-144">서버 이름 및 hello 리소스 그룹 이름은 hello 서버에서 기존 방화벽 규칙을 업데이트 hello Azure MySQL을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="268dc-145">입력 및 시작 IP 및 끝 IP 특성 tooupdate hello로 hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="268dc-146">요청이 성공 하면 hello 명령 출력을 업데이트 한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="268dc-147">오류가 있으면 hello 출력 대신 오류 메시지 텍스트로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="268dc-148">Hello 방화벽 규칙이 존재 하지 않습니다 hello 업데이트 명령으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="268dc-149">MySQL용 Azure Database 서버에서 방화벽 규칙 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="268dc-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="268dc-150">Hello Azure MySQL 서버 이름 및 hello 리소스 그룹 이름을 사용 하 여, hello 기존 방화벽 규칙 세부 정보 hello 서버에서 표시할 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="268dc-151">Hello 이름 hello 기존 방화벽 규칙의 입력으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="268dc-152">요청이 성공 하면 hello 명령 출력은 사용자가 지정한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="268dc-153">오류가 있으면 hello 출력 대신 오류 메시지 텍스트로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="268dc-154">MySQL용 Azure Database 서버에서 방화벽 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="268dc-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="268dc-155">Hello Azure MySQL을 사용 하 여 서버 이름 및 hello 리소스 그룹 이름은 기존 방화벽 규칙에서에서 제거 hello 서버 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="268dc-156">Hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="268dc-157">성공하면 출력은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-157">Upon success, there is no output.</span></span> <span data-ttu-id="268dc-158">실패 시 hello 오류 메시지 텍스트를 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="268dc-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="268dc-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="268dc-159">Next steps</span></span>
- <span data-ttu-id="268dc-160">[MySQL용 Azure Database 서버 방화벽 규칙](./concepts-firewall-rules.md) 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="268dc-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="268dc-161">만들기 및 hello Azure 포털을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="268dc-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
