---
title: "Azure CLI 스크립트 샘플 - 운영 체제 디스크 탑재 | Microsoft Docs"
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
ms.openlocfilehash: b54a94d833644ebfae4c1fac59e4753ab723ced4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="d014e-103">VM 운영 체제 디스크 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d014e-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="d014e-104">이 스크립트는 실패했거나 문제가 있는 가상 컴퓨터의 운영 체제 디스크를 두 번째 가상 컴퓨터에 대한 데이터 디스크로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span></span> <span data-ttu-id="d014e-105">디스크 문제를 해결하거나 데이터를 복구할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d014e-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d014e-106">Sample script</span></span>

<span data-ttu-id="d014e-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="d014e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="d014e-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d014e-108">Script explanation</span></span>

<span data-ttu-id="d014e-109">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d014e-110">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d014e-111">명령</span><span class="sxs-lookup"><span data-stu-id="d014e-111">Command</span></span> | <span data-ttu-id="d014e-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d014e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d014e-113">az vm show</span><span class="sxs-lookup"><span data-stu-id="d014e-113">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="d014e-114">가상 컴퓨터 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-114">Return a list of virtual machines.</span></span> <span data-ttu-id="d014e-115">이 경우 가상 컴퓨터 운영 체제 디스크를 반환하는 데 쿼리 옵션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-115">In this case, the query option is used to return the virtual machine operating system disk.</span></span> <span data-ttu-id="d014e-116">그러면 이 값이 변수 이름 'uri'에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-116">This value is then added to a variable name ‘uri’.</span></span> |
| [<span data-ttu-id="d014e-117">az vm delete</span><span class="sxs-lookup"><span data-stu-id="d014e-117">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="d014e-118">가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-118">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="d014e-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="d014e-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d014e-120">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-120">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="d014e-121">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="d014e-121">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="d014e-122">디스크를 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-122">Attaches a disk to a virtual machine.</span></span> |
| [<span data-ttu-id="d014e-123">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="d014e-123">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="d014e-124">가상 컴퓨터의 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-124">Returns the IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d014e-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d014e-125">Next steps</span></span>

<span data-ttu-id="d014e-126">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d014e-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d014e-127">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d014e-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
