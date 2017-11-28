---
title: "aaaAzure CLI 스크립트 샘플-ACS DC/OS 클러스터 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - ACS DC/OS 클러스터 만들기"
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
ms.openlocfilehash: 35213fd615b2145642add908dfc48516c33ff332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="8eba9-104">Azure Container Service DC/OS 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8eba9-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="8eba9-105">이 샘플에서는 DC/OS를 실행하는 Azure Container Service 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8eba9-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8eba9-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="8eba9-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="8eba9-107">Clean up deployment</span></span> 

<span data-ttu-id="8eba9-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8eba9-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8eba9-109">Script explanation</span></span>

<span data-ttu-id="8eba9-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="8eba9-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8eba9-112">명령</span><span class="sxs-lookup"><span data-stu-id="8eba9-112">Command</span></span> | <span data-ttu-id="8eba9-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8eba9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8eba9-114">az group create</span><span class="sxs-lookup"><span data-stu-id="8eba9-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8eba9-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8eba9-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="8eba9-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="8eba9-117">ACS 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8eba9-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8eba9-118">Next steps</span></span>

<span data-ttu-id="8eba9-119">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8eba9-120">추가 Azure 컨테이너 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 컨테이너 서비스 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8eba9-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
