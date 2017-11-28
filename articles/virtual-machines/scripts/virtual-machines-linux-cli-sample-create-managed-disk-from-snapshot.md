---
title: "CLI 스크립트 샘플-aaaAzure 스냅숏으로에서 관리 되는 디스크를 만들 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 스냅숏에서 관리 디스크 만들기"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="26e27-103">CLI를 사용하여 스냅숏에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="26e27-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="26e27-104">이 스크립트는 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="26e27-105">OS 및 데이터 디스크의 스냅숏 기반에서으로 가상 컴퓨터 toorestore 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="26e27-106">각 스냅숏에서 OS 및 데이터 관리 디스크를 만든 다음 관리 디스크를 연결하여 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="26e27-107">스냅숏에서 만든 데이터 디스크를 연결하여 기존 VM의 데이터 디스크를 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="26e27-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="26e27-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="26e27-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="26e27-109">Script explanation</span></span>

<span data-ttu-id="26e27-110">이 스크립트 명령 toocreate 다음 스냅숏에서 관리 되는 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="26e27-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="26e27-112">명령</span><span class="sxs-lookup"><span data-stu-id="26e27-112">Command</span></span> | <span data-ttu-id="26e27-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="26e27-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26e27-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="26e27-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="26e27-115">모든 hello 속성의 hello 이름을 사용 하 여 스냅숏 및 hello 스냅숏의 리소스 그룹 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="26e27-116">Id 속성은 사용 되는 toocreate 관리 되는 디스크.</span><span class="sxs-lookup"><span data-stu-id="26e27-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="26e27-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="26e27-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="26e27-118">관리 스냅숏의 스냅숏 Id를 사용하여 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="26e27-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26e27-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26e27-119">Next steps</span></span>

[<span data-ttu-id="26e27-120">관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="26e27-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="26e27-121">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="26e27-122">추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="26e27-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
