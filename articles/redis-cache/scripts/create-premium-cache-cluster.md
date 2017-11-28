---
title: "aaaAzure CLI 스크립트 샘플-클러스터링과 함께 프리미엄 Azure Redis 캐시 만들기 | Microsoft Docs"
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
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="8fd09-103">클러스터링이 포함된 프리미엄 Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="8fd09-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="8fd09-104">이 시나리오에서는 어떻게 toocreate 6GB Premium 계층 Azure Redis Cache 클러스터링과 함께 사용 하 고 두 개의 분할 된 데이터베이스를 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd09-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="8fd09-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8fd09-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8fd09-106">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8fd09-106">Script explanation</span></span>

<span data-ttu-id="8fd09-107">이 스크립트를 사용 명령 toocreate 다음 hello 리소스 그룹 및 프리미엄 계층 redis 캐시 클러스터링 사용.</span><span class="sxs-lookup"><span data-stu-id="8fd09-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="8fd09-108">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd09-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8fd09-109">명령</span><span class="sxs-lookup"><span data-stu-id="8fd09-109">Command</span></span> | <span data-ttu-id="8fd09-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8fd09-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8fd09-111">az group create</span><span class="sxs-lookup"><span data-stu-id="8fd09-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8fd09-112">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fd09-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8fd09-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="8fd09-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="8fd09-114">Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fd09-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8fd09-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8fd09-115">Next steps</span></span>

<span data-ttu-id="8fd09-116">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd09-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8fd09-117">추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fd09-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
