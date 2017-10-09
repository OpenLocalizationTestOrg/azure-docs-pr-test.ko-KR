---
title: "PowerShell 스크립트 샘플-aaaAzure 운영 체제 디스크와 관리 되는 디스크를 연결 하 여 VM 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="c2820-103">PowerShell과 기존 관리 OS 디스크를 사용하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c2820-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="c2820-104">이 스크립트는 기존 관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="c2820-105">이전 시나리오에서는 이 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="c2820-106">다른 구독의 관리 디스크에서 복사된 기존의 관리 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c2820-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="c2820-107">특수화된 VHD 파일에서 만든 기존 관리 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c2820-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="c2820-108">스냅숏에서 만든 기존의 관리 OS 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c2820-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c2820-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c2820-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c2820-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="c2820-110">Clean up deployment</span></span> 

<span data-ttu-id="c2820-111">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c2820-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c2820-112">Script explanation</span></span>

<span data-ttu-id="c2820-113">이 스크립트 명령 tooget 관리 되는 디스크 속성을 다음 hello를 사용 하 여, 관리 되는 디스크 tooa 연결 새 VM 및 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="c2820-114">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c2820-115">명령</span><span class="sxs-lookup"><span data-stu-id="c2820-115">Command</span></span> | <span data-ttu-id="c2820-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c2820-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c2820-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="c2820-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="c2820-118">Hello 이름 및 디스크의 hello 리소스 그룹에 따라 디스크 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="c2820-119">Hello의 id 속성 디스크 개체를 사용 하는 tooattach hello 디스크 tooa 반환 된 새 VM</span><span class="sxs-lookup"><span data-stu-id="c2820-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="c2820-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="c2820-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c2820-121">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-121">Creates a VM configuration.</span></span> <span data-ttu-id="c2820-122">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c2820-123">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c2820-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="c2820-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="c2820-125">OS 디스크 tooa 새 가상 컴퓨터로 hello 디스크의 hello Id 속성을 사용 하 여 관리 되는 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="c2820-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="c2820-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c2820-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c2820-127">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="c2820-128">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c2820-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c2820-129">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="c2820-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c2820-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c2820-131">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="c2820-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c2820-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c2820-133">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c2820-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2820-134">Next steps</span></span>

<span data-ttu-id="c2820-135">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c2820-136">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2820-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
