---
title: "Azure PowerShell 스크립트 샘플 - Docker | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Docker"
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c8b700d13e4645d408e4e752a541e521ef93a6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-docker-host-with-powershell"></a><span data-ttu-id="5ddd8-103">PowerShell을 사용하여 Docker 호스트 만들기</span><span class="sxs-lookup"><span data-stu-id="5ddd8-103">Create a Docker host with PowerShell</span></span>

<span data-ttu-id="5ddd8-104">이 스크립트는 Docker를 사용하는 가상 컴퓨터를 만들고 컨테이너에서 NGINX를 실행하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-104">This script creates a virtual machine with Docker enabled and starts a container running NGINX.</span></span> <span data-ttu-id="5ddd8-105">스크립트를 실행한 후에 Azure Virtual Machine의 FQDN을 통해 NGINX 웹 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5ddd8-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5ddd8-106">Sample script</span></span>

<span data-ttu-id="5ddd8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Docker 호스트 만들기")]</span><span class="sxs-lookup"><span data-stu-id="5ddd8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Create Docker host")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5ddd8-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="5ddd8-108">Clean up deployment</span></span> 

<span data-ttu-id="5ddd8-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5ddd8-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5ddd8-110">Script explanation</span></span>

<span data-ttu-id="5ddd8-111">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5ddd8-112">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5ddd8-113">명령</span><span class="sxs-lookup"><span data-stu-id="5ddd8-113">Command</span></span> | <span data-ttu-id="5ddd8-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5ddd8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5ddd8-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5ddd8-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5ddd8-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5ddd8-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5ddd8-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5ddd8-118">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-118">Creates a subnet configuration.</span></span> <span data-ttu-id="5ddd8-119">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="5ddd8-120">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5ddd8-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5ddd8-121">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5ddd8-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5ddd8-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5ddd8-123">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5ddd8-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5ddd8-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5ddd8-125">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5ddd8-126">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="5ddd8-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5ddd8-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5ddd8-128">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="5ddd8-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5ddd8-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5ddd8-130">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-130">Gets subnet information.</span></span> <span data-ttu-id="5ddd8-131">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5ddd8-132">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5ddd8-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5ddd8-133">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="5ddd8-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5ddd8-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5ddd8-135">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-135">Creates a VM configuration.</span></span> <span data-ttu-id="5ddd8-136">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5ddd8-137">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5ddd8-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5ddd8-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5ddd8-139">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="5ddd8-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="5ddd8-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="5ddd8-141">가상 컴퓨터에 VM 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="5ddd8-142">이 샘플에서는 Docker를 구성하고 NGINX Docker 컨테이너를 실행하기 위해 Docker 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-142">In this sample, the Docker extension is used to configure Docker and run an NGINX Docker container.</span></span> |
|[<span data-ttu-id="5ddd8-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5ddd8-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5ddd8-144">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5ddd8-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ddd8-145">Next steps</span></span>

<span data-ttu-id="5ddd8-146">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5ddd8-147">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Linux VM 설명서](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-147">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
