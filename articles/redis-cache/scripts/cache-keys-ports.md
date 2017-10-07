---
title: "CLI 스크립트 샘플-Get hello 호스트 이름, 포트 및 Azure Redis Cache에 대 한 키 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Get hello 호스트 이름, 포트 및 Azure Redis 캐시 인스턴스에 대 한 키"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="3e230-103">Azure Redis Cache에 대 한 hello 호스트 이름, 포트 및 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="3e230-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="3e230-104">이 시나리오에서는 tooretrieve hello 호스트 이름, 포트 및 키 tooconnect tooan Azure Redis 캐시 인스턴스에 사용 되는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="3e230-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3e230-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="3e230-106">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3e230-106">Script explanation</span></span>

<span data-ttu-id="3e230-107">이 스크립트 명령 tooretrieve hello 호스트 이름, 키 및 Azure Redis Cache 인스턴스 포트를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="3e230-108">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3e230-109">명령</span><span class="sxs-lookup"><span data-stu-id="3e230-109">Command</span></span> | <span data-ttu-id="3e230-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3e230-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3e230-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="3e230-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="3e230-112">Azure Redis Cache 인스턴스에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="3e230-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="3e230-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="3e230-114">Azure Redis Cache 인스턴스에 대한 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3e230-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e230-115">Next steps</span></span>

<span data-ttu-id="3e230-116">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3e230-117">추가 Azure Redis 캐시 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Redis Cache 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e230-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
