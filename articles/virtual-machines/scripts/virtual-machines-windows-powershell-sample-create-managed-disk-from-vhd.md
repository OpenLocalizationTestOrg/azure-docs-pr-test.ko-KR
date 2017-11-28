---
title: "Azure PowerShell 스크립트 샘플 - 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기"
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="a19c7-103">PowerShell을 사용하여 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="a19c7-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="a19c7-104">이 스크립트는 같은 구독 또는 다른 구독의 저장소 계정에 VHD 파일의 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="a19c7-105">이 스크립트를 사용하여 관리 OS 디스크에 특수화된(일반화/sysprep되지 않음) VHD를 가져와 가상 컴퓨터를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="a19c7-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="a19c7-106">또한 데이터 VHD를 관리되는 데이터 디스크로 가져오는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="a19c7-107">VHD 파일에서 단시간에 동일한 관리 디스크를 여러 개 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a19c7-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="a19c7-108">Vhd 파일에서 관리 디스크를 만들기 위해 vhd 파일에서 Blob 스냅숏이 만들어진 후 관리 디스크를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="a19c7-109">1분에 하나의 Blob 스냅숏만 만들 수 있으므로 제한으로 인해 디스크 생성 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="a19c7-110">이 제한을 피하려면 [vhd 파일에서 관리 스냅숏](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)을 만든 후 관리 스냅숏을 사용하여 단시간에 여러 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-110">To avoid this throttling, create a [managed snapshot from the vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a19c7-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a19c7-111">Sample script</span></span>

<span data-ttu-id="a19c7-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "VHD에서 관리 디스크 만들기")]</span><span class="sxs-lookup"><span data-stu-id="a19c7-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="a19c7-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a19c7-113">Script explanation</span></span>

<span data-ttu-id="a19c7-114">이 스크립트에서는 다음 명령을 사용하여 다른 구독의 VHD에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="a19c7-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a19c7-116">명령</span><span class="sxs-lookup"><span data-stu-id="a19c7-116">Command</span></span> | <span data-ttu-id="a19c7-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a19c7-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a19c7-118">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a19c7-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a19c7-119">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a19c7-120">저장소 형식, 위치, 부모 VHD가 저장된 저장소 계정의 리소스 ID, 부모 VHD의 VHD URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="a19c7-121">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a19c7-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a19c7-122">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a19c7-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a19c7-123">Next steps</span></span>

[<span data-ttu-id="a19c7-124">관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="a19c7-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a19c7-125">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a19c7-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a19c7-126">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a19c7-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>