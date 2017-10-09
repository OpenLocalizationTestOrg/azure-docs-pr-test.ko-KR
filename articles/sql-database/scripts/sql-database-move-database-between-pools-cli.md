---
title: "aaaCLI 예제 이동 Azure SQL 데이터베이스 SQL 탄력적인 풀 | Microsoft Docs"
description: "Azure CLI 예제 스크립트 toomove SQL 탄력적 풀의 SQL 데이터베이스"
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
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="c91e0-103">SQL 탄력적인 풀에 CLI toomove Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c91e0-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="c91e0-104">이 Azure CLI 스크립트 예에서는 두 탄력적 풀을 만듭니다 및 Azure SQL 데이터베이스 하나 SQL 탄력적 풀에서 다른 SQL 탄력적 풀으로 이동한 다음 탄력적 풀 tooa 단일 Azure 데이터베이스 성능 수준을 벗어났습니다 hello 데이터베이스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c91e0-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c91e0-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c91e0-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c91e0-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c91e0-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c91e0-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="c91e0-109">Clean up deployment</span></span>

<span data-ttu-id="c91e0-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c91e0-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c91e0-111">Script explanation</span></span>

<span data-ttu-id="c91e0-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-112">This script uses hello following commands.</span></span> <span data-ttu-id="c91e0-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c91e0-114">명령</span><span class="sxs-lookup"><span data-stu-id="c91e0-114">Command</span></span> | <span data-ttu-id="c91e0-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c91e0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c91e0-116">az group create</span><span class="sxs-lookup"><span data-stu-id="c91e0-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c91e0-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c91e0-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="c91e0-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="c91e0-119">데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c91e0-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="c91e0-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="c91e0-121">Hello 논리 서버 내에서 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="c91e0-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="c91e0-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="c91e0-123">논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="c91e0-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="c91e0-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="c91e0-125">데이터베이스 속성을 업데이트하거나 탄력적 풀로/에서 또는 탄력적 풀 간에 데이터베이스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="c91e0-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="c91e0-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c91e0-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c91e0-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c91e0-128">Next steps</span></span>

<span data-ttu-id="c91e0-129">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c91e0-130">추가 SQL 데이터베이스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 설명서](../sql-database-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c91e0-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


