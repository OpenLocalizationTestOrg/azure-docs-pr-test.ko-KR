---
title: "aaaAzure CLI 스크립트 샘플-Azure Redis Cache 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Redis Cache 만들기"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="ed092-103">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="ed092-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="ed092-104">이 시나리오에서는 Azure Redis 캐시 하는 toocreate 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="ed092-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ed092-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ed092-106">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ed092-106">Script explanation</span></span>

<span data-ttu-id="ed092-107">이 스크립트는 리소스 그룹 및 redis 캐시 명령을 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="ed092-108">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ed092-109">명령</span><span class="sxs-lookup"><span data-stu-id="ed092-109">Command</span></span> | <span data-ttu-id="ed092-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ed092-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ed092-111">az group create</span><span class="sxs-lookup"><span data-stu-id="ed092-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ed092-112">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ed092-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="ed092-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="ed092-114">Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ed092-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed092-115">Next steps</span></span>

<span data-ttu-id="ed092-116">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ed092-117">추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed092-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
