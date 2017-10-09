---
title: "CLI 스크립트 샘플-aaaAzure 내부 및 외부 NSG 갖는 두 개의 Vm을 만들 | Microsoft Docs"
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="fd294-103">가상 컴퓨터 간의 네트워크 트래픽 보안</span><span class="sxs-lookup"><span data-stu-id="fd294-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="fd294-104">이 스크립트 두 가상 컴퓨터를 만들고 들어오는 트래픽을 tooboth의 보안을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="fd294-105">인터넷에서 액세스할 수 있는 가상 컴퓨터는 hello 이며가 NSG ()를 네트워크 보안 그룹 구성 tooallow 트래픽을 포트 22 및 포트 80에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="fd294-106">hello 두 번째 가상 컴퓨터에 액세스할 수 없는 인터넷 hello 및에 구성 된 NSG tooonly hello 첫 번째 가상 컴퓨터에서 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fd294-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="fd294-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fd294-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="fd294-108">Clean up deployment</span></span> 

<span data-ttu-id="fd294-109">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fd294-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="fd294-110">Script explanation</span></span>

<span data-ttu-id="fd294-111">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="fd294-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fd294-113">명령</span><span class="sxs-lookup"><span data-stu-id="fd294-113">Command</span></span> | <span data-ttu-id="fd294-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fd294-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd294-115">az group create</span><span class="sxs-lookup"><span data-stu-id="fd294-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fd294-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fd294-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="fd294-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="fd294-118">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="fd294-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="fd294-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="fd294-120">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="fd294-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="fd294-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fd294-122">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="fd294-123">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="fd294-124">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="fd294-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="fd294-125">네트워크 보안 그룹 규칙에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="fd294-126">이 샘플에서는 hello 규칙 이름은 hello 스크립트에서 나중에 사용 하기 위해 변수에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="fd294-127">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="fd294-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="fd294-128">NSG 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-128">Updates an NSG rule.</span></span> <span data-ttu-id="fd294-129">이 샘플에서는 hello 백 엔드 규칙이 업데이트 toopass hello 프런트 엔드 서브넷 에서만에서 트래픽을 통해 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="fd294-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="fd294-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fd294-131">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd294-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd294-132">Next steps</span></span>

<span data-ttu-id="fd294-133">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fd294-134">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd294-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
