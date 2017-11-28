---
title: "PostgreSQL Azure CLI를 사용 하 여 서버 로그 aaaConfigure 및 액세스 | Microsoft Docs"
description: "이 문서에서는 PostgreSQL Azure CLI 명령줄을 사용 하 여에 대 한 tooconfigure 및 액세스 hello 서버 Azure 데이터베이스에서 로그 하는 방법을 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="9faa7-103">Azure CLI를 사용하여 서버 로그 구성 및 액세스</span><span class="sxs-lookup"><span data-stu-id="9faa7-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="9faa7-104">명령줄 인터페이스 (Azure CLI) hello를 사용 하 여 hello PostgreSQL 서버 오류 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="9faa7-105">그러나 액세스 tootransaction 로그는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9faa7-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9faa7-106">Prerequisites</span></span>
<span data-ttu-id="9faa7-107">이 방법 tooguide 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="9faa7-108">[PostgreSQL용 Azure Database 서버](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9faa7-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="9faa7-109">설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티 또는 사용 하 여 Azure 클라우드 셸에에서 hello hello 브라우저.</span><span class="sxs-lookup"><span data-stu-id="9faa7-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="9faa7-110">PostgreSQL용 Azure Database에 대한 로깅 구성</span><span class="sxs-lookup"><span data-stu-id="9faa7-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="9faa7-111">Hello 서버 tooaccess 쿼리 로그 및 오류 로그를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="9faa7-112">오류 로그에는 자동 진공, 연결 및 검사점 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="9faa7-113">로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="9faa7-113">Turn on logging</span></span>
2. <span data-ttu-id="9faa7-114">업데이트 로그\_문과 로그\_min\_기간\_문 tooenable 쿼리 로깅</span><span class="sxs-lookup"><span data-stu-id="9faa7-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="9faa7-115">보존 기간 업데이트</span><span class="sxs-lookup"><span data-stu-id="9faa7-115">Update retention period</span></span>

<span data-ttu-id="9faa7-116">자세한 내용은 [서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9faa7-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="9faa7-117">PostgreSQL용 Azure 데이터베이스 서버에 대한 로그 나열</span><span class="sxs-lookup"><span data-stu-id="9faa7-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="9faa7-118">hello 실행 서버에 대해 toolist hello 사용 가능한 로그 파일 [az postgres 서버 로그 목록](/cli/azure/postgres/server-logs#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="9faa7-119">서버에 대 한 hello 로그 파일을 나열할 수 있습니다 **mypgserver 20170401.postgres.database.azure.com** 리소스 그룹 아래의 **myresourcegroup**, 및 tooa 텍스트를 직접 라는 파일 **로그\_파일\_list.txt 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9faa7-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="9faa7-120">Hello 서버에서 로그를 로컬로 다운로드</span><span class="sxs-lookup"><span data-stu-id="9faa7-120">Download logs locally from hello server</span></span>
<span data-ttu-id="9faa7-121">hello [az postgres 서버 로그를 다운로드](/cli/azure/postgres/server-logs#download) 명령을 사용 하면 서버에 대 한 toodownload 개별 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="9faa7-122">이 예제에서는 다운로드 hello hello 서버에 대 한 특정 로그 파일 **mypgserver 20170401.postgres.database.azure.com** 리소스 그룹 아래의 **myresourcegroup** tooyour 로컬 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9faa7-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="9faa7-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9faa7-123">Next steps</span></span>
- <span data-ttu-id="9faa7-124">서버 로그에 대해 자세히 toolearn 참조 [PostgreSQL에 대 한 Azure 데이터베이스에서 서버 로그](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="9faa7-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="9faa7-125">서버 매개 변수에 대한 자세한 내용은 [Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정](howto-configure-server-parameters-using-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9faa7-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
