---
title: "Azure CLI 스크립트 샘플 - WordPress를 사용하여 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - WordPress를 사용하여 Linux VM 만들기"
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
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="1de9f-103">WordPress를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1de9f-103">Create a VM with WordPress</span></span>

<span data-ttu-id="1de9f-104">이 스크립트는 가상 컴퓨터를 만들고 Azure Virtual Machine 사용자 지정 스크립트 확장을 사용하여 WordPress를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="1de9f-105">스크립트를 실행하면 `http://<public IP of VM>/wordpress`에서 WordPress 구성 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1de9f-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1de9f-106">Sample script</span></span>

<span data-ttu-id="1de9f-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="1de9f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1de9f-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="1de9f-108">Clean up deployment</span></span> 

<span data-ttu-id="1de9f-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1de9f-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1de9f-110">Script explanation</span></span>

<span data-ttu-id="1de9f-111">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1de9f-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1de9f-113">명령</span><span class="sxs-lookup"><span data-stu-id="1de9f-113">Command</span></span> | <span data-ttu-id="1de9f-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1de9f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1de9f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="1de9f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1de9f-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1de9f-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="1de9f-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1de9f-118">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="1de9f-119">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="1de9f-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="1de9f-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="1de9f-121">인바운드 트래픽을 허용하도록 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="1de9f-122">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="1de9f-123">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="1de9f-123">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1de9f-124">가상 컴퓨터에 WordPress를 설치하는 스크립트를 호출하는 사용자 지정 스크립트 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-124">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
| [<span data-ttu-id="1de9f-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="1de9f-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1de9f-126">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1de9f-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1de9f-127">Next steps</span></span>

<span data-ttu-id="1de9f-128">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1de9f-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1de9f-129">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de9f-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
