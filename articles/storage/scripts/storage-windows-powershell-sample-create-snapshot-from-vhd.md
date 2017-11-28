---
title: "Azure PowerShell 스크립트 샘플 - VHD에서 스냅숏을 만들어 약간의 시간 동안 같은 관리 디스크 여러 개 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - VHD에서 스냅숏을 만들어 약간의 시간 동안 같은 관리 디스크 여러 개 만들기"
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
ms.openlocfilehash: 8588a33a1f0b4cce0059a40239301587cdc28920
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="f4874-103">PowerShell을 사용하여 VHD에서 스냅숏을 만들어 약간의 시간 동안 같은 관리 디스크 여러 개 만들기</span><span class="sxs-lookup"><span data-stu-id="f4874-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="f4874-104">이 스크립트는 같은 구독 또는 다른 구독의 저장소 계정에 VHD 파일의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="f4874-105">이 스크립트를 사용하여 특수화된(일반화되지 않은/sysprep을 실행하지 않은) VHD를 스냅숏으로 가져온 다음 스냅숏을 사용하여 약간의 시간 동안 같은 관리 디스크를 여러 개 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="f4874-106">또한 이 스크립트를 사용하여 데이터 VHD를 스냅숏으로 가져온 다음 스냅숏을 사용하여 약간의 시간 동안 관리 디스크를 여러 개 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f4874-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f4874-107">Sample script</span></span>

<span data-ttu-id="f4874-108">[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "VHD에서 스냅숏 만들기")]</span><span class="sxs-lookup"><span data-stu-id="f4874-108">[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="f4874-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f4874-109">Script explanation</span></span>

<span data-ttu-id="f4874-110">이 스크립트에서는 다음 명령을 사용하여 다른 구독의 VHD에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="f4874-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f4874-112">명령</span><span class="sxs-lookup"><span data-stu-id="f4874-112">Command</span></span> | <span data-ttu-id="f4874-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f4874-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f4874-114">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="f4874-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="f4874-115">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="f4874-116">저장소 형식, 위치, 부모 VHD가 저장된 저장소 계정의 리소스 ID 및 부모 VHD의 VHD URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="f4874-117">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="f4874-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="f4874-118">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4874-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4874-119">Next steps</span></span>

[<span data-ttu-id="f4874-120">스냅숏에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="f4874-120">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="f4874-121">관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="f4874-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f4874-122">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4874-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f4874-123">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4874-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>