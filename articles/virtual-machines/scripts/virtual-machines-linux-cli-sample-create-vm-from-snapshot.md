---
title: "CLI 스크립트 샘플-aaaAzure 스냅숏에서 VM 만들기 | Microsoft Docs"
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
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="28904-103">CLI를 사용하여 스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="28904-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="28904-104">이 스크립트는 OS 디스크의 스냅숏에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28904-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="28904-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="28904-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="28904-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="28904-106">Clean up deployment</span></span> 

<span data-ttu-id="28904-107">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28904-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="28904-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="28904-108">Script explanation</span></span>

<span data-ttu-id="28904-109">이 스크립트 명령 toocreate 있는 관리 되는 디스크, 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="28904-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="28904-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="28904-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="28904-111">명령</span><span class="sxs-lookup"><span data-stu-id="28904-111">Command</span></span> | <span data-ttu-id="28904-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="28904-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="28904-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="28904-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="28904-114">스냅숏 이름 및 리소스 그룹 이름을 사용하여 스냅숏을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28904-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="28904-115">Id의 개체를 반환 하는 hello 속성이 사용 되는 관리 되는 디스크 toocreate입니다.</span><span class="sxs-lookup"><span data-stu-id="28904-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="28904-116">az disk create</span><span class="sxs-lookup"><span data-stu-id="28904-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="28904-117">스냅숏 Id, 디스크 이름, 저장소 유형 및 크기를 사용하여 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28904-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="28904-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="28904-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="28904-119">관리 OS 디스크를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28904-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="28904-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28904-120">Next steps</span></span>

<span data-ttu-id="28904-121">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="28904-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="28904-122">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="28904-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
