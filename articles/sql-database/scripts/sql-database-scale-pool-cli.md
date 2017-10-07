---
title: "SQL 탄력적인 풀 Azure SQL 데이터베이스를 조정 하는 예제 aaaCLI | Microsoft Docs"
description: "Azure CLI 예제 스크립트 tooscale Azure SQL 데이터베이스에서 SQL 탄력적인 풀"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="3a92e-103">CLI tooscale Azure SQL 데이터베이스에서 SQL 탄력적인 풀을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3a92e-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="3a92e-104">이 Azure CLI 스크립트 예제는 SQL 탄력적 풀을 만들고 풀된 Database를 이동한하며 탄력적 풀 성능 수준을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3a92e-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3a92e-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3a92e-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3a92e-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3a92e-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3a92e-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3a92e-109">Clean up deployment</span></span>

<span data-ttu-id="3a92e-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3a92e-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3a92e-111">Script explanation</span></span>

<span data-ttu-id="3a92e-112">이 스크립트 명령 toocreate 리소스 그룹, 논리 서버, SQL 데이터베이스 및 방화벽 규칙을 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="3a92e-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3a92e-114">명령</span><span class="sxs-lookup"><span data-stu-id="3a92e-114">Command</span></span> | <span data-ttu-id="3a92e-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3a92e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a92e-116">az group create</span><span class="sxs-lookup"><span data-stu-id="3a92e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3a92e-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a92e-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="3a92e-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="3a92e-119">Hello SQL 데이터베이스를 호스트 하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="3a92e-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="3a92e-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="3a92e-121">Hello 논리 서버 내에서 탄력적 데이터베이스 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="3a92e-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="3a92e-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="3a92e-123">논리 서버 hello에에서 hello SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="3a92e-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="3a92e-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="3a92e-125">이 예제에서는 변경 내용 hello edtu로 할당에서 탄력적 데이터베이스 풀을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="3a92e-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="3a92e-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3a92e-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a92e-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a92e-128">Next steps</span></span>

<span data-ttu-id="3a92e-129">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3a92e-130">추가 SQL 데이터베이스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 설명서](../sql-database-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a92e-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
