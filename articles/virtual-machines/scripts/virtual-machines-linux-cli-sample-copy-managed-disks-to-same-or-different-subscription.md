---
title: "Azure CLI 스크립트 샘플 - 관리 디스크를 동일한 구독이나 다른 구독으로 복사(이동) | Microsoft Docs "
description: "Azure CLI 스크립트 샘플 - 관리 디스크를 동일한 구독이나 다른 구독으로 복사(이동)"
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
ms.openlocfilehash: dcf92babf84872ffbbba81127952f8422104c723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="9017f-103">CLI를 사용하여 관리 디스크를 동일한 구독이나 다른 구독으로 복사</span><span class="sxs-lookup"><span data-stu-id="9017f-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="9017f-104">이 스크립트는 관리 디스크를 동일한 구독이나 같은 지역에 있지만 다른 구독으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9017f-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="9017f-105">Sample script</span></span>

<span data-ttu-id="9017f-106">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "관리 디스크 복사")]</span><span class="sxs-lookup"><span data-stu-id="9017f-106">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="9017f-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="9017f-107">Script explanation</span></span>

<span data-ttu-id="9017f-108">이 스크립트에서는 다음 명령을 사용하여 원본 관리 디스크의 ID를 사용하여 대상 구독에 새 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="9017f-109">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9017f-110">명령</span><span class="sxs-lookup"><span data-stu-id="9017f-110">Command</span></span> | <span data-ttu-id="9017f-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9017f-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9017f-112">az disk show</span><span class="sxs-lookup"><span data-stu-id="9017f-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="9017f-113">관리 디스크의 이름 및 리소스 그룹 속성을 사용하여 관리 디스크의 모든 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="9017f-114">Id 속성은 관리 디스크를 다른 구독으로 복사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="9017f-115">az disk create</span><span class="sxs-lookup"><span data-stu-id="9017f-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="9017f-116">부모 관리 디스크의 Id 및 이름을 사용하여 다른 구독에서 새 관리 디스크를 만들어 관리 디스크를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="9017f-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9017f-117">Next steps</span></span>

[<span data-ttu-id="9017f-118">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="9017f-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9017f-119">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9017f-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9017f-120">추가 가상 컴퓨터 및 관리 디스크 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9017f-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
