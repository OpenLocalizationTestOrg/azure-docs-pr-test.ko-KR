---
title: "Azure CLI 스크립트 샘플 - CLI를 사용하여 관리 디스크의 스냅숏을 동일한 구독이나 다른 구독으로 복사(이동) | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - CLI를 사용하여 관리 디스크의 스냅숏을 동일한 구독이나 다른 구독으로 복사(이동)"
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
ms.openlocfilehash: 6cc0125c08ccb77d014b4642d702c556fffdc8bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="4ad2a-103">CLI를 사용하여 관리 디스크의 스냅숏을 동일한 구독이나 다른 구독으로 복사</span><span class="sxs-lookup"><span data-stu-id="4ad2a-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="4ad2a-104">이 스크립트는 관리 디스크의 스냅숏을 동일한 구독이나 다른 구독으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="4ad2a-105">이 스크립트를 사용하여 부모 스냅숏과 같은 지역의 다른 구독으로 스냅숏을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4ad2a-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4ad2a-106">Sample script</span></span>

<span data-ttu-id="4ad2a-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "스냅숏 복사")]</span><span class="sxs-lookup"><span data-stu-id="4ad2a-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="4ad2a-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="4ad2a-108">Script explanation</span></span>

<span data-ttu-id="4ad2a-109">이 스크립트에서는 다음 명령을 사용하여 원본 스냅숏의 ID를 사용하여 대상 구독에 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="4ad2a-110">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4ad2a-111">명령</span><span class="sxs-lookup"><span data-stu-id="4ad2a-111">Command</span></span> | <span data-ttu-id="4ad2a-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4ad2a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ad2a-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="4ad2a-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="4ad2a-114">스냅숏의 이름 및 리소스 그룹 속성을 사용하여 스냅숏의 모든 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="4ad2a-115">Id 속성은 스냅숏을 다른 구독으로 복사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="4ad2a-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="4ad2a-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="4ad2a-117">부모 스냅숏의 Id와 이름을 사용하여 다른 구독에 스냅숏을 만들어 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="4ad2a-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4ad2a-118">Next steps</span></span>

[<span data-ttu-id="4ad2a-119">스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="4ad2a-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4ad2a-120">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4ad2a-121">추가 가상 컴퓨터 및 관리 디스크 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad2a-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
