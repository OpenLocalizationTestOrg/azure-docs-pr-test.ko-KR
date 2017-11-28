---
title: "Azure CLI 스크립트 샘플 - 내부 및 외부 NSG를 사용하여 두 개의 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 내부 및 외부 NSG를 사용하여 두 개의 VM 만들기"
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
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7bd8c315ab0b7b3bcbbd9ebc8f17728079611f9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="d98ac-103">가상 컴퓨터 간의 네트워크 트래픽 보안</span><span class="sxs-lookup"><span data-stu-id="d98ac-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="d98ac-104">이 스크립트는 두 개의 가상 컴퓨터를 만들고 해당 컴퓨터에 들어오는 트래픽의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="d98ac-105">첫 번째 가상 컴퓨터는 인터넷에 액세스할 수 있고 포트 22 및 포트 80에서 트래픽을 허용하도록 NSG(네트워크 보안 그룹)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 22 and port 80.</span></span> <span data-ttu-id="d98ac-106">두 번째 가상 컴퓨터는 인터넷에 액세스할 수 없고 NSG가 첫 번째 가상 컴퓨터의 트래픽을 허용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d98ac-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d98ac-107">Sample script</span></span>

<span data-ttu-id="d98ac-108">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "NSG를 사용하여 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="d98ac-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d98ac-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d98ac-109">Clean up deployment</span></span> 

<span data-ttu-id="d98ac-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d98ac-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d98ac-111">Script explanation</span></span>

<span data-ttu-id="d98ac-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d98ac-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d98ac-114">명령</span><span class="sxs-lookup"><span data-stu-id="d98ac-114">Command</span></span> | <span data-ttu-id="d98ac-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d98ac-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d98ac-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d98ac-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d98ac-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d98ac-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d98ac-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="d98ac-119">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="d98ac-120">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="d98ac-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d98ac-121">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="d98ac-122">az vm create</span><span class="sxs-lookup"><span data-stu-id="d98ac-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d98ac-123">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="d98ac-124">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d98ac-125">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="d98ac-125">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="d98ac-126">네트워크 보안 그룹 규칙에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-126">Returns information about a network security group rule.</span></span> <span data-ttu-id="d98ac-127">이 샘플에서 규칙 이름은 스크립트에서 나중에 사용하기 위해 변수에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-127">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="d98ac-128">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="d98ac-128">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="d98ac-129">NSG 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-129">Updates an NSG rule.</span></span> <span data-ttu-id="d98ac-130">이 샘플에서 백 엔드 규칙은 프런트 엔드 서브넷의 트래픽을 통과하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-130">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="d98ac-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="d98ac-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d98ac-132">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d98ac-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d98ac-133">Next steps</span></span>

<span data-ttu-id="d98ac-134">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d98ac-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d98ac-135">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d98ac-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
