---
title: "Azure CLI 스크립트 샘플 - Azure Redis Cache의 호스트 이름, 포트 및 키 가져오기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Redis Cache 인스턴스의 호스트 이름, 포트 및 키 가져오기"
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
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="009a7-103">Azure Redis Cache의 호스트 이름, 포트 및 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="009a7-103">Get the hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="009a7-104">이 시나리오에서는 Azure Redis Cache 인스턴스에 연결하는 데 사용되는 호스트 이름, 포트 및 키를 검색하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="009a7-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="009a7-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="009a7-105">Sample script</span></span>

<span data-ttu-id="009a7-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="009a7-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="009a7-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="009a7-107">Script explanation</span></span>

<span data-ttu-id="009a7-108">이 스크립트는 다음 명령을 사용하여 Azure Redis Cache 인스턴스의 호스트 이름, 포트 및 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="009a7-108">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="009a7-109">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="009a7-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="009a7-110">명령</span><span class="sxs-lookup"><span data-stu-id="009a7-110">Command</span></span> | <span data-ttu-id="009a7-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="009a7-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="009a7-112">az redis show</span><span class="sxs-lookup"><span data-stu-id="009a7-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="009a7-113">Azure Redis Cache 인스턴스에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="009a7-113">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="009a7-114">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="009a7-114">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="009a7-115">Azure Redis Cache 인스턴스에 대한 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="009a7-115">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="009a7-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="009a7-116">Next steps</span></span>

<span data-ttu-id="009a7-117">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="009a7-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="009a7-118">추가 Azure Redis Cache CLI 스크립트 샘플은 [Azure Redis Cache 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="009a7-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>