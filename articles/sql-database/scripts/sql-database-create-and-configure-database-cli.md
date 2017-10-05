---
title: "CLI 예제 Azure SQL Database 만들기 | Microsoft Docs"
description: "SQL Database를 만드는 Azure CLI 예제 스크립트"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="32a38-103">CLI를 사용하여 단일 Azure SQL Database 만들기 및 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="32a38-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="32a38-104">이 Azure CLI 스크립트 예제는 Azure SQL Database를 만들고 서버 수준 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="32a38-105">스크립트가 성공적으로 실행되면 모든 Azure 서비스 및 구성된 IP 주소에서 SQL Database에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="32a38-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="32a38-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="32a38-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32a38-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="32a38-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="32a38-109">Sample script</span></span>

<span data-ttu-id="32a38-110">[!code-azurecli-interactive[기본](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "SQL Database 만들기")]</span><span class="sxs-lookup"><span data-stu-id="32a38-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="32a38-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="32a38-111">Clean up deployment</span></span>

<span data-ttu-id="32a38-112">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="32a38-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="32a38-113">Script explanation</span></span>

<span data-ttu-id="32a38-114">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-114">This script uses the following commands.</span></span> <span data-ttu-id="32a38-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="32a38-116">명령</span><span class="sxs-lookup"><span data-stu-id="32a38-116">Command</span></span> | <span data-ttu-id="32a38-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="32a38-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="32a38-118">az group create</span><span class="sxs-lookup"><span data-stu-id="32a38-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="32a38-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="32a38-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="32a38-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="32a38-121">SQL Database를 호스팅하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="32a38-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="32a38-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="32a38-123">입력한 IP 주소 범위의 서버에서 모든 SQL Database에 액세스할 수 있도록 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="32a38-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="32a38-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="32a38-125">논리 서버에 SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="32a38-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="32a38-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="32a38-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="32a38-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32a38-128">Next steps</span></span>

<span data-ttu-id="32a38-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32a38-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="32a38-130">추가 SQL Database CLI 스크립트 샘플은 [Azure SQL Database 설명서](../sql-database-cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32a38-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

