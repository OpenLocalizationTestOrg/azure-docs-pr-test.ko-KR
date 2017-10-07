---
title: "CLI 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독과 CLI의 복사본 (이동) 스냅숏 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독과 CLI의 스냅숏 복사 (이동)"
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="499bc-103">관리 되는 디스크 toosame 또는 다른 구독과 CLI의 스냅숏을 복사합니다</span><span class="sxs-lookup"><span data-stu-id="499bc-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="499bc-104">이 스크립트는 관리 되는 디스크 toosame 또는 다른 구독에 대 한 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="499bc-105">이 스크립트 toomove 스냅숏 toodifferent 구독을 사용 하 여 hello에 hello 부모 스냅숏의와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="499bc-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="499bc-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="499bc-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="499bc-107">Script explanation</span></span>

<span data-ttu-id="499bc-108">이 스크립트 명령 toocreate 다음 사용 하 여 사용 하 여 hello 대상 구독에서 스냅숏 hello hello 소스 스냅숏의 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="499bc-109">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="499bc-110">명령</span><span class="sxs-lookup"><span data-stu-id="499bc-110">Command</span></span> | <span data-ttu-id="499bc-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="499bc-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="499bc-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="499bc-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="499bc-113">모든 hello 속성의 hello 이름을 사용 하 여 스냅숏 및 hello 스냅숏의 리소스 그룹 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="499bc-114">Id 속성은 사용 되는 toocopy hello 스냅숏 toodifferent 구독.</span><span class="sxs-lookup"><span data-stu-id="499bc-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="499bc-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="499bc-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="499bc-116">복사본의 Id 및 이름을 사용 하 여 다른 구독에서 스냅숏을 만들어 스냅숏 hello hello 부모 스냅숏의 합니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="499bc-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="499bc-117">Next steps</span></span>

[<span data-ttu-id="499bc-118">스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="499bc-118">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="499bc-119">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="499bc-120">추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="499bc-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
