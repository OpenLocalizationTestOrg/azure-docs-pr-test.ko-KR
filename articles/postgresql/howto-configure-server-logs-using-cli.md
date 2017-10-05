---
title: "Azure CLI를 사용하여 PostgreSQL용 서버 로그 구성 및 액세스 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 명령줄을 사용하여 PostgreSQL용 Azure 데이터베이스의 서버 로그를 구성 및 액세스하는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="d2430-103">Azure CLI를 사용하여 서버 로그 구성 및 액세스</span><span class="sxs-lookup"><span data-stu-id="d2430-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="d2430-104">Azure CLI(명령줄 인터페이스)를 사용하여 PostgreSQL 서버 오류 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="d2430-105">그러나 트랜잭션 로그에 대한 액세스는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d2430-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2430-106">Prerequisites</span></span>
<span data-ttu-id="d2430-107">이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="d2430-108">[PostgreSQL용 Azure Database 서버](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d2430-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="d2430-109">[Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티를 설치하거나, 브라우저에서 Azure Cloud Shell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="d2430-110">PostgreSQL용 Azure Database에 대한 로깅 구성</span><span class="sxs-lookup"><span data-stu-id="d2430-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="d2430-111">쿼리 로그 및 오류 로그에 액세스하도록 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="d2430-112">오류 로그에는 자동 진공, 연결 및 검사점 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="d2430-113">로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="d2430-113">Turn on logging</span></span>
2. <span data-ttu-id="d2430-114">log\_statement and log\_min\_duration\_statement를 업데이트하여 쿼리 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="d2430-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="d2430-115">보존 기간 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2430-115">Update retention period</span></span>

<span data-ttu-id="d2430-116">자세한 내용은 [서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2430-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="d2430-117">PostgreSQL용 Azure 데이터베이스 서버에 대한 로그 나열</span><span class="sxs-lookup"><span data-stu-id="d2430-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="d2430-118">서버에 대한 사용 가능한 로그 파일을 나열하려면 [az postgres server-logs list](/cli/azure/postgres/server-logs#list) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="d2430-119">리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 로그 파일을 나열하고 **log\_files\_list.txt**라는 텍스트 파일로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="d2430-120">로그를 서버에서 로컬로 다운로드</span><span class="sxs-lookup"><span data-stu-id="d2430-120">Download logs locally from the server</span></span>
<span data-ttu-id="d2430-121">[az postgres server-logs download](/cli/azure/postgres/server-logs#download) 명령을 사용하여 서버에 대한 개별 로그 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="d2430-122">이 예제에서는 리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 특정 로그 파일을 로컬 환경으로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2430-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="d2430-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2430-123">Next steps</span></span>
- <span data-ttu-id="d2430-124">서버 로그에 대한 자세한 내용은 [PostgreSQL용 Azure Database의 서버 로그](concepts-server-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2430-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="d2430-125">서버 매개 변수에 대한 자세한 내용은 [Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2430-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
