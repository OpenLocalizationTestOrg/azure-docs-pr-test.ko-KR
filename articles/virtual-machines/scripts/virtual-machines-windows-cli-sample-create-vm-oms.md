---
title: "Azure CLI 스크립트 샘플 - OMS 모니터링을 사용하여 Windows Server 2016 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - OMS 모니터링을 사용하여 Windows Server 2016 VM 만들기"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: ddb191163061dc47712e024c8c1d7a6f4bdf325b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="a85e1-103">Operations Management Suite를 사용하여 VM 모니터링</span><span class="sxs-lookup"><span data-stu-id="a85e1-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="a85e1-104">이 스크립트는 Azure Virtual Machine을 만들고 OMS(Operations Management Suite) 에이전트를 설치하고 OMS 작업 영역을 사용하여 시스템을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="a85e1-105">스크립트를 실행하면 가상 컴퓨터가 OMS 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a85e1-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a85e1-106">Sample script</span></span>

<span data-ttu-id="a85e1-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="a85e1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a85e1-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="a85e1-108">Clean up deployment</span></span> 

<span data-ttu-id="a85e1-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a85e1-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a85e1-110">Script explanation</span></span>

<span data-ttu-id="a85e1-111">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a85e1-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a85e1-113">명령</span><span class="sxs-lookup"><span data-stu-id="a85e1-113">Command</span></span> | <span data-ttu-id="a85e1-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a85e1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a85e1-115">az group create</span><span class="sxs-lookup"><span data-stu-id="a85e1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a85e1-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a85e1-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="a85e1-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a85e1-118">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="a85e1-119">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="a85e1-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="a85e1-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a85e1-121">가상 컴퓨터에 대한 VM 확장을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="a85e1-122">이 경우에 Operations Management Suite 에이전트 확장은 OMS 에이전트를 설치하고 OMS 작업 영역에서 VM을 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="a85e1-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="a85e1-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a85e1-124">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a85e1-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a85e1-125">Next steps</span></span>

<span data-ttu-id="a85e1-126">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a85e1-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a85e1-127">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a85e1-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
