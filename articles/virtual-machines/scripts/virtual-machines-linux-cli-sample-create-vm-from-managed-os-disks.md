---
title: "Azure CLI 스크립트 샘플 - 관리 디스크를 OS 디스크로 연결하여 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 관리 디스크를 OS 디스크로 연결하여 VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="ca222-103">CLI와 기존 관리 OS 디스크를 사용하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ca222-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="ca222-104">이 스크립트는 기존 관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="ca222-105">이전 시나리오에서는 이 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="ca222-106">다른 구독의 관리 디스크에서 복사된 기존의 관리 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ca222-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="ca222-107">특수화된 VHD 파일에서 만든 기존 관리 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ca222-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="ca222-108">스냅숏에서 만든 기존의 관리 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ca222-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ca222-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ca222-109">Sample script</span></span>

<span data-ttu-id="ca222-110">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "관리 디스크에서 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="ca222-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ca222-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ca222-111">Clean up deployment</span></span> 

<span data-ttu-id="ca222-112">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ca222-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ca222-113">Script explanation</span></span>

<span data-ttu-id="ca222-114">이 스크립트는 다음 명령을 사용하여 관리 디스크 속성을 가져오고 관리 디스크를 새 VM에 연결하며 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="ca222-115">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ca222-116">명령</span><span class="sxs-lookup"><span data-stu-id="ca222-116">Command</span></span> | <span data-ttu-id="ca222-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ca222-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ca222-118">az disk show</span><span class="sxs-lookup"><span data-stu-id="ca222-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="ca222-119">디스크 이름 및 리소스 그룹 이름을 사용하여 관리 디스크 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="ca222-120">Id 속성은 새 VM에 관리 디스크를 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="ca222-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="ca222-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ca222-122">관리 OS 디스크를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="ca222-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca222-123">Next steps</span></span>

<span data-ttu-id="ca222-124">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca222-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ca222-125">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca222-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
