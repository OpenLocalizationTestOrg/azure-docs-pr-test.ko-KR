---
title: "Azure CLI 스크립트 샘플 - Azure Redis Cache 삭제 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Redis Cache 삭제"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="c3d63-103">Azure Redis Cache 삭제</span><span class="sxs-lookup"><span data-stu-id="c3d63-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="c3d63-104">이 시나리오에서는 Azure Redis Cache를 삭제하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c3d63-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="c3d63-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c3d63-105">Sample script</span></span>

<span data-ttu-id="c3d63-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="c3d63-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c3d63-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c3d63-107">Script explanation</span></span>

<span data-ttu-id="c3d63-108">이 스크립트는 다음 명령을 사용하여 Azure Redis Cache 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c3d63-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="c3d63-109">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3d63-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c3d63-110">명령</span><span class="sxs-lookup"><span data-stu-id="c3d63-110">Command</span></span> | <span data-ttu-id="c3d63-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c3d63-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c3d63-112">az redis delete</span><span class="sxs-lookup"><span data-stu-id="c3d63-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="c3d63-113">Redis Cache 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c3d63-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c3d63-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3d63-114">Next steps</span></span>

<span data-ttu-id="c3d63-115">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3d63-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c3d63-116">추가 Azure Redis Cache CLI 스크립트 샘플은 [Azure Redis Cache 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3d63-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>