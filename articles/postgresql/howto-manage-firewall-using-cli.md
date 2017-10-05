---
title: "Azure CLI를 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 명령줄을 사용하여 PostgreSQL용 Azure 데이터베이스 방화벽 규칙을 만들고 관리하는 방법을 설명합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="0e133-103">Azure CLI를 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="0e133-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="0e133-104">관리자는 서버 수준 방화벽 규칙을 사용하여 특정 IP 주소 또는 IP 주소 범위에서 PostgreSQL용 Azure Database 서버에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="0e133-105">편리한 Azure CLI 명령을 사용하면 서버를 관리하는 방화벽 규칙을 만들고, 업데이트하고, 삭제하며, 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="0e133-106">PostgreSQL용 Azure Database 방화벽에 대한 개요는 [PostgreSQL용 Azure Database 서버 방화벽 규칙](concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e133-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e133-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0e133-107">Prerequisites</span></span>
<span data-ttu-id="0e133-108">이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="0e133-109">[PostgreSQL용 Azure Database 서버 및 데이터베이스](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0e133-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="0e133-110">[Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티를 설치하거나, 브라우저에서 Azure Cloud Shell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="0e133-111">PostgreSQL용 Azure Database에 대한 서버 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="0e133-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="0e133-112">[az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) 명령은 방화벽 규칙을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="0e133-113">방화벽 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="0e133-113">List firewall rules</span></span> 
<span data-ttu-id="0e133-114">서버의 기존 서버 방화벽 규칙을 나열하려면 [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="0e133-115">출력에 기본적으로 JSON 형식으로 규칙(있는 경우)이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="0e133-116">읽기 쉬운 테이블 형식으로 출력하기 위해 `--output table` 스위치를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="0e133-117">방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="0e133-117">Create firewall rule</span></span>
<span data-ttu-id="0e133-118">서버에 새 방화벽 규칙을 만들려면 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="0e133-119">이 예제에서는 모든 IP 주소 범위에서 **mypgserver-20170401.postgres.database.azure.com** 서버에 액세스하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="0e133-120">단일 IP 주소의 액세스를 허용하려면 이 예제에서와 같이 시작 IP 및 끝 IP와 동일한 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="0e133-121">성공하면 명령 출력은 사용자가 만든 방화벽 규칙의 세부 정보를 기본적으로 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="0e133-122">오류가 있는 경우 출력은 오류 메시지 텍스트를 대신 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="0e133-123">방화벽 규칙 업데이트</span><span class="sxs-lookup"><span data-stu-id="0e133-123">Update firewall rule</span></span> 
<span data-ttu-id="0e133-124">[az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) 명령을 사용하여 서버에서 기존 방화벽 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="0e133-125">기존 방화벽 규칙의 이름과 업데이트할 시작 IP 및 끝 IP 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="0e133-126">성공하면 명령 출력은 업데이트한 방화벽 규칙의 세부 정보를 기본적으로 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="0e133-127">오류가 있는 경우 출력은 오류 메시지 텍스트를 대신 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="0e133-128">방화벽 규칙이 존재하지 않는 경우 업데이트 명령으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="0e133-129">방화벽 규칙 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="0e133-129">Show firewall rule details</span></span>
<span data-ttu-id="0e133-130">[az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) 명령을 실행하여 서버에 대한 기존 방화벽 규칙 세부 정보를 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="0e133-131">성공하면 명령 출력은 지정한 방화벽 규칙의 세부 정보를 기본적으로 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="0e133-132">오류가 있는 경우 출력은 오류 메시지 텍스트를 대신 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="0e133-133">방화벽 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="0e133-133">Delete firewall rule</span></span>
<span data-ttu-id="0e133-134">서버에서 IP 범위에 대한 액세스를 해지하려면 [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) 명령을 실행하여 기존 방화벽 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="0e133-135">기존 방화벽 규칙의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="0e133-136">성공하면 출력은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-136">Upon success, there is no output.</span></span> <span data-ttu-id="0e133-137">실패하면 오류 메시지 텍스트가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e133-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e133-138">Next steps</span></span>
- <span data-ttu-id="0e133-139">마찬가지로 웹 브라우저를 통해 [Azure Portal을 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리](howto-manage-firewall-using-portal.md)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e133-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="0e133-140">[PostgreSQL용 Azure Database 서버 방화벽 규칙](concepts-firewall-rules.md) 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="0e133-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="0e133-141">PostgreSQL용 Azure Database 서버 연결에 대한 도움말은 [PostgreSQL용 Azure Database에 대한 연결 라이브러리](concepts-connection-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e133-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
