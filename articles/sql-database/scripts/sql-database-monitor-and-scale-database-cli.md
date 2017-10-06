---
title: "aaaCLI 예제 모니터-눈금 단일 Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure CLI 예제 스크립트 toomonitor 및 소수 자릿수는 단일 Azure SQL 데이터베이스"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="fb7d3-103">CLI toomonitor를 사용 하 고 단일 SQL 데이터베이스 확장</span><span class="sxs-lookup"><span data-stu-id="fb7d3-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="fb7d3-104">Azure CLI 스크립트 예제는 hello 데이터베이스의 hello 크기 정보를 쿼리 한 후 단일 Azure SQL 데이터베이스 tooa 다양 한 성능 수준을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb7d3-105">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fb7d3-106">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fb7d3-107">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fb7d3-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="fb7d3-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fb7d3-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="fb7d3-109">Clean up deployment</span></span>

<span data-ttu-id="fb7d3-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fb7d3-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="fb7d3-111">Script explanation</span></span>

<span data-ttu-id="fb7d3-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-112">This script uses hello following commands.</span></span> <span data-ttu-id="fb7d3-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb7d3-114">명령</span><span class="sxs-lookup"><span data-stu-id="fb7d3-114">Command</span></span> | <span data-ttu-id="fb7d3-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fb7d3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb7d3-116">az group create</span><span class="sxs-lookup"><span data-stu-id="fb7d3-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fb7d3-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fb7d3-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="fb7d3-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="fb7d3-119">데이터베이스를 호스트하는 논리 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="fb7d3-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="fb7d3-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="fb7d3-121">데이터베이스에 대 한 hello 크기 사용 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="fb7d3-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="fb7d3-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="fb7d3-123">데이터베이스 속성 (예: hello 서비스 계층 또는 성능 수준)을 업데이트 하거나 위치, 부재 중 또는 탄력적 풀 간에 데이터베이스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="fb7d3-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="fb7d3-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fb7d3-125">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="fb7d3-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb7d3-126">Next steps</span></span>

<span data-ttu-id="fb7d3-127">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb7d3-128">추가 SQL 데이터베이스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 설명서](../sql-database-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb7d3-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
