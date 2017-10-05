---
title: "Azure CLI 스크립트 샘플 - 내부 및 외부 NSG를 사용하여 두 개의 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 내부 및 외부 NSG를 사용하여 두 개의 VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: cc80e3fc5aaa12200e9a441db9d4a9c613c0548a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="ff40e-103">가상 컴퓨터 간의 네트워크 트래픽 보안</span><span class="sxs-lookup"><span data-stu-id="ff40e-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="ff40e-104">이 스크립트는 두 개의 가상 컴퓨터를 만들고 해당 컴퓨터에 들어오는 트래픽의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="ff40e-105">첫 번째 가상 컴퓨터는 인터넷에 액세스할 수 있고 포트 3389 및 포트 80에서 트래픽을 허용하도록 네트워크 보안 그룹(NSG)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="ff40e-106">두 번째 가상 컴퓨터는 인터넷에 액세스할 수 없고 NSG가 첫 번째 가상 컴퓨터의 트래픽을 허용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ff40e-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ff40e-107">Sample script</span></span>

<span data-ttu-id="ff40e-108">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "NSG를 사용하여 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="ff40e-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ff40e-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ff40e-109">Clean up deployment</span></span> 

<span data-ttu-id="ff40e-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="ff40e-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ff40e-111">Script explanation</span></span>

<span data-ttu-id="ff40e-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="ff40e-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ff40e-114">명령</span><span class="sxs-lookup"><span data-stu-id="ff40e-114">Command</span></span> | <span data-ttu-id="ff40e-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ff40e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff40e-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ff40e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ff40e-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ff40e-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="ff40e-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="ff40e-119">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="ff40e-120">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="ff40e-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="ff40e-121">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="ff40e-122">az vm create</span><span class="sxs-lookup"><span data-stu-id="ff40e-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ff40e-123">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="ff40e-124">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ff40e-125">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="ff40e-125">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="ff40e-126">NSG 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-126">Updates an NSG rule.</span></span> <span data-ttu-id="ff40e-127">이 샘플에서 백 엔드 규칙은 프런트 엔드 서브넷의 트래픽을 통과하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-127">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="ff40e-128">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="ff40e-128">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="ff40e-129">네트워크 보안 그룹 규칙에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-129">Returns information about a network security group rule.</span></span> <span data-ttu-id="ff40e-130">이 샘플에서 규칙 이름은 스크립트에서 나중에 사용하기 위해 변수에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-130">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="ff40e-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="ff40e-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ff40e-132">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff40e-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff40e-133">Next steps</span></span>

<span data-ttu-id="ff40e-134">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff40e-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ff40e-135">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff40e-135">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
