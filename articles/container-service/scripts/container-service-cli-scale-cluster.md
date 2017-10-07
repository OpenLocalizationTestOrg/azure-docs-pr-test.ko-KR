---
title: "CLI 스크립트 샘플-aaaAzure ACS 클러스터의 크기를 조정 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - ACS 클러스터 크기 조정"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="b594a-104">Azure Container Service 클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b594a-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="b594a-105">이 샘플에서는 Azure Container Service의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b594a-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b594a-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="b594a-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="b594a-107">Clean up deployment</span></span> 

<span data-ttu-id="b594a-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b594a-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b594a-109">Script explanation</span></span>

<span data-ttu-id="b594a-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="b594a-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b594a-112">명령</span><span class="sxs-lookup"><span data-stu-id="b594a-112">Command</span></span> | <span data-ttu-id="b594a-113">참고</span><span class="sxs-lookup"><span data-stu-id="b594a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b594a-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="b594a-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="b594a-115">ACS 클러스터를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b594a-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b594a-116">Next steps</span></span>

<span data-ttu-id="b594a-117">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b594a-118">추가 Azure 컨테이너 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 컨테이너 서비스 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b594a-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

