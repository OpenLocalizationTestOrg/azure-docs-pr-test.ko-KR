---
title: "Azure CLI 스크립트 샘플 - ACS Linux Kubernetes 클러스터 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - ACS Linux Kubernetes 클러스터 만들기"
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
ms.openlocfilehash: c6a392217f84f549f2cae3c68fed85b9f888db77
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="fa865-104">Azure Container Service Kubernetes Linux 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="fa865-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="fa865-105">이 샘플에서는 Linux 기반 컨테이너에서 Kubernetes를 실행하는 Azure Container Service 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fa865-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="fa865-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="fa865-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="fa865-107">Clean up deployment</span></span> 

<span data-ttu-id="fa865-108">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fa865-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="fa865-109">Script explanation</span></span>

<span data-ttu-id="fa865-110">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="fa865-111">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fa865-112">명령</span><span class="sxs-lookup"><span data-stu-id="fa865-112">Command</span></span> | <span data-ttu-id="fa865-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fa865-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fa865-114">az group create</span><span class="sxs-lookup"><span data-stu-id="fa865-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fa865-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fa865-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="fa865-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="fa865-117">ACS 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fa865-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fa865-118">Next steps</span></span>

<span data-ttu-id="fa865-119">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa865-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fa865-120">추가 Azure Container Service CLI 스크립트 샘플은 [Azure Container Service 설명서](../cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa865-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

