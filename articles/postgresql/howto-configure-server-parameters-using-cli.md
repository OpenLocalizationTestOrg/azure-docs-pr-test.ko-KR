---
title: "PostgreSQL용 Azure Database에서 서비스 매개 변수 구성 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 명령줄을 사용하여 PostgreSQL용 Azure 데이터베이스에서 서비스 매개 변수를 구성하는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="32f2b-103">Azure CLI를 사용하여 서버 구성 매개 변수 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="32f2b-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="32f2b-104">Azure CLI(명령줄 인터페이스)를 사용하여 Azure PostgreSQL 서버의 구성 매개 변수를 나열하고, 표시하며, 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="32f2b-105">그러나 엔진 구성의 하위 집합만 서버 수준에서 노출하고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="32f2b-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32f2b-106">Prerequisites</span></span>
<span data-ttu-id="32f2b-107">이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="32f2b-108">서버 및 데이터베이스 [PostgreSQL용 Azure Database 만들기](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="32f2b-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="32f2b-109">[Azure CLI 2.0](/cli/azure/install-azure-cli) 명령줄 유틸리티를 설치하거나, 브라우저에서 Azure Cloud Shell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="32f2b-110">PostgreSQL 서버용 Azure 데이터베이스에 대한 서버 구성 매개 변수 나열</span><span class="sxs-lookup"><span data-stu-id="32f2b-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="32f2b-111">서버의 수정 가능한 모든 매개 변수와 해당 값을 나열하려면 [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="32f2b-112">리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 서버 구성 매개 변수를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="32f2b-113">서버 구성 매개 변수 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="32f2b-113">Show server configuration parameter details</span></span>
<span data-ttu-id="32f2b-114">서버에 대한 특정 구성 매개 변수의 세부 정보를 표시하려면 [az postgres server configuration show](/cli/azure/postgres/server/configuration#show) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="32f2b-115">이 예에서는 리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버에 대한 **log\_min\_messages** 서버 구성 매개 변수의 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="32f2b-116">서버 구성 매개 변수 값 수정</span><span class="sxs-lookup"><span data-stu-id="32f2b-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="32f2b-117">특정 서버 구성 매개 변수의 값을 수정할 수 있습니다. 그러면 PostgreSQL 서버 엔진에 대한 기본 구성 값이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="32f2b-118">구성 값을 업데이트하려면 [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="32f2b-119">리소스 그룹 **myresourcegroup**에 있는 **mypgserver-20170401.postgres.database.azure.com** 서버의 **log\_min\_messages** 서버 구성 매개 변수를 업데이트하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="32f2b-120">구성 매개 변수 값을 다시 설정하려는 경우 선택 사항인 `--value` 매개 변수를 유지하도록 선택하기만 하면 서비스에서 기본 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="32f2b-121">위의 예제에서는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="32f2b-122">이렇게 하면 **log\_min\_messages** 구성이 기본값 **WARNING**으로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f2b-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="32f2b-123">서버 구성 및 허용되는 값에 자세한 내용은 [서버 구성](https://www.postgresql.org/docs/9.6/static/runtime-config.html)의 PostgreSQL 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32f2b-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32f2b-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32f2b-124">Next steps</span></span>
- <span data-ttu-id="32f2b-125">서버 로그를 구성하고 액세스하려면 [PostgreSQL용 Azure Database의 서버 로그](concepts-server-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32f2b-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
