---
title: "Azure PowerShell 스크립트 샘플 - 스냅숏에서 관리 디스크 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 스냅숏에서 관리 디스크 만들기"
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
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 9105d9dc06eea33b3a4e1eeea7fd793919166c9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="45b65-103">PowerShell을 사용하여 스냅숏에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="45b65-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="45b65-104">이 스크립트는 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="45b65-105">이를 사용하여 OS 및 데이터 디스크의 스냅숏에서 가상 컴퓨터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="45b65-106">각 스냅숏에서 OS 및 데이터 관리 디스크를 만든 다음 관리 디스크를 연결하여 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="45b65-107">스냅숏에서 만든 데이터 디스크를 연결하여 기존 VM의 데이터 디스크를 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="45b65-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="45b65-108">Sample script</span></span>

<span data-ttu-id="45b65-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "스냅숏에서 관리 디스크 만들기")]</span><span class="sxs-lookup"><span data-stu-id="45b65-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="45b65-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="45b65-110">Script explanation</span></span>

<span data-ttu-id="45b65-111">이 스크립트에서는 다음 명령을 사용하여 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="45b65-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="45b65-113">명령</span><span class="sxs-lookup"><span data-stu-id="45b65-113">Command</span></span> | <span data-ttu-id="45b65-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="45b65-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45b65-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="45b65-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="45b65-116">스냅숏 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="45b65-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="45b65-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="45b65-118">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="45b65-119">부모 스냅숏의 리소스 ID, 부모 스냅숏의 위치와 같은 위치 및 저장소 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="45b65-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="45b65-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="45b65-121">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="45b65-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45b65-122">Next steps</span></span>

[<span data-ttu-id="45b65-123">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="45b65-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="45b65-124">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45b65-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="45b65-125">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45b65-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>