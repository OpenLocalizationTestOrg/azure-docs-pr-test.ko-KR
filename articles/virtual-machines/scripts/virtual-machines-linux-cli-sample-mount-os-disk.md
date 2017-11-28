---
title: "CLI 스크립트 샘플-운영 체제 디스크를 탑재 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 운영 체제 디스크 탑재"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="7e868-103">VM 운영 체제 디스크 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e868-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="7e868-104">이 스크립트를 데이터 디스크 tooa 두 번째 가상 컴퓨터로 실패 했거나 문제가 있는 가상 컴퓨터의 hello 운영 체제 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="7e868-105">디스크 문제를 해결하거나 데이터를 복구할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7e868-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="7e868-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="7e868-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="7e868-107">Script explanation</span></span>

<span data-ttu-id="7e868-108">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="7e868-109">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7e868-110">명령</span><span class="sxs-lookup"><span data-stu-id="7e868-110">Command</span></span> | <span data-ttu-id="7e868-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7e868-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7e868-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="7e868-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="7e868-113">가상 컴퓨터 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-113">Return a list of virtual machines.</span></span> <span data-ttu-id="7e868-114">이 경우 hello 쿼리 옵션에 사용 되는 tooreturn hello 가상 컴퓨터 운영 체제 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="7e868-115">이 값 tooa 변수 이름 'uri' 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="7e868-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="7e868-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="7e868-117">가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="7e868-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="7e868-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7e868-119">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="7e868-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="7e868-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="7e868-121">디스크 tooa 가상 컴퓨터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="7e868-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="7e868-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="7e868-123">반환 hello 가상 컴퓨터의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e868-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e868-124">Next steps</span></span>

<span data-ttu-id="7e868-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7e868-126">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e868-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
