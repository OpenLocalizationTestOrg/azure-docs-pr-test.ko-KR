---
title: "PowerShell 스크립트 샘플-aaaAzure WordPress | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b011726a772bb4d13fcfcba088eac4d0305967c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="0da2a-103">PowerShell로 WordPress VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0da2a-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="0da2a-104">이 스크립트는 가상 컴퓨터를 만들고 hello Azure 가상 컴퓨터 사용자 지정 스크립트 확장 tooinstall WordPress를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-104">This script creates a virtual machine and uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="0da2a-105">Hello 스크립트를 실행 한 후에 hello WordPress 구성 사이트에 액세스할 수 있습니다 `http://<public IP of VM>/wordpress`합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0da2a-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0da2a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0da2a-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0da2a-107">Clean up deployment</span></span> 

<span data-ttu-id="0da2a-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0da2a-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0da2a-109">Script explanation</span></span>

<span data-ttu-id="0da2a-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="0da2a-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0da2a-112">명령</span><span class="sxs-lookup"><span data-stu-id="0da2a-112">Command</span></span> | <span data-ttu-id="0da2a-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0da2a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0da2a-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0da2a-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0da2a-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0da2a-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0da2a-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0da2a-117">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-117">Creates a subnet configuration.</span></span> <span data-ttu-id="0da2a-118">이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="0da2a-119">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0da2a-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="0da2a-120">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="0da2a-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0da2a-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="0da2a-122">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="0da2a-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="0da2a-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="0da2a-124">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="0da2a-125">이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="0da2a-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="0da2a-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="0da2a-127">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="0da2a-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0da2a-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0da2a-129">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-129">Gets subnet information.</span></span> <span data-ttu-id="0da2a-130">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="0da2a-131">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0da2a-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="0da2a-132">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="0da2a-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="0da2a-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="0da2a-134">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-134">Creates a VM configuration.</span></span> <span data-ttu-id="0da2a-135">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="0da2a-136">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="0da2a-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0da2a-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="0da2a-138">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="0da2a-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="0da2a-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="0da2a-140">스크립트 tooinstall WordPress를 호출 하는 hello 사용자 지정 스크립트 확장 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-140">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
|[<span data-ttu-id="0da2a-141">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0da2a-141">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0da2a-142">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-142">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0da2a-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0da2a-143">Next steps</span></span>

<span data-ttu-id="0da2a-144">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-144">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0da2a-145">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0da2a-145">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
