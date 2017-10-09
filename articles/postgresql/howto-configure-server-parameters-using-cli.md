---
title: "PostgreSQL에 대 한 Azure 데이터베이스에서 aaaConfigure hello 서비스 매개 변수 | Microsoft Docs"
description: "이 문서에서는 tooconfigure hello 서비스 매개 변수 Azure 데이터베이스에서 PostgreSQL 사용에 대 한 Azure CLI 명령줄 hello 하는 방법을 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="d4042-103">Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d4042-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="d4042-104">목록, 표시 하 고 hello 명령줄 인터페이스 (Azure CLI)를 사용 하는 Azure PostgreSQL 서버에 대 한 구성 매개 변수를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="d4042-105">그러나 엔진 구성의 하위 집합만 서버 수준에서 노출하고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d4042-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d4042-106">Prerequisites</span></span>
<span data-ttu-id="d4042-107">이 방법 tooguide 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="d4042-108">서버 및 데이터베이스 [PostgreSQL용 Azure Database 만들기](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d4042-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="d4042-109">설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티 또는 사용 하 여 Azure 클라우드 셸에에서 hello hello 브라우저.</span><span class="sxs-lookup"><span data-stu-id="d4042-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="d4042-110">PostgreSQL 서버용 Azure 데이터베이스에 대한 서버 구성 매개 변수 나열</span><span class="sxs-lookup"><span data-stu-id="d4042-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="d4042-111">서버 및 해당 값을 수정할 수 있는 모든 매개 변수가 실행 toolist hello [az postgres 서버 구성 목록](/cli/azure/postgres/server/configuration#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="d4042-112">서버 hello에 대 한 hello 서버 구성 매개 변수를 나열할 수 있습니다 **mypgserver 20170401.postgres.database.azure.com** 리소스 그룹 아래의 **myresourcegroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="d4042-113">서버 구성 매개 변수 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="d4042-113">Show server configuration parameter details</span></span>
<span data-ttu-id="d4042-114">hello를 실행 하는 서버에 대 한 특정 구성 매개 변수에 대 한 세부 정보 tooshow [az postgres 서버 구성 표시](/cli/azure/postgres/server/configuration#show) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="d4042-115">Hello에 대 한 세부 정보를 보여 주는이 예제 **로그\_min\_메시지** 서버에 대 한 서버 구성 매개 변수 **mypgserver 20170401.postgres.database.azure.com** 아래 리소스 그룹 **myresourcegroup 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d4042-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="d4042-116">서버 구성 매개 변수 값 수정</span><span class="sxs-lookup"><span data-stu-id="d4042-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="d4042-117">Hello는 특정 서버 구성 매개 변수 값을 수정할 수 있습니다 및 이렇게 hello hello PostgreSQL 서버 엔진에 대 한 기본 구성 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="d4042-118">tooupdate hello 구성 사용 하 여 hello [az postgres 서버 구성 집합](/cli/azure/postgres/server/configuration#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="d4042-119">tooupdate hello **로그\_min\_메시지** 서버의 서버 구성 매개 변수 **mypgserver 20170401.postgres.database.azure.com** 리소스그룹**myresourcegroup 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d4042-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="d4042-120">선택적 hello 아웃 tooleave tooreset hello 구성 매개 변수 값을 사용 하도록 하려는 경우 선택 하면 `--value` 매개 변수 및 hello 서비스는 hello 기본값 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="d4042-121">위의 예제에서는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="d4042-122">이렇게 하면 hello 다시 설정 **로그\_min\_메시지** 구성 toohello 기본값 **경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4042-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="d4042-123">서버 구성 및 허용되는 값에 자세한 내용은 [서버 구성](https://www.postgresql.org/docs/9.6/static/runtime-config.html)의 PostgreSQL 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4042-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4042-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4042-124">Next steps</span></span>
- <span data-ttu-id="d4042-125">tooconfigure 및 액세스 서버 로그를 참조 [PostgreSQL에 대 한 Azure 데이터베이스에서 서버 로그](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="d4042-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
