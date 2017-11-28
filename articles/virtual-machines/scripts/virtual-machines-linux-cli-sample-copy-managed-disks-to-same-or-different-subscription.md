---
title: "CLI 스크립트 샘플-aaaAzure 복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독"
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
ms.openlocfilehash: b1fa207bd6e05d7094be08855e7823e3b7686013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="15b88-103">관리 되는 디스크 toosame 또는 CLI 다른 구독 복사</span><span class="sxs-lookup"><span data-stu-id="15b88-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="15b88-104">이 스크립트는 관리 되는 디스크 toosame 또는 다른 구독 복사 하지만 동일한 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="15b88-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="15b88-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="15b88-106">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="15b88-106">Script explanation</span></span>

<span data-ttu-id="15b88-107">이 스크립트를 사용 하 여 다음 명령을 toocreate 사용 하 여 hello 대상 구독에 관리 되는 새 디스크를 hello hello 원본의 Id 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="15b88-108">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="15b88-109">명령</span><span class="sxs-lookup"><span data-stu-id="15b88-109">Command</span></span> | <span data-ttu-id="15b88-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="15b88-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="15b88-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="15b88-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="15b88-112">Hello 관리 되는 디스크의 hello 이름과 리소스 그룹 속성을 사용 하 여 관리 되는 디스크의 모든 hello 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="15b88-113">Id 속성에 사용 되는 toocopy hello 관리 되는 디스크 toodifferent 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="15b88-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="15b88-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="15b88-115">관리 되는 디스크 Id 및 이름을 사용 하는 다른 구독에 새 관리 되는 디스크를 만들어 복사 hello 부모 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="15b88-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15b88-116">Next steps</span></span>

[<span data-ttu-id="15b88-117">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="15b88-117">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="15b88-118">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="15b88-119">추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="15b88-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
