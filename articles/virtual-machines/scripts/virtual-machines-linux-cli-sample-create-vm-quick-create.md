---
title: "Azure CLI 스크립트 샘플 - Linux VM 빠른 생성 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Linux VM 빠른 생성"
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
ms.openlocfilehash: 3df3affcedf9edbe6e548d881a877f14204ec280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="2ed65-103">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="2ed65-103">Create a virtual machine</span></span>

<span data-ttu-id="2ed65-104">이 스크립트는 Ubuntu 운영 체제 및 관련 네트워킹 리소스에서 Azure Virtual Machine을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="2ed65-105">스크립트를 실행하면 SSH를 통해 가상 컴퓨터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2ed65-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2ed65-106">Sample script</span></span>

<span data-ttu-id="2ed65-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="2ed65-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2ed65-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="2ed65-108">Clean up deployment</span></span> 

<span data-ttu-id="2ed65-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2ed65-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2ed65-110">Script explanation</span></span>

<span data-ttu-id="2ed65-111">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2ed65-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2ed65-113">명령</span><span class="sxs-lookup"><span data-stu-id="2ed65-113">Command</span></span> | <span data-ttu-id="2ed65-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2ed65-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2ed65-115">az group create</span><span class="sxs-lookup"><span data-stu-id="2ed65-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2ed65-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2ed65-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="2ed65-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2ed65-118">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="2ed65-119">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="2ed65-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="2ed65-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2ed65-121">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2ed65-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ed65-122">Next steps</span></span>

<span data-ttu-id="2ed65-123">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ed65-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2ed65-124">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ed65-124">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
