---
title: "PowerShell 스크립트 샘플-aaaAzure 스냅숏에서 VM 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="3c0e9-103">PowerShell를 사용하여 스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="3c0e9-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="3c0e9-104">이 스크립트는 OS 디스크의 스냅숏에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3c0e9-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3c0e9-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3c0e9-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3c0e9-106">Clean up deployment</span></span> 

<span data-ttu-id="3c0e9-107">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3c0e9-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3c0e9-108">Script explanation</span></span>

<span data-ttu-id="3c0e9-109">이 스크립트 명령 tooget 스냅숏 속성 스냅숏에서 관리 되는 디스크를 만들 및 VM 만들기를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="3c0e9-110">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3c0e9-111">명령</span><span class="sxs-lookup"><span data-stu-id="3c0e9-111">Command</span></span> | <span data-ttu-id="3c0e9-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3c0e9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3c0e9-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="3c0e9-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="3c0e9-114">스냅숏 이름을 사용하여 스냅숏을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="3c0e9-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="3c0e9-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="3c0e9-116">디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-116">Creates a disk configuration.</span></span> <span data-ttu-id="3c0e9-117">이 구성은 hello 디스크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="3c0e9-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="3c0e9-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="3c0e9-119">관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="3c0e9-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="3c0e9-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="3c0e9-121">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-121">Creates a VM configuration.</span></span> <span data-ttu-id="3c0e9-122">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="3c0e9-123">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="3c0e9-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="3c0e9-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="3c0e9-125">OS 디스크 toohello 가상 컴퓨터로 hello 관리 되는 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="3c0e9-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="3c0e9-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="3c0e9-127">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="3c0e9-128">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="3c0e9-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="3c0e9-129">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="3c0e9-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="3c0e9-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="3c0e9-131">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="3c0e9-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3c0e9-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3c0e9-133">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c0e9-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c0e9-134">Next steps</span></span>

<span data-ttu-id="3c0e9-135">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3c0e9-136">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c0e9-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
