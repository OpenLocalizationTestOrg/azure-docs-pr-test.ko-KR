---
title: "CLI 스크립트 샘플-Azure Redis Cache의 세부 정보를 가져올 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Redis Cache의 세부 정보 가져오기"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3ad1fdf000bbab52e84dbf9f002a5e9fa6d347a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="f39b8-103">Azure Redis Cache의 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="f39b8-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="f39b8-104">이 시나리오에서는 해당 프로 비전 상태를 포함 하 여 Azure Redis Cache의 tooretrieve hello 세부 정보 인스턴스 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f39b8-104">In this scenario, you learn how tooretrieve hello details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f39b8-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f39b8-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]

## <a name="script-explanation"></a><span data-ttu-id="f39b8-106">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f39b8-106">Script explanation</span></span>

<span data-ttu-id="f39b8-107">이 스크립트는 다음 명령을 tooretrieve hello 세부 정보는 Azure Redis 캐시 인스턴스의 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f39b8-107">This script uses hello following commands tooretrieve hello details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="f39b8-108">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f39b8-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f39b8-109">명령</span><span class="sxs-lookup"><span data-stu-id="f39b8-109">Command</span></span> | <span data-ttu-id="f39b8-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f39b8-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f39b8-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="f39b8-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="f39b8-112">Azure Redis Cache 인스턴스에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f39b8-112">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f39b8-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f39b8-113">Next steps</span></span>

<span data-ttu-id="f39b8-114">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f39b8-114">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f39b8-115">추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f39b8-115">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
