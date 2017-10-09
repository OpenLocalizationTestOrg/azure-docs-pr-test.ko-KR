---
title: "aaaAzure CLI 스크립트 샘플-피어 두 가상 네트워크 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 2개 가상 네트워크 피어링"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="d4ad5-103">2개 가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="d4ad5-103">Peer two virtual networks</span></span>

<span data-ttu-id="d4ad5-104">이 스크립트를 만들고 hello에 두 개의 가상 네트워크를 연결 동일한 지역 trhough hello Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="d4ad5-105">Hello 스크립트를 실행 한 후 두 개의 가상 네트워크 간의 피어 링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="d4ad5-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d4ad5-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d4ad5-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d4ad5-107">Clean up deployment</span></span> 

<span data-ttu-id="d4ad5-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d4ad5-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d4ad5-109">Script explanation</span></span>

<span data-ttu-id="d4ad5-110">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d4ad5-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d4ad5-112">명령</span><span class="sxs-lookup"><span data-stu-id="d4ad5-112">Command</span></span> | <span data-ttu-id="d4ad5-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d4ad5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4ad5-114">az group create</span><span class="sxs-lookup"><span data-stu-id="d4ad5-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d4ad5-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4ad5-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d4ad5-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="d4ad5-117">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="d4ad5-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="d4ad5-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="d4ad5-119">두 가상 네트워크 간에 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="d4ad5-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="d4ad5-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d4ad5-121">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4ad5-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4ad5-122">Next steps</span></span>

<span data-ttu-id="d4ad5-123">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d4ad5-124">추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ad5-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
