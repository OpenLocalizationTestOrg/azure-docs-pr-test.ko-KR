---
title: "Azure CLI 스크립트 샘플 - DSC를 사용하는 IIS로 Windows Server 2016 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - DSC를 사용하는 IIS로 Windows Server 2016 VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 1f605c0260fcaea29851d76c90ba0b287bec5ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="483f7-103">DSC를 사용하는 IIS로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="483f7-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="483f7-104">이 스크립트는 가상 컴퓨터를 만들고 Azure Virtual Machine DSC 사용자 지정 스크립트 확장을 사용하여 IIS를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-104">This script creates a virtual machine, and uses the Azure Virtual Machine DSC custom script extension to install and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="483f7-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="483f7-105">Sample script</span></span>

<span data-ttu-id="483f7-106">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="483f7-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="483f7-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="483f7-107">Clean up deployment</span></span> 

<span data-ttu-id="483f7-108">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="483f7-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="483f7-109">Script explanation</span></span>

<span data-ttu-id="483f7-110">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="483f7-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="483f7-112">명령</span><span class="sxs-lookup"><span data-stu-id="483f7-112">Command</span></span> | <span data-ttu-id="483f7-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="483f7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="483f7-114">az group create</span><span class="sxs-lookup"><span data-stu-id="483f7-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="483f7-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="483f7-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="483f7-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="483f7-117">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="483f7-118">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="483f7-119">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="483f7-119">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="483f7-120">가상 컴퓨터에 IIS를 설치하는 스크립트를 호출하는 사용자 지정 스크립트 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-120">Add the Custom Script Extension to the virtual machine which invokes a script to install IIS.</span></span> |
| [<span data-ttu-id="483f7-121">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="483f7-121">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="483f7-122">인바운드 트래픽을 허용하도록 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-122">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="483f7-123">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-123">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="483f7-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="483f7-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="483f7-125">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="483f7-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="483f7-126">Next steps</span></span>

<span data-ttu-id="483f7-127">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="483f7-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="483f7-128">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="483f7-128">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
