---
title: "CLI 예제 Azure SQL Database 이동 SQL 탄력적 풀 | Microsoft Docs"
description: "SQL 탄력적 풀에서 SQL Database를 이동하는 Azure CLI 예제 스크립트"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="faced-103">CLI를 사용하여 SQL 탄력적 풀에서 Azure SQL Database 이동</span><span class="sxs-lookup"><span data-stu-id="faced-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="faced-104">이 Azure CLI 스크립트 예제는 두 개의 탄력적 풀을 만들고 한 SQL 탄력적 풀에서 다른 SQL 탄력적 풀로 Azure SQL Database를 이동한 다음 탄력적 풀의 데이터베이스를 단일 Azure 데이터베이스 성능 수준으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="faced-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="faced-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="faced-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="faced-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="faced-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="faced-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="faced-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="faced-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="faced-108">Sample script</span></span>

<span data-ttu-id="faced-109">[!code-azurecli-interactive[기본](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "풀 간에 데이터베이스 이동")]</span><span class="sxs-lookup"><span data-stu-id="faced-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="faced-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="faced-110">Clean up deployment</span></span>

<span data-ttu-id="faced-111">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faced-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="faced-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="faced-112">Script explanation</span></span>

<span data-ttu-id="faced-113">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="faced-113">This script uses the following commands.</span></span> <span data-ttu-id="faced-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="faced-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="faced-115">명령</span><span class="sxs-lookup"><span data-stu-id="faced-115">Command</span></span> | <span data-ttu-id="faced-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="faced-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="faced-117">az group create</span><span class="sxs-lookup"><span data-stu-id="faced-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="faced-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faced-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="faced-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="faced-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="faced-120">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faced-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="faced-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="faced-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="faced-122">논리 서버 내에 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faced-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="faced-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="faced-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="faced-124">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faced-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="faced-125">az sql db update</span><span class="sxs-lookup"><span data-stu-id="faced-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="faced-126">데이터베이스 속성을 업데이트하거나 탄력적 풀로/에서 또는 탄력적 풀 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="faced-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="faced-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="faced-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="faced-128">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="faced-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="faced-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="faced-129">Next steps</span></span>

<span data-ttu-id="faced-130">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="faced-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="faced-131">추가 SQL Database CLI 스크립트 샘플은 [Azure SQL Database 설명서](../sql-database-cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faced-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


