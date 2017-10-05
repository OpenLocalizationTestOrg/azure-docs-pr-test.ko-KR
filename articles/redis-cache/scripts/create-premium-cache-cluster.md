---
title: "Azure CLI 스크립트 샘플 - 클러스터링이 포함된 프리미엄 Azure Redis Cache 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 클러스터링이 포함된 프리미엄 계층 Azure Redis Cache 만들기"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="55095-103">클러스터링이 포함된 프리미엄 Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="55095-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="55095-104">이 시나리오에서는 활성화된 클러스터링 및 2개의 분할이 포함된 6GB 프리미엄 계층 Azure Redis Cache를 만드는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="55095-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="55095-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="55095-105">Sample script</span></span>

<span data-ttu-id="55095-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="55095-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="55095-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="55095-107">Script explanation</span></span>

<span data-ttu-id="55095-108">이 스크립트는 다음 명령을 사용하여 리소스 그룹과 클러스터링 활성화가 포함된 프리미엄 계층 Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55095-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="55095-109">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="55095-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="55095-110">명령</span><span class="sxs-lookup"><span data-stu-id="55095-110">Command</span></span> | <span data-ttu-id="55095-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="55095-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55095-112">az group create</span><span class="sxs-lookup"><span data-stu-id="55095-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="55095-113">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55095-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55095-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="55095-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="55095-115">Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55095-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="55095-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55095-116">Next steps</span></span>

<span data-ttu-id="55095-117">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55095-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="55095-118">추가 Azure Redis Cache CLI 스크립트 샘플은 [Azure Redis Cache 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55095-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>