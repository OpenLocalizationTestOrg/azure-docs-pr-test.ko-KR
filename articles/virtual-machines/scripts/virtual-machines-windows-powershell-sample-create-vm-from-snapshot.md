---
title: "Azure PowerShell 스크립트 샘플 - 스냅숏에서 VM 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 스냅숏에서 VM 만들기"
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
ms.openlocfilehash: 63d108bbfd0f58f8a40bf1c7c8649e3a1f7ed288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="72609-103">PowerShell를 사용하여 스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="72609-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="72609-104">이 스크립트는 OS 디스크의 스냅숏에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="72609-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="72609-105">Sample script</span></span>

<span data-ttu-id="72609-106">[!code-powershell[기본](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "관리 os 디스크에서 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="72609-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="72609-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="72609-107">Clean up deployment</span></span> 

<span data-ttu-id="72609-108">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72609-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="72609-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="72609-109">Script explanation</span></span>

<span data-ttu-id="72609-110">이 스크립트는 다음 명령을 사용하여 스냅숏 속성을 가져오고 스냅숏에서 관리 디스크를 만들며 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-110">This script uses the following commands to get snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="72609-111">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="72609-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="72609-112">명령</span><span class="sxs-lookup"><span data-stu-id="72609-112">Command</span></span> | <span data-ttu-id="72609-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="72609-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="72609-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="72609-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="72609-115">스냅숏 이름을 사용하여 스냅숏을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="72609-115">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="72609-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="72609-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="72609-117">디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-117">Creates a disk configuration.</span></span> <span data-ttu-id="72609-118">이 구성은 디스크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="72609-118">This configuration is used with the disk creation process.</span></span> |
| [<span data-ttu-id="72609-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="72609-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="72609-120">관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-120">Creates a managed disk.</span></span> |
| [<span data-ttu-id="72609-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="72609-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="72609-122">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-122">Creates a VM configuration.</span></span> <span data-ttu-id="72609-123">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="72609-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="72609-124">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="72609-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="72609-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="72609-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="72609-126">관리 디스크를 가상 컴퓨터에 OS 디스크로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="72609-126">Attaches the managed disk as OS disk to the virtual machine</span></span> |
| [<span data-ttu-id="72609-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="72609-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="72609-128">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="72609-129">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="72609-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="72609-130">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="72609-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="72609-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="72609-132">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72609-132">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="72609-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="72609-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="72609-134">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72609-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72609-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72609-135">Next steps</span></span>

<span data-ttu-id="72609-136">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72609-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="72609-137">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72609-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>