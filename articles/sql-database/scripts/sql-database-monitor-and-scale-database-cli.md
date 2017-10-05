---
title: "CLI 예제 모니터링 크기 조정 단일 SQL Database | Microsoft Docs"
description: "단일 Azure SQL Database를 모니터링하고 크기를 조정하는 Azure CLI 예제 스크립트"
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="55b0f-103">CLI를 사용하여 단일 SQL Database 모니터링 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="55b0f-103">Use CLI to monitor and scale a single SQL database</span></span>

<span data-ttu-id="55b0f-104">이 Azure CLI 스크립트 예제는 데이터베이스에 대한 크기 정보를 쿼리한 후에 단일 Azure SQL Database를 다양한 성능 수준으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-104">This Azure CLI script example scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="55b0f-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="55b0f-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="55b0f-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55b0f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="55b0f-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="55b0f-108">Sample script</span></span>

<span data-ttu-id="55b0f-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "단일 SQL Database 모니터링 및 크기 조정")]</span><span class="sxs-lookup"><span data-stu-id="55b0f-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="55b0f-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="55b0f-110">Clean up deployment</span></span>

<span data-ttu-id="55b0f-111">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="55b0f-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="55b0f-112">Script explanation</span></span>

<span data-ttu-id="55b0f-113">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-113">This script uses the following commands.</span></span> <span data-ttu-id="55b0f-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="55b0f-115">명령</span><span class="sxs-lookup"><span data-stu-id="55b0f-115">Command</span></span> | <span data-ttu-id="55b0f-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="55b0f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55b0f-117">az group create</span><span class="sxs-lookup"><span data-stu-id="55b0f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="55b0f-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55b0f-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="55b0f-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="55b0f-120">데이터베이스를 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-120">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="55b0f-121">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="55b0f-121">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="55b0f-122">데이터베이스의 크기 사용량 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-122">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="55b0f-123">az sql db update</span><span class="sxs-lookup"><span data-stu-id="55b0f-123">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="55b0f-124">데이터베이스 속성(예: 서비스 계층 또는 성능 수준)을 업데이트하거나 데이터베이스 정보를 탄력적 풀로/에서 또는 탄력적 풀 간에 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-124">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="55b0f-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="55b0f-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="55b0f-126">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="55b0f-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55b0f-127">Next steps</span></span>

<span data-ttu-id="55b0f-128">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55b0f-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="55b0f-129">추가 SQL Database CLI 스크립트 샘플은 [Azure SQL Database 설명서](../sql-database-cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b0f-129">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
