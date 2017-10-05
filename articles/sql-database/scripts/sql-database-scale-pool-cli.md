---
title: "CLI 예제 SQL 탄력적 풀 크기 조정 - Azure SQL Database | Microsoft Docs"
description: "Azure SQL Database에서 SQL 탄력적 풀의 크기를 조정하는 Azure CLI 예제 스크립트"
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
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="0b8dd-103">CLI를 사용하여 Azure SQL Database에서 SQL 탄력적 풀의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0b8dd-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="0b8dd-104">이 Azure CLI 스크립트 예제는 SQL 탄력적 풀을 만들고 풀된 Database를 이동한하며 탄력적 풀 성능 수준을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0b8dd-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0b8dd-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="0b8dd-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0b8dd-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0b8dd-108">Sample script</span></span>

<span data-ttu-id="0b8dd-109">[!code-azurecli-interactive[기본](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "풀 간에 데이터베이스 이동")]</span><span class="sxs-lookup"><span data-stu-id="0b8dd-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0b8dd-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0b8dd-110">Clean up deployment</span></span>

<span data-ttu-id="0b8dd-111">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0b8dd-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0b8dd-112">Script explanation</span></span>

<span data-ttu-id="0b8dd-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 논리 서버, SQL Database 및 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="0b8dd-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b8dd-115">명령</span><span class="sxs-lookup"><span data-stu-id="0b8dd-115">Command</span></span> | <span data-ttu-id="0b8dd-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0b8dd-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b8dd-117">az group create</span><span class="sxs-lookup"><span data-stu-id="0b8dd-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0b8dd-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0b8dd-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="0b8dd-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="0b8dd-120">SQL Database를 호스팅하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="0b8dd-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="0b8dd-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="0b8dd-122">논리 서버 내에서 Elastic Database 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="0b8dd-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="0b8dd-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="0b8dd-124">논리 서버에 SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="0b8dd-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="0b8dd-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="0b8dd-126">Elastic Database 풀을 업데이트하고 이 예제에서 할당된 eDTU를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="0b8dd-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="0b8dd-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0b8dd-128">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b8dd-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b8dd-129">Next steps</span></span>

<span data-ttu-id="0b8dd-130">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0b8dd-131">추가 SQL Database CLI 스크립트 샘플은 [Azure SQL Database 설명서](../sql-database-cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8dd-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
