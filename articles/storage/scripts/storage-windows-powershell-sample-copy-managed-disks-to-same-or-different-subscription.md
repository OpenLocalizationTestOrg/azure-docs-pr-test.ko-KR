---
title: "Azure PowerShell 스크립트 샘플 - 같은 구독 또는 다른 구독으로 관리 디스크 복사(이동) | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 같은 구독 또는 다른 구독으로 관리 디스크 복사(이동)"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 6fa94de0461cc538a60d57ca3518141afd9d0469
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-in-the-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="77a44-103">PowerShell을 사용하여 같은 구독 또는 다른 구독에 관리 디스크 복사</span><span class="sxs-lookup"><span data-stu-id="77a44-103">Copy managed disks in the same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="77a44-104">이 스크립트는 같은 구독 또는 다른 구독에 기존 관리 디스크의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-104">This script creates a copy of an existing managed disk in the same subscription or different subscription.</span></span> <span data-ttu-id="77a44-105">새 디스크는 부모 관리 디스크와 같은 지역에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-105">The new disk is created in the same region as the parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="77a44-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="77a44-106">Sample script</span></span>

<span data-ttu-id="77a44-107">[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "관리 디스크 복사")]</span><span class="sxs-lookup"><span data-stu-id="77a44-107">[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="77a44-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="77a44-108">Script explanation</span></span>

<span data-ttu-id="77a44-109">이 스크립트에서는 다음 명령을 사용하여 원본 관리 디스크의 ID를 사용하여 대상 구독에 새 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-109">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="77a44-110">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="77a44-111">명령</span><span class="sxs-lookup"><span data-stu-id="77a44-111">Command</span></span> | <span data-ttu-id="77a44-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="77a44-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77a44-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="77a44-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="77a44-114">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="77a44-115">부모 디스크의 리소스 ID와 부모 디스크의 위치와 같은 위치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-115">It includes the resource Id of the parent disk and location that is same as the location of parent disk.</span></span>  |
| [<span data-ttu-id="77a44-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="77a44-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="77a44-117">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="77a44-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77a44-118">Next steps</span></span>

[<span data-ttu-id="77a44-119">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="77a44-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="77a44-120">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77a44-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="77a44-121">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77a44-121">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>