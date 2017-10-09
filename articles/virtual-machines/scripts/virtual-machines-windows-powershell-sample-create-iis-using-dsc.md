---
title: "PowerShell 스크립트 샘플-aaaAzure dsc IIS | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - DSC를 사용하는 IIS"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: ef855bf92ef7b0fd07466527bc5f71f688e150fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="2ea01-103">PowerShell을 사용하여 IIS VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2ea01-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="2ea01-104">이 스크립트는 Windows Server 2016을 실행 하는 Azure 가상 컴퓨터 만들고 hello Azure 가상 컴퓨터 DSC 확장 tooinstall IIS를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine DSC Extension tooinstall IIS.</span></span> <span data-ttu-id="2ea01-105">Hello 스크립트를 실행 한 후 hello 기본 IIS 웹 사이트 hello hello 가상 컴퓨터의 공용 IP 주소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2ea01-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2ea01-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2ea01-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="2ea01-107">Clean up deployment</span></span> 

<span data-ttu-id="2ea01-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2ea01-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2ea01-109">Script explanation</span></span>

<span data-ttu-id="2ea01-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="2ea01-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2ea01-112">명령</span><span class="sxs-lookup"><span data-stu-id="2ea01-112">Command</span></span> | <span data-ttu-id="2ea01-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2ea01-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2ea01-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2ea01-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2ea01-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2ea01-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2ea01-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="2ea01-117">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-117">Creates a subnet configuration.</span></span> <span data-ttu-id="2ea01-118">이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="2ea01-119">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="2ea01-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="2ea01-120">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="2ea01-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="2ea01-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="2ea01-122">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="2ea01-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="2ea01-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="2ea01-124">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="2ea01-125">이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="2ea01-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="2ea01-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="2ea01-127">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="2ea01-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2ea01-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="2ea01-129">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-129">Gets subnet information.</span></span> <span data-ttu-id="2ea01-130">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="2ea01-131">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2ea01-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="2ea01-132">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="2ea01-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="2ea01-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="2ea01-134">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-134">Creates a VM configuration.</span></span> <span data-ttu-id="2ea01-135">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="2ea01-136">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="2ea01-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2ea01-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="2ea01-138">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="2ea01-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="2ea01-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="2ea01-140">VM 확장 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="2ea01-141">이 샘플에서 hello 사용자 지정 스크립트 확장 사용 되는 tooinstall IIS는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="2ea01-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2ea01-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2ea01-143">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2ea01-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ea01-144">Next steps</span></span>

<span data-ttu-id="2ea01-145">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2ea01-146">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea01-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
