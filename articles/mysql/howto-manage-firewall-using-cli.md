---
title: "Azure CLI를 사용한 MySQL용 Azure Database 방화벽 규칙 만들기 및 관리 | Microsoft Docs"
description: "Azure CLI 명령줄을 사용하여 MySQL용 Azure Database 방화벽 규칙을 만들고 관리하는 방법을 설명합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="7deb3-103">Azure CLI를 사용한 MySQL용 Azure Database 방화벽 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="7deb3-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="7deb3-104">관리자는 서버 수준 방화벽 규칙을 사용하여 특정 IP 주소 또는 IP 주소 범위에서 MySQL용 Azure Database 서버에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="7deb3-105">편리한 Azure CLI 명령을 사용하면 서버를 관리하는 방화벽 규칙을 만들고, 업데이트하고, 삭제하며, 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="7deb3-106">MySQL용 Azure Database 방화벽에 대한 개요는 [MySQL용 Azure Database 서버 방화벽 규칙](./concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7deb3-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7deb3-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7deb3-107">Prerequisites</span></span>
* [<span data-ttu-id="7deb3-108">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="7deb3-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="7deb3-109">PostgreSQL 및 MySQL용 Azure Python SDK 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="7deb3-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="7deb3-110">PostgreSQL 및 MySQL용 Azure CLI 구성 요소 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="7deb3-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="7deb3-111">MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="7deb3-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="7deb3-112">방화벽 규칙 명령:</span><span class="sxs-lookup"><span data-stu-id="7deb3-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="7deb3-113">**az mysql server firewall-rule** 명령은 Azure CLI에서 방화벽 규칙을 만들고, 삭제, 나열, 표시 및 업데이트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="7deb3-114">명령:</span><span class="sxs-lookup"><span data-stu-id="7deb3-114">Commands:</span></span>
- <span data-ttu-id="7deb3-115">**create**: Azure MySQL 서버 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="7deb3-116">**delete**: Azure MySQL 서버 방화벽 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="7deb3-117">**list**: Azure MySQL 서버 방화벽 규칙을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="7deb3-118">**show**: Azure MySQL 서버 방화벽 규칙의 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="7deb3-119">**update**: Azure MySQL 서버 방화벽 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="7deb3-120">Azure에 로그인 및 MySQL용 Azure Database 서버 나열</span><span class="sxs-lookup"><span data-stu-id="7deb3-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="7deb3-121">Azure 계정으로 Azure CLI를 안전하게 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="7deb3-122">**az login** 명령을 사용하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="7deb3-123">명령줄에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="7deb3-124">이 명령은 다음 단계에서 사용할 코드를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="7deb3-125">웹 브라우저를 사용하여 [https://aka.ms/devicelogin](https://aka.ms/devicelogin) 페이지를 열고 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="7deb3-126">프롬프트가 나타나면 Azure 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="7deb3-127">로그인 권한이 부여되면 구독 목록은 콘솔에 인쇄됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="7deb3-128">원하는 구독의 ID를 복사하여 앞으로 진행하는 데 사용되는 현재 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="7deb3-129">이름이 확실치 않은 경우 리소스 그룹 및 구독에 대한 MySQL용 Azure Databases 서버를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="7deb3-130">나열되는 이름 특성은 작업할 MySQL 서버가 무엇인지 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="7deb3-131">필요한 경우 이름 특성을 사용하여 이름이 올바른지 확인하기 위해 해당 서버에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="7deb3-132">MySQL용 Azure Database 서버에서 방화벽 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="7deb3-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="7deb3-133">서버 이름 및 리소스 그룹 이름을 사용하여 기존 서버 방화벽 규칙을 서버에 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="7deb3-134">서버 이름 특성은 **--name** 스위치가 아닌 **--server** 스위치에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="7deb3-135">출력은 있을 경우 기본적으로 JSON 형식으로 규칙을 나열하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="7deb3-136">더 읽기 쉬운 테이블 형식에 대해 스위치 **--output table**을 출력으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="7deb3-137">MySQL용 Azure Database 서버에서 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="7deb3-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="7deb3-138">Azure MySQL 서버 이름 및 리소스 그룹 이름을 사용하여 서버에 새로운 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="7deb3-139">규칙에 사용할 이름, 규칙에 대한 시작 IP 및 끝 IP를 제공하여 액세스를 허용할 IP 주소의 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="7deb3-140">액세스를 허용할 단일 IP 주소에 대해 이 예제에서와 같이 시작 IP 및 끝 IP와 동일한 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="7deb3-141">성공하면 명령 출력은 사용자가 만든 방화벽 규칙의 세부 정보를 기본적으로 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="7deb3-142">오류가 있는 경우 출력은 오류 메시지 텍스트를 대신 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="7deb3-143">MySQL용 Azure Database 서버에서 방화벽 규칙 업데이트</span><span class="sxs-lookup"><span data-stu-id="7deb3-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="7deb3-144">Azure MySQL 서버 이름 및 리소스 그룹 이름을 사용하여 서버에서 기존 방화벽 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="7deb3-145">기존 방화벽 규칙의 이름과 업데이트할 시작 IP 및 끝 IP 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="7deb3-146">성공하면 명령 출력은 업데이트한 방화벽 규칙의 세부 정보를 기본적으로 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="7deb3-147">오류가 있는 경우 출력은 오류 메시지 텍스트를 대신 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="7deb3-148">방화벽 규칙이 존재하지 않는 경우 업데이트 명령으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="7deb3-149">MySQL용 Azure Database 서버에서 방화벽 규칙 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="7deb3-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="7deb3-150">Azure MySQL 서버 이름 및 리소스 그룹 이름을 사용하여 서버에서 기존 방화벽 규칙 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="7deb3-151">기존 방화벽 규칙의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="7deb3-152">성공하면 명령 출력은 지정한 방화벽 규칙의 세부 정보를 기본적으로 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="7deb3-153">오류가 있는 경우 출력은 오류 메시지 텍스트를 대신 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="7deb3-154">MySQL용 Azure Database 서버에서 방화벽 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="7deb3-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="7deb3-155">Azure MySQL 서버 이름 및 리소스 그룹 이름을 사용하여 서버에서 기존 방화벽 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="7deb3-156">기존 방화벽 규칙의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="7deb3-157">성공하면 출력은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-157">Upon success, there is no output.</span></span> <span data-ttu-id="7deb3-158">실패하면 오류 메시지 텍스트가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7deb3-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7deb3-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7deb3-159">Next steps</span></span>
- <span data-ttu-id="7deb3-160">[MySQL용 Azure Database 서버 방화벽 규칙](./concepts-firewall-rules.md) 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="7deb3-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="7deb3-161">Azure Portal을 사용한 MySQL용 Azure Database 방화벽 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="7deb3-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
