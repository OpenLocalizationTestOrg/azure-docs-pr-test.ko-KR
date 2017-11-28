---
title: "aaaCreate 및 Azure CLI를 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 및 Azure CLI 명령줄을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스를 관리 합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="fd9f8-103">Azure CLI를 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="fd9f8-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="fd9f8-104">서버 수준 방화벽 규칙에서 특정 IP 주소 또는 IP 주소 범위 PostgreSQL 서버에 대 한 관리자 toomanage 액세스 tooan Azure 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="fd9f8-105">편리 하 게 Azure CLI 명령을 사용 하 여, 수를 만들고 업데이트, 삭제, 목록, 서버 방화벽 규칙 toomanage를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="fd9f8-106">PostgreSQL용 Azure Database 방화벽에 대한 개요는 [PostgreSQL용 Azure Database 서버 방화벽 규칙](concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd9f8-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fd9f8-107">Prerequisites</span></span>
<span data-ttu-id="fd9f8-108">이 방법 tooguide 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="fd9f8-109">[PostgreSQL용 Azure Database 서버 및 데이터베이스](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="fd9f8-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="fd9f8-110">설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티 또는 사용 하 여 Azure 클라우드 셸에에서 hello hello 브라우저.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="fd9f8-111">PostgreSQL용 Azure Database에 대한 서버 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="fd9f8-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="fd9f8-112">hello [az postgres 서버 방화벽 규칙](/cli/azure/postgres/server/firewall-rule) 명령을 사용 하는 tooconfigure 방화벽 규칙 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="fd9f8-113">방화벽 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="fd9f8-113">List firewall rules</span></span> 
<span data-ttu-id="fd9f8-114">hello 실행 hello 서버에 서버 방화벽 규칙 toolist hello 기존 [az postgres 서버 방화벽 규칙 목록](/cli/azure/postgres/server/firewall-rule#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="fd9f8-115">hello 출력 형식 JSON에서 기본적으로 모든 hello 규칙을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="fd9f8-116">Hello 스위치를 사용할 수 있습니다 `--output table` hello 출력으로 더 읽기 쉬운 테이블 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="fd9f8-117">방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="fd9f8-117">Create firewall rule</span></span>
<span data-ttu-id="fd9f8-118">toocreate hello를 실행 하는 hello 서버에 새 방화벽 규칙 [az postgres 서버 방화벽 규칙 만들기](/cli/azure/postgres/server/firewall-rule#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="fd9f8-119">이 예에서는 모든 IP 주소 tooaccess hello 서버 범위를 허용 **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="fd9f8-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="fd9f8-120">단일 IP 주소 tooaccess tooallow 제공 IP 시작 및 끝 IP 다음이 예제와 같이 hello 처럼 동일한 주소 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="fd9f8-121">요청이 성공 하면 hello 명령 출력 JSON 형식에서 기본적으로 만든 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="fd9f8-122">오류가 있으면 hello 대신 showserror 메시지 텍스트를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="fd9f8-123">방화벽 규칙 업데이트</span><span class="sxs-lookup"><span data-stu-id="fd9f8-123">Update firewall rule</span></span> 
<span data-ttu-id="fd9f8-124">사용 하 여 hello 서버에서 기존 방화벽 규칙 업데이트 [az postgres 서버 방화벽 규칙 업데이트](/cli/azure/postgres/server/firewall-rule#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="fd9f8-125">입력 및 시작 IP 및 끝 IP 특성 tooupdate hello로 hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="fd9f8-126">요청이 성공 하면 hello 명령 출력을 업데이트 한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="fd9f8-127">오류가 있으면 hello 대신 showserror 메시지 텍스트를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="fd9f8-128">Hello 방화벽 규칙이 없으면 hello 업데이트 명령으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="fd9f8-129">방화벽 규칙 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="fd9f8-129">Show firewall rule details</span></span>
<span data-ttu-id="fd9f8-130">표시할 수도 있습니다 hello 기존 방화벽 규칙 세부 정보는 서버에 대 한 실행 하 여 [az postgres 서버 방화벽 규칙 표시](/cli/azure/postgres/server/firewall-rule#show) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="fd9f8-131">요청이 성공 하면 hello 명령 출력을 지정한 JSON 형식에서 기본적으로 hello 방화벽 규칙의 hello 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="fd9f8-132">오류가 있으면 hello 대신 showserror 메시지 텍스트를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="fd9f8-133">방화벽 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="fd9f8-133">Delete firewall rule</span></span>
<span data-ttu-id="fd9f8-134">hello를 실행 하 여 기존 방화벽 규칙을 삭제 하는 hello 서버에서 IP 범위에 대 한 액세스 toorevoke [az postgres 서버 방화벽 규칙 삭제](/cli/azure/postgres/server/firewall-rule#delete) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="fd9f8-135">Hello 기존 방화벽 규칙의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="fd9f8-136">성공하면 출력은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-136">Upon success, there is no output.</span></span> <span data-ttu-id="fd9f8-137">실패 시 오류 메시지 텍스트 hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd9f8-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd9f8-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd9f8-138">Next steps</span></span>
- <span data-ttu-id="fd9f8-139">웹 브라우저도 사용할 수는 마찬가지로, 소개[만들기 및 hello Azure 포털을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fd9f8-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="fd9f8-140">[PostgreSQL용 Azure Database 서버 방화벽 규칙](concepts-firewall-rules.md) 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="fd9f8-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="fd9f8-141">PostgreSQL 서버에 대 한 tooan Azure 데이터베이스 연결에 대 한 도움말을 참조 하십시오. [PostgreSQL에 대 한 Azure 데이터베이스에 대 한 연결 라이브러리](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="fd9f8-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
