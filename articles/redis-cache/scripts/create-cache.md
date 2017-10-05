---
title: "Azure CLI 스크립트 샘플 - Azure Redis Cache 만들기 | Microsoft Docs"
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
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="520e4-103">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="520e4-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="520e4-104">이 시나리오에서는 Azure Redis Cache를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="520e4-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="520e4-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="520e4-105">Sample script</span></span>

<span data-ttu-id="520e4-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="520e4-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="520e4-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="520e4-107">Script explanation</span></span>

<span data-ttu-id="520e4-108">이 스크립트는 다음 명령을 사용하여 리소스 그룹 및 Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="520e4-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="520e4-109">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="520e4-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="520e4-110">명령</span><span class="sxs-lookup"><span data-stu-id="520e4-110">Command</span></span> | <span data-ttu-id="520e4-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="520e4-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="520e4-112">az group create</span><span class="sxs-lookup"><span data-stu-id="520e4-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="520e4-113">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="520e4-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="520e4-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="520e4-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="520e4-115">Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="520e4-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="520e4-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="520e4-116">Next steps</span></span>

<span data-ttu-id="520e4-117">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="520e4-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="520e4-118">추가 Azure Redis Cache CLI 스크립트 샘플은 [Azure Redis Cache 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="520e4-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>