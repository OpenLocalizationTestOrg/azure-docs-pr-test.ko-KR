---
title: "Azure Redis 캐시를 삭제 하는 CLI 스크립트 샘플-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="366d5-103">Azure Redis Cache 삭제</span><span class="sxs-lookup"><span data-stu-id="366d5-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="366d5-104">이 시나리오에서는 Azure Redis 캐시 하는 toodelete 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-104">In this scenario, you learn how toodelete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="366d5-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="366d5-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="366d5-106">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="366d5-106">Script explanation</span></span>

<span data-ttu-id="366d5-107">이 스크립트 명령 toodelete Azure Redis Cache 인스턴스 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-107">This script uses hello following commands toodelete an Azure Redis Cache instance.</span></span> <span data-ttu-id="366d5-108">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="366d5-109">명령</span><span class="sxs-lookup"><span data-stu-id="366d5-109">Command</span></span> | <span data-ttu-id="366d5-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="366d5-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="366d5-111">az redis delete</span><span class="sxs-lookup"><span data-stu-id="366d5-111">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="366d5-112">Redis Cache 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-112">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="366d5-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="366d5-113">Next steps</span></span>

<span data-ttu-id="366d5-114">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-114">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="366d5-115">추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="366d5-115">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
