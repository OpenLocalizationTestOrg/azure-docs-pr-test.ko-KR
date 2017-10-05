---
title: "Azure PowerShell 스크립트 샘플 - 관리 디스크를 OS 디스크로 연결하여 VM 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 관리 디스크를 OS 디스크로 연결하여 VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ec532811e94647c8a04b9faf9474f6749969f83e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="cea5a-103">PowerShell과 기존 관리 OS 디스크를 사용하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="cea5a-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="cea5a-104">이 스크립트는 기존 관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="cea5a-105">이전 시나리오에서는 이 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="cea5a-106">다른 구독의 관리 디스크에서 복사된 기존의 관리 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cea5a-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="cea5a-107">특수화된 VHD 파일에서 만든 기존 관리 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cea5a-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="cea5a-108">스냅숏에서 만든 기존의 관리 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cea5a-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cea5a-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="cea5a-109">Sample script</span></span>

<span data-ttu-id="cea5a-110">[!code-powershell[기본](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "스냅숏에서 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="cea5a-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="cea5a-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="cea5a-111">Clean up deployment</span></span> 

<span data-ttu-id="cea5a-112">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="cea5a-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="cea5a-113">Script explanation</span></span>

<span data-ttu-id="cea5a-114">이 스크립트는 다음 명령을 사용하여 관리 디스크 속성을 가져오고 관리 디스크를 새 VM에 연결하며 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="cea5a-115">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cea5a-116">명령</span><span class="sxs-lookup"><span data-stu-id="cea5a-116">Command</span></span> | <span data-ttu-id="cea5a-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="cea5a-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cea5a-118">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="cea5a-118">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="cea5a-119">디스크의 이름 및 리소스 그룹에 따라 디스크 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-119">Gets disk object based on the name and the resource group of a disk.</span></span> <span data-ttu-id="cea5a-120">반환된 디스크 개체의 Id 속성은 디스크를 새 VM에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-120">Id property of the returned disk object is used to attach the disk to a new VM</span></span> |
| [<span data-ttu-id="cea5a-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="cea5a-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="cea5a-122">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-122">Creates a VM configuration.</span></span> <span data-ttu-id="cea5a-123">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="cea5a-124">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="cea5a-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="cea5a-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="cea5a-126">디스크의 Id 속성을 사용하여 관리 디스크를 OS 디스크로 새 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-126">Attaches a managed disk using the Id property of the disk as OS disk to a new virtual machine</span></span> |
| [<span data-ttu-id="cea5a-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="cea5a-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="cea5a-128">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="cea5a-129">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="cea5a-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="cea5a-130">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="cea5a-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cea5a-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="cea5a-132">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-132">Create a virtual machine.</span></span> |
|[<span data-ttu-id="cea5a-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cea5a-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="cea5a-134">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cea5a-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cea5a-135">Next steps</span></span>

<span data-ttu-id="cea5a-136">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cea5a-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cea5a-137">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea5a-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>