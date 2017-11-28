---
title: "Azure CLI 스크립트 샘플 - 스냅숏에서 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 스냅숏에서 VM 만들기"
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
ms.openlocfilehash: 6e47c3baebd5b68ec29d55c43dc00ae7665c81f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="0a35b-103">CLI를 사용하여 스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0a35b-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="0a35b-104">이 스크립트는 OS 디스크의 스냅숏에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0a35b-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0a35b-105">Sample script</span></span>

<span data-ttu-id="0a35b-106">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "스냅숏에서 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="0a35b-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0a35b-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0a35b-107">Clean up deployment</span></span> 

<span data-ttu-id="0a35b-108">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0a35b-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0a35b-109">Script explanation</span></span>

<span data-ttu-id="0a35b-110">이 스크립트는 다음 명령을 사용하여 관리 디스크, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-110">This script uses the following commands to create a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="0a35b-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0a35b-112">명령</span><span class="sxs-lookup"><span data-stu-id="0a35b-112">Command</span></span> | <span data-ttu-id="0a35b-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0a35b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0a35b-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="0a35b-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="0a35b-115">스냅숏 이름 및 리소스 그룹 이름을 사용하여 스냅숏을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-115">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="0a35b-116">반환된 개체의 Id 속성은 관리 디스크를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-116">Id property of the returned object is used to create a managed disk.</span></span>  |
| [<span data-ttu-id="0a35b-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="0a35b-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="0a35b-118">스냅숏 Id, 디스크 이름, 저장소 유형 및 크기를 사용하여 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-118">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="0a35b-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="0a35b-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0a35b-120">관리 OS 디스크를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-120">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a35b-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a35b-121">Next steps</span></span>

<span data-ttu-id="0a35b-122">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a35b-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0a35b-123">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a35b-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
