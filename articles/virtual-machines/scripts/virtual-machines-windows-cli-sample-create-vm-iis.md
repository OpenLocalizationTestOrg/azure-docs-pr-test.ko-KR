---
title: "Azure CLI 스크립트 샘플 - IIS 설치 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - IIS 설치"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 426418c01b23845372443af5b8f4e826fb321f7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="3ce3e-103">Azure CLI를 사용하여 가상 컴퓨터 빠른 생성</span><span class="sxs-lookup"><span data-stu-id="3ce3e-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="3ce3e-104">이 스크립트는 Windows Server 2016을 실행하는 Azure Virtual Machine을 만들고 Azure Virtual Machine 사용자 지정 스크립트 확장을 사용하여 IIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="3ce3e-105">스크립트를 실행하면 가상 컴퓨터의 공용 IP 주소에서 기본 IIS 웹 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3ce3e-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3ce3e-106">Sample script</span></span>

<span data-ttu-id="3ce3e-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="3ce3e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3ce3e-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3ce3e-108">Clean up deployment</span></span> 

<span data-ttu-id="3ce3e-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3ce3e-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3ce3e-110">Script explanation</span></span>

<span data-ttu-id="3ce3e-111">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="3ce3e-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3ce3e-113">명령</span><span class="sxs-lookup"><span data-stu-id="3ce3e-113">Command</span></span> | <span data-ttu-id="3ce3e-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3ce3e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3ce3e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="3ce3e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3ce3e-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3ce3e-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="3ce3e-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="3ce3e-118">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="3ce3e-119">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="3ce3e-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="3ce3e-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="3ce3e-121">인바운드 트래픽을 허용하도록 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="3ce3e-122">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="3ce3e-123">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="3ce3e-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3ce3e-124">VM에 가상 컴퓨터 확장을 추가하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="3ce3e-125">이 샘플에서 사용자 지정 스크립트 확장은 IIS를 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-125">In this sample, the custom script extension is used to install IIS.</span></span>|
| [<span data-ttu-id="3ce3e-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="3ce3e-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3ce3e-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ce3e-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ce3e-128">Next steps</span></span>

<span data-ttu-id="3ce3e-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3ce3e-130">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ce3e-130">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
