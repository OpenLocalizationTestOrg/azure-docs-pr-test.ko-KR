---
title: "Azure CLI 스크립트 샘플 - Docker 호스트 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Docker 호스트 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: e8704824dec66d724f2d30dab4d6bdf019c6b206
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="ee436-103">Docker를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ee436-103">Create a VM with Docker</span></span>

<span data-ttu-id="ee436-104">이 스크립트는 Docker를 사용하는 가상 컴퓨터를 만들고 Docker 컨테이너에서 NGINX를 실행하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="ee436-105">스크립트를 실행한 후에 Azure Virtual Machine의 FQDN을 통해 NGINX 웹 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ee436-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ee436-106">Sample script</span></span>

<span data-ttu-id="ee436-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker 호스트")]</span><span class="sxs-lookup"><span data-stu-id="ee436-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ee436-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ee436-108">Clean up deployment</span></span> 

<span data-ttu-id="ee436-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ee436-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ee436-110">Script explanation</span></span>

<span data-ttu-id="ee436-111">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ee436-112">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ee436-113">명령</span><span class="sxs-lookup"><span data-stu-id="ee436-113">Command</span></span> | <span data-ttu-id="ee436-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ee436-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ee436-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ee436-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ee436-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ee436-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="ee436-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ee436-118">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="ee436-119">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ee436-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="ee436-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="ee436-121">인바운드 트래픽을 허용하도록 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="ee436-122">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="ee436-123">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="ee436-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ee436-124">VM에 가상 컴퓨터 확장을 추가하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="ee436-125">이 샘플에서는 Docker VM 확장을 사용하여 Docker 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-125">In this sample, the Docker VM extension is used to configure a Docker host.</span></span>|
| [<span data-ttu-id="ee436-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="ee436-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ee436-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-127">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ee436-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ee436-128">Next steps</span></span>

<span data-ttu-id="ee436-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee436-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ee436-130">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee436-130">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
